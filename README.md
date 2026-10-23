# CatUI

CatUI is a custom Android TV home screen with a glass-style interface and a pixel-art bedroom scene. It is designed for TV remotes and can be installed as the default Home app. The app package is `com.asish.catui`.

## Download

For a ready-to-install build, upload **`release/CatUI-v2.3.apk`** as an asset on the GitHub Release page. Download that APK from Releases; the source tree also contains the launcher code and build scripts.

The APK in this release is version **2.3** (version code 4). Minimum Android version: **Android 8.0 / API 26**. The tested TV runs Android 9 / API 28.

## Features

- A glass-style home screen, app dock, and full-screen app drawer navigated with a TV remote.
- Preferred dock order: YouTube, Jellyfin, Hotstar, SonyLIV, and Zee5. Apps that are not installed are skipped.
- An Inputs menu for available HDMI/AV/TV inputs, plus Settings and Wi-Fi controls.
- Clock, date, and weather for Paradip, Odisha. Weather is fetched from Open-Meteo using the configured coordinates; the TV needs internet access for current weather.
- Four local-time looks: morning, afternoon, evening, and night. Rain changes the scene and lighting; rain droplets, cup steam, and the night fireplace are animated separately. The cat stays still.
- A subtle background pan, and a removable **Scene demo** tile in the app drawer for previewing scenes.
- No root, firmware flashing, firmware updates, or third-party remote-remapping app is required.

## Tested TV and remote buttons

Tested on a Xiaomi Mi TV reported by Android as `MiTV-AXSO0` (device `dangal`), Android 9 / API 28, build `PI.6036 release-keys`.

With CatUI's built-in **Home button** accessibility service enabled on this remote, the confirmed mappings are:

| Remote button | CatUI action | Linux key scan code on the tested TV |
| --- | --- | ---: |
| Netflix | Open YouTube | 393 |
| Prime Video | Open Jellyfin | 399 |
| Mi | Open CatUI Inputs | 580 |

Remote key codes differ by TV and remote. These scan codes are specific to the tested Xiaomi remote; other users should capture their own button events and choose their mappings. The accessibility service is opt-in and only needs enabling if the user wants these shortcuts.

## Install from a GitHub Release

1. Enable ADB/network debugging in the TV's developer settings and accept the computer's debugging prompt.
2. Install Android Platform Tools on the computer. Open PowerShell or a terminal in the folder containing the downloaded APK.
3. Connect to the TV, replacing the address with the TV's IP:

   ```powershell
   adb connect TV_IP_ADDRESS:5555
   adb devices
   adb install -r .\CatUI-v2.3.apk
   ```

4. Set CatUI as Home:

   ```powershell
   adb shell cmd package set-home-activity --user 0 com.asish.catui/com.gathin.tvhome.MainActivity
   adb shell input keyevent KEYCODE_HOME
   ```

   The built-in build/install script leaves the TV's existing launcher installed and enabled. Keep a working system launcher as a fallback. If the command is not supported by a particular TV, use that TV's Home-app picker instead.

5. To enable the built-in Netflix/Prime/Mi mappings, open the TV's **Settings → Accessibility → Home button** service and turn it on. Keep any accessibility services you already use enabled. Then test each physical button. If the key labels or behavior differ, configure the service for the actual remote instead of reusing the table above.

For the complete TV-specific safety checklist and LLM copy/paste prompt, see [PROMPT.md](PROMPT.md).

## Build and install from source

Requirements: JDK 17, Android SDK Platform 34, Android Build Tools 34, Python 3, and an authorized ADB connection to the TV.

First create the ADB helper environment from the repository root.

Windows PowerShell:

```powershell
py -3 -m venv tools\venv
.\tools\venv\Scripts\python.exe -m pip install -r tools\requirements.txt
$env:TV_HOST = 'TV_IP_ADDRESS'
```

macOS/Linux:

```bash
python3 -m venv tools/venv
tools/venv/bin/python -m pip install -r tools/requirements.txt
export TV_HOST=TV_IP_ADDRESS
```

Then build and install:

```powershell
# Windows; add -HomeKeyService only if you chose CatUI's remote shortcuts.
.\launcher\build-and-install.ps1 -TvHost $env:TV_HOST -HomeKeyService
```

```bash
# macOS/Linux; HOME_KEY_SERVICE enables the built-in remote shortcut service.
HOME_KEY_SERVICE=1 launcher/build-and-install.sh
```

Omit `-HomeKeyService` / `HOME_KEY_SERVICE=1` if you do not want the Netflix, Prime Video, and Mi shortcuts. The scripts set CatUI as Home and leave existing launchers enabled; they do not debloat the TV. Review the scripts before running them. For updates, use an APK signed with the same signing key as the installed build; a different signing key requires uninstalling first and can erase CatUI's settings.

The source build uses the Android SDK and may require internet access to download Gradle dependencies. The release APK is at `release/CatUI-v2.3.apk` in this checkout; the Gradle output is `launcher/app/build/outputs/apk/release/app-release.apk`.

## Credits and image ownership

- **CatUI bedroom scene art and concept images:** © **Asish Mohapatra**. The scene art is supplied by the project author; please ask the author before reusing it.
- **[CleanYourTV](https://cleanyour.tv/#ch-04)** — Android TV setup and debloating reference. The upstream project and its license are linked in [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md).
- **[glassOS-tv](https://github.com/jmarknavarro/glassOS-tv)** — inspiration for CatUI's glass-style interface only. The bedroom art is by Asish Mohapatra.
- **[Cosy Home TV](https://github.com/oliverjwroberts/cosy-home-tv)** — earlier launcher/scene-weather work informed the prior CosyGlassOS iteration. It did not provide CatUI's bedroom artwork.
- **Outfit typeface** — [Outfit Fonts](https://github.com/Outfitio/Outfit-Fonts), SIL Open Font License 1.1.
- **Weather** — [Open-Meteo](https://open-meteo.com/).

See [THIRD_PARTY_NOTICES.md](THIRD_PARTY_NOTICES.md), `licenses/`, and `launcher/FONT-LICENSE-OFL.txt` for complete notices. CatUI is independent and is not affiliated with Xiaomi, Google, Apple, or the authors of the referenced projects.
