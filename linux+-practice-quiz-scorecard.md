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

    I've used B too many times to count. **CORRECT**
