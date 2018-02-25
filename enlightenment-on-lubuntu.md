# Enlightenment on Lubuntu
## My journey through getting an unsupported window manager to do what I want

I decided I was tired of having a "boring" desktop environment (LXDE) and that
I should have a more ＡＥＳＴＨＥＴＩＣ experience. A lot of the
ＡＥＳＴＨＥＴＩＣ window managers are tiling and I didn't want that. I also
definitely wanted tray icons. So I gravitated to Enlightenment, which I believe
was the original ＡＥＳＴＨＥＴＩＣ window manager.

Installing it is pretty innocent:

```
sudo add-apt-repository ppa:niko2040/e19
sudo apt install e17
```

The package includes an .xsession file for use with LightDM, so you can go
ahead and just change the session up in the top right. The icon specified in
the .xsession file doesn't display in LightDM properly. That annoys me, but
it's a minor issue. I may come back to it later.

Anyway, I fired up Enlightenment for the first time in over a *decade* and went
through some initial configuration steps. I've never seen a window manager do
that before and I thought it was pretty innovative. And it functions as a
compositor as well and that means I also get the modestly useful feature of
translucent terminal windows and push notifications.  But I had an issue right
away! When I went and opened GNOME Terminal I noticed immediately that the
rendering of the font in the toolbar and tabs just didn't *look* right, too
thin. I went searching for font issues with GTK and eventually found a solution
that works, which was putting the following in a file called
`$HOME/.Xresources`:

```
Xft.hintstyle: hintslight
Xft.hinting: 1
Xft.antialias: 1
Xft.rgba: rgb
```

The next thing I wanted to do was ensure that—notwithstanding the
extraordinarily dumb views of its creator—the xscreensaver daemon and MEGASync
clients were both autostarted. This was a little roundabout. It is possible to
autostart programs in Settings → Apps → Startup Applications—if an appropriate
.desktop file is available. This was available in the case of MEGASync but not
for xscreensaver. I did manage to find something to start with, though, namely
`/usr/share/xscreensaver/xscreensaver-daemon.desktop`. (Why the .desktop file
was there where it wouldn't be recognized is anyone's guess.) That was a start,
but I had to make one change, so I *copied* it into `/usr/share/applications`
and deleted the line that said `NoDisplay=true`, allowing the .desktop entry in
question to appear in the list of startup applications. That squared away my
autostart issues.

Something else I resolved while tackling these more difficult problems was
streamlining the shelf at the bottom of the screen. There was too much clutter
initially. I completely gutted the shelf and put gadgets back in the following
order:

1. Start
2. IBar (including, in this order, GNOME Terminal, PCManFM and Firefox, then
whatever else)
3. Pager
4. Tasks
5. Systray (disabled by default; needs to be enabled in Settings → Extensions →
Modules)
6. Clock (digital, no seconds, 24 hour mode)
7. System

This was the layout I had when I was using LXDE and I liked it.

The next issue was establishing a Compose key. I had been using Caps Lock
earlier. Mercifully, this was a simple matter of going into Settings → Input →
Keyboard and checking the relevant box. (And IIRC checking off another one—no
need for two Compose keys.)

Then came something that really rustled my jimmies. No matter what I did in
LXAppearance or in editing configuration files manually, I couldn't change the,
in my opinion, ugly default GNOME income theme for Gtk. After a lot of
searching I found out that this has to be done through Settings → Look →
Application Theme → Icons.

Another issue with keyboard input was the shortcut for cycling through windows.
I want Alt-Tab to be free for completion in Midnight Commander so I turned it
off as the cycling shortcut. After derping for a moment I realized it was
possible to *add* shortcuts and not just change existing ones (duh) and set up
Ctrl-Tab for this purpose.

A small but important change I added after this was going into Settings → Input
→ Edge Bindings and deleting all of them to prevent accidental change of
virtual desktop by mousing over the wrong thing.

An issue that is persistent for me at the moment is how the MEGASync client
won't enter the tray as it should. I should report this to the developers at
some point but for now my stopgap solution is changing the border style to the
default—if it's going to act like a regular window, I'm going to treat it like
one—and sending it to the last virtual desktop I never use so it isn't an
eyesore.
