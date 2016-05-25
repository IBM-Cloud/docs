---

 

copyright:

  years: 2016

 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Bluemix-CLI-Plug-in für VPN

*Letzte Aktualisierung:* 18. Januar 2016

*Version:* 0.1.5

Mit dem Bluemix-CLI-Plug-in für VPN können Sie Ihren IBM VPN-Service (VPN = Virtual Private Network) konfigurieren und verwalten.
{:shortdesc}

In den folgenden Informationen werden alle Befehle, die von dem Bluemix-CLI-Plug-in für VPN unterstützt werden, mit Namen, Optionen, Syntax, Voraussetzungen, Beschreibungen und Beispielen aufgeführt.

**Hinweis:** Unter *Voraussetzungen* wird aufgelistet, welche Aktionen vor der Verwendung des Befehls ausgeführt werden müssen. Zu den Voraussetzungen könnten eine oder mehrere der folgenden Aktionen gehören:
<dl>
<dt>**Endpunkt**</dt>
<dd>Vor der Verwendung des Befehls muss mittels `bluemix api` ein API-Endpunkt festgelegt werden.</dd>
<dt>**Anmeldung**</dt>
<dd>Vor der Verwendung des Befehls ist die Anmeldung über den Befehl `bluemix login` erforderlich.</dd>
<dt>**Ziel**</dt>
<dd>Vor der Verwendung dieses Befehls muss der Befehl `bluemix target` zum Festlegen einer Organisation oder eines Bereichs verwendet werden.</dd>
</dl>


## bluemix vpn connection-create
Erstellt eine VPN-Verbindung.

```
bluemix vpn connection-create CONNECTION_NAME -g GATEWAY_NAME -k PRESHARED_KEY -subnets "SUBNET/MASK" -cip CUSTOMER_GATEWAY_IP_ADDRESS [-d DESCRIPTION][-peer_id PEER_ID] [-admin_state ADMIN_STATE][-dpd-action ACTION] [-gateway_ip IP_ADDRESS][-i INITIATOR_STATE] [-dpd-timeout VALUE][-dpd-interval VALUE] [-ike NAME][-ipsec NAME]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*CONNECTION_NAME* (erforderlich): Der Name der Verbindung.

-g *GATEWAY_NAME* (erforderlich): Der Name des Gateways.

-k *PRESHARED_KEY* (erforderlich): Der vorab verteilte Schlüssel.

-subnets "*SUBNET*/*MASK*" (erforderlich): Die Adresse des fernen Teilnetzes im CIDR-Format.

-cip *CUSTOMER_GATEWAY_IP_ADDRESS* (erforderlich): Die IP-Adresse des fernen Endpunkts des VPN-Tunnels.

-d *DESCRIPTION* (optional): Die Beschreibung der angegebenen Parameter.

-peer_id *PEER_ID* (optional): Die ID des fernen Peers. Der andere Endpunkt des VPN-Tunnels.

-admin_state *ADMIN_STATE* (optional): Der Status der VPN-Verbindung. Gültige Werte: `UP` oder `DOWN`.

-dpd-action *ACTION* (optional): Die auszuführende Aktion, wenn der Peer als inaktiv erkannt wird. Gültige Werte: `hold`, `clear`, `disabled`, `restart` oder `restart-by-peer`. Standardwert: `hold`.

-gateway_ip *IP_ADDRESS* (optional): Die IP-Adresse des lokalen VPN-Tunnelendpunkts.

-i *INITIATOR_STATE* (optional): Der Status des Initiators. Standardwert: `bi-directional`.

-dpd-timeout *VALUE* (optional): Der Wert für das Zeitlimit in Sekunden, nach dessen Ablauf die Sitzung beendet wird. Bereich: 6 - 86400 Sekunden. Standardwert: `120` Sekunden.

-dpd-interval *VALUE* (optional): Das Keepalive-Intervall in Sekunden. Sendet Keepalive-Nachrichten im konfigurierten Intervall, um den Aktivitätszustand des Peers zu prüfen. Bereich: 5-86399 Sekunden. Standardwert: `15` Sekunden.

-ike *NAME* (optional): Der Name der IKE-Richtlinie.

-ipsec *NAME* (optional): Der Name der IPSec-Richtlinie.

**Beispiele**:

Neue VPN-Verbindung mit dem Namen `my_connection` erstellen:
```
bluemix vpn connection-create my_connection -g my_gateway -k 123456 -subnets "192.168.10.0/24" -cip 162.135.1.1
```


## bluemix vpn ike-create
Erstellt eine IKE-Richtlinie.

```
bluemix vpn ike-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION][-pfs GROUP] [-e ENCRYPTION_ALGORITHM][-lv LIFETIME_VALUE]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*POLICY_NAME* (erforderlich): Der Name der IKE-Richtlinie.

-g *GATEWAY_NAME* (erforderlich): Der Name des Gateways.

-d *DESCRIPTION* (optional): Die Beschreibung der angegebenen Parameter.

-pfs *GROUP* (optional): Die Diffie-Hellman-Gruppen-ID (DH-Gruppen-ID). Gültige Werte: `Group2`, `Group5` oder `Group14`. Standardwert: `Group2`.

-e *ENCRYPTION_ALGORITHM* (optional): Der Verschlüsselungsalgorithmus. Gültige Werte: `aes-128`, `aes-192`, `aes-256` oder `3des`. Standardwert: `aes-128`.

-lv *LIFETIME_VALUE* (optional): Der Lebensdauerwert der IKE-Sicherheitszuordnung. Bereich: 60 - 86400 Sekunden. Standardwert: `86400` Sekunden.

**Beispiele**:

Neue IKE-Richtlinie mit dem Namen `my_ike` erstellen:
```
bluemix vpn ike-create my_ike -g my_gateway
```


## bluemix vpn ipsec-create
Erstellt eine IPSec-Richtlinie.

```
bluemix vpn ipsec-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION][-pfs GROUP] [-e ENCRYPTION_ALGORITHM][-lv LIFETIME_VALUE]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*POLICY_NAME* (erforderlich): Der Name der IPSec-Richtlinie.

-g *GATEWAY_NAME* (erforderlich): Der Name des Gateways.

-d *DESCRIPTION* (optional): Die Beschreibung der angegebenen Parameter.

-pfs *GROUP* (optional): Die Diffie-Hellman-Gruppen-ID (DH-Gruppen-ID). Gültige Werte: `Group2`, `Group5` oder `Group14`. Standardwert: `Group2`.

-e *ENCRYPTION_ALGORITHM* (optional): Der Verschlüsselungsalgorithmus. Gültige Werte: `aes-128`, `aes-192`, `aes-256` oder `3des`. Standardwert: `aes-128`.

-lv *LIFETIME_VALUE* (optional): Der Lebensdauerwert der Sicherheitszuordnung. Bereich: 60 - 86400 Sekunden. Standardwert: `3600` Sekunden.

**Beispiele**:

IPSec-Richtlinie mit dem Namen `my_policy` erstellen:
```
bluemix vpn ipsec-create my_policy -g my_gateway
```


## bluemix vpn gateway-create
Erstellt ein VPN-Gateway.

```
bluemix vpn gateway-create GATEWAY_NAME -t TYPE [-gateway_ip IP_ADDRESS][-subnets SUBNET_ADDRESS]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*GATEWAY_NAME* (erforderlich): Der Name des Gateways.

-t *TYPE* (erforderlich): Die Container, für die der Service aktiviert werden soll. Gültige Werte: `allSingleContainers`, `allContainerGroups` oder `allContainers`. Kein Standardwert; Sie müssen einen Typ angeben.

-gateway_ip *IP_ADDRESS* (optional): Die IP-Adresse des Gateways.

-subnets *SUBNET_ADDRESS* (optional): Die Teilnetzadresse im CIDR-Format.

**Beispiele**:

Gateway mit dem Namen `my_gateway` und dem Typ `allContainerGroups` erstellen:
```
bluemix vpn gateway-create my_gateway -t allContainerGroups
```


## bluemix vpn connections
Zeigt Informationen zu allen aktuellen Verbindungen an.

```
bluemix vpn connections
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel


## bluemix vpn ikes
Zeigt Informationen zu den aktuellen IKE-Verbindungen an.

```
bluemix vpn ikes
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel


## bluemix vpn ipsecs
Zeigt Informationen zu den aktuellen IPSec-Verbindungen an.

```
bluemix vpn ipsecs
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel


## bluemix vpn gateways
Zeigt Informationen zu den aktuellen Gateways an.

```
bluemix vpn gateways
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel


## bluemix vpn connection
Zeigt alle Informationen zu einer bestimmten Verbindung an.

```
bluemix vpn connection CONNECTION_NAME
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*CONNECTION_NAME* (erforderlich): Der Name der anzuzeigenden Verbindung.


## bluemix vpn ike
Zeigt Informationen zu einer IKE-Verbindung an.

```
bluemix vpn ike POLICY_NAME
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*POLICY_NAME* (erforderlich): Der Name der anzuzeigenden IKE-Richtlinie.


## bluemix vpn ipsec
Zeigt Informationen zu einer IPSec-Verbindung an.

```
bluemix vpn ipsec POLICY_NAME
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*POLICY_NAME* (erforderlich): Der Name der anzuzeigenden IPSec-Richtlinie.


## bluemix vpn gateway
Zeigt Verbindungsinformationen zu einem Gateway an.

```
bluemix vpn gateway GATEWAY_NAME
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*GATEWAY_NAME* (erforderlich): Der Name des anzuzeigenden Gateways.


## bluemix vpn connection-delete
Löscht eine vorhandene Verbindung.

```
bluemix vpn connection-delete CONNECTION_NAME
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*CONNECTION_NAME* (erforderlich): Der Name der zu löschenden Verbindung.


## bluemix vpn ike-delete
Löscht eine vorhandene IKE-Richtlinie.

```
bluemix vpn ike-delete POLICY_NAME
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*POLICY_NAME* (erforderlich): Der Name der zu löschenden IKE-Richtlinie.


## bluemix vpn ipsec-delete
Löscht eine vorhandene IPSec-Richtlinie.

```
bluemix vpn ipsec-delete POLICY_NAME
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*POLICY_NAME* (erforderlich): Der Name der zu löschenden IPSec-Richtlinie.


## bluemix vpn gateway-delete
Löscht ein vorhandenes Gateway.

```
bluemix vpn gateway-delete GATEWAY_NAME
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*GATEWAY_NAME* Der Name des zu löschenden Gateways.


## bluemix vpn connection-update
Aktualisiert eine vorhandene VPN-Verbindung.

```
bluemix vpn connection-update CONNECTION_NAME [-g GATEWAY_NAME][-k PRESHARED_KEY] [-subnets "SUBNET/MASK"][-cip CUSTOMER_GATEWAY_IP_ADDRESS] [-d DESCRIPTION][-peer_id PEER_ID] [-admin_state ADMIN_STATE][-dpd-action ACTION] [-gateway_ip IP_ADDRESS][-i INITIATOR_STATE] [-dpd-timeout VALUE][-dpd-interval VALUE] [-ike NAME][-ipsec NAME]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*CONNECTION_NAME* (erforderlich): Der Name der Verbindung.

-g *GATEWAY_NAME* (optional): Der Name des Gateways.

-k *PRESHARED_KEY* (optional): Der vorab verteilte Schlüssel.

-subnets "*SUBNET*/*MASK*" (optional): Die Teilnetzadresse im CIDR-Format.

-cip *CUSTOMER_GATEWAY_IP_ADDRESS* (optional): Die IP-Adresse des fernen Endpunkts des VPN-Tunnels.

-d *DESCRIPTION* (optional): Die Beschreibung der angegebenen Parameter.

-peer_id *PEER_ID* (optional): Die ID des fernen Peers. Der andere Endpunkt des VPN-Tunnels.

-admin_state *ADMIN_STATE* (optional): Der Status der VPN-Verbindung. Gültige Werte: `UP` oder `DOWN`.

-dpd-action *ACTION* (optional): Die auszuführende Aktion, wenn der Peer als inaktiv erkannt wird. Gültige Werte: `hold`, `clear`, `disabled`, `restart` oder `restart-by-peer`.

-gateway_ip *IP_ADDRESS* (optional): Die IP-Adresse des lokalen VPN-Tunnelendpunkts.

-i *INITIATOR_STATE* (optional): Der Status des Initiators.

-dpd-timeout *VALUE* (optional): Der Wert für das Zeitlimit in Sekunden, nach dessen Ablauf die Sitzung beendet wird. Bereich: 6 - 86400 Sekunden.

-dpd-interval *VALUE* (optional): Das Keepalive-Intervall in Sekunden. Sendet Keepalive-Nachrichten im konfigurierten Intervall, um den Aktivitätszustand des Peers zu prüfen. Bereich: 5-86399 Sekunden.

-ike *NAME* (optional): Der Name der IKE-Richtlinie.

-ipsec *NAME* (optional): Der Name der IPSec-Richtlinie.


## bluemix vpn ike-update
Aktualisiert eine IKE-Richtlinie.

```
bluemix vpn ike-update POLICY_NAME [-g GATEWAY_NAME][-d DESCRIPTION] [-pfs GROUP][-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*POLICY_NAME* (erforderlich): Der Name der IKE-Richtlinie.

-g *GATEWAY_NAME* (optional): Der Name des Gateways.

-d *DESCRIPTION* (optional): Die Beschreibung der angegebenen Parameter.

-pfs *GROUP* (optional): Die Diffie-Hellman-Gruppen-ID (DH-Gruppen-ID). Gültige Werte: `Group2`, `Group5` oder `Group14`.

-e *ENCRYPTION_ALGORITHM* (optional): Der Verschlüsselungsalgorithmus. Gültige Werte: `aes-128`, `aes-192`, `aes-256` oder `3des`.

-lv *LIFETIME_VALUE* (optional): Der Lebensdauerwert der IKE-Sicherheitszuordnung. Bereich: 60 - 86400 Sekunden.


## bluemix vpn ipsec-update
Aktualisiert eine IPSec-Richtlinie.

```
bluemix vpn ipsec-update POLICY_NAME [-g GATEWAY_NAME][-d DESCRIPTION] [-pfs GROUP][-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*POLICY_NAME* (erforderlich): Der Name der IPSec-Richtlinie.

-g *GATEWAY_NAME* (optional): Der Name des Gateways.

-d *DESCRIPTION* (optional): Die Beschreibung der angegebenen Parameter.

-pfs *GROUP* (optional): Die Diffie-Hellman-Gruppen-ID (DH-Gruppen-ID). Gültige Werte: `Group2`, `Group5` oder `Group14`.

-e *ENCRYPTION_ALGORITHM* (optional): Der Verschlüsselungsalgorithmus. Gültige Werte: `aes-128`, `aes-192`, `aes-256` oder `3des`.

-lv *LIFETIME_VALUE* (optional): Der Lebensdauerwert der Sicherheitszuordnung. Bereich: 60 - 86400 Sekunden.


## bluemix vpn gateway-update
Aktualisiert ein vorhandenes VPN-Gateway.

```
bluemix vpn gateway-update GATEWAY_NAME [-t TYPE][-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**Voraussetzungen**:  Endpunkt, Anmeldung, Ziel

**Befehlsoptionen**:

*GATEWAY_NAME* (erforderlich): Der Name des Gateways.

-t *TYPE* (optional): Die Container, für die der Service aktiviert werden soll. Gültige Werte: `allSingleContainers`, `allContainerGroups` oder `allContainers`.

-gateway_ip *IP_ADDRESS* (optional): Die IP-Adresse des Gateways.

-subnets *SUBNET_ADDRESS* (optional): Die Teilnetzadresse im CIDR-Format.
