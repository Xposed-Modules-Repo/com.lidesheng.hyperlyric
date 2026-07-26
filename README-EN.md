<h1 align="center">HyperLyric</h1>

<p align="center">
  <strong>HyperOS HyperIsland Lyrics Enhancement & Notification Lyric Service</strong>
</p>

<p align="center">
  <a href="https://github.com/limczhh/HyperLyric/blob/main/LICENSE"><img src="https://img.shields.io/badge/License-GPL--3.0-blue.svg" alt="License GPL-3.0"/></a>
  <a href="https://android.com"><img src="https://img.shields.io/badge/Android-13.0%20--%2016-3DDC84.svg" alt="Android Support"/></a>
  <a href="https://github.com/compose-miuix-ui/miuix"><img src="https://img.shields.io/badge/UI--Framework-Miuix--Compose-0084FF.svg" alt="Miuix UI"/></a>
  <a href="https://github.com/libxposed/api"><img src="https://img.shields.io/badge/Hook--Framework-libxposed%20102-purple.svg" alt="libxposed"/></a>
  <a href="https://github.com/limczhh/HyperLyric/releases"><img src="https://img.shields.io/github/downloads/limczhh/HyperLyric/total?style=flat&color=orange" alt="Downloads"/></a>
</p>

<p align="center">
  <a href="https://qm.qq.com/q/5ZiRlGtvkQ"><img src="https://img.shields.io/badge/QQ%20Group-0084FF?style=flat&logo=qq&logoColor=white" alt="QQ Group"/></a>
  <a href="https://t.me/MiniLeaf"><img src="https://img.shields.io/badge/Telegram-26A5E4?style=flat&logo=telegram&logoColor=white" alt="Telegram"/></a>
</p>

<p align="center">
  <a href="README.md"><strong>简体中文</strong></a> | English
</p>

---

HyperLyric is a lyric display tool designed for Xiaomi HyperOS. It supports two modes: as an **Xposed module** injecting into SystemUI HyperIsland for word-by-word dynamic lyrics, or as a **standalone app** displaying lyrics via notification bar / Notification Spotlight — no root required.

---

## Operating Modes

### 1. Xposed Mode (SystemUI Process)
For rooted devices with an Xposed framework (e.g. LSPosed). HyperLyric injects into SystemUI plugins via Modern Xposed API (libxposed API 102):
- **View injection**: Intercepts `BaseDexClassLoader`, hooks into HyperIsland slots through `SystemUIHookRegistry`, and injects a custom Canvas lyric renderer (`RichLyricLineView`).
- **Runtime hot-reload**: Listens for preference changes via `OnSharedPreferenceChangeListener`. Style and animation updates take effect immediately without restarting SystemUI.

### 2. Standalone App Mode (App Process)
No root required. HyperLyric runs as a regular app and receives lyric data through the notification bar.

---


## Compatibility

> ⚠️ Plugin updates across systems and Android versions are frequent. Actual behavior depends on your specific device.

| Feature | Android | System | Notes |
| :--- | :--- | :--- | :--- |
| **HyperIsland Lyrics** | Android 15+ | HyperOS 3 | Requires injecting `miui.systemui.plugin` |
| **Remove Notification Spotlight Whitelist** | Android 13+ | HyperOS 2, HyperOS 3 | Intercepts `com.xiaomi.xmsf` |
| **Remove HyperIsland Pull-down Whitelist** | Android 16 | HyperOS 3.0.300+ | Bypasses pull-down expanded island restrictions |
| **Live Update Lyrics** | Android 16 | HyperOS 3.0.300+, ColorOS 16 | Uses standard Android Live Update notification API |
| **Notification Spotlight Lyrics** | Android 13+ | HyperOS 2, HyperOS 3 | Standalone app with Shizuku bypass |

---

## Lyric Sources

Lyric sources are decoupled from HyperLyric. All sources are dispatched through `RootLyricSink`.

| Source | How It Works | Compatible Players | Dependencies |
| :--- | :--- | :--- | :--- |
| **Lyricon** (`lyricon`) | Reads lyric data forwarded by the Lyricon status bar module. | NetEase Cloud Music, QQ Music, Kugou, etc. | Requires [Lyricon central](https://github.com/tomakino/lyricon/releases/tag/core) and [LyricProvider](https://github.com/proify/LyricProvider/releases) |
| **SuperLyric** (`superlyric`) | Retrieves word-level timestamped lyrics from SuperLyric. | Kuwo, QQ Music, Qishui, etc. | Requires [SuperLyric](https://github.com/HChenX/SuperLyric) with broadcast enabled |
| **LyricInfo** (`lyricinfo`) | Reads the lyricinfo field from MediaSession. | QQ Music, Salt Player, etc. | [LyricInfo](https://github.com/limczhh/LyricInfo) recommended (optional) |

---

## Screenshots

<table>
  <tr>
    <td><img src="https://github.com/limczhh/HyperLyric/blob/main/assets/001.webp?raw=true" width="300" alt="Screenshot 001"/></td>
    <td><img src="https://github.com/limczhh/HyperLyric/blob/main/assets/002.webp?raw=true" width="300" alt="Screenshot 002"/></td>
    <td><img src="https://github.com/limczhh/HyperLyric/blob/main/assets/003.webp?raw=true" width="300" alt="Screenshot 003"/></td>
  </tr>
  <tr>
    <td><img src="https://github.com/limczhh/HyperLyric/blob/main/assets/004.webp?raw=true" width="300" alt="Screenshot 004"/></td>
    <td><img src="https://github.com/limczhh/HyperLyric/blob/main/assets/005.webp?raw=true" width="300" alt="Screenshot 005"/></td>
    <td><img src="https://github.com/limczhh/HyperLyric/blob/main/assets/006.webp?raw=true" width="300" alt="Screenshot 006"/></td>
  </tr>
</table>

---

## Credits & License

- Licensed under **GNU General Public License v3.0**.
- Thanks to:
 - [miuix-kmp](https://github.com/compose-miuix-ui/miuix) — HyperOS-style Compose UI component library.
 - [lyricon](https://github.com/tomakino/lyricon) — Most lyric animations are ported from this project.
 - [SuperLyric](https://github.com/HChenX/SuperLyric)
 - [LyricInfo](https://github.com/limczhh/LyricInfo)
 - [libxposed](https://github.com/libxposed/api)
