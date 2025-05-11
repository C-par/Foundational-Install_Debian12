# Foundational Debian 12 Install

Foundational Debian 12 Install - a predefined process or chain of task strategically outlined with the end goal of installing Debian 12 as a noob. This is my very first attempt at using Linux all together and due to the learning curve involved, I will be documenting my steps learned/taken via this - Foundational Debian 12 Install documentation. Anyone can install this OS however, it will be beneficial to have a basic understanding of the hardware you are working with and its corresponding overall compatability with Debian 12. For the most part, as long as you have the prerequisites advised here [2.1. Supported Hardware](https://www.debian.org/releases/bookworm/amd64/ch02s01.en.html), you should be able to get it installed without issue.   

Special 'Thank You' to Chris Titus, who inspired me to start my Linux journey via his detail youtube walk-throughs. Here is a link to his Website & Github where you will find a multitude of guides and how-to documents: [Website](https://christitus.com/) & [Github](https://github.com/ChrisTitusTech)



## Lets get started!

> [!TIP]
> Remember, it is important to know what you installed via the command line because various installs may impact your system negitivley. You can check what you installed via the command line, use the code below.


- `sudo cat /var/log/apt/history.log |grep install`


> [!TIP]
> Optional: De-bloat Debian 12 by removing pre-installed games, use the code below. 
- `sudo apt purge iagno lightsoff four-in-a-row gnome-robots pegsolitaire gnome-2048 hitori gnome-klotski gnome-mines gnome-mahjongg gnome-sudoku quadrapassel swell-foop gnome-tetravex gnome-taquin aisleriot gnome-chess five-or-more gnome-nibbles tali ; sudo apt autoremove`


Managing a firewall on a system can be a monumental task, but one of the most important is managing the traffic coming to and from your computer. The best packages for this in Linux is ufw and fail2ban.


> [!IMPORTANT]
> The Uncomplicated Firewall (ufw) is a frontend for iptables and is particularly well-suited for host-based firewalls. ufw provides a framework for managing netfilter, as well as a command-line
> interface for manipulating the firewall
### [Install UFW](https://christitus.com/linux-security-mistakes/#google_vignette)

> Install code below:
- `sudo apt install ufw`


> Recommended Rules. Install code below:
- `sudo ufw limit 22/tcp`
- `sudo ufw allow 80/tcp`
- `sudo ufw allow 443/tcp`
- `sudo ufw default deny incoming`
- `sudo ufw default allow outgoing`
- `sudo ufw enable`


> [!IMPORTANT]
> Fail2Ban scans log files like /var/log/auth.log and bans IP addresses conducting too many failed login attempts. It does this by updating system firewall rules to reject new connections from > those IP addresses, for a configurable amount of time. 
### [Install Fail2Ban](https://christitus.com/linux-security-mistakes/#google_vignette)

> Install code below:
- `sudo apt install fail2ban`


> Enabling Fail2Ban. Install code below:
- `sudo systemctl enable fail2ban`
- `sudo systemctl start fail2ban`




> [!IMPORTANT]
> Linux System Hardening with auditd
> Step-by-Step Guide: Harden Linux with auditd
> 1. Install auditd
------------------
- `sudo apt update`
- `sudo apt install auditd audispd-plugins`
> 2. Enable and Start auditd
---------------------------
- `sudo systemctl enable auditd`
- `sudo systemctl start auditd`
- `sudo systemctl status auditd`
> 3. All-Encompassing auditd Rules
--------------------------------


- `sudo nano /etc/audit/rules.d/hardening.rules`

  
- Paste the following:
- ## ==== Start of Audit Rules ==== ##
- ## Monitor user logins
- `-w /var/log/faillog -p wa -k logins`
- `-w /var/log/lastlog -p wa -k logins`
- `-w /var/log/tallylog -p wa -k logins`
- `-w /var/log/wtmp -p wa -k logins`
- `-w /var/log/btmp -p wa -k logins`
- ## Monitor usage of privileged commands
- `-w /usr/bin/sudo -p x -k privilege`
- `-w /bin/su -p x -k privilege`
- `-w /usr/bin/passwd -p x -k privilege`
- `-w /usr/bin/chsh -p x -k privilege`
- ## Watch for changes to critical system files
- `-w /etc/passwd -p wa -k user_mods`
- `-w /etc/shadow -p wa -k user_mods`
- `-w /etc/group -p wa -k user_mods`
- `-w /etc/gshadow -p wa -k user_mods`
- `-w /etc/sudoers -p wa -k sudoers`
- ## Track all command executions (64-bit and 32-bit)
- `-a always,exit -F arch=b64 -S execve -k exec_log`
- `-a always,exit -F arch=b32 -S execve -k exec_log`
- ## Monitor file deletions by users
- `-a always,exit -F arch=b64 -S unlink -S unlinkat -S rename -S renameat -F auid>=1000 -F`
- `auid!=4294967295 -k delete`
- ## Monitor system time changes
- `-a always,exit -F arch=b64 -S adjtimex -S settimeofday -S clock_settime -k time_change`
- `-w /etc/localtime -p wa -k time_change`
- ## Monitor changes to audit configuration
- `-w /etc/audit/ -p wa -k audit_rules`
- `-w /etc/audit/audit.rules -p wa -k audit_rules`
- ## Monitor network configuration
- `-w /etc/hosts -p wa -k net_config`
- `-w /etc/network/ -p wa -k net_config`
- `-w /etc/hostname -p wa -k net_config`
- ## Monitor kernel module changes
- `-w /sbin/insmod -p x -k kernel_modules`
- `-w /sbin/rmmod -p x -k kernel_modules`
- `-w /sbin/modprobe -p x -k kernel_modules`
- `-a always,exit -F arch=b64 -S init_module -S delete_module -k kernel_modules`
- ## ==== End of Audit Rules ==== ##
> 4. Apply the Rules
-------------------
- `sudo augenrules --load`
- `sudo systemctl restart auditd`
> 5. View Logs
-------------
- `sudo ausearch -k exec_log`
- `sudo aureport --summary`
> 6. Enable audit at Boot
------------------------
- `sudo nano /etc/default/grub`
- `GRUB_CMDLINE_LINUX="audit=1"`
- Update grub:
- `sudo update-grub`
