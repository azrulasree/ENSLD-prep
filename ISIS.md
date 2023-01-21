# IS-IS
## Basic of IS-IS
* Created for ISO network not IP network.
* have lot in common in OSPF
* Link-state protocol

## Based on level:
Intra-Area (Level 1) ES-IS
Inter-Area (Level 2) IS-IS
Different-Area (Level 3)

Endpoint System (ES) <-Level 0-> Intermediate System (IS) <-Level 1->

## Area
* Dont need Area0 as backbone
* Best practise to have transit fabric (area)

### Transit Area
* Handle all level2 communication
* transit for network.
![image](https://user-images.githubusercontent.com/83261924/213869763-e050c052-ce98-4083-b562-41dfd3620874.png)

```
router isis
is-type level-1 //adjacency form only same level# and area#
is-type level-2 //adjacency from on same level# and different area#
is-type level-1-2 //will have 2 hello packet. will give ATT bit
```
> have is-is DB. seperated from L1 and L2 
similar with totally NSSA of OSPF.
> L1-L2 --> give ATT bit = tell L1 that he is the default route (0.0.0.0/0)

## Configure NET
![image](https://user-images.githubusercontent.com/83261924/213876749-12378069-de9d-4825-a465-32c1edb1294b.png)
### NET - Network Entity Title == Router ID of OSPF
length: 6bit --> 16-bit

49.0001.0000.0000.0001.00 --> 49(AFI).0001(area ID).(0000.0000.0001(MAC)).00(this is me)

49.0002.0000.0000.0002.00 --> 49(AFI).0002(area ID).(0000.0000.0002(MAC)).00(this is me)

Protocol
* Hello packet
* LSP (PDU)
* every isis router will have metric of 10. each hop increment at 90



---

## Configure 
```
R1
router isis
net 49.0001.0000.0000.0001.00 //declare NET
is-type level-1 //Declare which DB will be in this router
metric-style-wide // increase max hop
exit
int g0/1
ip router isis //advertise hello packet L1 at this interface
```
``` 
R2
router isis
net 49.0001.0000.0000.0002.00
is-type level-1
metric-style-wide
exit
int r g0/1-2
ip router isis
```
``` 
R3
router isis
net 49.0001.0000.0000.0003.00
is-type level-2-only //only advertise L2 hello
is-tyoe level-1-2 //advertise L1 L2 hello
metric-style-wide
exit
int r g0/1-2
ip router isis
``` 
```
R4
router isis
net 49.0002.0000.0000.0004.00
is-type level-1-2
exit
int r g0/1-2
ip router isis
``` 
```
R5
router isis
net 49.0002.0000.0000.0005.00
is-type level-1
exit
int r g0/1-2
ip router isis
```
```
R6
router isis
net 49.0002.0000.0000.0006.00
is-type level-1
exit
int g0/2
ip router isis
```
## Tshoot
```
show isis
show isis neighbors
show run | s isis //section
```

##  wireshark
![image](https://user-images.githubusercontent.com/83261924/213877378-55ac1717-e91f-44ac-9423-0734d38e53fd.png)

![image](https://user-images.githubusercontent.com/83261924/213877436-894497ea-be5c-480c-a4a8-b42af7b0bc3f.png)
Neighbor adjacencies take place at Layer 2. Not require IP address.

---

## Security
security policy in 3 layers
* link level (between interface)
* area level (for that area)
* domain level (with different area)
encryption: HMAC-MD5
``` 
R1
int eth g0/0
isis password r1r2 //link-level auth
R2
int eth g/0
isis password r1r2

R4/R5/R6
router isis
area-password area2pw //area-level auth


R4/R5/R6
router isis
domain-password pw49 //domain-level auth
```
---

## Design
### Flat area
![image](https://user-images.githubusercontent.com/83261924/213879462-e7948c44-a422-4a67-b9a3-e634cd54a008.png)
* if All L1 --> scalability issue (all need to be in same area) 
* if All L1-L2 --> good at first(only L1 database created) --> when next area added --> all this area will have L2 database as well --> cpu overheat
* hence -->make all L2. --> when add new area (have L1-L2) --> not get those L1-L2

### 3-tier enterprise campus
![image](https://user-images.githubusercontent.com/83261924/213879769-a83572d3-eefa-4b7a-a78f-86d759801d1d.png)
1) start at core layer (all L2). only know explicit exit
if it become L1-L2 --> cause suboptimal routing
2) at distribution layer (L1-L2)
3) at access layer (L0)

### Hybrid design
For collapse core architecture ( 2-tier design)
![image](https://user-images.githubusercontent.com/83261924/213881471-90609ab5-5289-473e-814d-fe29c19f124c.png)
* simpler design. Harder scalability


