---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# ﻿C# for device developers
{: #c_sharp}

Puoi utilizzare C# per creare e personalizzare i dispositivi che interagiscono con la tua organizzazione su {{site.data.keyword.iot_full}}. Utilizza le informazioni e gli esempi forniti per iniziare a sviluppare i tuoi dispositivi utilizzando C#.
{:shortdesc}

## Scaricare le risorse e il client C#
{: #csharp_client_download}

Per accedere alle risorse e al lcient C# per {{site.data.keyword.iot_short_notm}}, vai al repository [iot-csharp ![Icona link esterno](../../../../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-watson-iot/iot-csharp){: new_window} in GitHub e completa le istruzioni di installazione.


## Constructor
{: #constructor}

Il constructor crea l'istanza client e accetta gli argomenti che contengono le seguenti definizioni:

|Definizione |Descrizione |
|:---|:---|
|`orgId`|Il tuo ID dell'organizzazione.|
|`deviceType`|Il tipo del tuo dispositivo.|
|`deviceId` |L'ID del tuo dispositivo.|
|`auth-method`   |Il metodo di autenticazione da utilizzare. L'unico valore al momento supportato è `token`.|
|`auth-token`   |Un token di autenticazione per la connessione sicura al tuo dispositivo su Watson IoT Platform.|


Se `deviceId` e `deviceType` sono i soli argomenti forniti, il client si collega al servizio Quickstart di {{site.data.keyword.iot_short_notm}} come un dispositivo non registrato. L'elenco degli argomenti definisce come il client si collega al modulo {{site.data.keyword.iot_short_notm}}.


```
namespace com.ibm.iotf.client

public DeviceClient(string orgId, string deviceType, string deviceID, string auth-method, string auth-token)
        : base(orgId, "d" + CLIENT_ID_DELIMITER + orgId + CLIENT_ID_DELIMITER + deviceType + CLIENT_ID_DELIMITER + deviceID, "use-token-auth", auth-token)
    {

    }
```

## Pubblicazione eventi
{: #publishing-events}

I dispositivi utilizzano gli eventi per pubblicare i dati all'istanza {{site.data.keyword.iot_short_notm}}. Il dispositivo controlla il contenuto dell'evento e assegna un nome ad ogni evento che invia.

Quando viene ricevuto un evento dall'istanza {{site.data.keyword.iot_short_notm}}, le credenziali dell'evento in entrata identificano il dispositivo di invio, il che significa che un dispositivo non può impersonare un altro dispositivo.

Gli eventi possono essere pubblicati in uno dei tre [livelli di QoS (quality of service)](../mqtt.html#managed-devices), definiti dal protocollo MQTT. Per impostazione predefinita, gli eventi vengono pubblicati al livello QoS 0.


## Pubblicazione di un evento utilizzando il livello QOS (quality of service) predefinito
{: #publish_event_default_qos}

```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}");
```


## Pubblicazione di un evento utilizzando il livello QOS (quality of service) definito dall'utente
{: #publish_event_user_qos}

Gli eventi pubblicati a un livello QoS MQTT maggiore di `0` includono ulteriori informazioni di conferma di ricezione e possono impiegare più tempo rispetto agli eventi che hanno un livello QoS di `0`.


```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}", 2);
```

## Gestione dei comandi
{: #handling_commands}

Quando un client del dispositivo si connette, effettua automaticamente la sottoscrizione a qualsiasi comando per questo dispositivo. Per elaborare comandi specifici devi registrare un metodo di callback del comando come mostrato nel seguente esempio:

```
public static void processCommand(string cmdName, string cmdFormat, string cmdData) {
...
 }
```

```
deviceClient.connect();
deviceClient.commandCallback += processCommand;
```
La seguente tabella illustra i parametri del metodo commandCallback:

|Parametro|Tipo di dati|Descrizione|
|:---|:---|
|`cmdName`|Stringa|Identifica il comando. |
|`cmdFormat`|Stringa|Il formato può essere qualsiasi stringa, ad esempio JSON.|
|`cmdData`|Dizionario|I dati per il payload. La lunghezza massima è di 131072 byte.|
