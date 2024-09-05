
# wpa_supplicant

[Arch linux docs](https://wiki.archlinux.org/title/Wpa_supplicant)
uses the wpa_cli to actually do all of the connecting things

## connecting to wifi network
based mostly on this [forum thread](https://sirlagz.net/2012/08/27/how-to-use-wpa_cli-to-connect-to-a-wireless-network/) with some things more flashed out and hopefully better explained

$ = shell commands 
\> = commands inside wpa_cli
\# = comments and should be ignored

\wlp* means any network interface that starts with wlp 
```shell
#getting the right wifi access point
$ ip link show
<list of host addresses>
<one should be named wlp*>

#invoking wpa_cli
$ wpa_cli -i <interfaceName (wlp*)>
Selected interface 'wlan0'

Interactive mode
> scan 
<2>CTRL-EVENT-SCAN-RESULTS

>scan_results
#example data taken from forum thread
bssid / frequency / signal level / flags / ssid
00:55:ab:25:ac:5a 2462 -71 [WPA2-PSK-CCMP][ESS] WLAN-Network
00:11:99:51:ba:f0 2437 -64 [WPA2-PSK-CCMP][ESS] WLAN-Network2
> add_network #creates a new network
0 #network ID
> set_network 0 ssid "WLAN-Network" #replace your Wlan network with said ssid 
> set_network 0 psk "<insert the password for said network>"
> enable_network 0
> save_config # not yet tested 
> reconnect # not really needed 
```

for more info go to the above linke forum thread, this is more of a small rundown of how to use it 


## adding it a bit more permanently
we use the 
```sh
> save_config
```
command
