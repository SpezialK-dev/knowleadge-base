# creating a PXE server
first to just boot a normal windows of this to install it. 

[a github guid](https://github.com/WillChamness/Dnsmasq-PXE)
[setting it up as tftp server](https://stelfox.net/blog/2013/12/using-dnsmasq-as-a-standalone-tftp-server/)

```shell
sudo dnsmasq  -d --interface=enp1s0 --dhcp-range=10.13.37.100,10.13.37.101,255.255.255.0,1h --dhcp-boot=bootx64.efi --enable-tftp --tftp-root=<path to your pxe root direcotry> --log-dhcp
```
though this command is not enought to get a working PXE boot. 

## 


## dnsmasq: failed to create listening socket for port 53: Address already in use

this is usually the case because of systemd-resolved you can simply stop this service and everything will continue to work.
