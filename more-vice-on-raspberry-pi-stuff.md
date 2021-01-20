# More VICE on Raspberry Pi Stuff
## Finally got it working in full

There's a Snap package available for VICE. Unfortunately, I installed it and
the keyboard didn't work for some reason, so I had to compile from source.
Additionally, for C64 emulation, three ROMs need to be in place, as of the
current release, in `$HOME/.local/share/vice/C64`. These are `basic`,
`chargen` and `kernal`. They can be found here:

http://www.zimmers.net/anonftp/pub/cbm/firmware/computers/c64/

Mind the different versions out there!

Here was the first game I succeeded in getting to run:

https://www.myabandonware.com/game/enchanter-1ns

The "Smart attach" option at the top of the File menu in VICE was fine to get
`ENCHANT.D64` to load, though it took a while.

Now to figure out things like GEOS!
