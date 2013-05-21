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

Note that naming the mod in the style of d130.pack may be important
for the game to actually load the it. Also note that I haven't tried
stacking several mods.
