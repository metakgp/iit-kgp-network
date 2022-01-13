# Index


* 0\. [Introduction](#0-introduction)
* 1\. [VPNs](#1-vpns)
  * 1.1 [Packet Filtering and Services](#11-packet-filtering-and-services)
  * 1.2 [Working VPNs](#12-working-vpns)
    * 1.2.1 [Using OpenVPN](#121-using-openvpn)
    * 1.2.2 [Using Wireguard](#122-using-wireguard)
    * 1.2.3 [Observation : ExpressVPN works best](#123-observation--expressvpn-works-best)
  * [Solution](#solution)
* 2\. [Slow LAN Speed](#2-slow-lan-speed)
* 3\. [Slow WIFI Speed](#3-slow-wifi-speed)
    * 3.1 [Best Solution](#31-best-solution)
    * 3.2 [Feasible Solution](#32-feasible-solution)
* 4\. [Discussion](#4-discussion)
* 5\. [To Do](#5-to-do)
* 6\. [Contributing](#6-contributing)
* 7\. [Credits](#7-credits)


# 0. Introduction


In this repo, I will write about the problems students face on campus network and attempt to provide solution (feasible or non feasible). The solutions end at Section 2.

From Section 3, I will write in depth discussion on why does few protocols, which are really good, like OpenVPN, Wireguard, etc. do not work on campus network. Feel free to skip this section if you are not interested.

Section 4 deals with Contributing rules and Section 5 ends with a vote of thanks to people who helped me in anyway.


# 1. VPNs


## 1.1 Packet Filtering and Services

| Protocol | Status | Proof | Remarks |
| ---  | --- | --- | --- |
| UDP  | ✅ | <ul><li>The network connected well to server hosted on Cloud on non standard port `55555` over UDP.</li></ul>  | <ul><li> UDP works and connects to an external server on **non reserved ports** (>1023)</li><li> As common and reserved ports are most probably blocked, services like `DNS` doesn't work. Hence programs depending on DNS-name resolution like `dig` and `nslookup` won't work. The server is able to use **only the DNS provided by campus network DHCP** </li><li>To make DNS work we need `iptables` magic on Linux. This `iptables` is used by expressvpn to forward DNS requests. Read More in Discussions.</li></ul> |        
| TCP  | ✅ | <ul><li>Server hosted on cloud could be connected via `netcat` and `telnet` without issues on port `55555` and similar private ports.</ul>|<ul><li>TCP Based VPNs do work even though very much slow</li><li>Servers outside the campus network can be accessed over TCP comfortably,, **on non reserved ports** (ports > 1023)</li><li>`tor` cannot be used (TCP over LTS) as it cannot connect to the nodes.</li><li> Need to check tor on a private port and update info.</ul>|
| ICMP | ❌ | <ul><li>`ping` and `traceroute` doesn't work at all</li></ul> | <ul><li>ICMP packets are plainly dropped displaying normal firewall behaviour.</li></ul> |


ℹ️ **Very Important Note** : Externally hosted servers can be accessed on private ports via both TCP and UDP. The problem is that a ` internally hosted server cannot be exposed to the external network`. Creation of socket on the all itnerface (0.0.0.0) requires resolution of hostname by the function `getnameinfo` which requires DNS resolution - which doesn't work due to the firewall. My strong speculation is that this can too be bypassed using `iptables` or `ngrok`.


## 1.2 Working VPNs


- Not all **UDP based** VPNs working ( reason [maybe] : UDP packets directly dropped )
- Some **TCP based** VPNs work but are really slow of course due to the facilities provided by TCP
- List of VPNs :

| VPN / DNS | Platform | Status |
| --- | --- | --- |
| ExpressVPN (Not free) | ![w] ![l] ![a] | ✔️ |
| Psiphon | ![a] | ✅ |
| HoxxVPN | ![w] ![l] | ✅ |
| SetupVPN | ![w] ![l] | ✅ |
| HotspotShield | ![w] ![l] | ❔ |
| Warp (1.1.1.1) | ![w] ![l] ![a] | ❌ |
| NordVpn | ![w] ![a] | ❌ |
| VPNHub by P\*rnhub |  ![a] | ❌ |
| OpenVPN hosted on Digital Ocean | ![w] ![l] ![a] | ❌ |
| OpenVPN hosted on Digital AWS ec2 | ![w] ![l] ![a] | ✅ |
| OpenVPN / Wireguard hosted on Linode | ![w] ![l] ![a] | ❔ |
| Wireguard hosted on AWS EC2 | ![w] ![l] ![a] | ❌ |
| Tor | ![w] ![l] ![a] | ❌ |

❔ : check pending <br/>
✅ : Connected but really slow

> Note : OpenVPN hosted on Linode has been successfully used by a senior but it costs momey to buy server credits. AWS, Azure, DigitalOcean free credits can be acquired using student account via Github. Wish they worked. The senior also informed something about using ngrok too. Need more information 


### 1.2.1 Using OpenVPN


### 1.2.2 Using Wireguard


### 1.2.3 Observation : ExpressVPN works best


Express VPN works and it works damn fast - it uses `Lightway Protocol` whose core is open sourced now [here](https://github.com/expressvpn/lightway-core) - and a combination of `iptable` rules and `DNS Resolution`.


My speculation is that it runs in TCP Mode and its fast. But I need to verify this by looking at logs and iptable entries. I speculate that `Lightway UDP` doesn't work because I tried it specifically on the Android version of the app, it didn't connect at all where the TCP counterpart connected quickly.


> So the ray of hope is that using the lightway core and iptables we may be able to manage creating out our version of VPN that can be hosted on any server obtained by Student credits.


***


## Solution

Its not much right now, but I am currently working on it. Reasearching currently about VPNs. I am really new to this, so it's gonna take some time 🥲

Ignore this section please.


***


# 2. Slow LAN Speed


# 3. Slow WIFI Speed

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


## 3.1 Best Solution


**Just buy a router**


Buy a good 300Mbps or (1 Gbps if u are rich) aand then use ethernet interface to distribute internet wia the wifi interface.<br/>
Setting up can be a bit tedious for beginners but it is relatively easier and much better than the next solution.

> Benefits : You can get 300Mbps internet, and even if u share with 3 room mates u still get arorund 100 Mbps in the worst case scenario which is much better than getting 12-13 Mbps on Wifi


## 3.2 Feasible Solution


This solution can be used if u have raspberry pi with you and don't want to buy a router.<br/>
- The logic is same, route the connections on Wifi interface via the ethernet interface.<br/>
- Buy a 150 Mbps usb adapter

> For detailed config : Check out my post [here](./rpi-express.md).<br/>
Benefits : As in the previous solution you can get much better speed than the institute wifi and can enjoy online streaming. Cheers!



# 4. Discussion


This section is a read for people who wish to know why various protocols like Wireguard or OpenVPN did not work. Anything that is written here are my observations and may not be absolutely correct. If you find any error please open an issue and inform me about it to make this repository more accurate. This is going to be a long read, so buckle up 🚀.

I feel blocking of UDP is a major culprit in VPNs not working. I am not sure but the topics here I discuss will be updated, because I will try my best to verufy those with supporting resources.

There is packet filtering (speculated too) as the network prohibits the use of ceritifcates for the connection and uses `PEAP + MSChapv2` which is very much vulnerable.  Credentials can be cracked easily. So it's better to use implement some security methods. For more info lookup : `chapcrack` on Google.

# 5. To Do


- [ ] Check tor working on non reserved port and update info
- [ ] Check if TCP and UDP are working on ports between (1024 and 49151) : reserved ports
- [ ] Verify VPNs except Express VPN if they do really work across devices. Detailed testing should bee done if many methods are available to connect.
- [ ] Research on ExpressVPN protocol being used across devices, iptables methds and DNS Bypassing.
- [ ] Check if `ngrok` works properly and if it works, what methodology does it use / and compare to other vpn protocols


# 6. Contributing

For tasks, take a look at [To Do section](#2-to-do). All help is appreciated. Please create a new issue to contribute. For VPN testing tasks, attach/enter the following data (even if the VPN failed ) :

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

For protocol testing tasks, please attach the following:
- The method of testing
- Screenshots or outputs from various programs if used like, `tcpdump` , `wireshark`, etc.

# 7. Credits

A great vote of thanks to the following contributors :
- Ishan Manchanda ([@IshanManchanda](https://github.com/IshanManchanda)) - Contribution to the list of working VPNs.
- Soham Sen ([@FadedCoder](https://github.com/FadedCoder)) - Testing UDP and TCP on external network on private ports via `netcat`.
- Rajiv Harlalka ([@rajivharlalka](https://github.com/rajivharlalka)) and Chirag Ghosh ([@chirag828049](https://github.com/chirag828049)) - Helping me with OpenVPN Setup.


***


<h3 align="center">Thank You for reading and contributing! ❤️❤️❤️ </h3>

<!-- Icons Load -->
[w]:./window.png 
[l]:./linux.png
[a]:./android.png
