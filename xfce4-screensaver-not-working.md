# Xfce4 Screensaver Not Working
## Dropped the ball, maintainers...

I did an update on Mint and the screen going blank and presenting with a lock
screen as it should went away. Well, after nearly posting on the official
forum, I finally figured out what to do. The upgrade migrated to
`xfce4-screensaver`. However, the upgrade did not install `xfce4-screensaver`!
What I did was make sure `xfce4-screensaver` was actually installed then go
into "Session and Startup" and make sure "Light Locker" and the correct
"Screensaver" (and no other "Screensaver"s) were selected and after a reboot I
was good to go.
