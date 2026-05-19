## Erstellen der SubInterfaces

### Physisches Interface einschalten
```text
Router(config)# interface GigabitEthernet0/0
Router(config-if)# no shutdown
Router(config)# exit
```

### Sub-Interface für VLAN 10 (IT)
```text
Router(config)# interface GigabitEthernet0/1.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 10.31.12.1 255.255.255.0
```

### Sub-Interface für VLAN 20 (Workstation)
```text
Router(config)# interface GigabitEthernet0/1.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 10.31.22.1 255.255.255.0

Router# wr
```

## DHCP

```text
Router(config)#ip dhcp excluded-address 10.31.12.1 10.31.12.9 
Router(config)#ip dhcp excluded-address 10.31.22.1 10.31.22.9

Router(config)#ip dhcp pool VLAN10_POOL
Router(dhcp-config)#network 10.31.12.0 255.255.255.0
Router(dhcp-config)#default-router 10.31.12.1
Router(dhcp-config)#dns-server 0.0.0.0

Router(config)#ip dhcp pool VLAN20_POOL
Router(dhcp-config)#network 10.31.22.0 255.255.255.0
Router(dhcp-config)#default-router 10.31.22.1
Router(dhcp-config)#dns-server 0.0.0.0
Router(dhcp-config)#end

Router#wr
```
