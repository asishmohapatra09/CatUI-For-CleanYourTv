# Release v1.0.0 — CatUI TV Cleaner: Apple TV Style Home & Debloater

**CatUI TV Cleaner** (`com.asish.cleanyourtv`) is a complete, phone-based companion app to debloat your Android TV / Google TV and install the clean, ad-free Apple TV-style **CatUI** launcher in just a few taps — no computer or terminal needed!

---

### 📦 Assets & Verification
- **Direct Download:** [CatUI-TV-Cleaner.apk](https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/APK_V1.0/CatUI-TV-Cleaner.apk)
- **Tag:** `APK_V1.0`
- **Application ID:** `com.asish.cleanyourtv`
- **Version:** `0.3.3` (Build 6)
- **File Size:** `24.8 MB` (`24,866,549 bytes`)
- **SHA-256 Checksum:** `2F23898F4171DB64F96C781BC63DC7750BAD797FC876339C51ABB455287E0C43`

---

### 🚀 What's New in this Release

- 🍏 **CatUI v2.3 Pre-bundled as Default Launcher**: Comes preloaded with the clean Apple TV-style CatUI launcher (`com.asish.catui`). Zero setup required — automatically installed and set as the default home screen.
- 📺 **Native realme TV Stick Profile (`realmeSureSet`)**: 
  - Full automatic detection for realme 4K TV Stick (`HP47DX2` / `sdt`).
  - Safely disables **15 background bloat and telemetry packages** (Play Movies & TV, Play Games, recommendation channels, factory test daemons, and residual telemetry).
  - Preserves Google Assistant, Chromecast Built-in, Dolby Audio, Bluetooth remote pairing, and Play Store 100% intact.
- 📊 **Real-Time RAM Usage Monitor**:
  - Automatically queries `/proc/meminfo` before and after debloating.
  - Displays a dedicated badge on the **Done** screen:  
    `RAM Usage Monitor: Before: 1240 MB ➔ Now: 890 MB (350 MB Freed!)`
- 🎛️ **Multi-Launcher Selector**:
  - Choose between **CatUI (Apple TV)** and **CleanYourTV Minimal** directly within the Customise sheet.
- 🛡️ **Intelligent Unknown TV Fallback**:
  - Unprofiled TV models no longer show an empty screen; instead, non-core preloaded apps and Google recommendation channels are presented in an interactive review checklist (`GroupDefault.ASK`) with system packages strictly protected.
- ⚡ **Android 14 Push-to-Temp Compatibility**:
  - Implemented automatic local push to `/data/local/tmp` followed by `pm install -r` to avoid streaming install hangs on Android 14.

---

### 📲 How to Install & Use
1. Download **`CatUI-TV-Cleaner.apk`** below to your Android phone.
2. Ensure both your phone and TV are connected to the same Wi-Fi network.
3. Open the app, tap **Connect** to detect your TV, and accept the ADB debugging prompt on your TV screen.
4. Review the planned debloat list and tap **Make it clean**!

---

### 🙏 Credits
- Companion app concept and architecture based on [udhaykumarbala/cleanyourtv-app](https://github.com/udhaykumarbala/cleanyourtv-app/releases).
- Maintained by [Asish Mohapatra](https://github.com/asishmohapatra09).
