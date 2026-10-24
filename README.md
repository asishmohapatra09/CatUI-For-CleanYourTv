# CatUI For CleanYourTV 📺🍎

> Transform your Android TV, Google TV, or realme TV Stick into a clean, ad-free, Apple TV-style streaming experience. Free up to 350+ MB of RAM, eliminate background telemetry, and take full control of your TV home screen.

[![Mobile Companion APK](https://img.shields.io/badge/Download_Phone_App-APK__V1.0-E50914?style=for-the-badge&logo=android&logoColor=white)](https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/APK_V1.0/CatUI-TV-Cleaner.apk)
[![TV Launcher APK](https://img.shields.io/badge/Download_TV_Launcher-Public__V1.0-007AFF?style=for-the-badge&logo=apple&logoColor=white)](https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/Public_V1.0/CatUI-v2.3.apk)
[![GitHub Release](https://img.shields.io/github/v/release/asishmohapatra09/CatUI-For-CleanYourTv?color=blue&logo=github)](https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases)
[![License](https://img.shields.io/badge/License-Apache_2.0-green.svg)](LICENSE)

---

## 📥 Direct Downloads

| Target Device | Package / Role | Version | Direct Download Link |
| :--- | :--- | :--- | :--- |
| 📱 **Android Phone / Tablet** | **CatUI TV Cleaner** *(Companion App)* | `v0.3.3` (Build 6) | [Download CatUI-TV-Cleaner.apk](https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/APK_V1.0/CatUI-TV-Cleaner.apk) *(~25.4 MB)* |
| 📺 **Android TV / Stick / Box** | **CatUI Standalone Launcher** *(TV Home)* | `v2.3` | [Download CatUI-v2.3.apk](https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/Public_V1.0/CatUI-v2.3.apk) *(~7.3 MB)* |

- **Companion App Package ID:** `com.asish.cleanyourtv`
- **TV Launcher Package ID:** `com.asish.catui`
- **Companion App SHA-256:** `A0F85AE01F3761667EB9BA679CE779DEE878370BF86D652937E4C755D28950A4`

---

## ⚡ Choose Your Setup Method

| Method | Requirements | Ease of Use | Estimated Time |
| :--- | :--- | :--- | :--- |
| **[Method 1: CatUI TV Cleaner Mobile App](#-method-1-catui-tv-cleaner-mobile-app-recommended)** | Android phone or tablet on the same Wi-Fi (No PC required) | 🟢 1-Tap from phone | ~2 minutes |
| **[Method 2: AI / LLM Terminal Setup](#-method-2-ai--llm-coding-assistant-prompt-pc--mac)** | PC / Mac with LLM (Claude Code, Antigravity, Cursor) | 🟡 Interactive CLI | ~5 minutes |

---

## 📱 Method 1: CatUI TV Cleaner Mobile App (Recommended)

Set up and debloat your TV directly from your Android phone without opening a terminal or connecting USB cables.

### 🌟 Key Features
- **No PC or Cables Needed**: Connects to your TV over local Wi-Fi via ADB.
- **Pre-bundled CatUI Launcher**: Automatically installs and sets **CatUI v2.3** (`com.asish.catui`) as the default TV home screen.
- **Native realme TV Stick Profile**: Built-in support for realme 4K TV Stick (`HP47DX2` / `BOS`) running Android 14. Eliminates the "We haven't met this exact TV" warning banner and safely debloats 15 background bloatware and telemetry packages.
- **Complete Home Button Takeover**: Automatically disables both `com.google.android.apps.tv.launcherx` and `com.google.android.tvlauncher` so pressing Home on your TV remote always opens CatUI.
- **Integrated RAM Usage Monitor**: Measures active memory usage via `/proc/meminfo` before and after debloating, displaying the net RAM freed on your TV.
- **Automatic Dock Sync**: Syncs your preferred TV apps directly into CatUI's bottom dock config (`/sdcard/Android/data/com.asish.catui/files/config.json`).
- **Launcher Selector & Custom UI Downloader**: Easily switch between CatUI, CleanYourTV Minimal, or paste a custom APK link from GitHub/web.
- **Wide TV Compatibility**: Works with Google TV, realme, Xiaomi/Mi TV, TCL, Hisense, Sony, OnePlus, Philips, Motorola, and generic Android TV boxes.

### 🚀 Step-by-Step Guide

#### Step 1: Enable Developer Options & USB Debugging on Your TV
1. On your TV, navigate to **Settings ⚙️ → Device Preferences (or System) → About**.
2. Scroll down to **Android TV OS build** (or **Build**) and press the remote's **OK button 7 times** until you see *"You are now a developer!"*.
3. Go back one level to **System / Device Preferences → Developer options**.
4. Enable **USB debugging** (and **Network / Wireless debugging** if present).
5. Ensure your TV and Android phone are connected to the same Wi-Fi network.

#### Step 2: Run CatUI TV Cleaner on Your Phone
1. Download and install [`CatUI-TV-Cleaner.apk`](https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/APK_V1.0/CatUI-TV-Cleaner.apk) on your Android phone.
2. Open the app. It will scan your local network and display your TV. Tap **Connect**.
3. Look at your TV screen: a prompt titled *"Allow USB debugging?"* will appear. Check **"Always allow from this computer"** and select **OK**.
4. Review the debloat plan and selected launcher (CatUI). Tap **Make it clean**.
5. The app will sideload CatUI, disable background bloatware, configure the remote Home button, and show your **RAM freed** statistics!

---

## ⚠️ Known Bugs in APK & Workarounds

Please read this section if you plan to switch between multiple launchers or test different UIs:

### 🐛 Bug 1: Switching from CleanYourTV Minimal Back to CatUI Gets Stuck
- **The Issue:** If you install CatUI, then switch to CleanYourTV Minimal, and later try switching back to CatUI, the companion app may retain the previous selection in its cached state. As a result, the TV might remain on CleanYourTV Minimal or fail to switch back to CatUI.
- **Workaround:**
  1. On your Android phone, go to **Settings → Apps → CatUI TV Cleaner → Storage & Cache → Clear Storage (Clear Data)**.
  2. Re-open **CatUI TV Cleaner**, reconnect to your TV, and select **CatUI**. The app will perform a fresh takeover and apply CatUI as default.
  3. *(Alternatively, tap **Restore Point / Undo** inside the app before switching launchers).*

### 🐛 Bug 2: Unused Launcher APKs Are Not Automatically Uninstalled
- **The Issue:** When you switch between CatUI and CleanYourTV Minimal (or install a custom UI via URL), the app disables the old launcher and enables the new one, but it does **not** automatically run `pm uninstall` on the old launcher APK. Both APKs remain on the TV storage.
- **Workaround:**
  - If you want to free up TV storage by removing the unused launcher:
    - **On your TV:** Go to **Settings ⚙️ → Apps → See all apps**, find the unused launcher (e.g. *CleanYourTV Minimal* or *CatUI*), and select **Uninstall**.
    - **Via ADB:** Run `adb shell pm uninstall com.gathin.tvhome` (to remove Minimal) or `adb shell pm uninstall com.asish.catui` (to remove CatUI).

> [!NOTE]
> **Upcoming Fix:** A dedicated **Launcher Manager** module will be added in the next release. It will separate UI switching into an independent screen outside the debloating workflow and include an option to cleanly uninstall old launchers automatically.

---

## 💻 Method 2: AI / LLM Coding Assistant Prompt (PC / Mac)

If you prefer using an AI assistant (such as **Claude Code**, **Google Antigravity**, **Cursor**, or any terminal agent with ADB access) from a PC/Mac connected to the same Wi-Fi:

### 📋 Copy & Paste This Prompt

```markdown
I want to debloat my Android TV and replace its launcher with a clean Apple TV-style home screen.
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
- Disable stock Google TV launchers: com.google.android.apps.tv.launcherx and com.google.android.tvlauncher.
- Disable manufacturer telemetry daemons and recommendation row providers.
- Keep Voice Assistant, Chromecast Built-in, Remote Pairing, and Google Play Store intact.
- Sideload CatUI v2.3 launcher (https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/Public_V1.0/CatUI-v2.3.apk) and set it as default home.
- Query /proc/meminfo before and after to verify memory freed.
```

---

## 🛡️ realme TV Stick Safe Debloat List

Tested and verified on the realme 4K TV Stick (`HP47DX2` / `BOS` running Android 14):

### 🚫 Safely Disabled Packages (Fully Reversible)

| Package Name | Description | Reason Disabled |
| :--- | :--- | :--- |
| `com.google.android.apps.tv.launcherx` | Google TV Home Launcher | Replaced by clean CatUI interface |
| `com.google.android.tvlauncher` | Stock Android TV Launcher Stub | Disabled to prevent fallback to stock UI |
| `com.google.android.videos` | Google Play Movies & TV | Replaced by direct app streaming |
| `com.google.android.play.games` | Google Play Games TV | Background sync and gaming services |
| `com.google.android.tvrecommendations` | Leanback Recommendation Channels | Background ad feeds and recommendation banners |
| `com.google.android.feedback` | Feedback & Crash Reporter | Continuous telemetry reporting |
| `com.google.android.partnersetup` | Partner Setup Service | OEM telemetry and initial setup stubs |
| `com.sdt.producttest` | Factory Production Test | Diagnostic hardware daemon |
| `com.sdt.vendor` | Vendor Daemon | Unused background vendor daemon |
| `com.oem.qa` | OEM QA Testing Daemon | Diagnostic logging agent |
| `com.oemservice` | OEM Telemetry Service | Background telemetry agent |
| `com.skyworth.smallclient` | Skyworth Client Daemon | Telemetry service |
| `com.skyworth.superservice` | Skyworth Super Service | Diagnostic daemon |
| `com.homwee.howtocast` | How-to-Cast Demo | Unused tutorial residual |
| `com.netflix.tokenmanager` | Netflix Token Manager | Unused vendor residual |
| `com.sdt.customization` | SDT Customization Overlay | Unused vendor UI customization |

### 🔒 Essential Packages Kept 100% Intact

- 🎙️ **Google Assistant** (`com.google.android.katniss`) — Remote mic button and voice search work perfectly.
- 📡 **Chromecast Built-in** (`com.google.android.apps.mediashell`) — Casting video/audio from phone or PC works as normal.
- 🔄 **System Updates & OTA** (`com.sdt.upgrade`, `com.sdt.ota`) — Firmware and security patches continue working.
- 🎧 **Hardware & Audio** — Dolby Audio (`com.dolby.android.audio.service`) and Bluetooth Remote Pairing (`com.mft.rcupair`).
- 🛒 **Store & Play Services** — Google Play Store (`com.android.vending`) and Google Play Services.

---

## 🔄 Restoring Stock Google TV Launcher

If you ever want to return to the default Google TV interface:

### Option A: From the Phone App
- In **CatUI TV Cleaner**, open the Launcher Selector menu and tap **Restore Stock TV Home Screen** (or tap **Undo / Restore** on the main dashboard).

### Option B: Via ADB Terminal
```bash
adb shell pm enable --user 0 com.google.android.apps.tv.launcherx
adb shell pm enable --user 0 com.google.android.tvlauncher
adb shell cmd package set-home-activity --user 0 com.google.android.apps.tv.launcherx/.home.HomeActivity
```

---

## ❓ Frequently Asked Questions

<details>
<summary><b>How does CatUI know my location for weather without me typing it?</b></summary>
<br>
CatUI requests the standard Android location permission (<code>ACCESS_FINE_LOCATION</code>). It queries Android TV's system location provider, which resolves your approximate coordinates using your Wi-Fi network's gateway and BSSID router signature. CatUI then calls the free Open-Meteo API (<code>https://api.open-meteo.com/v1/forecast</code>) with those coordinates, and uses Android's built-in Geocoder service to display your city name automatically.
</details>

<details>
<summary><b>Will this void my TV warranty or prevent system updates?</b></summary>
<br>
No. The debloating process only disables packages in user space (<code>pm disable-user</code>) and does not root or unlock the bootloader. System OTA updates (<code>com.sdt.upgrade</code> and <code>com.sdt.ota</code>) are intentionally preserved and will continue to work.
</details>

---

## 🙏 Credits & Acknowledgments

- **CleanYourTV App Concept:** Sincere thanks and credit to [udhaykumarbala/cleanyourtv-app](https://github.com/udhaykumarbala/cleanyourtv-app) for the open-source companion app architecture and design concepts.
- **CleanYourTv Concept:** Sincere thanks and credit to Gathin23 (https://github.com/Gathin23/cleanyourtv)
- **CatUI Launcher:** Credit to the CatUI project for the sleek Apple TV-style interface.
- **Maintained & Enhanced By:** [Asish Mohapatra](https://github.com/asishmohapatra09)

---

## ⚖️ License

Distributed under the Apache 2.0 License. See [LICENSE](LICENSE) for details.
