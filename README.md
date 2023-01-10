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


