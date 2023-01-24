# OSPF

## Basic
* Dijkstra Algorithm - Shortest Path First-> each router need to uniquely identify all posible path
* hello timer:10 dead timer:40
* Non Broadcast Multi-access network: Hello timer:30 Dead timer: 120

## OSPF Adjacencies Formation
![image](https://user-images.githubusercontent.com/83261924/214029117-20709d50-527a-4c08-947d-bd1d4bbb14bf.png)

* point-to-point adjacencies
* broadcast adjacencies



## configuration
```
int lo0
ip add 1.1.1.1 255.255.255.255 //always up.
```
```
router ospf 1 //1 is only locally significant
router-id 1.1.1.1 //uniquely identified by each router. best practise = Use loopback0 -> if not will use highest IP.
network 192.168.23.0 0.0.0.255 area 0 //Hello packet on this network + area# + area type + 
```
OSPF interface-level
```
int e 0/1
ip ospf 1 area 0
```
Remove LSA type-2. 
```
ip ospf network point-to-point //preferred when possible
```

## Election
DR - Designated Router. Will handle flooding(updates to all ospf router)

BDR - Backup Designated Router (ensure DR stay alive)

Router ID are only used if OSPF prio are not being configured.
Default priority is 1. If set to 0, router will not become DR/BDR
Highest Router-ID will become DR

When new highest Router-ID joined network. all router need to ```restart ospf process``` for new DR/BDR election.

Neighbor Multicast - 224.0.0.5

DR Multicast - 224.0.0.6

## OPSF Adjacency State Machine
1) Down state - try to find hello. will receive hello packet back in multicast(224.0.0.5)
2) Init state - start database. unicast
3) 2-way state //finding DR, BDR
* Exchange session: Higher Priority / routerID
4) Exstart state - Database Descriptor(DBD) packet - what route know in own ospf database 
5) Eschange - LSA or route that dont know
6) Loading - load routing database from other router
7) full state - state completed

## LSA
leveraged by service provider
1) Type 1 - Router LSA (Router-ID + direcly connected)
2) Type 2 - Network LSA ( Identify DR/BDR routing)
3) Type 3 - summary LSA (area)
4) Type 4 - Route Redistribution (Autonomous System Boundary Router - ASBR, for different ospf area)
5) Type 5 - Route Redistribution (External Route)
7) Type 7 - External Route ( Not So Stubby Area - NSSA)

## Troubleshoot
```
sh ip ospf int b
sh ip ospf nei
show ip ospf database // check age (LSA / SPF) --> flooding
```
