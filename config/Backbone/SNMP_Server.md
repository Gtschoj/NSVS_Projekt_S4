### SNMP-Abfrage auf dem Server (Kurzanleitung)

1. **Tool öffnen:** Auf dem `PC-PT SNMP-Server` den **MIB Browser** starten.
2. **Verbindung einrichten:** Oben rechts auf **Advanced...** klicken und Folgendes eintragen:
   * **Address:** IP-Adresse des Routers (Schnittstelle Richtung Backbone)
   * **Read Community:** `public`
   * **SNMP Version:** `V2c`
3. **OID (Zielobjekt) auswählen:** Im linken MIB-Baum den Pfad zum Gerätenamen aufklappen:
   * `router_std MIBs` $\rightarrow$ `.iso` $\rightarrow$ `.org` $\rightarrow$ `.dod` $\rightarrow$ `.internet` $\rightarrow$ `.mgmt` $\rightarrow$ `.mib-2` $\rightarrow$ `.system` $\rightarrow$ **`sysName`**
4. **Abfrage starten:** Die Operation auf **Get** stellen und rechts auf **GO** klicken. Das Ergebnis erscheint in der *Result Table*.
5. **Weitere Router abfragen:** Über den Button *Advanced...* lediglich die IP-Adresse auf den nächsten Router abändern und erneut auf *GO* klicken.
