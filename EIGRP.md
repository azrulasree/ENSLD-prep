# EIGRP
## Basic
* RFC 7868
* Distance Vector Protocol - Know distance + know vector (like road sign)
* hybrid protocol
* Fast Robust Stable
* Reliable Transport Protocol (RTP)
* Feasibility condition
* Open Standard
* Lack???

---
## EIGRP Neighborship
![image](https://user-images.githubusercontent.com/83261924/213881751-7c808108-d319-4ba1-9bd5-7a707219d1ac.png)
### Feasibility condition
How to determine best path forward, acceptable, backup path
* classical mode
``` 
router eigrp 10 //autonomous system#
network 192.168.0.0 0.0.255.255 //match this network with interfaces in router
```
* named mode //more option
``` 
router eigrp ENSLD
address-family IPv4 unicast autonomous-system 10
```
### Query Mechanish
1) RTP --> send hello packet on multicast (224.0.0.10)
2) R1 <-hello-> R2 
3) R1 send unicast update packet (contain sequence number)
4) R2 send ```SEC ACK``` (every sequence number that R1 give)
5) Keep updating until send ```Hello ACK``` (no sequence contained)

### Packet
1) Hello packet (every 5sec -> 60sec, dead interval 15sec -> 180sec)
2) Sync packet
3) ACK

### Metrics
![image](https://user-images.githubusercontent.com/83261924/213892735-c2479c77-2134-446f-8072-4b51cd4f6de3.png)

calculation to the best path:
1) Bandwidth - lowest
2) Delay - sum of all delay
3) Reliability -unused
4) Load - unused
5) MTU - not changes
To calculate K Values

loop free topology
Advertise Distance / Route Distance
Choose lower FD. as Successor Route
