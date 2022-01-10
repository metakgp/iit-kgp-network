# Index


* 0\. [Index](#index)
* 1\. [Information about Institute Internet](#1-problems-with-institute-internet)
  * 1.1 [Packet Filtering and Services](#11-packet-filtering-and-services)
  * 1.2 [Working VPNs](#12-working-vpns)
    * 1.2.1 [Interesting : ExpressVPN works](#121-interesting--expressvpn-works)
  * [Solution to the above problems](#solution-to-the-above-problems)
  * 1.3 [Slow WIFI Speed](#13-slow-wifi-speed)
    * 1.3.1 [Best Solution](#131-best-solution)
    * 1.3.2 [Feasible Solution](#132-feasible-solution)
* 2\. [To Do](#2-to-do)
* 3\. [Contributing](#3-contributing)
* 4\. [Credits](#4-Credits)

# 1. Problems with Institute Internet


## 1.1 Packet Filtering and Services

| Protocol | Status | Proof | Remarks |
| ---  | --- | --- | --- |
| UDP  | ⚠️ | <ul><li> Programs using UDP like `dig`, `nslookup` (DNS on port 53). No custom DNS work neither on port 53, nor on 5353</li><li> The problem is some UDP ports **work**. I created a UDP port using netcat on DigitalOcean server on port `55554` and connected it from the institute wifi network using netcat on my laptop and it connected.</li></ul> | <ul><li>Its really confusing what is happening. Need more insight on how filtering is happening. Loos like `standard ports`, `DNS Servers` and common `IP addresses` are being blocked. Need more info</li><li>Need to create own UDP server and test if its just connecting or data is also transferred.</li><li>Need to look at implementation of netcat if required to know how it works with UDP.</ul> |        
| TCP  | ⚠️ | <ul><li>Netcat server on DigitalOcean on port `55555` connected successfully on netcat client on laptop as well as on `telnet`</li><li>`ssh` to external servers doesn't work (common ports maybe blocked)</li><li>`tor` cannot be used (TCP over LTS) as it cannot connect to the nodes (strange : bare IPs are blocked)</li><li>TCP Based VPNs do work even though very much slow</li></ul>|<ul><li>Domain name servers work, but bare IP addressees don't work</li><li>Strangely bare IP to my DigitalOcean server connected on netcat</li><li> Need more info by creating server on various ports </li></ul>|
| ICMP | ❌ | `ping` and `traceroute` doesn't work at all | ICMP packets are plainly dropped |

There is packet filtering too as the network prohibits the use of ceritifcates for the connection and uses `PEAP + MSChapv2` which is very much vulnerable.  Credentials can be cracked easily. So it's better to use implement some security methods. For more info lookup : `chapcrack`.



## 1.2 Working VPNs


- Not all **UDP based** VPNs working ( reason [maybe] : UDP packets directly dropped )
- Some **TCP based** VPNs work but are really slow of course due to the facilities provided by TCP
- List of VPNs :

| VPN / DNS | Platform | Status |
| --- | --- | --- |
| ExpressVPN | ![w] ![l] ![a] | ✔️ |
| Psiphon | ![a] | ✅ |
| HoxxVPN | ![w] ![l] | ✅ |
| SetupVPN | ![w] ![l] | ✅ |
| HotspotShield | ![w] ![l] | ❔ |
| Warp (1.1.1.1) | ![w] ![l] ![a] | ❌ |
| NordVpn | ![w] ![a] | ❌ |
| VPNHub by P\*rnhub |  ![a] | ❌ |
| OpenVPN hosted on Digital Ocean | ![w] ![l] ![a] | ❌ |
| Wireguard hosted on AWS EC2 | ![w] ![l] ![a] | ❌ |
| OpenVPN / Wireguard hosted on Azure | ![w] ![l] ![a] | ❔ |
| OpenVPN / Wireguard hosted on Linode | ![w] ![l] ![a] | ❔ |
| Tor | ![w] ![l] ![a] | ❌ |

❔ : check pending <br/>
✅ : Connected but so slow that it's unusable

> Note : OpenVPN hosted on Linode has been successfully used by a senior but it costs momey to buy server credits. AWS, Azure, DigitalOcean free credits can be acquired using student account via Github. Wish they worked. The senior also informed something about using ngrok too. Need more information 


### 1.2.1 Interesting : ExpressVPN works


Express VPN works and it works damn fast - it uses `Lightway Protocol` whose core is open sourced now [here](https://github.com/expressvpn/lightway-core) - and a combination of `iptable` rules and `DNS Resolution`.


My speculation is that it runs in TCP Mode and its fast. But I need to verify this by looking at logs and iptable entries. I speculate that `Lightway UDP` doesn't work because I tried it specifically on the Android version of the app, it didn't connect at all where the TCP counterpart connected quickly.


> So the ray of hope is that using the lightway core and iptables we may be able to manage creating out our version of VPN that can be hosted on any server obtained by Student credits.

***


## Solution to the above problems

Its not much right now, but I am currently working on it. Reasearching currently about VPNs. I am really new to this, so it's gonna take some time 🥲

***

## 1.3 Slow WIFI Speed

The institute has a fast Ethernet connection but a notoriously slow Wifi due to its usage of `2.4 ghz` and `20MHz` bandwidth with a Bit-rate of `72.2Mb/s` (Megabits/s). This wifi is shared with many people in the same wing which brings its speed down to 10-12 Mbps.



```console
lagnos@rog:~$ iwconfig wlo1
wlo1      IEEE 802.11  ESSID:"STUDENT_SECURED"
          Mode:Managed  Frequency:2.412 GHz  Access Point: E8:BA:70:61:38:E2
          Bit Rate=72.2 Mb/s   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=50/70  Signal level=-60 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:2004  Invalid misc:5420   Missed beacon:0
```


### 1.3.1 Best Solution


**Just buy a router**


Buy a good 300Mbps or (1 Gbps if u are rich) aand then use ethernet interface to distribute internet wia the wifi interface.<br/>
Setting up can be a bit tedious for beginners but it is relatively easier and much better than the next solution.

> Benefits : You can get 300Mbps internet, and even if u share with 3 room mates u still get arorund 100 Mbps in the worst case scenario which is much better than getting 12-13 Mbps on Wifi


### 1.3.2 Feasible Solution


This solution can be used if u have raspberry pi with you and don't want to buy a router.<br/>
- The logic is same, route the connections on Wifi interface via the ethernet interface.<br/>
- Buy a 150 Mbps usb adapter

> For detailed config : Check out my post [here](./rpi-express.md).<br/>
Benefits : As in the previous solution you can get much better speed than the institute wifi and can enjoy online streaming. Cheers!


# 2. To Do


- [ ] Verify protocols and services filtering, need more proof.
- [ ] Verify VPNs except Express VPN if they do really work across devices. Detailed testing should bee done if many methods are available to connect.
- [ ] Research on ExpressVPN protocol being used across devices, iptables methds and DNS Bypassing.
- [ ] Check if `ngrok` works properly and if it works, what methodology does it use / and compare to other vpn protocols


# 3. Contributing

For tasks, take a look at [To Do section](#2-to-do). All help is appreciated. For VPN testing tasks, please create a new issue and attach/enter the following data (even if the VPN failed ) :

For all systems : 

- Error or warning messages if any.
- If the VPN failed or worked
- If the VPN worked, check `DNS Leak` from here (any of the standard or extended test) : [https://www.dnsleaktest.com/](https://www.dnsleaktest.com/results.html) .DNS Leak test is **passed** only if the IP addresses shown in the results are the IP address assigned buy the VPN. Enter either *passed* or *failed* for this.

:warning: DNS Leak test is important as the institute does filter DNS requests. Please don't open any blocked website right away before check the DNS Leak Test. First perform the test, then verify the IP location at atleast 2 website service online.

For Linux tests only :

- Name of the dns resolver used by your system.
- Contents of `/etc/resolv.conf` before and after using the vpn.
- `iptables` rules before and after using the vpn.

ℹ️ VPN Tests on Linux is preferred as it will provide much more information than the other OS.

# 4. Credits

A great vote of thanks to the following contributors :
- Ishan Manchanda (@IshanManchanda) - Contribution to the list of working VPNs.


***


<h3 align="center">Thank You for reading and contributing! ❤️❤️❤️ </h3>

<!-- Icons Load -->
[w]:./window.png 
[l]:./linux.png
[a]:./android.png
