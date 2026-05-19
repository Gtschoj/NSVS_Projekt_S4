# IP G1/1 to Backbone
```text
ciscoasa>
ciscoasa>enable
Password: 
ciscoasa#configure terminal
ciscoasa(config)#interface GigabitEthernet1/1
ciscoasa(config-if)#no shutdown
ciscoasa(config-if)#ip address 10.31.10.2 255.255.255.252
```
# IP G1/2 to Router Internet
```text
ciscoasa(config)#interface GigabitEthernet1/2
ciscoasa(config-if)#ip address 10.31.0.41 255.255.255.252
ciscoasa(config-if)#no shutdown
```
