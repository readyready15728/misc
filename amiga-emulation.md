# Amiga Emulation

* Log in to OAGD / Open Retro on FS-UAE Launcher to gain access to the many
database entries for Amiga games with their associated downloads.
* It does not appear to be possible to delete game entries in FS-UAE Launcher
because changes made to the local .ini file and SQLite database will be
updated on next login from the server. However, if you delete local floppy disk
images containing a certain game and need to restore them, put them in the
FS-UAE downloads directory and do Update File Database.
* Install Kickstart ROMs for better compatibility. The replacement ROM can
only go so far. In particular, for gaming, 1.3 and 3.1, I was once told, are
especially important.
* The Amiga 500 was the most popular of the series. It's a sensible default
for settings and searches for documentation.
* FS-UAE Launcher actually includes a save disk for each configuration so you
don't have to set your own up, assuming everything can fit on it. To use it,
hit F12 and use one of the empty slots under Removable Media. (N.b. there has
to *be* an empty slot in the first place. If your game uses two floppies then
you need to add at least one more floppy drive to use this feature.)
* If the floppy sounds annoy you, you can turn those off in the full settings
menu.
* Clean Up and Snapshot are useful features of the Amiga Workbench for
arranging icons. (Hint: right click with window in question focused and
navigate to menu.) Clean Up will arrange the icons into a grid and Snapshot
will "freeze" the current position of icons that have been selected.
* Screenshot directory can be changed in Advanced Setting in FS-UAE Launcher
with, say, `screenshots_output_dir = ~/Pictures`.
* `joystick_port_1 = nothing` needs to be in settings for the cursor keys to
function properly. This is recommended to be used on a per-config basis only,
not globally.
* The default color palette in Workbench is ugly. On Workbench 2.1, at least,
this can be changed by going into Colors under Tools and using the following
palette: EEE, 898, 131, 282 for a nice green theme. Something similar, but even
better, can be done in 3.1 by going to Prefs and then Palette but here decimal
RGB triplets are used: (237, 237, 237), (18, 50, 18), (136, 153, 136), (34,
136, 34). Then for enhanced legibility, assign the colors to the different
roles as follows:
    * Important Text: #4
    * Bright Edges: #3
    * Dark Edges: #2
    * Active Window Title Bars: #4
    * Active Window Titles: #1
    * Menu Background: #2
    * Menu Text: #1

    Finally click Save.
* Populous appears not to cooperate well with any version of Workbench and
should just be run on its own; the same may be true of other games. (What if
it's an issue of not enough memory? Perhaps this could be configured around.
Would WHDLoad fix it maybe?)
* Consider installing ClassicWB? (What are the real advantages?)
* If a program bugs you about the lack of an FPU, then use custom configuration
to set `fpu` to one of the options that you can find in
`src/fs-uae/config-hardware.c` in the FS-UAE source. (Look for the variable
`uae_fpu_model` to see your options. Alternatively, you can change the CPU in
FS-UAE Launcher because CPU settings entail FPU settings.
* [WhichAmiga](http://aminet.net/package/util/moni/WhichAmiga) can be
incredibly useful for diagnostic purposes; it gives all major data about your
(emulated) hardware and software.
* Use `EndCLI` to quit a running instance of AmigaDOS.
* Installed libraries go in the top-level `Libs` folder.
* If you installed a library already and a program is still bugging you about
it not being there, try alternative versions of the same. Also use the Linux
program `strings` to see what other libraries it might require.
* Just because it's there in the file system doesn't mean Workbench sees it.
Workbench needs an .info file to see things. The utility
[AddIcon](http://aminet.net/package/util/wb/AddIcon) can help with this.
(Actually, no, that wasn't quite right: Workbench *can* see the entire
contents of a directory if you go to Window → Show → All Files. I still need
to figure out getting associations sorted out properly if it can be done,
though.)
* `/` means "parent directory", the same as `..` does everywhere else in
computing today.
* `PATH` can be used to add to the search path in a single AmigaDOS instance;
`ASSIGN` can be used to add to it globally. (For more information on that,
see [here](http://wiki.amigaos.net/wiki/AmigaOS_Manual:_AmigaDOS_Command_Examples#Changing_the_Search_Path).
This does not appear to be compatible with paths containing spaces, so don't
use them.
* `MAKEDIR` is the equivalent of `mkdir`.
* `RENAME` does move operations. It can be even be used with the target
filename omitted, like so: `RENAME file directory`.
* If you enable emulation of the Toccata sound card and install
`toccata.library` (see [here](http://aminet.net/package/util/libs/toclib12),
the CPU appears to be relieved of some of the burden of playing sound
(presumably because of the DSP) for playing software that supports Toccata.
What this means, for example, is that, for me,
[Eagleplayer](http://bax.comlab.uni-rostock.de/~bj/software/eagleplayer/) will
play .wav files normally under my install of Workbench 3.1 on Amiga 1200 if
Toccata Amplifier is enabled but MP3 playback continues to stutter and lock up
the system. :( I'm still looking into what can be done about this. (Issue
apparently resolved; see below.)
* The following very, *very* specific constellation of FS-UAE settings enables
virtually perfect MP3 playback in Eagleplayer, for me at least:
    * JIT enabled
    * 68040-NOMMU CPU chosen (because JIT doesn't support MMU anyway)
    * Toccata emulation enabled
    * `toccata.library` installed in `Libs`
    * Toccata Amplifier enabled
* If you see an install script written in what looks like some kind of Lisp,
you need [Installer](http://aminet.net/package/util/misc/Installer-43_3) to
run it.
* Motherboard and Zorro III memory can apparently be used to go over and above
what FS-UAE will support in fast RAM.
* FS-UAE can work with .dms demo files directly, but they don't necessarily
play along well with Workbench.
* Ctrl-C can be used in the CLI to terminate an Amiga binary (though it may not
have effect, at least immediately); the equivalent for an AmigaDOS script is
Ctrl-D.
* There are a number of other useful keyboard shortcuts in the CLI for some
versions of Workbench:
    * Ctrl-W: deletes one word backwards
    * Ctrl-X: deletes entire current line
    * Ctrl-K: "kills" to end of line
    * Ctrl-Y: pastes kill buffer
    * Ctrl-U: deletes backwards to start of line
    * Ctrl-S: suspends output
    * Ctrl-Q: resumes output
    * Ctrl-\: ends CLI instance
* Universal wildcard on Amiga is #?, not \*. (\* stands for the keyboard
and current screen; for example `COPY filename to *` will print contents
of said file to console.)
* "To instruct Amiga DOS to search through the directories from the root
(top-level) directory of a volume (disk or partition), you type a colon (:)
at the beginning of the file description."
