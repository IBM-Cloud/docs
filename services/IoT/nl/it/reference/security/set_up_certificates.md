---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configurazione dei certificati
{: #set_up_certificates.md}
Ultimo aggiornamento: 15 novembre 2016
{: .last-updated}

Utilizzando il componente di gestione della sicurezza e del rischio, i certificati sono utilizzati per l'autenticazione del dispositivo o per sostituire il certificato del server IBM Watson IoT Platform predefinito per la messaggistica MQTT. A ogni dispositivo che non dispone di certificati firmati validi viene negato l'accesso e non può comunicare con il server.

Per configurare i certificati e l'accesso al server per i dispositivi, l'operatore di sistema registra i certificati con autorità di certificazione (CA) e i certificati del server di messaggistica nella piattaforma Watson IoT. 

## Requisiti del certificato

Il certificato che registri deve avere un ID dispositivo inserito come il CN (Common Name) o il SubjectAltName nel certificato. Per il campo *CN*, il formato è CN=d:devtype:devid. Per il campo SubjectAltName, il formato è: SubjectAltName=d:devtype:devid dove devtype è il tipo di dispositivo e devid è l'ID client del dispositivo.

L'utilizzo di un elenco di revoche di certificati (CRL), per indicare a quali dispositivi non è più concessa la connessione, non è supportato nella release beta.

Se aggiungi i certificati CA o sostituisci il certificato del server di messaggistica, tutti i dispositivi devono collegarsi utilizzando un client MQ che supporta Server Name Indication (SNI). Con l'architettura a più tenant, SNI indica al server MQTT quali certificati devono essere utilizzati per ogni connessione organizzazione/tenant.

##Registrazione dei certificati con autorità di certificazione (CA) per l'autenticazione del dispositivo

1. Accedi alla piattaforma Watson IoT e passa a **General Settings**.
2. Nella sezione **Risk Management**, in **CA Certificates**, fai clic su **Add Certificate**.
3. Individua e seleziona un file del certificato da caricare o trascina e rilascia un file nella finestra **Add Certificate**. Il file può avere solo un certificato al suo interno e le date del certificato devono essere valide. I file con le estensioni .pem, .cer, .cert, or .crt sono accettati. Puoi visualizzare in anteprima le informazioni del certificato nel file selezionato.
4. Immetti una descrizione del file del certificato.
5. Conferma che il file corretto sia selezionato e fai clic su **Save**. Il certificato selezionato viene elencato nella tabella ed è attivo per impostazione predefinita. 

## Registrazione dei certificati del server di messaggistica

I certificati del server predefiniti sono forniti con la piattaforma. Puoi utilizzare uno dei certificati predefiniti o caricarne uno dalla tua organizzazione. Se ancora non hai un certificato da utilizzare, puoi creare una richiesta per un nuovo certificato. Dopo aver ricevuto il nuovo certificato, devi firmarlo e ricaricarlo nella piattaforma.

Per utilizzare uno dei certificati predefiniti o un altro certificato che è già stato caricato, selezionare il certificato che desideri utilizzare dall'elenco a discesa **Default messaging server certificate** nella tabella in **Messaging Server Certificates**.

### <a name="upload"> </a> Caricamento di un certificato dalla tua organizzazione

1. Nella sezione **Risk Management** di **General Settings**, in **Messaging Server Certificates**, fai clic su **Add Certificate**.
2. Individua e seleziona un file del certificato da caricare o trascina e rilascia un file nella finestra **Add Certificate**. 
3. Individua e seleziona un file della chiave privata da caricare o trascina e rilascia un file nella finestra **Add Certificate**.   
4. Immetti la passphrase della chiave privata se è stata crittografata con una passphrase.
5. Conferma che il file corretto sia selezionato e fai clic su **Save**. 
6. Seleziona il certificato appena caricato dall'elenco a discesa **Default messaging server certificate**. Il certificato selezionato viene elencato nella tabella come un certificato attivo.


### Richiesta di un nuovo certificato

 Se desideri utilizzare un nuovo certificato del server di messaggistica, puoi generare una richiesta firma certificato (CSR) per richiedere un nuovo certificato.

 1. Nella sezione **Risk Management** di **General Settings**, in **Messaging Server Certificates**, fai clic su **Generate CSR**.
 2. Immetti i dettagli per effettuare una richiesta firma certificato (CSR) per il tuo server e fai clic su **Generate**. La CSR viene visualizzata nella tabella.
 3. Scarica la richiesta e inviala all'autorità del certificato per la firma.
 4. Dopo aver ottenuto un certificato, puoi caricarlo seguendo le istruzioni in Caricamento di un certificato dalla tua organizzazione. Dopo aver caricato il certificato, la CSR nella tabella viene sostituita dal certificato caricato.
