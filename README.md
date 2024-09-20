# Foundational Install
Foundational Install - a predefined process or chain of task strategically outlined with the end goal of installing Debian 12 as a noob. This is my very first attempt at using Linux all together and due to the learning curve involved, I will be documenting my steps via this - Foundational Install documentation. 




Managing a firewall on a system can be a monumental task, but one of the most important is managing the traffic coming to and from your computer. The best packages for this in Linux is ufw and fail2ban.



#Install UFW
1. Uncomplicated Firewall is easy to setup and understand. It blocks traffic and allows it.

sudo apt install ufw

2. Recommended Rules

sudo ufw limit 22/tcp
sudo ufw allow 80/tcp
sudo ufw allow 443/tcp
sudo ufw default deny incoming
sudo ufw default allow outgoing
sudo ufw enable


#Install Fail2Ban
3. Fail2Ban is one of the best programs that is installed in every single Linux server I have EVER installed. This program is a intrusion prevention utility. Most install it, but forget to configure and use it. These are the settings I like to use.


sudo apt install fail2ban

4. Enabling Fail2Ban

sudo systemctl enable fail2ban
sudo systemctl start fail2ban
