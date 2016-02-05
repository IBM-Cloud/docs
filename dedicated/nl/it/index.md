{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} dedicato
{: #dedicated}

*Ultimo aggiornamento: 18 gennaio 2016*

{{site.data.keyword.Bluemix}} è
una piattaforma basata su cloud open standard per la creazione, esecuzione e
gestione delle applicazioni. Con {{site.data.keyword.Bluemix_notm}} dedicato, ottieni la potenza unita alla semplicità di {{site.data.keyword.Bluemix_notm}}&mdash; nel tuo ambiente SoftLayer dedicato che è connesso in modo protetto sia all'ambiente {{site.data.keyword.Bluemix_notm}} pubblico sia alla tua rete.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} dedicato
include un catalogo privato che visualizza i servizi dedicati
disponibili in esclusiva per te. Sono compresi inoltre dei servizi aggiuntivi
che vengono diffusi e messi a tua disposizione da {{site.data.keyword.Bluemix_notm}} pubblico.

{{site.data.keyword.Bluemix_notm}} dedicato è costruito su SoftLayer, così da permetterti di usufruire della struttura cloud dalle prestazioni più elevate. Ciascun data center fornisce rigorosi controlli di sicurezza 24 ore al giorno, 7
giorni a settimana. Tu e IBM accedete all'istanza di {{site.data.keyword.Bluemix_notm}} dedicato tramite un tunnel VPN e una VLAN privata.

![{{site.data.keyword.Bluemix_notm}} Dedicato](images/detaileddedicated.png "{{site.data.keyword.Bluemix_notm}} dedicato")

*Figura 1. Diagramma dettagliato di {{site.data.keyword.Bluemix_notm}} dedicato*

Gli ambienti di {{site.data.keyword.Bluemix_notm}} dedicato
hanno gli stessi standard di sicurezza di {{site.data.keyword.Bluemix_notm}} pubblico in
termini di sicurezza fisica, operativa e di infrastruttura. Tuttavia,
l'accesso degli sviluppatori a {{site.data.keyword.Bluemix_notm}} dedicato è
controllato dalle tue politiche LDAP, che possono essere configurate dal team di {{site.data.keyword.Bluemix_notm}}
nel momento in cui configurano il tuo ambiente. All'interno dell'ambiente dedicato,
puoi gestire i ruoli e le autorizzazioni degli utenti. Per i dettagli, vedi [Gestione di utenti e autorizzazioni](../admin/index.html#oc_useradmin).

{{site.data.keyword.Bluemix_notm}} dedicato
viene fornito con tutti i runtime {{site.data.keyword.Bluemix_notm}} inclusi
e 128 GB di memoria per le applicazioni.

È inoltre disponibile una serie di servizi inclusi per impostazione predefinita e altri facoltativi che puoi scegliere per la tua istanza dedicata.

| **Tipo**        | **Nome**            | **Descrizione** |      
|-----------------|-------------------|-------------------|
| Incluso | {{site.data.keyword.autoscaling}} | Ti permette di aumentare o ridurre dinamicamente la capacità
di elaborazione della tua applicazione in base alle politiche. Con questo servizio,
avrai un uso illimitato nel tuo ambiente {{site.data.keyword.Bluemix_notm}}
dedicato. |
| Incluso | {{site.data.keyword.datacshort}} | Questo servizio fornisce una griglia di dati in memoria
che supporta scenari di cache distribuita per le tue applicazioni. Include
50 GB di cache in memoria. |
| Facoltativo | {{site.data.keyword.mql}} | {{site.data.keyword.mqlfull}} per {{site.data.keyword.Bluemix_notm}} è un servizio di messaggistica basato sul cloud che fornisce una messaggistica flessibile e facile da usare per le applicazioni {{site.data.keyword.Bluemix_notm}}. {{site.data.keyword.mql}} fornisce una soluzione con ridotte esigenze gestionali alla messaggistica. Puoi utilizzare {{site.data.keyword.mql}} per rendere le tue applicazioni più reattive e ridimensionabili e puoi condividere e scaricare lavoro tra le applicazioni con una semplice e potente API. |
| Facoltativo | {{site.data.keyword.dashdbshort}} | Usa dashDB per memorizzare dati relazionali, inclusi i tipi speciali quali i dati geospaziali. Quindi, analizza tali dati utilizzando l'analisi integrata SQL o avanzata come l'analisi predittiva e il data mining, l'analisi con R e l'analisi geospaziale. |
|Facoltativo | {{site.data.keyword.APIM}} | Utilizza il servizio {{site.data.keyword.APIMfull}}
per comporre, gestire e socializzare le API. Puoi importare delle API con risorse utilizzando un URL proxy o assemblando dati dalle origini dati HTTP. Il servizio {{site.data.keyword.APIM}} offre il vantaggio che puoi gestire la modalità di utilizzo delle tue API. |
|Facoltativo | {{site.data.keyword.SecureGateway}} | Il servizio {{site.data.keyword.SecureGateway}} fornisce un modo sicuro per connettere le applicazioni {{site.data.keyword.Bluemix_notm}} da posizioni remote installate in loco o nel cloud.  |

*Tabella 1. Servizi dedicati*


##Configurazione dell'istanza di {{site.data.keyword.Bluemix_notm}} dedicato
{: #setupdedicated}

{{site.data.keyword.Bluemix_notm}} dedicato
è progettato per fornire una versione privata dell'offerta {{site.data.keyword.Bluemix_notm}}
pubblico. Puoi utilizzare i servizi e i runtime {{site.data.keyword.Bluemix_notm}} per supportare le tue esigenze di elaborazione in un account SoftLayer ospitato da IBM.

IBM ti fornisce l'accesso a {{site.data.keyword.Bluemix_notm}} dedicato, utilizzando un accesso protetto da password. Puoi accedere a servizi, runtime
e risorse associate nonché distribuire e rimuovere applicazioni {{site.data.keyword.Bluemix_notm}}. IBM si avvale di più sedi SoftLayer per la distribuzione di {{site.data.keyword.Bluemix_notm}} dedicato, il che ti permette di ottenere la tua versione privata in una sede a te vicina.

Per configurare la tua versione privata di {{site.data.keyword.Bluemix_notm}}:

<ol>
<li>Per iniziare, contatta il tuo rappresentante dell'account designato IBM oppure <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">contatta {{site.data.keyword.Bluemix_notm}}</a>.</li>
<li>Determina insieme a IBM la quota per la tua istanza di {{site.data.keyword.Bluemix_notm}} dedicato. La quota mensile ricorrente si basa sui servizi dedicati
che desideri utilizzare, oltre a una sottoscrizione a tutti i servizi pubblici
{{site.data.keyword.Bluemix_notm}}. Riceverai quindi una fattura per tutto ciò che scegli di utilizzare
al di fuori di tale accordo di sottoscrizione.</li>
<li>Identifica le scadenze per ogni fase di configurazione
della tua istanza di {{site.data.keyword.Bluemix_notm}}
dedicato. Per informazioni su ciascuna fase e sulle attività coinvolte, vedi <a href="index.html#rolesresponsibilities" target="_blank">Ruoli e responsabilità {{site.data.keyword.Bluemix_notm}} dedicato</a>.</li>
<li>Seleziona la <a href="http://www.softlayer.com/data-centers" target="_blank">sede data center SoftLayer</a> per la tua istanza dedicata. Vengono creati quindi la tua piattaforma dedicata e il tuo account. Per l'account, devi identificare le persone all'interno della tua organizzazione
a cui assegnare i ruoli necessari per rendere operativa la tua istanza
dedicata. Per informazioni sui ruoli che puoi assegnare, vedi <a href="index.html#rolesresponsibilities" target="_blank">Ruoli e responsabilità {{site.data.keyword.Bluemix_notm}} dedicato</a>.
</li>
<li>Definisci e stabilisci la connettività di rete tra la tua rete aziendale e l'istanza di {{site.data.keyword.Bluemix_notm}}
dedicato.
	<ol type="a">
	<li>IBM installa l'infrastruttura di monitoraggio e di sicurezza per l'istanza dedicata.</li>
	<li>IBM installa i servizi dedicati a singolo tenant che hai selezionato.</li>
	<li>Fornisci gli endpoint e la configurazione di rete
per cose come indirizzi IP o firewall e accedi al tuo LDAP per
l'integrazione in {{site.data.keyword.Bluemix_notm}}.</li>
	</ol>
</li>
<li>Identifica e assegna i ruoli del tuo team amministrativo per l'ambiente.
	<ol type="a">
	<li>IBM configura l'accesso alla rete e il LDAP in base alle informazioni che hai fornito. L'accesso amministrativo
viene fornito ai contatti da te designati. Devi designare un
contatto anche per il supporto e la fatturazione.</li>
	<li>IBM configura un catalogo diffuso nell'ambiente dedicato per visualizzare i tuoi servizi dedicati. Il catalogo diffuso include dei servizi aggiuntivi che vengono diffusi e messi a tua disposizione da {{site.data.keyword.Bluemix_notm}} pubblico. Hai la possibilità di decidere quali servizi pubblici rispondono ai tuoi requisiti aziendali, sulla base di criteri di sicurezza e privacy dei dati.</li>
	<li>Convalidi la configurazione di rete e del firewall e l'accesso e l'endpoint LDAP.</li>
	</ol>
</li>
</ol>

Per la distribuzione e configurazione iniziale del tuo ambiente puoi prevedere un processo simile a quello elencato di seguito. Per i dettagli sui responsabili di ciascuna attività, vedi [Ruoli e responsabilità](../dedicated/index.html#rolesresponsibilities).

<ol>
<li>Seleziona il data center che verrà utilizzato per ospitare l'istanza dedicata. Per informazioni sulle opzioni dei data center, vedi <a href="http://www.softlayer.com/data-centers" target="_blank">Sede data center SoftLayer</a>.</li>
<li>Specifica i nomi di dominio per la distribuzione e gli ID che desideri utilizzare. Quando configuri l'istanza {{site.data.keyword.Bluemix_notm}}, ottieni tre domini.  Puoi scegliere il prefisso per <code>*mycompany*.*region*.bluemix.net</code> e <code>*mycompany*.*region*.mybluemix.net</code>. Inoltre, puoi scegliere il nome completo per il terzo dominio.<br />
<p>Puoi scegliere il numero di domini personalizzati desiderato. Tuttavia, sarai responsabile dei certificati dei domini personalizzati. Per ulteriori informazioni sulla creazione del dominio personalizzato, consulta <a href="../manageapps/updapps.html#domain">Creazione e utilizzo di un dominio personalizzato</a>.</p></li>
<li>Identifica un proprietario per l'account pubblico che viene utilizzato per rappresentare la tua azienda in {{site.data.keyword.Bluemix_notm}} pubblico. IBM utilizza questo account per tracciare l'utilizzo dei servizi diffusi.</li>
<li>Seleziona il tipo di connessione sicura al tuo data center. Puoi selezionare tra SoftLayer VPN, SoftLayer Direct Link e AT&T Net Bond.</li>
<li>Decidi se consentire l'accesso al tuo ambiente dedicato dall'Internet pubblico. </li>
<li>Seleziona il tipo di autenticazione che verrà utilizzato. Puoi selezionare ID IBM o Active Directory. Per informazioni sull'utilizzo e la registrazione di un ID IBM, consulta la pagina <a href="https://www.ibm.com/account/profile/us?page=regfaqhelp#4">Help and FAQ</a>.
</li>
<li>Identifica e assegna i ruoli del tuo team amministrativo per l'ambiente. Per informazioni sui ruoli che devi assegnare, vedi <a href="index.html#rolesresponsibilities" target="_blank">Ruoli e responsabilità {{site.data.keyword.Bluemix_notm}} dedicato</a>.</li>
<li>IBM distribuisce la piattaforma di base che include i runtime elastici, la console, la funzione di amministrazione e il monitoraggio.</li>
<li>IBM configura il tuo accesso amministrativo all'ambiente.</li>
<li>Puoi iniziare a utilizzare la tua istanza dedicata, monitorata dal team operativo IBM, al fine di rispondere agli avvisi.</li>
</ol>

Una volta configurata la tua istanza {{site.data.keyword.Bluemix_notm}}, puoi monitorare e gestire l'istanza {{site.data.keyword.Bluemix_notm}} utilizzando la pagina Amministrazione. Per ulteriori informazioni, vedi [Gestione di {{site.data.keyword.Bluemix_notm}} locale e dedicato](../administer/index.html#mng). Per informazioni su aggiornamenti e manutenzione, vedi [Manutenzione dell'istanza dedicata](index.html#maintaindedicated).

##Ruoli e responsabilità
{: #rolesresponsibilities}

Se hai configurato un account {{site.data.keyword.Bluemix_notm}} dedicato, devi identificare le persone all'interno della tua organizzazione a cui assegnare i ruoli necessari per rendere operativa la tua istanza.

###Ruoli

Il seguente elenco mostra i ruoli e le responsabilità dei clienti che puoi assegnare:

<dl>
<dt>**Procurement focal**</dt>
<dd>Lavora con il rappresentante IBM per organizzare il tuo ambiente {{site.data.keyword.Bluemix_notm}} dedicato, occupandosi inoltre dell'identificazione delle persone adeguate a gestire ogni aspetto del progetto all'interno della tua organizzazione. La persona assegnata a questo ruolo assume un ruolo di gestione dei progetti e controlla la selezione del modello, gli accordi commerciali e la disposizione dell'accesso alle risorse dei clienti. Il Procurement focal è il contatto generale per la configurazione dell'istanza dedicata e la traccia del processo di distribuzione.</dd>
<dt>**Responsabile della conformità**</dt>
<dd>Lavora con il rappresentante IBM per selezionare un'opzione di topologia e distribuzione che risponda ai tuoi requisiti di sicurezza. La persona assegnata a questo ruolo collabora con i consulenti di conformità IBM per determinare quali modelli di distribuzione raggiungono gli obiettivi di conformità.</dd>
<dt>**Network specialist**</dt>
<dd>Lavora con il rappresentante IBM per identificare i piani di rete per la distribuzione di {{site.data.keyword.Bluemix_notm}}. La persona assegnata a questo ruolo riesamina le specifiche di rete richieste da IBM e lavora con IBM su un piano di implementazione. Al termine della fase di installazione e verifica, la persona assegnata a questo ruolo conferma che la configurazione di rete è in conformità con gli standard aziendali.</dd>
<dt>**DevOps focal**</dt>
<dd>Lavora con il rappresentante IBM per pianificare e applicare gli aggiornamenti di manutenzione necessari per la piattaforma, i servizi e i runtime {{site.data.keyword.Bluemix_notm}}. La persona assegnata a questo ruolo lavora anche con il rappresentante IBM sulla configurazione della tua istanza di {{site.data.keyword.Bluemix_notm}} dedicato.</dd>
</dl>

I tuoi rappresentanti dei clienti collaborano con il tuo rappresentante dedicato e altri specialisti IBM che lavorano insieme per garantirti tutto il supporto di cui hai bisogno. Il rappresentante dedicato è il tuo unico punto di contatto all'interno del team di supporto allo sviluppo {{site.data.keyword.Bluemix_notm}} che svolge le seguenti attività:

<ul>
<li>Consente una rapida adozione del tuo ambiente {{site.data.keyword.Bluemix_notm}} dedicato.</li>
<li>Offre utili materiali didattici e di abilitazione per migliorare la tua autosufficienza.</li>
<li>Promuove una relazione a lungo termine tra te e lo sviluppo, il supporto e i servizi {{site.data.keyword.Bluemix_notm}} che utilizzi.</li>
</ul>

Il team operativo e di supporto {{site.data.keyword.Bluemix_notm}} che insieme a te gestisce l'istanza {{site.data.keyword.Bluemix_notm}} potrebbe accedere al tuo ambiente locale, ma lo fa solo per i seguenti motivi.

<ul>
<li>Per rispondere agli avvisi ed eseguire la manutenzione operativa</li>
<li>Per tentare di riprodurre un problema riportato su un ticket di supporto</li>
</ul>

###Responsabilità

Dalla configurazione del tuo ambiente alla manutenzione continua, è necessario completare una serie di attività. La seguente tabella illustra le attività richieste e il proprietario per lo svolgimento delle attività attraverso le fasi di inizio, avanzamento e completamento.

La fase di inizio è utilizzata per organizzare l'ambiente {{site.data.keyword.Bluemix_notm}} dedicato. Gli obiettivi principali di questa fase sono i seguenti:

- Esaminare l'accordo finanziario e stabilire le date cardine per la distribuzione.
- Creare la piattaforma {{site.data.keyword.Bluemix_notm}} e fornire accesso a runtime e servizi.
- Definire e stabilire la connettività di rete tra la tua rete aziendale e le operazioni {{site.data.keyword.Bluemix_notm}}.
- Identificare e assegnare i ruoli per il team amministrativo.

*Tabella 1. Attività della fase di inizio*

| **Attività** | **Dettagli attività** | **Parte responsabile** |
|----------|------------------|-----------------------|
|Impostare gli standard di conformità | Identificare gli standard governativi, di settore e aziendali richiesti per l'ambiente. | Cliente |
|Creare un piano di integrazione di sicurezza e conformità | Creare un piano di sicurezza e di integrazione che includa i costi, la pianificazione e le risorse necessarie per garantire la conformità di sicurezza. | IBM |
|Approvazione del piano di conformità | Approvare il piano di conformità. | Cliente |
|Creare il dimensionamento per l'ambiente |  	Creare il dimensionamento dell'ambiente sulla base di scelte predefinite che tengono in considerazione gli obiettivi di alta disponibilità e ripristino di emergenza, così come il provisioning iniziale di DEA e servizi necessario per supportare le applicazioni create con la piattaforma. Lavora insieme a IBM per definire, ad esempio, quali database sono necessari, quali servizi vengono offerti nel catalogo diffuso del cliente e altro ancora. | Responsabilità condivisa tra IBM e il cliente |
|Selezionare l'architettura | Selezionare l'architettura sulla base di scelte predefinite che tengono in considerazione i requisiti di alta disponibilità e ripristino di emergenza. | IBM |
|Definire gli obiettivi del ripristino di emergenza | Definire i requisiti di ripristino di emergenza per l'ambiente. | Cliente |
|Creare il piano di ripristino di emergenza | Consultare e definire il piano di ripristino di emergenza. IBM crea un modello di ripristino di emergenza e con te stabilisce dove fornire il feedback e approvare il piano. | Responsabilità condivisa tra IBM e il cliente |
|Creare il piano di backup e ripristino | Creare un piano di backup e ripristino che definisce la frequenza e i requisiti per la distribuzione interna ed esterna del backup. IBM esegue il backup dei componenti dell'infrastruttura, dei servizi IBM, dei metadati dei servizi inclusi i ruoli utente e altro ancora. Tu esegui il backup dei dati specifici dell'applicazione di cui sei responsabile. | Responsabilità condivisa tra IBM e il cliente |
|Identificare gli strumenti per il rilevamento degli eventi e la determinazione dei problemi | Identificare gli strumenti IBM e di terze parti utilizzati per il rilevamento degli eventi e la determinazione dei problemi a livello della piattaforma {{site.data.keyword.Bluemix_notm}}. | IBM |
|Definire il piano di escalation | Definire il piano di escalation per valutare e risolvere gli eventi rilevati dai componenti di monitoraggio. | IBM |
|Firmare gli accordi relativi a infrastruttura, piattaforma e supporto | Firmare l'accordo di sottoscrizione che include i termini e le condizioni finanziarie per l'ambiente. Firmare l'accordo di monitoraggio di rete e sicurezza. Firmare la sottoscrizione di supporto. | Cliente |
|Disporre l'ambiente | Disporre le risorse di calcolo, la rete e la memoria incluso la VLAN core e dei servizi per ospitare {{site.data.keyword.Bluemix_notm}} e i servizi bare metal per ospitare Data Power e SoftLayer Firewall. Fornire l'infrastruttura per consentire il tunnel VPN. | Cliente |
|Installare i componenti dell'infrastruttura, dell'applicazione e di monitoraggio e gestione | Installare, configurare e verificare i componenti dell'infrastruttura, come ad esempio BOSH Director, Cloud Controller, Health Manager, messaggistica, router, DEA e provider di servizi e i componenti di monitoraggio definiti nel piano di escalation e rilevamento dei problemi. | IBM |
|Installare e configurare i componenti di sicurezza | Installare e configurare i componenti di sicurezza vincolati nel piano di monitoraggio e di escalation, tra cui IBM QRadar, archivio credenziali, sistema di prevenzione delle intrusioni, IBM BigFix e IBM Security Privileged Identity Management. | IBM |
|Installare e configurare i componenti personalizzati |  	Installare e configurare i componenti personalizzati che si trovano al di fuori del campo di applicazione del prodotto e dei servizi {{site.data.keyword.Bluemix_notm}}. | Cliente |
|Stabilire la configurazione di rete iniziale | Stabilire la configurazione di rete iniziale inclusi i firewall, DataPower, Fortigate e DNS. | IBM |
|Connettere la pipeline {{site.data.keyword.Bluemix_notm}} | Connettere la pipeline di fornitura e di integrazione continua {{site.data.keyword.Bluemix_notm}} ai repository IBM. | IBM |
|Personalizzare i componenti della soluzione esterni | Personalizzare i servizi di bilanciamento del carico per gli scenari di ripristino di emergenza. | Cliente |
|Installare la soluzione VPN | Installare la soluzione VPN bidirezionale. | IBM |
|Configurare il server di accesso | Configurare il server di accesso per l'utilizzo del LDAP aziendale. | IBM |
|Tracciare lo stato per le verifiche di sicurezza, conformità e controllo  | Tracciare lo stato fino al punto in cui vengono osservati tutti gli strumenti e processi per raggiungere la conformità identificata. | Cliente |
|Controllare l'infrastruttura fisica | Controllare le sedi fisiche che ospitano i componenti della soluzione per individuare eventuali minacce e riesaminare i controlli di sicurezza per proteggere il data center. | Cliente |
|Ispezionare il software di monitoraggio | Ispezionare i componenti di monitoraggio e gestione, come definito nel piano di escalation e determinazione dei problemi. | Cliente |
|Ispezionare il sistema operativo | Verificare che l'immagine del sistema operativo rispetti gli standard di conformità. IBM fornisce l'accesso all'immagine del sistema operativo. | Responsabilità condivisa tra IBM e il cliente |

La fase successiva è quella di avanzamento. La fase di avanzamento descrive il rapporto di collaborazione in corso tra te e IBM Cloud. Gli obiettivi principali per questa fase sono i seguenti:

- Esaminare le capacità e coordinare le modifiche necessarie.
- Esaminare i miglioramenti di manutenzione e piattaforma.
- Coordinare le attività per la risoluzione dei problemi e l'analisi delle cause principali.

*Tabella 2. Attività della fase di avanzamento*

| **Attività** | **Dettagli attività** | **Parte responsabile** |
|----------|------------------|-----------------------|
|Esaminare i report sulle capacità settimanali | Esaminare i report sulle capacità settimanali e adottare misure correttive laddove necessario. | Cliente |
|Creare proiezioni mensili | Raccogliere informazioni e creare una proiezione mensile della capacità e del consumo. | Responsabilità condivisa tra IBM e il cliente |
|Esaminare le proiezioni della capacità | Esaminare le proiezioni della capacità relative ad eventi esterni che potrebbero influire sulle capacità così come sulle nuove distribuzioni previste per le applicazioni. Lavorare con IBM per esaminare le proiezioni e creare un piano adeguato. | Responsabilità condivisa tra IBM e il cliente |
|Esaminare le proiezioni | Esaminare le proiezioni della capacità relative ad eventi esterni che potrebbero influire sulle capacità. | Cliente |
|Regolare la capacità |  Aggiungere o rimuovere capacità al mutare delle esigenze. | IBM |
|Pubblicare gli aggiornamenti e la manutenzione previsti | Creare la documentazione per la manutenzione richiesta dei componenti IBM. | IBM |
|Effettuare la manutenzione | Lavorare con IBM per pianificare la manutenzione richiesta all'interno di una finestra di 30 giorni. Puoi fornire delle date di non disponibilità all'interno della finestra di 30 giorni e IBM organizzerà di conseguenza la manutenzione. | Responsabilità condivisa tra IBM e il cliente |
|Rilevamento di errori di provisioning | Correggere gli errori di provisioning, se presenti, per i servizi creati dal cliente che vengono distribuiti nel catalogo. | IBM |
|Eseguire scansioni di rete e IP | Eseguire scansioni di rete e IP giornaliere e mensili. | Responsabilità condivisa tra IBM e il cliente |
|Fornire accesso ai log di controllo | Fornire accesso a tutti i log di controllo amministrativo e della sicurezza.   | Responsabilità condivisa tra IBM e il cliente |
|Effettuare dei test | Effettuare periodicamente il test dei controlli chiave sulle operazioni e il test di penetrazione di terze parti. | Responsabilità condivisa tra IBM e il cliente |
|Segnalazione dello stato, coordinamento dei controlli e incontri di conformità  | Completare la segnalazione dello stato, il coordinamento del controllo esterno e la rappresentazione negli incontri sullo stato di revisione della conformità. | IBM |
|Verifica dell'occupazione lavorativa e delle esigenze aziendali | Completare la verifica trimestrale dell'occupazione lavorativa e la verifica delle continue esigenze aziendali per i rappresentanti IBM che hanno accesso all'ambiente del cliente. | IBM |
|Risoluzione delle vulnerabilità di sicurezza | Risolvere le vulnerabilità di sicurezza segnalate nella piattaforma. | IBM |

La fase finale di completamento rappresenta la fine del rapporto tra te e IBM {{site.data.keyword.Bluemix_notm}}. Le attività principali per questa fase sono le seguenti:

* Termine dell'accordo finanziario
* Rimozione di tutte le connessioni di rete
* Riciclaggio dell'infrastruttura

*Tabella 3. Attività della fase di completamento*

| **Attività** | **Dettagli attività** | **Parte responsabile** |
|----------|------------------|-----------------------|
|Terminare l'accordo finanziario | Discutere e concordare un termine per il contratto dell'accordo finanziario. | Responsabilità condivisa tra IBM e il cliente |
|Rimuovere le autorizzazioni per l'ambiente | Disattivare l'accesso e le credenziali per l'ambiente. | Responsabilità condivisa tra IBM e il cliente |
|Rimuovere le connessioni di rete del cliente | Rimuovere le connessioni di rete tra IBM e l'ambiente del cliente. | Responsabilità condivisa tra IBM e il cliente |
|Riciclare l'infrastruttura | Il tuo ambiente viene riciclato in base ai processi definiti da SoftLayer. | IBM |

##Gestione della tua istanza dedicata
{: #maintaindedicated}

IBM effettua la manutenzione e l'installazione di aggiornamenti e correzioni ogni qualvolta lo ritenga appropriato per la piattaforma, i runtime e i servizi di {{site.data.keyword.Bluemix_notm}} dedicato.

**Importante**: IBM si riserva il diritto di interrompere i servizi per applicare la manutenzione di emergenza a seconda delle necessità. IBM potrebbe modificare le ore di manutenzione pianificate, ma verrai avvisato di tali modifiche nonché di tutte le informazioni relative alla manutenzione di emergenza.

Per
{{site.data.keyword.Bluemix_notm}} dedicato sono richiesti i seguenti tipi di manutenzione:
<dl>
<dt>**Finestre di manutenzione standard**</dt>
<dd>I servizi utilizzano delle finestre di manutenzione standard predefinite, che potrebbero causare la non disponibilità del servizi. IBM non richiede l'approvazione dei clienti per eseguire la manutenzione, ma prova a ridurre al minimo l'impatto sui tuoi servizi.<br />
<br />
IBM invia messaggi broadcast relativi alle modifiche pianificate per ciascuna finestra di manutenzione tramite email, telefono o altri metodi.<br />
<br />
**Importante**: alcuni servizi potrebbero non essere a tua disposizione durante il periodo di manutenzione.</dd>

<dt>**Finestra di modifica mensile**</dt>
<dd>La finestra di manutenzione mensile viene applicata in base al coordinamento tra te e IBM entro una finestra di 21 giorni. Puoi fornire a IBM date od orari specifici entro la finestra di 21 giorni che potrebbero non andare bene per te. IBM prova a pianificare gli aggiornamenti tenendo conto di tali indicazioni temporali. In base alle richieste, IBM ti comunica la finestra di manutenzione pianificata. Non si prevede che le finestre di modifica mensili abbiano un impatto sull'ambiente Bluemix dedicato in esecuzione.<br />
<br />
**Nota:** se non richiedi una data/ora specifica per l'aggiornamento, la manutenzione viene applicata automaticamente alla fine della finestra.<br />
<br />
Vai a **AMMINISTRAZIONE > INFORMAZIONI DI SISTEMA** per visualizzare gli aggiornamenti in sospeso, impostare le date non disponibili e approvare gli aggiornamenti. Per ulteriori informazioni sulle notifiche e sulla pianificazione degli aggiornamenti in sospeso, vedi <a href="../admin/index.html#oc_system">Visualizzazione delle informazioni sul sistema</a>.</dd>

<dt>**Altro**</dt>
<dd>IBM intende limitare gli interventi di manutenzione che potrebbero influire sui tuoi servizi, in particolare sulla disponibilità dell'ambiente, dei runtime e dei servizi del tuo {{site.data.keyword.Bluemix_notm}} dedicato, agli aggiornamenti standard e mensili. In via eccezionale, potrebbero essere utilizzate altre finestre di modifica per la gestione
dell'ambiente. IBM si impegnerà a ridurre al minimo l'impatto sul tuo lavoro durante tali finestre di modifica e ti avviserà anticipatamente.</dd>
</dl>

Per configurare la manutenzione della tua istanza dedicata, collabora con il rappresentante designato IBM per identificare una finestra concordata per la manutenzione standard.

Se viene segnalato un problema dopo l'aggiornamento di manutenzione, insieme al rappresentante IBM puoi stabilire se sia utile consentire a IBM di eseguire il rollback dell'aggiornamento. Previo accordo, IBM esegue il rollback dell'aggiornamento per ripristinare l'ambiente allo stato precedente.

## Ripristino di emergenza
{: #dr}

{{site.data.keyword.Bluemix_short}} pubblico fornisce una piattaforma costantemente disponibile per l'innovazione. Le diverse misure alternative fanno sì che le tue organizzazioni, gli spazi e le applicazioni siano sempre disponibili. La distribuzione delle applicazioni in più regioni geografiche consente una disponibilità continua che protegge contro l'imprevista perdita simultanea di più componenti hardware o software o la perdita di un intero data center; in tal modo, anche in caso di catastrofe naturale in una posizione geografica, le istanze distribuite della tua applicazione {{site.data.keyword.Bluemix_notm}} pubblico saranno disponibili in posizioni geografiche alternative.
{: shortdesc}

Il ripristino di emergenza per {{site.data.keyword.Bluemix_short}} dedicato è reso possibile grazie alla disponibilità continua per le tue applicazioni, all'alta disponibilità intrinseca della piattaforma e alla possibilità di ripristinare l'istanza in caso di errore. Sei responsabile dell'abilitazione della disponibilità continua delle tue applicazioni mediante la distribuzione a più regioni. L'alta disponibilità viene integrata a livello della piattaforma tramite le tecnologie incluse in Cloud Foundry e altri componenti. Inoltre, puoi collaborare con IBM per assicurarti che il backup dei tuoi dati venga eseguito correttamente nel caso in cui sia necessario ripristinare la tua istanza.

### Abilitazione della disponibilità continua per {{site.data.keyword.Bluemix_notm}} dedicato
{: #enabling}

Per impostazione predefinita, {{site.data.keyword.Bluemix_notm}} pubblico viene distribuito in più posizioni geografiche. Tuttavia, per abilitare le istanze {{site.data.keyword.Bluemix_notm}} dedicato distribuite a livello globale, devi effettuare le seguenti attività:

* Assicurati che gli sviluppatori stiano distribuendo le applicazioni in più di una regione, mediante un processo manuale o automatico. Le regioni dovrebbero trovarsi a più di 200 km di distanza l'una dall'altra per garantire che, in caso di catastrofe naturale, non vengano colpite entrambe le posizioni geografiche.
* Configurare un programma di bilanciamento del carico globale, come Akamai o Dyn, per puntare ad applicazioni in almeno due regioni diverse.

**Nota**: non tutti i servizi {{site.data.keyword.Bluemix_notm}} supportano la distribuzione regionale. Quando crei un'applicazione, se vuoi garantire una distribuzione geografica, devi fare in modo che i servizi utilizzati dall'applicazione abbiano come funzione fondamentale la sincronizzazione dei dati.

#### Distribuzione di applicazioni {{site.data.keyword.Bluemix_notm}} dedicato in più posizioni geografiche
{: #deploying}

Per eseguire la distribuzione in una seconda posizione o in più posizioni, devi seguire un processo simile a quello effettuato per abilitare la posizione geografica primaria:

1. Abilita un nuovo ambiente dedicato per ospitare istanze aggiuntive delle tue applicazioni. Per creare un nuovo ambiente, contatta il team del settore vendite IBM per avviare il processo. Per ulteriori informazioni sulla configurazione di un'istanza dedicata, vedi [Configurazione di {{site.data.keyword.Bluemix_notm}} dedicato](../dedicated/index.html#setupdedicated). Devi effettuare un accesso distinto per ogni ambiente. Ciascuna posizione fisica degli ambienti host deve trovarsi ad almeno 200 km di distanza dalla posizione originale per garantire la disponibilità.
2. Ottieni il nome di dominio univoco in cui verrà ospitata la tua nuova applicazione distribuita.  Ad esempio, se il dominio originale è *mycompany.east.bluemix.net*, puoi creare un nuovo ambiente locale con un nuovo dominio come, ad esempio, *mycompany.west.bluemix.net* e distribuire al nuovo dominio.
3. Ogni volta che distribuisci l'applicazione originale, esegui anche la distribuzione nella nuova posizione. Per ulteriori informazioni sulla distribuzione, vedi [Caricamento della tua applicazione](../starters/upload_app.html).


#### Abilitazione di un programma di bilanciamento del carico globale per {{site.data.keyword.Bluemix_notm}} dedicato
{: #glb}

Un programma di bilanciamento del carico globale non solo garantisce la disponibilità continua ed è richiesto per il ripristino di emergenza, ma presenta anche diversi vantaggi aggiuntivi:

* Indirizza gli utenti alla regione {{site.data.keyword.Bluemix_notm}} più vicina per impostazione predefinita
* Indirizza in base alle prestazioni
* Instrada selettivamente una percentuale di traffico a una nuova versione dell'applicazione
* Fornisce il failover del sito in base alla verifica dell'integrità della regione
* Fornisce il failover del sito in base alla verifica dell'integrità dell'applicazione
* Utilizza un instradamento ponderato tra gli endpoint

Puoi scegliere un programma di bilanciamento del carico globale come Akamai o Dyn. Per ulteriori informazioni sull'utilizzo di Akamai come programma di bilanciamento del carico globale, vedi [Global traffic management](https://www.akamai.com/us/en/solutions/products/web-performance/global-traffic-management.jsp){: new_window}. Per ulteriori informazioni sull'utilizzo di Dyn come programma di bilanciamento del carico globale, vedi [4 Reasons Businesses Are Taking Global Load Balancing to the Cloud](http://dyn.com/blog/4-reasons-businesses-are-taking-global-load-balancing-to-the-cloud/){: new_window}.

### Alta disponibilità
{: #ha}

Oltre a consentire la disponibilità continua, {{site.data.keyword.Bluemix_notm}} fornisce anche l'alta disponibilità in tutta la piattaforma utilizzando le tecnologie integrate in Cloud Foundry, Docker e altri componenti.

Queste tecnologie includono:

<dl>
<dt>Scalabilità in Cloud Foundry</dt>
<dd>Un <a href="https://docs.cloudfoundry.org/concepts/architecture/execution-agent.html" target="_blank">DEA (Droplet Execution Agent)</a> Cloud Foundry effettua verifiche dell'integrità nelle applicazioni eseguite al suo interno. Se si verifica un problema con l'applicazione o con lo stesso DEA, distribuisce ulteriori istanze dell'applicazione a un DEA alternativo per risolvere il problema. Per ulteriori informazioni, vedi <a href="https://docs.cloudfoundry.org/concepts/high-availability.html" target="_blank">Configuring CF for High Availability with Redundancy</a>.
</dd>
<dt>Ridondanza SoftLayer</dt>
<dd>Con SoftLayer negli ambienti dedicati, i dati presenti in ciascun cluster di archiviazione cloud vengono scritti più volte e i cluster di archiviazione sono configurati con capacità di riparazione automatica in caso di guasto dell'unità. Se si verifica un problema con una macchina virtuale, SoftLayer prova a riavviare la macchina virtuale in un altro host.</dd>
<dt>Backup dei metadati</dt>
<dd>I metadati vengono sottoposti a backup mediante il sistema SoftLayer EVault Backup in una posizione che si trova ad almeno 200 km di distanza.</dd>
</dl>

##Ripristino della tua istanza dedicata
{: #restorededicated}

Il backup di impostazioni, metadati e configurazioni di {{site.data.keyword.Bluemix_notm}} dedicato viene eseguito periodicamente come tutela in caso di eventuali interruzioni non pianificate nell'ambiente. I dati per i quali sei responsabile del backup includono i dati dell'applicazione, i dati dei servizi del database cloud e gli archivi oggetti.

Come parte del backup dei dati, che include i metadati del sistema e le configurazioni, IBM completa le seguenti attività:

<ul>
<li>Crittografa tutte le copie di backup e gestisce le chiavi di crittografia</li>
<li>Monitora e gestisce l'attività di backup</li>
<li>Fornisce i file di backup crittografati</li>
<li>Ripristina i dati richiesti</li>
<li>Gestisce i conflitti di pianificazione tra le operazioni di gestione dei backup e delle correzioni</li>
</ul>

Poiché la protezione dei dati privati è di importanza critica, IBM ha bisogno della tua collaborazione quando si occupa della gestione dei file di backup in modo che i file non vengano spostati all'esterno dei tuoi data center. Nello specifico, IBM richiede che tu completi le seguenti attività:

<ul>
<li>Spostare una copia dei tuoi dati di backup crittografati fuori sede, proprio come faresti per qualsiasi altro dato di backup da te gestito.</li>
<li>Fornire i file di backup per l'operatore IBM nel caso occorra eseguire un ripristino.</li>
</ul>

# rellinks
## general
* [Scopri: {{site.data.keyword.Bluemix_notm}} dedicato](http://www.ibm.com/cloud-computing/bluemix/hybrid/dedicated/)
* [Gestione di {{site.data.keyword.Bluemix_notm}} locale e {{site.data.keyword.Bluemix_notm}} dedicato](../admin/index.html#mng)
* [Come contattare il supporto](../troubleshoot/getting_customer_support.html#bluemix_support)
