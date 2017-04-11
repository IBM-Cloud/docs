---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Embedded C per gli sviluppatori dei dispositivi
{: #embedded_c}

Puoi utilizzare Embedded C per creare e personalizzare i dispositivi che interagiscono con la tua organizzazione su {{site.data.keyword.iot_full}}. Utilizza le informazioni e gli esempi forniti per iniziare a sviluppare i tuoi dispositivi utilizzando Embedded C.
{:shortdesc}

## Scaricamento delle risorse e del client Embedded C
{: #embeddedc_client_download}

Per accedere agli esempi e alle librerie client Embedded C per {{site.data.keyword.iot_short_notm}}, vai al repository [iotf-embeddedc ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-messaging/iotf-embeddedc){: new_window} in GitHub e completa le istruzioni di installazione.


## Dipendenze
{: #dependencies}

|Dipendenza |Descrizione|
|:---|:---|
|[Eclipse Paho Embedded C library ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](http://git.eclipse.org/c/paho/org.eclipse.paho.mqtt.embedded-c.git){: new_window} |Fornisce un libreria client MQTT C. Per ulteriori informazioni, consulta [MQTT Client Package -  C for embedded devices ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](http://www.eclipse.org/paho/clients/c/embedded/){: new_window}.|


## Installazione
{: #installation}

Per installare la libreria client {{site.data.keyword.iot_short_notm}} per Embedded C, completa le seguenti istruzioni:

1. Per installare l'ultima versione della libreria, immetti il seguente codice nella riga di comando:
```
  [root@localhost ~]# git clone https://github.com/ibm-messaging/iotf-embeddedc.git
```
2. Copia il file .tar della libreria Paho nella directory *lib*.
```
    cd iotf-embeddedc
    cp ~/org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz lib/
```
3. Estrarre il file libreria
```  cd lib
    tar xvzf org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz
```
Il client scaricato ha la seguente struttura file:

```
 |-lib - contains all the dependent files
 |-samples - contains the helloWorld and sampleDevice samples
   |-sampleDevice.c - sample device implementation
   |-helloworld.c - quickstart application
   |-README.md
   |-Makefile
   |-build.sh
 |-iotfclient.c - Main client file
 |-iotfclient.h - Header file for the client
```

## Inizializzazione della libreria client
{: #initialize_client_library}

Dopo aver scaricato il client, deve essere inizializzato e collegato a {{site.data.keyword.iot_short_notm}}. Puoi inizializzare la libreria client {{site.data.keyword.iot_short_notm}} per Embedded C trasmettendo i parametri o utilizzando un file di configurazione.

### Trasmissione dei parametri

La funzione `initialize` utilizza i seguenti parametri per collegarsi al servizio {{site.data.keyword.iot_short_notm}}:

|Definizione |Descrizione |
|:---|:---|
|`client`|Un puntatore a *iotfclient*.|
|`org`|Il tuo ID dell'organizzazione.|
|`type` |Il tipo del tuo dispositivo.|
|`id` |L'ID del dispositivo.|
|`auth-method` |Il metodo di autenticazione da utilizzare. L'unico valore al momento supportato è `token`.|
|`auth-token`|Un token di autenticazione per la connessione sicura al tuo dispositivo su Watson IoT Platform.|


```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	//quickstart
	rc = initialize(&client,"quickstart","iotsample","001122334455",NULL,NULL);
	//registered
	rc = initialize(&client,"org","type","id","auth-method","auth-token");
	....
```

### Utilizzo di un file di configurazione

Puoi anche utilizzare un file di configurazione per inizializzare la libreria client Embedded C. La funzione `initialize_configfile` utilizza il percorso del file di configurazione come un parametro.

```
	#include "iotfclient.h"
	....
	....
	char *filePath = "./device.cfg";
	Iotfclient client;
	rc = initialize_configfile(&client, filePath);
	....
```

Il file di configurazione deve essere nel seguente formato:

```
	org=$orgId
	type=$myDeviceType
	id=$myDeviceId
	auth-method=token
	auth-token=$token
```

## Connessione al servizio
{: #connecting_service}

Dopo aver inizializzato la libreria client Embedded C di {{site.data.keyword.iot_short_notm}}, puoi collegarti a {{site.data.keyword.iot_short_notm}} richiamando la funzione `connectiotf`.

```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	char *configFilePath = "./device.cfg";

	rc = initialize_configfile(&client, configFilePath);

	if(rc != SUCCESS){
		printf("initialize failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}

	rc = connectiotf(&client);

	if(rc != SUCCESS){
		printf("Connection failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}
	....
```

## Gestione dei comandi
{: #handling_commands}

Quando il client del dispositivo si connette, effettua automaticamente la sottoscrizione a qualsiasi comando per questo dispositivo. Per elaborare comandi specifici, devi registrare una funzione di callback del comando richiamando la funzione `setCommandHandler`. La funzione di callback ha le seguenti proprietà:

|Proprietà |Descrizione|
|:---|:---|
|`commandName`  |Il nome del comando che è stato richiamato. |  
|`format`  |Il formato dell'evento. Il formato può essere qualsiasi stringa, ad esempio JSON.|
|`payload`  |I dati per il payload del comando. La lunghezza massima è di 131072 byte. |


```
	#include "iotfclient.h"

	void myCallback (char* commandName, char* format, void* payload)
	{
	printf("The command received :: %s\n", commandName);
	printf("format : %s\n", format);
	printf("Payload is : %s\n", (char *)payload);
	}
	...
	...
	char *filePath = "./device.cfg";
	rc = connectiotfConfig(filePath);
	setCommandHandler(myCallback);

	yield(1000);
	....

```
**Nota:** la funzione `yield()` abilita il dispositivo a ricevere i comandi da Watson IoT Platform e a mantenere la connessione attiva. Se la funzione `yield()` non è richiamata nell'intervallo di tempo specificato nell'intervallo keepAlive, tutti i comandi inviati dalla piattaforma non saranno ricevuti dal dispositivo. Il valore assegnato alla funzione `yield()` specifica la durata (in millisecondi) in cui i dati possono essere letti dal socket prima che il controllo sia restituito all'applicazione.

## Pubblicazione eventi
{: #publishing_events}

Gli eventi possono essere pubblicati con le seguenti proprietà:

|Proprietà |Descrizione|
|:---|:---|
|eventType  |Il tipo di evento che viene pubblicato, ad esempio stato o gps. |  
|eventFormat  |Il formato può essere una stringa, ad esempio `json`. |
|data  |I dati per il payload. La lunghezza massima è di 131072 byte. |
|QoS  |Il livello QOS (quality of service) per l'evento pubblicato. I valori supportati sono `0`, `1`, `2`.|


```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", "{\"d\" : {\"temp\" : 34 }}", QOS0);
	....
```

## Disconnessione del client
{: #disconnect_client}

Per scollegare il client e rilasciare le connessioni, esegui il seguente frammento di codice:

```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", payload , QOS0);
	...
	rc = disconnect();
	....
```

## Esempi
{: #samples}

Il codice dell'applicazione e del dispositivo di esempio sono forniti in [GitHub ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-messaging/iotf-embeddedc/tree/master/samples){: new_window}.
