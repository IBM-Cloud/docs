---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestione di organizzazioni e spazi
{: #orgsspacesusers}
*Ultimo aggiornamento: 16 maggio 2016*

In qualità di proprietario dell'account, puoi gestire le tue organizzazioni andando all'icona **Account e supporto** ![icona Account e supporto](../admin/images/account_support.svg) &gt; pagina **Gestisci organizzazioni**. I gestori dell'organizzazione possono anche utilizzare la pagina Gestisci organizzazioni per gestire le organizzazioni dove sono impostati come gestore.
{:shortdesc}

Le attività di gestione includono quanto segue:

* Creazione di un'organizzazione o di uno spazio
* Rinominazione di un'organizzazione
* Eliminazione di un'organizzazione o di uno spazio esistenti
* Elencazione dei membri del team aggiunti al tuo account o alla tua organizzazione
* Gestione o visualizzazione della quota
* Gestione dei domini personalizzati

## Organizzazioni
{: #orginfo}

Le organizzazioni possono estendersi a più regioni e sono definite dai seguenti elementi:

<dl>
<dt>Membri dei team</dt>
<dd>Il ruolo con l'autorizzazione di base in organizzazioni e spazi. Devi essere assegnato
a un'organizzazione prima che ti possano essere concesse altre autorizzazioni agli
spazi all'interno dell'organizzazione. Per informazioni dettagliate,
consulta [Utenti e ruoli](users_roles.html#userrolesinfo).</dd>
<dt>Domini</dt>
<dd>Fornisci la rotta su internet che è assegnata all'organizzazione. Una rotta ha un dominio secondario e un dominio. Un dominio secondario è di norma il
nome dell'applicazione. Un dominio può essere un dominio di sistema o un dominio personalizzato che hai registrato per la tua applicazione. Vedi [Gestione dei domini personalizzati](orgs_spaces.html#managedomains).<br/>
<p>**Nota**: se aggiungi un dominio personalizzato, devi configurare il server DNS per risolvere il tuo dominio personalizzato per puntare al dominio di sistema {{site.data.keyword.Bluemix_notm}}. In questo modo, quando {{site.data.keyword.Bluemix_notm}} riceve una richiesta per il tuo dominio personalizzato, può correttamente instradarla alla tua applicazione.</p></dd>
<dt>Quota</dt>
<dd>Rappresenta i limiti di risorse per l'organizzazione, compreso il numero di servizi
e la quantità di memoria che può essere assegnata per l'utilizzo da parte dell'organizzazione. Le quote vengono assegnate quando
vengono create le organizzazioni. Applicazioni o servizi in uno spazio dell'organizzazione contribuiscono tutti
all'utilizzo della quota. Con i piani Pagamento a consumo o Sottoscrizione, puoi regolare la tua quota per le applicazioni e i contenitori Cloud Foundry in base al variare delle esigenze della tua organizzazione. Vedi [Gestione della quota](orgs_spaces.html#managequota).</dd>
</dl>

In {{site.data.keyword.Bluemix_notm}}, puoi utilizzare le organizzazioni per abilitare la collaborazione tra i membri del team e per facilitare il raggruppamento
logico di risorse dei progetti nei seguenti modi:

<ul>
<li>Puoi raggruppare un insieme di spazi, applicazioni, servizi, domini, rotte e membri del team nelle organizzazioni.</li>
<li>Puoi gestire l'accesso agli spazi e alle organizzazioni in base ai singoli utenti.</li>
</ul>

Quando crei
un'organizzazione, il suo nome deve essere univoco in {{site.data.keyword.Bluemix_notm}}. Se il nome dell'organizzazione è già utilizzato da un altro utente di {{site.data.keyword.Bluemix_notm}} pubblico, dedicato o locale, devi specificare un nuovo nome. Dopo che hai creato l'organizzazione, ti verrà automaticamente assegnata
l'autorizzazione *Gestore organizzazione*, che ti consente di modificare il nome dell'organizzazione, di aggiungere membri del team e di creare o eliminare spazi nell'organizzazione.

Per eliminare un'organizzazione devi rivolgerti al [Supporto di {{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport){: new_window}. Quando richiedi al team di supporto di eliminare un'organizzazione, vengono eliminati tutti gli spazi, i servizi e le applicazioni al suo interno.

I seguenti [ruoli utente](users_roles.html#userrolesinfo) possono essere assegnati ai membri del team in un'organizzazione:

<ul>
<li>Gestore organizzazione</li>
<li>Gestore fatturazione dell'organizzazione</li>
<li>Revisore organizzazione</li>
</ul>

<!-- Add info on Manage infrastructure option under a space -->

## Spazi
{: #spaceinfo}

In un'organizzazione, puoi utilizzare gli spazi per raggruppare una serie di applicazioni, servizi e membri del team. Gli spazi sono collegati a una specifica
regione in {{site.data.keyword.Bluemix_notm}}.

Dopo che hai aggiunto dei membri del team a un'organizzazione, puoi concedere loro le autorizzazioni agli spazi. Analogamente alle organizzazioni, anche gli spazi hanno una serie di [ruoli utente](users_roles.html#userrolesinfo) con specifiche autorizzazioni che vengono assegnati ai membri del team:

<ul>
<li>Gestore spazio</li>
<li>Sviluppatore spazio</li>
<li>Revisore spazio</li>
</ul>

**Nota**: a un membro del team deve essere assegnata almeno una delle autorizzazioni nello spazio.

## Creazione di organizzazioni e spazi
{: #createorg}

Solo i proprietari di account con degli account Pagamento a consumo possono creare un'organizzazione. Puoi creare un'organizzazione completando la seguente procedura:

1. Vai all'icona **Account e supporto** ![icona Account e supporto](../admin/images/account_support.svg) &gt; pagina **Gestisci organizzazioni**.
2. Fai clic su **Aggiungi una nuova organizzazione**.
3. Immetti il nome dell'organizzazione.
4. Fai clic su **Aggiungi**.

Puoi creare degli spazi nella tua organizzazione; ad esempio,
uno spazio *dev* come un ambiente di sviluppo,
uno spazio *test* come un ambiente di test e uno
spazio *production* come un ambiente di produzione. Puoi quindi associare le tue applicazioni agli spazi. Per creare uno spazio, completa la seguente procedura:

1. Vai all'icona **Account e supporto** ![icona Account e supporto](../admin/images/account_support.svg) &gt; pagina **Gestisci organizzazioni**.
2. Identifica l'organizzazione a cui vuoi aggiungere uno spazio e seleziona **Visualizza dettagli**.
3. Fai clic su **Modifica**.
4. Fai clic su **Aggiungi uno spazio**.
5. Immetti il nome dello spazio.
6. Fai clic su **Aggiungi**.


## Rinominazione di un'organizzazione
{: #orgrename}

Per rinominare la tua organizzazione, attieniti alla seguente procedura:

1. Vai all'icona **Account e supporto** ![icona Account e supporto](../admin/images/account_support.svg) &gt; pagina **Gestisci organizzazioni**.
2. Identifica l'organizzazione che vuoi modificare e seleziona **Visualizza dettagli**.
3. Seleziona **Modifica**.
4. Seleziona **Modifica** per il titolo dell'organizzazione.
5. Immetti il nome della nuova organizzazione.
6. Fai clic su **Salva**.

## Eliminazione di un'organizzazione o di uno spazio esistenti
{: #deleteorgs}

In qualità di proprietario dell'account, puoi rivolgerti al [supporto di {{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport){: new_window} per eliminare un'organizzazione. 

**Nota**: le operazioni di eliminazione sono irreversibili. Perdi tutte le applicazioni e tutti i servizi associati all'organizzazione.

Puoi eliminare uno spazio dalla pagina **Gestisci organizzazioni**:

1. Vai all'icona **Account e supporto** ![icona Account e supporto](../admin/images/account_support.svg) &gt; pagina **Gestisci organizzazioni**.
2. Identifica l'organizzazione che vuoi modificare e seleziona **Visualizza dettagli**.
3. Identifica lo spazio che vuoi eliminare e seleziona **Modifica**.
4. Fai clic su **Elimina il tuo spazio**.

## Elenco dei membri
{: #listmembers}

Per elencare i membri per una specifica organizzazione, completa la seguente procedura:

1. Vai all'icona **Account e supporto** ![icona Account e supporto](../admin/images/account_support.svg) &gt; **Gestisci organizzazioni**.
2. Identifica l'organizzazione per cui vuoi visualizzare i membri e fai clic su **Visualizza dettagli**.
3. Fai clic su **Modifica**.
4. Puoi visualizzare i membri della tua organizzazione e i loro ruoli nella scheda **Utenti**.

Per elencare i membri per uno specifico spazio, completa la seguente procedura:

1. Vai all'icona **Account e supporto** ![icona Account e supporto](../admin/images/account_support.svg) &gt; pagina **Gestisci organizzazioni**.
2. Identifica l'organizzazione per cui vuoi visualizzare i membri e fai clic su **Visualizza dettagli**.
3. Identifica lo spazio per cui vuoi visualizzare i membri e fai clic su **Modifica**.
4. Puoi visualizzare i membri del tuo spazio e i loro ruoli nella scheda **Utenti**.

## Gestione della quota
{: #managequota}

In qualità di proprietario dell'account o di gestore dell'organizzazione, puoi visualizzare la quota assegnata e utilizzata per la tua organizzazione. La quota rappresenta i limiti di risorse per l'organizzazione che viene assegnata quando l'organizzazione viene creata. Applicazioni o servizi in uno spazio dell'organizzazione contribuiscono tutti
all'utilizzo della quota.

Per visualizzare la quota per la tua organizzazione, completa la seguente procedura:

1. Vai all'icona **Account e supporto** ![icona Account e supporto](../admin/images/account_support.svg) &gt; pagina **Gestisci organizzazioni**.
2. Identifica l'organizzazione per cui vuoi visualizzare la quota e fai clic su **Visualizza dettagli**.
3. Fai clic su **Modifica**.
4. Seleziona la scheda **Quota**.

Per aggiornare la quota per la tua organizzazione, devi aprire un ticket di supporto. Per ulteriori informazioni sull'apertura di
un ticket di supporto, vedi [Richiesta di assistenza clienti](../support/index.html#contacting-support). Per ulteriori informazioni
sulla quota per i contenitori, vedi [Quota](../containers/container_creating_ov.html#container_quota) nella documentazione dei contenitori.

## Gestione dei domini
{: #managedomains}

In qualità di proprietario dell'account o di gestore dell'organizzazione, puoi visualizzare il dominio di sistema e aggiungere domini personalizzati per le applicazioni create all'interno di un'organizzazione e dei relativi spazi. In qualità di gestore spazio, la scheda **Domini** per uno spazio è un elenco di sola lettura dei domini assegnati allo spazio. 

1. Vai all'icona **Account e supporto** ![icona Account e supporto](../admin/images/account_support.svg) &gt; pagina **Gestisci organizzazioni**.
2. Identifica l'organizzazione per cui vuoi visualizzare o modificare i domini.
3. Seleziona **Visualizza dettagli** per tale organizzazione.
4. Fai clic su **Modifica**.
5. Fai clic su **Domini**.

Se aggiungi un dominio personalizzato, devi configurare il server DNS per risolvere il tuo dominio personalizzato per puntare al dominio di sistema {{site.data.keyword.Bluemix_notm}}. In questo modo, quando {{site.data.keyword.Bluemix_notm}} riceve una richiesta per il tuo dominio personalizzato, può correttamente instradarla alla tua applicazione. Il dominio di sistema è sempre disponibile per uno spazio e a uno spazio è anche possibile assegnare dei domini personalizzati. Le applicazioni create in uno spazio possono utilizzare qualsiasi dominio elencato per tale spazio. Per ulteriori informazioni sulla creazione e l'utilizzo dei domini personalizzati, consulta [Utilizzo di un dominio personalizzato](../manageapps/updapps.html#domain).
