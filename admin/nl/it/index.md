{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#Amministrazione di {{site.data.keyword.Bluemix_notm}}
{: #administer}
*Ultimo aggiornamento: 18 novembre 2015*

Gestisci le tue organizzazioni, i tuoi spazi e i tuoi utenti assegnati facendo clic su **Account e supporto** &gt; **Gestisci organizzazioni**. Se sei un utente {{site.data.keyword.Bluemix_notm}} locale o {{site.data.keyword.Bluemix_notm}} dedicato, vedi [Gestione di {{site.data.keyword.Bluemix_notm}} locale e {{site.data.keyword.Bluemix_notm}} dedicato](index.html#mng) per ulteriori informazioni sull'amministrazione della tua istanza locale o dedicata.
{:shortdesc}

##Gestione del tuo account
{: #mngacct}

In {{site.data.keyword.Bluemix}}, puoi gestire organizzazioni e spazi, compreso l'accesso degli utenti, e tutto questo dal dashboard nell'interfaccia utente. Puoi anche monitorare il tuo utilizzo e la fatturazione a tuo carico.
{:shortdesc}

###Organizzazioni e spazi
{: #orgsandspaces}

In qualità di gestore dell'organizzazione o proprietario dell'account, puoi utilizzare la pagina Gestisci organizzazioni per visualizzare e gestire le impostazioni dell'organizzazione o dello spazio, incluso l'accesso degli utenti.
Per aprire la pagina Gestisci organizzazioni, nel menu vai a *Account e supporto* &gt; **Gestisci organizzazioni**.

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
visualizzare e gestire gli utenti dell'organizzazione. Puoi anche invitare gli utenti alla tua organizzazione facendo clic sul link **Invita un nuovo utente** nella scheda **Utenti**.
Agli utenti in un'organizzazione possono essere assegnate le seguenti autorizzazioni:

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
problema, consulta il documento relativo all'<a href="../troubleshoot/accessing.html#tr_adduser">impossibilità di aggiungere utenti a un'organizzazione</a>.</p>
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
<li>Aggiungere gli utenti allo spazio e gestire gli utenti.</li>
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
puoi gestire le tue organizzazioni. Le attività di gestione includono la creazione di
un'organizzazione, la rinominazione di un'organizzazione, la creazione di uno
spazio, l'invito di utenti a uno spazio e l'eliminazione di un'organizzazione esistente.

<ul>
<li>Creazione di un'organizzazione
<p>Solo gli utenti con account a pagamento possono creare un'organizzazione. Con un account a pagamento,
puoi creare un'organizzazione attenendoti alla seguente procedura:</p>
<ol>
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona nell'angolo superiore destro e seleziona **Gestisci organizzazioni**.</li>
<li>Fai clic su **Crea un'organizzazione** e attieniti alle richieste che
ti vengono presentate per creare la tua organizzazione.</li>
</ol>
</li>
<li>Rinominazione di un'organizzazione
<p>Per rinominare la tua organizzazione, attieniti alla seguente procedura:</p>
<ol>
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona nell'angolo superiore destro e seleziona **Gestisci organizzazioni**.</li>
<li>Seleziona l'organizzazione che desideri rinominare.</li>
<li>Immetti un nuovo nome nel campo **Organizzazione** e fai
clic su **Salva**.</li>
</ol>
</li>
<li>Elenco dei membri
<p>Attieniti alla seguente procedura per elencare i membri della tua organizzazione o del tuo spazio:</p>
<ol>
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona nell'angolo superiore destro e seleziona **Gestisci organizzazioni**.Puoi visualizzare i membri
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
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona nell'angolo superiore destro e seleziona **Gestisci organizzazioni**.</li>
<li>Fai clic su **Crea uno spazio** sotto al tuo nome organizzazione e attieniti alle richieste che
ti vengono presentate per creare il tuo spazio.</li>
</ol>
</li>
<li>Invito di utenti a uno spazio
<p>Puoi invitare degli utenti alla tua organizzazione come collaboratori. Puoi anche aggiungere
degli utenti della tua organizzazione a spazi differenti. Gli utenti possono accedere solo allo
spazio al quale sono stati aggiunti. Per aggiungere un utente a uno spazio, attieniti alla seguente procedura:</p>
<ol>
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona nell'angolo superiore destro e seleziona **Gestisci organizzazioni**.Fai quindi clic su **Aggiungi utente** nella tua organizzazione e attieniti alle richieste che ti vengono presentate per aggiungere l'utente alla tua organizzazione.</li>
<li>Aggiungi l'utente a uno spazio. Seleziona lo spazio dal riquadro di navigazione di sinistra,
fai clic su **Aggiungi utente** e attieniti alle richieste che ti vengono
presentate per aggiungere l'utente allo spazio.</li>
</ol>
</li>
<li>Eliminazione di un'organizzazione esistente
<p>Per eliminare la tua organizzazione, contatta il supporto delle registrazioni e degli ID {{site.data.keyword.Bluemix_notm}}.</p>
<p>**Nota**: le operazioni di eliminazione sono irreversibili. Perdi tutte le applicazioni e tutti i servizi associati all'organizzazione.</p>
</li>
</ul>

## Gestione di {{site.data.keyword.Bluemix_notm}} locale e {{site.data.keyword.Bluemix_notm}} dedicato
{: #mng}

Utilizza la Console di gestione per gestire risorse, monitorare l'utilizzo, amministrare le autorizzazioni utente e visualizzare report di sicurezza, log, stato e notifiche di upgrade per il tuo ambiente {{site.data.keyword.Bluemix}} locale o dedicato.
{:shortdesc}

### Accesso alla Console di gestione
{: #oc_access}

Puoi accedere alla Console di gestione immettendo il seguente URL:

`https://opsconsole.&lt;dominiosecondario&gt;.bluemix.net/`.

<dl>
<dt><strong>&lt;dominiosecondario&gt;</strong></dt>
<dd>Questo valore è il nome della tua istanza locale o dedicata. Il nome del dominio secondario per la tua istanza {{site.data.keyword.Bluemix}} è stato
assegnato durante l'onboarding.</dd>
</dl>

### Visualizzazione delle informazioni sul sistema
{: #oc_system}

Utilizza la Console di gestione per monitorare le tue informazioni sul sistema.

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
<li>Apri l'applicazione calendario.</li>
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

Utilizza la Console di gestione per monitorare l'utilizzo di risorse e rete.

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
* Puoi espandere e visualizzare i diversi report dal riquadro di navigazione a
sinistra.
* Puoi effettuare ricerche nella tua raccolta di report e log. La ricerca si applica ai nomi di report e al contenuto testuale
all'interno di report e log. Puoi anche scegliere di filtrare la ricerca in base
agli **Eventi di amministrazione**, ai **Report DataPower**, al **Firewall** e al **Controllo accessi**.
* Durante la visualizzazione di un report o log, puoi fare clic sull'icona ![Scarica](images/icon_download.png) nell'angolo superiore destro del report per scaricarlo.

### Visualizzazione dello stato
{: #oc_status}

Puoi monitorare lo stato per la tua istanza {{site.data.keyword.Bluemix_notm}} tramite la
Console di gestione. Inoltre, puoi sottoscrivere un feed RSS per le notifiche in modo da non doverle controllare personalmente.

Per visualizzare lo stato per la tua istanza {{site.data.keyword.Bluemix_notm}}, completa la seguente procedura:

1. Nella Console di gestione nell'angolo superiore destro, fai clic sull'icona **Impostazioni profilo**.

2. Quindi, fai clic su **Stato**.

Viene visualizzata la pagina Stato del sistema. Il riquadro a sinistra visualizza lo stato dei tuoi
runtime e dei tuoi servizi nelle regioni e nella tua istanza {{site.data.keyword.Bluemix_notm}}. Il riquadro a destra mostra
le notifiche.

3. Se hai configurato il tuo browser per i feed RSS, puoi sottoscrivere a un feed RSS delle
notifiche. Individua l'icona ![RSS](images/icon_RSS.png) posta a destra di **AGGIORNAMENTI** nella parte superiore sinistra dell'elenco di
notifiche e seleziona una delle seguenti azioni:

* Trascina l'icona ![RSS](images/icon_RSS.png) nel lettore RSS.
* Fai clic con il tasto destro del mouse sull'icona RSS, seleziona **Copia indirizzo link** e incolla l'URL
nel lettore RSS.

4. Filtra le notifiche da visualizzare. Fai clic su **FILTRO** in alto a
destra dell'elenco di notifiche. Puoi quindi cercare e restringere l'elenco di notifiche immettendo
una parola che ti aspetti di trovare in una notifica, ad esempio "manutenzione". Oppure, puoi
selezionare quali notifiche visualizzare in base a **Tipo**,
**Regione**, **Categoria**, **Data di inizio**
o **Data di fine**.

### Gestione del tuo Catalogo
{: #oc_catalog}

Puoi gestire quali servizi e starter {{site.data.keyword.Bluemix_notm}} sono visibili agli utenti nel Catalogo {{site.data.keyword.Bluemix_notm}}.

Per utilizzare la Console di gestione per gestire il Catalogo, fai clic su **AMMINISTRAZIONE &gt; GESTIONE CATALOGO**.

Seleziona un tile di servizio o di starter per modificare la visibilità del piano di servizio o starter. Per modificare la
visibilità, seleziona dalle seguenti opzioni:
* Per visualizzare il servizio o lo starter nascosto in modo che sia visibile ai tuoi utenti nel Catalogo,
seleziona **ABILITA TUTTI I PIANI**.
* Per nascondere il servizio o lo starter agli utenti nel Catalogo {{site.data.keyword.Bluemix_notm}},
seleziona **DISABILITA TUTTI I PIANI**.
* Per controllare la visibilità di un singolo piano, seleziona il nome del piano e utilizza quindi
il menu a discesa per selezionare **Abilita per tutte le organizzazioni**, **Disabilita per
tutte le organizzazioni** o **Abilita piano per specifiche organizzazioni**.

### Amministrazione delle organizzazioni
{: #oc_organizations}

Puoi gestire le tue organizzazioni attraverso la creazione e l'eliminazione di organizzazioni, l'aggiunta di gestori alle organizzazioni e il monitoraggio dell'utilizzo delle quote.

Per utilizzare la Console di gestione per gestire le tue organizzazioni, fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE ORGANIZZAZIONI**.

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
memoria di sistema totale che ti è stata assegnata per tutte le organizzazioni.  Tuttavia, in molti casi,
è possibile che le organizzazioni non utilizzino la quota totale assegnata singolarmente a ciascuna di esse. Inoltre, è possibile che le organizzazioni non utilizzino contemporaneamente
la propria assegnazione di quota totale della memoria.</dd>
	<dt><strong>Quota totale</strong></dt>
	<dd>    La memoria totale assegnata su tutte le organizzazioni.</dd>
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
	* Per eliminare l'organizzazione, fai clic su ![Elimina](images/icon_trash.png) nella colonna Azioni.
	* Per visualizzare e modificare il piano di quota per un'organizzazione, fai clic sul nome per l'organizzazione nell'elenco.
	* Per modificare il nome dell'organizzazione e aggiungere o rimuovere gestori, fai clic sul nome per l'organizzazione nell'elenco.

### Gestione di utenti e autorizzazioni
{: #oc_useradmin}
Puoi aggiungere degli utenti alla tua istanza {{site.data.keyword.Bluemix_notm}} dal registro utenti della tua azienda tramite LDAP. Puoi aggiungere gli utenti singolarmente
o in gruppi e visualizzarne le autorizzazioni. Se disponi dell'autorizzazione `ammin`,
puoi anche impostare e gestire le autorizzazioni per gli altri utenti.

Per utilizzare la Console di gestione per gestire gli utenti, fai clic su **AMMINISTRAZIONE &gt; AMMINISTRAZIONE UTENTI**.

La pagina Amministrazione utenti visualizza tutti gli utenti per l'istanza locale o dedicata.
Sono visualizzate le autorizzazioni per ciascun utente. Le autorizzazioni possono essere: Nessuna,
`Ammin`, `Catalogo`, `Accesso`,
`Report` e `Utenti`. È possibile abilitare le autorizzazioni oppure
è possibile fornire agli utenti la capacità di `visualizzazione` o di `scrittura` per
l'autorizzazione indicata, come rappresentato dalle icone. Consulta [Autorizzazioni](#permissions) per delle descrizioni di
ciascun tipo e una spiegazione delle icone.

Scegli tra le seguenti opzioni:
* Individuare gli utenti. Puoi individuare gli utenti nella tabella utilizzando il campo **Ricerca**
posto in alto.
* Aggiungi utenti. Se disponi dell'autorizzazione `ammin` o
dell'autorizzazione `utenti` con la capacità di `scrittura`, puoi aggiungere gli utenti. Per aggiungere un utente o un gruppo di utenti, fai clic su **AGGIUNGI SINGOLO UTENTE** o **AGGIUNGI GRUPPO
DI UTENTI**. Nel campo **Ricerca**, immetti un nome utente o nome gruppo da
ricercare, quindi seleziona l'organizzazione a cui aggiungere l'utente o il gruppo di utenti
dall'elenco **Organizzazione**. Una volta trovato l'utente o il gruppo che desideri aggiungere,
fai clic sul nome utente e quindi su **AGGIUNGI UTENTE** o **AGGIUNGI UTENTI**.
I gruppi di più di 50 utenti vengono aggiunti attraverso un processo batch in background. Se l'operazione di aggiunta viene
completata correttamente, l'utente o il gruppo viene aggiunto alla tabella per la visualizzazione e la ricerca. Quando gli utenti vengono aggiunti,
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
	* Rimuovi un utente da un'organizzazione facendo clic sull'icona ![Rimuovi, rappresentato da un segno meno](images/icon_remove.png).
Al termine, fai clic su **SALVA**.
* Rimuovi gli utenti. Se disponi dell'autorizzazione `ammin` o
dell'autorizzazione `utenti` con la capacità di `scrittura`, puoi rimuovere
gli utenti.
Per rimuovere un utente, individualo e fai clic sull'icona ![Elimina](images/icon_trash.png) e quindi su **Rimuovi**.

#### Autorizzazioni
{: #permissions}

È possibile assegnare agli utenti le seguenti autorizzazioni:

| **Autorizzazione utente** | **Descrizione** |
|-----------------|-------------------|
| Ammin | Gli utenti con l'autorizzazione `ammin` possono
modificare le autorizzazioni per gli altri utenti. |
| Catalogo | Agli utenti con l'autorizzazione `catalogo` può essere assegnata la capacità di `visualizzare` o `scrivere` (modificare) quali servizi sono disponibili nell'istanza locale o dedicata.  |
| Accesso | Agli utenti con l'autorizzazione `accesso` è consentito accedere alla Console di gestione. Senza questa autorizzazione, gli utenti non possono accedere. |
| Report | Agli utenti con l'autorizzazione `report` può essere assegnata la capacità di
`visualizzare` o `scrivere` (modificare) i report di sicurezza. |
| Utenti | Agli utenti con l'autorizzazione `utenti` può essere assegnata la capacità
di `visualizzare` l'elenco di utenti o di `scrivere` (aggiungere o rimuovere) gli utenti. Questa autorizzazione non ti consente di impostare le autorizzazioni per gli altri utenti.|

*Tabella 1. Autorizzazioni*

È possibile abilitare le autorizzazioni oppure è possibile fornire agli utenti la capacità di `visualizzazione` o
di `scrittura` per l'autorizzazione indicata, come rappresentato dalle seguenti icone:

* L'icona ![Abilitato, rappresentata da un segno di spunta](images/icon_enabled.png) accanto a un'autorizzazione significa che essa è abilitata.
* L'icona ![Visualizza, rappresentata da un occhio](images/icon_read.png) significa che l'utente dispone della capacità di `visualizzazione` (sola lettura) per tale
autorizzazione.
* L'icona ![Scrittura, rappresentata da una matita](images/icon_write.png) significa che l'utente dispone della capacità di `scrittura` (modifica, aggiunta o rimozione) per tale
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
* `"guid"`. Fornisci il GUID dell'orgnizzazione da [Elenco delle organizzazioni](index.html#listingorg).

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
<code>
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
</code><br/><br/>
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
 &lt; HTTP/1.1 201 Created
 &lt; x-powered-by: Express
 &lt; vary: X-HTTP-Method-Override
 &lt; content-type: application/json
 &lt; date: Wed, 22 Apr 2015 19:32:54 GMT
 &lt; connection: close
 &lt; transfer-encoding: chunked
 &lt; X-Time_Check: Proxy Time: 5612 msec
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
 &gt; DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 &gt; User-Agent: curl/7.37.1
 &gt; Host: localhost:3000
 &gt; Accept: */*
 &gt; Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 &gt;
 &lt; HTTP/1.1 201 Created
 &lt; x-powered-by: Express
 &lt; content-type: application/json
 &lt; date: Wed, 22 Apr 2015 21:01:09 GMT
 &lt; connection: close
 &lt; transfer-encoding: chunked
 &lt; X-Time_Check: Proxy Time: 1922 msec
 &lt;
 ```
{: screen}

### Gestione degli utenti con la CLI cf
{: #usingadmincli}

Puoi gestire gli utenti per il tuo ambiente {{site.data.keyword.Bluemix_notm}}
utilizzando l'interfaccia riga di comando Cloud Foundry insieme al plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI. Ad
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

#### Utilizzo del plug-in {{site.data.keyword.Bluemix_notm}} Admin
CLI

Puoi utilizzare il plug-in {{site.data.keyword.Bluemix_notm}} Admin CLI per aggiungere o rimuovere utenti, assegnare o annullare l'assegnazione degli utenti dalle organizzazioni ed
effettuare altre attività di gestione. Per visualizzare un elenco di comandi, immetti il seguente
comando:

`cf plugins`
{: codeblock}

Per ulteriore assistenza per un comando, utilizza
l'opzione `--help`.

#### Connessione e accesso a {{site.data.keyword.Bluemix_notm}}

Prima di poter utilizzare il plug-in Admin CLI per la gestione degli utenti,
devi connetterti ed effettuare l'accesso.

<ol>
<li>Per stabilire una connessione all'endpoint API {{site.data.keyword.Bluemix_notm}}>, esegui questo comando:<br/><br/>
<code>
cf api https://api.&lt;dominiosecondario&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;dominiosecondario&gt;</dt>
<dd class="pd">Dominio secondario dell'URL per la tua istanza {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>
<p>Puoi controllare l'URL corretto nella pagina Risorse e informazioni della Console di gestione. L'URL viene mostrato
nella sezione Informazioni API all'interno del campo **URL API**.</p>
</li>
<li>Accedi a {{site.data.keyword.Bluemix_notm}} con il seguente comando:<br/><br/>
<code>
cf login
</code>
</li>
</ol>

#### Aggiunta di un utente

Puoi aggiungere un utente al tuo ambiente {{site.data.keyword.Bluemix_notm}} da un registro LDAP. Immetti il seguente comando:

`cf bluemix-admin-add-user <nome_utente> <organizzazione>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nome_utente&gt;</dt>
<dd class="pd">Il nome dell'utente nel registro LDAP.</dd>
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui aggiungere l'utente.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **baau** come un alias per il nome comando **bluemix-admin-add-user** più lungo.

#### Rimozione di un utente

Puoi rimuovere un utente dal tuo ambiente {{site.data.keyword.Bluemix_notm}}
immettendo il seguente comando: 

`cf bluemix-admin-remove-user <nome_utente>`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;nome_utente&gt;</dt>
<dd class="pd">Il nome dell'utente in {{site.data.keyword.Bluemix_notm}}.</dd>

</dl>

**Suggerimento: ** puoi anche utilizzare **baru** come un alias per
il nome comando **bluemix-admin-remove-user** più lungo.

#### Aggiunta ed eliminazione di un'organizzazione

Puoi aggiungere ed eliminare un'organizzazione.

* Per aggiungere un'organizzazione, immetti il seguente comando:

`cf Bluemix-admin-create-organization <organizzazione> <gestore>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o il GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} da aggiungere.</dd>
<dt class="pt dlterm">&lt;gestore&gt;</dt>
<dd class="pd">Il nome utente del gestore per l'organizzazione.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **baco** come un alias per il nome comando **bluemix-admin-create-organization** più lungo.

* Per eliminare un'organizzazione, immetti il seguente comando:

`cf Bluemix-admin-delete-organization <organizzazione>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o il GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} da eliminare.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **bado** come un alias per
il nome comando **bluemix-admin-create-organization** più lungo.

#### Assegnazione di un utente a un'organizzazione

Puoi assegnare un utente nel tuo ambiente {{site.data.keyword.Bluemix_notm}} a una
specifica organizzazione. Immetti il seguente comando:

`cf bluemix-admin-set-org <nome_utente> <organizzazione> [<ruolo>]`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nome_utente&gt;</dt>
<dd class="pd">Il nome dell'utente in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui assegnare l'utente.</dd>
<dt class="pt dlterm">&lt;ruolo&gt;</dt>
<dd class="pd">Vedi [Ruoli](#roles) per i ruoli utente di {{site.data.keyword.Bluemix_notm}} e le relative
descrizioni.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **baso** come un alias per
il nome comando **bluemix-admin-set-org** più lungo.

#### Annullamento dell'assegnazione di un utente da un'organizzazione

Puoi annullare l'assegnazione di un utente del tuo ambiente {{site.data.keyword.Bluemix_notm}}
da una specifica organizzazione. Immetti il seguente comando:

`cf bluemix-admin-unset-org <nome_utente> <organizzazione> [<ruolo>]`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;nome_utente&gt;</dt>
<dd class="pd">Il nome dell'utente in {{site.data.keyword.Bluemix_notm}}.</dd>
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui assegnare l'utente.</dd>
<dt class="pt dlterm">&lt;ruolo&gt;</dt>
<dd class="pd">Vedi [Ruoli](#roles) per i ruoli utente di {{site.data.keyword.Bluemix_notm}} e le relative
descrizioni.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **bauo** come un alias per
il nome comando **bluemix-admin-unset-org** più lungo.

#### Ruoli

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">Gestore organizzazione. Un gestore organizzazione ha l'autorità per svolgere le seguenti azioni:
<ul>
<li>Creare o eliminare spazi all'interno dell'organizzazione.</li>
<li>Invitare gli utenti all'organizzazione e gestirli.</li>
<li>Gestire i domini dell'organizzazione.</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">Gestore fatturazione. Un gestore fatturazione può visualizzare le informazioni relative all'utilizzo di runtime e servizi
per l'organizzazione.</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">Revisore organizzazione. Un revisore organizzazione può visualizzare i contenuti di applicazioni e servizi in uno
spazio.</dd>
</dl>

#### Impostazione di una quota per un'organizzazione

Puoi impostare la quota di utilizzo per una specifica organizzazione.

`cf bluemix-admin-set-quota <organizzazione> <piano>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o il GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} per cui impostare la quota.</dd>
<dt class="pt dlterm">&lt;piano&gt;</dt>
<dd class="pd">Il piano di quota per un'organizzazione.</dd>
</dl>

**Suggerimento:** puoi anche utilizzare **basq** come un alias per il nome comando **bluemix-admin-set-quota** più lungo.

#### Aggiunta, eliminazione e richiamo di report

Puoi aggiungere, eliminare e richiamare report di sicurezza.
* Per aggiungere un report, immetti questo comando:

`cf bluemix-admin-add-report <categoria> <data> <PDF|TXT|LOG> <RTF>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;categoria&gt;</dt>
<dd class="pd">La categoria per il report. Se c'è uno spazio nel nome, racchiudi il nome tra virgolette.</dd>
<dt class="pt dlterm">&lt;data&gt;</dt>
<dd class="pd">La data del report nel formato <samp class="ph codeph">AAAAMMGG</samp>.</dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">Il percorso per il file di log, file di testo o PDF del report da caricare.</dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">Un'opzione per includere una versione RTF (Rich Text Format) del PDF. Questa opzione si
applica solo se hai incluso un percorso al PDF del report. La versione RTF viene utilizzata per l'indicizzazione e la ricerca.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **baar** come un alias per
il nome comando **bluemix-admin-add-report** più lungo.

* Per eliminare un report, immetti questo comando:

`cf bluemix-admin-delete-report <categoria> <data> <nome>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;categoria&gt;</dt>
<dd class="pd">La categoria per il report. Se c'è uno spazio nel nome, racchiudi il nome tra virgolette.</dd>
<dt class="pt dlterm">&lt;data&gt;</dt>
<dd class="pd">La data del report nel formato <samp class="ph codeph">AAAAMMGG</samp>.</dd>
<dt class="pt dlterm">&lt;nome&gt;</dt>
<dd class="pd">Il nome del report.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **badr** come un alias per
il nome comando **bluemix-admin-delete-report** più lungo.

* Per richiamare un report, immetti il seguente comando:

`cf bluemix-admin-retrieve-report <categoria> <data> <nome>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;categoria&gt;</dt>
<dd class="pd">La categoria per il report. Se c'è uno spazio nel nome, racchiudi il nome tra virgolette.</dd>
<dt class="pt dlterm">&lt;data&gt;</dt>
<dd class="pd">La data del report nel formato <samp class="ph codeph">AAAAMMGG</samp>.</dd>
<dt class="pt dlterm">&lt;nome&gt;</dt>
<dd class="pd">Il nome del report.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **barr** come un alias per
il nome comando **bluemix-admin-retrieve-report** più lungo.

#### Abilitazione e disabilitazione dei servizi per tutte le organizzazioni

Puoi abilitare o disabilitare la visualizzazione di un servizio nel Catalogo {{site.data.keyword.Bluemix_notm}} per tutte le organizzazioni.

* Per abilitare la visibilità di un servizio nel Catalogo {{site.data.keyword.Bluemix_notm}} per tutte le organizzazioni, immetti il seguente comando:

`cf bluemix-admin-enable-service-plan <identificativo_piano>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificativo_piano&gt;</dt>
<dd class="pd">Il nome o il GUID del servizio che vuoi abilitare. Se immetti un nome servizio non univoco, ti vengono presentati i piani di servizio da cui scegliere.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **baesp** come un alias per
il nome comando **bluemix-admin-enable-service-plan** più lungo.

* Per disabilitare la visualizzazione di un servizio nel Catalogo {{site.data.keyword.Bluemix_notm}} per tutte le organizzazioni, immetti questo comando:

`cf bluemix-admin-disable-service-plan <identificativo_piano>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificativo_piano&gt;</dt>
<dd class="pd">Il nome o il GUID del servizio che vuoi disabilitare. Se immetti un nome servizio non univoco, ti vengono presentati i piani di servizio da cui scegliere.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **badsp** come un alias per
il nome comando **bluemix-admin-disable-service-plan** più lungo.

#### Aggiunta, rimozione e modifica della visibilità dei servizi per le organizzazioni

Puoi aggiungere o rimuovere un'organizzazione dall'elenco di organizzazioni che possono vedere uno specifico servizio nel Catalogo {{site.data.keyword.Bluemix_notm}}. Puoi anche modificare e sostituire l'elenco di servizi che specifiche organizzazioni possono vedere nel Catalogo {{site.data.keyword.Bluemix_notm}}.

* Per consentire a un'organizzazione di visualizzare uno specifico servizio nel Catalogo {{site.data.keyword.Bluemix_notm}}, immetti questo comando:

`cf bluemix-admin-add-service-plan-visibility <identificativo_piano> <organizzazione>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificativo_piano&gt;</dt>
<dd class="pd">Il nome o il GUID del servizio per cui vuoi aggiungere la visibilità. Se immetti un nome servizio non univoco, ti vengono presentati i piani di servizio da cui scegliere.</dd>
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o il GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} da aggiungere all'elenco di visibilità del servizio.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **baaspv** come un alias per
il nome comando **bluemix-admin-add-service-plan-visibility** più lungo.

* Per rimuovere la visibilità di un servizio nel Catalogo {{site.data.keyword.Bluemix_notm}} per
un'organizzazione, immetti il seguente comando:

`cf bluemix-admin-remove-service-plan-visibility <identificativo_piano> <organizzazione>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;identificativo_piano&gt;</dt>
<dd class="pd">Il nome o il GUID del servizio per cui vuoi rimuovere la visibilità. Se immetti un nome servizio non univoco, ti vengono presentati i piani di servizio da cui scegliere.</dd>
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o il GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} da rimuovere dall'elenco di visibilità del servizio.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **barspv** come un alias per
il nome comando **bluemix-admin-remove-service-plan-visibility** più lungo.

* Per sostituire tutti i servizi visibili esistenti per un'organizzazione o più organizzazioni, utilizza questo comando.

`cf bluemix-admin-edit-service-plan-visibilities <identificativo_piano> <organizzazione_1> <organizzazione_facoltativa_2>`
{: codeblock}

**Nota:** questo comando sostituisce i servizi visibili esistenti per le organizzazioni specificate con il servizio da te specificato nel comando.

<dl class="parml">
<dt class="pt dlterm">&lt;identificativo_piano&gt;</dt>
<dd class="pd">Il nome o il GUID del servizio che vuoi rendere visibile. Se immetti un nome servizio non univoco, ti vengono presentati i piani di servizio da cui scegliere.</dd>
<dt class="pt dlterm">&lt;organizzazione&gt;</dt>
<dd class="pd">Il nome o il GUID dell'organizzazione {{site.data.keyword.Bluemix_notm}} per cui aggiungere la visibilità. Puoi abilitare la visibilità del servizio per più di una singola organizzazione immettendo i GUID o i nomi organizzazione aggiuntivi nel comando.</dd>
</dl>

**Suggerimento: ** puoi anche utilizzare **baespv** come un alias per
il nome comando **bluemix-admin-edit-service-plan-visibility** più lungo.
