# 时光印记（ShiGuang YinJi）

我的 Android 混合应用作品（简历项目）——一个基于腾讯 App 生成器 + Capacitor 构建的 H5 应用，Kotlin 原生壳包装 Web 前端。

> 安装包在右侧 [Releases](https://github.com/l-umos/shiguang-yinji/releases) 中下载。

## 应用简介

「时光印记」是一站式生活记录与成长陪伴应用，包含五年计划、统计看板、角色管理、情绪管理、AI 助手等模块。

![应用图标](icon.png)

## 功能页面

| 路由 | 页面 |
| --- | --- |
| `/` | 首页 |
| `/five-year` | 五年计划 |
| `/stats` | 统计看板 |
| `/characters` | 角色管理 |
| `/profile` | 个人中心 |
| `/mood-manage` | 情绪管理 |
| `/ai` | AI 助手 |
| `/ai-prefs` | AI 偏好设置 |
| `/settings` | 设置 |

## 安装方法

1. 前往 [Releases](https://github.com/l-umos/shiguang-yinji/releases) 下载 `shiguang-yinji.apk`
2. 在手机设置中允许「安装未知来源应用」
3. 打开 APK 安装，完成后即可使用

## 文件校验

`shiguang-yinji.apk` SHA-256：

```
B614AA80012A022ED3310A5CAE90CF5F08E66A5EBB6DF80E01ABD252151BD391
```

## 技术栈

- **Capacitor**：Android 混合应用壳
- **Kotlin / Java**：原生层（MainActivity / MainApplication）
- **WebView + H5**：Angular / Vite 构建产物（`assets/public`）
- **OkHttp**：网络请求层
- **PictureSelector**：图片选择与处理
- **腾讯 Aegis**：前端可观测性 SDK

## 构建说明

本应用使用腾讯「App 生成器」配置并导出，H5 运行时与部分 SDK 由腾讯提供；应用图标、页面配置、打包与发布由我完成。

## 后续计划

- 补充各页面截图
- 将核心页面重构为自研前端 / 原生组件
- 接入自建后端与真实 AI 服务
