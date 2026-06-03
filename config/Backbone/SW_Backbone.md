# 1. VLANs anlegen
```text
vlan 10
 name SNMP-Server
vlan 20
 name Link-ASA0
vlan 30
 name Link-ASA2
vlan 40
 name Link-ISA1
vlan 50
 name Link-IoT
exit
```
# 2. Virtuelle Switch-Interfaces (Gateways) konfigurieren
```text
interface vlan 10
 ip address 10.31.10.1 255.255.255.252
 no shutdown

interface vlan 20
 ip address 10.31.0.1 255.255.255.252
 no shutdown

interface vlan 30
 ip address 10.31.0.5 255.255.255.252
 no shutdown

interface vlan 40
 ip address 10.31.0.9 255.255.255.252
 no shutdown

interface vlan 50
 ip address 10.31.0.13 255.255.255.252
 no shutdown
exit
```
# 3. Physische Ports den VLANs zuweisen
## SNMP Server an FastEthernet 1/0/5
```text
interface fastEthernet 1/0/5
 switchport mode access
 switchport access vlan 10
 no shutdown
```
## Internet-Firewall ASA0 an GigabitEthernet 1/0/8
```text
interface gigabitEthernet 1/0/8
 switchport mode access
 switchport access vlan 20
 no shutdown
```
## Office-Firewall ASA2 an GigabitEthernet 1/0/6
```text
interface gigabitEthernet 1/0/6
 switchport mode access
 switchport access vlan 30
 no shutdown
```
## Produktions-Firewall ISA1 an GigabitEthernet 1/0/7
```text
interface gigabitEthernet 1/0/7
 switchport mode access
 switchport access vlan 40
 no shutdown
```
## IoT-Switch an GigabitEthernet 1/1/1
```text
interface gigabitEthernet 1/1/1
 switchport mode access
 switchport access vlan 50
 no shutdown
exit

write memory
```

## routing office
```text
ip route 10.31.1.0 255.255.255.0 10.31.0.6
```
## routing produktion
```text
ip route 10.31.2.0 255.255.255.0 10.31.0.10
```
## routing DMZ
```text
ip route 10.31.3.0 255.25.255.0 10.31.0.2
```
