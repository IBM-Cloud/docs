---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Modello dispositivo
{: #device_model}
Ultimo aggiornamento: 13 settembre 2016 {: .last-updated}

Il modello dispositivo descrive le caratteristiche di gestione e metadati di un dispositivo. Il database del dispositivo in {{site.data.keyword.iot_full}} è l'origine principale delle informazioni sul dispositivo. Le applicazioni e i dispositivi gestiti possono inviare gli aggiornamenti incluse le modifiche dell'ubicazione o il progresso di un aggiornamento del firmware, al database. Non appena sono stati ricevuti questi aggiornamenti da {{site.data.keyword.iot_short_notm}}, il database del dispositivo viene aggiornato e le informazioni sono disponibili alle applicazioni.

**Nota:** con l'eccezione dell'estensione di gestione, il modello dispositivo completo è disponibile per i dispositivi gestiti e non gestiti. Tuttavia, un dispositivo non gestito non può aggiornare direttamente il suo modello di dispositivo nel database.

## Identificativo dispositivo
{: #device_id}

Ogni dispositivo dispone di un attributo `typeId` e `deviceId`. Generalmente, `typeId` rappresenta il modello del tuo dispositivo, mentre `deviceId` può rappresentarne il numero di serie. Nella tua organizzazione
{{site.data.keyword.iot_short_notm}}, la combinazione di `typeId` e `deviceId` deve essere univoca per ogni dispositivo.

In aggiunta, {{site.data.keyword.iot_short_notm}} crea un altro identificativo per ogni periferica, che viene denominato `clientId`. `clientId` si basa sul tuo `organizationId` e anche sui valori del dispositivo `typeId` e `deviceId` e fornisce un modo per identificare univocamente un dispositivo individuale.

I caratteri possono essere utilizzati in questi identificativi e limitati in modo che siano compatibili con i protocolli di comunicazione delle API REST. I seguenti identificativi facoltativi del dispositivo
vengono anche utilizzati nel protocollo di gestione del dispositivo:

- deviceInfo.manufacturer
- deviceInfo.serialNumber
- deviceInfo.model
- deviceInfo.deviceClass
- deviceInfo.description

Per ulteriori informazioni sugli identificativi e sulle descrizioni dei loro identificativi comparativi in altri standard di gestione, consulta [Attributi](#attributes).


## Tipi di dispositivo e identificativi
{: #id_and_device_types}

Ogni dispositivo collegato a {{site.data.keyword.iot_short_notm}} viene associato a un tipo di dispositivo. I tipi di dispositivo sono gruppi di dispositivi che condividono le caratteristiche o i comportamenti.

Un tipo di dispositivo dispone di una serie di attributi. Quando un dispositivo viene aggiunto a {{site.data.keyword.iot_short_notm}}, gli attributi e i loro tipi di dispositivo vengono utilizzati come template sovrascritti dagli attributi specifici del dispositivo. Ad esempio, il tipo di dispositivo può avere un valore per l'attributo `deviceInfo.fwVersion`, che rispecchia la versione del firmware al momento della produzione e questo valore sarà copiato dal tipo di dispositivo nei dispositivi come vengono aggiunti. Quando viene aggiunto un dispositivo, se il valore `deviceInfo.fwVersion` già esiste, non viene sovrascritto dal tipo di dispositivo.

Quando un tipo di dispositivo viene aggiornato, soltanto i nuovi dispositivi registrati ereditano le modifiche dal template del tipo di dispositivo. I dispositivi esistenti di un tipo di dispositivo non sono influenzati e rimango immutati.

## Attributi
{: #attributes}

La seguente tabella mostra l'elenco degli attributi che possono essere applicati ai dispositivi in {{site.data.keyword.iot_short_notm}}. Inoltre, anche gli attributi in corsivo possono essere applicati ai tipi di dispositivo.

- API/AGD: Può essere aggiornato da API/Agent gestione dispositivo

  - R: Sola lettura
  - W: Scrittura e lettura
  - A: Accoda

Attributo                        | Tipo       | Descrizione                                       | API | DMA   
------------- | ------------- | ------------- | ------------- | -------------  
 clientId                         | stringa     | L'ID client utilizzato con le connessioni MQTT          |  R  |     
 *typeId*                         | stringa     | Tipo dispositivo                                       |  R  |     
 deviceId                         | stringa     | ID dispositivo                                         |  R  |     
 classId                          | stringa     | Classe del dispositivo ("Dispositivo" o "Gateway")           |  R  |     
 gatewayTypeId                    | stringa     | L'ID tipo del gateway che sta utilizzando questo dispositivo       |  R  |     
 gatewayId                        | stringa     | L'ID dispositivo del gateway che sta utilizzando questo dispositivo      |  R  |     
 status.alert                     | booleano    | Se il dispositivo ha un avviso                    |  W  |     
 *deviceInfo.serialNumber*        | stringa     | Il numero di serie del dispositivo                   |  W  |  W    
 *deviceInfo.manufacturer*        | stringa     | Il produttore del dispositivo                    |  W  |  W   
 *deviceInfo.model*               | stringa     | Il modello del dispositivo                           |  W  |  W  
 *deviceInfo.deviceClass*         | stringa     | La classe del dispositivo                           |  W  |  W  
 *deviceInfo.description*         | stringa     | Il nome descrittivo del dispositivo                |  W  |  W  
 *deviceInfo.fwVersion*           | stringa     | La versione del firmware che correntemente è noto sia sul dispositivo    |  W  |  W  
 *deviceInfo.hwVersion*           | stringa     | La versione hardware del dispositivo                |  W  |  W  
 *deviceInfo.descriptiveLocation* | stringa     | L'ubicazione descrittiva, come una stanza, il numero di build o una regione geografica      |  W  |  W  
 *metadata*                       | complesso    | Metadati in formato libero                                 |  W  |  W  
 added.auth.id                    | stringa     | ID che ha aggiunto il dispositivo                          |  R  |     
 added.dateTime                   | stringa     | Data-ora ISO8601: La data e l'ora in cui il dispositivo è stato aggiunto |  R  |     
 refs.diag.errorCodes             | stringa     | L'URI dell'estensione diag per codici di errore, se presente  |  R  |     
 refs.diag.logs                   | stringa     | L'URI dell'estensione diag per log, se presente        |  R  |     
 refs.location                    | stringa     | L'URI dell'estensione ubicazione, se presente             |  R  |     
 refs.mgmt                        | stringa     | L'URI dell'estensione mgmt, se presente                 |  R  |     



## Attributi estesi
{: #extended_attributes}

In aggiunta agli attributi principali elencati nella precedente sezione Attributi, esistono ulteriori attributi
che sono trattati come estensioni del modello di dispositivo principale. Query semplici sul dispositivo restituiscono informazioni
dal modello di dispositivo principale, ma non le estensioni. Le informazioni
dalle estensioni devono essere specificamente richieste. 


Nome estensione    | Prefisso degli attributi | Scopo      
------------- | ------------- | -------------                                         
 Diagnostica       | diag                 | Log degli errori e informazioni di diagnostica                 
 Ubicazione          | location             | Ubicazione del dispositivo, potenzialmente aggiornato regolarmente
 Gestione dispositivo | mgmt                 | Azioni di gestione dispositivo, ad esempio aggiornamento firmware       


### Estensioni di diagnostica


Gli attributi di diagnostica sono facoltativi e presenti solo per i dispositivi con informazioni di log degli errori. Questi attributi sono progettati per la diagnosi dei problemi del dispositivo, non per la risoluzione dei problemi di connettività a {{site.data.keyword.iot_short_notm}}. Per poter richiamare le informazioni in questi attributi, devono essere interrogate separatamente, perché le informazioni memorizzate in tali attributi possono essere molto grandi.

Le informazioni del log di diagnostica sono una schiera di voci che possono avere voci accodate utilizzando l'API, tuttavia, ciò può provocare la perdita di voci precedenti, al fine di mantenere gestibile la dimensione dei log di diagnostica. Ogni voce consiste di un messaggio, un'indicazione di severità, una registrazione data/ora e una schiera byte di dati facoltativa. 


Attributo            | Tipo       | Descrizione                                                 | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 diag.errorCodes[]    | array di </br> numeri interi  | Schiera di codici di errore                                         |  A  |  A  
 diag.log[]           | array      | Schiera di dati diagnostici                                    |  A  |  A  
 diag.log[].message   | stringa     | Messaggio di diagnostica                                           |     |     
 diag.log[].timestamp | stringa     | Data-ora ISO8601: La data e l'ora della voce di log               |     |     
 diag.log[].logData   | stringa     | byte: dati diagnostici, codificato base-64                       |     |     
 diag.log[].severity  | numero     | Severità del messaggio, 0: informativo, 1: avvertenza, 2: errore  |     |     


### Estensione dell'ubicazione

Questi attributi sono facoltativi e presenti solo per i dispositivi con informazioni di ubicazione. Le informazioni di ubicazione vengono archiviate separatamente per consentire l'uso di meccanismi di archiviazione più adatti alle informazioni dinamiche in caso di informazioni aggiornate di frequente, ad esempio, nel caso di un dispositivo mobile.

Per le soluzioni che danno particolare importanza agli aggiornamenti dell'ubicazione frequenti, è previsto che l'ubicazione sia trattata come parte del payload dell'evento del dispositivo, abilitando i ritmi di aggiornamento più frequenti, l'archiviazione cronologica semplice e l'analisi.


Attributo                 | Tipo   | Descrizione                                             | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 location.longitude        | numero | Longitudine in gradi decimali utilizzando WGS84                |  W  |  W  
 location.latitude         | numero | Latitudine in gradi decimali utilizzando WGS84                 |  W  |  W  
 location.elevation        | numero | Altitudine in metri utilizzando WGS84                         |  W  |  W  
 location.measuredDateTime | stringa |Data-ora ISO8601: La data e l'ora della misurazione ubicazione |  W  |  W  
 location.updatedDateTime  | stringa | Data-ora ISO8601: La data e l'ora                        |  R  |     
 location.accuracy         | numero | Accuratezza della posizione in metri                      |  W  |  W  


### Estensione della gestione del dispositivo 

Gli attributi `mgmt.` sono presenti solo per i sistemi gestiti. Quando un sistema gestito diventa inattivo, diventa non gestito e gli attributi `mgmt.` vengono eliminati. Gli attributi `mgmt.` sono impostati da {{site.data.keyword.iot_short_notm}} come risultato dell'elaborazione delle richieste di gestione del dispositivo. Questi attributi non possono essere scritti direttamente utilizzando l'API. 

I dispositivi hanno un ciclo di vita di gestione, che è definito in base al proprio stato come dispositivi gestiti. L'agent di gestione dispositivo sul dispositivo è responsabile dell'invio di una richiesta Gestisci dispositivo utilizzando il protocollo di gestione dispositivo. Per gestire i dispositivi inattivi in una gran numero di dispositivi, è possibile impostare un sistema gestito ad inviare una richiesta di gestione del dispositivo regolarmente, consentendo a {{site.data.keyword.iot_short_notm}} di essere notificato quando un dispositivo diventa inattivo. Per facilitare questa funzionalità, la richiesta di gestione del dispositivo dispone di un parametro del ciclo di vita facoltativo. Quando {{site.data.keyword.iot_short_notm}} riceve una richiesta di gestione del dispositivo, calcola il tempo prima che sia effettuata un'altra richiesta e l'archivia nell'attributo `mgmt.dormantDateTime`.


Attributo                      | Tipo    | Descrizione                                            | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 mgmt.dormant                   | booleano | Se il dispositivo è diventato inattivo                  |  R  |     
 mgmt.dormantDateTime           | stringa  | Data-ora ISO8601: La data e l'ora in cui il dispositivo gestito diventerà inattivo   |  R  |     
 mgmt.lastActivityDateTime      | stringa  | Data-ora ISO8601: La data e l'ora dell'ultima attività, aggiornata periodicamente    |  R  |     
 mgmt.supports.deviceActions    | booleano | Indica se il dispositivo supporta le azioni Riavvia e Reimpostazione alle impostazioni di fabbrica  |  R  |     
 mgmt.supports.firmwareActions  | booleano | Indica se il dispositivo supporta le azioni Scaricamento firmware e Aggiornamento firmware    |  R  |     
 mgmt.firmware.version          | stringa  | La versione del firmware sul dispositivo              |  R  |  W  
 mgmt.firmware.name             | stringa  | Il nome del firmware da utilizzare sul dispositivo      |  R  |  W  
 mgmt.firmware.uri              | stringa  | L'URI da cui può essere scaricata l'immagine del firmware |  R  |  W  
 mgmt.firmware.verifier         | stringa  | Il verificatore, ad esempio un checksum per l'immagine del firmware per convalidarne l'integrità |  R  |  W  
 mgmt.firmware.state            | numero  | Indica lo stato dello scaricamento del firmware                |  R  |  W  
 mgmt.firmware.updateStatus     | numero  | Indica lo stato dell'aggiornamento                      |  R  |  W  
 mgmt.firmware.updatedDateTime  | stringa  | Data-ora ISO8601: La data dell'ultimo aggiornamento                 |  R  |     
