
![image](https://user-images.githubusercontent.com/83261924/222783942-60837192-978a-4727-b9d1-afc3f7353253.png)

![image](https://user-images.githubusercontent.com/83261924/222784631-e9fed661-5ddf-40b2-8455-c4ff75608020.png)

![image](https://user-images.githubusercontent.com/83261924/222855093-565af349-cb5c-4c5b-9ebf-e58d39ba1647.png)


show run bgp 
```
router bgp 65001
neighbor 10.0.071
remote-as 65001
address-family ipv4 unicast
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

