---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Panoramica funzione {{site.data.keyword.iot_short_notm}}
{: #feature_overview}

Ultimo aggiornamento: 29 giugno 2016
{: .last-updated}

{{site.data.keyword.iot_full}} si basa sulle seguenti aree chiave:

  1. Connect - Connessione dei dispositivi e sviluppo delle applicazioni
  2. Information Management - Archiviare e controllare i dati del dispositivo e integrare il tuo {{site.data.keyword.iot_short_notm}} con altri servizi.
  3. Analytics - Visualizzare i dati del dispositivo in tempo reale utilizzando il dashboard {{site.data.keyword.iot_short_notm}}.
  4. Risk Management - Configurare l'architettura e la connettività sicure con il controllo dell'accesso per gli utenti e le applicazioni.

## Connect
{: #connect}

{{site.data.keyword.iot_short_notm}} Connect è il punto di partenza per qualsiasi servizio {{site.data.keyword.iot_short_notm}}. La connessione dei dispositivi, la creazione delle applicazioni, il controllo dei tuoi dispositivi e l'interazione con i servizi di terze parti sono tutti i disponibili in {{site.data.keyword.iot_short_notm}} Connect.

### Dispositivi gateway

Utilizzando un gateway, puoi collegare dispositivi a {{site.data.keyword.iot_short_notm}} che altrimenti non possono collegarsi a internet. I dispositivi gateway combinano la funzione di un dispositivo e di un'applicazione. I gateway possono ricevere i comandi e inviare i dati del dispositivo come un dispositivo, ma possono anche inviare i comandi ad altri dispositivi ad esso collegati come un'applicazione.

I dispositivi che non possono collegarsi direttamente a internet possono essere collegati a un dispositivo gateway e i loro dati possono essere inviati a un dispositivo gateway, il quale può inviarli al tuo servizio {{site.data.keyword.iot_short_notm}}.

### Gestione del dispositivo

Le funzioni di gestione del dispositivo sono fornite tramite la combinazione di un'API di gestione del dispositivo e un agent di gestione del dispositivo che è installata sui dispositivi. I dispositivi gestiti possono eseguire le azioni di gestione del dispositivo, che possono essere attivate tramite il dashboard {{site.data.keyword.iot_short_notm}}.

La gestione del dispositivo ti fornisce la possibilità di riavviare, scaricare e installare gli aggiornamenti firmware e reimpostare i dispositivi alle impostazioni predefinite in remoto, tutto tramite l'interfaccia utente {{site.data.keyword.iot_short_notm}}.

### Integrazioni di servizi di terze parti

L'integrazione di servizi di terze parti è integrata in {{site.data.keyword.iot_short_notm}}, incluso il supporto per i servizi di rilevamento meteo della Weather Company, che ti consente di trovare il meteo corrente in un'ubicazione del dispositivo.

---

## Information Management
{: #information_management}

{{site.data.keyword.iot_short_notm}} Information Management controlla i dati inviati dai dispositivi dopo la ricezione nel tuo servizio {{site.data.keyword.iot_short_notm}}. La gestione delle informazioni include la trasformazione e l'archivio dei dati.

### Ultima cache evento del dispositivo

Utilizzando l'API Ultima cache evento {{site.data.keyword.iot_short_notm}}, puoi richiamare l'ultimo evento che è stato inviato a un dispositivo. Funziona sia se il dispositivo è online che offline e ti consente di richiamare lo stato del dispositivo indipendentemente dalla sua ubicazione fisica o stato di utilizzo. Gli ultimi dati evento possono essere richiamati per ogni evento specifico verificatosi negli ultimi 365 giorni.

### Archivio dati evento del dispositivo

I dati evento del dispositivo dal servizio {{site.data.keyword.iot_short_notm}} possono essere archiviati per un utilizzo successivo. L'archivio dati è un primo passo fondamentale per l'esecuzione di analisi approfondite per ottenere informazioni approfondite da tali dati.  Ad esempio, puoi tracciare le modifiche per periodi di tempo più lunghi e archiviare le serie di dati da utilizzare con strumenti di analisi più potenti, incluso l'utilizzo con le API Watson e il calcolo cognitivo.

---

## Analytics
{: #analytics}

### Visualizzare i dati del dispositivo in tempo reale

Puoi visualizzare i dati del dispositivo in tempo reale utilizzando le schede del dashboard. Le schede del dashboard monitorano e visualizzano i dati del dispositivo in tempo reale, il che ti consente di tenere traccia dei dispositivi chiave e dei dati del dispositivo. Queste visualizzazioni vengono mostrate nel dashboard {{site.data.keyword.iot_short_notm}} principale per fornirti un rapido accesso al contesto e allo stato dei dati del dispositivo in tempo reale.

---

## Risk Management
{: #risk_management}

### Architettura e connettività sicure

L'architettura di {{site.data.keyword.iot_short_notm}} è progetta per evitare che i dispositivi siano impersonati da altri dispositivi, il che conserva l'integrità dei tuoi dati del dispositivo. I dispositivi si collegano a {{site.data.keyword.iot_short_notm}} utilizzando una combinazione di ID client e token di autenticazione, che solo tu conosci. Una volta che i dispositivi sono stati registrati o sono state generate le chiavi API, il token di autenticazione viene distribuito in modo casuale per conservare la sicurezza delle tue credenziali. La connettività tramite TLS v1.2 è completamente supportata.

---
