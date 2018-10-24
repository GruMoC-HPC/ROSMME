# ROSMME
Setting up an in-house cluster

### FIRST STEP: Downloading the OS and setting up the repository
The ISO image will be downloaded in the folder `/distro/iso/`, which is already created. We are going to use CentOS 7.5 in our cluster. The ISO image was downloaded from the mirror in the UPB:
```
$> cd /distro/iso
$> cd wget http://mirror.upb.edu.co/centos/7.5.1804/isos/x86_64/CentOS-7-x86_64
```
Create the folder where the repository is going to be located:
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
Intento de edicion
