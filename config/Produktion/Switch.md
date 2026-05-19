## VLan
```text
Switch>enable
Switch#configure terminal
Switch(config)#vlan 10
Switch(config-vlan)#name Halle_1
Switch(config-vlan)#exit
Switch(config)#vlan 20
Switch(config-vlan)#name Halle_2

```

## Ports zuweisen
```text
Switch(config)#interface FastEthernet 1/1
Switch(config-if)#switchport mode access 
Switch(config-if)#switchport access vlan 10
Switch(config-if)#exit

Switch(config)#interface FastEthernet 2/1
Switch(config-if)#switchport mode access 
Switch(config-if)#switchport access vlan 20
Switch(config-if)#exit
```

## Trunk für Router
```text
Switch(config)#interface GigabitEthernet 0/1
Switch(config-if)#switchport mode trunk
```
