# Modified DXVK's D3D9 adding eyecandy of bigger cursor

This repository is a fork of [DXVK](https://github.com/doitsujin/dxvk/) with following modification:

- Adding a new config option: `d3d9.enlargeHardwareCursor = 2 or 3 or 4`. When enabled, D3D9 hardware cursor would be enlarged into 2X, 3X or 4X size. So when play an elder D3D9 game on modern HiDPI display should be easier to see mouse cursor. Values other than 2, 3, 4 would be ignored.

- Allowing sideload images into D3D9 hardware cursor. While hqx algorithm is specially designed for pixel-art scaling, small cursor enlargement still result in low quality output. So this work also provide a way to sideload high resolution images into D3D9 hardware cursor.

- Enable `d3d9.enlargeHardwareCursor = 2` and `d3d9.deviceLossOnFocusLoss = True` for WoW.exe WoWFoV.exe and WoW_tweaked.exe. 

The `d3d9.deviceLossOnFocusLoss = True` option is for running Vanilla WoW via [WINE-GE](https://github.com/GloriousEggroll/wine-ge-custom) and when enable [AMD FSR](https://www.amd.com/en/technologies/fidelityfx-super-resolution) just like Retail WoW. When multiboxing, it seems Vanilla WoW need `d3d9.deviceLossOnFocusLoss` to switch between multiple full-screen FSR windows.

If you have issue report, you could reply at [Turtle WoW forum](https://forum.turtle-wow.org/viewtopic.php?t=12997)



## How to use

For [Turtle WoW](https://turtle-wow.org/):

- Enable Hardware Cursor in game Video Options

- Windows 11: Put d3d9.dll under the same folder with WoW.exe

- Debian Linux and WINE: Put d3d9.dll into WINEPREFIX/drive_c/windows/system32/

- Debian Linux and Proton: Put d3d9.dll into Proton_Directory/files/lib/wine/dxvk/

- WINE may need a DLL override via winecfg to mark d3d9 as Native. Proton don't need this.

For other games you might find more info from [upstream DXVK](https://github.com/doitsujin/dxvk/)



## How to get 4X sized HUGE cursor instead of default 2X size

For Windows 11
- Create a text file named `dxvk.conf` at the same location with d3d9.dll, with its contents: `d3d9.enlargeHardwareCursor = 4`


For Linux
- Run the game with an environment variable: `DXVK_CONFIG="d3d9.enlargeHardwareCursor=4;" turtle-wow`



## Sideload image into cursor

- Enable `d3d9.enlargeHardwareCursor` option, the multiplier would be ignored when using sideload. So 2 or 3 or 4 would be the same.

- Create a new folder named `SideloadCursors` at the same location with d3d9.dll

- Put desired image into `SideloadCursors`. Its size must NOT bigger than 128x128 pixel. It could be JPG, PNG, TGA, BMP, PSD, GIF, HDR, PIC. It must contain 4 color channels including RED GREEN BLUE and ALPHA.

- Rename the image like `CursorHash-HotSpotX,HotSpotY.png`.

- Any number of image could be sideloaded. If the corresponding in-game cursor don't have sideload image, hqx algorithm scaling would be used.


Every in-game cursor would have a different CursorHash. We could get this information via DXVK debug info. Run the game with an environment variable: `DXVK_LOG_LEVEL=info`

Whenever in-game cursor change, a CursorHash would be printed to terminal/log-file as
`info:  Enlarge D3D9 hardware cursor: 2f4f94382e0e5b958fae25559151a1c02aea9ea3`

HotSpot is the clickable spot coordinates on image.

For example we would like (11, 11) be hot spot for cursor `2f4f94382e0e5b958fae25559151a1c02aea9ea3`,
we could rename our image as `2f4f94382e0e5b958fae25559151a1c02aea9ea3-11,11.png`.



## Limitation

- Only works for **SOME** D3D9 games. No D3D11 nor D3D12.
- Only works for hardware cursor, not software cursor.
- Sideload only work for static image, no animation.
- I tested it on Debian Linux and Windows 11 using [Turtle WoW](https://turtle-wow.org/)
- According to MS document, if the underlaying platform can not support cursor size bigger than 32x32, API should scale the size back. However current implementation do not have such fallback capability. You may end up with no cursor.
- Vanilla WoW has a hard-coded 32x32 cursor. So current code has a 128x128 buffer for it. If you try using this code for another game, beware that if that game's cursor is already bigger than 32x32, the enlargement code would be bypassed.



## Algorithm

This work employs [hqx](https://en.wikipedia.org/wiki/Hqx). Its implementation is from https://github.com/grom358/hqx



## DISCLAIMERS

This work follow DXVK's original Zlib license.

Included hqx algorithm code is LGPL.
Care, it's LGPL.

Included [stb_image](https://github.com/nothings/stb) is public domain.

It is recommended to build your own .dlls from source code. Downloading arbitrary binary from Internet and apply them onto Azeroth could lead into Burning Legion invasion or lose of your account.



