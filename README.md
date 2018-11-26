# ROSMME
Setting up an in-house cluster

### FIRST STEP: Downloading the OS and setting up the repository
The ISO image will be downloaded in the folder `/distro/iso/`, which is already created. We are going to use CentOS 7.5 in our cluster. The ISO image was downloaded from the mirror in the UPB:
```
$> cd /distro/iso
$> cd wget http://mirror.upb.edu.co/centos/7.5.1804/isos/x86_64/CentOS-7-x86_64
```
Create a folder where the repository is going to be located:
```
$> mkdir -pv /distro/CentOS-7.5-x86_64
```
The following commands allow us to check if the ISO image is correct:
```
$> mount -t iso9660 -o loop /distro/iso/CentOS-7-x86_64-DVD-1804.iso /distro/CentOS-7.5-x86_64/
```
This should show the installation files in `/distro/CentOS-7.5-x86_64/`. If everything is as expected, we unmount the image as follows:
```
$> umount /distro/CentOS-7.5-x86_64/
```
After unmounting, no file should be shown in `/distro/CentOS-7.5-x86_64/` after doing `ls` in it.
In order to have the files of the ISO image available for a future installation, the following line has to be added in the `/etc/fstab` file:
```
/distro/iso/CentOS-7-x86_64-DVD-1804.iso /distro/CentOS-7.5-x86_64 iso9660 loop,ro 0 0
```
The following commands allow us to verify that the additional line in `/etc/fstab` works as expected:
```
$> mount /distro/CentOS-7.5-x86_64
$> dg /distro/CentOS-7.5-x86_64/
```
Thus, when `$> ls /distro/CentOS-7.5-x86_64/` is excecuted, the installation files are shown.



### etc / exports
In Linux system with NFS you can specify in which computers the content is shared. The list of resources that the server computer will share is located in / etc / exports Therefore The **/ etc /** exports file controls which file systems are exported to remote hosts (host or host computers or other connected devices), the Export file specifies options such as which devices it is possible to connect to for an assigned IP range and privileges or options that these hosts have
The options for each of the hosts must be placed in parentheses directly after the host identifier, without spaces separating the host and the first parenthesis, for our case the hosts are a function of a range of IP addresses  `/ distro `,  is a folder that contains the server which is being shared for the host range assigned inside the parentheses are the permissions for the computers of the network in this case we have applied

`/ distro 10.10.0.0/16(ro,root_squash,mp,crossmnt)`
```
• ro: read-only permissions, if nothing is specified by default this permission is applied.
• rw: write permissions.
• root_squash: mapping the identity of the root user for security. When the client with the root user is connected to the shared folder, the UID of the root user will be mapped by that of an anonymous user of the server computer, so that he can not be a root user on the server computer. By default this option is activated if not specified otherwise.
• no_root_squash: the identity of the root user will not be mapped, so the client root user will also be mapped to the server share.
• all_squash: the UID of any user of the client computer will be replaced by an anonymous UID of the server equipment.
• no_all_squash: option given by default, the UIDs of the users will not be mapped.
• squash_uids: you can put a UID or a range of UIDs to be mapped as an anonymous user. It can also be applied to squash_gids groups.
• anonuid: you can map the identity of the users you want to specify. Very useful if you want to share a directory but want to know from which machine is being written.
• nohide -> If you import a directory that has another directory mounted inside it and the one in the lower level resides in another partition, the client will only be able to see the content of the superior.
• crossmnt -> It is equivalent to nohide but you do not need to make the entries in exports of the child directory.
```


### / etc / hosts
This file is used to obtain a relation between a machine name and an IP address: on each line of / etc / hosts an IP address and the corresponding machine names are specified, so that a user does not have to remember addresses but host names. Usually they include the addresses, names and aliases of all the equipment connected to the local network. The purpose of assigning names to IP numbers is to make them easy for people to remember. Actually, an IP address identifies a network interface associated with a device such as a network card. Since each computer can have several network cards and several interfaces on each card, a single computer can have several names in the domain name system. Each team is identified The format of a line in this file can be
```

#*** SP Management ***
#iDRAC:
10.0.255.100  n00.sp    node00.sp    sp-n00    sp-rosmme
10.0.255.1    n01.sp    node01.sp    sp-n01    sp-node01
10.0.255.2    n02.sp    node02.sp    sp-n02    sp-node02
10.0.255.3    n03.sp    node03.sp    sp-n03    sp-node03
10.0.255.4    n04.sp    node04.sp    sp-n04    sp-node04
10.0.255.5    n05.sp    node05.sp    sp-n05    sp-node05


#*** 40 Gb ***
#eth0:
20.40.1.1     n01.mpi    mpi-n01    n01.40ge    node01.mpi
20.40.1.2     n02.mpi    mpi-n02    n02.40ge    node02.mpi
20.40.1.3     n03.mpi    mpi-n03    n03.40ge    node03.mpi
20.40.1.4     n04.mpi    mpi-n04    n04.40ge    node04.mpi
20.40.1.5     n05.mpi    mpi-n05    n05.40ge    node05.mpi
```
### The sysconfig directory

This directory contains files that control the configuration of your system. The contents of this section highlight some of the files found in the directory **/ etc / sysconfig /**, its function, and its contents. This information is not intended to be exhaustive, as many of these files have a variety of options that are only used in very specific circumstances, so the content of this directory depends on the packages you have installed on your system.

**/ etc / sysconfig / nfs**

Controls which ports use remote procedure call **(RPC)**  services for NFS v2 and v3. This file allows you to configure firewall rules for **NFS**

**/ etc / sysconfig / dhcpd**
It contains the arguments of the dhcpd daemon **"Dynamic Host Configuration Protocol (DHCP)"** and the **"Internet Bootstrap Protocol (BOOTP)"**. **DHCP** and **BOOTP** assign names of servers to machines on the network.
