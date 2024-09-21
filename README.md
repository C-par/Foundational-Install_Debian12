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
> Uncomplicated Firewall is easy to setup and understand. It blocks traffic and allows it.
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
> Fail2Ban is one of the best programs that is installed in every single Linux server I have EVER installed. This program is a intrusion prevention utility. Most install it, but forget to
> configure and use it. These are the settings I like to use.
### [Install Fail2Ban](https://christitus.com/linux-security-mistakes/#google_vignette)

> Install code below:
- `sudo apt install fail2ban`


> Enabling Fail2Ban. Install code below:
- `sudo systemctl enable fail2ban`
- `sudo systemctl start fail2ban`
