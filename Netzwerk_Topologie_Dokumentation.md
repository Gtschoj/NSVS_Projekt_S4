# Technische Dokumentation: Netzwerk-Topologie

## 1. Projektübersicht (Management Summary)
Diese Netzwerk-Topologie beschreibt ein hochverfügbares, segmentiertes Enterprise-Unternehmensnetzwerk nach dem **Collapsed-Backbone-Design**. Es verbindet die Bereiche **Verwaltung (Office)**, **Produktion (Halle 1 & 2)** sowie eine isolierte **IoT-WLAN-Umgebung** über ein zentrales Transfernetz und sichert alle Übergänge durch dedizierte Firewalls ab.

---

## 2. Netzwerk-Architektur & Segmente
Das Netzwerk ist sternförmig aufgebaut, um eine zentrale Kontrolle und maximale Performance zu gewährleisten:

* **Zentraler Kern (`SW-Backbone`):** Ein modularer Schicht-2/3-Switch, der als zentraler Routing-Knotenpunkt und Transfernetz für alle Gateways dient.
* **Office-Bereich:** Angebunden über den `Router Office`, der das Inter-VLAN-Routing für die lokalen Endgeräte (IT, Workstations) übernimmt.
* **Produktions-Bereich:** Angebunden über den `Router Produktion`, welcher die Fertigungsnetzwerke von Halle 1 und Halle 2 trennt.
* **IoT-WLAN-Infrastruktur:** Über einen `HomeRouter` isolierte Smart-Home-Geräte (Kamera, Ventilator, Windsensor). Die physische Anbindung an den Backbone erfolgt über eine störungssichere **Glasfaser-Strecke** via `IoT Fiber-GW-Switch`.

---

## 3. Sicherheits- und Zonenkonzept
Die Sicherheit wird durch eine strikte Segmentierung mittels dedizierter Firewalls auf Hardware-Ebene realisiert (*Stateful Packet Inspection*):

| Zone / Firewall | Gerätetyp | Schutzfunktion & Beschreibung |
| :--- | :--- | :--- |
| **Internet-Grenze (`ASA0`)** | Cisco ASA 5506-X | Schützt den Backbone vor dem öffentlichen Internet. Erlaubt nur von innen initiierte Verbindungen. |
| **Office-Schutz (`ASA2`)** | Cisco ASA 5506-X | Isoliert sensible Unternehmensdaten (IT, Verwaltung) vor Zugriffen aus anderen internen Netzen. |
| **Produktion-Schutz (`ASA1`)** | Cisco ASA 5506-X  | Ioliert die Produktion und somit die Maschinen von unerlaubten Zugriff |

### Out-of-Band (OOB) Management
Die Administration der Firewalls erfolgt physisch getrennt über die **Management-Schnittstellen (`Ma1/1`)** und dedizierte Admin-PCs. Dies verhindert unbefugten Zugriff über produktive Datenleitungen und sichert den Zugriff bei Netzwerkausfällen.

---

## 4. Zentrale Dienste & Protokolle

* **Zentraler Überwachungs-Server (`SNMP-Server`):** Direkt am `SW-Backbone` angeschlossen. Er dient dem zentralen Monitoring via **SNMP** und sammelt Systemprotokolle (**Syslog**) aller Netzwerkkomponenten.
* **DNS-Server:** Isoliert im externen Internet-Netzwerk platziert (**DMZ-Prinzip**). Dadurch ist er für alle Zonen erreichbar, isoliert jedoch potenzielle Angriffe von außen.
* **Redundante DHCP-Konzepte:**
  * *Office-Bereich:* Nutzt einen dedizierten `Server-PT Web/DHCP`. Der `Router Office` leitet Anforderungen via **IP-Helper-Address** weiter.
  * *Produktions-Bereich:* Der `Router Produktion` verteilt IP-Adressen autark über lokale **DHCP-Pools**, um die Produktion bei Serverausfällen abzusichern.

---

## 5. Physikalische Medien
* **Kupferkabel (Twisted Pair):** Gigabit-Ethernet-Verbindungen für alle internen Endgeräte, Server, Router und Firewalls.
* **Glasfaser (Fiber Optic):** Exklusiv für die Backbone-Kopplung des `IoT Fiber-GW-Switch` zur galvanischen Trennung und Vermeidung elektromagnetischer Störungen aus der Produktion.
