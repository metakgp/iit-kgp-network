- Link aggregation :
	- Aggregating LAN ports of the modem to make it Gbps ???

- For bridging EoIP ( ehternet over IP ) can be used, it encapsulates L2 packets with overhead of 42 bytes.

# Tunnels

- Tunnels in the kernel:
	- IPIP
		- Incapsulate only IPv4 unicast. No multicast
		- Less overhead in performance
		- Can setup only 1 tunnel for one endpoint pair
		- Overhead of 20 bytes
		- Contain 2 IP headers
		- Packet acknnowledgement available like TCP
		- Less secure
	- GRE
		- Incapsulate IPv4/IPv6 unicast and multicast.
		- de-facto tunnel used for dynamic routed networks
		- 64K tunnels for a unique tunnel endpoint
		- overhead of 24 bytes
		- No packet acknowledgement, behaves like raw socket/ UDP.
		- More secure but not much secure, uses checksum only.
	- SIT 
		- IPv6 over IPv6 
		- Not much interested in this

IMPORTANT : `Since tunneling involves overhead, MTU size is affected so for that MSS has to be reeduced to prevent IP fragmentation that causes network issues`, its better to use security mechanism like IPSec together with it.

- Userland Kernels:

