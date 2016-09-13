---

copyright:
 years: 2015, 2016

---

# Informazioni su {{site.data.keyword.mobilepushshort}}
{: #overview-push}
Ultimo aggiornamento: 16 agosto 2016
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} è un servizio che puoi utilizzare per inviare notifiche ai dispositivi iOS e Android. Le notifiche possono essere destinate a tutti gli utenti dell'applicazione oppure a uno specifico insieme di utenti e dispositivi facendo uso delle tag. Puoi amministrare dispositivi, tag e sottoscrizioni. Puoi anche utilizzare API (application program interface) REST (Representational State Transfer) e SDK (software development kit) per sviluppare ulteriormente le tue applicazioni client. 

{{site.data.keyword.mobilepushshort}} è anche disponibile come servizio Bluemix Dedicato. Per informazioni sul servizio dedicato {{site.data.keyword.mobilepushshort}}, vedi [Servizi dedicati](../../dedicated/index.html). Tieni presente che la scheda di monitoraggio di {{site.data.keyword.mobilepushshort}} non visualizza dati di analisi.

Il servizio {{site.data.keyword.mobilepushshort}} è ora abilitato con OpenWhisk. Per ulteriori informazioni, vedi [OpenWhisk](../../openwhisk/index.html).


## Processo del servizio {{site.data.keyword.mobilepushshort}}
{: #overview_push_process}

I client mobili possono sottoscrivere e registrarsi per il servizio {{site.data.keyword.mobilepushshort}}. All'avvio, le applicazioni mobili si registrano al servizio {{site.data.keyword.mobilepushshort}} e lo sottoscrivono. Le notifiche vengono spedite
                al servizio APNS (Apple Push Notification Service) o al server GCM (Google Cloud Messaging)
                e inviate quindi ai client mobili registrati.

![Panoramica Push](images/overview.jpg)


###applicazioni mobili
{: mobile-applications}

All'avvio, le applicazioni mobili si registrano al servizio {{site.data.keyword.mobilepushshort}} e lo sottoscrivono per ricevere notifiche.

###Applicazioni di backend
{: backend-applications}

Le applicazioni di backend possono essere in loco o in un cloud pubblico. Le applicazioni di backend utilizzeranno il servizio {{site.data.keyword.mobilepushshort}} per inviare notifiche sensibili al contesto agli utenti mobili. Le applicazioni di back non devono necessariamente conservare e gestire informazioni sugli utenti e i dispositivi mobili per inviare notifiche di push. Invece, le applicazioni di backend possono utilizzare il servizio {{site.data.keyword.mobilepushshort}}.

###Proprietario backend applicazione
{: app-backend-owner}

Il proprietario del backend dell'applicazione crea l'applicazione di backend mobile che aggrega un'istanza al servizio {{site.data.keyword.mobilepushshort}}. Il proprietario del backend dell'applicazione configurare inoltre il servizio {{site.data.keyword.mobilepushshort}} in modo che le applicazioni di backend utilizzino il servizio con le applicazioni mobili destinate a {{site.data.keyword.mobilepushshort}}.

###Servizio {{site.data.keyword.mobilepushshort}}
{: push-notification-service}

Il servizio {{site.data.keyword.mobilepushshort}} gestisce tutte le informazioni relative ai dispositivi registrati per le notifiche. Il servizio fornisce alle tue applicazioni la trasparenza dei dettagli di tecnologia relativi all'invio di notifiche a queste eterogenee piattaforme mobili, gestendo tutto questo internamente. 

###Gateway
{: gateways}

Servizi cloud specifici per piattaforme di dispositivi mobili quali GCM (Google Cloud Messaging) o APNS (Apple Push Notification Service) utilizzando il servizio {{site.data.keyword.mobilepushshort}} per inviare notifiche alle applicazioni mobili.

###Sicurezza push
{: push-security}

Le API {{site.data.keyword.mobilepushshort}} sono protette da due tipi di segreti - i) appSecret ii) clientSecret.  'appSecret' protegge le API normalmente richiamate dalle applicazioni di backend come le API da inviare a {{site.data.keyword.mobilepushshort}}, l'API configura le impostazioni.   'clientSecret' protegge le API normalmente richiamate dalle applicazioni client mobili.  Al momento, è presente solo un'API correlata alla registrazione di un dispositivo con un ID utente associato che richiede 'clientSecret'. Tutte le altre API richiamate dai client mobili non richiedono clientSecret. 'appSecret' e 'clientSecret' sono assegnati a ogni istanza del servizio al momento del bind di un'applicazione al servizio {{site.data.keyword.mobilepushshort}}. Fai riferimento alla documentazione API ReST per ulteriori informazioni su come i segreti vengono trasmessi e a quale API.

## Tipi di {{site.data.keyword.mobilepushshort}}
{: #overview-push-types}

###Broadcast
{: broadcast}

Quando un'applicazione mobile si registra al servizio {{site.data.keyword.mobilepushshort}}, può iniziare a ricevere i broadcast. Le notifiche broadcast sono messaggi destinati a tutti i dispositivi con un'applicazione installata e configurata per il servizio {{site.data.keyword.mobilepushshort}}. Le notifiche broadcast sono abilitate per impostazione predefinita con qualsiasi applicazione abilitata per {{site.data.keyword.mobilepushshort}}. Le applicazioni abilitate per il servizio {{site.data.keyword.mobilepushshort}} hanno una sottoscrizione predefinita alla tag Push.ALL, che viene utilizzata dal server per eseguire il broadcast dei messaggi di notifica a tutti i dispositivi. Per inviare una notifica broadcast che utilizza la API Push
                        REST, assicurati che la destinazione ("target") sia un JSON vuoto all'inserimento nella
                        risorsa messaggi.

###Notifiche basate sulle tag
{: tag-based-notifications}

Le notifiche basate sulle tag sono messaggi destinati a tutti i dispositivi sottoscritti a una particolare tag. Le notifiche basate sulle tag
                        consentono la segmentazione di notifiche sulla base di argomenti o di aree
                        oggetto. I destinatari della notifica possono scegliere di ricevere le notifiche solo
                        se sono relative a un oggetto o a un argomento a cui sono interessati. Pertanto,
                        la notifica basata sulle tag fornisce un mezzo per segmentare i destinatari. Questa funzione
                        consente di definire delle tag e quindi di inviare e ricevere messaggi in
                        base alle tag. Un messaggio viene indirizzato solo ai dispositivi che hanno
                        sottoscritto una tag. Devi prima creare le tag per l'applicazione, impostare le sottoscrizioni di tag e iniziare quindi le notifiche basate sulle tag. Per inviare una notifica basata sulle tag che utilizza la API REST, assicurati che i "tagName" siano forniti all'inserimento nella risorsa messaggi. 

###Notifiche Unicast
{: unicast-notifications}

Le notifiche Unicast sono messaggi destinati a un dispositivo o un utente particolare. Le notifiche Unicast destinate ai dispositivi non richiedono alcuna impostazione aggiuntiva e sono abilitate per impostazione predefinita quando l'applicazione è abilitata per {{site.data.keyword.mobilepushshort}}.

Tuttavia, le notifiche Unicast destinate agli utenti richiedono:

- L'associazione di un ID utente a un dispositivo al momento della registrazione del dispositivo mobile per le notifiche push.  

- L'autorizzazione come una registrazione ID utente che trasmette un 'clientSecret' assegnato durante il bind dell'applicazione di backend al servizio {{site.data.keyword.mobilepushshort}}. 

Normalmente, un'applicazione mobile prima eseguirà un ciclo di autenticazione in cui l'utente dell'applicazione mobile viene autenticato in un servizio di autenticazione [come Mobile Client Access](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html). Dopo la corretta autenticazione, l'ID dell'utente autenticato viene trasmesso all'API Push Device Registration con un clientSecret. La presenza di un clientSecret impone solo l'associazione autorizzata di ID utente con le registrazioni del dispositivo mobile.
Per inviare notifiche Unicast tramite l'API REST, assicurati che gli ID del dispositivo o dell'utente siano forniti durante l'inserimento in una risorsa messaggi.

###Notifiche basate sulla piattaforma
{: platform-based-notifications}

Il recapito delle notifiche può essere destinato a una specifica piattaforma di dispositivo. Ad esempio, una notifica può essere
                            inviata solo a tutti gli utenti Android. Per inviare una notifica basata sulla
                            piattaforma che utilizza la API REST, assicurati che le piattaforme
                            di destinazione siano fornite all'inserimento in una risorsa messaggi. Specifica
                            le piattaforme come un array. Le piattaforme supportate sono:
* A (Apple)
* G (Google)

## Dimensione messaggio {{site.data.keyword.mobilepushshort}}
{: #push-message-size}

La dimensione del payload del messaggio di {{site.data.keyword.mobilepushshort}} dipende dai mediatori. 

###iOS
{: ios-message-size}

Per iOS 8 e successivi, la dimensione massima consentita è 2 kilobyte. Il Push Notification service per Apple non invia notifiche che superano questo limite.

###Android
{: android-message-size}

Non esistono limitazione nella piattaforma Android.
