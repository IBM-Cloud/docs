---

 

copyright:

  years: 2014, 2017
  
lastupdated: "2017-01-11"

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Sicurezza {{site.data.keyword.Bluemix_notm}}
{: #security}

Sviluppata con procedure di progettazione sicura, la piattaforma {{site.data.keyword.Bluemix}} offre diversi livelli di controlli di sicurezza tra la rete e l'infrastruttura. {{site.data.keyword.Bluemix_notm}} fornisce un gruppo di servizi di sicurezza che possono essere utilizzati dagli sviluppatori di applicazioni per proteggere le proprie applicazioni mobili e Web. Questi elementi si combinano per rendere {{site.data.keyword.Bluemix_notm}} una piattaforma con scelte chiare per lo sviluppo di applicazioni sicure.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} garantisce disponibilità immediata della sicurezza aderendo alle politiche di sicurezza basate sulle procedure ottimali in IBM per i sistemi, la rete e la progettazione sicura. Tali politiche includono procedure quali, ad esempio, scansione del codice sorgente, scansione dinamica, modellazione dei rischi e test di penetrazione. {{site.data.keyword.Bluemix_notm}} segue il processo IBM PSIRT (Product Security Incident Response Team) per la gestione degli incidenti di sicurezza. Per i dettagli, consulta il sito [IBM Security Vulnerability Management (PSIRT) ![icona link esterno](../icons/launch-glyph.svg)](http://www-03.ibm.com/security/secure-engineering/process.html){: new_window}.

{{site.data.keyword.Bluemix_notm}} pubblico e dedicato utilizzano i servizi cloud {{site.data.keyword.BluSoftlayer}} IaaS (Infrastructure-as-a-Service) e si avvalgono appieno della sua architettura di sicurezza. Per le tue applicazioni e i tuoi dati, {{site.data.keyword.BluSoftlayer}} IaaS fornisce molteplici livelli di protezione che si sovrappongono tra di loro. Per {{site.data.keyword.Bluemix_notm}} locale, la sicurezza fisica è di tua competenza e fornisci l'infrastruttura ospitando {{site.data.keyword.Bluemix_notm}} locale nel tuo data center dietro un firewall aziendale. Inoltre, {{site.data.keyword.Bluemix_notm}} aggiunge funzionalità di sicurezza a livello PaaS (Platform as a Service) in diverse categorie: piattaforma, dati e applicazione.

## Sicurezza della piattaforma {{site.data.keyword.Bluemix_notm}}
{: #platform-security}

{{site.data.keyword.Bluemix_notm}} fornisce sicurezza funzionale, di infrastruttura, operativa e fisica (tramite {{site.data.keyword.BluSoftlayer}}) per la piattaforma di base. Tuttavia, {{site.data.keyword.Bluemix_notm}} locale è unico per il fatto che il cliente fornisce l'infrastruttura e il data center ed è di sua competenza la sicurezza fisica.

L'ambiente {{site.data.keyword.Bluemix_notm}} su {{site.data.keyword.BluSoftlayer}} è conforme ai più severi standard di sicurezza IT (information technology) IBM, che soddisfano o superano gli standard del settore. Tali standard includono: rete, crittografia di dati e controllo dell'accesso
 * ACL applicazione, autorizzazioni e test di penetrazione
 * Identificazione, autenticazione e autorizzazione
 * Protezione di informazioni e dati
 * Integrità e disponibilità dei servizi
 * Vulnerabilità e gestione delle correzioni
 * Rilevamento di attacchi Denial of Service e sistematici
 * Risposta agli incidenti di sicurezza

![Panoramica della sicurezza della piattaforma Bluemix](images/platform_sec.svg)

Figura 1. Panoramica della sicurezza della piattaforma {{site.data.keyword.Bluemix_notm}}

Con {{site.data.keyword.Bluemix_notm}} locale, ospiti {{site.data.keyword.Bluemix_notm}} dietro il tuo firewall aziendale e nel tuo data center. Pertanto, sei responsabile di determinati aspetti legati alla sicurezza. La seguente immagine illustra in modo dettagliato quali parti della sicurezza sono di competenza del cliente e quali sono invece gestite da IBM.

![Panoramica della sicurezza della piattaforma Bluemix locale](images/security_local_platform.svg)

Figura 2. Panoramica della sicurezza della piattaforma {{site.data.keyword.Bluemix_notm}} locale

IBM installa, esegue il monitoraggio in remoto e gestisce {{site.data.keyword.Bluemix_notm}} locale nel tuo data center attraverso Relay, una funzionalità di consegna inclusa in {{site.data.keyword.Bluemix_notm}} locale. Relay si connette in modo sicuro con i certificati specifici di ciascuna istanza {{site.data.keyword.Bluemix_notm}} locale. Per ulteriori informazioni su {{site.data.keyword.Bluemix_notm}} locale e Relay, vedi [Bluemix locale](/docs/local/index.html).

### Sicurezza funzionale

{{site.data.keyword.Bluemix_notm}} fornisce diverse capacità di sicurezza funzionali, tra cui l'autenticazione degli utenti, l'autorizzazione degli accessi, il controllo delle operazioni critiche e la protezione dei dati.

<dl>
<dt>Autenticazione</dt>
<dd>Gli sviluppatori di applicazioni sono autenticati presso {{site.data.keyword.Bluemix_notm}} utilizzando l'identità web IBM.

Per {{site.data.keyword.Bluemix_notm}} dedicato e locale, l'autenticazione tramite LDAP è supportata per impostazione predefinita. Altrimenti, su richiesta, per {{site.data.keyword.Bluemix_notm}} è possibile configurare l'autenticazione tramite l'identità Web IBM.
</dd>

<dt>Autorizzazione</dt>
<dd>{{site.data.keyword.Bluemix_notm}} utilizza i meccanismi Cloud Foundry per assicurare che ogni sviluppatore di applicazioni abbia accesso solo alle applicazioni e alle istanze di servizio da essi create. L'autorizzazione ai servizi {{site.data.keyword.Bluemix_notm}} è basata su OAuth. L'accesso a tutti gli endpoint interni della piattaforma {{site.data.keyword.Bluemix_notm}} è limitato per gli utenti esterni.</dd>

<dt>Controllo</dt>
<dd>I log di controllo vengono creati per tutti i tentativi di autenticazione riusciti e non riusciti degli sviluppatori di applicazioni. I log di controllo vengono creati anche per l'accesso privilegiato ai sistemi Linux che ospitano i contenitori dove vengono eseguite le applicazioni {{site.data.keyword.Bluemix_notm}}.</dd>

<dt>Protezione dei dati</dt>
<dd> Tutto il traffico {{site.data.keyword.Bluemix_notm}} transita per i prodotti IBM WebSphere® DataPower® SOA Appliances, che forniscono funzioni di proxy inverso, terminazione SSL e bilanciamento del carico Sono consentiti i seguenti metodi HTTP:
<ul>
<li>DELETE</li>
<li>GET</li>
<li>HEAD</li>
<li>OPTIONS</li>
<li>POST</li>
<li>PUT</li>
<li>TRACE</li>
</ul>
 Il timeout per inattività HTTP è fissato a 2 minuti.</dd>
<dd>Le seguenti intestazioni sono compilate da DataPower:
<dl>
<dt>$wsis</dt>
<dd>Impostala su true se la connessione lato client è protetta (HTTPS), altrimenti impostala su false.</dd>
<dt>$wssc</dt>
<dd>Impostala su uno dei seguenti schemi di connessione client: https, http, ws o wss.</dd>
<dt>$wssn</dt>
<dd>Impostala sul nome host inviato dal client.</dd>
<dt>$wssp</dt>
<dd>Impostala sulla porta server a cui si connette il client.</dd>
<dt>x-client-ip</dt>
<dd>Impostala sull'indirizzo IP del client.</dd>
<dt>x-forwarded-proto</dt>
<dd>Impostala su uno dei seguenti schemi di connessione client: https, http, ws o wss.</dd>
</dl>
</dd>

<dt>Procedure di sviluppo sicuro</dt>
<dd> Per {{site.data.keyword.Bluemix_notm}} pubblico e dedicato, vengono eseguite delle scansioni di vulnerabilità della sicurezza periodiche su diversi componenti di {{site.data.keyword.Bluemix_notm}} tramite IBM Security AppScan® Dynamic Analyzer. Vengono eseguite le procedure di modellazione dei rischi e test di penetrazione per individuare e risolvere eventuali possibili vulnerabilità per tutti i tipi di distribuzioni {{site.data.keyword.Bluemix_notm}}. Inoltre, gli sviluppatori di applicazioni possono utilizzare il servizio AppScan Dynamic Analyzer per proteggere le proprie applicazioni web distribuite su {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>

### Sicurezza dell'infrastruttura

{{site.data.keyword.Bluemix_notm}} si sviluppa su Cloud Foundry per fornire una solida base per l'esecuzione delle tue applicazioni. All'interno dell'architettura, vengono forniti diversi componenti per la sicurezza e l'isolamento. Inoltre, vengono implementate procedure di gestione delle modifiche e di backup e ripristino per garantire l'integrità e la disponibilità.

<dl>
<dt>Separazione degli ambienti</dt>
<dd> Per {{site.data.keyword.Bluemix_notm}} pubblico, gli ambienti di sviluppo e di produzione vengono separati tra loro per migliorare la stabilità e la sicurezza dell'applicazione.</dd>

<dt>Firewall</dt>
<dd> I firewall vengono implementati per limitare l'accesso alla rete {{site.data.keyword.Bluemix_notm}}. Per {{site.data.keyword.Bluemix_notm}} locale, il tuo firewall aziendale separa il resto della tua rete dalla tua istanza {{site.data.keyword.Bluemix_notm}}.</dd>

<dt>Protezione intrusioni</dt>
<dd>{{site.data.keyword.Bluemix_notm}} pubblico e dedicato abilitano la protezione dalle intrusioni per il rilevamento di minacce in modo che sia possibile risolverle. Le politiche di protezione intrusioni sono abilitate sui firewall.</dd>

<dt>Gestione del contenitore applicazioni sicuro</dt>
<dd>Ciascuna applicazione {{site.data.keyword.Bluemix_notm}} è isolata e viene eseguita nel suo proprio contenitore che ha specifici limiti di risorsa per processore, memoria e disco.</dd>

<dt>Protezione avanzata del sistema operativo</dt>
<dd>Gli amministratori IBM eseguono regolarmente la protezione avanzata del sistema operativo e della rete, utilizzando strumenti come IBM Endpoint Manager.</dd>
</dl>

### Sicurezza operativa

{{site.data.keyword.Bluemix_notm}} fornisce un solido ambiente di sicurezza operativa con i seguenti controlli.

<dl>
<dt>Scansione delle vulnerabilità</dt>
<dd>{{site.data.keyword.Bluemix_notm}} utilizza lo strumento di scansione delle vulnerabilità Tenable Network Security, Nessus, per rilevare eventuali problemi con le configurazioni di rete e host in modo da consentire di occuparsene.</dd>

<dt>Gestione delle correzioni automatizzate</dt>
<dd>Gli amministratori di {{site.data.keyword.Bluemix_notm}} garantiscono che le correzioni per i sistemi operativi vengano applicate con frequenza adeguata. Le correzioni automatizzate vengono abilitate utilizzando IBM Endpoint Manager.</dd>

<dt>Consolidamento e analisi dei log di controllo</dt>
<dd>{{site.data.keyword.Bluemix_notm}} utilizza gli strumenti IBMSecurity QRadar® per accorpare i log Linux per monitorare l'accesso privilegiato sui sistemi Linux. {{site.data.keyword.Bluemix_notm}} utilizza inoltre IBM QRadar SIEM (security information and event management) per monitorare i tentativi di accesso riusciti e non riusciti degli sviluppatori di applicazioni.</dd>

<dt>Gestione degli accessi utente</dt>
<dd>All'interno di {{site.data.keyword.Bluemix_notm}}, vengono seguite le linee guida di Separazione dei compiti per assegnare agli utenti dei privilegi di accesso granulari e per garantire che gli utenti dispongano soltanto dell'accesso richiesto per eseguire i propri lavori in base al principio del minimo privilegio.

Negli ambienti {{site.data.keyword.Bluemix_notm}} dedicato e locale, gli amministratori assegnati possono gestire i ruoli e le autorizzazioni per gli utenti {{site.data.keyword.Bluemix_notm}} nella propria organizzazione utilizzando la Console di gestione. Per i dettagli, vedi [Gestione di {{site.data.keyword.Bluemix_notm}}](/docs/admin/adminpublic.html#mng).
</dd>
</dl>

### Sicurezza fisica

{{site.data.keyword.Bluemix_notm}} pubblico e dedicato si avvalgono della topologia di rete all'interno di una rete di {{site.data.keyword.BluSoftlayer}} per la sicurezza della rete fisica. Questa architettura di rete all'interno di una rete garantisce che i sistemi siano pienamente accessibili solo al personale autorizzato. Per {{site.data.keyword.Bluemix_notm}} locale, è di tua competenza la sicurezza fisica per l'istanza locale. Il tuo data center è protetto dietro il tuo firewall aziendale.

Nella rete all'interno di una rete {{site.data.keyword.BluSoftlayer}}, il livello di rete pubblico gestisce il traffico pubblico a siti Web su host o risorse in linea. Il livello di rete privato consente una effettiva gestione fuori banda mediante un terzo vettore autonomo e distinto su gateway SSL, PPTP o IPSec VPN. Il livello di rete data center-data center fornisce una connettività gratuita e protetta tra server alloggiati in strutture {{site.data.keyword.BluSoftlayer}} separate. 

Ogni data center {{site.data.keyword.BluSoftlayer}} è pienamente protetto, con controlli che soddisfano i requisiti SSAE 16 e quelli riconosciuti dal settore, senza alcuna eccezione.

## Sicurezza dei dati
{: #data-security}

Con {{site.data.keyword.Bluemix_notm}}, la protezione dei dati da accessi non autorizzati è uno sforzo congiunto tra te e {{site.data.keyword.Bluemix_notm}}.

I dati associati a un'applicazione in esecuzione possono trovarsi in uno di tre stati: data-in-transit, data-at-rest e data-in-use.

<dl>
<dt>Data-in-transit</dt>
<dd>Dati che vengono trasferiti tra i nodi su una rete.</dd>

<dt>Data-at-rest</dt>
<dd>Dati che vengono memorizzati.</dd>

<dt>Data-in-use</dt>
<dd>Dati che non sono attualmente memorizzati a cui verrà applicata un'azione in un endpoint.</dd>
</dl>

Quando pianifichi la sicurezza dei dati, è necessario considerare ciascun tipo di dati.

La piattaforma {{site.data.keyword.Bluemix_notm}} protegge i data-in-transit proteggendo l'accesso dell'utente finale all'applicazione utilizzando SSL, per tutta la rete,
finché i dati non raggiungono l'IBM DataPower Gateway al limite della rete interna {{site.data.keyword.Bluemix_notm}}. IBM DataPower Gateway funge da proxy inverso e fornisce la terminazione SSL. Da lì all'applicazione, IPSEC viene utilizzato per proteggere i dati mentre vengono trasmessi dall'IBM DataPower Gateway all'applicazione.

Come sviluppatore della tua applicazione, sei responsabile della sicurezza sia dei data-in-use che dei data-at-rest. Puoi usufruire dei diversi servizi correlati ai dati disponibili nel catalogo {{site.data.keyword.Bluemix_notm}} per informazioni a tale riguardo.

## Sicurezza delle applicazioni {{site.data.keyword.Bluemix_notm}}
{: #application-security}

In quanto sviluppatore di applicazioni, è tuo compito abilitare le configurazioni di sicurezza, compresa la protezione dei dati applicativi, per le tue applicazioni che vengono eseguite su {{site.data.keyword.Bluemix_notm}}.

Per proteggere le tue applicazioni puoi servirti delle funzionalità di sicurezza fornite da diversi servizi {{site.data.keyword.Bluemix_notm}}. Tutti i servizi {{site.data.keyword.Bluemix_notm}} prodotti da IBM seguono le procedure di sviluppo di IBM Secure Engineering.

**Nota:** alcuni dei servizi qui descritti potrebbero non essere validi per le istanze {{site.data.keyword.Bluemix_notm}} dedicato o locale.

### Servizio SSO

IBM Single Sign On per {{site.data.keyword.Bluemix_notm}} è un servizio di autenticazione basato sulle politiche che fornisce una funzionalità SSO (single sign-on) facile da incorporare per le applicazioni Node.js o Liberty for Java™. Per consentire a uno sviluppatore applicazioni di incorporare la funzionalità SSO in un'applicazione, l'amministratore crea istanze del servizio e aggiunge origini di identità.

Il servizio Single Sign On supporta diverse origini di identità in cui vengono memorizzate le credenziali dei tuoi utenti:

<dl>
<dt>SAML Enterprise</dt>
<dd>Un registro utenti con uno scambio di token SAML che completa l'autenticazione.</dd>

<dt>Cloud Directory</dt>
<dd>Un registro utenti ospitato in IBM Cloud.</dd>

<dt>Origini di identità sociale</dt> <dd> I registri utenti gestiti da Google, Facebook e LinkedIn.</dd>
</dl>

Per ulteriori informazioni, vedi [Introduzione a Single Sign On](/docs/services/SingleSignOn/index.html).

### Application Security on Cloud

Questo servizio fornisce un'analisi della sicurezza delle applicazioni Web e mobili e ti consente di scansionare il codice sorgente alla ricerca di vulnerabilità di sicurezza. Per ulteriori informazioni, vedi [Introduzione a Application Security on Cloud](/docs/services/ApplicationSecurityonCloud/index.html).

### Plug-in IBM UrbanCode per il test di sicurezza delle applicazioni

Il plug-in IBM Application Security Testing for {{site.data.keyword.Bluemix_notm}} ti consente di eseguire la scansione sulle tue applicazioni Web o Android ospitate su {{site.data.keyword.Bluemix_notm}}. Questo plug-in è sviluppato e supportato dalla IBM UrbanCode™ Deploy Community sulla piattaforma IBM Bluemix DevOps Services.

Per ulteriori informazioni, vai a [IBM Application Security Testing for Bluemix ![icona link esterno](../icons/launch-glyph.svg)](https://developer.ibm.com/urbancode/plugindoc/ibmucd/ibm-application-security-testing-bluemix/1-0/){: new_window}.

### dashDB

Il servizio dashDB utilizza un server LDAP integrato per l'autenticazione utente. La connessione tra le applicazioni e il database è protetta da certificati SSL. Questo servizio utilizza la capacità di crittografia nativa di DB2® per crittografare automaticamente il tuo database distribuito e i tuoi backup di database. La rotazione della chiave master è automatica e si verifica ogni 90 giorni.

Per ulteriori informazioni, vedi [Introduzione a dashDB](/docs/services/dashDB/index.html).

### Secure Gateway

Il servizio Secure Gateway ti consente di connettere in modo sicuro le applicazioni {{site.data.keyword.Bluemix_notm}} a posizione remote, siano essere installate in loco o nel cloud. Fornisce una connettività sicura e stabilisce un tunnel tra la tua organizzazione {{site.data.keyword.Bluemix_notm}} e la posizione remota a cui vuoi connetterti. Puoi configurare e creare un gateway sicuro utilizzando l'interfaccia utente {{site.data.keyword.Bluemix_notm}} o un pacchetto API.

Per ulteriori informazioni, vedi [Introduzione a Secure Gateway](/docs/services/SecureGateway/secure_gateway.html).

### SIEM (Security Information and Event Management)

Puoi utilizzare gli strumenti SIEM (Security Information and Event Management) per analizzare gli avvisi di sicurezza nei log dell'applicazione. Uno di questi strumenti è IBM Security QRadar&reg; SIEM, che fornisce servizi di sicurezza in ambienti cloud. Per informazioni, vedi [IBM QRadar Security Intelligence Platform ![icona link esterno](../icons/launch-glyph.svg)](http://www-01.ibm.com/support/knowledgecenter/SS42VS/welcome?lang=en){: new_window}.

## Distribuzione della sicurezza {{site.data.keyword.Bluemix_notm}}
{: #security-deployment}

L'architettura della distribuzione della sicurezza {{site.data.keyword.Bluemix_notm}} include flussi di informazioni differenti per gli utenti dell'applicazione e gli sviluppatori al fine di garantire un accesso sicuro.

![Architettura della distribuzione della sicurezza Bluemix](images/sec_deployment.svg)

Figura 3. Architettura della distribuzione della sicurezza Bluemix

Per gli *utenti dell'applicazione* {{site.data.keyword.Bluemix_notm}}, il **flusso utente applicazione** è il seguente:
 1. Tramite firewall, con il rilevamento delle intrusioni e la sicurezza di rete attivi.
 2. Tramite IBM DataPower Gateway con proxy inverso e proxy di terminazione SSL.
 3. Tramite il router di rete.
 4. Raggiunge il runtime dell'applicazione nel DEA (Droplet Execution Agent).

Lo *sviluppatore* {{site.data.keyword.Bluemix_notm}} segue due flussi principali: quello per l'accesso e quello per lo sviluppo e la distribuzione.
 * Il **flusso di accesso degli sviluppatori** include quanto segue:
    * Per gli sviluppatori che accedono a {{site.data.keyword.Bluemix_notm}} pubblico, il flusso avviene come segue:
      1. Tramite il servizio IBM Single Sign On.
      2. Tramite l'identità Web IBM.
    * Per gli sviluppatori che accedono a {{site.data.keyword.Bluemix_notm}} dedicato o locale, il flusso passa attraverso il protocollo LDAP aziendale.
 * Il **flusso di sviluppo e distribuzione** è il seguente:
    1. Tramite firewall, con il rilevamento delle intrusioni e la sicurezza di rete attivi. Ciò vale solo per {{site.data.keyword.Bluemix_notm}} dedicato.
    2. Tramite IBM DataPower Gateway con proxy inverso e proxy di terminazione SSL.
    3. Tramite il router di rete.
    4. Tramite autorizzazione utilizzando il controller Cloud Foundry, per garantire l'accesso alle sole applicazioni e istanze del servizio create dallo sviluppatore.

Per gli *amministratori* di {{site.data.keyword.Bluemix_notm}} dedicato e {{site.data.keyword.Bluemix_notm}} locale, il **flusso amministratore** è il seguente:
 1. Tramite firewall, con il rilevamento delle intrusioni e la sicurezza di rete attivi.
 2. Tramite IBM DataPower Gateway con proxy inverso e proxy di terminazione SSL.
 3. Tramite il router di rete.
 4. Raggiunge la pagina Amministrazione nell'interfaccia utente {{site.data.keyword.Bluemix_notm}}.

Oltre agli utenti descritti in questi percorsi, un team per le operazioni di sicurezza IBM svolge diverse attività di sicurezza operativa, tra cui:
 * Scansioni delle vulnerabilità. Per {{site.data.keyword.Bluemix_notm}} locale, sono di tua competenza la sicurezza fisica e le eventuali scansioni all'interno del tuo firewall.
 * Gestione degli accessi utente.
 * Protezione avanzata del sistema operativo mediante l'applicazione periodica di correzioni con IBM Endpoint Manager.
 * Gestione dei rischi con protezione intrusioni.
 * Monitoraggio della sicurezza con QRadar.
 * Report di sicurezza disponibili sulla pagina Amministrazione.

## Conformità di sicurezza
{: #compliance}

{{site.data.keyword.Bluemix}} fornisce una piattaforma cloud sicura di cui ti puoi fidare. La conformità {{site.data.keyword.Bluemix_notm}} deriva da una piattaforma e da servizi basati sui migliori standard di sicurezza, tra cui ISO 27001 e ISO 27002.
{:shortdesc}

![Clausola del modello di protezione dati UE](images/icon_eumc.png)  una **Clausola del modello dell'Unione Europea (UE)** è un accordo studiato per proteggere i dati personali che vengono trasferiti dall'Unione Europea (UE) o dallo Spazio economico europeo (SEE) verso un terzo paese. La Clausola del modello UE viene firmato tra il client ubicato nell'UE o SEE come esportatore di dati e il processore di dati IBM ubicato nel paese terzo come importatore dei dati. La [Clausola del modello UE IBM SaaS ![icona link esterno](../icons/launch-glyph.svg)](http://www-01.ibm.com/common/ssi/cgi-bin/ssialias?subtype=ST&infotype=SA&htmlfid=KUJ12408USEN&attachment=KUJ12408USEN.PDF){: new_window} contiene i diritti e gli obblighi dell'esportatore e dell'importatore dei dati nonché i diritti dei soggetti interessati. La Clausola del modello UE IBM SaaS garantisce che i dati personali, quando elaborati in un paese terzo, siano posti sotto una protezione analoga a quella disponibile all'interno dell'UE o SEE.

Per i clienti che vogliono trasferire i dati provenienti dallo Spazio economico europeo a un paese fuori dal SEE, {{site.data.keyword.Bluemix}} offre clausole del modello europeo nel formato approvato dalle autorità di protezione dei dati della Commissione Europea e dell'Unione Europea. Le clausole del modello europeo garantiscono ai clienti europei che {{site.data.keyword.Bluemix_notm}} supporti le protezioni della privacy dei dati necessarie in ogni punto nel mondo.

![Financial Industry Information Systems](images/FISC.gif)  Per le istituzioni bancarie e finanziarie correlate in Giappone, i sistemi informatici devono disporre di procedure di sicurezza in vigore basate sulle linee guida di sicurezza FICS (Center for Financial Industry Information Systems). Le linee guida di sicurezza FISC vengono fatte rispettate dal Japan Financial Services Agency (FSA), Bank of Japan (BOJ) e FISC.
 

![ISO 27001/2](images/icon_iso27k1.png)  {{site.data.keyword.Bluemix_notm}} è certificato secondo gli **standard ISO (International Organization for Standardization) 27001 e 27002**, che definiscono le procedure ottimali per i processi di gestione della sicurezza informatica. ISO 27001 è uno standard di sicurezza globale ampiamente adottato che delinea i requisiti per i sistemi di gestione della sicurezza informatica. Fornisce un approccio sistematico nella gestione delle informazioni aziendali e dei clienti basato su periodiche valutazioni dei rischi. Lo standard più recente, ISO/IEC 27001:2013, è stato pubblicato il 25 settembre 2013 dall'**International Organization of Standardization (ISO) e International Electrotechnical Commission (IEC)** sotto la sottocommissione congiunta ISO e IEC. Lo standard ISO 27001 specifica i requisiti per stabilire, implementare e documentare i sistemi di gestione della sicurezza delle informazioni (ISMS) e i requisiti per applicare dei controlli di sicurezza in base alle esigenze delle singole organizzazioni. Lo standard ISO 27002 illustra in dettaglio ciascun controllo di sicurezza dell'ISO 27001. L'insieme di standard ISO 27000 incorpora un processo di ridimensionamento del rischio e valutazione delle risorse, con l'obiettivo di salvaguardare la riservatezza, l'integrità e la disponibilità delle informazioni scritte, orali ed elettroniche.

Per ottenere la certificazione ISO 27001:2013, un'azienda deve dimostrare che ha un approccio sistematico e costante nella gestione dei rischi della sicurezza informatica che influiscono sulla riservatezza, l'integrità e la disponibilità delle informazioni aziendali e dei clienti. Questo standard sottolinea la misurazione e la valutazione dell'efficacia del sistema di gestione della sicurezza delle informazioni (ISMS) di un'organizzazione e include anche i controlli relativi alla sicurezza di informazioni basati su requisiti di sistema e altri requisiti.

{{site.data.keyword.Bluemix_notm}} è controllato da una società di sicurezza di terze parti e rispetta tutti i requisiti per l'ISO 27001: [Bluemix ISO 27001:2013 Certificate of Registration ![icona link esterno](../icons/launch-glyph.svg)](ftp://public.dhe.ibm.com/cloud/bluemix/compliance/Bluemix_ISO27K1_WWCert_2016.pdf){: new_window}.

![PCI DSS](images/icon_pci.png)  il **PCI (Payment Card Industry) DSS (Data Security Standard)** è uno standard di sicurezza delle informazioni studiato per proteggere i dati delle carte di credito. PCI DSS si applica a tutte le entità coinvolte nell'elaborazione delle carte di pagamento, tra cui commercianti, processori, emittenti e fornitori di servizi. Si applica anche a tutte le altre entità che memorizzano, elaborano o trasmettono dati del titolare della carta o dati sensibili di autenticazione.

Se memorizzi o elabori i dati delle carte di credito, la conformità al PCI (Payment Card Industry) e la sicurezza di rete sono di primaria importanza per il tuo business. Per garantire standard coerenti per i commercianti, il Payment Card Industry Security Standards Council ha stabilito gli standard di sicurezza dei dati PCI. Questi standard incorporano le procedure ottimali per proteggere i dati del titolare della carta e spesso richiedono la convalida da parte di un QSA (Qualified Service Assessor) di terze parti. IBM aiuta i clienti a soddisfare le loro esigenze di conformità PCI, fornendo un Attestato di conformità da un QSA indipendente. L'attestazione di conformità può essere utilizzata insieme al report SOC 2 e alla certificazione ISO 27001 per dimostrare che l'infrastruttura rispetta i controlli PCI.

{{site.data.keyword.Bluemix}} completa una valutazione PCI DSS annuale utilizzando un QSA (Qualified Security Assessor) approvato. {{site.data.keyword.Bluemix_notm}} è esaminato come conforme in PCI DSS versione 3.1 al livello 1 del provider di servizi come descritto in [Bluemix PCI DSS AOC ![icona link esterno](../icons/launch-glyph.svg)](ftp://public.dhe.ibm.com/cloud/bluemix/compliance/IBM_Bluemix_PCI.pdf){: new_window}. Per informazioni e assistenza sulla conformità agli standard PCI DSS per il tuo ambiente {{site.data.keyword.Bluemix_notm}}, contatta il settore vendite in [Contatti ![icona link esterno](../icons/launch-glyph.svg)](https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs){: new_window}.

![SSAE16 SOC1/2/3](images/icon_aicpa.png) I report **Service Organization Controls (SOC)** definiscono la valutazione delle principali pratiche di controllo interno che riguardano la sicurezza, la disponibilità, l'integrità di elaborazione, la riservatezza e la privacy in un'organizzazione di servizi. I report generati mediante la Guida AICPA (American Institute of Certified Public Accountant) includono i seguenti elementi: 
  * Controllo dell'organizzazione
  * Programma di gestione dei fornitori
  * Processi interni del governo di impresa e della gestione dei rischi
  * Controllo regolamentare
 
{{site.data.keyword.Bluemix_notm}} fornisce i report SOC 1, SOC 2 e SOC 3. Per ulteriori informazioni, contatta il team delle [vendite {{site.data.keyword.Bluemix_notm}} ![icona link esterno](../icons/launch-glyph.svg)](mailto:bmxcert1@us.ibm.com){:new_window} team. 


![HIPAA](images/icon_hipaa.png) L'HIPAA (Health Insurance Portability and Accountability Act), approvato dal Congresso degli Stati Uniti nel 1996, protegge la copertura assicurativa sanitaria per i dipendenti dopo la perdita del posto di lavoro. HIPAA è regolamentato e applicato dall'Ufficio di diritti civili e del Dipartimento di Salute e Servizi Umani degli Stati Uniti. HIPAA comprende normative dell'atto del 1996, nonché i requisiti di privacy dell'atto Health Information Technology for Economic and Clinical Health (HITECH) del 2009. {{site.data.keyword.Bluemix_notm}} soddisfa tutti i requisiti per HIPAA sul lato data center o provider di servizi.

Per ulteriori informazioni o assistenza per ottenere, certificare e mantenere la conformità HIPAA per il tuo ambiente Bluemix, contatta il team {{site.data.keyword.Bluemix_notm}} [reparto vendite ![icona link esterno](../icons/launch-glyph.svg)](mailto:cloudplatform_compliance@us.ibm.com){:new_window}.


![ISO 27017](images/icon_ISO27017.png) ISO/IEC 27017:2015 fornisce linee guida per i controlli della sicurezza delle informazioni applicabili alla fornitura e all'uso dei servizi cloud. Fornisce inoltre delle indicazioni di implementazione per i fornitori e i clienti dei servizi cloud. ISO 27017 offre indicazioni di implementazione per i controlli rilevanti specificati in ISO/IEC 27002 nonché ulteriori controlli e indicazioni che si riferiscono specificamente ai servizi cloud.

L'allineamento di {{site.data.keyword.Bluemix_notm}} con ISO 27017:2015 dimostra che IBM utilizza un sofisticato sistema di controlli specifici del cloud. Inoltre, mostra un impegno ad essere il migliore in campo IaaS, sia a livello nazionale che internazionale.


![ISO 27018](images/icon_ISO27018.png) ISO 27018:2014 stabilisce obiettivi di controllo, controlli e linee guida comunemente accettati per attuare misure atte a proteggere le informazioni personali. Queste misure sono conformi ai principi della privacy nell'ISO 29100 per l'ambiente di elaborazione cloud pubblico.

In particolare, ISO 27018:2014 specifica le linee guida che si basano sull'ISO 27002. Le linee guida considerano i requisiti di regolamentazione per la protezione dei informazioni personali, che potrebbero essere applicabili nel contesto di ambienti a rischio di sicurezza delle informazioni di un fornitore di servizi cloud pubblici.


![Cloud Security Alliance – STAR Registrant](images/icon_CSA.png) Cloud Security Alliance è un'organizzazione no profit la cui missione è quella di promuovere l'utilizzo di procedure ottimali per fornire garanzie di sicurezza all'interno di un ambiente di elaborazione cloud. Uno dei meccanismi utilizzati da Cloud Security Alliance per perseguire la sua missione è il registro STAR (Security, Trust, and Assurance Registry). STAR è un registro gratuito, accessibile al pubblico, che documenta i controlli di sicurezza forniti dalle varie offerte di elaborazione cloud.


![CJIS Standards](images/icon_CJIS.png) La divisione CJIS (Criminal Justice Information Systems) è una divisione del Dipartimento di Giustizia dell'FBI degli Stati uniti. La divisione CJIS ha creato e pubblicato una politica di sicurezza (CJISD-ITS-DOC-08140-5.4). Questa politica di sicurezza contiene i requisiti minimi di sicurezza delle informazioni, le linee guida e gli accordi che riflettono la volontà delle forze dell'ordine e delle agenzie di giustizia penale per la protezione di fonti, trasmissioni, archiviazioni e generazione di informazioni di giustizia penale (CJI, Criminal Justice Information).



### Conformità di servizi e piattaforme
La seguente tabella mostra quali servizi {{site.data.keyword.Bluemix_notm}} sono conformi a ciascuno standard.

|Componenti {{site.data.keyword.Bluemix_notm}}		|FISC		|ISO 27001	|PCI |SOC 2 Type 1		|
|:----------------------|:---------:|:---------:|:---------:|:---------:|
|Piattaforma {{site.data.keyword.Bluemix_notm}}		|S			|S	|S	|S	|
|{{site.data.keyword.APIM}}			|S	|S |S	|			|
|{{site.data.keyword.autoscaling}}			|S	|S |S	|			|
|{{site.data.keyword.bigicloudst}}			|S |S |	|S |
|{{site.data.keyword.cloudant}}				|S |S |	|S	|
|{{site.data.keyword.dashdbshort}}			|S	|S	|	|S	|
|{{site.data.keyword.datacshort}}			|S	|S	|S	|			|
|{{site.data.keyword.jazzhub_short}}					|S	|S	|	|			|
|{{site.data.keyword.containerlong}}			|S		|S	|	|			|
|{{site.data.keyword.mql}}				|S	|S	|S	|	 		|
|{{site.data.keyword.SecureGateway}}			|S	|S |	|	 		|
|{{site.data.keyword.sescashort}}     |S |S |S	|  |
{: caption="Table 1. Platform and service compliance" caption-side="top"}

# Link correlati
{: #rellinks}

## Link correlati
{: #general}

* [IBM SaaS security ![icona link esterno](../icons/launch-glyph.svg)](http://www.ibm.com/cloud-computing/built-on-cloud/saas-security){: new_window}
* [Introduzione a Single Sign On](/docs/services/SingleSignOn/index.html)
