# Forza Horizon 6 - RX 500 Series Fix

Experimental fix for **AMD RX 580 / Polaris** graphics cards that receive the **FH201** or **FH205** error when opening the game.

Created by **João Lucas**.

YouTube Channel: https://www.youtube.com/@MEGADROIDGAMESS


## Before starting

This fix was made for those who installed the AMD Agility SDK / Work Graphs driver and are still stuck on the **FH201** error.

The driver used in testing was:

```text
amd-software-adrenalin-edition-23.10.01.14-win10-win11-work-graphs
```

Important:

- The fix is experimental.
- It may not work on all graphics cards or game versions.
- It does not include game files.
- It does not remove DRM.
- Use at your own risk.

## How to install

1. Download this repository.

2. Open the folder:

```text
bin
```

3. Copy the file:

```text
d3d12.dll
```

4. Paste this file into the main game folder, where the executable is located.

Example:

```text
...\Forza Horizon 6\d3d12.dll
```

The correct folder is the same one where several `.dll` files of the game and the main executable are located.

5. Open the game normally.

## How to know if it's working

If previously it showed:

```text
FH201
FH205
```

and now the game opens, the fix is loading correctly.

The fix also creates a log file in the game folder:

```text
ForzaFix_RX580.log
```

If this file appears, it means the DLL was loaded.

## If FH205 still occurs

The **FH205** error normally means that the driver is not yet reporting support for **Enhanced Barriers**.

In this case, install the AMD Agility SDK / Work Graphs driver and restart the PC.

Then run:

```text
tools\D3D12Caps.exe
```

Look for this line:

```text
OPTIONS12: OK EnhancedBarriersSupported=TRUE
```

If `FALSE` appears, the driver has not activated the necessary support.

## If FHE01 occurs or the game closes by itself

Try to:

- verify the integrity of the game files;
- remove other mods/fixes;
- remove `dxgi.dll`, ReShade, OptiScaler or other third-party DLLs from the game folder;
- test with a clean game and only this `d3d12.dll`.

## How to remove the fix

Delete this file from the game folder:

```text
d3d12.dll
```

Done. The game will go back to using normal Windows DirectX.

## For developers

The source code is in:

```text
src
```

To compile, install:

- Visual Studio 2022 Build Tools;
- Desktop development with C++;
- Windows SDK.

Then run:

```powershell
powershell -ExecutionPolicy Bypass -File .\build_proxy.ps1
```

The compiled DLL will be output in:

```text
proxy_build\d3d12.dll
```

## What the fix does

It creates a proxy DLL named `d3d12.dll`.

It intercepts some DirectX 12 calls and forces the game to see support for `Feature Level 12_1`, helping to pass the **FH201** error.

Support for **Enhanced Barriers** must come from the driver. This is why the AMD Agility SDK / Work Graphs driver is important.
