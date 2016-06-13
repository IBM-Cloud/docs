---

copyright:
 years: 2015, 2016

---

# Informazioni su Push Notifications
{: #overview-push}

Push Notifications è un servizio che puoi utilizzare per inviare notifiche al dispositivo iOS e Android. Le notifiche possono essere destinate a tutti gli utenti dell'applicazione oppure a uno specifico insieme di utenti e dispositivi facendo uso delle tag. Puoi amministrare dispositivi, tag e sottoscrizioni. Puoi anche utilizzare API (application program interface) REST (Representational State Transfer) e SDK (software development kit) per sviluppare ulteriormente le tue applicazioni client. Per informazioni sul servizio dedicato Push, vedi [Servizi dedicati](../../dedicated/index.html). 


## Processo Push notification service
{: #overview_push_process}

I client mobili possono sottoscrivere e registrarsi per il Push Notification Service. All'avvio,
                le applicazioni mobili si registrano al Push
                Notification Service e lo sottoscrivono. Le notifiche vengono spedite
                al servizio APNS (Apple Push Notification Service) o al server GCM (Google Cloud Messaging)
                e inviate quindi ai client mobili registrati.

![Panoramica Push](images/overview.jpg)


###applicazioni mobili

All'avvio, le applicazioni mobili si registrano al Push Notification Service e lo sottoscrivono per ricevere notifiche.

###Applicazioni di backend

Le applicazioni di backend possono essere in loco o in un cloud pubblico. Le applicazioni di backend utilizzano il Push
                        Notification Service per inviare notifiche sensibili al contesto agli utenti
                        mobili. Le applicazioni di backend non devono necessariamente conservare e gestire
                        informazioni sugli utenti e i dispositivi mobili per inviare notifiche di push. Le
                        applicazioni di backend possono invece utilizzare il Push Notification Service.

###Proprietario backend applicazione

Il ruolo che ha creato l'applicazione di backend mobile che aggrega un'istanza del Push Notification Service. Questa persona configura
                        e imposta il Push Notification Service in modo adatto alle applicazioni di backend che utilizzano
                        il Push Notification Service e alle applicazioni mobili che sono la destinazione delle notifiche di push.

###Push Notification Service

Il Push Notification Service gestisce tutte le informazioni correlate ai dispositivi che eseguono la registrazione per le notifiche. Il servizio fornisce alle tue applicazioni la trasparenza dei dettagli di tecnologia relativi all'invio di notifiche a queste eterogenee piattaforme mobili, gestendo tutto questo internamente.

###Gateway

Servizi cloud specifici per piattaforme di dispositivi mobili quali GCM (Google Cloud
                        Messaging) o APNS (Apple Push Notification Service) utilizzando il Push
                        Notification Service per inviare notifiche alle applicazioni mobili.

## Tipi di notifica di push
{: #overview-push-types}

###Broadcast

Quando un'applicazione mobile si registra al Push Notification Service, può iniziare a ricevere i broadcast. Le notifiche broadcast sono messaggi di notifica destinati a tutti i
                        dispositivi che hanno l'applicazione installata e configurata per il Push
                        Notification Service. Le notifiche broadcast sono abilitate per impostazione predefinita con qualsiasi
                        applicazione abilitata per le notifiche di push. Qualsiasi applicazione abilitata per il Push Notification Service ha una sottoscrizione predefinita alla tag Push.ALL, che viene utilizzata dal server per eseguire il broadcast dei messaggi di notifica a tutti i dispositivi. Per inviare una notifica broadcast che utilizza la API Push
                        REST, assicurati che la destinazione ("target") sia un JSON vuoto all'inserimento nella
                        risorsa messaggi.

###Notifiche basate sulle tag

Le notifiche basate sulle tag sono messaggi di notifica destinati a tutti i dispositivi che hanno
                        una sottoscrizione a una specifica tag. Le notifiche basate sulle tag
                        consentono la segmentazione di notifiche sulla base di argomenti o di aree
                        oggetto. I destinatari della notifica possono scegliere di ricevere le notifiche solo
                        se sono relative a un oggetto o a un argomento a cui sono interessati. Pertanto,
                        la notifica basata sulle tag fornisce un mezzo per segmentare i destinatari. Questa funzione
                        consente di definire delle tag e quindi di inviare e ricevere messaggi in
                        base alle tag. Un messaggio viene indirizzato solo ai dispositivi che hanno
                        sottoscritto una tag. Devi prima creare le tag per l'applicazione, impostare
                        le sottoscrizioni di tag e iniziare quindi le notifiche basate sulle
                        tag. Per inviare una notifica basata sulle tag che utilizza la API REST,
                        assicurati che i "tagName" siano forniti all'inserimento nella
                        risorsa messaggi.

###Notifiche Unicast

Le notifiche Unicast sono messaggi di notifica destinati a uno specifico dispositivo. Le notifiche Unicast non richiedono alcuna impostazione
                        aggiuntiva e sono abilitate per impostazione predefinita quando l'applicazione
                        è abilitata per le notifiche di push. Per inviare una notifica Unicast che utilizza la API REST, assicurati che siano forniti gli ID dispositivo (deviceId) all'inserimento in una risorsa messaggi.

###Notifiche basate sulla piattaforma

Il recapito delle notifiche può essere destinato a una specifica piattaforma di dispositivo. Ad esempio, una notifica può essere
                            inviata solo a tutti gli utenti Android. Per inviare una notifica basata sulla
                            piattaforma che utilizza la API REST, assicurati che le piattaforme
                            di destinazione siano fornite all'inserimento in una risorsa messaggi. Specifica
                            le piattaforme come un array. Le piattaforme supportate sono:
* A (Apple)
* G (Google)
