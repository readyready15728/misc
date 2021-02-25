# Pharo on Raspberry Pi
## "You did it. The crazy son of a bitch, you did it."

I had pretty much thrown in the towel on the prospect of ever running Pharo on
my Pi 400 and ironically settling for Squeak led me to the solution. The
official Squeak 5.3 bundle for 32-bit ARM segfaults, which led me to the (as
of this writing)
[latest virtual machine release
page](https://github.com/OpenSmalltalk/opensmalltalk-vm/releases/tag/202003021730).
I was able to get Squeak to run from separately downloaded image, change and
source files with the "stack" VM release. (The "cog" release also segfaulted.)

Looking through these releases I saw there was also a VM for Pharo, same
architecture. (By the way, that release is **NOT** in any of the release files
for Pharo's official [pharo-vm](https://github.com/pharo-project/pharo-vm)
repository, so looking there would have gotten me nowhere!) I was intrigued
and attempted to do with that Pharo VM what I did with Squeak. More
segfaulting.

After some Google searching, I read that instability in the behavior of the VM
over time caused the same issue so I tried an earlier release. It *almost*
worked but for complaint about the VM being too old and an error with
`LGitLibrary` not being able to find a shared library. Further research into
that problem revealed that `libgit2.so.0` (or alternatively just `libgit2.so`)
was missing. What ended up solving the issue was going into
`lib/pharo/5.0-201901172323` and linking the system library like so: `ln -s
/usr/lib/arm-linux-gnueabihf/libgit2.so.0.27.7 libgit2.so.0`.

The other issue about complaining of an old VM was solved by using a somewhat
newer VM. I tried one a few releases back and it solved both problems.

And, actually, after having done a bit of research, getting the newest VM from
[here](http://files.pharo.org/vm/pharo-spur32/linux/armv6/) (very confusing!)
and combining it with the latest image and ancillary files worked even better!
(Symbolic link still needed as before.)
