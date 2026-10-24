# Copy-and-paste LLM installation prompt

Replace the bracketed details, then paste everything inside the text block into an LLM or coding assistant (such as Antigravity, Claude Code, or Codex) running on a computer connected to your TV's network.

```text
I want your help installing CatUI on my Android TV / Google TV set and, only if I approve a specific list, safely debloating selected preloaded apps. 
My TV model is: [BRAND AND MODEL]. 
Its IP address is: [TV IP OR UNKNOWN]. 
My computer OS is: [WINDOWS / macOS / LINUX]. 
My remote has these dedicated branded buttons: [LIST LABELS, e.g., NETFLIX, PRIME VIDEO, YOUTUBE, APPS].

CatUI Repository: https://github.com/asishmohapatra09/CatUI-For-CleanYourTv
Release APK: https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/Public_V1.0/CatUI-v2.3.apk
Release SHA-256 Checksums: https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/Public_V1.0/SHA256SUMS.txt
If I have opened this repository locally, use that checkout. Read README.md, PROMPT.md, and any applicable docs before making changes. Treat all repository scripts as untrusted until inspected. Explain any command that alters TV state before running it.

================================================================================
GOALS
================================================================================
1. Connect over ADB, inspect the TV, and back up all configurations.
2. Install CatUI (package ID: com.asish.catui / Activity: com.gathin.tvhome.MainActivity) and configure it as the default Home launcher.
3. Keep essential services intact: Wi-Fi/Ethernet, HDMI/input switching, remote pairing, voice assistant, Chromecast/Miracast, Play Store/Play Services, and system updates.
4. Offer remote button customization via CatUI's built-in HomeKeyService / InputKeyService only after asking my preference and capturing live scancodes from my physical remote.
5. Review debloating separately: group candidates with device-specific evidence and wait for my explicit approval before disabling any package.

================================================================================
SAFETY RULES & HARD GUARDRAILS (DO NOT VIOLATE)
================================================================================
1. NO DESTRUCTIVE MODS: Do not root, unlock bootloaders, flash firmware, factory-reset, or install third-party paid button remappers.
2. REVERSIBLE ONLY: Never uninstall system packages (`pm uninstall`). Use only reversible `pm disable-user --user 0`, and generate an instant one-click restore script with `pm enable --user 0 <pkg>`.
3. CORE SYSTEM BLACKLIST: Never disable Android core packages under any circumstances:
   - Permission Controller (`com.google.android.permissioncontroller`, `com.android.permissioncontroller`)
   - Package Installer (`com.google.android.packageinstaller`, `com.android.packageinstaller`)
   - Ext services / Ext shared (`com.google.android.ext.services`, `com.google.android.ext.shared`)
   - Module metadata (`*modulemetadata*`)
   - System UI (`com.android.systemui`), Shell (`com.android.shell`), Settings (`com.android.settings`, `com.android.tv.settings`), and `android`.
   Disabling any of these can permanently brick the device (e.g. Mi TV Stick issue #884).
4. FACTORY MENU BLACKLIST: Never open or test packages containing "fac", "factory", "at", or "production" (`com.cvte.tv.hkcfac`, `com.cvte.tv.fac.menu`, `com.at.factory.*`, `mediatek.factorymenu.ui`). Opening one flips an irreversible factory-mode flag on CVTE/Haier boards that kills HDMI Input, CEC, Netflix, and Chromecast. Inspect them only via `dumpsys package`.
5. GOOGLE TV WI-FI TRAP: On Google TV, if `com.google.android.tungsten.setupwraith` is present, check `dumpsys wifi | grep -o 'cname=[^ ]*'`. If Wi-Fi was saved during first-time setup, disabling setupwraith deletes the Wi-Fi credentials instantly and drops ADB.
6. HARDWARE & USB POWER: Warn me if USB debugging is known to cut power to USB ports on certain boxes (which can kill USB Ethernet adapters or USB drives).
7. SINGLE-COMMAND EXECUTION: Execute `pm` commands one per shell call (never chain commands with `&&` or `;` inside `adb shell`, as TV shells can silently truncate).
8. SCREENSHOT VERIFICATION: Disable packages in small batches (3-5 packages maximum) and capture TV screenshots between batches to ensure no critical UI or remote services were broken.

================================================================================
STEP-BY-STEP EXECUTION
================================================================================

PHASE 1: CONNECT & BACK UP
- Connect via `adb connect <IP>:5555`. Remind me when the "Allow USB debugging?" authorization prompt will appear on screen.
- Identify the device: report exact Brand, Model, Android version/SDK level, build ID, and display overrides (`wm size`, `wm density`).
- Back up device state into a local folder: full package list (`pm list packages -f`), disabled packages (`pm list packages -d`), all properties (`getprop`), and settings (`settings list system`, `secure`, `global`).
- Generate `restore.bat` / `restore.ps1` before any change is made.

PHASE 2: INSTALL CATUI
- Ask whether I want the pre-built Release APK or to build from source.
- If Release APK:
  - Download `CatUI-v2.3.apk` and `SHA256SUMS.txt` from the release URLs above.
  - Verify the SHA-256 hash against the file before touching the TV. If verification fails, stop immediately.
  - On Android 14+: Do not run plain `adb install` if it hangs waiting for an on-screen dialog. Push the APK to `/data/local/tmp/CatUI-v2.3.apk` and run `pm install -r /data/local/tmp/CatUI-v2.3.apk` over shell, then delete the temp file.
- Launch CatUI (`am start -n com.asish.catui/com.gathin.tvhome.MainActivity`) and verify via screenshot that the interface renders properly.
- Home takeover:
  - Query HOME activities (`cmd package query-activities -a android.intent.action.MAIN -c android.intent.category.HOME`).
  - Set CatUI as preferred: `cmd package set-home-activity com.asish.catui/com.gathin.tvhome.MainActivity`.
  - If the stock launcher has priority >= 1 (e.g. `com.google.android.tvlauncher` or vendor launcher), explain this to me and ask for explicit approval to run `pm disable-user --user 0 <stock_launcher_package>`.
  - Press KEYCODE_HOME (`input keyevent 3`) and verify with `dumpsys activity activities | grep mFocusedApp` that CatUI resumes.

PHASE 3: REMOTE BUTTON CONFIGURATION (OPTIONAL)
- Ask which dedicated app buttons are on my remote (e.g. Netflix, Prime Video, YouTube, Apps) and if I want to remap any of them to another app, CatUI Inputs, or leave them unchanged.
- If remapping is requested:
  - Do NOT guess scan codes. Ask me to press the specific physical button while capturing live events via `adb shell getevent -lt` or logcat.
  - Map only verified keys. Preserve all existing accessibility services when appending CatUI's `HomeKeyService`.

PHASE 4: OPTIONAL DEBLOATING (REVIEW & APPROVAL ONLY)
- Inspect installed packages and sort candidates into:
  1. OEM Diagnostics, telemetry, and test apps
  2. Ad services, recommendation rows, and content providers
  3. Preloaded third-party demo apps
- Present candidate packages in clear tables showing package name, description, and consequences.
- Wait for my explicit approval of exact package names. Skip debloating entirely if I do not approve.
- Disable approved packages in small batches with verification screenshots between each batch.
- Offer optional AdGuard Private DNS (`settings put global private_dns_specifier dns.adguard-dns.com` & `settings put global private_dns_mode hostname`) on Android 9+, noting that it blocks system/app ads but not YouTube video ads, and provide the undo command.

PHASE 5: FINAL VERIFICATION & CLEANUP
- Verify D-pad navigation (Up, Down, Left, Right, OK), app launching, and settings access.
- Confirm Wi-Fi, audio, and Bluetooth remote pairing remain 100% operational.
- Provide a summary of all changes made, the paths to the backups and restore script, and ask whether I want to keep network ADB open or close debugging.
