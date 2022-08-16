# Contributing

Any help is appreciated. Please create a new issue to contribute. For VPN testing tasks, attach/enter the following data (even if the VPN failed ) :

For all systems : 

- Error or warning messages, if any.
- If the VPN failed or worked.
- If the VPN worked, check `DNS Leak` from here (any of the standard or extended test) : [https://www.dnsleaktest.com/](https://www.dnsleaktest.com/results.html) .DNS Leak test is **passed** only if the IP addresses shown in the results are the IP address assigned by the VPN. Enter either *passed* or *failed* for this.

:warning: DNS Leak test is important as the institute does filter DNS requests. Please don't open any blocked website right away before check the DNS Leak Test. First perform the test, then verify the IP location at atleast 2 website service online.

For Linux tests only :

- Name of the DNS resolver used by your system.
- Contents of `/etc/resolv.conf` before and after using the vpn.
- `iptables` rules before and after using the VPN.

ℹ️ VPN Tests on Linux/MacOS is preferred as it will provide much more information than the other OS.

For protocol testing tasks, please attach the following:
- The method of testing
- Screenshots or outputs from various programs if used like, `tcpdump` , `wireshark`, etc.


