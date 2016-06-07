---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# CLI IBM VPN
*Ultimo aggiornamento: 3 maggio 2016*

Puoi utilizzare la CLI (command line interface) per configurare e gestire il tuo servizio IBM® VPN (Virtual Private Network). La CLI IBM VPN è un plug-in utilizzato con il plug-in CLI Cloud Foundry. Il plug-in è disponibile per i sistemi operativi Windows, MAC e Linux. Assicurati di utilizzare il plug-in applicabile per te.

Prima di iniziare, installa la CLI Cloud Foundry. Per i dettagli, consulta [Interfaccia riga di comando Cloud Foundry](https://console.{DomainName}/docs/cli/downloads.html). 

##Installa il plug-in CLI IBM VPN
**Nota:** se hai una versione precedente del plug-in CLI IBM VPN installato, devi prima disinstallarlo. Utilizza il comando: 

```
cf uninstall-plugin vpn
```  

**Installa localmente**

1. Scarica il plug-in IBM VPN per la tua piattaforma da [IBM Bluemix CLI Plug-in Repository](http://plugins.ng.bluemix.net).
2. Installa il plug-in IBM VPN utilizzando il seguente comando:
**Nota:** passa nell'ubicazione del plug-in della VPN o specifica il percorso dell'ubicazione del plug-in.  

	**Per SO MS Windows:**

	```
	cf install-plugin vpn_windows64.exe
	```  

	**Per SO Apple MAC:**

	```
	cf install-plugin vpn_mac_os_amd64
	```  

	**Per SO Linux:**

	```
	cf install-plugin vpn_linuxamd64
	```  


**Installa dal repository Bluemix**  

1. Aggiungi il repository Bluemix nei repository della CLI Cloud Foundry. Utilizza il seguente comando:

	```
	cf add-plugin-repo bluemix http://plugins.ng.bluemix.net
	```  
2. Esegui il seguente comando:  

	```
	cf install-plugin vpn -r bluemix
	```
##Elenco dei comandi del servizio IBM VPN

### cf vpn-create connection

Crea una connessione alla VPN.

```
cf vpn-create connection <connection name> -g <gateway name> -k <preshared key> -subnets ["<subnet/mask>"] -cip <customer gateway IP address> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### Parametri
{: #p1}

**connection name:**
Nome della connessione.

**gateway name:**
Nome del gateway.

**-k:**
Chiave precondivisa.

**subnet/mask:**
Indirizzo della sottorete remota nel formato CIDR. 

**customer gateway IP address:**
Indirizzo IP dell'endpoint remoto del tunnel VPN. 

##### Parametri facoltativi:
{: #op1}

**-d:** Descrizione dei parametri specificati.

**-peer_id:** ID del peer remoto. Altro endpoint del tunnel VPN.

**-admin_state:** Stato della connessione VPN. Valori: UP o DOWN.

**-dpd-action:** Azione da intraprendere quando il peer viene individuato come inattivo. Valori: hold; clear; disabled; restart; restart-by-peer. Valore predefinito: hold

**-gateway_ip:** Indirizzo IP dell'endpoint del tunnel VPN locale. 

**-i:** Stato dell'iniziatore. Valore predefinito: bi-directional.

**-dpd-timeout:** Valore di timeout in secondi dopo il quale la sessione viene terminata.  Intervallo: 6 - 86400 secondi. Valore predefinito: 120 secondi. Il valore di timeout keepalive deve essere maggiore del valore dell'intervallo keepalive.

**-dpd-interval:** Intervallo keepalive in secondi. Invia i messaggi keepalive all'intervallo configurato per controllare lo stato di attività del peer. Intervallo: 5-86399 secondi. Valore predefinito: 15 secondi

**-ike:**Nome della politica IKE.

**-ipsec:**Nome della politica IPSec.


### cf vpn-create ike

Crea una politica IKE.

```
cf vpn-create ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### Parametri
{: #p2}

**policy name:**
Nome della politica IKE.

**gateway name:**
Nome del gateway. 

##### Parametri facoltativi:
{: #op2}

**-d:** Descrizione dei parametri specificati.

**-pfs:** Identificativo del gruppo DH (Diffie-Hellman). Valori: Group2; Group5; Group14. Valore predefinito: Group2 

**-e:** Algoritmo di crittografia. Valori: aes-128; aes-192; aes-256; 3des. Valore predefinito: aes-128

**-lv:** Valore di durata dell'associazione di sicurezza IKE. Intervallo: 60 - 86400 secondi. Valore predefinito: 86400 secondi


### cf vpn-create ipsec

Crea una politica IPSec.

```
cf vpn-create ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### Parametri
{: #p3}

**policy name:**
Nome della politica IPSec. 

**gateway name:**
Nome del gateway. 

##### Parametri facoltativi:
{: #op3}

**-d:** Descrizione dei parametri specificati.

**-pfs:** Identificativo del gruppo DH (Diffie-Hellman). Valori: Group2; Group5; Group14. Valore predefinito: Group2  

**-e:** Algoritmo di crittografia. Valori: aes-128; aes-192; aes-256; 3des. Valore predefinito: aes-128

**-lv:** Valore di durata dell'associazione di sicurezza. Intervallo: 60 - 86400 secondi. Valore predefinito: 3600 secondi

### cf vpn-create gateway

Crea un gateway VPN.

```
cf vpn-create gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### Parametri
{: #p4}

**gateway name:**
Nome del gateway.

**-t:** Contenitori per i quali vuoi abilitare il servizio. Valori: allSingleContainers; allContainerGroups; allContainers. Valore predefinito: Nessun valore predefinito; devi specificare un tipo. 

#####Parametri facoltativi:
{: #op4}

**-gateway_ip:**
Indirizzo IP del gateway. 

**-subnets:**
Indirizzo di sottorete in formato CIDR. 

### cf vpn-show gateways

Visualizza le informazioni sui gateway correnti.

```
cf vpn-show gateways
```
### cf vpn-show ikes

Visualizza le informazioni sulle connessioni IKE correnti.

```
cf vpn-show ikes
```
### cf vpn-show ipsecs

Visualizza le informazioni sulle connessioni IPSec correnti.

```
cf vpn-show ipsecs
```
### cf vpn-show connections

Visualizza le informazioni su tutte le connessioni correnti.

```
cf vpn-show connections
```
### cf vpn-show ike

Visualizza le informazioni su una connessione IKE.

```
cf vpn-show ike <policy name>
```
### cf vpn-show ipsec

Visualizza le informazioni su una connessione IPSec.

```
cf vpn-show ipsec <policy name>
```
### cf vpn-show gateway

Visualizza le informazioni di connessione relative a un gateway.

```
cf vpn-show gateway <gateway name>
```
### cf vpn-show connection

Visualizza tutte le informazioni su una specifica connessione.

```
cf vpn-show connection <connection name>
```
### cf vpn-delete

Elimina un gateway, una politica o una connessione esistenti.

```
cf vpn-delete ike <policy name>
```

```
cf vpn-delete ipsec <policy name>
```

```
cf vpn-delete connection <connection name>
```

```
cf vpn-delete gateway <gateway name>
```


### cf vpn-update connection

Aggiorna una connessione VPN esistente.

```
cf vpn-update connection <connection name> -g <gateway name> -cip <customer gateway IP address> -subnets ["<subnet/mask>"] -k <preshared key> -d <description> -peer_id <peer ID> -admin_state <admin state> -dpd-action <action> -gateway_ip <IP address> -i <initiator state> -dpd-timeout <value> -dpd-interval <value> -ike <name> -ipsec <name>
```
#### Parametri
{: #p5}

**connection name:**
Nome della connessione.


##### Parametri facoltativi:
{: #op5}

**gateway name:**
Nome del gateway.

**customer gateway IP address:**
Indirizzo IP dell'endpoint remoto del tunnel VPN. 

**subnet/mask:**
Indirizzo di sottorete in formato CIDR. 

**-k:**
Chiave precondivisa.

**-d:** Descrizione dei parametri specificati.

**-peer_id:** ID del peer remoto. Altro endpoint del tunnel VPN.

**-admin_state:** Stato della connessione VPN. Valori: UP o DOWN.

**-dpd-action:** Azione da intraprendere quando il peer viene individuato come inattivo. Valori: hold; clear; disabled; restart; restart-by-peer. Valore predefinito: hold

**-gateway_ip:** Indirizzo IP dell'endpoint del tunnel VPN locale. 

**-i:** Stato dell'iniziatore. Valore predefinito: bi-directional.

**-dpd-timeout:** Valore di timeout in secondi dopo il quale la sessione viene terminata. Intervallo: 6 - 86400 secondi. Valore predefinito: 120 secondi

**-dpd-interval:** Intervallo keepalive in secondi. Invia i messaggi keepalive all'intervallo configurato per controllare lo stato di attività del peer. Intervallo: 5-86399 secondi. Valore predefinito: 15 secondi

**-ike:**Nome della politica IKE.

**-ipsec:**Nome della politica IPSec.


### cf vpn-update ike

Aggiorna una politica IKE.

```
cf vpn-update ike <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### Parametri
{: #p6}

**policy name:**
Nome della politica IKE. 

##### Parametri facoltativi:
{: #op6}

**gateway name:**
Nome del gateway. 

**-d:** Descrizione dei parametri specificati.

**-pfs:** Identificativo del gruppo DH (Diffie-Hellman). Valori: Group2; Group5; Group14. Valore predefinito: Group2 

**-e:** Algoritmo di crittografia. Valori: aes-128; aes-192; aes-256; 3des. Valore predefinito: aes-128

**-lv:** Valore di durata dell'associazione di sicurezza IKE. Intervallo: 60 - 86400 secondi. Valore predefinito: 86400 secondi


### cf vpn-update ipsec

Aggiorna una politica IPSec.

```
cf vpn-update ipsec <policy name> -g <gateway name> -d <description> -pfs <group> -e <encryption algorithm> -lv <lifetime value>
```
#### Parametri
{: #p7}

**policy name:**
Nome della politica IPSec.


##### Parametri facoltativi:
{: #op7}

**gateway name:**
Nome del gateway.

**-d:** Descrizione dei parametri specificati.

**-pfs:** Identificativo del gruppo DH (Diffie-Hellman). Valori: Group2; Group5; Group14. Valore predefinito: Group2 

**-e:** Algoritmo di crittografia. Valori: aes-128; aes-192; aes-256; 3des. Valore predefinito: aes-128

**-lv:** Valore di durata dell'associazione di sicurezza. Intervallo: 60 - 86400 secondi. Valore predefinito: 3600 secondi

### cf vpn-update gateway

Aggiorna un gateway VPN esistente.

```
cf vpn-update gateway <gateway name> -t <type> -gateway_ip <IP address> -subnets <subnet address>
```
#### Parametri
{: #p8}

**gateway name:**
Nome del gateway.

#####Parametri facoltativi:
{: #op8}

**-t:** Contenitori per i quali vuoi abilitare il servizio. Valori: allSingleContainers; allContainerGroups; allContainers. Valore predefinito: Nessun valore predefinito; devi specificare un tipo.

**-gateway_ip:**
Indirizzo IP del gateway. 

**-subnets:**
Indirizzo di sottorete in formato CIDR. 

# rellinks
## general  
{: #general}  
* [Servizio IBM VPN](../../../services/vpn/index.html)
* [CLI Cloud Foundry](https://console.{DomainName}/docs/cli/downloads.html){: new_window}
