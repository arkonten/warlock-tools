# Modding tools for Warlock: Master of the Arcane

These are some rudimentary scripts for unpacking and repacking the
game's data files, and converting between the proprietary TXML version
2 format and XML.

## Requirements

Python 2.7, but higher 2.x versions should also be ok, maybe even
python 3.x.

Note: So far I've only run these scripts in Linux, but they should
work on Windows using its terminal.

## Short HOWTO

First of all, note that each of the tools has a --help. Read it!

Here's a short guide of how to create a rudimentary mod (sorry for
potential UNIX-isms):

1. Create a directory that will contain your modded files:

    mkdir my-mod-dir

2. Unpack some Warlock .pack file that contain files you want to
   modify, e.g. d110.pack seems to contain most game logic related
   data:

    python pack-util unpack d110.pack d110-unpack-dir

3. Convert the files you are interested in to human-readable XML, e.g.
   units.binary, which contains the unit stats:

    python txml-conv toxml d110-unpack-dir/units.binary units.binary.xml

4. Edit the units.binary.xml to your heart's content.

5. Convert the modded XML files to the binary format and put it in you
   mod's directory:

    python txml-conv fromxml units.binary.xml my-mod-dir/units.binary

6. Repeat 3-5 until you're satisfied.

7. Pack the mod:

    python pack-util pack my-mod-dir d130.pack

8. Place the new .pack file in your Warlock installation directory.

To uninstall the mod, simply remove the .pack file from Warlock's
installation directory.

Random notes
------------

* Naming the mods in the style of "dXXX.pack", where XXX is a number,
  seems to be important for the game to actually load the mod.

* The number XXX in "dXXX.pack" seems to have to do with .pack load
  order, so to have the mod override existing .pack files XXX must be
  the highest.

* Stacking several mods is so far untested.

* A mod that *changes* some existing game content file must be
  included in its entirety in the mod, i.e. the modded file (e.g.
  units.binary) can not only list the modified entries (e.g. the
  new/modified units), but must also include all unchanged data if you
  wish it to still be included in the game.

* Because of the above point, distributing such mods may infringe on
  the intellectual property of Ino-Co/Paradox. You have been warned!

* Side-stepping the above potential legal issue has a technical
  solution: instead of distributing complete .pack files that contain
  Ino-Co/Paradox's intellectual property, we could distribute only the
  steps necessary to re-create the modded .pack file from the original
  .pack files by automating steps 1-8 in the HOWTO. An additional tool
  for this must be written if this turns out to me necessary.
