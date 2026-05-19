# IP G1/2 to SW_Backbone
```text
ciscoisa>enable
Password: 
ciscoisa#configure terminal
ciscoisa(config)#interface GigabitEthernet1/2
ciscoisa(config-if)#ip address 10.31.0.10 255.255.255.252
ciscoisa(config-if)#no shutdown
```
# IP G1/1 to Router Produktion
```text
ciscoisa>enable
Password: 
ciscoisa#configure terminal
ciscoisa(config)#interface GigabitEthernet1/1
ciscoisa(config-if)#ip address 10.31.0.37 255.255.255.252
ciscoisa(config-if)#no shutdown
```
