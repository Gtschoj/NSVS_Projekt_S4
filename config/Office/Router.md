## IP-Adresse
'''
Router#configure terminal
Router(config)#interface GigabitEthernet 0/0
Router(config-if)# ip address 10.31.1.1 255.255.255.0
Router(config-if)# no shutdown
Router(config-if)# exit
Router(config)# exit
Router# write memory
