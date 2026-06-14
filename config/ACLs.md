1. Büro-Schutz Firewall (ASA2)

    Interfaces laut Dokumentation:

        inside (Richtung Router Office / Büro-Netze)

        outside (Richtung SW-Backbone)

    Sicherheitsstufen (Best Practice): inside = 100, outside = 10

Da das Büro (Stufe 100) standardmäßig alles in Richtung Backbone senden darf, schränken wir mit der ACL OFFICE_IN den ausgehenden Verkehr am inside-Interface ein.
Code-Snippet

# --- ALLGEMEINE DIENSTE ---
# Erlaubt dem gesamten Büro-Netzwerk (10.31.1.0/24) DNS-Anfragen an deinen DNS-Server
access-list OFFICE_IN extended permit udp 10.31.1.0 255.255.255.0 host 10.31.3.2 eq 53

# Erlaubt dem Büro-Netzwerk das Senden von Syslog-Daten an den SNMP/Syslog-Server
access-list OFFICE_IN extended permit udp 10.31.1.0 255.255.255.0 host 10.31.10.2 eq 514

# --- WEB / INTERNET / DMZ ---
# Erlaubt dem Büro HTTP und HTTPS ins Internet / zur DMZ (10.31.3.0/24)
access-list OFFICE_IN extended permit tcp 10.31.1.0 255.255.255.0 any eq 80
access-list OFFICE_IN extended permit tcp 10.31.1.0 255.255.255.0 any eq 443

# --- ZUGRIFF AUF PRODUKTION (ERP-BEISPIEL) ---
# Erlaubt dem Server-Subnetz (z.B. ERP-Server im Büro 10.31.1.16/28) den Zugriff auf die Produktions-Hallen
access-list OFFICE_IN extended permit tcp 10.31.1.16 255.255.255.240 10.31.2.0 255.255.255.128 eq 1433
access-list OFFICE_IN extended permit tcp 10.31.1.16 255.255.255.240 10.31.2.128 255.255.255.128 eq 1433

# --- PING FREISCHALTUNG ---
# Erlaubt Pings vom Büro in alle Netze zu Testzwecken
access-list OFFICE_IN extended permit icmp 10.31.1.0 255.255.255.0 any

# --- REGELN AKTIVIEREN & ICMP INSPECTION ---
access-group OFFICE_IN in interface ininside

policy-map global_policy
 class inspection_default
  inspect icmp

2. Produktion-Schutz Firewall (ASA1)

    Interfaces laut Dokumentation:

        inside (Richtung Router Produktion / Hallen)

        outside (Richtung SW-Backbone)

    Sicherheitsstufen (Best Practice): ininside = 90, inside = 10

Die Produktion soll stark isoliert werden. Sie darf von sich aus keine Verbindungen aufbauen, außer zu den absolut notwendigen Infrastruktur-Diensten (DNS, Syslog) und Pings.
A. Eingehender Datenverkehr von der Produktion zum Backbone (inside)
Code-Snippet

# Erlaubt den Produktionshallen (10.31.2.0/24 komplett) DNS-Anfragen an den DNS-Server
access-list PROD_IN extended permit udp 10.31.2.0 255.255.255.0 host 10.31.3.2 eq 53

# Erlaubt der Produktion das Senden von Überwachungsdaten/Logs an den SNMP-Server
access-list PROD_IN extended permit udp 10.31.2.0 255.255.255.0 host 10.31.10.2 eq 514
access-list PROD_IN extended permit udp 10.31.2.0 255.255.255.0 host 10.31.10.2 eq 161

# Erlaubt der Produktion das Pingen zu Testzwecken (z.B. Gateways oder DNS)
access-list PROD_IN extended permit icmp 10.31.2.0 255.255.255.0 any

# Aktivieren (Alles andere, wie unbefugtes Surfen im Internet, wird geblockt)
access-group PROD_IN in interface ininside

B. Eingehender Datenverkehr vom Backbone zur Produktion (outside)

Da der Verkehr vom Backbone (Stufe 10) in die Produktion (Stufe 90) fließt, blockiert die ASA dies standardmäßig. Wir müssen den ERP-Zugriff und Pings aus dem Büro hier explizit erlauben:
Code-Snippet

# Erlaubt dem Büro-Server-Subnetz den Zugriff auf die Maschinen/Datenbanken in Halle 1 & 2
access-list BACKBONE_TO_PROD extended permit tcp 10.31.1.16 255.255.255.240 10.31.2.0 255.255.255.128 eq 1433
access-list BACKBONE_TO_PROD extended permit tcp 10.31.1.16 255.255.255.240 10.31.2.128 255.255.255.128 eq 1433

# Erlaubt dem Büro-Netzwerk (z.B. IT-Admins) das Pingen der Produktions-Endgeräte
access-list BACKBONE_TO_PROD extended permit icmp 10.31.1.0 255.255.255.0 10.31.2.0 255.255.255.0

# Aktivieren auf dem outside-Interface (Backbone-Seite)
access-group BACKBONE_TO_PROD in interface inside

# ICMP Inspection aktivieren für die Stateful-Rückantworten
policy-map global_policy
 class inspection_default
  inspect icmp

Anpassung für die Internet- & DMZ-Firewall (ASA0)

    Schnittstellen-Setup laut deiner IP-Tabelle:

        interface GigabitEthernet1/2 (Richtung Router DMZ/Internet)

            nameif outside (Sicherheitsstufe 0)

            IP-Adresse: 10.31.0.41 255.255.255.252

        interface GigabitEthernet1/1 (Richtung SW-Backbone)

            nameif inside (Sicherheitsstufe 10)

            IP-Adresse: 10.31.0.2.

Die ACL für das Inside-Interface (inside)

Da der Verkehr vom Backbone (Stufe 10) zum Router/Internet (Stufe 0) fließt, greift hier die ACL für den ausgehenden Verkehr. Wir erlauben hier gezielt den Zugriff auf deinen DNS-Server (10.31.3.2), Web-Traffic und Pings.
Code-Snippet

# 1. Erlaubt dem Büro (10.31.1.0/24) und der Produktion (10.31.2.0/24) DNS-Anfragen an den DNS-Server hinter dem Router
access-list BACKBONE_IN extended permit udp 10.31.1.0 255.255.255.0 host 10.31.3.2 eq 53
access-list BACKBONE_IN extended permit udp 10.31.2.0 255.255.255.0 host 10.31.3.2 eq 53

# 2. Erlaubt dem Büro HTTP und HTTPS ins Internet (bzw. zu den Webservern hinter dem Router)
access-list BACKBONE_IN extended permit tcp 10.31.1.0 255.255.255.0 any eq 80
access-list BACKBONE_IN extended permit tcp 10.31.1.0 255.255.255.0 any eq 443

# 3. PING-FREISCHALTUNG: Erlaubt Büro und Produktion das Pingen des DNS-Servers und des Internet-Routers
access-list BACKBONE_IN extended permit icmp 10.31.1.0 255.255.255.0 host 10.31.3.2
access-list BACKBONE_IN extended permit icmp 10.31.2.0 255.255.255.0 host 10.31.3.2
# Erlaubt das Pingen der Router-Schnittstelle (Transit Internet) zu Testzwecken
access-list BACKBONE_IN extended permit icmp any host 10.31.0.42
# Erlaubt das Pingen des "Internets"
access-list BACKBONE_IN extended permit icmp any any

# --- ACL AKTIVIEREN & INSPECTION ---
# Wir binden die Liste an das INSIDE-Interface (da der Traffic dort hineinfließt)
access-group BACKBONE_IN in interface inside

# ICMP-Inspection global aktivieren, damit Antworten vom Router/Internet automatisch zurückdürfen
policy-map global_policy
 class inspection_default
  inspect icmp
