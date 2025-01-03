# BASIC commandline Usage 

this explains some basic commandline usage

# Windows 

## creating a inital virtual maschine 
[A guid for win10](https://pragmaticaddict.com/qemu-win10.html)
[Win11 adds some more complexity](https://k4i.top/posts/windows-11-vm-with-qemu-kvm/)
Though some things can be let out since this is orignally aimed at people wanting to update garmin devices the normal setps can be reproduuced just with small changes

the following command creates the your virtual drive
```shell
qemu-img create -f qcow2  <name of the drive>.qcow2 100G
```

the following command then runs the Virtual maschine 
```shell
#!/bin/sh 

exec qemu-system-x64_64 \
    -enable-kvm -cpu host -m 16G \
    -drive file=<name of your drive>,if=virtio \
    -device  virtio-tablet \
    -rtc base=localtime \
    -net nic,model=virtio-net-pci -net user,hostname=win10 \
    -monitor stdio \
    -name "win10" \
    -display gtk,grab-on-hover=on \
    
"$@"
```
the last line "$@" allows more commandline parameters
all of the commands are explained in the top linked article 
excep the -tpm modul this is from the faking a TPm setion 


```sh
sh <script from abouve>.sh -boot d -drive file=<path to windows iso>.iso media=cdrom 
```

### Win 11
the above mentionted will not work wit win 11

the abouve should work with win10 and below but windows 11 brings another challange so we have some problems. 

That are mainly TPM 2.0 and Secure boot requirements. You can disable/bypass them but that is not what you usually want if you want to test something in that regard
```shell
#!/bin/sh 

exec qemu-system-x64_64 \
    -machine q35,smm=on,accel=kvm \    
    -enable-kvm -cpu host -m 16G \
    -drive file=<name of your drive>,if=virtio \
    -device  virtio-tablet \
    -rtc base=localtime \
    -net nic,model=virtio-net-pci -net user,hostname=win11 \
    -monitor stdio \
    -name "win11" \
    -display gtk,grab-on-hover=on \
    -chardev socket,id=chrtpm,path=/tmp/emulated_tpm/swtpm-sock \
    -tpmdev emulator,id=tpm0,chardev=chrtpm -device tpm-tis,tpmdev=tpm0 \     
    -drive if=pflash,format=raw,readonly=on,file=<Path to OVMF_CODE.secboot.4m.fd> \
    -drive if=pflash,format=raw,file=<Path to OVMF_VARS.4m.fd> \

"$@"
```

THe Following command needs to be run in a seperate terminal window everytime before you start the VM to create a new TPM modul
```shell
mkdir /tmp/emulated_tpm
swtpm socket --tpmstate dir=/tmp/emulated_tpm --ctrl type=unixio,path=/tmp/emulated_tpm/swtpm-sock --log level=20 --tpm2
```



## Faking a TPM

the following additional packages need to be installed 
 
this is to fake a TPM modul to satisfy the windows 11 Instalation aswell as for research purposes.

A Guid on [TPM2 Device emulation](https://tpm2-software.github.io/2020/10/19/TPM2-Device-Emulation-With-QEMU.html) 


run the following command to start emulating a tpm 
It needs to be run every time you want to start the VM if the command isnt already running

```shell
mkdir /tmp/emulated_tpm
swtpm socket --tpmstate dir=/tmp/emulated_tpm --ctrl type=unixio,path=/tmp/emulated_tpm/swtpm-sock --log level=20 --tpm2
```

this creates a temporary directory for the tpm state and then opens a socket for wich the tpm can communicate with the VM.

the the following option needs to be added to the VM script 
as it is mentioned before 
```shell
    ...
  -chardev socket,id=chrtpm,path=/tmp/emulated_tpm/swtpm-sock \
  -tpmdev emulator,id=tpm0,chardev=chrtpm -device tpm-tis,tpmdev=tpm0 \

```


## Faking secure boot and UEFI

The packages you need to have fake secure boot are 

- swtpm
- edk2-ovmf

some sources used to understand this 
[Superuser Question](https://superuser.com/questions/1660806/how-to-install-a-windows-guest-in-qemu-kvm-with-secure-boot-enabled)
[Securish boot with qemu](https://www.labbott.name/blog/2016/09/15/secure-ish-boot-with-qemu/)



### UEFI 

first we will create a backup of the firmware files that we installed with edk2-ovmf. 
Since I do not want them changed, though they should not change but this also shortens our paths. 


you might need to adjust these paths since they where used under arch linux 
```shell
cp /usr/share/edk2/x64/* ./UEFI/
```
Theoretically you only need to copy the VARs file since that is the  only thing being [changed](https://wiki.debian.org/SecureBoot/VirtualMachine)
 

the add the following 4 lines to your script 
```shell 
...   
 #UEFI 
    -drive if=pflash,format=raw,readonly=on,file=<Path to OVMF_CODE.secboot.4m.fd> \
    -drive if=pflash,format=raw,file=<Path to OVMF_VARS.4m.fd> \
    -machine q35,smm=on,accel=kvm \
```

##### Display output not active

you forgot to add the line 

```shell
-machine q35,smm=on,accel=kvm \
```
most likely 

##### Failed to load Boot0001 "UEFI Misc Device" from ...
[Proxmox Forums](https://forum.proxmox.com/threads/guest-has-not-initialized-the-display-yet-on-new-ovmf-vms-after-update-to-7-0-13.98179/) 

Just wait to get into the UEFI shell 
once you are there type the following commands :


[Command Help](https://hatchjs.com/efi-shell-version-2-70-commands/)
[A helpfull guid to fixing this problem and related ones ](https://mricher.fr/post/boot-from-an-efi-shell/)

if you wait long enought you get into a uefi boot menue where you can should be able to select the boot drive but it does not find any drives.
