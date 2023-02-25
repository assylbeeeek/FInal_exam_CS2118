# Final_exam_CS2118
This repository provides the written code in with which we have completed all 3 tasks by Aiken, Sofiya, Adina, Irina, Assylbek. With some explanations, more in report file.
(The code from linux terminal has this signs: ~, #, these making strikethrough and marked up text in github, so we removed these signs here in some places. Unfortunately, some of the written codes have not been saved.)\
## Task 1 codes
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

Ubuntu comes with ABSOLUTELY NO WARRANTY, to the extent permitted by applicable law.
No directory, logging in with HOME=/\
$ whoami\
student\
To check the result in etc/passwd file\
assylbek@assylbek-VirtualBox:/etc$ open passwd
## Task 2 codes
**1. "Direct" IP connection**\
In the manual configuration mode of the IPv4 in wired connection entered this settings:\
*Address: 10.0.2.15\
Netmask: 255.255.255.0 \
Gateway: 10.0.2.2\
DNS: 162.168.1.1 (IPv4 address of my home router)*\
Checked results in settins and in terminal by typing commands:\
sonya@sonya:$ ip addr \
sonya@sonya:$ ping google.com (this test checks the speed and stability of the entered internet connection)\
**2.	Connection via NAT.**\
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
**3.	Connectian via a Proxy server.**\
For this type of connection method, I used information from special sites that give out up-to-date proxy servers, to do this work I used a Singapore server. 
*I connected everything manually.\
a) I went straight into Wired Connected -> Wired Settings -> Wired and clicked on the  Network Proxy button (by that I turned on whole system of proxy, because it was previously disabled).\
b) Then, I entered all essential data:\
HTTP Proxy: 180.210.206.52\
HTTPS Proxy: 180.210.206.52\
FTP Proxy: 180.210.206.52\
Port, that I’ve entered everywhere: 3128\
c) Then, I used terminal to check the quality of the network connection.\
sonya@sonya:$ ping google.com\
PING google.com (142.250.74.46) 50(84) bytes of data.\
64 bytes from arn09s22-in-f14.1e100.net (142.250.74.46): icmp_seq=1 ttl=56 time=160ms\
64 bytes from arn09s22-in-f14.1e100.net (142.250.74.46): icmp_seq=2 ttl=56 time=132ms\
64 bytes from arn09s22-in-f14.1e100.net (142.250.74.46): icmp_seq=3 ttl=56 time=164ms\
64 bytes from arn09s22-in-f14.1e100.net (142.250.74.46): icmp_seq=4 ttl=56 time=179ms\
Overall, people use proxy servers because it offers several benefits, such as: security, privacy and access to restricted content.
## Task 3 codes
Linux distributions have modprobe, insmod and depmod commands for working with module packages. Loading them with:\
sudo apt-get install build-essential kmod\
Сheck which modules are loaded into the kernel via:\
sudo lsmod\
Prescribed the path to the modules:\
sudo cat /proc/modules \
Through these commands we check the available cores:\
sudo apt-get update \
apt-cache search linux-headers-`uname -r` \
After that we download the latest version of the kernel:\
sudo apt-get install kmod linux-headers-5.4.0-80-generic\
We create a text catalog calculator-2.ko with mkdir command\
aika@aika-virtual-machine: $ mkdir -p ~/develop/kernel/calculator-2\
Then we upload the C code with the calculator there:\
#include <linux/init.h>\
#include <linux/module.h>\
#include <linux/kernel.h>\
\
int calculator_init(void) {\
    printk(KERN_INFO "Calculator module loaded\n");\
\
    char op;\
    int num1, num2;\
\
    // Read operator and operands from user\
    printk(KERN_INFO "Enter operator (+,-,*,/): ");\
    scanf("%c", &op);\
\
    printk(KERN_INFO "Enter two operands: ");\
    scanf("%d %d", &num1, &num2);\
    // Perform the operation\
    switch(op) {\
        case '+':\
            printk(KERN_INFO "%d + %d = %d\n", num1, num2, num1 + num2);\
            break;\
        case '-':\
            printk(KERN_INFO "%d - %d = %d\n", num1, num2, num1 - num2);\
            break;\
        case '*':\
            printk(KERN_INFO "%d * %d = %d\n", num1, num2, num1 * num2);\
            break;\
        case '/':\
            if(num2 == 0) {\
                printk(KERN_ERR "Error: Division by zero\n");\
            } else {\
                printk(KERN_INFO "%d / %d = %d\n", num1, num2, num1 / num2);\
            }\
            break;\
        default:\
            printk(KERN_ERR "Error: Invalid operator\n");\
            break;\
    }\
    return 0;\
}\
\
void calculator_exit(void) {\
    printk(KERN_INFO "Calculator module unloaded\n");\
}\
module_init(calculator_init);\
module_exit(calculator_exit);\
MODULE_LICENSE("GPL");\
MODULE_AUTHOR("Your name");\
MODULE_DESCRIPTION("A simple calculator kernel module");\
Next we create with text editor nano a Makefile\
aika@aika-virtual-machine: $ cd ~/develop/kernel/calculator-2\
aika@aika-virtual-machine: ~/develop/kernel/calculator-2$ nano Makefile\
At the end, we execute the make command\
aika@aika-virtual-machine: ~/develop/kernel/calculator-2$ make\
Next we run our sudo insmod calculator-2.ko file and test it with simple calculation\
aika@aika-virtual-machine: ~/develop/kernel/calculator-2$ sudo insmod calculator-2.ko\
aika@aika-virtual-machine: ~/develop/kernel/calculator-2$ 23 - 13\
10
