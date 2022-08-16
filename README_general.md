# Index

* 1\. [VPNs](#1-vpns)
    * 1.1 [Using OpenVPN](#11-using-openvpn)
* 2\. [LAN](#2-lan)
* 3\. [WIFI](#3-wifi)


# 1. VPNs
 
**Working VPNs**

- [Speedify](https://speedify.com/) (Not free)
- [ExpressVPN](https://www.expressvpn.com/) (Not free)
- [OpenVPN](https://openvpn.net/) hosted on [DigitalOcean](https://www.digitalocean.com/) or [AWS ec2](https://aws.amazon.com/ec2/)
- [SecureVPN](https://play.google.com/store/apps/details?id=com.fast.free.unblock.secure.vpn&hl=en_IN&gl=US) (free user)
- [NoCardVPN](https://play.google.com/store/search?q=no%20cardvpn&c=apps&hl=en_IN&gl=US)
- [Psiphon](https://play.google.com/store/search?q=psiphon&c=apps&hl=en_IN&gl=US)
- [SetupVPN](https://chrome.google.com/webstore/detail/setupvpn-lifetime-free-vp/oofgbpoabipfcfjapgnbbjjaenockbdp)
- [HoxxVPN](https://chrome.google.com/webstore/detail/hoxx-vpn-proxy/nbcojefnccbanplpoffopkoepjmhgdgh)

**TCP** based VPNs that work on port `443` or `80` will only work.

## 1.1 Using OpenVPN

### Step 1: Get an AWS account

> ⚠️ Make sure to setup the server properly at your own risk. I am not liable to any charges you receive for your mistakes. First watch video about Billing here - [Billing and Terminating Instances](https://www.youtube.com/watch?v=Ptij0mq1Mv4).

Watch this video on how to create a free AWS account - [Create new AWS account](https://www.youtube.com/watch?v=gA9pl-A9gDM). Remember this step requires you to have a debit card (Mastercard, American Express or Visa).


### Step 2: Create a free ec2 instance

Watch this video on how to create an ec2 instance- [Creating an AWS EC2 instance](https://www.youtube.com/watch?v=bJUBSqWaPBQ).

> The further 2 steps are derived from a blog, [IIT KGP: Bypassing network restrictions without compromising on internet speed by Anjay Goel](https://anjaygoel.github.io/posts/IIT-KGP-Bypass-Internet-Restrictions/#step-3-setting-up-openvpn-access-server) 

### Step 3: Setting Up OpenVPN Access Server:

You will need mobile hotspot for this setup.
To setup OpenVPN Access Server, watch this video - [Steps to create OpenVPN Server on AWS](https://www.youtube.com/watch?v=7vxWiIRWwF4).

### Step 4: Bill Management

This is a very important setup, to avoid any extra charges from your debit card. Watch this video - [Billing and Terminating Instances](https://www.youtube.com/watch?v=Ptij0mq1Mv4). <br/>
Remember to use only one instance. <br/>
Remember that bandwidth is _**free upto 100GB per month**_, so its better not to waste resource on the vpn. Use it for daily usages like whatsapp, discord, etc. Prevent torrenting, etc. which can eat up resources.<br/>
Remember to check your usage weekly/biweekly as shown in the video.<br/><br/>
If in any case you have to stop an instance forcibly, do it to be on the safe side.

# 2. LAN 

### 2.1 LAN Cable : 

Make sure your cable is CAT 5e and better (6, 6e, etc.) that you can get easily in TechM. 

### 2.2 Ethernet Adapter properties :

Check if your system supports 1 Gbps connection. Check online tutorials for your operating system for that.


# 3. WIFI 

To use Wifi on your devices :
- Select Authentication type : `MSCHAPv2`
- CA Certificate : `Do not validate`
- Identity : `Your Roll number`
- Password : `Password set in ERP`
- Anonymous Identity : Keep Blank

:warning: On some latest version of Android 11, the interface does not have option to disable Certificate Validation. Please use your laptop as Wifi-Hostpot.

**Setting up router at your room :**

Buy a good 300Mbps or (1 Gbps if u are rich) and then use ethernet interface to distribute internet wia the wifi interface.<br><br>
- Reset the router if its not new
- Go to setup after connecting to the internet
- When asked for Connection type, select any of the following available : `bridge`, `ethernet bridge`.
- Then setup your wifi properties
- If asked for DNS settings, select `automatic`, otherwise use the DNS address as : `127.0.0.53`

# 4. Credits

A great vote of thanks to the following contributors :
- Ishan Manchanda ([@IshanManchanda](https://github.com/IshanManchanda)) - Contribution to the list of working VPNs.
- Soham Sen ([@FadedCoder](https://github.com/FadedCoder)) - Testing UDP and TCP on external network on private ports via `netcat`.
- Rajiv Harlalka ([@rajivharlalka](https://github.com/rajivharlalka)) and Chirag Ghosh ([@chirag828049](https://github.com/chirag828049)) - Helping me with OpenVPN Setup.
- Anjay Goel ([@AnjayGoel](https://github.com/AnjayGoel)) for his intuitive blog on setting up OpenVPN Server.
- Arpit Bhardwaj ([@proffapt](https://github.com/proffapt)) for helping to organize the repository and make it more accessible.

***
<h3 align="center">Thank You for reading and contributing! ❤️❤️❤️ </h3>

