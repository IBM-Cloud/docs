---



copyright:

  years: 2015，2017

lastupdated: "2016-06-20"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Plug-in {{site.data.keyword.vpn_short}} per la CLI {{site.data.keyword.Bluemix_notm}}

*Versione:* 1.4.0

Puoi utilizzare la CLI (command line interface) per configurare e gestire il tuo servizio {{site.data.keyword.vpn_full}}. Il plug-in della CLI {{site.data.keyword.vpn_short}} è disponibile in due versioni: una per l'utilizzo del plug-in con la CLI Cloud Foundry e l'altra per l'utilizzo del plug-in con la CLI {{site.data.keyword.Bluemix}}. Entrambe le versioni del plug-in forniscono la stessa funzionalità.
{:shortdesc}

Il plug-in {{site.data.keyword.vpn_short}} è disponibile per i sistemi operativi Windows, MAC e Linux. Assicurati di utilizzare il plug-in adatto a te.

Le seguenti istruzioni servono a gestire il plug-in della CLI {{site.data.keyword.Bluemix_notm}}. Per utilizzare il plug-in con il plug-in della CLI Cloud Foundry (cf), consulta [{{site.data.keyword.vpn_short}} CLI plug-in for cf CLI](../vpn/index.html).


Le informazioni qui di seguito elencano tutti i comandi supportati dalla CLI {{site.data.keyword.vpn_short}} per la CLI Bluemix CLI e includono i relativi nomi, opzioni, utilizzo, prerequisiti, descrizioni ed esempi. Consulta [Extend your Bluemix command line interface](../../index.html#cli_bluemix_ext) su come installare il plug-in vpn.

**Nota:** i *Prerequisiti* elencano quali azioni sono richieste prima di utilizzare il comando. I prerequisiti possono includere una o più delle seguenti azioni:
<dl>
<dt>**Endpoint**</dt>
<dd>Un endpoint API deve essere impostato mediante `bluemix api` prima di utilizzare il comando.</dd>
<dt>**Accesso**</dt>
<dd>L'accesso utilizzando il comando `bluemix login` è richiesto prima di utilizzare questo comando.</dd>
<dt>**Destinazione**</dt>
<dd>Il comando `bluemix target` deve essere utilizzato per impostare un'organizzazione e uno spazio prima di utilizzare questo comando.</dd>
</dl>


## bluemix vpn connection-create
Crea una connessione VPN.

```
bluemix vpn connection-create CONNECTION_NAME -g GATEWAY_NAME -k PRESHARED_KEY -subnets "SUBNET/MASK" -cip CUSTOMER_GATEWAY_IP_ADDRESS [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_CONNESSIONE*  (obbligatorio):  il nome della connessione.

-g *NOME_GATEWAY*  (obbligatorio):  il nome del gateway.

-k *CHIAVE_PRECONDIVISA*  (obbligatorio): la chiave precondivisa.

-subnets "*SOTTORETE*/*MASCHERA*"  (obbligatorio):  l'indirizzo di sottorete remota in formato CIDR.

-cip *INDIRIZZO_IP_GATEWAY_CLIENTE*  (obbligatorio):  l'indirizzo IP dell'endpoint remoto del tunnel VPN.

-d *DESCRIZIONE*  (facoltativo): la descrizione dei parametri specificati.

-peer_id *ID_PEER*  (facoltativo): l'ID del peer remoto. Altro endpoint del tunnel VPN.

-admin_state *STATO_AMMINISTRAZIONE*  (facoltativo): lo stato della connessione VPN. I valori validi sono `UP` o `DOWN`.

-dpd-action *AZIONE*  (facoltativo): l'azione da eseguire quando viene rilevato che il peer è inattivo. I valori validi sono `hold`, `clear`, `disabled`, `restart` o `restart-by-peer`. Il valore predefinito è `hold`.

-gateway_ip *INDIRIZZO_IP*  (facoltativo): l'indirizzo IP dell'endpoint del tunnel VPN locale.

-i *STATO_INIZIATORE*  (facoltativo):  lo stato dell'iniziatore. Il valore predefinito è `bi-directional`.

-dpd-timeout *VALORE*  (facoltativo): il valore di timeout, espresso in secondi, dopo il quale la sessione viene terminata. Intervallo: 6 - 86400 secondi. Il valore predefinito è `120` secondi.

-dpd-interval *VALORE*  (facoltativo): l'intervallo keepalive, in secondi. Invia dei messaggi keepalive all'intervallo configurato per verificare lo stato di attività del peer. Intervallo: 5-86399 secondi. Il valore predefinito è `15` secondi.

-ike *NOME*  (facoltativo): il nome della politica IKE.

-ipsec *NOME*  (facoltativo): il nome della politica IPSec.

**Esempi**:

Crea una nuova connessione vpn con il nome `my_connection`:
```
bluemix vpn connection-create my_connection -g my_gateway -k 123456 -subnets "192.168.10.0/24" -cip 162.135.1.1
```


## bluemix vpn ike-create
Crea una politica IKE.

```
bluemix vpn ike-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_POLITICA*  (obbligatorio): il nome della politica IKE.

-g *NOME_GATEWAY*  (obbligatorio):  il nome del gateway.

-d *DESCRIZIONE*  (facoltativo): la descrizione dei parametri specificati.

-pfs *GRUPPO*  (facoltativo): l'identificativo del gruppo DH (Diffie-Hellman). I valori validi sono `Group2`, `Group5` o `Group14`. Il valore predefinito è `Group2`.

-e *ALGORITMO_DI_CRITTOGRAFIA*  (facoltativo): l'algoritmo di crittografia. I valori validi sono `aes-128`, `aes-192`, `aes-256` o `3des`. Il valore predefinito è `aes-128`.

-lv *VALORE_DURATA*  (facoltativo): il valore di durata dell'associazione di sicurezza IKE. Intervallo: 60 - 86400 secondi. Il valore predefinito è `86400` secondi.

**Esempi**:

Crea una nuova politica IKE con il nome `my_ike`:
```
bluemix vpn ike-create my_ike -g my_gateway
```


## bluemix vpn ipsec-create
Crea una politica IPSec.

```
bluemix vpn ipsec-create POLICY_NAME -g GATEWAY_NAME [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_POLITICA*  (obbligatorio): il nome della politica IPSec.

-g *NOME_GATEWAY*  (obbligatorio):  il nome del gateway.

-d *DESCRIZIONE*  (facoltativo): la descrizione dei parametri specificati.

-pfs *GRUPPO*  (facoltativo): l'identificativo del gruppo DH (Diffie-Hellman). I valori validi sono `Group2`, `Group5` o `Group14`. Il valore predefinito è `Group2`.

-e *ALGORITMO_DI_CRITTOGRAFIA*  (facoltativo): l'algoritmo di crittografia. I valori validi sono `aes-128`, `aes-192`, `aes-256` o `3des`. Il valore predefinito è `aes-128`.

-lv *VALORE_DURATA*  (facoltativo): il valore di durata dell'associazione di sicurezza. Intervallo: 60 - 86400 secondi. Il valore predefinito è `3600` secondi.

**Esempi**:

Crea una politica IPSec con il nome `my_policy`:
```
bluemix vpn ipsec-create my_policy -g my_gateway
```


## bluemix vpn gateway-create
Crea un gateway VPN.

```
bluemix vpn gateway-create GATEWAY_NAME -t TYPE [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_GATEWAY* (obbligatorio): il nome del gateway.

-t *TIPO*  (obbligatorio): contenitori per i quali vuoi abilitare il servizio. I valori validi sono `allSingleContainers`, `allContainerGroups` o `allContainers`. Nessun valore predefinito; devi specificare un tipo.

-gateway_ip *INDIRIZZO_IP*  (facoltativo); l'indirizzo IP del gateway.

-subnets *INDIRIZZO_SOTTORETE*  (facoltativo): l'indirizzo di sottorete in formato CIDR.

**Esempi**:

Crea un gateway con il nome `my_gateway` e il tipo `allContainerGroups`:
```
bluemix vpn gateway-create my_gateway -t allContainerGroups
```


## bluemix vpn connections
Visualizza le informazioni su tutte le connessioni correnti.

```
bluemix vpn connections
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione


## bluemix vpn ikes
Visualizza le informazioni sulle connessioni IKE correnti.

```
bluemix vpn ikes
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione


## bluemix vpn ipsecs
Visualizza le informazioni sulle connessioni IPSec correnti.

```
bluemix vpn ipsecs
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione


## bluemix vpn gateways
Visualizza le informazioni sui gateway correnti.

```
bluemix vpn gateways
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione


## bluemix vpn connection
Visualizza tutte le informazioni su una specifica connessione.

```
bluemix vpn connection NOME_CONNESSIONE
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_CONNESSIONE*  (obbligatorio): il nome della connessione da visualizzare.


## bluemix vpn ike
Visualizza le informazioni su una connessione IKE.

```
bluemix vpn ike NOME_POLITICA
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_POLITICA* (obbligatorio): il nome della politica IKE da visualizzare.


## bluemix vpn ipsec
Visualizza le informazioni su una connessione IPSec.

```
bluemix vpn ipsec NOME_POLITICA
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_POLITICA* (obbligatorio): il nome della politica IPSec da visualizzare.


## bluemix vpn gateway
Visualizza le informazioni di connessione relative a un gateway.

```
bluemix vpn gateway NOME_GATEWAY
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_GATEWAY*  (obbligatorio): il nome del gateway da visualizzare.


## bluemix vpn connection-delete
Elimina una connessione esistente.

```
bluemix vpn connection-delete NOME_CONNESSIONE
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_CONNESSIONE*  (obbligatorio): il nome della connessione da eliminare.


## bluemix vpn ike-delete
Elimina una politica IKE esistente.

```
bluemix vpn ike-delete NOME_POLITICA
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_POLITICA* (obbligatorio): il nome della politica IKE da eliminare.


## bluemix vpn ipsec-delete
Elimina una politica IPSec esistente.

```
bluemix vpn ipsec-delete NOME_POLITICA
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_POLITICA* (obbligatorio): il nome della politica IPSec da eliminare.


## bluemix vpn gateway-delete
Elimina un gateway esistente.

```
bluemix vpn gateway-delete NOME_GATEWAY
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_GATEWAY*  (obbligatorio): il nome del gateway da eliminare.


## bluemix vpn connection-update
Aggiorna una connessione VPN esistente.

```
bluemix vpn connection-update CONNECTION_NAME [-g GATEWAY_NAME] [-k PRESHARED_KEY] [-subnets "SUBNET/MASK"] [-cip CUSTOMER_GATEWAY_IP_ADDRESS] [-d DESCRIPTION] [-peer_id PEER_ID] [-admin_state ADMIN_STATE] [-dpd-action ACTION] [-gateway_ip IP_ADDRESS] [-i INITIATOR_STATE] [-dpd-timeout VALUE] [-dpd-interval VALUE] [-ike NAME] [-ipsec NAME]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_CONNESSIONE*  (obbligatorio):  il nome della connessione.

-g *NOME_GATEWAY*  (facoltativo):  il nome del gateway.

-k *CHIAVE_PRECONDIVISA*  (facoltativo): la chiave precondivisa.

-subnets "*SOTTORETE*/*MASCHERA*"  (facoltativo):  l'indirizzo di sottorete in formato CIDR.

-cip *INDIRIZZO_IP_GATEWAY_CLIENTE*  (facoltativo):  l'indirizzo IP dell'endpoint remoto del tunnel VPN.

-d *DESCRIZIONE*  (facoltativo): la descrizione dei parametri specificati.

-peer_id *ID_PEER*  (facoltativo): l'ID del peer remoto. Altro endpoint del tunnel VPN.

-admin_state *STATO_AMMINISTRAZIONE*  (facoltativo): lo stato della connessione VPN. I valori validi sono `UP` o `DOWN`.

-dpd-action *AZIONE*  (facoltativo): l'azione da eseguire quando viene rilevato che il peer è inattivo. I valori validi sono `hold`, `clear`, `disabled`, `restart` o `restart-by-peer`.

-gateway_ip *INDIRIZZO_IP*  (facoltativo): l'indirizzo IP dell'endpoint del tunnel VPN locale.

-i *STATO_INIZIATORE*  (facoltativo):  lo stato dell'iniziatore.

-dpd-timeout *VALORE*  (facoltativo): il valore di timeout, espresso in secondi, dopo il quale la sessione viene terminata. Intervallo: 6 - 86400 secondi.

-dpd-interval *VALORE*  (facoltativo): l'intervallo keepalive, in secondi. Invia dei messaggi keepalive all'intervallo configurato per verificare lo stato di attività del peer. Intervallo: 5-86399 secondi.

-ike *NOME*  (facoltativo): il nome della politica IKE.

-ipsec *NOME*  (facoltativo): il nome della politica IPSec.


## bluemix vpn ike-update
Aggiorna una politica IKE.

```
bluemix vpn ike-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_POLITICA*  (obbligatorio): il nome della politica IKE.

-g *NOME_GATEWAY*  (facoltativo):  il nome del gateway.

-d *DESCRIZIONE*  (facoltativo): la descrizione dei parametri specificati.

-pfs *GRUPPO*  (facoltativo): l'identificativo del gruppo DH (Diffie-Hellman). I valori validi sono `Group2`, `Group5` o `Group14`.

-e *ALGORITMO_DI_CRITTOGRAFIA*  (facoltativo): l'algoritmo di crittografia. I valori validi sono `aes-128`, `aes-192`, `aes-256` o `3des`.

-lv *VALORE_DURATA*  (facoltativo): il valore di durata dell'associazione di sicurezza IKE. Intervallo: 60 - 86400 secondi.


## bluemix vpn ipsec-update
Aggiorna una politica IPSec.

```
bluemix vpn ipsec-update POLICY_NAME [-g GATEWAY_NAME] [-d DESCRIPTION] [-pfs GROUP] [-e ENCRYPTION_ALGORITHM] [-lv LIFETIME_VALUE]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_POLITICA*  (obbligatorio): il nome della politica IPSec.

-g *NOME_GATEWAY*  (facoltativo):  il nome del gateway.

-d *DESCRIZIONE*  (facoltativo): la descrizione dei parametri specificati.

-pfs *GRUPPO*  (facoltativo): l'identificativo del gruppo DH (Diffie-Hellman). I valori validi sono `Group2`, `Group5` o `Group14`.

-e *ALGORITMO_DI_CRITTOGRAFIA*  (facoltativo): l'algoritmo di crittografia. I valori validi sono `aes-128`, `aes-192`, `aes-256` o `3des`.

-lv *VALORE_DURATA*  (facoltativo): il valore di durata dell'associazione di sicurezza. Intervallo: 60 - 86400 secondi.


## bluemix vpn gateway-update
Aggiorna un gateway VPN esistente.

```
bluemix vpn gateway-update GATEWAY_NAME [-t TYPE] [-gateway_ip IP_ADDRESS] [-subnets SUBNET_ADDRESS]
```

**Prerequisiti**:  Endpoint, Accesso, Destinazione

**Opzioni del comando**:

*NOME_GATEWAY* (obbligatorio): il nome del gateway.

-t *TIPO*  (facoltativo): contenitori per i quali vuoi abilitare il servizio. I valori validi sono `allSingleContainers`, `allContainerGroups` o `allContainers`.

-gateway_ip *INDIRIZZO_IP*  (facoltativo); l'indirizzo IP del gateway.

-subnets *INDIRIZZO_SOTTORETE*  (facoltativo): l'indirizzo di sottorete in formato CIDR.
