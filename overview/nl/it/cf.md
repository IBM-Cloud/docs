---


copyright:
  years: 2016, 2017
lastupdated: "2017-03-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Come funziona Bluemix Cloud Foundry
{: #howwork}

Quando distribuisci un'applicazione a {{site.data.keyword.Bluemix_notm}} Cloud Foundry, devi configurare {{site.data.keyword.Bluemix_notm}} con una quantità sufficiente di informazioni per supportare l'applicazione.

* Per un'applicazione mobile, {{site.data.keyword.Bluemix_notm}} contiene una risorsa che rappresenta il back-end dell'applicazione mobile, ad esempio i servizi utilizzati dall'applicazione mobile per comunicare con un server.
* Per un'applicazione web, devi assicurarti che le informazioni sul runtime e sul framework siano comunicate a {{site.data.keyword.Bluemix_notm}}, in modo che {{site.data.keyword.Bluemix_notm}} possa configurare l'ambiente di esecuzione appropriato per eseguire l'applicazione.

Ogni ambiente di esecuzione, compresi sia quello mobile sia quello web, è isolato dall'ambiente di esecuzione di altre applicazioni. Gli ambienti di esecuzione sono isolati anche se tali applicazioni si trovano sulla stessa macchina fisica. La seguente figura mostra il flusso di base del modo in cui {{site.data.keyword.Bluemix_notm}} Cloud Foundry gestisce la distribuzione di applicazioni:

![Distribuzione di un'applicazione](images/deploy.png)

Figura 3. Distribuzione di un'applicazione

Quando crei un'applicazione e la distribuisci a {{site.data.keyword.Bluemix_notm}} Cloud Foundry, l'ambiente {{site.data.keyword.Bluemix_notm}} determina un server virtuale appropriato a cui inviare l'applicazione o le risorse da essa rappresentate. Per un'applicazione mobile, su {{site.data.keyword.Bluemix_notm}} viene creata una proiezione di back-end mobile. Tutto il codice per l'applicazione mobile in esecuzione nel cloud alla fine viene eseguito nell'ambiente {{site.data.keyword.Bluemix_notm}}. Per un'applicazione web, il codice in esecuzione nel cloud è l'applicazione stessa che lo sviluppatore distribuisce a {{site.data.keyword.Bluemix_notm}}. La determinazione del server virtuale si basa su diversi fattori, tra cui:

* Il carico già sulla macchina
* I runtime o i framework supportati da tale server virtuale.

Una volta selezionato un server virtuale, su ciascun server virtuale un gestore dell'applicazione installa il framework e il runtime appropriati per l'applicazione. L'applicazione può quindi essere distribuita in tale framework. Una volta completata la distribuzione, le risorse dell'applicazione vengono avviate.

La seguente figura mostra la struttura di un server virtuale, nota anche come DEA (Droplet Execution Agent), su cui sono distribuite più applicazioni:

![Progetto di un server virtuale](images/container.png)

Figura 4. Progetto di un server virtuale

In ciascun server virtuale, un gestore dell'applicazione comunica con il resto dell'infrastruttura {{site.data.keyword.Bluemix_notm}} e gestisce le applicazioni distribuite a tale server. Ogni server virtuale dispone di contenitori per separare e proteggere le applicazioni. In ogni contenitore, {{site.data.keyword.Bluemix_notm}} installa il framework e il runtime appropriati richiesti per ogni applicazione.

Quando l'applicazione viene distribuita, se ha un'interfaccia web (come per un'applicazione web Java), o altri servizi basati su REST (come i servizi mobili presentati pubblicamente all'applicazione mobile), gli utenti dell'applicazione possono comunicare con essa utilizzando normali richieste HTTP.

![Chiamata di un'applicazione {{site.data.keyword.Bluemix_notm}}](images/execute.png)

Figura 5. Richiamo di un'applicazione {{site.data.keyword.Bluemix_notm}}

A ogni applicazione può essere associato uno o più URL, ma tutti devono puntare all'endpoint {{site.data.keyword.Bluemix_notm}}. Quando viene ricevuta una richiesta, {{site.data.keyword.Bluemix_notm}} la esamina, determina qual è l'applicazione a cui è destinata, quindi seleziona un'istanza dell'applicazione per ricevere la richiesta.


## Architettura {{site.data.keyword.Bluemix_notm}} Cloud Foundry
{: #architecture}

In generale, non devi preoccuparti dei livelli di infrastruttura e sistema operativo durante l'esecuzione delle applicazioni su {{site.data.keyword.Bluemix_notm}} in Cloud Foundry. I livelli
quali, ad esempio, i file system root e i componenti middleware vengono astratti e pertanto puoi concentrarti sul
codice della tua applicazione. Tuttavia, se hai bisogno di specifiche su dove è in esecuzione
la tua applicazione, puoi consultare ulteriori informazioni su questi livelli.

Per i dettagli, vedi [Visualizzazione dei livelli dell'infrastruttura {{site.data.keyword.Bluemix_notm}}](/docs/manageapps/infra.html#viewinfra).

In qualità di sviluppatore, puoi interagire con l'infrastruttura {{site.data.keyword.Bluemix_notm}} utilizzando un'interfaccia utente basata sul browser. Puoi anche utilizzare un'interfaccia riga di comando Cloud Foundry, denominata cf, per distribuire applicazioni
web.

I client, che possono essere applicazioni mobili, applicazioni che vengono eseguite esternamente, applicazioni basate su {{site.data.keyword.Bluemix_notm}} o sviluppatori che stanno utilizzando dei browser, interagiscono con le applicazioni ospitate da {{site.data.keyword.Bluemix_notm}}. I client utilizzano API REST o HTTP per instradare le richieste tramite {{site.data.keyword.Bluemix_notm}} a una delle istanze dell'applicazione o ai servizi compositi.

La seguente figura mostra l'architettura {{site.data.keyword.Bluemix_notm}} Cloud Foundry di alto livello.

![Architettura di {{site.data.keyword.Bluemix_notm}}](images/arch.png)

Figure 1. Architettura {{site.data.keyword.Bluemix_notm}} Cloud Foundry

Puoi distribuire le
tue applicazioni a regioni {{site.data.keyword.Bluemix_notm}} differenti, per
considerazioni di sicurezza o di latenza. Puoi scegliere di effettuare la distribuzione su una singola regione o tra più regioni.


![Sviluppo di applicazioni a più regioni](images/multi-region.png)

Figura 2. Distribuzione di applicazioni a più regioni


## Regioni
{: #ov_intro_reg}

Una regione {{site.data.keyword.Bluemix_notm}} è un territorio geografico definito a cui puoi distribuire le applicazioni. Puoi creare applicazioni e istanze di servizio in regioni differenti con la stessa infrastruttura {{site.data.keyword.Bluemix_notm}} per la gestione di applicazioni e la stessa vista dei dettagli di utilizzo per la fatturazione. Puoi selezionare la regione più vicina ai tuoi clienti e distribuire le tue applicazioni a tale regione per ottenere una bassa latenza di applicazione. Puoi anche selezionare la regione dove desideri conservare i dati delle applicazioni per far fronte ai problemi di sicurezza. Quando crei applicazioni in più regioni, se una regione non è più disponibile, le applicazioni che si trovano nelle altre regioni continuano a essere eseguite. La disponibilità di risorse è la stessa per ogni regione che usi.

Se utilizzi l'interfaccia utente {{site.data.keyword.Bluemix_notm}}, puoi passare a una regione differente per lavorare con gli spazi in tale regione. Fai clic sul link delle preferenze dell'account utente, espandi il selettore **Regione** e seleziona la regione richiesta dall'elenco.

Se utilizzi l'interfaccia riga di comando cf, per connetterti alla regione {{site.data.keyword.Bluemix_notm}} con cui vuoi lavorare, utilizza il comando cf api e specifica l'endpoint API della regione. Ad esempio, immetti il seguente comando per stabilire una connessione alla regione {{site.data.keyword.Bluemix_notm}} Europa Regno Unito:

```
cf api https://api.eu-gb.{{site.data.keyword.Bluemix_notm}}.net
```

A
ciascuna regione viene assegnato un prefisso univoco. {{site.data.keyword.Bluemix_notm}} fornisce le
seguenti regioni e i seguenti prefissi di regione.

<!-- PRODUCTION ONLY: Ensure that URLs are production URLs, not stage1-->

| **Nome della regione** | **Ubicazione geografica** | **Prefisso della regione** | **Endpoint API cf** | **Console Interfaccia grafica** |
|-----------------|-------------------------|-------------------|---------------------|----------------|
| Regione Stati Uniti Sud | Dallas, Stati Uniti | ng | api.ng.bluemix.net | console.ng.bluemix.net |
| Regione Regno Unito | Londra, Inghilterra | eu-gb | api.eu-gb.bluemix.net | console.eu-gb.bluemix.net |
| Regione Sydney | Sydney, Australia | au-syd | api.au-syd.bluemix.net | console.au-syd.bluemix.net |
| Regione Germania | Francoforte, Germania | eu-de | api.eu-de.bluemix.net | console.eu-de.bluemix.net |
{: caption="Tabella 1. Elenco regioni Bluemix" caption-side="top"}



## Resilienza {{site.data.keyword.Bluemix_notm}}
{: #resiliency}

{{site.data.keyword.Bluemix_notm}} è progettato per ospitare applicazioni e risorse dell'applicazione resilienti con capacità di scalabilità per rispondere alle tue esigenze e in grado di rimanere altamente disponibili e di riprendere rapidamente la normale operatività dopo eventuali problemi. {{site.data.keyword.Bluemix_notm}} separa i componenti che tracciano lo stato delle interazioni (con stato) dai componenti che invece non lo fanno (senza stato). Questa separazione consente a {{site.data.keyword.Bluemix_notm}} di spostare la flessibilità delle applicazioni come necessario per ottenere scalabilità e resilienza.

Puoi avere una o più istanze in esecuzione per la tua applicazione. Per più istanze di una singola applicazione, l'applicazione viene caricata solo una volta. Tuttavia, {{site.data.keyword.Bluemix_notm}} distribuisce il numero di istanze dell'applicazione richiesto e le distribuisce sul maggior numero possibile di server virtuali.

Devi salvare tutti i dati persistenti in un archivio dati con stato che sia esterno alla tua applicazione, come ad esempio su uno dei servizi di archivio dati forniti da {{site.data.keyword.Bluemix_notm}}. Poiché i dati contenuti nella cache in memoria o su un disco potrebbero non essere disponibili anche dopo un riavvio, puoi utilizzare lo spazio di memoria o il file system di una singola istanza di {{site.data.keyword.Bluemix_notm}} come una breve cache per singola transazione. Con una configurazione a istanza singola, la richiesta alla tua applicazione potrebbe essere interrotta a causa della natura senza stato di {{site.data.keyword.Bluemix_notm}}. Una procedura consigliata consiste nell'utilizzare almeno tre istanze per ciascuna applicazione per garantirne la disponibilità.

Tutta l'infrastruttura {{site.data.keyword.Bluemix_notm}}, i componenti Cloud Foundry e i componenti di gestione specifici per {{site.data.keyword.IBM_notm}} sono altamente disponibili. Per bilanciare il carico vengono utilizzate più istanze dell'infrastruttura.

## Integrazione con i system of record
{: #sor}

{{site.data.keyword.Bluemix_notm}} può aiutare gli sviluppatori connettendo due ampie categorie di sistemi in un ambiente cloud:

* I *system of record* includono le applicazioni e i database che memorizzano i record di business e automatizzano i processi standardizzati.
* I
*system of engagement* sono funzionalità che espandono l'utilità dei system of record e li rendono più interessanti per gli utenti.

Integrando un system of record con l'applicazione che crei in {{site.data.keyword.Bluemix_notm}}, puoi eseguire queste azioni:

 * Abilitare delle comunicazioni protette tra l'applicazione e il database di back-end scaricando e installando in loco un connettore sicuro.
 * Richiamare un database in modo sicuro.
 * Creare delle API dai flussi di integrazione con i database e i sistemi di back-end, come ad esempio un sistema di gestione delle relazioni con la clientela.
 * Presentare solo gli schemi e le tabelle che desideri siano presentati all'applicazione.
 * In qualità di gestore organizzazione di {{site.data.keyword.Bluemix_notm}},
pubblicare una API come un servizio privato visibile solo ai membri della tua organizzazione.

Per integrare un system of record con le applicazioni che hai creato in {{site.data.keyword.Bluemix_notm}}, utilizza il servizio Cloud Integration. Utilizzando il servizio Cloud Integration, puoi creare una API Cloud Integration e pubblicarla come un servizio privato per la tua organizzazione.

<dl>
<dt>API Cloud Integration</dt>
    <dd>Una API Cloud Integration fornisce un accesso protetto ai system of record che si trovano dietro un firewall tramite le API web. Quando
crei la API Cloud Integration, scegli la risorsa a cui si desideri accedere tramite la API web, specifichi le operazioni consentite e includi SDK ed esempi per accedere alla API. Per ulteriori informazioni su come creare una API Cloud Integration, consulta [Introduzione a Cloud Integration](/docs/services/CloudIntegration/CldInt_GetStart.html).</dd>
<dt>Servizio privato</dt>
    <dd>Un servizio privato consiste in una API Cloud Integration, degli SDK e delle politiche di titolarità. Il servizio privato può inoltre contenere della documentazione o altri elementi dal provider di servizi. Solo il gestore dell'organizzazione può pubblicare una API Cloud Integration come un servizio privato. Per visualizzare i servizi privati a tua disposizione, seleziona la casella di spunta Privato nel catalogo {{site.data.keyword.Bluemix_notm}}. Puoi selezionare un servizio privato ed eseguire il bind a un'applicazione senza stabilire una connessione al servizio Cloud Integration. Puoi eseguire il bind di servizi privati alla tua applicazione nello stesso modo che adotti per altri servizi {{site.data.keyword.Bluemix_notm}}. Per informazioni su come pubblicare una API come un servizio privato, vedi Pubblicazione di una API come un servizio privato.</dd>
</dl>

### Scenario: creazione di una completa applicazione mobile per stabilire una connessione al tuo system of record
{: #scenario}

{{site.data.keyword.Bluemix_notm}} fornisce una piattaforma dove puoi integrare l'applicazione mobile, i servizi cloud e i system of record aziendali per fornire un'applicazione che interagisce con i tuoi dati in loco.

Ad esempio, puoi
creare un'applicazione mobile per interagire con il tuo sistema di gestione delle relazioni con la clientela installato in loco dietro un firewall. Puoi richiamare il system of record in modo sicuro e avvalerti dei servizi mobili in {{site.data.keyword.Bluemix_notm}} in modo da poter creare un'applicazione mobile completa.

Innanzitutto, il tuo sviluppatore dell'integrazione crea l'applicazione di back-end mobile in {{site.data.keyword.Bluemix_notm}}. Viene usato il contenitore tipo Mobile Cloud che utilizza il più noto runtime Node.js.

Quindi, utilizzando il servizio Cloud Integration nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}, espone un'API tramite un connettore sicuro. Il tuo sviluppatore dell'integrazione scarica il
connettore sicuro e lo installa in loco per abilitare le comunicazioni protette tra la sua API e il database. Dopo che ha creato l'endpoint database, consulta tutti gli schemi ed estrae le tabelle che intende esporre come API all'applicazione.

Lo sviluppatore dell'integrazione aggiunge il servizio Push per offrire notifiche mobili agli utenti interessati. Aggiunge anche un servizio di business partner per generare un tweet quando viene creato un nuovo record cliente con una API Twitter.

Quindi, in qualità di sviluppatore dell'applicazione,
puoi effettuare il login a {{site.data.keyword.Bluemix_notm}},
scaricare il toolkit di sviluppo Android e sviluppare del codice che richiama le API create
dallo sviluppatore dell'integrazione. Puoi sviluppare un'applicazione mobile che consente agli utenti di immettere le loro informazioni sul loro dispositivo mobile. L'applicazione mobile crea quindi un record cliente nel sistema di gestione dei clienti. Quando viene creato il record, l'applicazione esegue il push di una notifica a un dispositivo mobile e avvia un tweet relativo al nuovo record.
