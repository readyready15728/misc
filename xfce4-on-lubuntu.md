# Xfce4 on Lubuntu
## My further travails with Xfce4 after finding Enlightenment dissatisfactory

The original story is that I thought LXDE was a little too boring and wanted to
use a more ＡＥＳＴＨＥＴＩＣ window manager / desktop environment, opting
initially for Enlightenment. However, Enlightenment proved a bit rough around
the edges and I then opted for Xfce4. It is indeed better overall.

First thing I did was chuck out the desktop icons because I consider them
redundant clutter. To do this, I right-clicked on the desktop, then headed over
to Desktop Settings then Icons and deselected all the default icons.

Then it came to setting up xscreensaver as I had done before. Here it was
necessary to go into Xfce4's settings manager (available in Settings in the
Xfce4 applications menu under Settings Manager or through
`xfce4-settings-manager`) and then Session and Startup. Well this time I
*didn't* have to do anything special, as was the case with
[Enlightenment](enlightenment-on-lubuntu.md), because apparently Xfce4 found
*another* .desktop file for xscreensaver that I missed and which was lurking in
`/etc/xdg/autostart` which apparently overrode the one I put in
`/usr/share/applications`. Good enough, I guess, though I'm not sure what I'm
doing to do with the other one. Maybe I'll just delete it.  There was a bunch
of other shit in the available autostart applications that I didn't need, to my
memory, a Bluetooth manager and Light Locker (redundant). So I turned it all
off.

The next issue to deal with was how GNOME Terminal looked wrong. The background
was white! I went into Edit → Profile Preferences → Colors and saw that GNOME
Terminal was using colors from the system theme. I certainly didn't want what
Gtk themes I could and couldn't use be tethered to the desired appearance of
GNOME Terminal, so I turned that off and got my familiar white-on-black scheme
back. Then I messed around with the palette settings a bit and got a pleasant
surprise: the Rxvt palette had much bolder colors than I was used to. Something
I also recommend doing at this point is setting up translucency if you haven't
already. There are 100 ticks on the slider and I recommend 15% translucency.

The next thing I wanted to do was change the background. This can also be done
through Desktop Settings, which was mentioned earlier. I like the default
mousey picture but I like my custom "NEUROPOL" background even more. If you
have an images folder *filled* with images, *don't* use it. Xfce4 will go
through an expensive process of coming up with a thumbnail of every image.
Better to create a subdirectory, or some other directory, and put your few
background(s) in there.

Then I wanted to set up the panels how I wanted them. Xfce4 features a default
layout very similar to Mac OS X, with a thin strip at the top and a fatter
application launch bar at the bottom. This is not a bad setup but it's one I
wanted to perfect. So I configured the top panel to be like it was in LXDE (on
the bottom), with the following ordering from left to right:

1. Applications Menu
2. Workspace Switcher
3. Window Buttons
4. A very important Separator, transparent and with Expand checked, because the
alternative is an an ugly panel all left-justified
5. Notification Area
6. Clock (in 24 hour mode)
7. Action Buttons (these give the ability to log out, reboot and so
on)

I didn't like the appearance of the first and last items, so I right-clicked to
get to Properties in both cases and eliminated the button title in the first
case and changed the appearance of the action buttons to ... well, actually,
"Action Buttons", from the default of "Session Menu".

After this I turned my attention to the bottom panel. I completely gutted it
and added only launchers for apps, one per launcher. These were, from left to
right:

1. GNOME Terminal
2. Thunar
3. Firefox
4. LXTask
5. Xfce4 Settings Manager

...and after that a bunch of other stuff that's more volatile and may be
changed around. Additionally I went into Panel Preferences and set the panel to
hide itself "Intelligently".

Next, I wanted to ensure that Midnight Commander can use `Alt-Tab`. In the
settings manager, I headed over to Window Manager → Keyboard and assigned
window cycling to `Ctrl`-Tab instead.

There was also a second modification to keyboard behavior, namely the Compose
key. Initially, I was under the impression that this is something that requires
a .desktop in `$HOME/.config/autostart`, but it's easier than that in fact. I
went into Keyboard in the settings manager and then Layout and turned off Use
system defaults, enabling me to set up Caps Lock as the Compose key.

Feeling pretty good about my results so far, of course a new issue cropped up,
and that was Mudlet flashing in the task bar whenever any new messages came in.
I was not having this issue with LXDE. Anyway, I found a Mudlet setting to
disable this behavior.

And now for some cosmetic but nice changes: I went into Appearance from the
settings and selected Xfce-4.6 for (Gtk) style and Lubuntu-dark-panel for
icons.

While I was doing all of this I noticed that the settings manager also includes
Preferred Applications so I made sure Firefox was my preferred browser and
GNOME Terminal my preferred terminal emulator.

And while I was looking for something else entirely I noticed that, by
right-clicking some part of the top panel other than the task bar (ironically
ineffective) then going to Panel → Panel Preferences → Items, selecting "Window
Buttons" (i.e. the task bar) and then clicking the gear icon, it becomes
possible to set the sorting order to None, allow drag-and-drop, which is useful
because I feel compelled to organize my task bar and greatly appreciated having
this feature when I was using LXDE. I'm glad Xfce4 supports it as well, though
it should be default behavior.
