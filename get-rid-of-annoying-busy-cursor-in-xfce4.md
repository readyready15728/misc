# Get Rid of Annoying Busy Cursor in Xfce4
## Get rid of annoying busy cursor in Xfce4

It kept happening when I opened Sage plots in Firefox. The recommendation was
to set `StartupNotify` to `false` in the correct `.desktop` file. The issue
was finding the right one. It wasn't anything for Firefox specifically but in
`/usr/share/applications/exo-web-browser.desktop`, which invokes Firefox.

Had I not figured this out I could have kept using `killall xfwm4` as it
automatically respawns.
