# NSVS_Projekt_S4

# Projekt: Netzwerkplanung und -dokumentation

## Aufgabenstellung
Die Firma **YUPP Software Entwicklung GmbH** hat ein rasantes Wachstum hinter sich und siedelt mit dem Hauptsitz auf einen neuen Campus in zwei Gebäude um. Zusätzlich sollen in einer weit entfernten Lagerhalle am Stadtrand verschiedene Internet-of-Things (IoT) Überwachungselemente aufgestellt werden.

Für diesen Zweck soll ein Firmennetzwerk (bzw. Teile daraus als Prototyp) projektiert und eine Dokumentation darüber angefertigt werden. Weiters sollen grundlegende Netzwerkfunktionen sichergestellt und Sicherheitsüberlegungen angestellt werden.

---

## Spezifikationen

### 1. Logisches Netzwerk
* **Adressierung:** Die IP-Adressen sollen in den angegebenen Bereichen verteilt und mittels **Subnetting** unter Verwendung von **VLSM** in unterschiedlich große Netze aufgeteilt werden.
* **IP-Zuweisung:** Alle Arbeitsstationen müssen ihre IP-Adressen **automatisch** beziehen (DHCP).
* **Adressbereich:** Im gesamten Netzwerk werden **private Adressen** verwendet.
* **Implementierung:** Router, Switches und Endgeräte sind für einen funktionstüchtigen Prototypen korrekt zu konfigurieren.

### 2. Switching
* **Struktur:** Die verschiedenen Netzwerke (PCs-LANs und Server-LANs) sind logisch in **VLANs** zu strukturieren.
* **Konfiguration:** Erforderliche Switches, VLANs und Trunks müssen eingerichtet werden.
* **Sicherheit:** Ein besonderes Augenmerk ist auf die **LAN-Security** zu legen.

### 3. WAN-Anbindung
* **Internet:** Die Anbindung erfolgt am Campus. Ein öffentlicher IP-Adressbereich wird vom ISP bereitgestellt (bzw. muss angefordert werden).
* **NAT/PAT:** Für die Internetanbindung ist die Implementierung von NAT/PAT am Border Router erforderlich.
* **Web-Service:** Zu Testzwecken soll ein Web-Service im Internet bereitgestellt werden (Hinweis: Nur offizielle Adressen routen!).

### 4. IoT und IoT-Server
* **Anbindung:** Der Standort Lagerhalle muss an den Campus angebunden werden.
* **Registrierung:** IoT-Elemente (mit privaten IP-Adressen) müssen auf einen zentralen **IoT-Registration-Server** zugreifen können.
* **Zugriffsbeschränkung:** * Der Server kann auf einem beliebigen Host aktiviert werden.
    * **Exklusivrecht:** Nur **PC22** ist berechtigt, auf den IoT-Server zuzugreifen und die Daten der IoT-Elemente einzusehen.
