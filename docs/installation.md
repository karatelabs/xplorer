---
layout: docs
title: Installation
---

# Installation

Karate Xplorer is a desktop application available for macOS, Windows, and Linux.

## Download

Download the latest version for your operating system from the [home page]({{ '/' | relative_url }}) or directly from [GitHub Releases](https://github.com/karatelabs/xplorer/releases).

**Available downloads:**
- **macOS (Apple Silicon)** - For M1, M2, M3 Macs (`.dmg`)
- **macOS (Intel)** - For Intel-based Macs (`.dmg`)
- **Windows** - 64-bit installer (`.msi`)
- **Linux** - Debian package (`.deb`)

## macOS Installation

1. Download the appropriate `.dmg` file for your Mac:
   - Apple Silicon (M1/M2/M3) or Intel
2. Open the downloaded `.dmg` file
3. Drag Karate Xplorer to your Applications folder
4. Launch from Applications

**First launch:**
- The application is enterprise-signed
- You may need to right-click and select "Open" on first launch
- Subsequent launches work normally

## Windows Installation

1. Download the `.msi` installer
2. Double-click to run the installer
3. Follow the installation wizard
4. Launch Karate Xplorer from the Start Menu or Desktop shortcut

**Note**: The application is signed for enterprise deployment.

## Linux Installation

1. Download the `.deb` package
2. Install using your package manager:
   ```bash
   sudo dpkg -i Xplorer-linux-x86_64-*.deb
   ```
3. Launch from your applications menu or terminal:
   ```bash
   xplorer
   ```

## Verification

To verify the installation:

1. Launch Karate Xplorer
2. You should see the welcome screen with:
   - "Welcome to Xplorer" heading
   - "Open" button
   - Drag-and-drop instructions
3. The application is ready to use

## System Requirements

**All platforms:**
- Sufficient disk space for application installation
- Internet connection (for downloading collections, making API calls)

**macOS:**
- macOS 10.14 or later

**Windows:**
- Windows 10 or later (64-bit)

**Linux:**
- Modern Linux distribution with X11 or Wayland

## Updating

To update to a newer version:

1. Download the new version installer/package
2. Install over the existing installation
3. Your settings and recent files are preserved

## Uninstalling

**macOS:**
- Drag Karate Xplorer from Applications to Trash

**Windows:**
- Use "Add or Remove Programs" in Windows Settings

**Linux:**
```bash
sudo dpkg -r xplorer
```

## Next Steps

- [Quick Start Guide](quick-start/)
- [Importing Collections](importing/)
- [Interface Overview](interface/)
