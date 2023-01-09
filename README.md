# ENSLD-prep
Preparing myself with coming certification
This is documentation for ENSLD certification.
Material are learnt through [cbtnugget](https://www.cbtnuggets.com/learn/it-training/playlist/nrn:playlist:certification:5f89f3953fcf100015966aae/2?autostart=1)

---

## Design IPv4 and IPv6

RFC1918 - private IP address
To address exausting public IP address
Require NAT to route the private IP

* class A - 0.0.0.1 -> 126.x.x.x 
  10.x.x.x/8
* 127.x.x.x - Loopback address
* class B - 128.x.x.x -> 191.x.x.x
  172.16.0.0.x/16 - 172.31.255.255/16
* class C - 192.0.x.x -> 223.x.x.x 
  192.168.0.0/24 -> 192.168.255.255/24
* class D - 224.x.x.x -> 239.x.x.x = Multicast
* class E - 240.x.x.x -> 255.255.255.254 = R&D
