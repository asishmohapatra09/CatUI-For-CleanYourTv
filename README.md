# CatUI For CleanYourTV 📺🍎

> Transform your Android TV, Google TV, or realme TV Stick into a clean, ad-free, Apple TV-style streaming experience. Free up to 350+ MB of RAM, eliminate background telemetry, and take control of your TV home screen.

[![Direct APK Download](https://img.shields.io/badge/Download_APK-APK__V1.0-E50914?style=for-the-badge&logo=android&logoColor=white)](https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/APK_V1.0/CatUI-TV-Cleaner.apk)
[![GitHub Release](https://img.shields.io/github/v/release/asishmohapatra09/CatUI-For-CleanYourTv?color=blue&logo=github)](https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases)
[![License](https://img.shields.io/badge/License-Apache_2.0-green.svg)](LICENSE)
[![Android](https://img.shields.io/badge/Platform-Android%20TV%20%7C%20Google%20TV-3DDC84.svg?logo=android)](https://developer.android.com/tv)

---

## ⚡ Choose Your Setup Method

| Method | Requirements | Ease of Use | Time |
| :--- | :--- | :--- | :--- |
| **[Method 1: CatUI TV Cleaner APK](#-method-1-catui-tv-cleaner-companion-app-recommended)** | Android Smartphone only (No PC required) | 🟢 1-Tap from phone | ~2 mins |
| **[Method 2: LLM / Terminal Setup](#-method-2-ai--llm-coding-assistant-prompt-pc--mac)** | PC / Mac with LLM (Claude Code, Antigravity) | 🟡 Interactive CLI | ~5 mins |

---

## 📱 Method 1: CatUI TV Cleaner Companion App (Recommended)

Run everything directly from your Android phone without needing a computer or typing ADB commands.

### 🌟 App Highlights
- **No PC Required**: Installs and controls everything directly from your Android smartphone over local Wi-Fi.
- **Apple TV-Style Launcher Bundled**: Comes preloaded with **CatUI v2.3** (`com.asish.catui`) as the default home screen.
- **Native realme TV Stick Profile**: Built-in tested profile for realme TV Sticks (`HP47DX2` / `sdt`) that disables 15 verified background bloat and telemetry packages while keeping Voice Assistant, Chromecast, and Bluetooth remote pairing 100% intact.
- **Real-Time RAM Usage Monitor**: Measures active memory usage via `/proc/meminfo` before and after debloating, displaying the exact net RAM freed on the completion screen.
- **Multi-Launcher Selector**: Easily switch between **CatUI (Apple TV style)** and **CleanYourTV Minimal** directly within the Customise sheet.
- **Safe Unknown TV Fallback**: If your TV model does not have a dedicated profile, the app performs a non-destructive probe and offers an interactive checklist of recommendation apps rather than giving up.
- **Android 14 Compatibility**: Automatic push-to-temp sideloading fallback so package installation never hangs waiting for on-screen confirmations.
- **130+ TV Brands Supported**: Fully compatible with Xiaomi, TCL, Hisense, Sony, OnePlus, Philips, Panasonic, XGIMI, and generic Android TV sets.

### 📥 Download APK

[![Download CatUI TV Cleaner](https://img.shields.io/badge/⬇️_Download-CatUI_TV_Cleaner_APK-2ea44f?style=for-the-badge&logo=android&logoColor=white)](https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/APK_V1.0/CatUI-TV-Cleaner.apk)

- **Direct Download Link:** [`CatUI-TV-Cleaner.apk`](https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/APK_V1.0/CatUI-TV-Cleaner.apk) *(~25.1 MB)*
- **GitHub Release Page:** [APK_V1.0 Release](https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/tag/APK_V1.0)
- **Application ID:** `com.asish.cleanyourtv`
- **Minimum Phone OS:** Android 8.0+
- **SHA-256:** `1AD02D490C0BE6804608C3C77DE588C2968FFB9522508C0C6F470401E19A4296`

### 🚀 Step-by-Step Instructions

#### 1. Enable ADB on your TV
1. On your TV, go to **Settings → Device Preferences (or System) → About**.
2. Scroll to **Build** and press **OK 7 times** until you see *"You are now a developer!"*.
3. Go back one screen → **Developer options**.
4. Turn **ON** **USB debugging** (and **Network / Wireless debugging** if listed).
5. Ensure your TV and Android phone are connected to the same Wi-Fi network.

#### 2. Clean & Install
1. Open **CatUI TV Cleaner** on your Android phone.
2. The app will automatically scan and detect your TV on your local network. Tap **Connect**.
3. A prompt saying *"Allow USB debugging?"* will appear on your TV screen — check **"Always allow from this computer"** and select **OK**.
4. Review the planned debloat packages and default CatUI launcher. Tap **Make it clean**.
5. Once complete, view the **RAM Usage Monitor** card to see the RAM freed on your TV!

---

## 💻 Method 2: AI / LLM Coding Assistant Prompt (PC / Mac)

If you prefer using an AI coding assistant (such as **Claude Code**, **Google Antigravity**, **Cursor**, or any terminal agent with ADB access) on a computer connected to the same Wi-Fi:

### 📋 Paste This Prompt Into Your Assistant

```markdown
I want to debloat my Android TV and replace its launcher with a clean Apple TV style home screen.
My TV model is: <ENTER YOUR TV MODEL HERE>. Work on the real device, step by step, and verify everything you
do with screenshots pulled from the TV. Ask me before anything that depends on my preferences.

Connect
- Find the TV on my network (hostname, ARP table, or ask me for the IP) and connect over ADB on port 5555.
- If port 5555 stays closed, check Wireless debugging pairing (adb pair, adb connect).
- Tell me when the "Allow USB debugging?" prompt will appear on the TV so I can accept it.
- If `adb install` hangs on Android 14, push the APK to /data/local/tmp and run `pm install -r` over the shell.

Back up first
- Save the full package list, disabled-package list, getprop output and settings to a backup folder.
- Generate a restore script that re-enables everything you disable.

Debloat & Setup
- Disable stock launcher, telemetry daemons, and recommendation row providers.
- Keep Voice Assistant, Chromecast Built-in, Remote Pairing, and Google Play Store intact.
- Sideload CatUI v2.3 launcher (com.asish.catui) and set it as default home.
- Query /proc/meminfo before and after to verify memory freed.
```

---

## 🛡️ realme TV Stick Safe Debloat List

Tested extensively on realme 4K TV Stick (`HP47DX2` running Android 14):

### 🚫 Disabled Packages (Reversible)
| Package | Description | Reason Disabled |
| :--- | :--- | :--- |
| `com.google.android.tvlauncher` | Stock Android TV Launcher | Replaced by clean CatUI |
| `com.google.android.videos` | Google Play Movies & TV | Ads & preloaded content |
| `com.google.android.play.games` | Google Play Games TV | Background sync service |
| `com.google.android.tvrecommendations` | Leanback Recommendation Channels | Background ad banners |
| `com.google.android.feedback` | Bug & Feedback Provider | Telemetry reporting |
| `com.google.android.partnersetup` | Partner Setup Service | Manufacturer telemetry |
| `com.sdt.producttest` | Factory Production Test | Diagnostic daemon |
| `com.sdt.vendor` | Vendor Daemon | Unused vendor service |
| `com.oem.qa` | OEM QA Testing Daemon | Diagnostic logging |
| `com.oemservice` | OEM Telemetry Service | Background telemetry |
| `com.skyworth.smallclient` | Skyworth Client Daemon | Telemetry service |
| `com.skyworth.superservice` | Skyworth Super Service | Diagnostic daemon |
| `com.homwee.howtocast` | How-to-Cast Demo | Unused tutorial residual |
| `com.netflix.tokenmanager` | Netflix Token Manager | Unused vendor residual |
| `com.sdt.customization` | SDT Customization Overlay | Unused overlay |

### 🔒 Kept 100% Intact
- 🎙️ **Google Assistant** (`com.google.android.katniss`) — Mic button works as normal.
- 📡 **Chromecast Built-in** (`com.google.android.apps.mediashell`) — Casting from phone/PC works flawlessly.
- 🔄 **System Updates & OTA** (`com.sdt.upgrade`, `com.sdt.ota`) — Firmware updates remain intact.
- 🎧 **Audio & Hardware** — Dolby Audio (`com.dolby.android.audio.service`) and Bluetooth Remote (`com.mft.rcupair`).
- 🛒 **Store & Core Framework** — Google Play Store (`com.android.vending`) & Google Play Services.

---

## 🔄 Reversing Changes / Restoring Stock

To revert all changes and restore the default stock launcher at any time:
- In the **CatUI TV Cleaner** app: Tap **Undo / Restore** from the menu.
- Or via ADB from your computer:
  ```bash
  adb shell pm enable --user 0 com.google.android.tvlauncher
  ```

---

## 🙏 Credits & Acknowledgments

- **CleanYourTV App Concept:** Special thanks and credit to [udhaykumarbala/cleanyourtv-app](https://github.com/udhaykumarbala/cleanyourtv-app/releases) for the open-source companion app architecture and design concepts.
- **CatUI Launcher:** Credit to the CatUI team for the Apple TV-style interface.
- **Maintained By:** [Asish Mohapatra](https://github.com/asishmohapatra09)

---

## ⚖️ License

Distributed under the Apache 2.0 License. See `LICENSE` for more details.
