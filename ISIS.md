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



