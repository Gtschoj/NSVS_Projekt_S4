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
