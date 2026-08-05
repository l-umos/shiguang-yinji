# APK 拆包结构说明

本目录是 `shiguang-yinji.apk` 的解压内容，用于调试与学习。

## 目录说明

| 路径 | 说明 |
| --- | --- |
| `assets/public/` | H5 前端代码（Angular/Vite 构建产物），包含 `index.html`、`routes.json`、JS bundle，**主要调试对象** |
| `assets/capacitor.config.json` | Capacitor 配置（appId、appName、webDir） |
| `assets/capacitor.plugins.json` | 插件配置 |
| `AndroidManifest.xml` | 二进制格式的应用清单（包名、权限、组件），可用 `aapt dump xmltree` 或 jadx 查看 |
| `resources.arsc` | 编译后的资源表 |
| `classes.dex` | 原生代码字节码，用 [jadx](https://github.com/skylot/jadx) 反编译 |
| `res/` | 编译后的资源文件（文件名被混淆，如 `8c.png`），用 `aapt2` 或资源表可还原 |
| `META-INF/` | 依赖版本信息（v1 签名缺失，使用 v2/v3 签名，签名块位于 ZIP 的 APK Signing Block） |

## 调试建议

1. 前端逻辑：修改 `assets/public/` 中的代码（`index.html`、JS bundle），重新打包。
2. 原生逻辑：用 jadx 打开 `classes.dex` 查看 Kotlin/Java 代码。
3. 应用信息：
   - 应用名：时光印记
   - 包名：`yyb.ai.y178577885095228c7d41ba89399cd`
   - 版本：1.0（versionCode 3），minSdk 23 / targetSdk 35
   - 权限：网络、录音、相册图片/视频读取等

## 注意

- `res/` 中部分文件名在 Windows 上大小写冲突（APK 内存在仅大小写不同的条目），解压时已自动重命名以避免覆盖。
- 本 APK 使用 APK Signature Scheme v2/v3 签名，修改后重新打包需要用 `apksigner` 重新签名才能安装。
