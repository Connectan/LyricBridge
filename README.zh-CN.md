# LyricBridge

[日本語](README.md) | [English](README.en.md) | **简体中文** | [繁體中文](README.zh-TW.md) | [한국어](README.ko.md)

![Android](https://img.shields.io/badge/Android-8.0%2B-3DDC84?logo=android&logoColor=white)
![Target](https://img.shields.io/badge/target-Android%2014%20(API%2034)-blue)
![Status](https://img.shields.io/badge/version-1.0-brightgreen)
![Spotify](https://img.shields.io/badge/for-Spotify-1DB954?logo=spotify&logoColor=white)
![Made with](https://img.shields.io/badge/Jetpack%20Compose-Kotlin-7F52FF?logo=kotlin&logoColor=white)

**一款跟随 Spotify 正在播放的歌曲，把实时同步的歌词显示在“通知”“岛（Island）／状态栏”和“锁屏”上的 Android 应用。**

它从 Spotify 的媒体会话中读取歌名、歌手和播放进度，自动在 [LRCLIB](https://lrclib.net) 上查找歌词，并持续显示当前正在唱的那一行。
对于 LRCLIB 上没有的歌曲或设备里的本地歌曲，也可以手动指定自己准备的 `.lrc` 文件。

---

## ⚠️ 必读

- 这里发布的 APK 是 **v1.0（正式版）**。包名为 `com.connectan.lyricbridge`，是正式（release）版本，不是调试版本。
- **只支持 Spotify（`com.spotify.music`）**。其他音乐应用播放的歌曲不会显示歌词。
- 查找歌词时会使用网络（LRCLIB）。
- 不是通过 Google Play 发布的。使用风险请自行承担。

---

## 下载

👉 **[从 Releases 下载 APK](https://github.com/Connectan/LyricBridge/releases/latest)**

| 项目 | 内容 |
|---|---|
| 文件名 | `LyricBridge_v1.0.apk` |
| 大小 | 约 16 MB |
| SHA-256 | `65376100c01eb1ebc82c2a42cdb130ca5e24abe662e0be97bf894bdf93b8d4ba` |

---

## 功能

| 功能 | 说明 |
|---|---|
| 自动显示同步歌词 | 在 Spotify 播放歌曲时，自动从 LRCLIB 查找歌词，并按播放进度逐行显示。间奏和前奏显示为“♪” |
| 通知栏歌词 | 显示带歌词的媒体通知。上一首／播放暂停／下一首的操作会直接传给 Spotify |
| 岛／状态栏歌词 | 把当前歌词放进应用自己的媒体会话的“歌名”栏，所以在支持“岛”（屏幕顶部弹出显示）的手机上会显示歌词。另有利用通知滚动文字（ticker）的“状态栏歌词（实验）” |
| 锁屏全屏歌词 | 在息屏或锁屏状态下开始播放时，自动打开带专辑封面的全屏歌词。解锁后会自动关闭 |
| 时间校正 | 觉得歌词对不上时，可以按 ±100ms 微调 |
| 使用自己的 LRC | 导入设备里的 `.lrc`／`.txt` 文件并指定给歌曲（支持 UTF-8／Shift_JIS／GBK）。适合 LRCLIB 上没有的歌或本地歌曲 |
| 歌词预览 | 在应用界面里直接查看正在播放的歌曲和歌词滚动 |
| 诊断日志 | 可以查看、复制锁屏启动和播放控制的记录，以及上次崩溃的详情。方便排查问题 |

---

## 使用方法

1. 打开应用，**允许** 界面上要求的权限（点未设置的项目会打开系统授权界面）
2. 在 Spotify 播放歌曲
3. 找到歌词后，通知、岛和应用界面上会开始滚动显示歌词
4. 想在锁屏上自动显示的话，在设置中打开“ロック画面で自動表示”（锁屏自动显示）
5. 歌词有偏差时，用“歌詞タイミング補正”（歌词时间校正）调整

※ 应用界面为日语，上面的设置名称为翻译。

---

## 需要的权限

| 权限 | 用途 |
|---|---|
| 通知使用权 | 获取 Spotify 的播放状态和专辑封面，**必需** |
| 显示通知（`POST_NOTIFICATIONS`） | 显示带歌词的媒体通知和岛 |
| 全屏通知（`USE_FULL_SCREEN_INTENT`） | 在锁屏上自动显示歌词界面（Android 14 及以上需要授权） |
| 显示在其他应用上层（`SYSTEM_ALERT_WINDOW`） | 锁屏时直接打开歌词界面 |
| 忽略电池优化 | 防止应用在后台待机时被结束 |
| 前台服务（媒体播放） | 在后台持续同步歌词 |
| 网络（`INTERNET`） | 从 LRCLIB 查找歌词 |

> **Android 13 及以上无法开启“通知使用权”时**
> 不是从 Google Play 安装的应用，这个权限可能会被当作“受限设置”拦截。
> 请进入“设置”→“应用”→“LyricBridge”→ 右上角“⋮”→“**允许受限制的设置**”，然后再开启一次。

> 在厂商定制系统（MIUI／HyperOS、ColorOS 等）上，如果不同时允许“后台弹出界面”和“自启动”，锁屏可能不会自动显示歌词。请在应用信息界面中允许。

---

## 安装方法

1. 从 [Releases](https://github.com/Connectan/LyricBridge/releases/latest) 下载 APK
2. 点击下载好的 APK
3. 如果提示“未知来源应用”，为浏览器（或文件管理器）打开 **允许来自此来源的应用**
4. 点“安装”

> 由于不是从 Google Play 安装，可能会出现 Play 保护机制的警告。遇到时请点“详细信息”→“仍然安装”。

---

## 运行环境

| 项目 | 内容 |
|---|---|
| Android | **8.0 及以上**（API 26+） |
| 目标版本 | Android 14（API 34） |
| CPU | arm64-v8a / armeabi-v7a / x86 / x86_64 |
| 需要的应用 | Spotify |

---

## 常见问题

**Q. 没有显示歌词**
A. LRCLIB 上没有收录的歌曲找不到歌词。这种情况请准备 `.lrc` 文件，通过“この曲にLRCを割り当てる”（为这首歌指定 LRC）来指定。纯音乐会显示“インストゥルメンタル楽曲です”（纯音乐）。

**Q. 歌词有点对不上**
A. 可以用歌词时间校正按 ±100ms 调整。

**Q. 只有不带时间信息的歌词**
A. 无法同步的歌词会以“同期なし (通常歌詞)”（不同步，普通歌词）的形式显示全文。

**Q. Spotify 以外的应用能用吗？**
A. 不能。只支持 Spotify。

**Q. 锁屏上没有自动显示**
A. 请在应用的“锁屏显示准备状况”里确认全屏通知、显示在其他应用上层、忽略电池优化都已允许。厂商定制系统可能还需要额外的权限（见上面的“需要的权限”）。

---

## 作者

**こねくたん（Connectan）**，又名 晓玲 清風
- 网站：https://connectan.github.io

深陷无技适国产手机坑的人。

---

## 注意

- “Spotify”是 Spotify AB 的商标。本应用是 **个人制作的非官方应用**，与 Spotify 无关。
- 歌词数据来自 [LRCLIB](https://lrclib.net)。歌词的著作权归各权利人所有。
- 使用风险请自行承担。
