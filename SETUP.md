## Setup

### base setup procedure on embedded boards

 - mkfs (ext3, ext4) on SD card, first sector: +100M
 - `dd(1)` uBoot + kernel (device specifig) to SD card
 - mount SD card, `cd(1)` into mountpoint
 - `debootstrap --foreign --arch armhf --verbose wheezy . http://ftp.at.debian.org/debian/`
 - edit inittab:
```
T0:23:respawn:/sbin/getty -L ttymxc0 115200 vt100
T1:23:respawn:/sbin/getty -L ttymxc1 115200 vt100
T2:23:respawn:/sbin/getty -L ttymxc2 115200 vt100
T3:23:respawn:/sbin/getty -L ttymxc3 115200 vt100
```
 - boot, login
 - `cd /debootstrap ; debootstrap --second-stage`
 - reboot, configure ethernet (DHCP)
 - `apt-get install xserver-xorg xserver-xorg-video-fbdev iceweasel
   x11-apps -y`

#### engicam specific:
```
sudo dd if=/srv/default_image/uImage of=/dev/sdb bs=1M seek=1
sudo tar xf /srv/default_image/rootfs.tgz
```