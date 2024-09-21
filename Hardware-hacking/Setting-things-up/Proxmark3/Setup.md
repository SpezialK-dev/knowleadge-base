
# A small guid on how to set up your proxmark under Arch linux

[Installation Guid](https://github.com/RfidResearchGroup/proxmark3/blob/master/doc/md/Installation_Instructions/Linux-Installation-Instructions.md)
[Compilation instructions](https://github.com/RfidResearchGroup/proxmark3/blob/master/doc/md/Use_of_Proxmark/0_Compilation-Instructions.md)

## Choosing a firmware 

The normal firmware proxmark firmware seems to be outdated ? The most maintained firmware seems to be the one from [iceman](https://github.com/RfidResearchGroup/proxmark3) . Here we also have documentation for Arch linux.


## Installing the right dependencies 

```shell
sudo pacman -Syu git base-devel readline bzip2 lz4 arm-none-eabi-gcc \
arm-none-eabi-newlib qt5-base bluez python gd --needed
```

IMPORTANT remove [modem manager ](https://github.com/RfidResearchGroup/proxmark3/blob/master/doc/md/Installation_Instructions/ModemManager-Must-Be-Discarded.md)


the clone the repo
```shell
git clone https://github.com/RfidResearchGroup/proxmark3.git
```