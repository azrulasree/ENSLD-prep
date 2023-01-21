# IS-IS
## Basic of IS-IS
* Created for ISO network not IP network.
* have lot in common in OSPF

## Based on level:
Intra-Area (Level 1) ES-IS
Inter-Area (Level 2) IS-IS
Different-Area (Level 3)

Endpoint System (ES) <-Level 0-> Intermediate System (IS) <-Level 1->

## Area
* Dont need Area0 as backbone
* Best practise to have transit fabric (area)

### Transit Area
*Handle all level2 communication
![image](https://user-images.githubusercontent.com/83261924/213869763-e050c052-ce98-4083-b562-41dfd3620874.png)

```
router isis
is-type level-1 //adjacency form only same level# and area#
is-type level-2 //adjacency from on same level# and different area#
is-type level-1-2 //will have 2 hello packet.
```
> have is-is DB. seperated from L1 and L2 
similar with totally NSSA of OSPF.


## Configure NET
![image](https://user-images.githubusercontent.com/83261924/213876749-12378069-de9d-4825-a465-32c1edb1294b.png)
### NET - Network Entity Title == Router ID of OSPF
length: 6bit --> 16-bit

49.0001.0000.0000.0001.00 --> 49(AFI).0001(area ID).(0000.0000.0001(MAC)).00(this is me)

49.0002.0000.0000.0002.00 --> 49(AFI).0002(area ID).(0000.0000.0002(MAC)).00(this is me)

``` 
router isis
net 49.0002.aabb.cc00.0600.00
```


