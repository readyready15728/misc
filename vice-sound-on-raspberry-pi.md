# VICE Sound on Raspberry Pi
## Immense pain in the ass no more

I compiled VICE for the Pi and all went well but for the fact that I had no
sound, which was of course unacceptable given that the primary target of VICE
is the Commodore 64, which had famously good sound capabilities in its day,
even being vital to some modern bitpop efforts now.

After doing some searching I found out the central issue was that VICE outputs
mono audio and Raspberry Pi only does stereo. That *was* the issue indeed but
the devil was in the details as always. The obvious thing to do was try to
enable stereo in the configuration file where the VICE documentation *says* I
should be able to change this, namely in `~/.vice/vicerc`. But VICE's
Commodore 64 emulator was very obviously not acknowledging my instructions
there. So I tried command line flags for a bit to no avail and then went
hunting through the menu system of the emulator, where all the sound options
were right in front of me. I found a constellation of settings that worked,
but I didn't know how to make it permanent. With a further look at the
documentation I found an approach that ultimately unraveled the mystery: it is
possible to dump the current configuration to the configuration file in the
emulator: it is possible to dump the current configuration to the
configuration file in the emulator. After I did this, I saw where the
configuration was *actually* dumped, which was `~/.vice/sdl-vicerc`. I then
made the changes to ensure that what I had achieved through the menu system
was made permanent:

```
SoundDeviceName="alsa"
Sound=1
SoundOutput=2
```

Briefly, `Sound=1` ensures that sound is enabled, `SoundOutput=2` forces
stereo and I used ALSA because PulseAudio is useless for the emulator in this
case, stereo audio or not. Other audio devices may be effective, just not this
latter one.
