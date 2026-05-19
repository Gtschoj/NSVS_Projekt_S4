## IP-Adresse
```text
Router#configure terminal
Router(config)#interface GigabitEthernet 0/0
Router(config-if)# ip address 10.31.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# exit
Router# write memory
```

## Löschen-IP-Adresse
Da wir die IP-Adress über den Trunk machen brauchen wir keine voreingestellte IP-Adresse
```text
Router> enable
Router# configure terminal
Router(config)# interface GigabitEthernet0/0
Router(config-if)# no ip address
Router(config-if)# no shutdown
Router(config-if)# exit
```

## Erstellen der SubInterfaces

### Physisches Interface einschalten
```text
Router(config)# interface GigabitEthernet0/0
Router(config-if)# no shutdown
Router(config)# exit
```

### Sub-Interface für VLAN 10 (IT)
```text
Router(config)# interface GigabitEthernet0/0.10
Router(config-subif)# encapsulation dot1Q 10
Router(config-subif)# ip address 10.31.10.1 255.255.255.0
```

### Sub-Interface für VLAN 20 (Workstation)
```text
Router(config)# interface GigabitEthernet0/0.20
Router(config-subif)# encapsulation dot1Q 20
Router(config-subif)# ip address 10.31.20.1 255.255.255.0
```

### Sub-Interface für VLAN 30 (Server)
```text
Router(config)# interface GigabitEthernet0/0.30
Router(config-subif)# encapsulation dot1Q 30
Router(config-subif)# ip address 10.31.30.1 255.255.255.0

Router# write memory
```
## Helper Adresse einrichten
```text
Router(config)# interface GigabitEthernet0/0.10
Router(config-subif)# ip helper-address 10.31.30.100
Router(config-subif)# exit

Router(config)# interface GigabitEthernet0/0.20
Router(config-subif)# ip helper-address 10.31.30.100
Router(config-subif)# exit

Router# write memory
```
