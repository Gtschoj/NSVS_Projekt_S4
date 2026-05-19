## VLan
´´´text
Switch>enable
Switch#configure terminal
Switch(config)#vlan 10
Switch(config-vlan)#name IT-Admin
Switch(config-vlan)#exit
Switch(config)#vlan 20
Switch(config-vlan)#name Office
Switch(config-vlan)#exit
Switch(config)#vlan 30
Switch(config-vlan)#name Server
Switch(config-vlan)#exit
´´´

## Ports zuweisen
´´´text
Switch(config)#interface FastEthernet 0/1
Switch(config-if)#switchport mode access 
Switch(config-if)#switchport access vlan 10
Switch(config-if)#exit

Switch(config)#interface FastEthernet 0/2
Switch(config-if)#switchport mode access 
Switch(config-if)#switchport access vlan 20
Switch(config-if)#exit

Switch(config)#interface FastEthernet 0/3
Switch(config-if)#switchport mode access 
Switch(config-if)#switchport access vlan 30
Switch(config-if)#exit
´´´

## Trunk für Router
´´´text
Switch(config)#interface GigabitEthernet 0/1
Switch(config-if)#switchport mode trunk
´´´
