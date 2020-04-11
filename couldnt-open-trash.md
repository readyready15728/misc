# Couldn't Open Trash
## Dammit

I just had this issue with how I couldn't open the trash folder in any file
manager on Ubuntu. "Timeout was reached" was the error message displayed by
two of them. `rm -r ~/.local/share/Trash/*` didn't do the trick and all of the
files therein were owned by my user and group so `sudo` was unnecessary. One
of the diagnostic threads mentioned gvfs version so I figured something was
the matter with that and sure enough killing the offending `gvfs-trash`
process was enough to fix the issue without necessitating a reboot.
