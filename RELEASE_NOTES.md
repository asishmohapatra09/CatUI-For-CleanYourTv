# Release v1.0.0 — CatUI TV Cleaner: Apple TV Style Home & Debloater

**CatUI TV Cleaner** (`com.asish.cleanyourtv`) is a complete, phone-based companion app to debloat your Android TV / Google TV and install the clean, ad-free Apple TV-style **CatUI** launcher in just a few taps — no computer or terminal needed!

---

### 📦 Assets & Verification
- **Direct Download:** [CatUI-TV-Cleaner.apk](https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/APK_V1.0/CatUI-TV-Cleaner.apk)
- **Tag:** `APK_V1.0`
- **Application ID:** `com.asish.cleanyourtv`
- **Version:** `0.3.3` (Build 6)
- **File Size:** `25.1 MB` (`25,119,503 bytes`)
- **SHA-256 Checksum:** `1AD02D490C0BE6804608C3C77DE588C2968FFB9522508C0C6F470401E19A4296`

---

### 🚀 What's New in this Release

- 🍏 **CatUI v2.3 Pre-bundled as Default Launcher**: Comes preloaded with the clean Apple TV-style CatUI launcher (`com.asish.catui`). Automatically installed and set as the default home screen.
- 📱 **CatUI Dock Apps Supported**: Config overlay pushes `config.json` directly into CatUI's directory (`/sdcard/Android/data/com.asish.catui/files/config.json`) and restarts CatUI so your selected dock apps appear immediately.
- 🔄 **Bidirectional Launcher Switching**: Switch seamlessly between **CatUI (Apple TV)** and **CleanYourTV Minimal** (or back) at any time. The app cleanly disables the inactive launcher and sets the selected launcher as the default HOME component.
- 🌐 **Custom UI / GitHub Release APK Download**: Added an interactive Launcher Picker sheet where you can select bundled launchers or paste any custom APK download link / GitHub release URL to install other launchers.
- 🎨 **Adaptive Customise Menu**: The "Look: Default" theme row is automatically hidden when CatUI is active, displaying only for CleanYourTV Minimal.
- 📺 **Native realme TV Stick Exact Profile**: 
  - Matched on `model = "TV Stick"`, `device = "BOS"`, `brand = "realme"`, `manufacturer = "SkyworthDigital"`.
  - Permanently eliminates the *"We haven't met this exact TV before"* warning banner.
  - Debloats 15 verified background bloat and telemetry packages while keeping Voice Assistant, Chromecast Built-in, Dolby Audio, Bluetooth remote pairing, and Play Store 100% intact.
- 📊 **Real-Time RAM Usage Monitor**:
  - Automatically queries `/proc/meminfo` before and after debloating.
  - Displays a dedicated badge on the **Done** screen:  
    `RAM Usage Monitor: Before: 1240 MB ➔ Now: 890 MB (350 MB Freed!)`
- 🔌 **Keep Debugging On by Default**: Prevents the TV from dropping ADB connection after setup completes.
- 🔁 **One-Tap Reconnect & Retry**: Tap the top status chip or the offline banner button to instantly reconnect to the TV without restarting the app.

---

### 📲 How to Install & Use
1. Download **`CatUI-TV-Cleaner.apk`** below to your Android phone.
2. Ensure both your phone and TV are connected to the same Wi-Fi network.
3. Open the app, tap **Connect** to detect your TV, and accept the ADB debugging prompt on your TV screen.
4. Review the planned debloat list and launcher. Tap **Make it clean**!

---

### 🙏 Credits
- Companion app concept and architecture based on [udhaykumarbala/cleanyourtv-app](https://github.com/udhaykumarbala/cleanyourtv-app/releases).
- CatUI TV Cleaner maintained by [Asish Mohapatra](https://github.com/asishmohapatra09).
