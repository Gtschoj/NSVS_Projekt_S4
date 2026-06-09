## VLan
```text
Switch>enable
Switch#configure terminal
Switch(config)#vlan 50
Switch(config-vlan)#name IoT
Switch(config-vlan)#exit

```

## Ports zuweisen
```text
Switch(config)#interface FastEthernet 8/1
Switch(config-if)#switchport mode access 
Switch(config-if)#switchport access vlan 50
Switch(config-if)#exit
```

## Trunk für Router
```text
Switch(config)#interface FastEthernet 9/1
Switch(config-if)#switchport mode trunk 
```