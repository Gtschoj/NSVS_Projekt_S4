# NSVS_Projekt_S4

# Aufgabenstellung

Die Firma YUPP Software Entwicklung GmbH. hat ein rasantes Wachstum hinter sich und siedelt mit dem Hauptsitz auf einen neuen Campus in 2 Gebäude. Zusätzlich sollen in einer weit entfernten Lagerhalle am Stadtrand verschiedene Internet-of-Things Überwachungselemente aufgestellt werden.
Für diesen Zweck soll ein Firmennetzwerk (bzw. Teile daraus als Prototyp) projektiert und eine Dokumentation darüber angefertigt werden. Weiters sollen grundlegende Netzwerkfunktionen sichergestellt und Sicherheitsüberlegungen angestellt werden. Jetzt sind sie gefordert!

Das Netzwerk soll folgender groben Spezifikationen genügen: 
    • Logisches Netzwerk:
Um das logische Netzwerk zu implementieren sollen die IP-Adressen in den angegebenen Bereichen verteilt und mittels Subnetting unter Verwendung von VLSM in unterschiedlich große Netze aufgeteilt werden. Alle Arbeits­stationen sollen ihre IP-Adressen automatisch beziehen. Im gesamten Netzwerk werden private Adressen verwendet.
    • Ein korrektes Konfigurieren der Router, Switches und Endgeräte soll dann für einen Firmennetzwerk-Prototypen erfolgen.
    • Switching:
Die verschiedenen Netzwerke der Fa. (d.h. PCs-LANs und Server-LANs) sind logisch in VLANs zu strukturieren. Es sind die erforderlichen Switches, VLANs und Trunks einzurichten und zu konfigurieren. Zusätzlich ist auf LAN-Security zu achten! 
    • WANs:
Es erfolgt am Campus eine Anbindung der Fa. an das Internet. Vom ISP haben sie dazu einen öffentlichen IP‑Adressbereich zugeteilt bekommen, bzw. müssen den benötigten Bereich anfordern.
Für die Anbindung an das Internet ist die Implementierung von NAT/PAT am Border Router erforderlich (zum Testen soll ein zusätzliches Web-Service ins Internet gestellt werden (Achtung: nur offizielle Adressen routen!)).
    • IoT und IoT-Server:
Die IoT-Elemente erhalten natürlich private IP-Adressen. Der Standort Lagerhalle ist an den Campus anzubinden. Überlegen sie sich eine mögliche Implementierung, damit die IoT-Elemente auf den zentralen IoT-Server zugreifen können (um sich dort zu registrieren). Dieser IoT-(Registration)-Server ist auf einem beliebigen Server zu aktivieren. Nur PC22 darf auf den IoT-Server zugreifen und die Daten der IoT-Elemente ansehen.
