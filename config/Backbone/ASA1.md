## IP G1/2 to SW_Backbone
```text
ciscoisa>enable
Password: 
ciscoisa#configure terminal
ciscoisa(config)#interface GigabitEthernet1/2
ciscoisa(config-if)#ip address 10.31.0.10 255.255.255.252
ciscoisa(config-if)#no shutdown
```
## IP G1/1 to Router Produktion
```text
ciscoisa>enable
Password: 
ciscoisa#configure terminal
ciscoisa(config)#interface GigabitEthernet1/1
ciscoisa(config-if)#ip address 10.31.0.37 255.255.255.252
ciscoisa(config-if)#no shutdown
```

## nameif to Router Produktion
```text
ciscoisa(config)#interface GigabitEthernet1/1
ciscoisa(config-if)#nameif ininside
ciscoisa(config-if)#security-level 100
ciscoisa(config-if)#no shutdown
```

## nameif to SW_Backbone
```text
ciscoisa(config)#interface GigabitEthernet1/2
ciscoisa(config-if)#nameif inside
ciscoisa(config-if)#security-level 100
ciscoisa(config-if)#no shutdown 
```

## Zum einrichten wird jeder IP Traffic auf der ACL erlaubt
```text
ciscoasa(config)#access-list ALLOW_ALL extended permit ip any any
ciscoasa(config)#access-group ALLOW_ALL in interface ininside
ciscoasa(config)#access-group ALLOW_ALL in interface inside
```

## Routing to SW_Backbone
```text
ciscoasa(config)#route inside 0.0.0.0 0.0.0.0 10.31.0.9
```


## Routing to Produktion
```text
ciscoasa(config)# route outside 10.31.2.0 255.255.255.0 10.31.0.38
```
