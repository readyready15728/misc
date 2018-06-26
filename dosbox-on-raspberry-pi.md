# DOSBox on Raspberry Pi
## Configuring DOSBox for optimal performance

The Pi, especially more recent models, can run DOS games with DOSBox pretty
well but getting the best performance can require a bit of black magic. I set
the fairly ambitious goal of running a very popular real-time strategy game
from the DOS era, [The Settlers
II](https://en.wikipedia.org/wiki/The_Settlers_II), and I was finally able to
get decent results, just as good as on a desktop, though there was some
bending over backwards to get this outcome.

One go-to solution that I ultimately decided against (for now) is
overclocking. This is partly out of lack of knowledge about overclocking (and
Raspbian on Pi 3 doesn't have have instant overclocking in `raspi-config`
anymore) and partly out of concern for the device (though I did try it a
little and the device wouldn't boot). A more important factor is that Pis vary
in their capacity for overclocking—or so I've heard—so, if I came up with a
performance solution requiring overclocking and somehow broke the Pi I have
now, the new one might not support this solution. What I can do in software is
much more reliable.

The most fundamental change I made was custom compilation of DOSBox. I found
out that the most important features were enabling dynamic recompilation and
using SDL instead of GL. To this I thought all the other more general
optimization flags that would be used for other software should be added. I
found a [guide](https://www.raspberrypi.org/forums/viewtopic.php?t=95421) that
explains how to do what I wanted to do but it is from 2015 and therefore kind
of outdated. I looked into which compilation flags are recommended for
Raspberry Pi 3 and found some
[advice](https://www.raspberrypi.org/forums/viewtopic.php?t=144115). To be
clear, this is what I ended up doing before running `make`:

```bash
CXXFLAGS="-O3 -mcpu=cortex-a53 -mfpu=neon-fp-armv8 -mfloat-abi=hard -funsafe-math-optimizations" ./configure --disable-opengl
```

On that note, I am not currently using RetroPie, preferring to do things
piecemeal, but somebody pointed me to the [script RetroPie uses to compile and
install
DOSBox](https://github.com/RetroPie/RetroPie-Setup/blob/master/scriptmodules/emulators/dosbox.sh)
which contains relevant information. This should continue to be a valuable
source of compilation pointers into the future, as new models of the Pi are
released. Of course, the particulars of compilation should always be kept up
to date with the model in question.

After compiling and installing the custom DOSBox, I focused more intensely on
something I had exposed myself to earlier, namely DOSBox configuration. The
suggestions in the 2015 compilation guide are a good template (see
[here](https://www.codingepiphany.com/2013/06/27/some-configs-to-increase-dosbox-performance-on-raspberry-pi/)
also), but one might want to alter things like the value of `frameskip` and so
on. `cycles` is a setting that may need special tailoring as no two games are
perfectly alike in their processing requirements. (Moreover, some developers
unwisely tied execution speed directly to a specific CPU model rather than
using the system clock.) Also, just throwing more and more cycles at a lagging
game will actually make it perform worse for whatever reason. I recommend
something like the following:

```
cycles=10000
cycleup=1000
cycledown=1000
```

This means that Ctrl-F11 and Ctrl-F12 will step up and down, respectively, in
increments of one thousand, which is probably granular enough. Then, when you
find the ideal cycle setting, you can put it in the configuration file.

One might also want to go beyond some of the more spartan recommendations of
the compilation guide. I definitely wanted sound for *The Settlers II* and
this required that both Sound Blaster *and* MIDI were enabled.

Anyhow, when all was said and done, I was able to run the game from LXDE with
reasonable performance. The audio was lagging to some extent and the animation
was a bit sluggish but it was basically playable (at least in the early stages
without a whole lot of sprites). Still I wanted more. Then I remembered that
someone said something about DOSBox running even faster in the console,
without X. I tried this but keyboard functionality totally broke down with the
keys crazily mapped to completely different values and I had to pull the plug
on the Pi to restart it. After looking into the issue further, I found out
that this might be fixed by altering the DOSBox configuration setting
`usescancodes`. Since it was set to true in the [GOG.com](https://www.gog.com)
setup I was using, I set it to false and tried again. Things went without a
hitch. The performance was every bit as good as I had at home with perfect
sound and smooth animation. I couldn't run it in X expecting that kind of
performance but oh well.

One other thing I didn't need that might still be relevant: if there are
processes that can be killed that might be getting in the way, kill them. I'm
not sure how much it would really help in most circumstances, but it might.
