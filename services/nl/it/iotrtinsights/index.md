---

copyright:
  years: 2015,2016

---

{:new_window: target=_"blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introduzione a {{site.data.keyword.iotrtinsights_full}}
{: #gettingstartedtemplate}
*Ultimo aggiornamento: 11 febbraio 2016*

Con {{site.data.keyword.iotrtinsights_full}} su Bluemix ({{site.data.keyword.iotrtinsights_short}}), puoi eseguire delle analisi sui dati in tempo reale dai tuoi dispositivi Internet delle cose (IoT) e avere informazioni approfondite sul loro stato di integrità e sullo stato complessivo delle tue operazioni.
{:shortdesc}

Prima di potere iniziare a usare {{site.data.keyword.iotrtinsights_short}} devi configurare il servizio {{site.data.keyword.iot_full}} ({{site.data.keyword.iot_short}}) per connettere il tuo motore di analisi ai tuoi dispositivi. Puoi utilizzare un servizio {{site.data.keyword.iot_short}} oppure crearne uno nuovo. Per essere rapidamente operativo, puoi distribuire l'applicazione telefonica Internet delle cose (IoT) e il suo servizio {{site.data.keyword.iot_short}} associato alla tua organizzazione.

Per essere rapidamente operativo con questo servizio, attieniti alla seguente procedura:
1. Distribuisci il servizio {{site.data.keyword.iotrtinsights_short}} alla tua organizzazione Bluemix.
  1. Dal dashboard del tuo account Bluemix, fai clic su **Utilizza servizi o API**.
  2. Individua la sezione Internet delle cose del catalogo servizi e seleziona **{{site.data.keyword.iotrtinsights_short}}**.
  3. Nella pagina {{site.data.keyword.iotrtinsights_short}}, verifica le selezioni Aggiungi servizio:  
    - Spazio - verifica che stai distribuendo il servizio nello stesso spazio in cui hai distribuito il servizio {{site.data.keyword.iot_short}}.
    - Applicazione - lascia senza binding.
    - Nome servizio - facoltativamente, modifica il nome servizio in qualcosa facile da ricordare. Questo nome viene visualizzato nel tile di {{site.data.keyword.iotrtinsights_short}} IoT nel dashboard Bluemix.
    - Piano selezionato - seleziona Gratuito oppure un piano di acquisto adatto per le tue esigenze.  
    > **Importante:** con il piano {{site.data.keyword.iotrtinsights_short}} gratuito, puoi distribuire solo una singola istanza del servizio per organizzazione.
  4. Fai clic su **Utilizza** per distribuire {{site.data.keyword.iotrtinsights_short}} ai tuoi servizi Bluemix.
2. Facoltativo: utilizza il tuo telefono come un dispositivo IoT con {{site.data.keyword.iotrtinsights_short}} IoT.
Utilizza l'applicazione telefonica Internet delle cose (IoT) per configurare rapidamente il tuo smartphone perché funga da dispositivo IoT che puoi utilizzare per verificare il
tuo ambiente {{site.data.keyword.iotrtinsights_short}} e iniziare a definire un'analisi in tempo reale sui dati. Per ulteriori informazioni sull'applicazione telefonica Internet delle cose (IoT), vedi il progetto relativo all'[applicazione telefonica Internet delle cose (IoT)](https://github.com/ibm-messaging/IoT-html5-phone).

  Per creare l'applicazione e connettere il tuo telefono a {{site.data.keyword.iot_full}}:
  1. Fai clic sul pulsante in basso per avviare il processo di distribuzione:
  [![Icona Distribuisci a Bluemix.](https://bluemix.net/deploy?repository=https://github.com/ibm-messaging/iot-html5-phone "Distribuire il telefono IoT a Bluemix")(images/deploy_to_bluemix.png "Icona Distribuisci a Bluemix")]  
  > **Nota:** la distribuzione dell'applicazione telefonica Internet delle cose (IoT) distribuisce anche un servizio {{site.data.keyword.iot_short}} (*iot-phone-iotf-service*) che si associa automaticamente all'applicazione telefonica. Aggiungi questo {{site.data.keyword.iot_short}} come un'origine dati per testare l'applicazione telefonica Internet delle cose (IoT). Crea anche un servizio Cloudant NoSQL DB (*iot-phone-cloudant-cloudantNoSQLDB*) che viene utilizzato dall'applicazione.

  2. Fai clic su **Approva** se ti viene richiesto di autoapprovare l'accesso per il servizio IBM Single Sign On Service (OAuth Consent).  
  >**Suggerimento:** se non hai un account Bluemix, puoi registrati per attivare la tua versione di prova di Bluemix.
  2. Modifica il campo NOME APPLICAZIONE in qualcosa facile da ricordare; lo indicheremo come *applicazione telefonica* nel resto di queste istruzioni. Questo nome sarà visualizzato in un tile di applicazione nel tuo dashboard Bluemix e fa parte dell'URL che utilizzerai quando connetterai il tuo telefono a {{site.data.keyword.iot_short}}.
  2. Fai clic su **Distribuisci**.
  2. Dopo che il processo di distribuzione è stato completato ed è stato presentato un messaggio che indica che l'operazione ha avuto esito positivo, torna al tuo dashboard Bluemix.
  Il tile *applicazione telefonica* e il tile *iot-phone-iotf-service* sono aggiunti al tuo account.
  1. Dal dashboard Bluemix, fai clic sul tile *applicazione telefonica*.
  2. Dal tuo telefono, apri un browser e vai all'URL rotte visualizzato sotto il nome applicazione. Quando ti viene richiesto, immetti un ID dispositivo a tua scelta per identificare il tuo telefono come un dispositivo nei dashboard {{site.data.keyword.iot_short}} e {{site.data.keyword.iotrtinsights_short}} IoT.
  3. Fai clic su **Connetti** per connettere l tuo telefono a {{site.data.keyword.iot_short}} *iot-phone-iotf-service*.
  Questa vista viene aggiornata per visualizzare i dati inviati dal tuo telefono al tuo {{site.data.keyword.iot_short}}.
2. Crea e configura un servizio Internet delle cose (IoT).   
> **Suggerimento:** se hai distribuito l'applicazione telefonica Internet delle cose (IoT), *iot-phone-iotf-service* è già stato creato e puoi tralasciare questo passo.  

  1. Accedi all'organizzazione Bluemix e seleziona lo spazio dove desideri distribuire {{site.data.keyword.iotrtinsights_short}}IoT.
  2. Dal dashboard Bluemix, fai clic su **Utilizza servizi o API**.
  3. Individua la sezione Internet delle cose del catalogo servizi e seleziona **Internet delle cose**.
  4. Nella pagina {{site.data.keyword.iot_full}}, verifica le selezioni Aggiungi servizio e fai clic su **Utilizza** per aggiungere {{site.data.keyword.iot_short}} ai tuoi servizi Bluemix.
  Dopo che il servizio {{site.data.keyword.iot_short}} è stato distribuito, vieni indirizzato alla pagina di gestione dei servizi.
3. Individua le chiavi API di connessione.
Se hai creato un nuovo servizio {{site.data.keyword.iot_short}}, devi ora creare le chiavi API per connettere i due servizi. Se stai utilizzando un servizio esistente, puoi utilizzare le chiavi esistenti.  
  1. Dal dashboard Bluemix, fai clic sul tile Internet delle cose.  
  >**Nota:** se stati utilizzando l'applicazione telefonica Internet delle cose (IoT), fai clic sul tile *iot-phone-iotf-service*.  

  1. Fai clic su **Avvia dashboard** per aprire il dashboard {{site.data.keyword.iot_full}}.
  2. Passa a **Accedi > Chiavi API**.
  3. Fai clic su **Genera chiave API**.
  3. Annota la chiave API, il token di autenticazione e l'ID organizzazione visualizzati nella parte superiore del dashboard {{site.data.keyword.iot_short}}. Utilizzerai tali informazioni in {{site.data.keyword.iotrtinsights_short}} IoT per connettere i servizi.
4. Connetti il tuo servizio {{site.data.keyword.iot_short}} e il servizio {{site.data.keyword.iotrtinsights_short}} IoT.
  1. Dal dashboard Bluemix, fai clic sul tile {{site.data.keyword.iotrtinsights_short}} IoT.  
  2. Nella pagina del servizio, fai clic su **Aggiungi una origine dati**.
  2. Nella pagina Gestisci origini dati della console {{site.data.keyword.iotrtinsights_short}}, fai clic su **Aggiungi nuova origine dati**.
  3. Dai un nome descrittivo all'origine dati e fornisci le seguenti informazioni che avevi raccolto in precedenza:
    - ID organizzazione
    - Chiave API
    - Token di autenticazione
  4. Fai clic su ![icona Crea.](images/create.png "Icona Crea") per creare l'origine dati e connetterti a essa.
4. Inizia usando {{site.data.keyword.iotrtinsights_short}}.
Puoi ora iniziare a usare {{site.data.keyword.iotrtinsights_short}} aggiungendo utenti, connettendo i tuoi dispositivi, configurando i dashboard per visualizzare i dati dispositivo pertinenti e impostando avvisi.
>**Selezionando la tua istanza di {{site.data.keyword.iotrtinsights_short}}:** se ti è stato concesso l'accesso ad eventuali istanze di {{site.data.keyword.iotrtinsights_short}} aggiuntive come un operatore o un amministratore, puoi rapidamente passare dall'una all'altra di tali istanze. Nella console {{site.data.keyword.iotrtinsights_short}}, fai clic sul tuo nome utente e seleziona l'istanza a cui vuoi accedere.   

# link correlati
## esempi
* [Applicazione telefonica Internet delle cose (IoT)](https://github.com/ibm-messaging/IoT-html5-phone)
* [Ricette Internet delle cose developerWorks](https://developer.ibm.com/recipes/)
* [Creazione di applicazioni con l'applicazione starter Internet delle cose](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500)

## api
* [Documentazione API](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)

## generale
* [Informazioni su](iotrtinsights_overview.html)   
* [Novità nei servizi Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category)
* [Introduzione a {{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html)
* [Risposte dW su IBM developerWorks](https://developer.ibm.com/answers/topics/iot-real-time/)
