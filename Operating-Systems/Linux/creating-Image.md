# Debian 


## packages required under arch linux 

- libisoburn (xorriso)
- rsync
- squashfs-tools
## Some guids 

This is a guid on creating a Debian image with some modified InitramFS. To allow
[A small guid (0)](https://d-i.debian.org/doc/internals/ch04.html)
A better guid that isnt offical seems this [Linuxquestions (1)](https://www.linuxquestions.org/questions/debian-26/tutorial-creating-a-custom-bootable-debian-live-iso-4175705804/)
with some adjustments from the [debian wiki: repack bootable iso (2)](https://wiki.debian.org/RepackBootableISO). 

## With secure boot

since we want to maintain the securebootability of this we will use a already signed instllation for this we will get a normal Installation of your choosing for debian.

the following commands are taken from Guid 1.

firstly we are geting out a isohdpfx.bin from the image 
```shell
dd if=<your debain ISO here>.iso bs=1 count=432 of=isohdpfx.bin
```

this creates the proper dirs in our current directory 
```shell
mkdir isoextract mnt
```

>OPTIONAL : 
> elevate to root with su or use the sudo in-front of these commands your choice

 
first we will mount it as a loopback device to mnt 
```shell
sudo mount -o loop <your debain ISO here>.iso mnt
```
then we will get all of the data from rsing excluding the squashfs system and copy t hat to the iso extracted dir 
```shell
rsync --exclude=/live/filesystem.squashfs -a mnt/ isoextract
```

Some steps are missing from here since the squasfs filesystem would not show up So I am trying a different aproach. with the Arch image. 
# Creating a secured boot Arch image

This Microsoft signed Ubunut shim exists this could be used to boot Arch linux which has a lot better documentation than debian. 
[shim-signed 15.8+ubuntu+1.59-1](https://aur.archlinux.org/packages/shim-signed)

This might fit better with my purpose.

you can acutally do it with a  [preloader](https://wiki.archlinux.org/title/Unified_Extensible_Firmware_Interface/Secure_Boot#PreLoader) as descriebed in one of the methodes in this [wiki page](https://wiki.archlinux.org/title/Unified_Extensible_Firmware_Interface/Secure_Boot#ISO_repacking)
