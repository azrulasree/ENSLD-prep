Spine-Leaf Architecture
East-west network traffic. because scaleable to the left or right

Top of Rack (TOR)

End of Row (EOR)

Read here Here(https://community.fs.com/blog/tor-vs-eor-data-center-architecture-design.html)

##
vxlan complex architecture

https://support.huawei.com/enterprise/en/doc/EDOC1100004176/dc23658a/hardware-centralized-vxlan-using-the-gateway-spine-leaf-three-layer-architecture


![download](https://user-images.githubusercontent.com/83261924/220834863-74f69b48-9a78-4cc1-ad73-86ec9fe8f97c.png)


===
Learnt in INE(https://my.ine.com/Networking/courses/e81fd034/applying-data-center-routing-protocols)
Topology
![image](https://user-images.githubusercontent.com/83261924/222427533-d859a77f-a1da-428e-9379-1dc42cac4bba.png)

## Basic command
show feature
show cdp nei 
show interface 1/3 - 4 status
show run int e1/5
default interface e1/7 //make interface back to default config

show ip opsf interface //show status of interface
show ip ospf neighbors //show adjacency
show ip route ospf // show routing for ospf
show ip ospf database // LSA
show ip ospf database router 10.0.0.51 detail //database of neighbor
show ip ospf border-routers // show ABR
show ip ospf database external 10.0.0.72 details


## lab command
### Starting command
conf t
feature ospf // features is turn on
router ospf 1 //ospf enable in global config

### n5k1
int e1/5
no switchport
ip address 10.51.71.51/24
no shut
ip router ospf 1 area 0 //opsf enable in port-level
int lo0
ip add 10.0.0.51/32
ip router ospf 1 area 0

### n7k1
#### enable interface
int e1/3
no switchport
ip add 10.51.71.71/23
no shut
int e1/4
ip add 10.52.71.71/24
no shut
int lo0
ip add10.0.0.71/32

#### enable ospf
feature ospf
router ospf 1
int lo0
router ospf 1 area 0
int e1/3 - 4
router ospf 1 area 0

router ospf 1
log-adjacency-changes
exit
logging monitor 7
terminal monitor //get log messages to local console


### N5K2
int e1/5
no switchport
ip add 10.52.71.52/24
no shut
router ospf 1 area 1
int e1/6
no switchport
ip add 10.52.72.52/24
no shut
router eigrp 1
int lo0
ip add 10.0.0.52
router ospf 1 area 1

feature ospf
router ospf 1 area 1
feature eigrp
router eigrp 1

route-map FERMIT_ALL
exit

#### redistribute
router ospf 1
redistribute eigrp 1 route-map PERMIT_ALL
router eigrp 1
redistribute ospf 1 route-map PERMIT_ALL

### N7K2
int e1/4
no switchp
ip add 10.52.72.72/24
no shut
ip router eigrp 1

int lo0
ip add 10.0.0.72/32
ip router eigrp 1

feature eigrp
router eigrp 1

