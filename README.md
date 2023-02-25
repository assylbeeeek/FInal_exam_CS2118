# Final_exam_CS2118
This repository provides the written code in with which we have completed all 3 tasks by Aiken, Sofiya, Adina, Irina, Assylbek.
(The code from linux terminal has this signs: ~, #, these making strikethrough and marked up text in github, so we removed these signs here in some places. Unfortunately, some of the written codes have not been saved.)\
# Task 1 codes
assylbek@assylbek-VirtualBox:$ sudo useradd new_user\
[sudo] password for assylbek: \
assylbek@assylbek-VirtualBox:$ sudo -i\
root@assylbek-VirtualBox:# useradd student\
root@assylbek-VirtualBox:# passwd student\
New password: \
BAD PASSWORD: The password is shorter than 8 characters\
Retype new password: \
passwd: password updated successfully \
root@assylbek-VirtualBox:# login student\
Password: \
Welcome to Ubuntu 22.04.1 LTS (GNU/Linux 5.15.0-58-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

223 updates can be applied immediately.
98 of these updates are standard security updates.
To see these additional updates run: apt list --upgradable


The list of available updates is more than a week old.
To check for new updates run: sudo apt update

The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.


The programs included with the Ubuntu system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by
applicable law.                                                                                                                             
No directory, logging in with HOME=/\
$ whoami\
student\

to check the result in etc/passwd file\
assylbek@assylbek-VirtualBox:/etc$ open passwd
# Task 2 code
1. "Direct" IP connection\
In the manual configuration mode of the IPv4 in wired connection entered this settings:\
Address: 10.0.2.15\
Netmask: 255.255.255.0 \
Gateway: 10.0.2.2\
DNS: 162.168.1.1 (IPv4 address of my home router)\
Checked results in settins and in terminal by typing commands:\
sonya@sonya:$ ip addr \
sonya@sonya:$ ping google.com (this test checks the speed and stability of the entered internet connection)\
2.	Connection via NAT.\
a) To connect via NAT, I used Iptables & to do it I had to get root access.\
b) First of all, I verified my connection, then configured eth0 with an IP external network and configured eth1 for LAN with an internal private network.\
a)	Gateway, DNS configuration.\
b)	Then, I did NAT configuration via IP tables:\
Deleted and flashed, also deleted all chains (that are not included to default filter & nat table).\
Set up IP forwarding and masquerading.\
Enabled packet forwarding & applied the configuration.\
In the /etc/systl.conf *\
/etc/sysctl.conf - Configuration ftle for setting system vartables\
 See /etc/sysctl.d/ for additional system vartables.\
 See sysctl.conf (5) for information.\
#kernel.domainname = example.com\
 Uncomment the following to stop low-level messages on console\
kernel.printk = 3 4 1 3\
#######＃############＃＃＃＃＃##＃#＃###########＃#######＃###＃#＃#＃＃＃＃＃＃丼＃#＃\
 Functions previously found in netbase\
 Uncomment the next two lines to enable spoof protection (reverse-path filter)\
 Turn on Source Address Verification in all interfaces to\
 prevent some spoofing attacks\
#net.tpv4.conf.default.rp_ filter=1\
#net.tpv4.conf.all.rp_filter=1\
In the /etc/networks/interfaces\
pre-up iptables-restore < /etc/iptables.up.rules\
up route add -net 192.168.0.0 netmask 255.255.255.0 dev eth1\
up route add -net 0.0.0.0 netmask 255.255.255.255 dev eth0\
