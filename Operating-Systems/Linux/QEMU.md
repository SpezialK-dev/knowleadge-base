# BASIC commandline Usage 

this explains some basic commandline usage

# Windows 

## creating a inital virtual maschine 
[A guid](https://pragmaticaddict.com/qemu-win10.html)
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
    -net nic,model=virtio-net-pci -net user,hostname=win11 \
    -monitor stdio \
    -name "win11" \
    -display gtk,grab-on-hover=on \
    
"$@"
```
the last line "$@" allows more commandline parameters
all of the commands are explained in the top linked article 
excep the -tpm modul this is from the faking a TPm setion 


```sh
sh <script from abouve>.sh -boot d -drive file=<path to windows iso>.iso media=cdrom 
```


## Faking a TPM 
this is to fake a TPM modul to satisfy the windows 11 Instalation aswell as for research purposes.

A Guid on [TPM2 Device emulation](https://tpm2-software.github.io/2020/10/19/TPM2-Device-Emulation-With-QEMU.html) 


run the following command to start emulating a tpm 


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
  -tpmdev emulator,id=tpm0,chardev=chrtpm -device tpm-tis,tpmdev=tpm0

```
