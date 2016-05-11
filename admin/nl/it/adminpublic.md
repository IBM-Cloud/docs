---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Amministrazione di 
{: #administer}
*Ultimo aggiornamento: 29 febbraio 2016*

Gestisci le tue organizzazioni, i tuoi spazi e i tuoi utenti assegnati facendo clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Gestisci organizzazioni**. Se sei un utente {{site.data.keyword.Bluemix_notm}} locale o {{site.data.keyword.Bluemix_notm}} dedicato, vedi [Gestione di {{site.data.keyword.Bluemix_notm}} locale e {{site.data.keyword.Bluemix_notm}} dedicato](../admin/index.html#mng) per ulteriori informazioni sull'amministrazione della tua istanza locale o dedicata.
{:shortdesc}

## Gestione di {{site.data.keyword.Bluemix_notm}} pubblico
{: #mngacct}

In {{site.data.keyword.Bluemix}} pubblico, puoi gestire organizzazioni e spazi, compreso l'accesso degli utenti, e tutto questo dal dashboard nell'interfaccia utente. Puoi anche monitorare il tuo utilizzo e la fatturazione a tuo carico.
{:shortdesc}

### Organizzazioni e spazi
{: #orgsandspaces}

In qualità di gestore dell'organizzazione o proprietario dell'account, puoi utilizzare la pagina Gestisci organizzazioni per visualizzare e gestire le impostazioni dell'organizzazione o dello spazio, incluso l'accesso degli utenti. Per aprire la pagina Gestisci organizzazioni, fai clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Gestisci organizzazioni**.

#### Organizzazioni

Un'organizzazione è definita dai seguenti elementi:

<dl>
<dt>Utenti</dt>
<dd>Il ruolo con l'autorizzazione di base in organizzazioni e spazi. Devi essere assegnato
a un'organizzazione prima che ti possano essere concesse altre autorizzazioni agli
spazi all'interno dell'organizzazione. Per informazioni dettagliate,
consulta [Utenti e ruoli](adminpublic.html#userroles).</dd>
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

#### Spazi

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

### Utenti e ruoli
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

#### Ruoli utente

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

**Nota**: gli utenti a cui è stato assegnato il ruolo di manager o sviluppatore possono accedere alla variabile di ambiente VCAP_SERVICES. Se all'utente viene assegnato il ruolo di revisore non può invece accedere a VCAP_SERVICES.

### Gestione delle tue organizzazioni
{: #orgmng}

In qualità di gestore dell'organizzazione o di proprietario dell'account,
puoi gestire le tue organizzazioni. Le attività di gestione includono la creazione di un'organizzazione, la rinominazione di un'organizzazione, la creazione di uno spazio, l'invito di utenti a uno spazio, la modifica dei ruoli utente e l'eliminazione di un'organizzazione esistente.

#### Creazione di un'organizzazione

Solo gli utenti con account a pagamento possono creare un'organizzazione. Con un account a pagamento,
puoi creare un'organizzazione attenendoti alla seguente procedura:

<ol>
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Gestisci organizzazioni**.</li>
<li>Fai clic su **Crea un'organizzazione** e attieniti alle richieste che
ti vengono presentate per creare la tua organizzazione.</li>
</ol>

#### Rinominazione di un'organizzazione

Per rinominare la tua organizzazione, attieniti alla seguente procedura:

<ol>
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Account e supporto** ![Account e supporto](images/account_support.svg), quindi seleziona **Gestisci organizzazioni**.</li>
<li>Seleziona l'organizzazione che desideri rinominare.</li>
<li>Immetti un nuovo nome nel campo **Organizzazione** e fai
clic su **Salva**.</li>
</ol>

#### Elenco dei membri 

Attieniti alla seguente procedura per elencare i membri della tua organizzazione o del tuo spazio:

<ol>
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Account e supporto** ![Account e supporto](../support/images/account_support.svg), quindi seleziona **Gestisci organizzazioni**. Puoi visualizzare i membri
della tua organizzazione e i loro ruolo nella scheda **Utenti**.</li>
<li>Fai clic sul nome dello spazio nella tua organizzazione per visualizzare i membri di questo spazio e i loro ruoli.</li>
</ol>

#### Creazione di uno spazio

Puoi creare degli spazi nella tua organizzazione; ad esempio,
uno spazio *dev* come un ambiente di sviluppo,
uno spazio *test* come un ambiente di test e uno
spazio *production* come un ambiente di produzione. Puoi quindi associare le tue applicazioni agli spazi. Per creare uno spazio, attieniti alla
seguente procedura:

<ol>
<li>Vai al Dashboard {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Account e supporto ** ![Account e supporto](images/account_support.svg), quindi seleziona **Gestisci organizzazioni**.</li>
<li>Fai clic su **Crea uno spazio** seguendo il nome dell'organizzazione e attieniti alle istruzioni per creare il tuo spazio.</li>
</ol>

#### Invito di utenti a uno spazio

Puoi invitare degli utenti ad accedere alle tue organizzazioni e ai tuoi spazi attraverso l'indirizzo e-mail. Gli utenti possono accedere solo allo
spazio al quale sono stati aggiunti. 

A seconda che l'invitato disponga o meno di un ID IBM, gli viene assegnato un ruolo `membro` o `collaboratore` per l'account. La seguente tabella indica dettagliatamente in che modo vengono assegnati i ruoli in base al tipo di invito.

*Tabella 1. Assegnazioni ruoli account*

| **Tipo di e-mail dell'invitato** | **Ruolo account assegnato** | 
|----------------|------------------|
|L'utente dispone di un account IBM ID collegato all'indirizzo e-mail dell'invitato  | Membro  | 
|L'utente non dispone di un ID IBM | Viene creato un ID IBM corrispondente all'indirizzo e-mail inoltrato e l'utente viene aggiunto come membro. | 
|Indirizzo e-mail per un utente {{site.data.keyword.Bluemix_notm}} corrente | Collaboratore | 

Completa la seguente procedura per aggiungere utenti con ruoli assegnati a spazi specifici per un'organizzazione prescelta:

<ol>
<li>Passa a **Account e supporto** &gt; **Account** &gt; **Gestisci organizzazioni**.</li>
<li>Seleziona **Invita utenti**.</li>
<li>Immetti l'indirizzo e-mail della persona che desideri invitare.</li>
<li>Seleziona il ruolo per l'organizzazione a cui prevedi di invitare il nuovo utente.</li>
<li>Seleziona il ruolo per lo spazio a cui prevedi di invitare il nuovo utente.</li>
<li>Seleziona **Invita**.</li>
<li>Visualizza la conferma di invio dell'invito nella sezione **In sospeso**. Seleziona **Reinvia e-mail** o **Annulla invito** per operare su un invito in sospeso.</li>
</ol>

#### Modifica dei ruoli utente

Per modificare i ruoli utente, attieniti alla seguente procedura:

<ol>
<li>Dall'interfaccia utente {{site.data.keyword.Bluemix_notm}}, fai clic sull'icona **Account e supporto** ![Account e supporto](images/account_support.svg), quindi seleziona **Gestisci organizzazioni**.</li>
<li>Nella scheda **UTENTI** seleziona la casella di spunta **GESTORE**, **GESTORE FATTURAZIONE** o **REVISORE** per modificare i ruoli degli utenti nella tua organizzazione. Oppure, seleziona uno spazio dal riquadro di navigazione e seleziona la casella di spunta **GESTORE**, **SVILUPPATORE** o **REVISORE** nella scheda **UTENTI** per modificare i ruoli degli utenti nello spazio. </li>
<li>Fai clic su **SALVA**.</li>
</ol>

#### Eliminazione di un'organizzazione esistente

Per eliminare la tua organizzazione, contatta il supporto delle registrazioni e degli ID {{site.data.keyword.Bluemix_notm}}.

**Nota**: le operazioni di eliminazione sono irreversibili. Perdi tutte le applicazioni e tutti i servizi associati all'organizzazione.

