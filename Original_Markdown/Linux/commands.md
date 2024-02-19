=== Linux commands ====
 `grep` - is a command-line utility for searching plain-text data sets for lines that match a regular expression. 
          Its name comes from g/re/p (globally search a regular expression and print)
          e.g. `grep "Hello" hello.txt` - print lines containing "Hello" in hello.txt)  
 `eog` - Eye of GNOME, is the official image viewer for the GNOME desktop environment
 `xdg-open` - opens a file or URL in the user's preferred application (e.g. `xdg-open hello.txt` - open hello.txt in the default text editor)
 `lsb_release -a` - show Linux distribution information  
 `cat /etc/os-release` - show Linux distribution information)  
 `tail -f /var/log/syslog` - show last 10 lines of syslog and continuously print new lines as they are appended to syslog  
 `tail -15 /var/log/syslog` - show last 15 lines of syslog  
 `stat` - display file or file system status (e.g. `stat /dev/ttyACM0` - show status of ttyACM0)  
 `tree` - list contents of directories in a tree-like format (install with `sudo apt install tree`)  
 `tree -L 1` - show only first level of directories  
 `tmux` - terminal multiplexer, allows you to run multiple terminal sessions inside a single   
          terminal window or remote terminal session (install with `sudo apt install tmux`)  
  `tmux ls` - list all tmux sessions  
  `tmux attach -t <session_name>` - attach to tmux session with specified name  
  `tmux kill-session -t <session_name>` - kill tmux session with specified name  
  `tmux new -s <session_name>` - create new tmux session with specified name  
  `tmux rename-session -t <old_session_name> <new_session_name>` - rename tmux session  
  `tmux detach` - detach from tmux session (keep session running in background) or simply `CTRL-B d`  
  `tmux windows` - list all windows in tmux session  
  `tmux new-window` - create new window in tmux session, or simply `CTRL-B c`  
  `Ctrl-b %` - split tmux window vertically  
  `Ctrl-b "` - split tmux window horizontally  
  `Ctrl-b <arrow key>` - switch between tmux windows  
  `Ctrl-b : list-command` - list all tmux commands  
  `Ctrl-b : [` - enter copy mode (use arrow keys to navigate, press `v` to select text, press `y` to copy selected text)  
  `chmod u+x simple_velocity_publisher.py` - make script executable for user (u - user, + - add permission, x - execute)

### Software management 
Apt - Advanced Package Tool (apt is a command-line utility for installing, updating, removing, and otherwise managing  
deb packages on Ubuntu, Debian, and related Linux distributions) apt is a newer command-line tool that provides 
the same functionality as apt-get, and possibly more.  
- `apt update` - update list of available packages
- `apt upgrade` - upgrade all installed packages
- `apt search <package_name>` - search for package in repositories
- `apt list --installed` - list all installed packages
- `apt insall --no-install-recommends <package_name>` - install package without recommended packages and only packages 
                                                      required to satisfy dependencies for the specified package 
                                                      (useful in docker images to reduce image size)
- `apt remove <package_name>` - remove package
- `apt purge <package_name>` - remove package and its configuration files
- `apt autoremove` - remove packages that were automatically installed to satisfy dependencies 
                   for other packages and are now no longer needed
- `apt-key add <key_file>` - add key_file to apt trusted keys (Key is a file containing a PGP key in ASCII armor format is needed  
                           to authenticate the package repository. The apt-key add command is used to add the key)  
- `apt-key list` - list apt trusted keys
- `dpkg` - install, remove, and inspect deb packages (dpkg is a low-level tool for installing, removing, and inspecting deb packages)
- `dpkg -i <package_name>` - install package (e.g. `dpkg -i google-chrome-stable_current_amd64.deb`)

### Process management
- `ps aux` - show all running processes (a - show processes of all users, u - show processes of current user, 
                                        x - show processes not attached to a terminal)
- `top` - display Linux processes (top -  display Linux processes in real time)  
  `top -p <PID>` - display Linux process with specified PID  
  `top -u <username>` - display Linux processes of specified user    
  `Shift + M` - sort processes by memory usage  
  `Shift + P` - sort processes by CPU usage  
- `pstree` - display a tree diagram of running processes  
  `pstree <PID>` - This will show the process tree starting from the specified PID
- `kill -l` - list all signals  
  `kill <PID>` - terminate process with specified PID (by default sends SIGTERM (15) signal to the process, same as `kill -SIGTERM <PID>`)  
  `kill -SIGINT <PID>` - terminate process with specified PID (sends SIGINT (2) signal to the process) this is the default signal  
                        sent by the `Ctrl + C` command. The primary purpose of SIGINT is to notify a process that  
                        the user has requested an interruption.  SIGINT is a gentle nudge asking the process to stop. If that fails,  
                        SIGTERM is a more forceful, but still polite request for the process to terminate (it still provides the process  
                        with a chance to tidy up (save data) before shutting down). 
                        Finally, if all else fails, SIGKILL terminates the process with no questions asked.  
  `kill -9 <PID>` (same as `kill -SIGKILL <PID>`) - terminate process with specified PID (sends SIGKILL (9) signal to the process)  
                  this is a "forceful" or "hard" kill signal because it immediately terminates the processes without allowing them  
                  to perform any cleanup tasks, to save any data or graceful shutdown procedures.  
- `killal` - send a signal to all processes running any of the specified commands  
  `killall chrome` -  terminate all running instances of the Google Chrome browser on your Linux system  
  `killall -9 process_name` - This signal is commonly known as a "forceful" or "hard" kill signal because it immediately  
                             terminates the processes without allowing them to perform any cleanup tasks or graceful shutdown procedures.  
- `Ctrl + Z` - bash job control. To suspend a foreground process running in a terminal. Stops the process and returns you  
              to the current shell. You can now type `fg` to continue process, or type `bg` to continue the process in the background  
              Ctrl+Z is a useful way to temporarily halt a process without terminating it, allowing you to continue using the terminal  
              for other tasks and then later bring the suspended process back when needed.  
              - If you have a process running in the foreground in your terminal, such as a long-running command or program,  
              pressing Ctrl+Z will suspend that process.  
              - You will see a message indicating that the process has been stopped, along with a job number, typically   
              something like [1]+ Stopped command  
              - The suspended process is now in the background, and you can use the `bg` command to resume it in the background  
              or the `fg` command to bring it back to the foreground.  
 - `Ctrl + C` - terminate a running process (SIGINT [Signal Interrupt - Signal Number 2] signal is sent to the process)  
              (SIGTERM [command kill sends TERM by default] is the preferred way as the process has the chance to terminate gracefully)  

 - `miniterm` - simple terminal program for the serial port (installed as part of pyserial package `sudo apt install python3-serial`)  
              can be used to send commands to the serial port (e.g. send to Arduino [Arduino is used as a motor controller])  
              `miniterm /dev/ttyACM0 115200` - open serial port with baudrate 115200  

 `wget` - command-line utility for downloading files from the web (install with `sudo apt install wget`)
          `wget -O <filename> <url>` - download file from url and save it as filename
          or simply `wget <url>` - download file from url and save it with original name
  


  --Shortcuts in Linux Ubuntu Gui
  `Ctrl + H` - show hidden files
  `Ctrl + L` - go to address bar
  `Ctrl + Shift + C` - copy path of selected file in terminal
  `Ctrl + Shift + V` - paste path of selected file in terminal
  `Ctrl + Z` - stops the process and returns you to the current shell. You can now type fg to 
               continue process, or type bg to continue the process in the background

  --- Journal is a system service for collecting and storing log data (it is a part of systemd) ---
  `journalctl` - query the systemd journal (systemd is a system and service manager for Linux operating systems, that is 
                 responsible for starting and stopping services and daemons, mounting and unmounting file systems, 
                 maintaining the system clock, and other system management tasks)
  `journalctl -fe` - show the latest journal entries and continuously print new entries as they are appended to the journal
  `journalctl -f` - show only new entries as they are appended to the journal
  `journalctl -b` - show messages from the current boot
  `journalctl -u <service_name>` - show logs of service (to get list of services use `systemctl list-units --type=service`)
                                 E.g. `journalctl -b -u docker.service` - show logs of docker service from the current boot            

Systemd is a replacement for init. It is intended to provide a better framework for expressing services' dependencies,
allowing for faster boot times through parallelization. It replaces the init system inherited from UNIX System V and Berkeley 
Software Distribution (BSD)
Init and Systemd are both init daemons but it is better to use the latter since it is commonly used in recent Linux Distros. 
Init uses service whereas Systemd uses systemctl to manage Linux services
The /sbin/init is a symbolic link to the actual init process. You can follow the symbolic link and see real process. 
I am using the stat command and you can see that /sbin/init is linked to /lib/systemd/systemd in Ubuntu. 
This is an indication that systemd is in use

--- Systemctl is a systemd utility that is responsible for Controlling the systemd system and service manager ---
      Service manager is a background process that manages the life cycle of services in the system
  `systemctl list-units`- lists all currently loaded in memory systemd units, which includes both active and inactive units
  `systemctl list-units --type=service` - show list of services that are currently loaded
  `systemctl list-unit-files` - lists all available systemd unit files on your system. Unit files define services, targets, 
                                sockets, timers, and other systemd units that can be activated.
    units are represented by unit files, which are stored in the /usr/lib/systemd/system/ and /etc/systemd/system/ directories.
    they are merely configuration files that describe the unit and define its behavior 
    (e.g. /etc/systemd/system/docker.service, .socket, .target, etc)                              
  `systemctl status <service_name>` - show status of service
  `systemctl enable <service_name>` - enable service to start automatically at boot
  `systemctl disable <service_name>` - disable service to start automatically at boot
  `systemctl start <service_name>` - start service
  `systemctl stop <service_name>` - stop service
  `systemctl get-default` - show default target (default target is a special systemd unit that is loaded by default when 
                            the system boots. It is similar to runlevel in the init system)
                            Target is a special kind of unit that does not do anything itself but instead acts as a
                            collection of other units. It is used to group units together and to simplify the boot process.
  `systemctl set-default <target_name>` - set default target (e.g. `systemctl set-default multi-user.target` 
                                                              - set default target to multi-user.target)
  `systemctl list-units --type=target` - show list of targets (shown only active targets)
  `systemctl list-dependencies <target_name>` - show list of units that are dependencies of target 
                                                (e.g. `systemctl list-dependencies multi-user.target`)

  --- RPi ---
  `vcgencmd` is a command-line utility used on Raspberry Pi devices that runs the VideoCore GPU on the Raspberry Pi.
             VideoCore is a low-power mobile multimedia processor originally developed for the Raspberry Pi project.
             It allows you to query various hardware-related information, such as firmware revision, temperature.
  `vcgencmd commands` - show all available commands
  `vcgencmd measure_temp` - show CPU temperature
  `vcgencmd get_throttled` - show under-voltage and over-temperature flags (if 0x0 - everything is ok, if 0x50000 - under-voltage, 
                             if 0x50005 - under-voltage and over-temperature,
                             if 0x50001 - under-voltage and currently throttled, if 0x50006 - under-voltage, over-temperature and currently throttled)
                             (throttled means that CPU frequency is reduced because of under-voltage or over-temperature)         

  To set RPi to boot to console (without GUI)
  `sudo systemctl set-default multi-user.target` - set default target to multi-user.target (multi-user.target is a target that 
                                                   provides a console login and is the default target for non-graphical Raspberry Pi OS images)

=== WSL2 ===
-- Attach USB devices
--- From an administrator command prompt on Windows, run this command. 
--- It will list all the USB devices connected to Windows.
usbipd wsl list

--- Select the bus ID of the device you’d like to attach to WSL and run this command. 
--- You’ll be prompted by WSL for a password to run a sudo command.
usbipd wsl attach --busid <busid>