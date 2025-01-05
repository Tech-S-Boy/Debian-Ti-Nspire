# Debian-Ti-Nspire

This is the repo where you can find the files and scripts to install debian on your Ti-Nspire

Prerequired :
A Ti-Nspire with Ndless
An Usb-mini-b otg cable (you can diy it)
A computer (or phone that runs linux)
An usb the size depends on what distribution you want on it and app, i use 4 gb image to be faster to flash
Internet (how are you reading this if you don't have it),only required to build the debian rootfs
Note !: i use linux and windows in this guide so some parts you will need to find yourself or use wine (might change later).
You can also get a premade image from the releases.

# 1st step:
Install all required stuff.
Download HHDRawcopy from the repo.
Rootfs: (if not making your own rootfs download your image) 
https://www.mediafire.com/file/v2zlm17qqsjrijj/Debian_Lenny_%2528X_server_is_broken%2529_V0.1.img/file
# Commands :
Install prerequisites :
sudo apt-get install debootstrap qemu-user-static
Make the directory and image of the rootfs : 
mkfs debian
sudo dd if=/dev/zero of=image.img iflag=fullblock bs=1M count=SIZE-OF-ROOTFS-IN-MB && sync
sudo mkfs -t ext3 image.img
sudo mount -o loop -t auto image.img debian/
After installing debootstrap and qemu make the root fs with this command :
Debian stretch: sudo debootstrap --foreign --arch=armel stretch debian/ http://archive.debian.org/debian/
Debian Bookworm (slower): sudo debootstrap --foreign --arch=armel bookworm debian/
After configuring it chroot into the install
Way 1 (if linux is with you):
sudo chroot debian/ /debootstrap/debootstrap --second-stage
sudo chroot debian/
Way 2 (if linux isn't with you):
cp /usr/bin/qemu-arm-static debian/usr/bin/qemu-arm-static
sudo chroot debian/ qemu-arm-static --cpu arm926 /debootstrap/debootstrap --second-stage
sudo chroot debian/ qemu-arm-static --cpu arm926 /bin/bash

