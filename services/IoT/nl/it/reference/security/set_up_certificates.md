---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-02"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configurazione dei certificati
{: #set_up_certificates}

I certificati sono utilizzati per l'autenticazione del dispositivo o per sostituire il certificato del server {{site.data.keyword.iot_full}} predefinito per la messaggistica MQTT. A ogni dispositivo che non dispone di certificati firmati validi viene negato l'accesso e non può comunicare con il server.

Per configurare i certificati e l'accesso al server per i dispositivi, l'operatore di sistema registra i certificati con autorità di certificazione (CA) e i certificati del server di messaggistica nella piattaforma {{site.data.keyword.iot_short_notm}}.

## Requisiti del certificato
{: #cert_reqs}

### Certificati CA
I certificati CA consentono all'organizzazione di riconoscere i certificati client sui dispositivi come attendibili in modo che i dispositivi possano collegarsi al server. Un certificato CA può utilizzare un elenco di revoche di certificati (CRL). Il CRL deve essere raggiungibile nel momento in cui il CA viene aggiunto alla piattaforma o il certificato CA sarà rifiutato.

Se aggiungi un certificato CA o sostituisci il certificato del server di messaggistica, tutti i dispositivi devono collegarsi utilizzando un client MQ che supporta Server Name Indication (SNI) in modo che tale server possa utilizzare i CA appropriati per l'autenticazione del dispositivo.

Se aggiungi un certificato CA ma non hai il componente aggiuntivo Gestione della sicurezza e del rischio abilitato, tutti i dispositivi si collegano con la politica di connessione TLS con autenticazione certificato client e token. Se hai il componente aggiuntivo Gestione della sicurezza e del rischio abilitato, puoi configurare diverse politiche di connessione. Per informazioni su come configurare le politiche di connessione, consulta [Configurazione delle politiche di sicurezza](set_up_policies.html).

### Certificati dispositivo e client
Rimangono sul dispositivo i soli certificati client o dispositivo e non sono caricati nella piattaforma. Il certificato di firma CA utilizzato per firmare tutti i certificati del dispositivo è l'unico certificato caricato nella piattaforma. Se stai utilizzando i certificati server autofirmati, devi caricare il CA intermedio e root (ca.pem) utilizzato per firmare il certificato client (cert.pem). 

L'unico certificato del dispositivo che firmi con il certificato CA deve avere l'ID dispositivo inserito come CN (Common Name) o SubjectAltName nel certificato. Per il campo *CN*, il formato è 'CN=d:devtype:devid'. Per il campo SubjectAltName, il formato è 'SubjectAltName=email:d:devtype:devid' dove 'devtype' è il tipo di dispositivo e 'devid' è l'ID client del dispositivo.

## Registrazione dei certificati con autorità di certificazione (CA) per l'autenticazione del dispositivo
{: #reg_ca_cert}

1. Accedi a {{site.data.keyword.iot_short_notm}} e passa a **General Settings**.
2. Nella sezione **Security**, in **CA Certificates**, fai clic su **Add Certificate**.
3. Individua e seleziona un file del certificato da caricare o trascina e rilascia un file nella finestra **Add Certificate**. Il file può avere solo un certificato al suo interno e le date del certificato devono essere valide. Sono accettati solo i certificati nel formato .pem o. der. Puoi visualizzare in anteprima le informazioni del certificato nel file selezionato.
4. Immetti una descrizione del file del certificato. 
5. Conferma che il file corretto sia selezionato e fai clic su **Save**. Il certificato selezionato viene elencato nella tabella ed è attivo per impostazione predefinita. 

## Registrazione dei certificati del server di messaggistica
{: #reg_msg_cert}

Viene fornito un certificato server predefinito con la piattaforma. Puoi utilizzare il certificato predefinito o caricarne uno dalla tua organizzazione. Se ancora non hai un certificato da utilizzare, puoi creare una richiesta per un nuovo certificato. Dopo aver ricevuto il nuovo certificato, devi firmarlo e ricaricarlo nella piattaforma.

Per utilizzare il certificato predefinito o un altro certificato che è già stato caricato, selezionare il certificato che desideri utilizzare dall'elenco a discesa **Default messaging server certificate** nella tabella in **Messaging Server Certificates**. 

**Nota:** le pagine del dashboard della piattaforma possono eseguire connessioni interne al server di messaggistica per richiamare le informazioni sul dispositivo. Quando si configurano i certificati server autofirmati per un'organizzazione, gli utenti dashboard devono aggiungere il certificato server come un certificato attendibile nei loro browser per evitare problemi di connessione perché i browser, per impostazione predefinita, non riconosceranno il server di messaggistica come un server attendibile.

### Caricamento di un certificato dalla tua organizzazione 
{: #upload_cert}
1. Nella sezione **Security** di **General Settings**, in **Messaging Server Certificates**, fai clic su **Add Certificate**.
2. Individua e seleziona un file del certificato da caricare o trascina e rilascia un file nella finestra **Add Certificate**.
3. Individua e seleziona un file della chiave privata da caricare o trascina e rilascia un file nella finestra **Add Certificate**.  
4. Immetti la passphrase della chiave privata se è stata crittografata con una passphrase.
5. Conferma che il file corretto sia selezionato e fai clic su **Save**.
6. Seleziona il certificato appena caricato dall'elenco a discesa **Default messaging server certificate**. Il certificato selezionato viene elencato nella tabella come un certificato attivo. 

### Richiesta di un nuovo certificato
{: #request_cert}

Se desideri utilizzare un nuovo certificato del server di messaggistica, puoi generare una richiesta firma certificato (CSR) per richiedere un nuovo certificato. 

 1. Nella sezione **Security Management** di **General Settings**, in **Messaging Server Certificates**, fai clic su **Generate CSR**.
 2. Immetti i dettagli per effettuare una CSR per il tuo server e fai clic su **Generate**. La CSR viene visualizzata nella tabella.
 3. Scarica la richiesta e inviala all'autorità del certificato per la firma.
 4. Dopo aver ottenuto un certificato, puoi caricarlo seguendo le istruzioni in [Caricamento di un certificato dalla tua organizzazione](#upload_cert). Dopo aver caricato il certificato, la CSR nella tabella viene sostituita dal certificato caricato.
