# Adding ROMs

NextUI automatically creates a "Roms" folder at the SD card root containing folders for each console NextUI currently
supports. 

You can rename these folders however you like; however, you must keep the uppercase tag name in parentheses in
order to retain the mapping to the correct emulator (eg. "Nintendo Entertainment System (FC)" could be renamed to "Nintendo (FC)", "NES (
FC)", or "Famicom (FC)").

When one or more folder share the same display name (eg. "Game Boy Advance (GBA)" and "Game Boy Advance (MGBA)") they
will be combined into a single menu item containing the roms from both folders (continuing the previous example, "Game
Boy Advance"). This allows opening specific roms with an alternate pak.

## Disc-based games

To streamline launching multi-file disc-based games with NextUI place your bin/cue (and/or iso/wav files) in a folder
with the same name as the cue file. NextUI will automatically launch the cue file instead of navigating into the folder
when selected, e.g.

```
  Harmful Park (English v1.0)/
      Harmful Park (English v1.0).bin
      Harmful Park (English v1.0).cue
```

For multi-disc games, put all the files for all the discs in a single folder. Then create an m3u file in that folder (
just a text file containing the relative path to each disc's cue file on a separate line) with the same name as the
folder. Instead of showing the entire messy contents of the folder, NextUI will launch the appropriate cue file, eg. For
a "Final Fantasy VII" folder structured like this:

```
  Policenauts (English v1.0)/
    Final Fantasy VII (English v1.0).m3u
    Final Fantasy VII (USA) (Disc 1).bin
    Final Fantasy VII (USA) (Disc 1).cue
    Final Fantasy VII (USA) (Disc 2).bin
    Final Fantasy VII (USA) (Disc 2).cue
    Final Fantasy VII (USA) (Disc 3).bin
    Final Fantasy VII (USA) (Disc 3).cue
```

The m3u file would contain just:

```
  Final Fantasy VII (USA) (Disc 1).cue
  Final Fantasy VII (USA) (Disc 2).cue
  Final Fantasy VII (USA) (Disc 3).cue
  ...
```

When a multi-disc game is detected the in-game menu's Continue item will also show the current disc. Press left or right
to switch between discs.

NextUI also supports chd files and official pbp files (multi-disc pbp files larger than 2GB are not supported).
Regardless of the multi-disc file format used, every disc of the same game share the same memory card and save state
slots.

## Collections

A collection is just a text file containing an ordered list of full paths to rom, cue, or m3u files. These text files
live in the "Collections" folder at the root of your SD card, eg. "/Collections/Metroid series.txt" might look like
this:

```
  /Roms/GBA/Metroid Zero Mission.gba
  /Roms/GB/Metroid II.gb
  /Roms/SNES (SFC)/Super Metroid.sfc
  /Roms/GBA/Metroid Fusion.gba
```

If you disable all viable folders under 'Roms', the 'Collections' folders contents will populate the main screen instead
of being nested in the 'Collections' folder in the UI.

## Display names

Certain (unsupported arcade) cores require roms to use arcane file names. You can override the display name used
throughout NextUI by creating a map.txt in the same folder as the files you want to rename. One line per file, `rom.ext`
followed by a single tab followed by `Display Name`. You can hide a file by adding a `.` at the beginning of the display
name. eg. The 'Collections' folder needs its own map.txt file as well.

```
  neogeo.zip	.Neo Geo Bios
  mslug.zip	Metal Slug
  sf2.zip	Street Fighter II
```

# Adding BIOS

Some emulators require or perform much better with official bios. NextUI is strictly BYOB. Place the bios for each
system in a folder that matches the tag in the corresponding "Roms" folder name (eg. bios for "Sony PlayStation (PS)"
roms goes in "/Bios/PS/"),

Bios file names are case-sensitive:

```
   FC: disksys.rom
   GB: gb_bios.bin
  GBA: gba_bios.bin
  GBC: gbc_bios.bin
   MD: bios_CD_E.bin
       bios_CD_J.bin
       bios_CD_U.bin
   PS: psxonpsp660.bin
 MGBA: gba_bios.bin
  PCE: syscard3.pce
  PKM: bios.min
  SGB: sgb.bios
```

# Adding Cheats

Cheats use RetroArch .cht file format. Many cheat files
are [here](https://github.com/libretro/libretro-database/tree/master/cht).

Cheat file name needs to match ROM name, and go underneath the "Cheats" directory. For example,
`/Cheats/GB/Super Mario Land (World).zip.cht`. When a cheat file is detected, it will show up in the "cheats" menu item
ingame. Not all cheats work with all cores, may want to clean up files to just the cheats you want.

# Adding BoxArt

NextUI looks for accompanying media for each emulator under /Roms/[Emulator]/.media folder.
Create the .media folder if not already present.
Put an image in PNG format with the exact same name as the ROM file.  
NextUI will automatically scale or resize the media file.

For example:

```
ROM: /Roms/Emulator/game.zip
Media: /Roms/Emulator/.media/game.png
```

# Adding Overlays

> [!IMPORTANT]
> Overlays are only supported for libretro emulators. Standalone emulators do not support overlays.

NextUI looks for accompanying media for each emulator under the `/Overlays/[System]` folder.
The `System` corresponds to the name of the Emu Pak specified in your Emulator folder name within parenthesis.
In this folder you can add 5 overlay PNG files, named overlay1.png to overlay5.png.

For example:

```
# For /Roms/Game Boy Color (GBA)
/Overlays/GBA/overlay1.png
/Overlays/GBA/overlay2.png
/Overlays/GBA/overlay3.png
/Overlays/GBA/overlay4.png
/Overlays/GBA/overlay5.png

# For /Roms/Super Nintendo (SFC)
/Overlays/SFC/overlay1.png
/Overlays/SFC/overlay2.png
/Overlays/SFC/overlay3.png
/Overlays/SFC/overlay4.png
/Overlays/SFC/overlay5.png
```

When in game, hit the `Menu` button and navigate to `Options -> Frontend`. This will display
an overlay setting to choose between overlay 1 to 5 or none.

# Adding Emulator Icons

Similarly, create .media under the appropriate folders to create icons for Emulator, Collection, Tools and other menu
items.

For example:

```
SD_CARD
├─ .media/
│  ├─ Collections.png
│  ├─ Recently Played.png
├─ Collections/
│  ├─ .media/
│  │  ├─ Collection 1.png
│  │  ├─ Collection 2.png
├─ Roms/
│  ├─ .media/
│  │  ├─ GBA.png
│  │  ├─ SFC.png
│  │  ├─ Custom Emulator Name (GBC).png
│  │  ├─ etc...
├─ Tools/
│  ├─ .media/
│  │  ├─ tg5040.png
```