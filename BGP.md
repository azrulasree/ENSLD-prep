
![image](https://user-images.githubusercontent.com/83261924/222783942-60837192-978a-4727-b9d1-afc3f7353253.png)

![image](https://user-images.githubusercontent.com/83261924/222784631-e9fed661-5ddf-40b2-8455-c4ff75608020.png)

![image](https://user-images.githubusercontent.com/83261924/222855093-565af349-cb5c-4c5b-9ebf-e58d39ba1647.png)

##ibgp ebgp
![image](https://user-images.githubusercontent.com/83261924/222871678-8d9551b6-d642-4cf0-8aa0-17c27fa5b120.png)

![image](https://user-images.githubusercontent.com/83261924/222871855-eee96107-fba2-4d9c-b4bb-056349b984d8.png)

![image](https://user-images.githubusercontent.com/83261924/222871889-15bef053-8e54-4cbf-aedb-b6655700abc7.png)

![image](https://user-images.githubusercontent.com/83261924/222871902-9c8f235f-0298-44e7-877d-e53c458e33c3.png)

![image](https://user-images.githubusercontent.com/83261924/222871952-ad7aa656-daf7-4311-87ec-7bc1296c3958.png)

![image](https://user-images.githubusercontent.com/83261924/222871983-d2f52cf5-4b68-4de3-84af-353f1f83ce50.png)

===
## confg
```
show run bgp
show ip bgp summary
```
show ip bgp neighbors 10.0.0.71 advertised-routes //see what route advertised from 10.0.0.71
![image](https://user-images.githubusercontent.com/83261924/222861698-991b13e6-9da2-4851-a758-02ec7c03827c.png)

### SPINE
```
router bgp 65001
neighbor 10.0.0.51
remote-as 65001
update-source lo0
address-family ipv4 unicast //by default is not enable
route-reflector-client

```
### LEAF
```
router bgp 65001
neighbor 10.0.0.71
remote-as 65001
address-family ipv4 unicast
network 51.51.51.51/32
update-source lo0
```

```
logging monitor 7
term mon

feature bgp
router bgp 65001
remote-as 65001
log-neighbor-changes
```

### EBGP
```
int e1/15
no switchport
no shut
int e1/15.51
encapsulation dot1Q 51
ip add 10.0.51.51/24
no shut
```
####  to advertise external hop towards all nexus
##### option 1
N5K1
```
int e1/15.51
ip router ospf 1 area 0
ip ospf passive-interface //just to make this ip part of ospf network. not share it own known network
```
##### option 2
```
router bgp 65001
neighbor 10.0.0.71
address-family ipv4 unicast
next-hop-self
neighbor 10.0.0.72
address-family ipv4 unicast
next-hop-self
```
