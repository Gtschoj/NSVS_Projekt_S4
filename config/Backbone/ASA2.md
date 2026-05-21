## IP G1/1 to SW_Backbone
```text
ciscoasa>enable
ciscoasa#configure terminal
ciscoasa(config)#interface GigabitEthernet1/1
ciscoasa(config-if)#ip address 10.31.0.6 255.255.255.252
ciscoasa(config-if)#no shutdown
```
## IP G1/2 to Router_Office

```text
ciscoasa>enable
ciscoasa#configure terminal
ciscoasa(config)#interface GigabitEthernet1/2
ciscoasa(config-if)#ip address 10.31.0.33 255.255.255.252
ciscoasa(config-if)#no shutdown
```

## Setting Security from SW_Backbone
```text
ciscoasa(config)#interface GigabitEthernet 1/1
ciscoasa(config-if)#nameif inside
INFO: Security level for "inside" set to 100 by default.
ciscoasa(config-if)#no shutdown
ciscoasa(config-if)#exit
```

## Setting Security from Office
```text
ciscoasa(config)#interface GigabitEthernet 1/2
ciscoasa(config-if)#nameif ininside
INFO: Security level for "outside" set to 0 by default.
ciscoasa(config-if)#no shutdown
```

## Routing to SW_Backbone
```text
ciscoasa(config)#route inside 0.0.0.0 0.0.0.0 10.31.0.5
```

## Routing to Office
```text
ciscoasa(config)# route outside 10.31.1.0 255.255.255.0 10.31.0.34
```

## Zum einrichten wird jeder IP Traffic auf der ACL erlaubt
```text
access-list ALLOW_ALL extended permit ip any any
access-group ALLOW_ALL in interface ininside
access-group ALLOW_ALL in interface inside
```
