# God of War: Betrayal Remastered — Native Android & PC Port

![God of War: Betrayal Remastered](.github/social-preview.jpg)

[![Platform](https://img.shields.io/badge/Platform-Android%20%7C%20Windows-blue.svg)](https://github.com/SupaRj/gow-betrayal-remastered-Android-Native-port)
[![Engine](https://img.shields.io/badge/Language-C%2B%2B17%20%7C%20Java-orange.svg)](https://github.com/SupaRj/gow-betrayal-remastered-Android-Native-port)
[![Frame Rate](https://img.shields.io/badge/FPS-60%20%2F%2090%20%2F%20120%20Hz-green.svg)](https://github.com/SupaRj/gow-betrayal-remastered-Android-Native-port)

A native Android and Windows C++ port of *God of War: Betrayal*, the 2007 side-scrolling *God of War* title created for J2ME (mobile Java) phones. It is rebuilt directly from the decompiled bytecode of the Sony Ericsson K800i release (MIDlet 1.4.20) — **not emulated**, running natively on modern hardware with widescreen, high frame rates, custom touch controls, and modern gamepads.

---

## 📱 Android Native Port Features

This fork introduces a **full native Android port (APK)** powered by **NDK, C++17, and SDL2**:

- ⚔️ **Spartan Touch Controls ("Bronze de Sparte & Méandre")**:
  - Immersive Ancient Greek / Spartan aesthetic (weathered bronze frame, obsidian dark outline for readability over both light and dark stone backgrounds).
  - Multi-touch support with smooth opacity fade-out during inactivity and glowing feedback on press.
  - Dedicated virtual keys for Attack, Jump, Grab/Parry, Magic/Weapons, Upgrade (Ω) and Pause.
- 🎮 **Full Gamepad Support with Auto-Detection**:
  - Plug-and-play support for Bluetooth and USB gamepads (Xbox, PlayStation, Android controllers).
  - When a physical controller is detected, the touch overlay hides automatically. Touch controls reappear instantly if the controller is disconnected.
- ⚡ **High Refresh Rates (60 / 90 / 120 FPS)**:
  - Sub-frame motion interpolation matching your device's native screen refresh rate (60 Hz, 90 Hz, 120 Hz) while preserving the exact 25 TPS logic clock.
- 🎵 **Multithreaded Low-Latency Audio Engine**:
  - Dedicated background audio executor with pre-warmed `MediaPlayer` instances.
  - Fixes combat frame drops: MIDI and WAV playback triggers instantly without synchronous disk I/O or JNI overhead.
- 📊 **Built-in Discrete FPS & TPS Counter**:
  - Lightweight 3×5 bitmap font overlay measuring real display FPS and logical ticks per second.
  - Configurable directly from the in-game **Options** menu.
- 📁 **Centralized `GOW-Betra` Storage & Robust Logging**:
  - Stores user saves, config (`android_display.cfg`), and diagnostic logs in `/storage/emulated/0/GOW-Betra/`.
  - Non-blocking permissions: if file access is declined, automatically falls back to internal private storage without losing saves or progress.
  - Automatic migration from internal private storage to `GOW-Betra` when permissions are granted.
  - Crash-safe rotating session logs (retaining the 10 most recent logs, 2 MB max each) with an async-signal-safe native crash reporter.
- 🖼️ **Adaptive & Themed App Icons**:
  - Full support for Android 8.0+ adaptive icons, Android 13+ themed/monochrome silhouettes, and custom console launchers (Cocoon Shell, DroidDeck, etc.).
- 🌐 **Widescreen & Multi-Language**:
  - Aspect ratio modes (Auto, Original, 16:9, 21:9) without stretching 2D sprites.
  - Fixes the original J2ME language selection bug (English, Français, Español, Deutsch, Italiano, Português).

---

## 📦 Download and Install (Android)

**The game assets are not distributed.** They belong to their respective copyright holders. You supply your own copy of the Sony Ericsson K800i `.jar` (`God-of-War-Betrayal_K800i_v1420.jar`).

### Quick Installation via ADB:
```powershell
adb install -r GodOfWar-Betrayal.apk
```

*(Optional: Grant storage access directly via ADB if you don't want the in-game permission prompt)*:
```powershell
adb shell appops set com.gow.betrayal MANAGE_EXTERNAL_STORAGE allow
```

---

## 🛠️ Building from Source

### Android APK Build

**Prerequisites**:
- Android Studio / Android SDK (API 35+ / Build Tools 36.0.0)
- Android NDK (r25+ / 27+)
- CMake 3.22+ and Ninja
- JDK 17+

Run from the `android/` directory:
```powershell
cd android
.\gradlew.bat assembleDebug
```
The generated APK will be at:
`android/app/build/outputs/apk/debug/app-debug.apk`

### Windows PC Port Build

You need Windows, Visual Studio (or VS Build Tools with C++ workload), CMake, and Ninja.
```powershell
python tools\extract_jar.py          # unpack your jar from roms\
python tools\decompile.py
python tools\rename_gow.py           # renamed Java -> betrayal\src + compile check
python tools\java2cpp.py             # -> betrayal\port\src\gen
betrayal\port\build.bat              # builds betrayal\port\build\gow_port.exe
```

---

## 📂 Repository Structure

| Path | Contents |
|---|---|
| `android/` | Android project (Gradle, CMake, SDL2 Java bindings, AndroidManifest, icons) |
| `android/app/src/main/cpp/` | Native Android glue (`main_android.cpp`, `platform_android.cpp`, touch controls, profiler) |
| `android/app/src/main/java/` | Java audio layer (`GowMidiPlayer.java`) and SDL activity |
| `betrayal/port/` | The original C++ port, Win32 launcher, and packaging scripts |
| `betrayal/src/` | Renamed, compile-checked Java sources |
| `tools/` | Extraction, decompilation, renaming, and C++ translation scripts |
| `roms/`, `betrayal/extracted/` | Your original JAR and unpacked data (gitignored) |

---

## ⚖️ Legal & Attribution

- Original reverse-engineering and C++ port by [samioan](https://github.com/samioan/gow-betrayal-remastered).
- Android Native Port, Spartan touch controls, audio optimization, and storage subsystem by [SupaRj](https://github.com/SupaRj/gow-betrayal-remastered-Android-Native-port).
- This project is an independent educational preservation effort. It is not affiliated with, endorsed by, or supported by Sony Interactive Entertainment, Santa Monica Studio, Glu Mobile, or Metaflow. *God of War* is a registered trademark of Sony Interactive Entertainment LLC. See [NOTICE.md](NOTICE.md) for attribution and third-party licenses.
