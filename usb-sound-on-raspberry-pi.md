# USB Sound on Raspberry Pi
## Getting the frigging external sound card to work on Raspberry Pi

Mention device (GeneralPlus)

/boot/config.txt (not needed)
/etc/asound.conf
/usr/share/alsa/alsa.conf

https://learn.adafruit.com/usb-audio-cards-with-a-raspberry-pi?view=all
http://www.raspberryvi.org/posts/usb-audio.html

Maybe the desktop icon? Probably not (actually yes)

[    2.869490] usb 1-1.4: Manufacturer: GeneralPlus
[    2.873164] input: GeneralPlus USB Audio Device as /devices/platform/soc/3f980000.usb/usb1/1-1/1-1.4/1-1.4:1.3/0003:1B3F:2008.0003/input/input2
[    2.951752] hid-generic 0003:1B3F:2008.0003: input,hidraw2: USB HID v2.01 Device [GeneralPlus USB Audio Device] on usb-3f980000.usb-1.4/input3

pcm.!default {
    type hw
    card 2
}
ctl.!default {
    type hw
    card 2
}

defaults.ctl.card 2
defaults.pcm.card 2

Still not clear on how to make default
