# MS-DOS on DOSBox
## Reviving the operating system that won out through skullduggery

As I chose to go about doing this, I first created a directory dedicated to
the task in question.

Then, therein, I created an image that serves as a virtual hard drive. 256 MB
is a sensible default. This can be done accordingly:

```bash
dd if=/dev/zero of=ms-dos.img bs=1M count=256
```

The next thing I did was to prepare a DOSBox configuration file for MS-DOS. I
wanted to keep it separate from the main DOSBox configuration file so that I
can launch MS-DOS programs without having MS-DOS launch. As of this writing, the
location of the main DOSBox configuration file was
`~/.dosbox/dosbox-0.74.conf`. I copied it into my MS-DOS directory with the
name `dosbox-0.74-ms-dos.conf`.

Before making any changes to this configuration file, I needed to procure
images of the MS-DOS 6.22 installation disks. There is a great website called
[WinWorld](https://winworldpc.com) that has the images for [MS-DOS 6.22 Plus
Enhanced Tools](https://winworldpc.com/download/c38fc38d-68c2-bbe2-80a6-4b11c3a4c2ac).
This will be downloaded as a 7zip archive. I used `p7zip -d` to extract it and
then moved the following files from the directory that was created by
extracting the archive into the parent MS-DOS directory:

* `Disk1.img`
* `Disk2.img`
* `Disk3.img`
* `Suppdisk.img`

The disk images now being immediately available, the next step was to alter the
section all the way at the bottom of the configuration file, `[autoexec]`.
Lines after `[autoexec]` will be treated as though they were DOSBox commands
in an actual `AUTOEXEC.BAT`. This is what I added there:

```
mount Z .
Z:
imgmount 2 ms-dos.img -size 512,63,16,520 -t hdd -fs none
boot Disk1.img Disk2.img Disk3.img -l a
```

It's not clear what the purpose of `2` after `imgmount` is. The only
information I can seem to find without digging through the DOSBox source code
is that it signifies master (as opposed to slave) drive. As far as I
understand things, the first three comma-delimited numbers following `-size`
never change, but the fourth does if one opts for a different image size than
256 MB. If a different size is desired, multiply the desired number of
megabytes by 2.03125 and (I guess) round to the nearest integer.

In any case, what these lines do, essentially is:

* Make the current directory the `Z:` drive
* Switch to the `Z:`
* Prepare the image as a blank hard drive
* Turn on the virtual machine and make the MS-DOS 6.22 installation disks
  available to boot from the `A:` drive.

With these preparations in place, I started the virtual machine like so:

```bash
dosbox -conf dosbox-0.74-ms-dos.conf &
```

From here the installation was fairly straightforward. I just did what made
sense and got the message "Reboot requested, quitting now". It didn't look
like the installation had completed so I thought an error occurred. It wasn't
an error though; all I had to do was repeat the above launch of DOSBox. From
there, installation was a breeze. The only issue is that, because a physical
floppy drive and floppy disks aren't present here, DOSBox needs to be told
which image to use. When I was asked for disk 2, I pressed `Ctrl-F4` to load
the second image and again when disk 3 was asked for.

But wait! The supplemental disk still hasn't been installed. Now that MS-DOS
has been installed, the `[autoexec]` section needs to be changed to this:

```
mount Z .
Z:
imgmount C ms-dos.img -size 512,63,16,520 -t hdd -fs fat
boot Suppdisk.img -l c
```

The system will now boot from the `C:` drive rather than the `A:` drive.
Apparently, DOSBox will assign `Suppdisk.img` to the `A:` drive by default. To
install the supplemental disk, I typed `A:` to switch to the `A:` drive
(because this has to be done; can't be done from the `C:` drive) and then
`SETUP C:\DOS`. VGA was the appropriate graphics setting and I overwrote all
the files. After this step is done, `Suppdisk.img` after `boot` can be removed
from the configuration file as it is no longer needed.

Having followed all these steps, I finally attained a full installation of the
last official standalone release of one of the mostly widely used operating
systems ever released. But there was one glaring issue remaining: how can I
install other software? If I could find installation disk images, then it
would be no harder than what has already been done. But the software I would
most like to use in an MS-DOS environment (i.e. games) is usually not
distributed in this format. Because getting Internet to work on MS-DOS appears
to be a very sketchy prospect, I would need to access the contents of the
image directly. After doing a little poking around, I found a straightforward
solution. I created a directory called `mnt` in the main MS-DOS directory and
mounted the image, like so:

```
sudo mount -t msdos -o loop,offset=32256 ms-dos.img mnt
```

Why `offset=32256`? Here is the output of running `fdisk -l ms-dos.img`:

```
Disk ms-dos.img: 256 MiB, 268435456 bytes, 524288 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0x00000000

Device      Boot Start    End Sectors   Size Id Type
ms-dos.img1 *       63 524159  524097 255.9M  6 FAT16
```

The start sector, numbered 63, has to be multiplied by the sector size, 512,
so that `mount` knows where to look for the partition.

And why `sudo`? Only root users can mount with options. Additionally, all of
the files in the image will have root ownership and this can't be changed, so
`sudo` will be required for any installations or removals to be done. When
direct access to the MS-DOS image is no longer desired, use `sudo umount mnt`
to release that access.

Having followed all these steps, I finally attained a full MS-DOS installation
to which new software can be added. I'm still having an issue with installing
new software from multiple disk images but I may be able to clear that hurdle
as well at some point in the future.
