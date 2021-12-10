# FreeBSD Notes
## Notes on the venerable "Unix" operating system from Berkeley

* New users can be added to `wheel` for the purposes of `sudo`. (Needs to be enabled using `visudo`.)
* The Ports tree can be built using `sudo portsnap auto`.
* `sudo periodic daily weekly monthly` seems like the only way to update the `locate` DB safely. :/
* `sudo pkg remove vim-console` needs to happen before any compilation of Vim using Ports.
* `sudo pkg install py37-pip` (as of now) installs Pip for Python 3. (More recently FreeBSD has upgraded to Python 3.8.)
* `sudo dmidecode -t processor -t cache` more or less corresponds to `/proc/cpuinfo`.
* `dmesg` also works.
* `sudo portmaster --show-work www/nginx | less` helped me keep track of how much of my nginx build was finished. (Had to be installed separately using `pkg`.)
* `sudo make config` reconfigures a Port.
* Had to add `nginx_enable="YES"` to `/etc/rc.conf` to make it start every boot.
* Maybe look more into Portmaster?
* `sftp` broke from attempting to connect from my Linux box. What fixed the problem was putting `Subsystem       sftp    internal-sftp` in `/etc/ssh/sshd_config` then running `sudo service sshd restart`.
* `sudo portsnap fetch update` updates the Ports tree.
* `sudo make deinstall` uninstalls a Port.
* `sudo make rmconfig` restores default Port settings.
* `sudo make deinstall` followed by `sudo make reinstall` reinstalls a botched Port.
* Don't forget to restart the appropriate service after changing a lot of config files!
* `alias ls='ls -G'` makes for decent color output of `ls` like one would expect on Linux.
* Making a symlink to the latest version of Python 3 as `python3` can be useful.
* The OCaml stuff I want installed requires installation of `bash`.
* Assuming you are still reading, avoid Ports as much as possible.
* I was able to compile YouCompleteMe for Vim after replacing the offending
  obsolete checksum in `third_party/ycmd/cpp/ycm/CMakeLists.txt` with the one
  that actually was computed for the clang download. 
