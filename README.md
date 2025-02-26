# smd_ida_tools2
The IDA Pro tools for the Sega Genesis/MegaDrive romhackers

## Contains
1. ROM files loader
2. Z80 sound drivers loader
3. IDA Pro debugger for Sega Mega Drive/Genesis roms and Z80 sound drivers

## How to compile
1. Edit paths to your IDA/SDK installation according to your real paths
2. Use **Visual Studio 2022** with integrated vcpkg (it will download and compile all dependencies) to compile

## How to use
1. Put files from the `loaders` dir into the corresponding IDA folder
2. Put files from the `plugins` dir into the corresponding IDA folder
3. Open ROM in IDA
4. Choose `GensIDA debugger plugin` or `Z80 debugger plugin` debugger
5. Press `F9` to start a debugging process
6. Run `gens_68k.exe` or `gens_z80.exe` from `gens` folder, choose a ROM
7. Debug!

## Available assemblers
![image](https://user-images.githubusercontent.com/7189309/214719964-66c90f66-fedc-4705-94af-d0fce28270b4.png)

## How to produce a compilable asm listing
1. Press `Shift+J` to choose how to mark your data range. Or mark it by yourself using available methods (listed below)
2. Press `File->Produce file->Create LST file...`. Save `.lst` listing file
3. Use any of AS/VASM/ASM68K assemblers to compile your `.lst` file. You can also use `assemble_as.bat`, `assemble_vasm.bat` or `assemble_asm68k.bat` for that

![image](https://user-images.githubusercontent.com/7189309/214720698-ba674d23-487e-4307-8594-d4b7b2618143.png)

## Data marking methods
All methods are specified like `START_TAG` - `END_TAG` (except `ORG` tag), where `START_TAG` must be specified using **Anterior comment** (`Ins`) at the first line of your data, and `END_TAG` must be inserted using **Posterior comment** (`Shift+Ins`).

Available TAGS:
1. `BIN "relative/path.bin"`. This tag allows you to save some data array (or even code) to the `"relative/path.bin"` during the extraction. It also inserts `binclude "relative/path.bin"` line to your listing.
2. `INC_START "relative/path.inc"` - `INC_END`. The same as the previous item, except it just stores copies all lines between these tags as is and inserts the following line: `include "relative/path.inc"`.
3. `DEL_START` - `DEL_END`. These tags can be used if you want to cut some lines from the resulting asm listing.
4. `ORG $SIZE`. This tag inserts `org $size` directive line in the output.
