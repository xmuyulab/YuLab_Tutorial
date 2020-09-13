# THGY - The Hitchhiker's Guide to YULAB

## Principles 
* You are not working for Prof. Yu.  Prof. Yu is working with you on **your** projects. 
* Asking for what you need rather than hoping that Prof. Yu will know what to provide
* Don't expect to figure everything out by yourself.  When you have a question, ask search engine first then your fellow students and Prof. Yu
* Thining from the end.  When start a project, start with a vision of what the “perfect paper” would look like. What will be novel? What will be the conceptual advance? And how will we validate it? After establishing the big goal, we then work backward to establish the work plan on how to proceed. 

## Survival skills
* Good programming skill (talk is cheap, show me the code)
* Git and github (harddisk breakdown randomly.  If no, I may randomly smash some when I am bored)  
* Good English reading skill (how many papers you read per day?) 

## IT resources

### Network structure and access
#### Set a Static IP on Ubuntu
This tutorial explains how to set a static IP on an Ubuntu system from the command line.

##### Step 1: Configure the network interface
In this step, you will manually configure your network interface by editing the following files using your preferred text editor(nano gedit vi). For the purpose of this example, I'm using the "nano" editor. You can edit the appropriate file by entering the following command into the terminal:

```
sudo nano /etc/network/interfaces
```

A configuration where the IP address get's assigned automatically by DHCP will look like this:

```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# The primary network interface
auto ens21f0 (or ens21f1)
iface ens21f0 inet dhcp
```

Statically configured network cards like this:

```
auto ens21f0
iface ens21f0 inet static
        address xxx.xxx.xxx.xxx(enter your ip here)
        netmask xxx.xxx.xxx.xxx
        gateway xxx.xxx.xxx.xxx(enter gateway ip here,usually the address of the router)
```

And here an example for Ubuntu 16.04 and newer:

```
# This file describes the network interfaces available on your system
# and how to activate them. For more information, see interfaces(5).

source /etc/network/interfaces.d/*

# The loopback network interface
auto lo
iface lo inet loopback

# test

# The primary network interface
auto ens21f1
iface ens21f1 inet static
 address 192.168.3.11
 netmask 255.255.255.128
 gateway 192.168.3.1
```
And here the complete network configuration file from an Ubuntu 16.04 system.

##### Step 2: Restart networking

Manually restart your network interface with the new settings.

```
sudo /etc/init.d/networking restart
```

At this point you can check if the settings are correct:

```
ifconfig
```
Then send ICMP request to a remote host to check the connectivity. For example: send to the gateway

```
ping 192.168.3.1
```
If every step goes well，you have completed the configuration of the static IP.

### Computing nodes

|IP | CPU  | RAM | Harddisk | Current user |
|---|---|---|---|---|
|10.24.80.101|32 cores Intel(R) Xeon(R) E5-2683v4\@2.10GHz|256G+44G(Swap)|/mnt/md0(11T)+/home(49G)|liuyu/qy/ryu/xiaoxu/zoelin|
|10.24.80.102|64 cores Intel(R) Xeon(R) E5-2683v4\@2.10GHz|256G+15G(Swap)|tmpfs(330G)+/home(184G)|lhj/liuyu/lmy/ryu/xmulsm/zoelin|
|10.24.80.103|40 cores Intel(R) Xeon(R) E5-2630v4\@2.20GHz|64G+128G(Swap)|/(760G)|gmx/gmx2/jupyter/liuyu/lyc/R/txw/xiaoxu/xmulsm/yulab3/zoelin|
|10.24.80.105|64 cores Intel(R) Xeon(R) E5-2683v4\@2.10GHz|256G+15G(Swap)|/(59G)+/mnt/md0(7.3T)+/home(147G)|gmx2/hjl/lcx/liuyu/lmy/lyc/myl/qy/syw/tlx/xwt/ytl/yu|
|10.24.80.106|32 cores Intel(R) Xeon(R) E5-2620v4\@2.10GHz|64G+15G(Swap)|/mnt/md0(55T)+/mnt/md1(49T)|cx/fzy/lihaojun/liuyu/myl/qiaoying/ryu/sy01/sy02/zoelin|


### Samba server

Our lab has a samba server located at 10.24.80.106.  To start with, ask the system admin (currently Liu Yu is kindly to help creating user account for this server) to obtain a user name and a password.  Once you have the user name and password, you can use the samba folder on either Windows or Linux machiine. 

On Windows, just aceess your samba share through //10.24.80.106/<your_user_id>.  You will be prompted to input the password when you  access it. We also have a public folder on //10.24.80.106/public which is accessible to all users to share common data. 

There are several ways to access this folder on Linux machine. On shared computing node in the server room, you can create a mount point under your home directory and mount the samba folder.  for example, if you create a share folder call ~/mnt/public under your home directory

```
mkdir ~/mnt/public
mkdir ~/mnt/<your_user_id>
```

The samba share can be mounted through

```
sudo mount -t cifs //10.24.80.106/public ~/mnt/public -o user=<your_user_id>,pass=<your_passwd>
sudo mount -t cifs //10.24.80.106/<your_user_id> ~/mnt/<your_user_id> -o user=<your_user_id>,pass=<your_passwd>
```

Alternatively, on your own desktop you may want to mount to be perminate, which can be done by adding the following to your /etc/fstab file

```
//10.24.80.106/public /mnt/public cifs user=<your_user_id>,pass=<your_passwd> 0 0
//10.24.80.106/<your_user_id> /mnt/<your_user_id> cifs user=<your_user_id>,pass=<your_passwd> 0 0
```

If you are curious on how to setup a samba server, here is a good tutorial guide on DigitalOcean [Tutorial on samba server setup](https://linuxize.com/post/how-to-install-and-configure-samba-on-ubuntu-18-04/).




