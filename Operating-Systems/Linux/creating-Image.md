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


## Required packages to follow this guid 

- [ArchIso](https://archlinux.org/packages/extra/any/archiso/)
- [PreLoader-Signed (AUR)](https://aur.archlinux.org/packages/preloader-signed) is optional and can be downloaded from other sources. 

## some sources

[Arch wiki on signed boot loaders](https://wiki.archlinux.org/title/Secure_Boot#Using_a_signed_boot_loader)

[Archboot](https://archboot.com/) also seems like a greate ressource if you want to take a look at secure boot. 
These images should be ready to boot, if you dont want to create your own and just want a secure boot ready installation. 


This is an alternative if you dont want to use preloader. 
[shim-signed 15.8+ubuntu+1.59-1](https://aur.archlinux.org/packages/shim-signed)

This might fit better with my purpose.

you can acutally do it with a  [preloader](https://wiki.archlinux.org/title/Unified_Extensible_Firmware_Interface/Secure_Boot#PreLoader) as descriebed in one of the methodes in this [wiki page](https://wiki.archlinux.org/title/Unified_Extensible_Firmware_Interface/Secure_Boot#ISO_repacking)


The tool used to create Archisos is called [archIso](https://wiki.archlinux.org/title/Archiso). The documentation is very helpfull in creating a base iso with what we need. 



## Actual rundown 

the following commands are all exectued under archlinux, under a different distro you would need to clone the tool first. 

since we want to modify the image we will make a copy 
```shell
cp -r /usr/share/archiso/configs/releng/ <dir that you want to work in>
```
I chose releng since I might need extra tooling but you could also slim this down a lot and just use baseline. 

If you want to customize things like hostname and the like you should be doing that in the airootfs, this is the filesystem that gets loaded during the startup as the live system. 


### setting up secure boot
Since we want secure boot on this ISO, and we dont want

The arch wiki has [2 options to enable secure boot](https://wiki.archlinux.org/title/Unified_Extensible_Firmware_Interface/Secure_Boot#Booting_an_installation_medium) you can repack the installation medium to include secure boot. I would use Preloader since I do not care about frequent kernel signing and I dont want to load new keys everysoften. 

This should be patchable to any arch installation.
Thus this step should be execute when the disk is created. 
The only problem Could be with preloader is that the ones that exist in the repos are from 2013 so quite old by now. They will work until 2026. This is when the keys will expire. And the Preloader might not work anymore. [Taken from this blog Post](https://blog.hansenpartnership.com/linux-foundation-secure-boot-system-released/) Since the binarys are also in the linked in the blogpost.

#### Replacing the boot loader 

[We will use this aproach](https://wiki.archlinux.org/title/Unified_Extensible_Firmware_Interface/Secure_Boot#Replacing_the_boot_loader_with_PreLoader) since, this is the easiest. 


### Further customization 


### Creating the image 

the command to create the image is as follows 

```shell
sudo mkarchiso -m iso -A <name of your application> -v ./ -w <path where you're files are>/releng <path where you're files are>/releng/
```

the -o option optional


#### Error <> is missing profiledef.sh


the file is inside of the image. 
