---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# IBM VPN-Befehlszeilenschnittstelle
*Letzte Aktualisierung: 03. Mai 2016*

Mit der Befehlszeilenschnittstelle können Sie den Service IBM® Virtual Private Network (VPN) konfigurieren und verwalten. Die IBM VPN-Befehlszeilenschnittstelle ist ein Plug-in, das zusammen mit dem Plug-in der Cloud Foundry-Befehlszeilenschnittstelle verwendet wird. Das Plug-in steht für die Betriebssysteme Windows, MAC und Linux zur Verfügung. Stellen Sie sicher, dass Sie das für Sie gültige Plug-in auswählen.

Installieren Sie zu Anfang die Cloud Foundry-Befehlszeilenschnittstelle. Details finden Sie in [Cloud Foundry-Befehlszeilenschnittstelle](https://console.{DomainName}/docs/cli/downloads.html). 

##Plug-in der IBM VPN-Befehlszeilenschnittstelle installieren
**Hinweis:** Wenn Sie eine installierte Vorgängerversion des Plug-ins der IBM VPN-Befehlszeilenschnittstelle haben, müssen Sie sie zunächst deinstallieren. Verwenden Sie folgenden Befehl: 

```
cf uninstall-plugin vpn
```  

**Lokal installieren**

1. Laden Sie das IBM VPN-Plug-in für Ihre Plattform von [IBM Bluemix CLI Plug-in Repository](http://plugins.ng.bluemix.net) herunter.
2. Installieren Sie das IBM VPN-Plug-in mit dem folgenden Befehl:
**Hinweis:** Wechseln Sie zur Position des VPN-Plug-ins oder geben Sie den Pfad zur Position des Plug-ins an.  

	**Betriebssystem Microsoft Windows:**

	```
	cf install-plugin vpn_windows64.exe
	```  

	**Betriebssystem Apple MAC:**

	```
	cf install-plugin vpn_mac_os_amd64
	```  

	**Betriebssystem Linux:**

	```
	cf install-plugin vpn_linuxamd64
	```  


**Über das Bluemix-Repository installieren**  

1. Fügen Sie das Bluemix-Repository zu den Repositorys der Cloud Foundry-Befehlszeilenschnittstelle hinzu. Verwenden Sie folgenden Befehl:

	```
	cf add-plugin-repo bluemix http://plugins.ng.bluemix.net
	```  
2. Führen Sie folgenden Befehl aus:  

	```
	cf install-plugin vpn -r bluemix
	```
##Liste der Befehle des Service IBM VPN

### cf vpn-create connection

Erstellt eine VPN-Verbindung.

```
cf vpn-create connection <Verbindungsname> -g <Gateway-Name> -k <vorab bekannter gemeinsamer Schlüssel> -subnets ["<Teilnetz/Maske>"] -cip <IP-Adresse des Kundengateways> -d <Beschreibung> -peer_id <Peer-ID> -admin_state <Administratorstatus> -dpd-action <Aktion> -gateway_ip <IP-Adresse> -i <Initiatorstatus> -dpd-timeout <Wert> -dpd-interval <Wert> -ike <Name> -ipsec <Name>
```
#### Parameter
{: #p1}

**Verbindungsname:**
Name der Verbindung.

**Gateway-Name:**
Name des Gateways.

**-k:**
Vorab bekannter gemeinsamer Schlüssel.

**Teilnetz/Maske:**
Adresse des fernen Teilnetzes im CIDR-Format. 

**IP-Adresse des Kundengateways**
IP-Adresse des fernen Endpunkts des VPN-Tunnels. 

##### Optionale Parameter:
{: #op1}

**-d:** Beschreibung der angegebenen Parameter.

**-peer_id:** ID des fernen Peers. Der andere Endpunkt des VPN-Tunnels.

**-admin_state:** Status der VPN-Verbindung. Werte: UP (aktiv) oder DOWN (inaktiv).

**-dpd-action:** Auszuführende Aktion, wenn erkannt wird, dass der Peer inaktiv ist. Werte: hold; clear; disabled; restart; restart-by-peer. Standardwert: hold

**-gateway_ip:** IP-Adresse des lokalen Endpunkts des VPN-Tunnels. 

**-i:** Status des Initiators. Standardwert: bi-directional.

**-dpd-timeout:** Zeitlimitwert in Sekunden, nach dessen Ablauf die Sitzung beendet wird.  Bereich: 6 bis 86400 Sekunden. Standardwert: 120 Sekunden. Der Zeitlimitwert für das Keepalive muss höher als der Wert für das Keepalive-Intervall sein.

**-dpd-interval:** Keepalive-Intervall in Sekunden. Senden Sie im konfigurierten Intervall Keepalive-Nachrichten, um den Aktivitätszustands des Peers zu überprüfen. Bereich: 5 bis 86399 Sekunden. Standardwert: 15 Sekunden

**-ike:** Name der IKE-Richtlinie.

**-ipsec:** Name der IPSec-Richtlinie.


### cf vpn-create ike

Erstellt eine IKE-Richtlinie.

```
cf vpn-create ike <Richtlinienname> -g <Gateway-Name> -d <Beschreibung> -pfs <Gruppe> -e <Verschlüsselungsalgorithmus> -lv <Wert für Lebensdauer>
```
#### Parameter
{: #p2}

**Richtlinienname:**
Name der IKE-Richtlinie.

**Gateway-Name:**
Name des Gateways. 

##### Optionale Parameter:
{: #op2}

**-d:** Beschreibung der angegebenen Parameter.

**-pfs:** Kennung für DH-Gruppe (DH - Diffie-Hellman). Werte: Gruppe 2; Gruppe 5; Gruppe 14. Standardwert: Gruppe 2 

**-e:** Verschlüsselungsalgorithmus. Werte: aes-128; aes-192; aes-256; 3des. Standardwert: aes-128

**-lv:** Wert für Lebensdauer der IKE-Sicherheitszuordnung. Bereich: 60 bis 86400 Sekunden. Standardwert: 86400 Sekunden


### cf vpn-create ipsec

Erstellt eine IPSec-Richtlinie.

```
cf vpn-create ipsec <Richtlinienname> -g <Gateway-Name> -d <Beschreibung> -pfs <Gruppe> -e <Verschlüsselungsalgorithmus> -lv <Wert für Lebensdauer>
```
#### Parameter
{: #p3}

**Richtlinienname:** Name der IPSec-Richtlinie. 

**Gateway-Name:**
Name des Gateways. 

##### Optionale Parameter:
{: #op3}

**-d:** Beschreibung der angegebenen Parameter.

**-pfs:** Kennung für DH-Gruppe (DH - Diffie-Hellman). Werte: Gruppe 2; Gruppe 5; Gruppe 14. Standardwert: Gruppe 2  

**-e:** Verschlüsselungsalgorithmus. Werte: aes-128; aes-192; aes-256; 3des. Standardwert: aes-128

**-lv:** Wert für Lebensdauer der Sicherheitszuordnung. Bereich: 60 bis 86400 Sekunden. Standardwert: 3600 Sekunden

### cf vpn-create gateway

Erstellt ein VPN-Gateway.

```
cf vpn-create gateway <Gateway-Name> -t <Typ> -gateway_ip <IP-Adresse> -subnets <Teilnetzadresse>
```
#### Parameter
{: #p4}

**Gateway-Name:**
Name des Gateways.

**-t:** Container, für die Sie den Service aktivieren wollen. Werte: allSingleContainers; allContainerGroups; allContainers. Standardwert: Es gibt keinen Standardwert; Sie müssen einen Typ angeben. 

#####Optionale Parameter:
{: #op4}

**-gateway_ip:**
IP-Adresse des Gateways. 

**-subnets:**
Teilnetzadresse im CIDR-Format. 

### cf vpn-show gateways

Zeigt Informationen zu den aktuellen Gateways an.

```
cf vpn-show gateways
```
### cf vpn-show ikes

Zeigt Informationen zu den aktuellen IKE-Verbindungen an.

```
cf vpn-show ikes
```
### cf vpn-show ipsecs

Zeigt Informationen zu den aktuellen IPSec-Verbindungen an.

```
cf vpn-show ipsecs
```
### cf vpn-show connections

Zeigt Informationen zu allen aktuellen Verbindungen an.

```
cf vpn-show connections
```
### cf vpn-show ike

Zeigt Informationen zu einer IKE-Verbindung an.

```
cf vpn-show ike <Richtlinienname>
```
### cf vpn-show ipsec

Zeigt Informationen zu einer IPSec-Verbindung an.

```
cf vpn-show ipsec <Richtlinienname>
```
### cf vpn-show gateway

Zeigt Verbindungsinformationen zu einem Gateway an.

```
cf vpn-show gateway <Gateway-Name>
```
### cf vpn-show connection

Zeigt alle Informationen zu einer bestimmten Verbindung an.

```
cf vpn-show connection <Verbindungsname>
```
### cf vpn-delete

Löscht eine vorhandene Verbindung, Richtlinie oder ein vorhandenes Gateway.

```
cf vpn-delete ike <Richtlinienname>
```

```
cf vpn-delete ipsec <Richtlinienname>
```

```
cf vpn-delete connection <Verbindungsname>
```

```
cf vpn-delete gateway <Gateway-Name>
```


### cf vpn-update connection

Aktualisiert eine vorhandene VPN-Verbindung.

```
cf vpn-update connection <Verbindungsname> -g <Gateway-Name> -cip <IP-Adresse des Kundengateways> -subnets ["<Teilnetz/Maske>"] -k <Vorab bekannter gemeinsamer Schlüssel> -d <Beschreibung> -peer_id <Peer-ID> -admin_state <Administratorstatus> -dpd-action <Aktion> -gateway_ip <IP-Adresse> -i <Initiatorstatus> -dpd-timeout <Wert> -dpd-interval <Wert> -ike <Name> -ipsec <Name>
```
#### Parameter
{: #p5}

**Verbindungsname:**
Name der Verbindung.


##### Optionale Parameter:
{: #op5}

**Gateway-Name:**
Name des Gateways.

**IP-Adresse des Kundengateways**
IP-Adresse des fernen Endpunkts des VPN-Tunnels. 

**Teilnetz/Maske:**
Teilnetzadresse im CIDR-Format. 

**-k:**
Vorab bekannter gemeinsamer Schlüssel.

**-d:** Beschreibung der angegebenen Parameter.

**-peer_id:** ID des fernen Peers. Der andere Endpunkt des VPN-Tunnels.

**-admin_state:** Status der VPN-Verbindung. Werte: UP (aktiv) oder DOWN (inaktiv).

**-dpd-action:** Auszuführende Aktion, wenn erkannt wird, dass der Peer inaktiv ist. Werte: hold; clear; disabled; restart; restart-by-peer. Standardwert: hold

**-gateway_ip:** IP-Adresse des lokalen Endpunkts des VPN-Tunnels. 

**-i:** Status des Initiators. Standardwert: bi-directional.

**-dpd-timeout:** Zeitlimitwert in Sekunden, nach dessen Ablauf die Sitzung beendet wird. Bereich: 6 bis 86400 Sekunden. Standardwert: 120 Sekunden

**-dpd-interval:** Keepalive-Intervall in Sekunden. Senden Sie im konfigurierten Intervall Keepalive-Nachrichten, um den Aktivitätszustands des Peers zu überprüfen. Bereich: 5 bis 86399 Sekunden. Standardwert: 15 Sekunden

**-ike:** Name der IKE-Richtlinie.

**-ipsec:** Name der IPSec-Richtlinie.


### cf vpn-update ike

Aktualisiert eine IKE-Richtlinie.

```
cf vpn-update ike <Richtlinienname> -g <Gateway-Name> -d <Beschreibung> -pfs <Gruppe> -e <Verschlüsselungsalgorithmus> -lv <Wert für Lebensdauer>
```
#### Parameter
{: #p6}

**Richtlinienname:**
Name der IKE-Richtlinie. 

##### Optionale Parameter:
{: #op6}

**Gateway-Name:**
Name des Gateways. 

**-d:** Beschreibung der angegebenen Parameter.

**-pfs:** Kennung für DH-Gruppe (DH - Diffie-Hellman). Werte: Gruppe 2; Gruppe 5; Gruppe 14. Standardwert: Gruppe 2 

**-e:** Verschlüsselungsalgorithmus. Werte: aes-128; aes-192; aes-256; 3des. Standardwert: aes-128

**-lv:** Wert für Lebensdauer der IKE-Sicherheitszuordnung. Bereich: 60 bis 86400 Sekunden. Standardwert: 86400 Sekunden


### cf vpn-update ipsec

Aktualisiert eine IPSec-Richtlinie.

```
cf vpn-update ipsec <Richtlinienname> -g <Gateway-Name> -d <Beschreibung> -pfs <Gruppe> -e <Verschlüsselungsalgorithmus> -lv <Wert für Lebensdauer>
```
#### Parameter
{: #p7}

**Richtlinienname:** Name der IPSec-Richtlinie.


##### Optionale Parameter:
{: #op7}

**Gateway-Name:**
Name des Gateways.

**-d:** Beschreibung der angegebenen Parameter.

**-pfs:** Kennung für DH-Gruppe (DH - Diffie-Hellman). Werte: Gruppe 2; Gruppe 5; Gruppe 14. Standardwert: Gruppe 2 

**-e:** Verschlüsselungsalgorithmus. Werte: aes-128; aes-192; aes-256; 3des. Standardwert: aes-128

**-lv:** Wert für Lebensdauer der Sicherheitszuordnung. Bereich: 60 bis 86400 Sekunden. Standardwert: 3600 Sekunden

### cf vpn-update gateway

Aktualisiert ein vorhandenes VPN-Gateway.

```
cf vpn-update gateway <Gateway-Name> -t <Typ> -gateway_ip <IP-Adresse> -subnets <Teilnetzadresse>
```
#### Parameter
{: #p8}

**Gateway-Name:**
Name des Gateways.

#####Optionale Parameter:
{: #op8}

**-t:** Container, für die Sie den Service aktivieren wollen. Werte: allSingleContainers; allContainerGroups; allContainers. Standardwert: Es gibt keinen Standardwert; Sie müssen einen Typ angeben.

**-gateway_ip:**
IP-Adresse des Gateways. 

**-subnets:**
Teilnetzadresse im CIDR-Format. 

# Zugehörige Links
## Allgemein  
{: #general}  
* [Service IBM VPN](../../../services/vpn/index.html)
* [Cloud Foundry-Befehlszeilenschnittstelle](https://console.{DomainName}/docs/cli/downloads.html){: new_window}
