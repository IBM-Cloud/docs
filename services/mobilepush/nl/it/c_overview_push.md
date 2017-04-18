---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Informazioni su {{site.data.keyword.mobilepushshort}}
{: #overview-push}
Ultimo aggiornamento: 18 gennaio 2017
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} è un servizio che puoi utilizzare per inviare notifiche a dispositivi e piattaforme. Le notifiche possono essere destinate a tutti gli utenti dell'applicazione oppure a uno specifico insieme di utenti e dispositivi facendo uso delle tag. Puoi amministrare dispositivi, tag e sottoscrizioni.  

Puoi utilizzare una delle seguenti opzioni per creare un servizio associato o non associato:

- Creando un'applicazione Bluemix mediante il contenitore tipo MobileFirst Services Starter dal catalogo. In questo modo si crea un servizio Push Notifications associato a un'applicazione di backend Bluemix.
- Creando un servizio Push Notifications non associato direttamente dal catalogo Mobile. Puoi associarlo in seguito a un'applicazione o scegliere di utilizzarlo non associato. 
- Utilizzando il [dashboard Mobile ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://console.ng.bluemix.net/docs/mobile/services.html "Icona link esterno"){: new_window}.

Tieni presente che la scheda di monitoraggio di {{site.data.keyword.mobilepushshort}} non visualizza dati di analisi.

Il servizio {{site.data.keyword.mobilepushshort}} è ora abilitato con OpenWhisk. Per ulteriori informazioni, vedi [OpenWhisk](/docs/openwhisk/index.html).


## Processo del servizio {{site.data.keyword.mobilepushshort}}
{: #overview_push_process}

I client browser web, mobili e le estensioni e le applicazioni Google Chrome possono sottoscriversi e registrarsi per il servizio {{site.data.keyword.mobilepushshort}}. All'avvio, le applicazioni client si registrano al servizio {{site.data.keyword.mobilepushshort}} e lo sottoscrivono. Le notifiche vengono spedite al servizio APNS (Apple Push Notification Service) o al server FCM (Firebase Cloud Messaging)/GCM (Google Cloud Messaging) e inviate quindi ai client mobili o browser registrati.

![Panoramica Push](images/overview.jpg)


### Applicazioni mobili e browser
{: mobile-applications}

All'avvio, le applicazioni client si registrano al servizio {{site.data.keyword.mobilepushshort}} e lo sottoscrivono per ricevere notifiche.

### Applicazioni di backend
{: backend-applications}

Le applicazioni di backend possono essere in loco o in un cloud pubblico. Le applicazioni di backend utilizzeranno il servizio {{site.data.keyword.mobilepushshort}} per inviare notifiche sensibili al contesto agli utenti mobili o browser. Le applicazioni di backend non devono necessariamente conservare e gestire informazioni sugli utenti, sugli agent browser e sui dispositivi mobili per inviare notifiche di push. Invece, le applicazioni di backend possono utilizzare il servizio {{site.data.keyword.mobilepushshort}} che le gestisce e mantiene.

### Proprietario backend applicazione
{: app-backend-owner}

Il proprietario del backend dell'applicazione crea l'applicazione di backend mobile che aggrega un'istanza al servizio {{site.data.keyword.mobilepushshort}}. Il proprietario del backend dell'applicazione configurare inoltre il servizio {{site.data.keyword.mobilepushshort}} in modo che le applicazioni di backend utilizzino il servizio con le applicazioni mobili e browser destinate a {{site.data.keyword.mobilepushshort}}.

### Servizio {{site.data.keyword.mobilepushshort}}
{: push-notification-service}

Il servizio {{site.data.keyword.mobilepushshort}} gestisce tutte le informazioni relative ai dispositivi mobili e ai client browser web registrati per le notifiche. Il servizio fornisce alle tue applicazioni la trasparenza dei dettagli di tecnologia relativi all'invio di notifiche a queste eterogenee piattaforme mobili e browser web, gestendo tutto questo internamente.

### Gateway
{: gateways}

Servizi cloud specifici per piattaforme quali FCM/GCM o APNS (Apple Push Notification Service) utilizzati dal servizio {{site.data.keyword.mobilepushshort}} IBM per inviare notifiche alle applicazioni mobili e browser.

### Sicurezza push
{: push-security}

Le API {{site.data.keyword.mobilepushshort}} sono protette da due tipi di segreti:

- **appSecret**: 'appSecret' protegge le API normalmente richiamate dalle applicazioni di backend, come l'API per inviare {{site.data.keyword.mobilepushshort}} e l'API per configurare le impostazioni.
- **clientSecret**:  'clientSecret' protegge le API normalmente richiamate dalle applicazioni client mobili. È presente solo un'API correlata alla registrazione di un dispositivo con un ID utente associato che richiede 'clientSecret'. Nessuna delle altre API richiamate dai client mobili richiede il clientSecret. 

'appSecret' e 'clientSecret' sono assegnati a ogni istanza del servizio al momento del bind di un'applicazione al servizio {{site.data.keyword.mobilepushshort}}. Fai riferimento alla documentazione [API REST ![Icona link esterno](../../icons/launch-glyph.svg "Icona link esterno")](https://mobile.{DomainName}/imfpush/ "Icona link esterno") per informazioni su come i segreti vengono trasmessi e a quale API.

**Nota**: sono necessarie le precedenti applicazioni per trasmettere il clientSecret solo quando viene seguita la registrazione o l'aggiornamento dei dispositivi con il campo userID. Tutte le altre API richiamate dai client mobili e browser non richiedono il clientSecret. Queste vecchie applicazioni possono continuare ad utilizzare il clientSecret facoltativamente per le registrazioni del dispositivo o per l'aggiornamento delle chiamate. Tuttavia, è fortemente raccomandato che il controllo clientSecret venga applicato a tutte le chiamate API client. Per applicarlo alle applicazioni esistenti, è stata pubblicata una nuova API denominata 'verifyClientSecret'.  Per le nuove applicazioni, il controllo clientSecret sarà imposto per tutte le chiamate API client e questo comportamento non può essere modificato con l'API 'verfiyClientSecret'.

Per impostazione predefinita, la verifica del segreto client viene forzata solo nelle nuove applicazioni. Alle applicazioni nuove e esistenti è consentito abilitare o disabilitare la verifica del segreto client utilizzando l'API REST verifyClientSecret. Ti raccomandiamo di forzare la verifica del segreto client per evitare l'esposizione dei dispositivi agli utenti che possono conoscere il applicationId e il deviceId.

Assicurati che il 'clientSecret' sia mantenuto confidenziale e non inserirlo mai nell'applicazione mobile. Esistono vari modelli di inizializzazione dell'applicazione che possono essere utilizzati per estrarre il 'clientSecret' dinamicamente durante il runtime delle applicazioni. Il diagramma della sequenza illustra il possibile modello.
![Enable_Push](images/init_client_secret.jpg) 

## Tipi di {{site.data.keyword.mobilepushshort}}
{: #overview-push-types}

### Broadcast
{: broadcast}

Quando un'applicazione client si registra al servizio {{site.data.keyword.mobilepushshort}}, può iniziare a ricevere i broadcast. Le notifiche broadcast sono messaggi destinati a tutte le istanze di un'applicazione installate nei dispositivi mobili, nei browser o implementate come applicazioni Chrome o istanze dell'estensione e configurate per il servizio {{site.data.keyword.mobilepushshort}}. Le notifiche broadcast sono abilitate per impostazione predefinita con qualsiasi applicazione abilitata per {{site.data.keyword.mobilepushshort}}. Le applicazioni abilitate per il servizio {{site.data.keyword.mobilepushshort}} hanno una sottoscrizione predefinita alla tag Push.ALL, che viene utilizzata dal server per eseguire il broadcast dei messaggi di notifica a tutti i dispositivi. Per inviare una notifica broadcast che utilizza la API Push
                        REST, assicurati che la destinazione ("target") sia un JSON vuoto all'inserimento nella
                        risorsa messaggi.

### Notifiche basate sulle tag
{: tag-based-notifications}

Le notifiche basate sulle tag sono messaggi destinati a tutti i dispositivi sottoscritti a una particolare tag. Le notifiche basate sulle tag
                        consentono la segmentazione di notifiche sulla base di argomenti o di aree
                        oggetto. I destinatari della notifica possono scegliere di ricevere le notifiche solo
                        se sono relative a un oggetto o a un argomento a cui sono interessati. Pertanto,
                        la notifica basata sulle tag fornisce un mezzo per segmentare i destinatari. Questa funzione
                        consente di definire delle tag e quindi di inviare e ricevere messaggi in
                        base alle tag. Un messaggio viene indirizzato solo alle istanze dell'applicazione client (mobili, browser o come un'applicazione o estensioni) sottoscritte a una tag. Devi prima creare le tag per l'applicazione, impostare le sottoscrizioni di tag e iniziare quindi le notifiche basate sulle tag. Per inviare una notifica basata sulle tag che utilizza la API REST, assicurati che i "tagName" siano forniti all'inserimento nella risorsa messaggi.

### Notifiche Unicast
{: unicast-notifications}

Le notifiche Unicast sono messaggi destinati a un dispositivo o un utente particolare. Le notifiche Unicast destinate ai dispositivi non richiedono alcuna impostazione aggiuntiva e sono abilitate per impostazione predefinita quando l'applicazione è abilitata per {{site.data.keyword.mobilepushshort}}.

Tuttavia, le notifiche Unicast indirizzate agli utenti richiedono l'associazione di un ID utente a un dispositivo al momento della registrazione del dispositivo mobile client o del browser web o delle estensioni e delle applicazioni Chrome per {{site.data.keyword.mobilepushshort}}.   

Normalmente, un'applicazione client prima eseguirà un ciclo di autenticazione in cui l'utente dell'applicazione mobile viene autenticato in un servizio di autenticazione come [Mobile Client Access](docs/services/mobileaccess/index.html). Dopo la corretta autenticazione, l'ID dell'utente autenticato viene trasmesso all'API Push Device Registration. 
Per inviare notifiche Unicast tramite l'API REST, assicurati che gli ID del dispositivo o dell'utente siano forniti durante l'inserimento in una risorsa messaggi.

### Notifiche basate sulla piattaforma
{: platform-based-notifications}

Il recapito delle notifiche può essere destinato a una specifica piattaforma di dispositivo. Ad esempio, una notifica può essere inviata solo a tutti gli utenti Android o solo agli utenti Google Chrome. Per inviare una notifica basata sulla
                            piattaforma che utilizza la API REST, assicurati che le piattaforme
                            di destinazione siano fornite all'inserimento in una risorsa messaggi. Specifica
                            le piattaforme come un array. Le piattaforme supportate sono:
* A (Apple)
* G (Google)
* WEB_CHROME (Google Chrome Browser Web Push)
* WEB_FIREFOX (Mozilla Firefox Browser Web Push)
* WEB_SAFARI (Safari Browser Web Push)
* APPEXT_CHROME (Google Chrome Apps & Extensions)

## Dimensione messaggio {{site.data.keyword.mobilepushshort}}
{: #push-message-size}

La dimensione del payload del messaggio di {{site.data.keyword.mobilepushshort}} dipende dai vincoli disposti dai gateway (FCM/GCM, APNs) e dalle piattaforme client. 

### iOS e Safari
{: ios-message-size}

Per iOS 8 e successivi, la dimensione massima consentita è 2 kilobyte. Il Push Notification service per Apple non invia notifiche che superano questo limite.

### Estensioni Android, browser Firefox, browser Chrome e applicazioni Chrome &
{: android-message-size}

Esiste una limitazione di 4 kilobyte come massimo consentito per la dimensione del payload del messaggio.  
