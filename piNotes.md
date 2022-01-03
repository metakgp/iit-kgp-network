#Acheieved Goals:

- Wifi connection at LBS:n<br/> 

| Device | Before | After | After with Express Vpn |
| --- | --- | --- | --- |
| Android | 16 Mbps | 60 Mbps | Same: 58-60 Mbps |
| Laptop | 8 Mbps | 24 Mbps | Same: 20-24 Mbps |

- Able to run vpn on raspberry pi.
- Generally to connect two different devices with VPN we need to different account connections ( for express vpn key obtained for free through some resources ). This lead to exhaustion of key + the slow wifi made it unusable. But now multiple devices can connect to the Pi and use vpn with just one account registered with Pi and that too with *high* speed!

#Method:

The method is very trivial to understand, just the setup was a bit tough ( for me :D ) <br/>
<img src="./piLan-img.jpg" width=900px height=400px />


#Tech Stack:

- hostapd : for AP creation (( check fast alternatives ))
- dnsmasq : for DNS/DHCP configuration of clients (( check for better and faster alternatives ))
- expressvpn : (( research in progress to find a better alternative [free, open source] ))

#Configs:

##interfaces config

##dnsmasq config

##hostapd config

##iptables config

#Know Issues and Bugs:

- Express vpn does not work properly - a dns issue as it cant retrieve ip addresses given the hostname but it CAN ping directly to ip addresses -if force_vpn_dns is true (( insti network blocks custom dns - need more data to verify, maybe wrong )).<br/>
Workaround : <br/>
1. Expressvpn after connecting saves dns address in file at `/etc/resolv.conf.bak` or similar ( can be verified by viewing the file ).
2. Just copy that dns address and paste it in the file `/etc/resolv.conf`.
3. To let connected clients connect to internet on vpn edit the file `/etc/dnsmasq.conf` and edit the line `server=<EXPRESSVPN IP HERE>` and then reload the dns service using `sudo systemctl restart dnsmasq.service`.<br/>

- Speed is slower : LAN 300 Mbps -> VPN 70 Mbps on Pi -> 60 Mbps Android (( MAYBE DUE TO BOTTLENECK ON PI and LESS BANDWIDTH OF INBUILT WIFI ADAPTER## To be verified with Pi fan and usb wifi 300Mbps ))

- Redirection issues while opening some nsfw websites (xnxx,xvideos) and torrent sites (1337x.to, rarbg.to) but pornhub, whatsapp, telegram, slack, discord, steam and online games work.
