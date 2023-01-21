# ENSLD-prep
Preparing myself with coming certification
This is documentation for ENSLD certification.
Material are learnt through [cbtnugget](https://www.cbtnuggets.com/it-training/cisco/300-420-ensld)

---

## Designing IPv4 and IPv6

* class A - 0.0.0.1 -> 126.x.x.x 
  10.x.x.x/8
* 127.x.x.x - Loopback address
* class B - 128.x.x.x -> 191.x.x.x
  172.16.0.0.x/16 - 172.31.255.255/16
* class C - 192.0.x.x -> 223.x.x.x 
  192.168.0.0/24 -> 192.168.255.255/24
* class D - 224.x.x.x -> 239.x.x.x = Multicast
* class E - 240.x.x.x -> 255.255.255.254 = R&D

### RFC1918 - private IP address
To address exausting public IP address
Require NAT to route the private IP

### VLSM
Why we do subnetting: 
* security
* scalebility
* stability
considering how big the broadcast domain. How this will affect the CPU of switches

![image](https://user-images.githubusercontent.com/83261924/211432770-3730c401-8c1a-4665-a4c0-8425719b6004.png)


Thing to consider:
* Devices/host

IPV6
2600:1700:a40:502f::437
* /128 bit
* /64 --> similar with /24 of ipv4
* :: = superfluous zeros are removed from the address
* leading 0 are removed
* :: --> can only be used 1 time
* No NAT, No ARP, No Broadcast
* Multi homing - 2 different ISP
* Previx Delegation
* Auto Configuration

Type of IPv6
* 2000::/3 - Global Unicast (ARIN - for reserve IP)
* FC00::/7 - Local Unique Unicast (Private / specific use cases)
* FEC0::/10 - Site-local IP address : deprecated(not used anymore)
* FF00::/8 - multicast
* FE80::/10 - link local = next hop.
 
 To get Neighbor Discovery Protocol (NDP):
* NS (Neighbor Solicitation) <--> NA (Neighbor advertisment)
 To get Global unicast:
* RS (Router Solicitation) <--> RA (Router Advertisement)
 
## IPv6 Assignment
### Stateless - SLAAC
Autoconfiguration. Easy. only get own IP.
1) NDP protocol -> Fe80:: MAC
2) Router discovery -> Global unicast -> 2600:/64 + eui-64
3) eui-64 -> 1/2 MAC + FFFE + 1/2 MAC

```
int e0/0
ipv6 add autoconfig //for link local
ipv6 add 2600:db8:dead:beef::/64 eui-64 //for global unicast
```

### Staful -DHCPv6
Get option. Default gateway, SIP server, else

### Stateless DHCPv6 / DHCPv6 Life
combination of both

## Interior Gateway Protocol
summarization at distribution layer:
* OSPF
* EIGRP

```
int e0/0
ipv6 add 
```
