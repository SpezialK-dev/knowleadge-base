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

# Setting up for direct SSH connections 

because sometimes you might just want to directly connect through something 
[A unix stackexchange post about it ](https://unix.stackexchange.com/questions/295238/how-to-connect-to-device-via-ssh-over-direct-ethernet-connection)

the following bash script will set up an appropriate server.

```shell
sudo dnsmasq -d -C /dev/null --port=0 --domain=localdomain --interface=<your ethernet interface> --dhcp-range=192.168.9.2,192.168.9.10,99h
```

-C /dev/null means it does not read the normal config file 
--port=0 --domain=localdomain deaktivates the dns server 