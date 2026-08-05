# 时光印记 · 技术要点（TECH-NOTES）

给面试官 / 工程师看的拆包分析笔记，说明"这个 App 是怎么组成的、怎么调试、踩过哪些坑"。

## 1. 应用概况

| 项目 | 值 |
| --- | --- |
| 形态 | 混合应用（Capacitor 原生壳 + WebView 加载 H5） |
| 应用名 | 时光印记 |
| 包名 | `yyb.ai.y178577885095228c7d41ba89399cd` |
| 版本 | 1.0（versionCode 3） |
| 系统要求 | minSdk 23（Android 6.0+）/ targetSdk 35 |
| 关键权限 | 网络、录音、相册图片/视频读取 |

## 2. APK 结构（拆包看到什么）

APK 本质是 ZIP 包，解压后：

```
assets/               # H5 前端 + Capacitor 配置（capacitor.config.json）
  public/             #   Angular/Vite 构建产物：index.html、routes.json、JS bundle
res/                  # 编译后资源（文件名被混淆，如 8c.png）
AndroidManifest.xml   # 二进制格式清单（包名、权限、组件、图标资源 ID）
resources.arsc        # 资源表（资源 ID -> 文件/值）
classes*.dex          # 原生字节码
META-INF/             # 依赖版本信息
APK Signing Block     # v2/v3 签名（位于 ZIP 尾部的独立区块）
```

关键点：`res/` 文件名随机化，真实资源名要通过 `resources.arsc` 反向映射；`AndroidManifest.xml` 是二进制 XML（string pool + 元素/属性结构），需要专门解析。

## 3. 签名机制与安装坑

- 该 APK **只有 v2/v3 签名，没有 v1（JAR）签名**（META-INF 里没有 `.RSA/.SF/.MF`，但能检测到 `APK Sig Block 42` 魔数）。
- 影响：部分安装器 / 旧设备 / 聊天工具转发场景会报「安装包有问题」。
- 修复方向：
  1. 用 `apksigner` 补签 v1 + v2（Android build-tools 自带）；
  2. 或从 App Bundle（AAB）用 `bundletool` 生成 universal APK；
  3. 或走应用宝官方渠道导出可安装包。

## 4. 拆包分析方法（这套笔记怎么来的）

1. `ZipFile` 解压 APK，得到完整文件树；
2. 解析二进制 `AndroidManifest.xml`：读 string pool → 遍历 START_ELEMENT 节点 → 提取 `android:icon`（0x7F080000）、minSdk、targetSdk、权限、组件；
3. 解析 `resources.arsc`：类型表（anim/drawable/id/mipmap…）→ key 池（资源名，如 `ic_launcher_foreground`）→ 条目值；
4. 检测签名块魔数，判断 v2/v3 签名是否存在；
5. 用正则扫描拆包内容，确认没有硬编码密钥。

## 5. 想自己改这个 App，从哪下手

- **改界面 / 功能（推荐）**：改 `assets/public/` 下的 H5 代码（路由在 `routes.json`，入口 `index.html`，逻辑在 JS bundle），重新打包 + 重签名。
- **看原生逻辑**：用 [jadx](https://github.com/skylot/jadx) 打开 `classes.dex`，看 `MainActivity` / `MainApplication`。
- **看资源映射**：`resources.arsc` + `res/` 对应关系，可用 `aapt2 dump resources` 查看。
- **注意**：任何修改后都必须重新签名才能安装，否则会被拒绝。

## 6. 面试可以讲的技术点

- 混合应用原理：原生壳 ↔ WebView ↔ 原生桥（Capacitor native-bridge.js）
- APK 逆向流程：zip → 二进制 XML → 资源表 → dex
- 签名方案演进：v1 / v2 / v3 的差异与兼容性
- 安全意识：拆包代码不含密钥（已扫描确认）；生产环境凭据必须放服务端，客户端只做展示
