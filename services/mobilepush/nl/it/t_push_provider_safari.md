---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configurazione delle credenziali per i browser Web
{: #configure-credential-for-browsers}
Ultimo aggiornamento: 11 gennaio 2017
{: .last-updated}

Il servizio IBM {{site.data.keyword.mobilepushshort}} ora estende le funzionalità per inviare le notifiche al tuo browser. 

L'URL o il nome dominio del tuo sito Web è richiesto dal servizio {{site.data.keyword.mobilepushshort}} per identificare le richieste che devono essere consentite. Un'istanza del servizio {{site.data.keyword.mobilepushshort}} supporta un solo nome dominio alla volta. Pertanto, assicurati che sia impostato lo stesso valore per Chrome, Firefox e Safari. 

I browser Chrome e Safari richiedono una configurazione aggiuntiva per il push web. Avrai bisogno di una chiave API FCM in quanto viene utilizzato un endpoint FCM per consegnare i messaggi in Chrome. Per ottenere la tua chiave API FCM, vedi [Configurazione delle credenziali per FCM](t_push_provider_android.html).



##Configurazione del push web per Chrome e Firefox 
{: #config-chrome-firefox}

1. Nel pannello del dashboard Push, seleziona **Configure**.
2. Seleziona la scheda Web.
	![Configurazioni push web](images/webpush_configure.jpg)
3. Configura la chiave API FCM/GCM e l'URL del tuo sito web che sarà registrato per ricevere le notifiche push.
4. Fai clic su **Save**.
5. Fasi successive. [Abilitazione delle notifiche per i browser Google Chrome e Mozilla Firefox](c_enable_push.html).


## Configurazione del push web per Safari 
{: #configure-safari}

La versione supportata per il servizio {{site.data.keyword.mobilepushshort}} su Safari è la 10.0. Prima di poter configurare il tuo browser per la ricezione delle notifiche, devi generare un certificato tramite il tuo account Apple Developer.

### Generazione di un certificato
{: #certificate-generation}

Assicurati di disporre in un account Apple Developer. Hai bisogno di registrare un ID push sito web e generare un certificato per configurare il tuo browser Safari per ricevere le notifiche. La seguente procedura ti aiuterà ad iniziare.

1. Nel Apple Developer Member center, fai clic su **Certificates, ID & Profiles**. 
2. Fai clic su **Identifiers** e quindi su **Website Push IDs**.
3. Scegli di creare una nuova voce selezionando l'icona più.
  ![Dashboard Push](images/safari_1.jpg)

4. Nel pannello Register Website Push ID, fornisci un ID identificativo e una descrizione Website Push ID appropriati. Ti raccomandiamo che sia nel formato del nome a dominio inverso, e che inizi con 'web'. Ad esempio: web.com.example.dailyweatherreports.
5. Registra l'ID push sito web. Ora hai un ID push sito web. 
6. Seleziona **Edit** per creare un certificato da utilizzare per l'ID push sito web.
7. Nella finestra Certificate Assistant per Certificate Information, fornisci il tuo indirizzo email e un nome comune. Lascia l'indirizzo email Certificate Authority vuoto.
8. Fai clic su **Save to disk** e seleziona **Continue**.
9. Scegli di salvare il certificato in una cartella appropriata.
10. Scegli il `.certSigningRequest` creato sul disco quando ti viene richiesto nella procedura guidata di creazione del certificato. Assicurati di scaricare il certificato di push sito web creato nel formato `.cer`.
11. Apri il certificato nello strumento KeyChain Access. Fai clic con il tasto destro del mouse ed esportalo come certificato p12. Annota la password fornita durante la generazione del certificato p12.


### Configurazione per le notifiche
  {: #configuration-notification}
 
Dopo aver generato il certificato, puoi configurare il servizio per l'invio di notifiche a Safari. 

Completa la procedura:

1. Nel dashboard del servizio Push Notifications, fai clic su **Configure**. 
2. Seleziona la scheda Web. 
3. Nella sezione Safari Push, aggiorna il modulo con le informazioni richieste. 
	- **Website Name**: il nome che hai fornito nel centro di notifica.
	- **Website Push ID**: aggiorna con la stringa reverse-domain per il tuo ID push sito web. Ad esempio, web.com.example.www.
	- **Website URL**: fornisci l'URL del sito web da sottoscrivere alle notifiche di push. Ad esempio, https://www.example.com.
	- **Allowed Domains**: parametro facoltativo. Indica l'elenco di siti web che richiedono l'autorizzazione dall'utente. Assicurati che gli URL siano valori separati da virgola. Se non si fornisce questo valore, verrà utilizzato quello specificato in Website URL. 
	- **URL Format String**: l'URL da risolvere quando si fa clic sulla notifica. Ad esempio, ["https://www.example.com"]. Assicurati che l'URL utilizzi lo schema http o https.
	- **Safari web push certificate**: carica il certificato .p12 e fornisci la password.
4. Fai clic su **Save**.	

![Dashboard Push](images/push_configure_safari.jpg)	

Il servizio è ora configurato per l'invio di notifiche di push al browser Safari.

	
