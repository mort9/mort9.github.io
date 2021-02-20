---
title: Mort9 Posts
author: Mortie Torabi 
---

# Linux - *Tips and Tricks*

#### UNIQUE HISTORY

To make `history` command, show and record latest upsert(update/insert) new commands enable this environment variable. You can also put this line in `~/.bashrc` to persist the effect.

```bash
export HISTCONTROL=ignoreboth:erasedups
```



#### Putting `/var/log/` on RAM

Log directory is where a lot of disk I/O happens. This could cause slow down for systems like Raspberry Pi which use SD cards as their main storage with very limited I/O bandwidths. One more issue with too much I/O is that it would decrease life-span of the hard drive. This is specially important when it comes to SSD drives which die after a finite number of writes happen on their cells. One good solution to this problem is putting high I/O tasks on memory but with considerations. The data we're dealing with is not of high importance and we can bear losing it if the machine halts suddenly. There should be some mechanism to preserve the data at least once in a while so that we can have logs after each reboot. These two issues are somehow tackled by a small app called `log2ram` and we're going to install it on our `rock64` board which is running Debian.

[How To Write Log Files In RAM Using Log2ram In Linux - OSTechNix](https://ostechnix.com/how-to-write-log-files-in-ram-using-log2ram-in-linux/)

```bash
git clone https://github.com/azlux/log2ram.git
cd log2ram
chmod +x install.sh
sudo ./install.sh
vim /etc/log2ram.conf #change log size to 128M or whatever size you like
```

After a **reboot** we can see the changes by using these commands:

```bash
df -h
mount
```



#### Putting even more directories into temporary memory

```shell
# fstab
tmpfs /var/cache/apt/archives/ tmpfs defaults  0 0
```

```shell
# rc.local
mkdir -p /var/cache/apt/archives/partial &
```

[Debian User Forums • View topic - SOLVED tmpfs for apt](http://forums.debian.net/viewtopic.php?f=5&t=135125)



#### Systemd Service Template

There are different types of services which are defined for various application behaviors. Here our `ExecStart` would keep running and stick to the terminal(stdout), thus we should set `Type=simple`  Other options could be learned in the links provided:

- `Restart=on-failure` If the main process dies the system would try to run it again after `RestartSec=5s`
- By using `ExecStrat=bash -c '(cd ...)'`  the service is run in the directory where its executables are located 
- `AssertPathExists=/root/rq_tgfwd/` makes sure this directory exists when running the service it's an assertion requirement.
- Some main service types in systemd terminology
  - **`simple`** - A long-running process that does not background its self and stays attached to the shell.
  - **`forking`** - A typical daemon that forks itself detaching it from the process that ran it, effectively backgrounding itself.
  - **`oneshot`** - A short-lived process that is expected to exit.

```shell
# telegram-fwd.service
[Unit]
Description=Telegram Forwarder Service
AssertPathExists=/root/rq_tgfwd/

[Service]
Type=simple
Restart=on-failure
RestartSec=5s
ExecStart=bash -c '(cd /root/rq_tgfwd/ && ./start-tfd.sh)'

[Install]
WantedBy=multi-user.target
```

[Understanding Systemd Units and Unit Files | DigitalOcean](https://www.digitalocean.com/community/tutorials/understanding-systemd-units-and-unit-files)
[systemd: The Good Parts (hashicorp.com)](https://www.hashicorp.com/resources/systemd-the-good-parts)



#### D-Bus

*The daemon handles the routing from one process to another. If you want to make 2 processes communicate, DBus is overkill. It makes sense when you have dozens of processes, and each one want to gather information / perform calls from / to several other ones. For example, if you want to broadcast information you send a dbus signal to the daemon, and the daemon take care of routing this signal to the registered listening processes.* [DBus vs UNIX sockets...? : commandline (reddit.com)](https://www.reddit.com/r/commandline/comments/13o581/dbus_vs_unix_sockets/)



#### Termination Signals

[List of Kill Signals - Unix & Linux Stack Exchange](https://unix.stackexchange.com/questions/317492/list-of-kill-signals)

```sh
01 => SIGHUP # ?, controlling terminal closed, 
02 => SIGINT # interupt process stream, ctrl-C 
03 => SIGQUIT # like ctrl-C but with a core dump, interuption by error in code, ctl-/ 
09 => SIGKILL # terminate immediately/hard kill, use when 15 doesnt work
15 => SIGTERM # terminate whenever/soft kill, typically sends SIGHUP as well? 
18 => SIGCONT # Resume process, ctrl-Z (2nd)
19 => SIGSTOP # Pause the process / free command line, ctrl-Z (1st)
```



#### Named Pipes using `mkfifo` command

FIFOs are pipes that can have multiple readers and writers simultaneously.  

*A FIFO special file (a named pipe) is similar to a pipe, except that it is accessed as part of the filesystem. [...] When processes are exchanging data via the FIFO, the kernel passes all data internally without writing it to the filesystem. Thus, the FIFO special file has no contents on the filesystem; the filesystem entry merely serves as a reference point so that processes can access the pipe using a name in the filesystem.*

```shell
if [[ ! -p $pipe ]]; then mkfifo fifopipe; fi
while true; do echo Alice; done; > fifopipe &
while true; do echo Bob; done; > fifopipe &
( cat < fifopipe ) > logfile
```

Here two processes are writing to the same output `fifopipe` which is a named pipe. Then the output is collected at once and sent to a logfile. If we didn't use the FIFO here only one of the two processes would have been able to write to the file because continuous outputs to a file is only allowed for one process in Linux.

[Linux mkfifo Command Tutorial for Beginners (with Examples) (howtoforge.com)](https://www.howtoforge.com/linux-mkfifo-command/)



#### Find Command

```shell
find . -name "*.bak" -type f  # Find All files ending with '.bak' extension
find . -name "*.bak" -type f -delete # The same as above but also delete those found files
```



#### Changing how current Bash session behaves by using `shopt` and `set` commands

*Bash* has some features that are enabled or disabled by default. By using `shopt` and `set`  we can enable or disable those features to fit bash to our style. Here are some popular options:

```bash
shopt -s globstar # ** would refer to the files and folders recursively for example if then we use ls ** it would list all files and folders in the current directory and in all its sub-directories recursively
shopt -s autocd # entering the name of a directory would move(cd) us to that location
shopt -s cdspell # minor typos in the spelling of a directory component in a cd command are corrected
shopt -s cmdhist # One line history entry for multiline commands
```

[Bash shopt builtin command help and examples (computerhope.com)](https://www.computerhope.com/unix/bash/shopt.htm)
[Linux set and unset command help and examples (computerhope.com)](https://www.computerhope.com/unix/uset.htm)



