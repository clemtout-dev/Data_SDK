# Clemtout Launcher

Clemtout Launcher is a custom-built, modern game launcher that provides an elegant interface to manage, launch, and patch your games. It features seamless Steam integration, automatic Steam emulator configuration fetching, and Photon network relay management for community server multiplayer.

## 🚀 Features

- **Modern UI/UX**: Built with HTML, CSS, and Vanilla JS, featuring a dark, high-tech glassmorphism aesthetic.
- **Steam Integration**: Extracts AppIDs automatically, fetches high-quality capsules from Steam CDN, and tracks local playtime across different Steam accounts.
- **Automated Game Patching**: Integrates an intelligent unpacking flow (Steamless) that detects SteamStub protection while bypassing non-protected files (like Unity exes) to prevent corruption.
- **Photon Network Relay**: A built-in configuration manager that modifies system hosts to redirect Exit Games (Photon) server traffic to community-hosted relays.
- **Multi-Launch Modes**: Launch games directly or through a Steam overlay wrapper (Spacewar - AppID 480) for advanced multiplayer capabilities.

## ⚠️ Important: Initial Setup

Before using or compiling the launcher, please note that the integrated **SteamCMD** utility is not fully functional out of the box.

1. **Manual Initialization**: You must first navigate to the `backend/steamcmd` directory and execute `steamcmd.exe` manually. 
2. **Download Updates**: This allows the utility to download its internal files and update itself to the latest version.
3. **Installation Completion**: Once SteamCMD reaches the `Steam>` prompt, you can close it. 
4. **Compilation**: Only after this manual step should you proceed to compile the launcher or run the Python backend. The launcher relies on a fully initialized SteamCMD to fetch game manifests and depot keys.

## 🛠️ Architecture

### 1. Frontend (`/frontend`)
The presentation layer uses standard web technologies inside a `pywebview` window. The `index.html` orchestrates a Single Page Application (SPA) feel, styled with `styles.css` and powered by `main.js`. It communicates asynchronously with the local Python backend.

### 2. Backend (`/backend`)
The core logic is powered by a **Python Flask server** (`app.py`). It handles:
- **Smart Unpacking**: Automatically scans for `steam_api.dll` (at root or in Unity `_Data` folders) and checks for the `.bind` / `steamstub` signature before attempting to unpack.
- **SteamCMD Automation**: Sequences commands to retrieve manifests and depot keys.
- **Privilege Management**: Handles Windows elevated permissions (`runas`) via PowerShell scripts for hosts file modification (Photon Patch).

### 3. The Game Loader (`game_loader.exe`)
When launching a game in "Crack Fix" mode, the launcher passes the game's executable path as an argument to the loader while forcing the Steam environment.

> **Note on Lost Source Code:** > The original C++ source code for `game_loader.exe` has been lost. It was a wrapper built using the Steam SDK to initialize the context and inject variables:
> ```cpp
> SetEnvironmentVariableA("SteamAppId", "480");
> SetEnvironmentVariableA("SteamNoAppIdCheck", "1");
> ```
> This forces the target application to bind to the **Spacewar (480)** context, enabling Steam features on community-patched games.

## ⚖️ Disclaimer & Sources

This launcher is a configuration utility intended for legitimate game owners to access alternative community servers. **This software does not endorse piracy.** Any misuse of this tool remains the sole responsibility of the end user. Clemtout Launcher is not affiliated with Valve Corporation, Steam, or Exit Games.

**Special Thanks & Attributions:**
- **Unpacker Engine:** [Steamless](https://github.com/atom0s/Steamless) by atom0s.
- **Steam Data Source:** [Manifesthub](https://gitlab.com/steamautocracks/manifesthub).

---
*Created by the ClemtoutLauncher Team. Licensed for non-commercial use only.*