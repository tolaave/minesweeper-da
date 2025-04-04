# Minesweeper DA
This is a quick fun project I quickly hacked up for #MARCHintosh 2025, a minesweeper clone implemented as Desk Accessory (DA) for older 68K Macs.

![minesweeper](https://github.com/user-attachments/assets/130b25fb-be0b-4bac-9d47-c7ac9e3a307d)

I always wanted to write my own version of Minesweeper, and doing it as a Desk Accessory felt like a fun way to do it, given how simple the game is (akin to the "Puzzle" game Apple bundled with older Mac system versions).

This project was almost completely (99.9%) developed under MACE without using other emulators or real hardware:
- Using THINK Pascal 4.0.1 to write, debug the code and build final DA
- ResEdit 2.1.3 to create all resources and draw the graphics. All graphics were hand-drawn using 100% ResEdit 2.1.3 to mimic the original Windows 3.x minesweeper as closely as possible, with some "mac-like" modifications to them :)
- Only external tools used were Compact Pro & Dropbin running in Basilisk2 to package the final, compiled game (as I didn't have time to figure out why CompactPro fails to create new archives under MACE, instead failing on resource loading error)

Some notes on the graphics:
- The DA should support multi-monitor setups with any color depths, even if crossing window between monitors (not tested though!)
- Tile graphics are implemented as 'cicn's drawn through PlotCIcon on color quickdraw systems, and as 'SICN's loaded into BitMaps drawn through CopyBits on b&w systems
- The 'cicn's have b&w versions (same as in 'SICN's) of tiles, so that they'll get automatically selected by QuickDraw depending on the target device (monochrome versions are used for 1- and 2-bit devices)
- Colors in the 'cicn' resources are selected so that they should look nice also in 16-color modes (as QuickDraw converts the 8-bit colors into the 4-bit palette during drawing)
- When handling Update events, DeviceLoop is used to determine color depth of drawing target devices to select proper background pattern & color combination for each device
- To make the game fully playable on older Macs, the minefield maximum size is capped by the 512x342 "classic" screen size, which has space for 30x16 tiles of 16x16 size in a window that covers almost the full screen (plus the status area at top). Interestingly, this is the same size as Windows 3.x minesweepers expert playfield, which seems to be quite interesting coincidence...

After compiling, this desk accessory was tested briefly running System 7.x in other emulators, and MacOS 9.x on real hardware.

Although game code is original, there's a couple bits of sample code from the THINK Pascal Demo application samples:
- The Desk Accessory project foundation was based on "Hex Dump DA" sample project (especially the DA Shell program used to test Desk Accessories within the THINK Pascal debugger)
- The dialog routines were borrowed from DialogUtils/DialogPresident module in "ObjectDraw" sample project (mostly just to provide nice default button roundrect drawing for System 6, and for shortcuts for dialog item string setters/getters)

Also, the "NewBitMap" function is borrowed from MacTech/MacTutor sample (also used by John Calhoun's Glider).

All source code is included in this repository for fun research purposes, in case somebody wants to write a DA or Minesweeper in Pascal :) I didn't have time to clean up the messy code, so there's a bunch of questionable parts there. The entire THINK Pascal 4.0.1 project is included in AppleDouble format, as that's the native file format of MACE emulator.

TECHNICAL NOTE: Although the game should be compatible with System 6, there were repeated random crashes when testing it under System 6.0.7 in Minivmac that I did not have time to debug before end of #MARCHintosh. I was thinking it might be problem with A4 setup, but I did manage to narrow it down a bit that it was not the issue (the last discovery when I had time to debug the System 6 version was that for some reason PBRead randomly only reads 512 bytes of highscores even though 780 bytes are requested, causing the scores to get partially zeroed out. Bigger problem was though the corruption of DRVR code, seeming as if host application data would end up getting copied over part of the DRVR code. I will someday get back to this, when I have time.

DISCLAIMER: This software may (and most likely does) have bugs, so use at your own risk! Avoid running in a production environment, and keep backups of whatever system you're testing this game on, in case there is data loss. I'm not liable for any data loss, or if the mines blow up your computer!

More information about MACE: https://mace.software
