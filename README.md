<div align="center">
  <h1># Forza Horizon 6 FH201/FH205 Fix for AMD RX 580 & RX 500 Series</h1>
  <p><strong>Experimental Windows fix for Forza Horizon 6 FH201 and FH205 startup errors on AMD RX 580, RX 570, RX 590 and other RX 500 Series / Polaris graphics cards. This uses a D3D12 proxy DLL to help unsupported AMD Polaris GPUs pass the game startup check.</strong></p>

  [![Creator](https://img.shields.io/badge/Created_by-Muhammad_Sameer-blue.svg)](https://www.youtube.com/@sameer-_-2605)
  [![YouTube](https://img.shields.io/badge/YouTube-Subscribe-red.svg?logo=youtube)](https://www.youtube.com/@sameer-_-2605)
  [![License](https://img.shields.io/badge/License-MIT-green.svg)](#)
  [![Platform](https://img.shields.io/badge/Platform-Windows-lightgrey.svg)](#)
</div>

---

## 📌 Overview

This repository provides an experimental proxy DLL designed to bypass the **FH201** and **FH205** errors in Forza Horizon 6 on older AMD graphics cards, specifically the **RX 580 / Polaris architecture**. It works by intercepting DirectX 12 calls and artificially reporting support for `Feature Level 12_1`.

> ⚠️ **IMPORTANT DISCLAIMER**
> - This fix is highly **experimental**.
> - It does not guarantee compatibility with all graphics cards or game versions.
> - **It DOES NOT include any game files and DOES NOT bypass DRM.**
> - Use at your own risk.

---

## 🚀 Prerequisites

Before installing this fix, you **must** have the AMD Agility SDK / Work Graphs driver installed. If you are stuck on the `FH201` error, ensure you are running a supported driver version.

Tested Driver Version:
```text
amd-software-adrenalin-edition-23.10.01.14-win10-win11-work-graphs
```

---

## 🛠️ Installation Guide

1. **Download** or clone this repository to your local machine.
2. Navigate to the `bin` directory:
   ```bash
   cd bin
   ```
3. Copy the compiled proxy file:
   `d3d12.dll`
4. **Paste** it directly into your main Forza Horizon 6 game folder (the same directory containing the game's executable and other `.dll` files).
   ```text
   Example: C:\Games\Forza Horizon 6\d3d12.dll
   ```
5. **Launch** the game normally.

---

## 🔎 Verification & Troubleshooting

### How to verify it's working
If your game previously crashed with `FH201` or `FH205` and now successfully launches, the proxy is active.

Additionally, a log file named `ForzaFix_RX580.log` will be generated in your game folder upon successful loading of the DLL.

### Still getting the FH205 error?
The `FH205` error typically indicates your driver is not reporting support for **Enhanced Barriers**. 
1. Reinstall the **AMD Agility SDK / Work Graphs driver** and reboot your PC.
2. Run the provided diagnostic tool:
   ```bash
   tools\D3D12Caps.exe
   ```
3. Check the output for:
   ```text
   OPTIONS12: OK EnhancedBarriersSupported=TRUE
   ```
   *If it says `FALSE`, your driver lacks the necessary feature support.*

### Crashing / FHE01 Error?
If the game closes unexpectedly or throws an `FHE01` error, try the following:
- Verify your game files' integrity.
- Remove other mods or fixes.
- Delete conflicting third-party DLLs (e.g., `dxgi.dll`, ReShade, OptiScaler).
- Test on a clean installation with only this `d3d12.dll` applied.

---

## 🗑️ Uninstallation

To remove the fix, simply delete the proxy DLL from your game directory:
```text
...\Forza Horizon 6\d3d12.dll
```
The game will automatically revert to using the standard Windows DirectX components.

---

## 💻 For Developers

Interested in how this works or want to compile it yourself? The source code is located in the `src` directory.

### Build Requirements
- **Visual Studio 2022 Build Tools**
- Desktop development with C++ workload
- Windows SDK

### Compilation Steps
Open PowerShell and run the build script:
```powershell
powershell -ExecutionPolicy Bypass -File .\build_proxy.ps1
```
The compiled DLL will be generated in the `proxy_build\` folder.

### Technical Details
This fix works by generating a proxy `d3d12.dll`. It intercepts specific DirectX 12 calls and forces the game to detect support for `Feature Level 12_1`, bypassing the `FH201` block. However, **Enhanced Barriers** support is still strictly required from the driver level (hence the requirement for the Agility SDK driver).

---
<div align="center">
  <i>Developed with ❤️ by <a href="https://www.youtube.com/@sameer-_-2605">Muhammad Sameer</a>.</i>
</div>
