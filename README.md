# Minesweeper DA
This is a quick fun project I quickly hacked up for #MARCHintosh 2025, a minesweeper clone implemented as Desk Accessory (DA) for older 68K Macs.

![minesweeper](https://github.com/user-attachments/assets/130b25fb-be0b-4bac-9d47-c7ac9e3a307d)

I always wanted to write my own version of Minesweeper, and doing it as a Desk Accessory felt like a fun way to do it, given how simple the game is (akin to the "Puzzle" game Apple bundled with older Mac system versions).

This project was almost completely (99.9%) developed under MACE without using other emulators or real hardware:
- Using THINK Pascal 4.0.1 to write, debug the code and build final DA
- ResEdit 2.1.3 to create all resources and draw the graphics. All graphics were hand-drawn using 100% ResEdit 2.1.3 to mimic the original Windows 3.x minesweeper as closely as possible, with some "mac-like" modifications to them :)
- Only external tools used was Compact Pro & Dropbin running in Basilisk2 (as I didn't have time to figure out why CompactPro fails to create new archives under MACE and instead fails on resource loading error)

After compiling, this desk accessory was tested briefly running System 7.x in other emulators, and MacOS 9.x on real hardware.

Although game code is original, there's a couple bits of sample code from the THINK Pascal Demo application samples:
- The Desk Accessory project foundation was based on "Hex Dump DA" sample project (especially the DA Shell program used to test Desk Accessories within the THINK Pascal debugger)
- The dialog routines were borrowed from DialogUtils/DialogPresident module in "ObjectDraw" sample project (mostly just to provide nice default button roundrect drawing for System 6, and for shortcuts for dialog item string setters/getters)

All source code is included in this repository for fun research purposes, in case somebody wants to write a DA or Minesweeper in Pascal :) I didn't have time to clean up the messy code, so there's a bunch of questionable parts there. The entire THINK Pascal 4.0.1 project is included in AppleDouble format, as that's the native file format of MACE emulator.

TECHNICAL NOTE: Although the game should be compatible with System 6, there were repeated random crashes when testing it under System 6.0.7 in Minivmac that I did not have to debug before end of #MARCHintosh. I was thinking it might be problem with A4 setup, but I did manage to narrow it down a bit that it was not the issue (the last discovery when I had time to debug the System 6 version was that for some reason PBRead randomly only reads 512 bytes of highscores even though 780 bytes are requested, causing the scores to get partially zeroed out. Bigger problem was though the corruption of DRVR code, seeming as if host application data would end up getting copied over part of the DRVR code. I will someday get back to this, when I have time.

DISCLAIMER: This software may (and most likely does) have bugs, so use at your own risk! Avoid running in a production environment, and keep backups of whatever system you're testing this game on, in case there is data loss. I'm not liable for any data loss, or if the mines blow up your computer!
