# LyricBridge

[日本語](README.md) | **English** | [简体中文](README.zh-CN.md) | [繁體中文](README.zh-TW.md) | [한국어](README.ko.md)

![Android](https://img.shields.io/badge/Android-8.0%2B-3DDC84?logo=android&logoColor=white)
![Target](https://img.shields.io/badge/target-Android%2014%20(API%2034)-blue)
![Status](https://img.shields.io/badge/version-1.0-brightgreen)
![Spotify](https://img.shields.io/badge/for-Spotify-1DB954?logo=spotify&logoColor=white)
![Made with](https://img.shields.io/badge/Jetpack%20Compose-Kotlin-7F52FF?logo=kotlin&logoColor=white)

**An Android app that shows real-time synced lyrics for whatever's playing on Spotify, in your notifications, the Island / status bar, and on the lock screen.**

It reads the song title, artist, and playback position from Spotify's media session. It finds the lyrics on [LRCLIB](https://lrclib.net) automatically and keeps showing the line being sung right now.
For songs LRCLIB doesn't have, or songs stored on your device, you can assign your own `.lrc` file.

---

## ⚠️ Read this first

- The APK here is **v1.0 (official release)**. The package name is `com.connectan.lyricbridge`, and it's a release build, not a debug build.
- It works with **Spotify (`com.spotify.music`) only**. Songs from other music apps won't get lyrics.
- It uses the internet (LRCLIB) to find lyrics.
- It's distributed outside Google Play. Use at your own risk.

---

## Download

👉 **[Download the APK from Releases](https://github.com/Connectan/LyricBridge/releases/latest)**

| Item | Details |
|---|---|
| File name | `LyricBridge_v1.0.apk` |
| Size | About 16 MB |
| SHA-256 | `65376100c01eb1ebc82c2a42cdb130ca5e24abe662e0be97bf894bdf93b8d4ba` |

---

## Features

| Feature | Details |
|---|---|
| Synced lyrics, automatically | When you play a song on Spotify, it finds the lyrics on LRCLIB and shows them line by line, matched to the playback position. Instrumental breaks and intros show as "♪" |
| Lyrics in the notification | Shows a media notification with the lyrics. Previous / play-pause / next are passed straight to Spotify |
| Island / status bar lyrics | It puts the current lyric line in the "title" field of its own media session, so phones with an Island (the pop-up display at the top of the screen) show the lyrics there. There's also an experimental "status bar lyrics" mode that uses the notification ticker text |
| Full-screen lyrics on the lock screen | When playback starts while the screen is off or locked, it opens full-screen lyrics with the album art automatically. It closes by itself when you unlock |
| Timing adjustment | If the lyrics feel off, fine-tune them in ±100ms steps |
| Use your own LRC files | Import `.lrc` / `.txt` files from your device and assign them to songs (UTF-8 / Shift_JIS / GBK supported). Handy for songs LRCLIB doesn't have, or local songs |
| Lyrics preview | See the current song and the lyrics as they play, right in the app |
| Diagnostic log | View and copy the history of lock-screen launches and playback controls, plus details of the last crash. Useful for finding out why something doesn't work |

---

## How to use

1. Open the app and **allow the permissions** it asks for (tap any item that isn't set up to open the permission screen)
2. Play a song on Spotify
3. Once lyrics are found, they start scrolling in the notification, the Island, and the app
4. To show lyrics on the lock screen automatically, turn on "ロック画面で自動表示" (show automatically on the lock screen) in the settings
5. If the lyrics are off, adjust them with "歌詞タイミング補正" (lyrics timing adjustment)

\* The app's screens are in Japanese. The setting names above are translated.

---

## Permissions

| Permission | What it's for |
|---|---|
| Notification access | **Required** to get Spotify's playback state and album art |
| Show notifications (`POST_NOTIFICATIONS`) | For the media notification with lyrics and the Island display |
| Full-screen notifications (`USE_FULL_SCREEN_INTENT`) | To open the lyrics screen on the lock screen automatically (needs permission on Android 14+) |
| Display over other apps (`SYSTEM_ALERT_WINDOW`) | To open the lyrics screen directly while the screen is locked |
| Ignore battery optimization | So the app isn't killed while waiting in the background |
| Foreground service (media playback) | To keep syncing lyrics in the background |
| Internet (`INTERNET`) | To find lyrics on LRCLIB |

> **Can't turn on "Notification access" on Android 13+?**
> Apps installed from outside Google Play can have this permission blocked as a "restricted setting".
> Go to Settings → Apps → LyricBridge → "⋮" in the top right → "**Allow restricted settings**", then try turning it on again.

> On manufacturer ROMs (MIUI / HyperOS, ColorOS, etc.), lyrics may not appear on the lock screen automatically unless you also allow "display pop-up windows while running in the background" and "autostart". Allow them from the app info screen.

---

## How to install

1. Download the APK from [Releases](https://github.com/Connectan/LyricBridge/releases/latest)
2. Tap the downloaded APK
3. If you are asked about "unknown apps", turn on **Allow from this source** for your browser (or file manager)
4. Tap "Install"

> Because this is installed from outside Google Play, Play Protect may show a warning. If it does, tap "More details" → "Install anyway".

---

## Requirements

| Item | Details |
|---|---|
| Android | **8.0 or later** (API 26+) |
| Target | Android 14 (API 34) |
| CPU | arm64-v8a / armeabi-v7a / x86 / x86_64 |
| Required app | Spotify |

---

## FAQ

**Q. No lyrics show up**
A. Songs that aren't on LRCLIB won't have lyrics. In that case, get an `.lrc` file and assign it with "この曲にLRCを割り当てる" (assign an LRC to this song). Instrumental tracks show "インストゥルメンタル楽曲です" (instrumental track).

**Q. The lyrics are slightly off**
A. Adjust them in ±100ms steps with the lyrics timing adjustment.

**Q. The only lyrics available have no timing info**
A. Lyrics that can't be synced are shown in full as "同期なし (通常歌詞)" (not synced, plain lyrics).

**Q. Does it work with apps other than Spotify?**
A. No. It's Spotify only.

**Q. Lyrics don't appear on the lock screen automatically**
A. Check in the app's lock-screen readiness section that full-screen notifications, display over other apps, and battery optimization exemption are all allowed. Manufacturer ROMs may need extra permissions (see "Permissions" above).

---

## Author

**Connectan (こねくたん)**, also known as 晓玲 清風
- Website: https://connectan.github.io

Lives deep in the rabbit hole of Chinese phones without Japanese certification.

---

## Notes

- "Spotify" is a trademark of Spotify AB. This is an **unofficial app made by an individual**. It is not affiliated with Spotify.
- Lyrics data comes from [LRCLIB](https://lrclib.net). Lyrics are copyrighted by their respective owners.
- Use at your own risk.
