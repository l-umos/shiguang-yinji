# 时光印记（ShiGuang YinJi）

我的 Android 应用作品（简历项目）——一款基于 Capacitor 的混合应用：Kotlin 原生壳 + H5 前端，开箱即用。

> 📦 安装包在右侧 [Releases](https://github.com/l-umos/shiguang-yinji/releases) 中下载。

## 应用截图

| | | | |
| :-: | :-: | :-: | :-: |
| <img src="screenshots/screenshot-1.jpg" width="200" alt="截图1"> | <img src="screenshots/screenshot-2.jpg" width="200" alt="截图2"> | <img src="screenshots/screenshot-3.jpg" width="200" alt="截图3"> | <img src="screenshots/screenshot-4.jpg" width="200" alt="截图4"> |

## ✨ 功能特性

- 🗓️ **五年计划**：把长期目标拆成可执行的年度 / 月度安排
- 📊 **统计看板**：记录坚持数据，直观看到自己的成长轨迹
- 🎭 **角色管理**：用不同角色视角记录生活与思考
- 💬 **情绪管理**：随手记录心情，发现情绪变化的规律
- 🤖 **AI 助手**：智能问答与陪伴，可个性化配置偏好
- ⚙️ **个人设置**：主题、AI 偏好、应用信息一应俱全

## 🚀 快速安装

1. 用手机浏览器打开 [Releases](https://github.com/l-umos/shiguang-yinji/releases) 下载 `shiguang-yinji.apk`
2. 在手机设置里允许「安装未知来源应用」
3. 点击安装，打开即可使用

> ⚠️ 小提示：不要用微信等聊天工具转发 APK——聊天工具容易损坏文件或触发安装拦截，直接从 GitHub 下载最稳妥。

## 📦 拆包代码

这个仓库还放了 APK 的拆包内容（`apk-extracted/`），方便自己研究、调试：

- `assets/public/`：H5 前端代码（Angular / Vite 产物，主要调试对象）
- `AndroidManifest.xml` / `resources.arsc` / `classes.dex`：原生部分
- `APK-STRUCTURE.md`：目录结构讲解

更深入的技术分析（APK 结构、签名机制、反编译方法等）见 [TECH-NOTES.md](TECH-NOTES.md)。

## 🧰 技术栈

Capacitor · Kotlin · WebView · OkHttp · PictureSelector · 腾讯 Aegis

## 📌 说明

本应用使用腾讯「App 生成器」配置并导出，H5 运行时与部分 SDK 由腾讯提供；应用图标、页面配置、打包与发布由我完成。应用名「时光印记」，包名 `yyb.ai.y178577885095228c7d41ba89399cd`，版本 1.0（versionCode 3）。

## 🔮 后续计划

- 将核心页面重构为自研前端 / 原生组件
- 接入自建后端与真实 AI 服务
- 修复图标资源命名，提供一键打包脚本

---

作者 [@l-umos](https://github.com/l-umos) · 简历作品项目
