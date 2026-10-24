# The prompt

Paste this into Claude Code (or another coding assistant with shell access) on a computer that is
on the same Wi-Fi as the TV. Works on Android TV / Google TV sets (Xiaomi, TCL, Hisense, Sony,
OnePlus, Realme, Nvidia Shield and most others). It will not work on Samsung Tizen, LG webOS or
Fire TV.

CatUI repository: https://github.com/asishmohapatra09/CatUI-For-CleanYourTv
Release APK: https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/Public_V1.0/CatUI-v2.3.apk
Release SHA-256 checksums: https://github.com/asishmohapatra09/CatUI-For-CleanYourTv/releases/download/Public_V1.0/SHA256SUMS.txt

Before you start, on the TV: Settings → Device Preferences → About → press OK on "Build" 7 times,
then go back → Developer options → turn on USB debugging (and Network/ADB debugging if your TV
shows it). Keep the TV on. Some boxes cut power to their USB port while USB debugging is on, so a
USB speaker or drive plugged into it goes dead until you switch debugging off again. A USB Ethernet
adapter on that port can drop the same way, so plan to do the whole session in one sitting.

---

I want to debloat my Android TV and replace its launcher with CatUI (a clean Apple TV style home screen with live weather).
My TV model is: <MODEL NAME HERE>. Work on the real device, step by step, and verify everything you
do with screenshots pulled from the TV. Ask me before anything that depends on my preferences.

Connect
- Find the TV on my network (hostname, ARP table, or ask me for the IP) and connect over ADB on port 5555.
  If the TV is in another home, I'll give you its Tailscale address instead (docs/REMOTE.md): use that,
  don't scan my local network.
- If the stock adb binary fails with "No route to host" on macOS even though the port is open, that is
  macOS Local Network privacy blocking adb. Don't debug it: use the Python `adb-shell` package in a venv
  as the ADB client instead. If its file push hangs on larger files, transfer files as base64 chunks
  through the shell and verify the md5.
- If your own commands can't reach the TV at all while it answers from an ordinary terminal (a sandbox that
  blocks the local network), ask me to run `tools/relay.py <tv ip>` in a terminal and leave it running, then
  use `TV_HOST=127.0.0.1 TV_PORT=15555` (`tools/relay.md`).
- If port 5555 stays closed, the TV may only offer Wireless debugging (Google TV sets often do): look for
  `_adb-tls-connect._tcp` with `dns-sd -B` or `adb mdns services`, ask me for the code and port under
  Developer options > Wireless debugging > Pair device with pairing code, then `adb pair`, `adb connect`
  and `adb tcpip 5555`. Android switches Wireless debugging off whenever Wi-Fi drops.
  Some firmware runs network ADB on another fixed port instead (a projector used 5877): if 5555 refuses and
  nothing advertises Wireless debugging, scan the TV's own TCP ports and try each open one with `TV_PORT`.
- Tell me when the "Allow USB debugging?" prompt will appear on the TV so I can accept it.
- If `adb install` hangs on Android 14 it is waiting for an on-screen confirmation; push the APK to
  `/data/local/tmp/` and run `pm install -r` over the shell instead.

Back up first
- Save the full package list, disabled-package list, getprop output and all settings to a backup folder
  before changing anything, and write a restore script that re-enables everything you disable.
- Ask me what is plugged into the TV's USB ports, and ask separately whether the TV's network comes
  through a USB Ethernet adapter: "nothing plugged in" can be true while the network itself is on that
  port. Some devices cut their power while USB debugging is on, so warn me, and remind me to switch
  debugging off once you're done. On a set that reaches the network over USB Ethernet, check before you
  change anything: `dumpsys usb | grep host_connected` (`host_connected=false` means the adapter is
  already gone) and `dumpsys connectivity | grep -o 'Transports: [A-Z]*'` (`WIFI` on a TV I call wired
  means the box fell back, and ADB is running over Wi-Fi). Finish the whole job in one sitting, not
  two: there the port only returns with USB debugging off, and that closes port 5555 as well. Prefer
  Wireless debugging if the TV has it.
- When you finish, close network ADB instead of leaving it open: switch USB debugging and
  Network/ADB debugging off on the TV, revoke the USB debugging authorisations, reboot, and check
  that the port refuses the connection. If the TV's network came over a USB Ethernet adapter, unplug
  and replug the adapter once debugging is off - the port comes back with it - and have me confirm the
  TV is on Ethernet again, not Wi-Fi. Don't trust `nc` on macOS: Local Network privacy can block it
  too, and its "No route to host" proves nothing; only "Connection refused" does. Port 5555 is
  plaintext, and on firmware with `ro.adb.secure=0` any device on the LAN can get a shell.

Debloat
- List installed packages and sort them into: manufacturer telemetry/analytics, manufacturer content
  and ad services (PatchWall, recommendation rows, content providers), background services I probably
  don't need (share/cast duplicates, cleaners), preloaded apps, and streaming apps.
- Disable the first categories with `pm disable-user --user 0`, never uninstall system packages.
- Never disable what the TV needs to work: the TV app and input services that play HDMI and the
  tuner, the input/source menu, remote control and Bluetooth pairing services, the on-screen
  keyboard, Google Play Store and Play Services. Manufacturer package names often don't say what a
  package does: check its activities and services with `dumpsys package` first, and ask me if it's
  still unclear.
- Never disable Android's own core packages, or the TV may not boot again: the permission controller,
  the package installer, ext services and ext shared, module metadata (each as `com.android.*` or
  `com.google.android.*`), `com.google.android.overlay.modules*`, `com.android.providers.*` (calendar,
  contacts, user dictionary and blocked numbers aside), `com.android.systemui`, `com.android.shell`,
  `com.android.phone`, `com.android.settings`, `com.android.tv.settings` and `android`. An original Mi TV
  Stick never booted again after a list took the first six
  ([#884](https://github.com/Gathin23/cleanyourtv/issues/884)); refuse such a list.
- Before touching streaming apps, voice assistant, Chromecast, Miracast or the update service, ask me
  which ones I use with a checklist question and disable only what I don't tick.
- Run `pm` commands one per shell call, chained commands may silently stop after the first.
- If `pm disable-user` is refused for every package, stop and tell me: some firmware (Fire OS 5 on a
  Fire TV Box, for one) refuses `pm disable-user` with a `SecurityException`, `pm uninstall --user 0`
  with `DELETE_FAILED_INTERNAL_ERROR`, and `pm hide` reports success while changing nothing. Check
  with `pm list packages -d` instead of the exit code, and don't burn the session retrying - there is
  nothing to debloat on such a set, so we fall back to its own privacy toggles and DNS blocking.
- Don't launch a package whose name says factory, production, AT or fac menu (`com.cvte.tv.hkcfac`,
  `com.cvte.tv.fac.menu`, `com.at.factory.*`, `mediatek.factorymenu.ui` and the like) to see what it does, even read-only:
  on Haier/CVTE boards opening one flips a factory-mode flag that kills the Input key and CEC, and
  makes the next boot disable Play services, Netflix and Chromecast - which the shell then cannot
  re-enable. `dumpsys package <name>` tells you what a package is without starting it.
- Disable in small batches and screenshot between them: a batch can take something load-bearing with
  it and you cannot tell which.
- After the last batch, reboot once and compare `pm list packages -d` with what you disabled: some
  firmware re-enables packages at every boot from its own list (TCL Android 9 does this for its user
  center). Note those in the list header instead of disabling them again after each boot. If
  setupwraith or the stock launcher came back and Home is black, check `logcat | grep
  RecoveryActivity` and re-enable the stock launcher before anything else.
- Offer me ad-blocking DNS as an optional extra: on Android 9 and newer, Private DNS set to an
  ad-blocking resolver (`settings put global private_dns_specifier dns.adguard-dns.com`, then
  `settings put global private_dns_mode hostname`). Tell me it doesn't block YouTube ads, check an app
  still plays afterwards, and note the undo (`private_dns_mode opportunistic`) in the README.

Launcher (CatUI)
- Check that the TV accepts APKs and verify SDK level: `getprop ro.build.version.sdk` (CatUI requires
  minSdk 26 / Android 8.0 or newer).
- Auto-download CatUI: download `CatUI-v2.3.apk` from the Release APK URL above, and `SHA256SUMS.txt`
  from the checksum URL above. Verify the downloaded APK's SHA-256 against `SHA256SUMS.txt` before
  installing. Stop immediately if the checksum does not match; never install an unverified APK.
- Install CatUI (`com.asish.catui`, MainActivity: `com.gathin.tvhome.MainActivity`). On Android 14,
  push the verified APK to `/data/local/tmp/CatUI-v2.3.apk` and run `pm install -r /data/local/tmp/CatUI-v2.3.apk`
  over the shell, then remove the temp file.
- Set CatUI as default Home: list HOME activities with `cmd package query-activities -a android.intent.action.MAIN -c android.intent.category.HOME`
  and set default with `cmd package set-home-activity com.asish.catui/com.gathin.tvhome.MainActivity`.
  Because stock launchers declare priority > 0, disable the stock launcher with `pm disable-user --user 0 <stock_launcher>`
  after asking for my confirmation, and verify with `dumpsys activity activities | grep mFocusedApp` that CatUI opens.
- Before disabling the stock launcher, check which other apps claim HOME: on Google TV the setup wizard
  (`com.google.android.tungsten.setupwraith`) takes over even after the stock launcher is disabled.
  Before disabling setupwraith, run `dumpsys wifi | grep -o 'cname=[^ ]*'`: a Wi-Fi network saved
  during first setup belongs to it, and Android deletes that network the moment it is disabled, which
  takes the TV off Wi-Fi and ADB. If it does, ask me to forget the network and re-join it in Settings first.
- On a CVTE board (any `com.cvte.*` package), leave its stock launcher (`com.cvte.tv.launcher.*`) enabled
  unless verified safe: make CatUI Home with `set-home-activity`, reboot once, and confirm Home and ADB
  come back before anything else.
- Weather & Location Setup: CatUI features an Apple TV style greeting, live clock, and a live weather
  scene that dynamically changes between day, dusk, night, rain, and snow using Open-Meteo.
  Ask me which city or town my TV is located in (or its latitude and longitude).
  Grant CatUI location permissions over shell: `pm grant com.asish.catui android.permission.ACCESS_FINE_LOCATION`
  and `pm grant com.asish.catui android.permission.ACCESS_COARSE_LOCATION`.
  Since TV sticks and boxes lack built-in GPS hardware, set the location on the device provider:
  enable mock location (`appops set 2000 android:mock_location allow`), add the network test provider
  (`cmd location providers add-test-provider network --requiresNetwork`), enable it, and set the coordinates
  (`cmd location providers set-test-provider-location network --location <LAT>,<LON>`) with matching timezone.
  Restart CatUI (`am force-stop com.asish.catui && am start -n com.asish.catui/com.gathin.tvhome.MainActivity`)
  and verify the weather temperature and condition match the city.
- Remote App Buttons & Key Services: On Google TV the stock launcher answers dedicated remote buttons
  (Netflix, Prime Video, YouTube, Apps). After disabling it, ask me to test each button.
  If any need remapping, capture real scan codes with `getevent -lt` or logcat and use CatUI's built-in
  accessibility key service (`com.gathin.tvhome.HomeKeyService` / `InputKeyService`).
  Before changing `enabled_accessibility_services`, inspect existing services and append CatUI's service
  without overwriting others.
- Ask how many dock slots I want (4, 5, 6 or 7), which apps, and their order; keep four or five if I
  have no preference.
- Design: Apple TV 4K style; pitch black background with dynamic live pixel weather; dock row inside a
  translucent rounded band holding the apps I pick; rest of the apps in an app grid below; frosted pill
  buttons top right for Control Center (Inputs, Wi-Fi, Bluetooth, Audio, and Settings); greeting, clock,
  date, and live weather forecast top left.
- Make D-pad navigation deterministic: Up/Down move exactly one row, Up from the dock goes to the top
  bar, the ends of the top bar don't fall through to tiles. Remember the last focused tile.
- Keep it light: TV sticks have about 1 GB of RAM. No heavy video backgrounds, no continuous polling.

Verify
- After each change, inject remote key presses over ADB, take a screenshot from the TV and look at it:
  capture what is on screen and pull the PNG. Fix what you see before moving on.
- Live TV, HDMI and some streaming apps (Netflix) give empty screenshots (0 bytes); that is the TV DRM,
  not a broken debloat. Check `dumpsys activity activities | grep topResumedActivity` instead.
- If the screen looks enlarged and clipped after an install or a reboot, check display overrides before
  editing anything: `wm size` and `wm density` show a physical value next to an override.
- When done, give me a complete restore script, a build/reinstall script, and a README that explains how
  to re-enable any package, how to change dock apps, and how to close network ADB.

---

Expect to answer four or five checklist questions (which apps you use, your city/location for the
live weather scene, the dock size and app order, whether to keep the voice assistant, Chromecast and
firmware updates). Everything is reversible.
