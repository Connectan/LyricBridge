# LyricBridge

[日本語](README.md) | [English](README.en.md) | [简体中文](README.zh-CN.md) | **繁體中文** | [한국어](README.ko.md)

![Android](https://img.shields.io/badge/Android-8.0%2B-3DDC84?logo=android&logoColor=white)
![Target](https://img.shields.io/badge/target-Android%2014%20(API%2034)-blue)
![Status](https://img.shields.io/badge/version-1.0-brightgreen)
![Spotify](https://img.shields.io/badge/for-Spotify-1DB954?logo=spotify&logoColor=white)
![Made with](https://img.shields.io/badge/Jetpack%20Compose-Kotlin-7F52FF?logo=kotlin&logoColor=white)

**一款跟著 Spotify 正在播放的歌曲，把即時同步的歌詞顯示在「通知」「島（Island）／狀態列」和「鎖定畫面」上的 Android App。**

它從 Spotify 的媒體工作階段讀取歌名、歌手和播放進度，自動在 [LRCLIB](https://lrclib.net) 上尋找歌詞，並持續顯示目前正在唱的那一行。
LRCLIB 上沒有的歌曲或裝置裡的本機歌曲，也可以手動指定自己準備的 `.lrc` 檔案。

---

## ⚠️ 必讀

- 這裡發布的 APK 是 **v1.0（正式版）**。套件名稱為 `com.connectan.lyricbridge`，是正式（release）版本，不是除錯版本。
- **只支援 Spotify（`com.spotify.music`）**。其他音樂 App 播放的歌曲不會顯示歌詞。
- 尋找歌詞時會使用網路（LRCLIB）。
- 不是透過 Google Play 發布的。使用風險請自行承擔。

---

## 下載

👉 **[從 Releases 下載 APK](https://github.com/Connectan/LyricBridge/releases/latest)**

| 項目 | 內容 |
|---|---|
| 檔名 | `LyricBridge_v1.0.apk` |
| 大小 | 約 16 MB |
| SHA-256 | `65376100c01eb1ebc82c2a42cdb130ca5e24abe662e0be97bf894bdf93b8d4ba` |

---

## 功能

| 功能 | 說明 |
|---|---|
| 自動顯示同步歌詞 | 在 Spotify 播放歌曲時，自動從 LRCLIB 尋找歌詞，並依播放進度逐行顯示。間奏和前奏顯示為「♪」 |
| 通知歌詞 | 顯示帶歌詞的媒體通知。上一首／播放暫停／下一首的操作會直接傳給 Spotify |
| 島／狀態列歌詞 | 把目前的歌詞放進 App 自己的媒體工作階段的「歌名」欄，所以在支援「島」（畫面頂端彈出顯示）的手機上會顯示歌詞。另有利用通知跑馬燈文字（ticker）的「狀態列歌詞（實驗）」 |
| 鎖定畫面全螢幕歌詞 | 在螢幕關閉或鎖定時開始播放，會自動開啟帶專輯封面的全螢幕歌詞。解鎖後會自動關閉 |
| 時間校正 | 覺得歌詞對不上時，可以以 ±100ms 為單位微調 |
| 使用自己的 LRC | 匯入裝置中的 `.lrc`／`.txt` 檔案並指定給歌曲（支援 UTF-8／Shift_JIS／GBK）。適合 LRCLIB 上沒有的歌或本機歌曲 |
| 歌詞預覽 | 在 App 畫面裡直接查看正在播放的歌曲和歌詞捲動 |
| 診斷記錄 | 可以查看、複製鎖定畫面啟動和播放控制的記錄，以及上次當機的詳細內容。方便排查問題 |

---

## 使用方式

1. 開啟 App，**允許** 畫面上要求的權限（點選未設定的項目會開啟系統授權畫面）
2. 在 Spotify 播放歌曲
3. 找到歌詞後，通知、島和 App 畫面上會開始捲動顯示歌詞
4. 想在鎖定畫面上自動顯示的話，在設定中開啟「ロック画面で自動表示」（鎖定畫面自動顯示）
5. 歌詞有偏差時，用「歌詞タイミング補正」（歌詞時間校正）調整

※ App 介面為日文，上面的設定名稱為翻譯。

---

## 需要的權限

| 權限 | 用途 |
|---|---|
| 通知存取權 | 取得 Spotify 的播放狀態和專輯封面，**必要** |
| 顯示通知（`POST_NOTIFICATIONS`） | 顯示帶歌詞的媒體通知和島 |
| 全螢幕通知（`USE_FULL_SCREEN_INTENT`） | 在鎖定畫面上自動顯示歌詞畫面（Android 14 以上需要授權） |
| 顯示在其他應用程式上層（`SYSTEM_ALERT_WINDOW`） | 鎖定時直接開啟歌詞畫面 |
| 忽略電池最佳化 | 防止 App 在背景待機時被結束 |
| 前景服務（媒體播放） | 在背景持續同步歌詞 |
| 網路（`INTERNET`） | 從 LRCLIB 尋找歌詞 |

> **Android 13 以上無法開啟「通知存取權」時**
> 不是從 Google Play 安裝的 App，這個權限可能會被當作「受限制的設定」擋下。
> 請到「設定」→「應用程式」→「LyricBridge」→ 右上角「⋮」→「**允許受限制的設定**」，然後再開啟一次。

> 在廠商客製系統（MIUI／HyperOS、ColorOS 等）上，如果沒有同時允許「背景彈出畫面」和「自動啟動」，鎖定畫面可能不會自動顯示歌詞。請在應用程式資訊畫面中允許。

---

## 安裝方式

1. 從 [Releases](https://github.com/Connectan/LyricBridge/releases/latest) 下載 APK
2. 點擊下載好的 APK
3. 如果出現「不明來源的應用程式」提示，請為瀏覽器（或檔案管理 App）開啟 **允許這個來源的應用程式**
4. 點「安裝」

> 由於不是從 Google Play 安裝，可能會出現 Play 安全防護的警告。遇到時請點「詳細資料」→「仍要安裝」。

---

## 運作環境

| 項目 | 內容 |
|---|---|
| Android | **8.0 以上**（API 26+） |
| 目標版本 | Android 14（API 34） |
| CPU | arm64-v8a / armeabi-v7a / x86 / x86_64 |
| 需要的 App | Spotify |

---

## 常見問題

**Q. 沒有顯示歌詞**
A. LRCLIB 上沒有收錄的歌曲找不到歌詞。這時請準備 `.lrc` 檔案，透過「この曲にLRCを割り当てる」（為這首歌指定 LRC）來指定。純音樂會顯示「インストゥルメンタル楽曲です」（純音樂）。

**Q. 歌詞有點對不上**
A. 可以用歌詞時間校正以 ±100ms 為單位調整。

**Q. 只有不帶時間資訊的歌詞**
A. 無法同步的歌詞會以「同期なし (通常歌詞)」（不同步，一般歌詞）的形式顯示全文。

**Q. Spotify 以外的 App 能用嗎？**
A. 不能。只支援 Spotify。

**Q. 鎖定畫面上沒有自動顯示**
A. 請在 App 的「鎖定畫面顯示準備狀況」確認全螢幕通知、顯示在其他應用程式上層、忽略電池最佳化都已允許。廠商客製系統可能還需要額外的權限（見上面的「需要的權限」）。

---

## 作者

**こねくたん（Connectan）**，又名 晓玲 清風
- 網站：https://connectan.github.io

深陷無技適中國手機坑的人。

---

## 注意

- 「Spotify」是 Spotify AB 的商標。本 App 是 **個人製作的非官方 App**，與 Spotify 無關。
- 歌詞資料來自 [LRCLIB](https://lrclib.net)。歌詞的著作權歸各權利人所有。
- 使用風險請自行承擔。
