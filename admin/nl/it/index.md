{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#Amministrazione di {{site.data.keyword.Bluemix_notm}}
{: #administer}
*Ultimo aggiornamento: 20 gennaio 2016*

Gestisci le tue organizzazioni, i tuoi spazi e i tuoi utenti assegnati facendo clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Gestisci organizzazioni**. Se sei un utente {{site.data.keyword.Bluemix_notm}} locale o {{site.data.keyword.Bluemix_notm}} dedicato, vedi [Gestione di {{site.data.keyword.Bluemix_notm}} locale e {{site.data.keyword.Bluemix_notm}} dedicato](index.html#mng) per ulteriori informazioni sull'amministrazione della tua istanza locale o dedicata.
{:shortdesc}

##Gestione del tuo account
{: #mngacct}

In {{site.data.keyword.Bluemix}} pubblico, puoi gestire organizzazioni e spazi, compreso l'accesso degli utenti, e tutto questo dal dashboard nell'interfaccia utente. Puoi anche monitorare il tuo utilizzo e la fatturazione a tuo carico.
{:shortdesc}

###Organizzazioni e spazi
{: #orgsandspaces}

In qualità di gestore dell'organizzazione o proprietario dell'account, puoi utilizzare la pagina Gestisci organizzazioni per visualizzare e gestire le impostazioni dell'organizzazione o dello spazio, incluso l'accesso degli utenti. Per aprire la pagina Gestisci organizzazioni, fai clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Gestisci organizzazioni**.

####Organizzazioni

Un'organizzazione è definita dai seguenti elementi:

<dl>
<dt>Utenti</dt>
<dd>Il ruolo con l'autorizzazione di base in organizzazioni e spazi. Devi essere assegnato
a un'organizzazione prima che ti possano essere concesse altre autorizzazioni agli
spazi all'interno dell'organizzazione. Per informazioni dettagliate,
consulta [Utenti e ruoli](index.html#userroles).</dd>
<dt>Domini</dt>
<dd>Fornisci la rotta su internet che è assegnata all'organizzazione. Una rotta ha un dominio secondario e un dominio. Un dominio secondario è di norma il
nome dell'applicazione. Un dominio può essere un dominio di sistema o un dominio personalizzato che hai registrato per la tua applicazione.<br/>
<p>**Nota**: se aggiungi un dominio personalizzato, devi configurare il server DNS per risolvere il tuo dominio personalizzato per puntare al dominio di sistema {{site.data.keyword.Bluemix_notm}}. In questo modo, quando {{site.data.keyword.Bluemix_notm}} riceve una richiesta per il tuo dominio personalizzato, può correttamente instradarla alla tua applicazione.</p></dd>
<dt>Quota</dt>
<dd>Rappresenta i limiti di risorse per l'organizzazione, compreso il numero di servizi
e la quantità di memoria che può essere assegnata per l'utilizzo da parte dell'organizzazione. Le quote vengono assegnate quando
vengono create le organizzazioni. Applicazioni o servizi in uno spazio dell'organizzazione contribuiscono tutti
all'utilizzo della quota. Con i piani Pagamento a consumo o Sottoscrizione, puoi regolare la tua quota per
le applicazioni e i contenitori Cloud Foundry in base al variare delle esigenze della tua organizzazione.</dd>
</dl>

In {{site.data.keyword.Bluemix_notm}},
puoi utilizzare le organizzazioni per abilitare la collaborazione tra utenti e per facilitare il raggruppamento
logico di risorse dei progetti nei seguenti modi:

<ul>
<li>Puoi raggruppare un insieme di spazi, applicazioni, servizi, domini, rotte e utenti nelle organizzazioni.</li>
<li>Puoi gestire l'accesso agli spazi e alle organizzazioni in base ai singoli utenti.</li>
</ul>

Quando crei
un'organizzazione, il suo nome deve essere univoco in {{site.data.keyword.Bluemix_notm}}. Dopo che hai creato l'organizzazione, ti verrà automaticamente assegnata
l'autorizzazione *Gestore organizzazione*, che ti consente di modificare il nome dell'organizzazione, di eliminarla e di creare spazi al suo interno.

Quando elimini un'organizzazione, tutti gli
spazi e i servizi e tutte le applicazioni al suo interno vengono eliminati.

{{site.data.keyword.Bluemix_notm}} consente la collaborazione sui progetti assegnando utenti all'interno di un'organizzazione e all'interno degli
spazi nell'organizzazione. Puoi utilizzare la scheda **Utenti** per
visualizzare e gestire gli utenti dell'organizzazione. Puoi anche invitare gli utenti alla tua organizzazione facendo clic sul link **Invita un nuovo utente** nella scheda **Utenti**. Agli utenti in un'organizzazione possono essere assegnate le seguenti autorizzazioni:

<ul>
<li>Utente organizzazione</li>
<li>Gestore organizzazione</li>
<li>Gestore fatturazione dell'organizzazione</li>
<li>Revisore organizzazione</li>
</ul>

####Spazi

All'interno di un'organizzazione, puoi utilizzare
gli spazi per raggruppare un insieme di applicazioni, servizi e utenti.

Dopo che hai aggiunto gli
utenti a un'organizzazione, puoi concedere loro le autorizzazioni agli spazi all'interno
dell'organizzazione. In modo analogo alle organizzazioni, anche gli spazi hanno una serie di autorizzazioni che possono
essere assegnate agli utenti:

<ul>
<li>Gestore spazio</li>
<li>Sviluppatore spazio</li>
<li>Revisore spazio</li>
</ul>

**Nota**: a un utente deve essere assegnata almeno una delle autorizzazioni nello spazio.

La scheda **Domini** per uno spazio
è un elenco di sola lettura dei domini assegnati allo spazio. Il dominio di sistema è sempre disponibile per uno spazio e allo
spazio è anche possibile assegnare dei domini personalizzati. Le applicazioni che erano state create nello spazio possono utilizzare qualsiasi dominio elencato per lo spazio.

###Utenti e ruoli
{: #userroles}

I proprietari degli account eseguono tutte le operazioni sulle organizzazioni
e sugli spazi.

####Tipi di utenti

Puoi essere un membro o un collaboratore di un account.

<dl>
<dt>Membro</dt>
<dd>Sei un membro di un account {{site.data.keyword.Bluemix_notm}} se
hai creato l'account, oppure se sei stato invitato all'account e hai quindi eseguito la
registrazione dall'invito, come tua prima esperienza con {{site.data.keyword.Bluemix_notm}}. </dd>
<dt>Collaboratore</dt>
<dd>Sei un collaboratore di un account {{site.data.keyword.Bluemix_notm}}
se hai in precedenza utilizzato {{site.data.keyword.Bluemix_notm}} con
un account differente ma sei stato quindi invitato a questo account e hai accettato
l'invito.</dd>
</dl>

####Ruoli utente

Agli utenti possono essere assegnate
le seguenti autorizzazioni per assumere ruoli utente differenti in
un'organizzazione o in uno spazio:

<dl>
<dt>Gestori organizzazione</dt>
<dd>I gestori organizzazione hanno le seguenti autorizzazioni:
<ul>
<li>Creare o eliminare spazi all'interno dell'organizzazione.</li>
<li>Invitare utenti all'organizzazione se sei anche un membro
dell'organizzazione oppure il proprietario dell'account.</li>
<li>Gestire gli utenti esistenti che già fanno parte dell'organizzazione.</li>
<li>Gestire i domini dell'organizzazione.</li>
</ul>
<p>**Nota**: se hai il tipo utente di collaboratore, e precedentemente hai utilizzato {{site.data.keyword.Bluemix_notm}} con un altro account, non puoi invitare utenti all'organizzazione anche se ti è stato assegnato il ruolo di gestore organizzazione. Devi avere
il tipo di utente di membro per invitare degli utenti. Per informazioni su come aggirare questo
problema, consulta il documento relativo all'<a href="../troubleshoot/index.html#ts_adduser">impossibilità di aggiungere utenti a un'organizzazione</a>.</p>
</dd>
<dt>Gestori fatturazione</dt>
<dd>I gestori fatturazione dispongono delle autorizzazioni per
visualizzare le informazioni su runtime e servizi per l'organizzazione.</dd>
<dt>Revisori organizzazione</dt>
<dd>I revisori organizzazione dispongono delle autorizzazioni per visualizzare
il contenuto di applicazioni e servizi nello spazio.</dd>
<dt>Gestori spazio</dt>
<dd>I gestori spazio hanno le seguenti autorizzazioni:
<ul>
<li>Aggiungere utenti allo spazio e gestire gli utenti.</li>
<li>Abilitare le funzioni per lo spazio</li>
</ul>
</dd>
<dt>Sviluppatori spazio</dt>
<dd>Gli sviluppatori spazio hanno le seguenti autorizzazioni:
<ul>
<li>Creare, eliminare e gestire applicazioni e servizi all'interno dello spazio.</li>
<li>Avere accesso ai log all'interno dello spazio</li>
</ul>
</dd>
<dt>Revisori spazio</dt>
<dd>I revisori spazio hanno le autorizzazioni per l'accesso in sola lettura
a tutte e informazioni sullo spazio, quali le informazioni su applicazioni e servizi,
impostazioni, report e log.</dd>
</dl>

###Gestione della tua organizzazione
{: #orgmng}

In qualità di gestore dell'organizzazione o di proprietario dell'account,
puoi gestire le tue organizzazioni. Le attività di gestione includono la creazione di un'organizzazione, la rinominazione di un'organizzazione, la creazione di uno spazio, l'invito di utenti a uno spazio, la modifica dei ruoli utente e l'eliminazione di un'organizzazione esistente.

<ul>
<li>Creazione di un'organizzazione
<p>Solo gli utenti con account a pagamento possono creare un'organizzazione. Con un account a pagamento,
puoi creare un'organizzazione attenendoti alla seguente procedura:</p>
<ol>
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Gestisci organizzazioni**.</li>
<li>Fai clic su **Crea un'organizzazione** e attieniti alle richieste che
ti vengono presentate per creare la tua organizzazione.</li>
</ol>
</li>
<li>Rinominazione di un'organizzazione
<p>Per rinominare la tua organizzazione, attieniti alla seguente procedura:</p>
<ol>
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Account e supporto** ![Account e supporto](images/account_support.svg), quindi seleziona **Gestisci organizzazioni**.</li>
<li>Seleziona l'organizzazione che desideri rinominare.</li>
<li>Immetti un nuovo nome nel campo **Organizzazione** e fai
clic su **Salva**.</li>
</ol>
</li>
<li>Elenco dei membri
<p>Attieniti alla seguente procedura per elencare i membri della tua organizzazione o del tuo spazio:</p>
<ol>
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Gestisci organizzazioni**.Puoi visualizzare i membri
della tua organizzazione e i loro ruolo nella scheda **Utenti**.</li>
<li>Fai clic sul nome dello spazio nella tua organizzazione per visualizzare i membri di questo spazio e i loro ruoli.</li>
</ol>
</li>
<li>Creazione di uno spazio
<p>Puoi creare degli spazi nella tua organizzazione; ad esempio,
uno spazio *dev* come un ambiente di sviluppo,
uno spazio *test* come un ambiente di test e uno
spazio *production* come un ambiente di produzione. Puoi quindi associare le tue applicazioni agli spazi. Per creare uno spazio, attieniti alla
seguente procedura:</p>
<ol>
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Account e supporto ** ![Account e supporto](images/account_support.svg), quindi seleziona **Gestisci organizzazioni**.</li>
<li>Fai clic su **Crea uno spazio** seguendo il nome dell'organizzazione e attieniti alle istruzioni per creare il tuo spazio.</li>
</ol>
</li>
<li>Invito di utenti a uno spazio
<p>Puoi invitare degli utenti alla tua organizzazione come collaboratori. Puoi anche aggiungere
degli utenti della tua organizzazione a spazi differenti. Gli utenti possono accedere solo allo
spazio al quale sono stati aggiunti. Per aggiungere un utente a uno spazio, attieniti alla seguente procedura:</p>
<ol>
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Gestisci organizzazioni**.Fai quindi clic su **Aggiungi utente** nella tua organizzazione e attieniti alle richieste che ti vengono presentate per aggiungere l'utente alla tua organizzazione.</li>
<li>Aggiungi l'utente a uno spazio. Seleziona lo spazio dal riquadro di navigazione, fai clic su **Aggiungi utente** e attieniti alle istruzioni per aggiungere l'utente allo spazio.</li>
</ol>
</li>
<li>Modifica dei ruoli utente
<p>Per modificare i ruoli utente, attieniti alla seguente procedura: </p>
<ol>
<li>Dall'interfaccia utente {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Account e supporto** ![Account e supporto](images/account_support.svg), quindi seleziona **Gestisci organizzazioni**.</li>
<li>Nella scheda **UTENTI** seleziona la casella di spunta **GESTORE**, **GESTORE FATTURAZIONE** o **REVISORE** per modificare i ruoli degli utenti nella tua organizzazione. Oppure, seleziona uno spazio dal riquadro di navigazione e seleziona la casella di spunta **GESTORE**, **SVILUPPATORE** o **REVISORE** nella scheda **UTENTI** per modificare i ruoli degli utenti nello spazio. </li>
<li>Fai clic su **SALVA**.</li>
</ol>
</li>
<li>Eliminazione di un'organizzazione esistente
<p>Per eliminare la tua organizzazione, contatta il supporto delle registrazioni e degli ID {{site.data.keyword.Bluemix_notm}}.</p>
<p>**Nota**: le operazioni di eliminazione sono irreversibili. Perdi tutte le applicazioni e tutti i servizi associati all'organizzazione.</p>
</li>
</ul>

## Gestione di {{site.data.keyword.Bluemix_notm}} locale e {{site.data.keyword.Bluemix_notm}} dedicato
{: #mng}

Se disponi dell'accesso come amministratore per {{site.data.keyword.Bluemix_notm}} locale o {{site.data.keyword.Bluemix_notm}} dedicato, vai alla pagina **Amministrazione** per gestire risorse, monitorare l'utilizzo delle quote, amministrare le autorizzazioni utente, pianificare le notifiche di aggiornamento, visualizzare i report e i log sulla sicurezza e altro. Puoi gestire le tue organizzazioni creando degli spazi e impostando dei ruoli e delle autorizzazioni per gli utenti; vedi [Gestione delle tue organizzazioni](index.html#orgmng).
{:shortdesc}

*Tabella 1. Attività amministrative per la gestione della tua istanza di {{site.data.keyword.Bluemix_notm}} locale o dedicato*

| Quali operazioni posso eseguire? | Dettagli |    
|----------------|---------|
|Monitorare l'utilizzo del sistema | Fai clic su **AMMINISTRAZIONE &gt; UTILIZZO**. Visualizza le informazioni di sistema, monitora l'utilizzo della CPU e pianifica l'utilizzo per ottimizzare il processo decisionale per la tua azienda.|
|Gestire il tuo catalogo | Fai clic su **AMMINISTRAZIONE &gt; GESTIONE CATALOGO**. Gestisci i servizi visibili agli utenti.|
|Amministrare le organizzazioni | Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE ORGANIZZAZIONI**. Crea organizzazioni, monitora le quote per le organizzazioni e prendi decisioni rapide basate sulle esigenze.|
|Creare spazi e assegnare i ruoli utente | Fai clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Gestisci organizzazioni**. Crea spazi all'interno delle tue organizzazioni. Aggiungi utenti e assegna loro dei ruoli per l'organizzazione e lo spazio. |
|Gestire le autorizzazioni degli utenti amministrativi | Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE UTENTI**. Aggiungi e rimuovi utenti e modifica le autorizzazioni utente. |
|Esaminare report e log | Fai clic su **AMMINISTRAZIONE &gt; REPORT E LOG**. Visualizza i report di sicurezza e i log di controllo relativi alla tua istanza.|
|Visualizzare le informazioni di sistema.  | Fai clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA**. Visualizza le informazioni di sistema, ad esempio aggiornamenti in sospeso, nome e versione della tua istanza, regione, URL API, URL CLI, dettagli di configurazione LDAP, associazioni di gruppi e utenti, statistiche e domini condivisi.  |

### Visualizzazione delle informazioni sul sistema
{: #oc_system}

Per visualizzare le informazioni sul sistema, fai clic su **AMMINISTRAZIONE &gt; INFORMAZIONI DI SISTEMA**.

Puoi espandere e visualizzare diverse sezioni relative ad aggiornamenti in sospeso, informazioni generali sul sistema e dettagli della configurazione LDAP.

* Nella sezione Aggiornamenti, puoi visualizzare gli eventuali aggiornamenti in sospeso che richiedono un tuo intervento. Puoi anche tenere facilmente traccia dei tuoi aggiornamenti utilizzando il link di calendario per importare i tuoi aggiornamenti pianificati in un'applicazione calendario.

<ol>
<li>Per intervenire per uno specifico aggiornamento, completa questa procedura:
<ol type="a">
<li>Fai clic su <strong><em>Numero</em> aggiornamenti in sospeso</strong> per visualizzare tutti
gli aggiornamenti in sospeso.</li>
<li>Seleziona un aggiornamento per intervenire o per visualizzare i relativi dettagli, che
includono la finestra di aggiornamento, la data pianificata e lo stato di interruzione del servizio.</li>
<li>Fai clic su <strong>IMPOSTA DATE NON DISPONIBILI</strong> per impostare degli specifici giorni nella finestra
di aggiornamenti che non siano opportuni per l'applicazione dell'aggiornamento. Se imposti delle date non disponibili, IBM approva
e pianifica il tuo aggiornamento in base alle tue selezioni. Ricevi una notifica quando l'aggiornamento viene approvato e pianificato.</li>
<li>Fai clic su <strong>APPROVA</strong> per approvare l'aggiornamento, se non hai alcuna data non disponibile. Se approvi, l'aggiornamento viene applicato durante la finestra di aggiornamento pianificata. IBM invia una notifica quando la distribuzione dell'aggiornamento inizia e finisce.</li>
</ol>
</li>
<li>Per importare i tuoi aggiornamenti pianificati in un'applicazione calendario a tua scelta, completa la seguente procedura:
<ol type="a">
<li>Apri la tua applicazione calendario.</li>
<li>Importa il calendario degli aggiornamenti incollando l'**URL calendario** elencato nella pagina Informazioni di sistema nella tua applicazione. In alternativa, scarica il file calendario facendo clic sull'URL calendario e importalo quindi nella tua applicazione calendario utilizzando il file `.ics`.</li>
<li>Immetti le tue credenziali.</li>
<li>Visualizza i tuoi aggiornamenti pianificati.</li>
</ol>
</li>
</ol>

* Nella sezione di informazioni generali, puoi visualizzare le seguenti informazioni:
    * Le informazioni di base sulla build {{site.data.keyword.Bluemix_notm}}.
    * Le informazioni sull'API, compresi versione, URL, regione e un link alla documentazione della CLI.
    * Le informazioni sul dominio condiviso relative al tuo sistema e al tuo servizio.
    * Le statistiche sul numero totale di applicazioni, utenti e organizzazioni.
* Nella sezione Dettagli di configurazione LDAP, puoi selezionare il server LDAP
e visualizzare le informazioni relative alle associazioni di utenti e gruppi. Se stai utilizzando {{site.data.keyword.IBM}} WebID, è indicato nella sezione Dettagli di configurazione LDAP.

### Visualizzazione delle informazioni sull'utilizzo
{: #oc_resource}

Per visualizzare le informazioni sulle risorse, fai clic su **AMMINISTRAZIONE &gt; UTILIZZO**.

Nella sezione di monitoraggio delle risorse, puoi visualizzare le seguenti informazioni:

* Informazioni sull'utilizzo delle risorse, ad esempio la quantità di GB di memoria e di GB di spazio su disco
utilizzata. Puoi visualizzare l'utilizzo della CPU calcolato come media su tutti i DEA (droplet execution agent). Fai clic
sul tile **CPU**, per potere così visualizzare l'utilizzo della CPU per ogni DEA. Il DEA con
l'utilizzo più elevato è elencato per primo; ognuno di essi è identificato dal relativo lavoro e indirizzo IP. L'utilizzo
della CPU è separato in tre categorie che includono la quantità di CPU impiegata nei processi di sistema, quella
impiegata nei processi utente e quella impiegata nei processi in attesa.
* Informazioni sull'utilizzo della rete per la larghezza di banda in entrata e in uscita, nel corso del giorno, settimana o
mese precedente.
I dati visualizzati sono basati sulla somma del traffico in entrata e in uscita per la rete pubblica e quella privata.
* Il tempo di risposta medio per {{site.data.keyword.Bluemix_notm}} nel corso degli ultimi 10 minuti, dell'ultima ora e dell'ultimo giorno.
* Le transazioni medie al secondo per {{site.data.keyword.Bluemix_notm}} nel corso degli ultimi 10 minuti, dell'ultima ora e dell'ultimo giorno.

### Visualizzazione dei report
{: #oc_report}

Puoi visualizzare i report e i log di sicurezza, quali DataPower&trade;, firewall e controllo accessi, per la tua istanza {{site.data.keyword.Bluemix_notm}}.

Per visualizzare report e log, fai clic su **AMMINISTRAZIONE &gt; REPORT E LOG**.

Seleziona dalle seguenti opzioni:

* Puoi selezionare le date di inizio e di fine dai campi per filtrare i report e i log da
visualizzare.
* Puoi espandere e visualizzare i diversi report dal riquadro di navigazione.
* Puoi effettuare ricerche nella tua raccolta di report e log. La ricerca si applica ai nomi di report e al contenuto testuale
all'interno di report e log. Puoi anche scegliere di filtrare la ricerca in base
agli **Eventi di amministrazione**, ai **Report DataPower**, al **Firewall** e al **Controllo accessi**.
* Durante la visualizzazione di un report o log, puoi fare clic sull'icona ![Download](images/icon_download.svg)
per scaricare il report.

### Visualizzazione dello stato
{: #oc_status}

Puoi monitorare lo stato per la tua istanza {{site.data.keyword.Bluemix_notm}} utilizzando la pagina Stato di {{site.data.keyword.Bluemix_notm}}. La pagina Stato è la posizione centrale per trovare notifiche e annunci sugli eventi chiave che interessano la piattaforma {{site.data.keyword.Bluemix_notm}} e i servizi principali in {{site.data.keyword.Bluemix_notm}}.

Puoi sottoscrivere a un feed RSS per le notifiche in modo da non doverle controllare personalmente. Per ulteriori informazioni sulla pagina Stato e sulla configurazione del feed RSS, vedi [Visualizzazione di {{site.data.keyword.Bluemix_notm}}](../troubleshoot/getting_customer_support.html#status).

### Gestione del tuo catalogo
{: #oc_catalog}

Puoi gestire quali servizi e starter {{site.data.keyword.Bluemix_notm}} sono visibili agli utenti nel Catalogo {{site.data.keyword.Bluemix_notm}}. Fai clic su **AMMINISTRAZIONE &gt; GESTIONE CATALOGO**.

Seleziona un tile di servizio o di starter per modificare la visibilità del piano di servizio o starter. Per modificare la
visibilità, seleziona dalle seguenti opzioni:
* Per visualizzare il servizio o lo starter nascosto in modo che sia visibile ai tuoi utenti nel Catalogo,
seleziona **ABILITA TUTTI I PIANI**.
* Per nascondere il servizio o lo starter ai tuoi utenti nel Catalogo {{site.data.keyword.Bluemix_notm}},
seleziona **DISABILITA TUTTI I PIANI**.
* Per controllare la visibilità di un singolo piano, seleziona il nome del piano e utilizza quindi
il menu a discesa per selezionare **Abilita per tutte le organizzazioni**, **Disabilita per
tutte le organizzazioni** o **Abilita piano per specifiche organizzazioni**.

### Amministrazione delle organizzazioni
{: #oc_organizations}

Puoi gestire le tue organizzazioni attraverso la creazione e l'eliminazione di organizzazioni, l'aggiunta di gestori alle organizzazioni e il monitoraggio dell'utilizzo delle quote.

Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE ORGANIZZAZIONI**. 

Puoi espandere e visualizzare le diverse sezioni. Puoi anche riesaminare e gestire i piani di quota per le tue organizzazioni.

* Per creare una nuova organizzazione e aggiungere dei gestori, fai clic su <strong>CREA ORGANIZZAZIONE</strong>.
Immetti un nome per l'organizzazione, quindi immetti il nome o l'email della persona che vuoi aggiungere come gestore. Puoi aggiungere più di un gestore immettendo e selezionando più nomi. Fai clic su <strong>CREA ORGANIZZAZIONE</strong> per salvare le tue modifiche e creare l'organizzazione.
* Nella sezione Monitoraggio quota, puoi espandere la sezione e visualizzare le seguenti informazioni:
    * Utilizzo della memoria dell'ambiente. Questa sezione mostra in dettaglio l'utilizzo della memoria per l'intero ambiente di sistema.
	Il grafico fornisce informazioni che includono la memoria di sistema utilizzata, la memoria totale di sistema, la quota utilizzata e la quota totale assegnata. Il seguente elenco di termini definisce i tipi di utilizzo di memoria visualizzati nel grafico.
	<dl>
	<dt><strong>Memoria di sistema utilizzata</strong></dt>
	<dd>La memoria fisica utilizzata dal tuo ambiente.</dd>
	<dt><strong>Memoria totale di sistema</strong></dt>
	<dd>La memoria fisica totale disponibile nel tuo ambiente.</dd>
	<dt><strong>Quota distribuita</strong></dt>
	<dd>La somma di memoria assegnata per tutte le applicazioni distribuite, su tutte le organizzazioni. La somma
	della quota distribuita può superare la memoria totale di sistema fisica per il tuo ambiente. Ad esempio,
se disponi di una memoria totale di sistema pari a 16 GB e assegni 4 GB di memoria ciascuna per un totale di cinque diverse organizzazioni, la quota totale supera la
memoria di sistema totale che ti è stata assegnata per tutte le organizzazioni. Tuttavia, in molti casi,
è possibile che le organizzazioni non utilizzino la quota totale assegnata singolarmente a ciascuna di esse. Inoltre, è possibile che le organizzazioni non utilizzino contemporaneamente
la propria assegnazione di quota totale della memoria. </dd>
	<dt><strong>Quota totale</strong></dt>
	<dd>La memoria totale assegnata su tutte le organizzazioni.</dd>
	</dl>
	* Utilizzo della memoria dell'organizzazione. Questa sezione mostra in dettaglio l'utilizzo della memoria a livello di organizzazione. Puoi visualizzare
la quota totale consentita e la quota che viene distribuita per ogni organizzazione. Il grafico fornisce informazioni che vengono elencate
in base all'utilizzo massimo della memoria per ogni organizzazione e, per impostazione predefinita, viene elencata per prima l'organizzazione che utilizza la maggiore quantità di memoria. Puoi ordinare per **Utilizzo massimo memoria** e **Assegnazione memoria in eccesso**.
	<dl>
	<dt><strong>Utilizzo massimo memoria</strong></dt>
	<dd>Usa questa opzione per identificare l'organizzazione che utilizza la maggior quantità di memoria. Ordina per Utilizzo
	massimo memoria per identificare le organizzazioni che stanno utilizzando la maggiore quantità di
memoria. L'elenco viene ordinato in base alla quota distribuita. </dd>
	<dt><strong>Assegnazione memoria in eccesso</strong></dt>
	<dd>Usa questa opzione per identificare le organizzazioni che hanno un piano di quota superiore a quello necessario.
	Ordina per Assegnazione memoria in eccesso per identificare le organizzazioni che utilizzano
la minore quantità di memoria per la quota assegnata per l'organizzazione. </dd>
	</dl>
* Per modificare il piano di quota per un'organizzazione, fai clic sulla barra del grafico
relativo all'organizzazione che vuoi modificare nella sezione Utilizzo della memoria dell'organizzazione o seleziona il nome dell'organizzazione dalla sezione Elenco organizzazioni. Nella pagina Modifica organizzazione, puoi modificare il piano di quota, modificare il nome dell'organizzazione e aggiungere o rimuovere gestori. Se selezioni un piano di quota che non è sufficiente per l'utilizzo corrente per l'organizzazione, riceverai un messaggio. Per salvare le eventuali modifiche che hai apportato nella pagina Modifica organizzazione,
fai clic su **SALVA**.
* Nella sezione Elenco organizzazioni, puoi visualizzare tutte le organizzazioni nell'ambiente {{site.data.keyword.Bluemix_notm}}.
	* Per eliminare l'organizzazione, fai clic su ![Elimina](images/icon_trash.svg) nella colonna Azioni.
	* Per visualizzare e modificare il piano di quota per un'organizzazione, fai clic sul nome per l'organizzazione nell'elenco.
	* Per modificare il nome dell'organizzazione e aggiungere o rimuovere gestori, fai clic sul nome per l'organizzazione nell'elenco.

### Gestione di utenti e autorizzazioni
{: #oc_useradmin}

Puoi aggiungere degli utenti alla tua istanza {{site.data.keyword.Bluemix_notm}} dal registro utenti della tua azienda tramite LDAP. Puoi aggiungere gli utenti singolarmente
o in gruppi e visualizzarne le autorizzazioni. Se disponi dell'autorizzazione `ammin`,
puoi anche impostare e gestire le autorizzazioni per gli altri utenti. Fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE UTENTI**. 

La pagina Amministrazione utenti visualizza tutti gli utenti per l'istanza locale o dedicata.
Sono visualizzate le autorizzazioni per ciascun utente. Le autorizzazioni possono essere: Nessuna,
`Ammin`, `Catalogo`, `Accesso`,
`Report` e `Utenti`. È possibile abilitare le autorizzazioni oppure
è possibile fornire agli utenti la capacità di `visualizzazione` o di `scrittura` per
l'autorizzazione indicata, come rappresentato dalle icone. Consulta [Autorizzazioni](#permissions) per delle descrizioni di
ciascun tipo e una spiegazione delle icone.

Scegli tra le seguenti opzioni:
* Individuare utenti. Puoi individuare gli utenti nella tabella utilizzando il campo
**Ricerca**.
* Aggiungere utenti. Se disponi dell'autorizzazione `ammin` o
dell'autorizzazione `utenti` con la capacità di `scrittura`, puoi aggiungere gli utenti. Per aggiungere un utente o un gruppo di utenti, fai clic su **AGGIUNGI SINGOLO UTENTE** o **AGGIUNGI GRUPPO
DI UTENTI**. Nel campo **Ricerca**, immetti un nome utente o nome gruppo da
ricercare, quindi seleziona l'organizzazione a cui aggiungere l'utente o il gruppo di utenti
dall'elenco **Organizzazione**. Una volta trovato l'utente o il gruppo che desideri aggiungere,
fai clic sul nome utente e quindi su **AGGIUNGI UTENTE** o **AGGIUNGI UTENTI**.
I gruppi di più di 50 utenti vengono aggiunti attraverso un processo batch in background. Se l'operazione di aggiunta viene
completata correttamente, l'utente o il gruppo viene aggiunto alla tabella per consentirti operazioni di visualizzazione e ricerca. Quando gli utenti vengono aggiunti,
non dispongono di autorizzazioni.
* Modificare autorizzazioni e organizzazioni. Se disponi dell'autorizzazione `ammin`, puoi modificare
le autorizzazioni e le organizzazioni per gli altri utenti. Per modificare le autorizzazioni, individua
l'utente e fai clic sul nome utente. Per abilitare o disabilitare autorizzazioni, seleziona dalle seguenti opzioni nella finestra che viene visualizzata:
	* Seleziona **Attivo** dall'elenco per abilitare un'autorizzazione.
	* Seleziona **Lettura** dall'elenco per consentire all'utente di disporre
della capacità di `visualizzazione` (sola lettura) per tale autorizzazione oppure **Scrittura**
per consentire la capacità di `scrittura` (modifica o aggiunta e rimozione) per l'autorizzazione.
	* Seleziona **Disattivo** per disabilitare l'autorizzazione.
Per modificare le organizzazioni, seleziona dalle seguenti opzioni:
	* Aggiungi l'utente a un'organizzazione utilizzando il campo di ricerca per individuare un'organizzazione, facendo clic per
selezionare dalle opzioni e facendo clic su **AGGIUNGI**.
	* Rimuovi un utente da un'organizzazione facendo clic sull'icona ![Rimuovi, rappresentato da un segno meno](images/icon_remove.svg).
Al termine, fai clic su **SALVA**.
* Rimuovere utenti. Se disponi dell'autorizzazione `ammin` o
dell'autorizzazione `utenti` con la capacità di `scrittura`, puoi rimuovere
gli utenti.
Per rimuovere un utente, individualo e fai clic sull'icona ![Elimina](images/icon_trash.svg) e quindi su **Rimuovi**.

### Autorizzazioni
{: #permissions}

È possibile assegnare agli utenti le seguenti autorizzazioni:

| **Autorizzazione utente** | **Descrizione** |       
|-----------------|-------------------|
| Ammin | Gli utenti con l'autorizzazione `ammin` possono
modificare le autorizzazioni per gli altri utenti. |
| Catalogo | Agli utenti con l'autorizzazione `catalogo` può essere assegnata la capacità di `visualizzare` o `scrivere` (modificare) quali servizi sono disponibili nell'istanza locale o dedicata. |  
| Accesso | Agli utenti con l'autorizzazione `accesso` è consentito visualizzare la pagina Amministrazione. Senza questa autorizzazione, gli utenti non possono vedere l'opzione di menu Amministrazione.  |
| Report | Agli utenti con l'autorizzazione `report` può essere assegnata la capacità di
`visualizzare` o `scrivere` (modificare) i report di sicurezza. |
| Utenti | Agli utenti con l'autorizzazione `utenti` può essere assegnata la capacità
di `visualizzare` l'elenco di utenti o di `scrivere` (aggiungere o rimuovere) gli utenti. Questa autorizzazione non ti consente di impostare le autorizzazioni per gli altri utenti.|

*Tabella 2. Autorizzazioni*

È possibile abilitare le autorizzazioni oppure è possibile fornire agli utenti la capacità di `visualizzazione` o
di `scrittura` per l'autorizzazione indicata, come rappresentato dalle seguenti icone:

* L'icona ![Abilitato, rappresentata da un segno di spunta](images/icon_enabled.svg) accanto a un'autorizzazione significa che essa è abilitata.
* L'icona ![Visualizza, rappresentata da un occhio](images/icon_read.svg) significa che l'utente dispone della capacità di `visualizzazione` (sola lettura) per tale
autorizzazione.
* L'icona ![Scrittura, rappresentata da una matita](images/icon_write.svg) significa che l'utente dispone della capacità di `scrittura` (modifica, aggiunta o rimozione) per tale
autorizzazione.

### Gestione degli utenti con la API REST Admin
{: #usingadminapi}

Puoi utilizzare l'API REST `Admin` per aggiungere e rimuovere utenti per l'istanza {{site.data.keyword.Bluemix_notm}}.
Gli endpoint della API REST `Admin` e le risposte JSON sono fornite su base sperimentale per abilitare le operazioni di base da una riga di comando. Gli endpoint e gli URL negli esempi nelle presenti
informazioni possono variare o potrebbero essere abbandonate con breve preavviso.

I seguenti strumenti sono prerequisiti per utilizzare gli esempi di seguito riportati. Puoi anche scegliere di
            utilizzare altri strumenti.
* cURL, per immettere richieste API REST come comandi. cURL è un programma di utilità gratuito che puoi
                    utilizzare per inviare richieste HTTP a un server e ricevere le risposte
                    attraverso un'interfaccia riga di comando. Puoi scaricare
cURL dal [sito cURL/Download](http://curl.haxx.se/download.html){: new_window}.
* Python, per utilizzare lo strumento JSON Pretty-Print Python. Questo strumento
facoltativo prende il testo JSON come input e fornisce un output facile da leggere. Puoi scaricare Python dal sito [Downloads di Python](https://www.python.org/downloads){: new_window}.

#### Accesso alla Console di gestione

Prima di poter eseguire qualsiasi richiesta API `Admin`,
devi eseguire l'accesso alla Console di gestione. Se disponi dell'autorizzazione `ammin`
o dell'autorizzazione `utenti` con la capacità di `scrittura`,
puoi aggiungere o rimuovere utenti. Per modificare le autorizzazioni di altri utenti devi disporre
dell'autorizzazione `ammin`.

Per accedere alla Console di gestione, puoi utilizzare l'autenticazione di accesso di base sull'endpoint `https://<il_tuo_host>.ibm.com/login`. Il server restituisce un cookie con la tua sessione. Puoi utilizzare tale
cookie per tutte le operazioni con la Console di gestione.

**Nota:** la sessione diventa non valida se non viene utilizzata per qualche ora.

Per accedere alla
Console di gestione, esegui questo comando:

`curl --user <id_utente>:<password> -c ./cookies.txt --header "Accept: application/json" https://<il_tuo_host>.ibm.com/login | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">--user <em>id_utente</em>:<em>password</em></dt>
<dd class="pd">Accetta l'ID utente e la password e invia un'intestazione di autorizzazione di base.</dd>


<dt class="pt dlterm">-c <em>nomefile</em></dt>
<dd class="pd">Memorizza l'ID utente e la password specificati come un cookie nel file specificato.</dd>


<dt class="pt dlterm">--header</dt>
<dd class="pd">Invia un'intestazione Accept.</dd>

</dl>

Il seguente esempio mostra l'output di questo
                comando:
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*cognome*",
        "givenName": "*nome*"
    }
}
```
{: screen}

#### Elenco delle organizzazioni
{: #listingorg}

Quando aggiungi un utente, devi specificare un'organizzazione. Puoi
utilizzare la API REST `Admin` per elencare tutte le organizzazioni. Devi disporre dell'autorizzazione `utenti` con la capacità di `lettura` per elencare le organizzazioni. Per elencare tutte le organizzazioni, esegui questo comando:

`curl -b ./cookies.txt https://<il_tuo_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>nomefile</em></dt>
<dd class="pd">Passa l'ID utente e la password memorizzati precedentemente
con l'opzione <samp class="ph codeph">-c</samp> nel file al server HTTP come
un cookie.</dd>

</dl>

Per ciascuna organizzazione, i risultati includono le seguenti informazioni:
* `"guid"`, GUID dell'organizzazione
* `"name"`, nome dell'organizzazione

Il seguente esempio mostra l'output di questo
                comando:
```
{
     "resources": [
         {
             "guid": "05af098d-d476-4fb0-8b87-a84350e72af3",
             "name": "org-1"
         },
         {
             "guid": "5129a5a8-37c2-4ee4-a9b2-bebae3531db5",
             "name": "org-2"
         },

		 		 ....

		 ],
		 "total_results": 284
}
```
{: screen}

#### Elenco degli utenti
{: #listingusr}

Puoi determinare se un utente è già stato aggiunto al tuo ambiente {{site.data.keyword.Bluemix_notm}} utilizzando
l'API REST `Admin` per elencare gli utenti registrati. Devi disporre dell'autorizzazione `utenti` con la capacità di `lettura` per elencare le organizzazioni. Per elencare tutti gli utenti, esegui questo comando:

`curl -b ./cookies.txt https://<il_tuo_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>nomefile</em></dt>
<dd class="pd">Passa l'ID utente e la password memorizzati precedentemente
con l'opzione <samp class="ph codeph">-c</samp> nel file al server HTTP come
un cookie.</dd>
</dl>

Per ciascun utente registrato, i risultati includono le seguenti informazioni:
* `"first_name"` (nome) e
                                `"last_name"` (cognome)
* `"user_id"`, ID utente e indirizzo email
* `"guid"`, GUID dell'organizzazione.
* `"permissions"`, ossia le autorizzazioni assegnate all'utente per la Console di gestione.

Il seguente esempio mostra l'output di questo
                comando:

```
{
    "next_url": "/codi/v1/users?results_per_page=100&amp;page=2",
    "prev_url": "",
    "resources": [
        {
            "active": true,
            "created_at": "2015-04-08T17:38:51.788Z",
            "created_by": "",
            "first_name": "some first name",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "some last name",
            "permissions": [
                {
                    "display": "ops.admin"
                },
                {
                    "display": "ops.catalog.write"
                },
                {
                    "display": "ops.reports.write"
                },
                {
                    "display": "ops.catalog.read"
                },
                {
                    "display": "ops.users.write"
                },
                {
                    "display": "ops.reports.read"
                },
                {
                    "display": "ops.login"
                },
                {
                    "display": "ops.users.read"
                }
            ],
            "user_id": "someid@us.ibm.com"
        },
		 		 ...


     }
    ],
    "total_pages": 395,
    "total_results": 39421
}

```
{: screen}

#### Aggiunta di un utente

Puoi utilizzare l'API REST `Admin` per aggiungere utenti all'istanza {{site.data.keyword.Bluemix_notm}}. Per aggiungere utenti devi disporre dell'autorizzazione `utenti`
con la capacità di `scrittura`.

Puoi aggiungere un singolo utente o un elenco di utenti. Puoi aggiungere gli utenti a una singola organizzazione
oppure a più organizzazioni.-->Per aggiungere un utente, devi fornire le seguenti informazioni:

* Nome e cognome dell'utente. Fornisci `"nome"` e `"cognome"` da [Elenco degli utenti](index.html#listingusr).
* Indirizzo email e ID utente: fornisci l'`"id_utente"` da [Elenco degli utenti](index.html#listingusr) sia per l'indirizzo email sia per l'ID utente.
* `"guid"`. Fornisci il GUID dell'organizzazione da [Elenco delle organizzazioni](index.html#listingorg).

Per fornire le informazioni, ti servi di un file JSON.

`curl -b ./cookies.txt https://<il_tuo_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>nomefile</em></dt>
<dd class="pd">Passa l'ID utente e la password memorizzati precedentemente
con l'opzione <samp class="ph codeph">-c</samp> nel file al server HTTP come
un cookie.</dd>
</dl>

<ol>
<li>Crea un file JSON che contiene le informazioni in un formato JSON corretto.
<p>Ad esempio, crea un file denominato `user.json` che presenta
questo contenuto:</p>
<pre>
{
    "members": [
        {
            "emails": [
                "un_id_utente@dominio.com"
            ],
            "first_name": "un_nome",
            "last_name": "un_cognome",
            "user_id": "un_id_utente@dominio.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</pre>
</li>
<li>Pubblica il contenuto del file JSON nell'endpoint dell'utente immettendo il seguente comando:<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<il_tuo_host>.ibm.com/codi/v1/users
</code>
</li>
</ol>

<dl class="parml">

<dt class="pt dlterm">-v </dt>
<dd class="pd">Specifica un output dettagliato.</dd>


<dt class="pt dlterm">-X POST</dt>
<dd class="pd">Specifica una richiesta POST, sovrascrivendo la richiesta GET predefinita.</dd>


<dt class="pt dlterm">-H "Content-Type: application/json"</dt>
<dd class="pd">Specifica l'intestazione content-type, che in questo caso è JSON.</dd>


<dt class="pt dlterm">-d *dati*</dt>
<dd class="pd">Specifica i dati, in questo caso il file `user.json`,
da inviare nella richiesta POST al server HTTP.</dd>

</dl>



Il seguente esempio mostra l'output di questo
                comando:

```
* Connected to localhost (127.0.0.1) port 3000 (#0)
 > POST /codi/v1/users HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 > Content-Type: application/json
 > Content-Length: 333
 >
 * upload completely sent off: 333 out of 333 bytes
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < vary: X-HTTP-Method-Override
 < content-type: application/json
 < date: Wed, 22 Apr 2015 19:32:54 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

#### Rimozione di un utente

Puoi utilizzare l'API REST `Admin` per rimuovere gli utenti dall'istanza {{site.data.keyword.Bluemix_notm}}. Per rimuovere gli utenti registrati devi disporre dell'autorizzazione `utenti` con la capacità di `scrittura`.

Per rimuovere un utente, devi fornire l'ID dell'utente: Immetti il seguente comando:

`curl -v -b ./cookies.txt -X DELETE https://<il_tuo_host>.ibm.com/codi/v1/users?user_id=<un_id_utente@dominio.com>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-X DELETE</dt>
<dd class="pd">Specifica una richiesta DELETE.</dd>
</dl>

Il seguente esempio mostra l'output di questo
                comando:

```
 * connect to ::1 port 3000 failed: Connection refused
 *   Trying 127.0.0.1...
 * Connected to localhost (127.0.0.1) port 3000 (#0)
 > DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 >
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < content-type: application/json
 < date: Wed, 22 Apr 2015 21:01:09 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 1922 msec
 <
 ```
{: screen}

### API del servizio personalizzato
{: #servicebrokerapi}

Sono disponibili tre API che ti consentono di registrare o creare un nuovo servizio, di aggiornare un servizio e di eliminare un servizio.

Tutte le API sono relative a <code>https://opsconsole.&lt;subdomain&gt;.bluemix.net/</code>.

<dl>
<dt><strong>&lt;dominiosecondario&gt;</strong></dt>
<dd>Questo valore è il nome della tua istanza locale o dedicata. Il nome del dominio secondario per la tua istanza {{site.data.keyword.Bluemix}} è stato
assegnato durante l'onboarding.</dd>
</dl>

### Registrazione di un nuovo servizio

Utilizza i seguenti esempi di API e codice per registrare un nuovo servizio.

#### Rotta

```
POST /codi/v1/serviceBrokers
```
{: screen}

#### Richiesta

*Tabella 3. Campi*

| **Nome** | **Descrizione** |
|-----------------|-------------------|
| name | Nome del broker dei servizi. |
| auth_username | Nome utente utilizzato per connettersi al broker dei servizi. |
| auth_password | Password utilizzata per connettersi al broker dei servizi. |
| broker_url | URL utilizzato per connettersi al broker dei servizi. |
| owningOrganization | Organizzazione iniziale per cui aggiungere il servizio nell'elenco elementi consentiti. |

##### Corpo

```
{
  "name" : "Nome del broker dei servizi",
  "auth_username" : "nome utente",
  "auth_password" : "password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

##### Intestazioni

```
Autorizzazione: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Risposta

##### Stato

```
201 Creato
```
{: screen}

##### Corpo

```
{
  "entity": {
    "name": "Nome del broker dei servizi",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "auth_username": "nome utente",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "49f3adcc-ecc2-46fa-83c1-03322f04b3b1",
    "created_at": "2015-12-07T19:51:50Z",
    "updated_at": null,
    "url": "/v2/service_brokers/49f3adcc-ecc2-46fa-83c1-03322f04b3b1"
  }
}
```
{: screen}

### Aggiornamento di un servizio

Utilizza i seguenti esempi di API e codice per aggiornare un servizio.

#### Rotta

`PUT /codi/v1/serviceBrokers`
{: screen}

#### Richiesta

*Tabella 4. Campi*

| **Nome** | **Descrizione** |
|-----------------|-------------------|
| name | Nome del broker dei servizi. Questo nome non può essere modificato dal nome con cui è stato creato il servizio. |
| auth_username | Nome utente utilizzato per connettersi al broker dei servizi. |
| auth_password | Password utilizzata per connettersi al broker dei servizi. |
| broker_url | URL utilizzato per connettersi al broker dei servizi. |
| owningOrganization | Organizzazione iniziale per cui aggiungere il servizio nell'elenco elementi consentiti. |

##### Corpo

```
{
  "name" : "Nome del broker dei servizi",
  "auth_username" : "nome utente",
  "auth_password" : "nuova password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

##### Intestazioni

```
Autorizzazione: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Risposta

##### Stato

```
201 Creato
```
{: screen}

##### Corpo

```
{
  "entity": {
    "name": "Nome del broker dei servizi",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "auth_username": "nome utente",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "2cbdb812-d37f-443b-894a-a96de31e5c38",
    "created_at": "2015-12-07T20:11:08Z",
    "updated_at": "2015-12-07T20:11:19Z",
    "url": "/v2/service_brokers/2cbdb812-d37f-443b-894a-a96de31e5c38"
  }
}
```
{: screen}

### Eliminazione di un servizio

Utilizza i seguenti esempi di API e codice per eliminare un servizio.

*Tabella 5. Parametro*

| **Nome** | **Descrizione** |
|-----------------|-------------------|
| name | Nome del broker dei servizi. Questo nome non può essere modificato dal nome con cui è stato creato il servizio. |

#### Rotta

```
DELETE /codi/v1/serviceBrokers?name=name of service broker
```
{: screen}

#### Richiesta

##### Intestazioni

```
Autorizzazione: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Risposta

##### Stato

```
204 Nessun contenuto
```
{: screen}

### Gestione degli utenti con la CLI cf
{: #usingadmincli}

Puoi gestire gli utenti per il tuo ambiente
{{site.data.keyword.Bluemix_notm}} locale o {{site.data.keyword.Bluemix_notm}} dedicato
utilizzando l'interfaccia riga di comando Cloud Foundry insieme al plug-in
{{site.data.keyword.Bluemix_notm}} Admin CLI. Ad
esempio, puoi aggiungere utenti da un registro LDAP.

Prima di iniziare, installa l'interfaccia riga di comando cf. Il plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI richiede cf versione 6.11.2 o successive. [Scarica
l'interfaccia riga di comando Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window}

**Limitazione:** l'interfaccia riga di comando Cloud Foundry non
è supportata da Cygwin. Utilizza l'interfaccia riga di comando Cloud Foundry
in una finestra riga di comando diversa da quella di Cygwin.

#### Aggiunta del plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI

Dopo aver installato l'interfaccia riga di comandi cf, puoi
aggiungere il plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI.

Completa la seguente procedura per aggiungere il repository e installare
il plug-in:

<ol>
<li>Per aggiungere il repository del plug-in {{site.data.keyword.Bluemix_notm}} Admin, esegui questo comando:<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://opsconsole.&lt;dominiosecondario&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;dominiosecondario&gt;</dt>
<dd class="pd">Dominio secondario dell'URL per la tua istanza {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>
</li>
<li>Per installare il plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI, esegui questo comando:<br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

Per visualizzare un elenco di comandi, immetti il seguente
comando:

`cf plugins`
{: codeblock}

Per ulteriore assistenza per un comando, utilizza l'opzione `-help`.

Per ulteriori informazioni su come utilizzare il plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI, vedi [{{site.data.keyword.Bluemix_notm}} admin](../cli/plugins/bluemix_admin/index.html).
