# USB Sound on Raspberry Pi
## Getting the frigging external sound card to work on Raspberry Pi

The built-in audio output on the Raspberry Pi 3 B was absolute garbage for me
so I bought one of these:

https://www.adafruit.com/product/1475

I looked at various tutorials and forum threads and cobbled together a
solution that actually worked for my model with Raspbian Stretch. The key was
looking at the output of `aplay -l`:

```
**** List of PLAYBACK Hardware Devices ****
card 0: ALSA [bcm2835 ALSA], device 0: bcm2835 ALSA [bcm2835 ALSA]
  Subdevices: 7/7
  Subdevice #0: subdevice #0
  Subdevice #1: subdevice #1
  Subdevice #2: subdevice #2
  Subdevice #3: subdevice #3
  Subdevice #4: subdevice #4
  Subdevice #5: subdevice #5
  Subdevice #6: subdevice #6
card 0: ALSA [bcm2835 ALSA], device 1: bcm2835 ALSA [bcm2835 IEC958/HDMI]
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 1: vc4hdmi [vc4-hdmi], device 0: MAI PCM vc4-hdmi-hifi-0 []
  Subdevices: 1/1
  Subdevice #0: subdevice #0
card 2: Device [USB Audio Device], device 0: USB Audio [USB Audio]
  Subdevices: 0/1
  Subdevice #0: subdevice #0
```

In other instructions, the USB audio becomes "card 1". Here, however, it is
"card 2".

I then edited `/etc/asound.conf`:

```
pcm.!default {
    type hw
    card 2
}
ctl.!default {
    type hw
    card 2
}
```

And the relevant part of `/usr/share/alsa/alsa.conf`:

```
defaults.ctl.card 2
defaults.pcm.card 2
```

I'm pretty sure I also had to right-click on the speaker icon in LXDE and
select "USB Audio Device". Not sure why and not sure how to do that from the
CLI either. Anyway it works now.

This page was especially useful in getting the USB audio card to work:

https://learn.adafruit.com/usb-audio-cards-with-a-raspberry-pi?view=all
