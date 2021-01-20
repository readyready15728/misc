# SML Installation on Ubuntu
## Working around an unbelievably shitty build process and documentation

>Create an SMLROOT directory for the installation (e.g., SMLROOT=/usr/local/sml) in a place where it is appropriate to install software packages.

Lie, it's `$INSTALLDIR`. And you can't set it in the environment and have it take effect. It gets clobbered by `install.sh`. I had to manually set `INSTALLDIR=/usr/local` in the script to get the desired outcome.
