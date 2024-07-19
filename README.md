# Modified DXVK's D3D9 adding eyecandy of bigger cursor

This repository is a fork of [DXVK](https://github.com/doitsujin/dxvk/) with following modification:

- Adding a new config option: `d3d9.enlargeHardwareCursor = 2 or 3 or 4`. When enabled, D3D9 hardware cursor would be enlarged into 2X, 3X or 4X size. So when play an elder D3D9 game on 
modern HiDPI display should be easier to see mouse cursor. Values other than 2, 3, 4 would be ignored.

- Enable `d3d9.enlargeHardwareCursor = 2` and `d3d9.deviceLossOnFocusLoss = True` for WoW.exe WoWFoV.exe and WoW_tweaked.exe. 

The later option is for running Vanilla WoW via [WINE-GE](https://github.com/GloriousEggroll/wine-ge-custom) and when enable [AMD FSR](https://www.amd.com/en/technologies/fidelityfx-super-resolution) just like Retail WoW. When multiboxing, it seems Vanilla WoW need `d3d9.deviceLossOnFocusLoss` to switch between multiple full-screen FSR windows.

If you have issue report, you could reply at [Turtle WoW forum](https://forum.turtle-wow.org/viewtopic.php?t=12997)


## How to use

For [Turtle WoW](https://turtle-wow.org/):

- Enable Hardware Cursor in game Video Options

- Windows 11: Put d3d9.dll under the same folder with WoW.exe

- Debian Linux and WINE: Put d3d9.dll into WINEPREFIX/drive_c/windows/system32/

- Debian Linux and Proton: Put d3d9.dll into Proton_Directory/files/lib/wine/dxvk/

- WINE may need a DLL override via winecfg to mark d3d9 as Native. Proton don't need this.

For other games you might find more info from upstream DXVK(https://github.com/doitsujin/dxvk/)

## Limitation

- Only works for **SOME** D3D9 games. No D3D11 nor D3D12.
- Only works for hardware cursor, not software cursor.
- I tested it on Debian Linux and Windows 11 using [Turtle WoW](https://turtle-wow.org/)
- According to MS document, if the underlaying platform can not support cursor size bigger than 32x32, API should scale the size back. However current implementation do not have such fallback capability. You may end up with no cursor.
- Vanilla WoW has a hard-coded 32x32 cursor. So current code has a 128x128 buffer for it. If you try using this code for another game, beware that if that game's cursor is already bigger than 32x32, the enlargement code would be bypassed.

## Algorithm

This work employs hqx-1.2 from https://github.com/grom358/hqx

## DISCLAIMERS

This work follow DXVK's original Zlib license.

Included hqx algorithm code is LGPL.
Care, it's LGPL.

It is recommended to build your own .dlls from source code. Downloading arbitrary binary from Internet and apply them onto Azeroth could lead into Burning Legion invasion or lose of your account.


