<h1 align="center">HyperLyric</h1>

<p align="center">
  <strong>HyperOS 超级岛歌词增强 & 通知歌词服务</strong>
</p>

<p align="center">
  <a href="https://github.com/limczhh/HyperLyric/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-GPL--3.0-blue.svg" alt="License GPL-3.0"/></a>
  <a href="https://android.com"><img src="https://img.shields.io/badge/Android-13.0%20--%2016-3DDC84.svg" alt="Android Support"/></a>
  <a href="https://github.com/compose-miuix-ui/miuix"><img src="https://img.shields.io/badge/UI--Framework-Miuix--Compose-0084FF.svg" alt="Miuix UI"/></a>
  <a href="https://github.com/libxposed/api"><img src="https://img.shields.io/badge/Hook--Framework-libxposed%20102-purple.svg" alt="libxposed"/></a>
  <a href="https://github.com/limczhh/HyperLyric/releases"><img src="https://img.shields.io/github/downloads/limczhh/HyperLyric/total?style=flat&color=orange" alt="Downloads"/></a>
</p>

<p align="center">
  <a href="https://qm.qq.com/q/5ZiRlGtvkQ"><img src="https://img.shields.io/badge/QQ 交流群-0084FF?style=flat&logo=qq&logoColor=white" alt="QQ Group"/></a>
  <a href="https://t.me/MiniLeaf"><img src="https://img.shields.io/badge/Telegram 频道-26A5E4?style=flat&logo=telegram&logoColor=white" alt="Telegram"/></a>
</p>

<p align="center">
  简体中文 | <a href="README-EN.md"><strong>English</strong></a>
</p>

---

HyperLyric 是一款专为小米 HyperOS 设计的歌词显示工具。支持两种运行方式：以 **Xposed 模块** 注入 SystemUI 超级岛，提供逐字动态歌词；或作为 **独立应用** 通过通知栏/焦点通知显示歌词，无需 Root。

---

## 运行模式

### 1. Xposed 模式 (SystemUI 进程)
适用于已 Root 且启用了 Xposed 框架（如 LSPosed）的设备。HyperLyric 通过 Modern Xposed API (libxposed API 102) 注入 SystemUI 插件：
- **视图注入**：拦截 `BaseDexClassLoader`，经 `SystemUIHookRegistry` 统一入口挂钩超级岛插槽，注入自定义 Canvas 歌词渲染器（`RichLyricLineView`）。
- **运行时热更新**：通过 `OnSharedPreferenceChangeListener` 监听偏好变动，样式与动效修改无需重启 SystemUI 即可生效。

### 2. 独立应用模式 (App 进程)
无需 Root。HyperLyric 作为普通应用运行，通过通知栏接收歌词数据。

---


## 兼容性

> ⚠️ 各系统与安卓版本的插件更新频繁，实际效果以具体设备为准。

| 功能 | Android 版本 | 系统版本 | 说明 |
| :--- | :--- | :--- | :--- |
| **超级岛歌词** | Android 15+ | HyperOS 3 | 需注入 `miui.systemui.plugin` |
| **移除焦点通知白名单** | Android 13+ | HyperOS 2、HyperOS 3 | 拦截 `com.xiaomi.xmsf` 进行判定 |
| **移除超级岛下拉白名单** | Android 16 | HyperOS 3.0.300+ | 突破下拉扩展岛的使用限制 |
| **实时通知歌词** | Android 16 | HyperOS 3.0.300+、ColorOS 16 | 通过标准 Android 实时通知接口推送 |
| **焦点通知歌词** | Android 13+ | HyperOS 2、HyperOS 3 | 独立应用配合 Shizuku 绕过发送限制 |

---

## 歌词源

歌词来源与 HyperLyric 解耦，所有源均通过 `RootLyricSink` 统一分发。

| 歌词源 | 原理 | 适用播放器 | 依赖 |
| :--- | :--- | :--- | :--- |
| **Lyricon** (`lyricon`) | 读取词幕状态栏歌词模块转发的歌词数据。 | 网易云音乐、QQ音乐、酷狗等 | 需安装 [Lyricon central](https://github.com/tomakino/lyricon/releases/tag/core) 及对应 [LyricProvider](https://github.com/proify/LyricProvider/releases) |
| **SuperLyric** (`superlyric`) | 获取 SuperLyric 的逐字时间戳歌词。 | 酷我音乐、QQ音乐、汽水音乐等 | 需安装 [SuperLyric](https://github.com/HChenX/SuperLyric) 并开启广播 |
| **LyricInfo** (`lyricinfo`) | 读取 MediaSession 中的 lyricinfo 字段。 | QQ音乐、Salt Player 等 | 建议安装 [LyricInfo](https://github.com/limczhh/LyricInfo)（可选） |

---

## 截图

<table>
  <tr>
    <td><img src="https://github.com/limczhh/HyperLyric/blob/main/assets/001.webp?raw=true" width="300" alt="截图 001"/></td>
    <td><img src="https://github.com/limczhh/HyperLyric/blob/main/assets/002.webp?raw=true" width="300" alt="截图 002"/></td>
    <td><img src="https://github.com/limczhh/HyperLyric/blob/main/assets/003.webp?raw=true" width="300" alt="截图 003"/></td>
  </tr>
  <tr>
    <td><img src="https://github.com/limczhh/HyperLyric/blob/main/assets/004.webp?raw=true" width="300" alt="截图 004"/></td>
    <td><img src="https://github.com/limczhh/HyperLyric/blob/main/assets/005.webp?raw=true" width="300" alt="截图 005"/></td>
    <td><img src="https://github.com/limczhh/HyperLyric/blob/main/assets/006.webp?raw=true" width="300" alt="截图 006"/></td>
  </tr>
</table>

---

## 致谢与协议

- 采用 **GNU General Public License v3.0** 开源协议。
- 感谢以下项目：
 - [miuix-kmp](https://github.com/compose-miuix-ui/miuix) — HyperOS 风格的 Compose 组件库。
 - [lyricon](https://github.com/tomakino/lyricon) — 大部分歌词动画移植自此项目。
 - [SuperLyric](https://github.com/HChenX/SuperLyric)
 - [LyricInfo](https://github.com/limczhh/LyricInfo)
 - [libxposed](https://github.com/libxposed/api)
