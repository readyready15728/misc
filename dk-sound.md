# Sound in Dungeon Keeper Gold

When I bought Dungeon Keeper Gold from GOG and tried to start playing it, I
noticed that the sound stuttered horrifically. A lot of people seem to have
this same problem. What appears to work for many of them is going into
`dosboxDK.conf` in the installation folder and changing `cycles=80000` to
`cycles=max`. I did not find this effective; in fact it made things even worse.
What I did find effective was in fact manually bringing cycles allocated down
to 40000 with `Ctrl-F11` to see what would solve the problem and then entering
that into `dosboxDF.conf` so that I would not have to repeat myself as
`cycles=40000`. It is possible that other values of `cycles` may be appropriate
on other platforms, but in any case fixed cycles may succeed where other
solutions fail.
