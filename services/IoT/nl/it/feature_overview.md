---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-12"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Panoramica funzione {{site.data.keyword.iot_short_notm}}
{: #feature_overview}

{{site.data.keyword.iot_full}} si basa sulle seguenti aree chiave:

  1. Connect - Connessione dei dispositivi e sviluppo delle applicazioni
  2. Information Management - Archiviare e controllare i dati del dispositivo e integrare il tuo {{site.data.keyword.iot_short_notm}} con altri servizi.
  3. Analytics - Visualizzare i dati del dispositivo in tempo reale utilizzando il dashboard {{site.data.keyword.iot_short_notm}}.
  4. Risk Management - Configurare l'architettura e la connettività sicure con il controllo dell'accesso per gli utenti e le applicazioni.

## Collegamento
{: #connect}

{{site.data.keyword.iot_short_notm}} Connect è il punto di partenza per qualsiasi servizio {{site.data.keyword.iot_short_notm}}. La connessione dei dispositivi, la creazione delle applicazioni, il controllo dei tuoi dispositivi e l'interazione con i servizi di terze parti sono tutti i disponibili in {{site.data.keyword.iot_short_notm}} Connect.

### Dispositivi gateway

Utilizzando un gateway, puoi collegare dispositivi a {{site.data.keyword.iot_short_notm}} che altrimenti non possono collegarsi a internet. I gateway hanno tutte le funzioni di un dispositivo ma possono inoltre pubblicare e sottoscrivere al posto dei dispositivi collegati ad essi. I dispositivi gateway consentono il raggruppamento dei sensori che non possono collegarsi a internet per connettersi a {{site.data.keyword.iot_short_notm}} inviando i loro dati a un gateway. Per ulteriori informazioni, consulta [developing for gateways](https://console.ng.bluemix.net/docs/services/IoT/gateways/gw_dev_index.html).

### Gestione del dispositivo

Le funzioni di gestione del dispositivo sono fornite tramite un'API di gestione del dispositivo e un agent di gestione del dispositivo che è installata sui dispositivi. I dispositivi possono eseguire le azioni di gestione del dispositivo, che possono essere attivate tramite il dashboard {{site.data.keyword.iot_short_notm}} o l'API di gestione del dispositivo. Le azioni di gestione del dispositivo ti permettono di riavviare, scaricare e installare gli aggiornamenti firmware e reimpostare i dispositivi alle impostazioni predefinite. La gestione del dispositivo può inoltre essere estesa per includere le azioni di gestione del dispositivo personalizzate. Per ulteriori informazioni, consulta la [device management documentation](https://console.ng.bluemix.net/docs/services/IoT/devices/device_mgmt/index.html).

### Estensioni e integrazioni del servizio

Le estensioni e le integrazioni del servizio permettono ai servizi esterni e alle estensioni definite dall'utente dei servizi core di essere aggiunti a un'istanza di {{site.data.keyword.iot_short_notm}}. I servizi esterni che possono essere integrati con {{site.data.keyword.iot_short_notm}} includono i servizi di rilevamento meteo della Weather Company, i dati SIM Jasper e {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}. Per ulteriori informazioni sulle estensioni e le integrazioni dei servizi di terze parti, consulta [integrazione di servizi esterni](https://console.ng.bluemix.net/docs/services/IoT/reference/extensions/index.html).

---

## Information Management
{: #information_management}

{{site.data.keyword.iot_short_notm}} Information Management controlla i dati inviati dai dispositivi dopo la ricezione nel tuo servizio {{site.data.keyword.iot_short_notm}}. La gestione delle informazioni include la trasformazione e l'archivio dei dati.

### Ultima cache evento del dispositivo

Utilizzando l'API Ultima cache evento {{site.data.keyword.iot_short_notm}}, puoi richiamare l'ultimo evento che è stato inviato a un dispositivo. Funziona sia se il dispositivo è online che offline e ti consente di richiamare lo stato del dispositivo indipendentemente dalla sua ubicazione fisica o stato di utilizzo. Gli ultimi dati evento possono essere richiamati per ogni evento specifico verificatosi negli ultimi 365 giorni.

### Archivio dati evento del dispositivo

I dati evento del dispositivo dal servizio {{site.data.keyword.iot_short_notm}} possono essere archiviati per un utilizzo successivo. L'archivio dati è un primo passo fondamentale per l'esecuzione di analisi approfondite per ottenere informazioni approfondite da tali dati.  Ad esempio, puoi tracciare le modifiche per periodi di tempo più lunghi e archiviare le serie di dati da utilizzare con strumenti di analisi più potenti, incluso l'utilizzo con le API Watson e il calcolo cognitivo. Per ulteriori informazioni, consulta [connecting a {{site.data.keyword.cloudant_short_notm}} historian service](https://console.ng.bluemix.net/docs/services/IoT/cloudant_connector.html) o [connecting a {{site.data.keyword.messagehub}} historian service](https://console.ng.bluemix.net/docs/services/IoT/message_hub.html).

---

## Analytics
{: #analytics}

### Visualizzare i dati del dispositivo in tempo reale

Puoi visualizzare i dati del dispositivo in tempo reale utilizzando le schede del dashboard. Le schede del dashboard monitorano e visualizzano i dati del dispositivo in tempo reale, il che ti consente di tenere traccia dei dispositivi chiave e dei dati del dispositivo. Queste visualizzazioni vengono mostrate nel dashboard {{site.data.keyword.iot_short_notm}} principale per fornirti un rapido accesso al contesto e allo stato dei dati del dispositivo in tempo reale. Per ulteriori informazioni, consulta [visualizzazione dei dati in tempo reale](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html).

### Analisi cloud e edge

Utilizzando le analisi cloud {{site.data.keyword.iot_short_notm}}, specifichi le condizioni della regola basate sui dati del dispositivo in tempo reale e che attivano gli avvisi e le azioni facoltative quando incontrate. Ad esempio, puoi creare una regola per assicurarti che quando viene eliminato un dispositivo o quando aumenta la temperatura del dispositivo, venga inviato un avviso al dashboard in un dispositivo dell'utente e che sia inviata una email all'amministratore. Per ulteriori informazioni, consulta la [cloud analytics documentation](https://console.ng.bluemix.net/docs/services/IoT/cloud_analytics.html).

Con le analisi edge, puoi spostare il processo di attivazione della regola di analisi dal cloud al gateway abilitato per l'analisi edge che riduce drasticamente la quantità di traffico dati del dispositivo nel cloud eseguendo l'elaborazione delle analisi vicino al dispositivo. Per ulteriori informazioni, consulta la [edge analytics documentation](https://console.ng.bluemix.net/docs/services/IoT/edge_analytics.html).

---

## Risk Management
{: #risk_management}

### Architettura e connettività sicure

L'architettura di {{site.data.keyword.iot_short_notm}} è progetta per evitare che i dispositivi siano impersonati da altri dispositivi, il che conserva l'integrità dei tuoi dati del dispositivo. I dispositivi si collegano a {{site.data.keyword.iot_short_notm}} utilizzando una combinazione di ID client e token di autenticazione, che solo tu conosci. Una volta che i dispositivi sono stati registrati o sono state generate le chiavi API, il token di autenticazione viene distribuito in modo casuale per conservare la sicurezza delle tue credenziali.

Il componente aggiuntivo di gestione della sicurezza e del rischio ti consente di migliorare la sicurezza {{site.data.keyword.iot_short_notm}} per assicurarti che tutti i punti di connessione tra il server e i dispositivi siano autenticati con le credenziali verificate. Con questo componente aggiuntivo, vengono utilizzati i certificati e l'autenticazione TLS (transport layer security) invece dell'utilizzo di {{site.data.keyword.iot_short_notm}} di token e ID utente. Durante la comunicazione tra i dispositivi e il server, a tutti i dispositivi che non dispongono di certificati validi con l'accesso al server, come configurato nel componente aggiuntivo di gestione della sicurezza e del rischio, non viene consentito l'accesso, anche se utilizzano password e ID utente validi.

---
