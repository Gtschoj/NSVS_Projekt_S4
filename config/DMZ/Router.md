# IP G0/0 to ASA0
```text
Router(config)#interface GigabitEthernet0/0
Router(config-if)#ip address 10.31.0.42 255.255.255.252
Router(config-if)#no shutdown
```

# IP G0/2 to ASA0
```text
Router(config)#interface GigabitEthernet0/0
Router(config-if)#ip address 10.31.3.1 255.255.255.0
Router(config-if)#no shutdown
```

## SNMP
```text
configure terminal
snmp-server community public RO
exit
write memory
```

# Routing
Router(config)#ip route 10.31.0.0 255.255.0.0 10.31.0.41
Router(config)#ip route 10.31.4.0 255.255.255.0 90.90.90.200
Router(config)#ip route 0.0.0.0 0.0.0.0 90.90.90.200