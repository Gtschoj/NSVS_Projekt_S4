## IP G1/1 to Backbone
```text
ciscoasa#configure terminal
ciscoasa(config)#interface GigabitEthernet1/1
ciscoasa(config-if)#nameif inside
ciscoasa(config-if)#securty-level 100
ciscoasa(config-if)#no shutdown
ciscoasa(config-if)#ip address 10.31.0.2 255.255.255.252
```

## IP G1/2 to Router Internet
```text
ciscoasa(config)#interface GigabitEthernet1/2
ciscoasa(config-if)#nameif outside
ciscoasa(config-if)#securty-level 0
ciscoasa(config-if)#ip address 10.31.0.41 255.255.255.252
ciscoasa(config-if)#no shutdown
```

## ACL Allow Ping
```text
ciscoasa(config)#access-list ALLOW_ALL extended permit ip any any
ciscoasa(config)#access-group ALLOW_ALL in interface outside
ciscoasa(config)#access-group ALLOW_ALL in interface inside
```

## Routing to SW_Backbone
```text
ciscoasa(config)#route inside 0.0.0.0 0.0.0.0 10.31.0.1
```

## Routing to DNS Internet
```text
ciscoasa(config)# route outside 10.31.3.0 255.255.255.0 10.31.0.42
```
