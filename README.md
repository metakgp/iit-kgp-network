# Index

* [0 Index](#index)
* [1 A journey to understand VPN](#a-journey-to-understand-vpn)
* [2 Information about Institute Internet](#information-about-institute-internet)
  * [2.1 Packet Filtering and Services](#packet-filtering-and-services)
  * [2.2 Information Related to VPNs](#information-related-to-vpns)
    * [2.2.1 A Ray of Hope : ExpressVPN works](#a-ray-of-hope--expressvpn-works)
  * [2.3 Slow WIFI Speed](#slow-wifi-speed)
    * [2.3.1 Best Solution](#best-solution)
    * [2.3.2 Feasible Solution](#feasible-solution)
* [3 To Do](#to-do)

# A journey to understand VPN

This is a repo which is my journey to understand VPNs in my free time. This repo will be updated until I grow bore of it and archive it. Thanks for visiting!

# Information about Institute Internet

## Packet Filtering and Services

- `UDP` packets are dropped - `dig`, `nslookup`, etc. don't work
- `ICMP` packets are dropped - `ping`, `traceroute`, etc. don't work
- Custom DNS Servers are not allowed as DNS servers commonly listen on `port 53` which is blocked. There is packet filtering too as the network prohibits the use of ceritifcates for the connection and uses `PEAP + MSChapv2` which is very much vulnerable.  Credentials can be cracked easily. Lookup `chapcrack`.
- Cannot `ssh` external network like `ec2`, `aws` and `digital ocean`.

## Working VPNs

- Not all `UDP` based VPNs working ( reason [maybe] : UDP packets directly dropped )
- Nord VPN, WARP or 1.1.1.1 by Cloudflare , VPNHub by Pornhub :  **Do not work** 
- `TCP` based VPNs work but are really slow of course due to the facilities provided by TCP

### A Ray of Hope : ExpressVPN works

Express VPN works - it uses `Lightway Protocol` whose core is open sourced now [here](https://github.com/expressvpn/lightway-core) - and a combination of `iptable` rules and `DNS Resolution`.


My speculation is that it runs in TCP Mode and its fast. But I need to verify this by looking at logs and iptable entries. I speculate that `Lightway UDP` doesn't work because I tried it specifically on the Android version of the app, it didn't connect at all where the TCP counterpart connected quickly.


> So the ray of hope is that using the lightway core and iptables we may be able to manage creating out our version of VPN that can be hosted on any server obtained by Student credits.


## Slow WIFI Speed

The institute has a fast Ethernet connection but a notoriously slow Wifi due to its usage of `2.4 ghz` and `20MHz` bandwidth with a Bit-rate of `72.2Mb/s` (Megabits/s). This wifi is shared with many people in the same wing which brings its speed down to 10-12 Mbps.



```bash
$ iwconfig wlo1
wlo1      IEEE 802.11  ESSID:"STUDENT_SECURED"
          Mode:Managed  Frequency:2.412 GHz  Access Point: E8:BA:70:61:38:E2
          Bit Rate=72.2 Mb/s   Tx-Power=20 dBm
          Retry short limit:7   RTS thr:off   Fragment thr:off
          Power Management:on
          Link Quality=50/70  Signal level=-60 dBm
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid frag:0
          Tx excessive retries:2004  Invalid misc:5420   Missed beacon:0
```


### Best Solution

**Just buy a router**


Buy a good 300Mbps or (1 Gbps if u are rich) aand then use ethernet interface to distribute internet wia the wifi interface.<br/>
Setting up can be a bit tedious for beginners but it is relatively easier and much better than the next solution.

> Benefits : You can get 300Mbps internet, and even if u share with 3 room mates u still get arorund 100 Mbps in the worst case scenario which is much better than getting 12-13 Mbps on Wifi

### Feasible Solution

This solution can be used if u have raspberry pi with you and don't want to buy a router.<br/>
- The logic is same, route the connections on Wifi interface via the ethernet interface.<br/>
- Buy a 150 Mbps usb adapter

> For detailed config : Check out my post [here](./rpi-express.md).<br/>
Benefits : As in the previous solution you can get much better speed than the institute wifi and can enjoy online streaming. Cheers!

# To Do

- [ ] Research on ExpressVPN protocol being used across devices
- [ ] ExpressVPN iptables
- [ ] ExpressVPN DNS Bypassing methodology
