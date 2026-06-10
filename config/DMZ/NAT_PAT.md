# Definition des internen Netzwerks via Standard-ACL
Router(config)# access-list 42 permit 10.31.0 0.0.255.255

# Verknüpfung der ACL mit dem externen Interface für PAT (Overload)
Router(config)# ip nat inside source list 42 interface GigabitEthernet0/0 (?) overload

# Zuweisung der NAT-Rollen an den Interfaces
Router(config)# interface GigabitEthernet0/0
Router(config-if)# ip nat inside
Router(config-if)# exit

Router(config)# interface GigabitEthernet0/2
Router(config-if)# ip nat inside
Router(config-if)# exit

Router(config)# interface GigabitEthernet0/1
Router(config-if)# ip nat outside
Router(config-if)# exit