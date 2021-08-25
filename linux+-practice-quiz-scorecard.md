# Linux+ Practice Quiz Scorecard
## Not even doing a subtitle for this one; you already know (XKO-004)

I took this one:

https://www.itexams.com/exam/XK0-004

Here are my answers and how I responded to getting things right or wrong:

1. In order to comply with new security policies, an administrator needs to prevent the SSH server from using insecure algorithms.
Which of the following files should be edited to accomplish this?

    A. `/etc/ssh/sshd_config`  
    B. `/etc/ssh/ssh_config`  
    C. `~/.ssh/ssh_config`  
    D. `/etc/ssh/known_hosts`  
    
    A, easy. I've had to set up X11 forwarding before. **CORRECT**

2. Which of the following configuration files should be modified to disable Ctrl+Alt+Del in Linux?

    A. `/etc/inittab`  
    B. `~/.bash_profile`  
    C. `/etc/securetty`  
    D. `/etc/security/limits.conf`  

    A isn't really for security. B would be obviously insecure. C has that
    nice Unix-y sound to it so I guessed that one. **WRONG**

3. Joe, a user, is unable to log in to the server and contracts the systems
administrator to look into the issue. The administrator examines the
`/etc/passwd` file and discovers the following entry:
`joe:x:505:505::/home/joe:/bin/false` Which of the following commands should
the administrator execute to resolve the problem?

    A. `usermod -s /bin/bash joe`  
    B. `passwd -u joe`  
    C. `useradd -s /bin/bash joe`  
    D. `chage -E -1 joe`  

    `/bin/false` is there to troll the user or, at least, to prevent
    unauthorized access. `usermod` is our pal here. **CORRECT**

4. A server is almost out of free memory and is becoming unresponsive. Which
of the following sets of commands will **BEST** mitigate the issue?

    A. `free`, `fack`, `partprobe`  
    B. `lsof`, `lvcreate`, `mdadm`  
    C. `df`, `du`, `rmmod`  
    D. `fdisk`, `mkswap`, `swapon -a`  

    You have a server slowing to a crawl and you create a swap partition. Now
    you have two problems! D it is! **CORRECT**

5. A Linux administrator is using a public cloud provider to host servers for
a company's website. Using the provider's tools, the administrator wrote a
JSON file to define how to deploy the servers. Which of the following
techniques did the administrator use?

    A. Infrastructure as code  
    B. Build automation  
    C. Platform as a service  
    D. Automated configuration  

    I don't know *too* much about DevOps but since "infrastructure" and "code"
    were mentioned I'm going with "infrastructure as code". **WRONG**

6. A Linux system is running normally when the systems administrator receives
an alert that one application spawned many processes. The application is
consuming a lot of memory, and it will soon cause the machine to become
unresponsive. Which of the following commands will stop each application
process?

    A. `` kill `pidof application` ``  
    B. `killall application`  
    C. `` kill -9 `ps -aux | grep application` ``  
    D. `pkill -9 application`  

    I've used B too many times to count. Getting the Markdown right for this
    one was a lot harder. **CORRECT**

7. A systems administrator configured a new kernel module, but it stopped
working after reboot. Which of the following will allow the systems
administrator to check for module problems during server startup?
    
    A. `lsmod`  
    B. `modprobe`  
    C. `modinfo`  
    D. `dmesg`  

    It's a kernel bug matter so I'm guessing `dmesg`. **WRONG**

8. A junior Linux administrator is installing patches using YUM. The
administrator issues the following command: `yum list installed`. The
output of the command is as follows:

    ![](https://i.imgur.com/nXGgN6Q.png)

    Given this scenario and the output, which of the following should the
    administrator do to address this issue?

    A. `renice -n 9 -p 5180`  
    B. `killall yum`  
    C. `ps -ef | grep yum`  
    D. `top | grep yum`  

    First thing to do is find the offending process. C. **CORRECT**

9. A systems administrator needs to retrieve specific fields from a CSV file.
Which of the following tools would accomplish this task?

    A. `awk`  
    B. `sort`  
    C. `print`  
    D. `echo`  

    I only ever use Ruby (and sometimes `sed`) for this sort of CLI
    text-mongling but it's obviously A. **CORRECT**

10. Two specific users need access to a directory owned by root where backups
are located. Which of the following commands would **BEST** ensure the
specified users can access the backup files?

    A. `umask`  
    B. `chcon`  
    C. `chmod`  
    D. `setfacl`  

    You've got to be kidding me! C! **WRONG** Apparently I need to read this
    later! https://www.redhat.com/sysadmin/linux-access-control-lists

11. Which of the following is the purpose of the monitoring server role?

    A. To aggregate web traffic to watch which websites employees are visiting
    B. To collect status and performance information about the servers in an environment
    C. To provide user authentication services to a network
    D. To provide real-time analysis of potential threats to the organization

    Obviously B and at least my certainty didn't steer me wrong this time.
    **CORRECT**

12. A junior administrator is migrating a virtual machine from a Type 1
hypervisor to a Type 2 hypervisor. To ensure portability, which of the
following formats should the administrator export from the Type 1 hypervisor
to ensure compatibility?

    A. OWASP
    B. VDI
    C. VMDK
    D. OVA

    I haven't used VMs much but I took a wild guess that was D. **CORRECT**

13. A junior systems administrator is upgrading a package that was installed
on a Red Hat-based system. The administrator is tasked with the following:

    * Update and install the new package.
    * Verify the new package version is installed.

    Which of the following should be done to **BEST** accomplish these task?
    (Choose two.)

    A. `yum install <package name>`  
    B. `yum upgrade`  
    C. `rpm -e <package name>`  
    D. `rpm -qa`  
    E. `apt-get <package name>`  
    F. `apt-get upgrade`  

    Haven't used RH or the like very much in the past years at all (except for
    that one Droplet) but it's A and D assuredly. **CORRECT**

14. Which of the following is the template for the `grub.cfg` file?

    A. `/etc/default/grub`  
    B. `/etc/grub2.cfg`  
    C. `/etc/sysct1.conf`  
    D. `/boot/efi`  

    I know just enough to answer A. **CORRECT**

15. A Linux administrator implemented a new HTTP server using the default
configuration. None of the users on the network can access the server. If
there is no problem on the network or with the users' workstations, which of
the following steps will **BEST** analyze and resolve the issue?

    A. Run `netstat` to ensure the port is correctly bound, and configure the firewall to allow access on ports 80 and 443
    B. Run `route` to ensure the port is correctly bound, and configure the firewall to allow access on ports 80 and 443
    C. Run `netcat` to ensure the port is correctly bound, and configure a static route to the web to allow access on ports 80 and 443
    D. Run `route` to ensure the port is correctly bound, and configure SELinux to allow access on ports 80 and 443

    I think `nmap` is better for port scanning but C is the only option here. **CORRECT**
