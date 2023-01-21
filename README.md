# ENSLD-prep
Preparing myself with coming certification
This is documentation for ENSLD certification.
Material are learnt through [cbtnugget](https://www.cbtnuggets.com/it-training/cisco/300-420-ensld)

---

## Design IPv4 and IPv6

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
 
 2000::/3 - Global Unicast (ARIN - for reserve IP)
 FC00::/7 - Local Unique Unicast (Private / specific use cases)
 FEC0::/10 - Site-local IP address : deprecated(not used anymore)
 FE80::/10 - link local = next hop.
 NS (Neighbor Solicitation) <--> NA (Neighbor advertisment)
 RS (Router Solicitation) <--> RA (Router Advertisement)
 FF00::/8 - multicast


