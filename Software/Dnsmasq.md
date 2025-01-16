# creating a PXE server



[a github guid](https://github.com/WillChamness/Dnsmasq-PXE)

```shell
sudo dnsmasq  -d --interface=enp1s0 --dhcp-range=10.13.37.100,10.13.37.101,255.255.255.0,1h --dhcp-boot=bootx64.efi --enable-tftp --tftp-root=<path to your pxe root direcotry> --log-dhcp
```

## dnsmasq: failed to create listening socket for port 53: Address already in use

this is usually the case because of systemd-resolved you can simply stop this service and everything will continue to work.
