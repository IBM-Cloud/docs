---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Creazione di organizzazioni e spazi
{: #orgsspacesusers}

In qualità di proprietario dell'account, puoi gestire le tue organizzazioni utilizzando la pagina Gestisci organizzazioni. I gestori dell'organizzazione possono anche utilizzare la pagina Gestisci organizzazioni per gestire le organizzazioni dove sono impostati come gestore.
{:shortdesc}

Per gestire le organizzazioni e gli spazi, dalla barra del menu {{site.data.keyword.Bluemix_notm}}, fai clic su **Gestione** &gt; **Account** &gt; **Organizzazioni**. 

**Nota**: per creare un'organizzazione devi essere il proprietario di un account con pagamento a consumo.

## Creazione di organizzazioni
{: #createorg}

Le organizzazioni possono estendersi a più regioni e sono definite dai seguenti elementi:

<dl>
<dt>Membri dei team</dt>
<dd>Il ruolo con l'autorizzazione di base in organizzazioni e spazi. Devi essere assegnato
a un'organizzazione prima che ti possano essere concesse altre autorizzazioni agli
spazi all'interno dell'organizzazione. Per informazioni dettagliate,
consulta [Utenti e ruoli](/docs/iam/users_roles.html#userrolesinfo).</dd>
<dt>Domini</dt>
<dd>Fornisci la rotta su internet che è assegnata all'organizzazione. Una rotta ha un dominio secondario e un dominio. Un dominio secondario è di norma il
nome dell'applicazione. Un dominio può essere un dominio di sistema o un dominio personalizzato che hai registrato per la tua applicazione. Vedi [Gestione dei domini personalizzati](/docs/admin/manageorg.html#managedomains).<br/>
<p>**Nota:** se aggiungi un dominio personalizzato, devi configurare il server DNS per far sì che il tuo dominio personalizzato punti al dominio di sistema {{site.data.keyword.Bluemix_notm}}. In questo modo, quando {{site.data.keyword.Bluemix_notm}} riceve una richiesta per il tuo dominio personalizzato, può correttamente instradarla alla tua applicazione.</p></dd>
<dt>Quota</dt>
<dd>Rappresenta le risorse disponibili per un'organizzazione, incluso il numero di servizi e la quantità di memoria che può essere assegnata per l'utilizzo da parte dell'organizzazione. Le quote vengono assegnate quando
vengono create le organizzazioni. Qualsiasi applicazione o servizio in uno spazio all'interno dell'organizzazione contribuisce all'utilizzo della quota. Con i piani Pagamento a consumo o Sottoscrizione, puoi regolare la tua quota per le applicazioni e i contenitori Cloud Foundry in base al variare delle esigenze della tua organizzazione. Vedi [Gestione della quota](/docs/admin/manageorg.html#managequota).
<p>**Nota:** in un account Sottoscrizione, la quota corrisponde a un limite definito dall'utente che attiva le notifiche di spesa.</p></dd>
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

Puoi utilizzare il comando [`bx iam org-delete`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam_org_delete) per eliminare le organizzazioni. Quando elimini un'organizzazione, tutti gli
spazi e i servizi e tutte le applicazioni al suo interno vengono eliminati.

I seguenti [ruoli utente](/docs/iam/users_roles.html#userrolesinfo) possono essere assegnati ai membri del team in un'organizzazione:

<ul>
<li>Gestore organizzazione</li>
<li>Gestore fatturazione dell'organizzazione</li>
<li>Revisore organizzazione</li>
</ul>

Solo i proprietari di account con degli account Pagamento a consumo possono creare un'organizzazione. Puoi creare un'organizzazione completando la seguente procedura:

1. Fai clic su **Gestione** &gt; **Account** &gt; **Organizzazioni**.
2. Fai clic su **Aggiungi una nuova organizzazione**.
3. Immetti il nome dell'organizzazione.
4. Fai clic su **Aggiungi**.

<!-- Add info on Manage infrastructure option under a space -->

## Creazione di spazi
{: #spaceinfo}

In un'organizzazione, puoi utilizzare gli spazi per raggruppare una serie di applicazioni, servizi e membri del team. Gli spazi sono collegati a una specifica
regione in {{site.data.keyword.Bluemix_notm}}.

Dopo che hai aggiunto dei membri del team a un'organizzazione, puoi concedere loro le autorizzazioni agli spazi. Analogamente alle organizzazioni, anche gli spazi hanno una serie di [ruoli utente](/docs/iam/users_roles.html#userrolesinfo) con specifiche autorizzazioni che vengono assegnati ai membri del team:

<ul>
<li>Gestore spazio</li>
<li>Sviluppatore spazio</li>
<li>Revisore spazio</li>
</ul>

**Nota**: a un membro del team deve essere assegnata almeno una delle autorizzazioni nello spazio.

Puoi creare degli spazi nella tua organizzazione; ad esempio,
uno spazio *dev* come un ambiente di sviluppo,
uno spazio *test* come un ambiente di test e uno
spazio *production* come un ambiente di produzione. Puoi quindi associare le tue applicazioni agli spazi. Per creare uno spazio, completa la seguente procedura:

1. Fai clic su **Gestione** &gt; **Account** &gt; **Organizzazioni**.
2. Identifica l'organizzazione a cui vuoi aggiungere uno spazio e seleziona **Visualizza dettagli**.
4. Fai clic su **Aggiungi uno spazio**.
5. Immetti il nome dello spazio.
6. Fai clic su **Aggiungi**.
