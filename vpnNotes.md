# Findings:

- Insti uses PEAP and MSCHAPv2 where MSCHAPv2 is crackable : chapcrack

# ToDo:

- Check for lightway setup and Wireguard setup
- Check for implemented vpn cracks and run them

# Available VPN Protocols :

- Wireguard and Express VPN are close in speed

- Wireguard and Express Vpn are open sourced..express von core is opensource
 https://github.com/expressvpn/lightway-core

- Security of openvpn in above pdf

- Expressvpn works on RAM, trusted server something : https://www.expressvpn.com/features/trustedserver

- PPTP maybe fastest but it is the unsafest...lightway best then and Wireguard best

- PPTP uses MCHAP v2 and can be cracked, insti wifi too uses MChapv2 I guess

https://www.expressvpn.com/what-is-vpn/protocols

Wireguard has am issue of WebRTC. Read More :

https://www.enablex.io/insights/know-these-risks-before-you-dive-into-webrtc/

- PPTP is inefficient and CANNOT bypass restrictions as it is blocked by ISP
- Look into softether..seems interesting

# Additional Resources

- https://blog.scottlowe.org/2021/02/22/setting-up-wireguard-for-aws-vpc-access/
- https://github.com/expressvpn/lightway-core/issues/2

