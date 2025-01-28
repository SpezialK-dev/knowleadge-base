
shim allows you to secure boot using the microsoft signed keys.

This can be usefull when dualbooting 

# disableing checking
if you want to load unsigned kernel modules or even an unsigned kernel but still have secure boot enabled in the bios you can simply disable shim checking for those things with the userland application mokutil

```shell
mokutil --disable-validation
```

this disables verifikation, and this allows unsigned code to run after the shim.
while still allowing you to secure boot. This also persistes between installations. since it is stored as a uefi variable most likely on the motherboard. 