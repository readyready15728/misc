# FreeBSD Notes
## Notes on the venerable "Unix" operating system from Berkeley

* New users can be added to `wheel` for the purposes of `sudo`. (Needs to be enabled using `visudo`.)
* The Ports tree can be built using `sudo portsnap auto`.
* `sudo periodic daily weekly monthly` seems like the only way to update the `locate` DB safely. :/
* `sudo pkg remove vim-console` needs to happen before any compilation of Vim using Ports.
* `sudo pkg install py37-pip` (as of now) installs Pip for Python 3.
* `sudo dmidecode -t processor -t cache` more or less corresponds to `/proc/cpuinfo`.
* `dmesg` also works.
* `sudo portmaster --show-work www/nginx | less` helped me keep track of how much of my nginx build was finished. (Had to be installed separately using `pkg`.)
* `sudo make config` reconfigures a Port.
* Had to add `nginx_enable="YES"` to `/etc/rc.conf` to make it start every boot.
* Maybe look more into Portmaster?
* `sftp` broke from attempting to connect from my Linux box. What fixed the problem was putting `Subsystem       sftp    internal-sftp` in `/etc/ssh/sshd_config` then running `sudo service sshd restart`.
