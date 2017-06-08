---

copyright:

  years: 2015, 2016
lastupdated: "2017-05-17"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Ruoli utente e autorizzazioni
{: #userroles}

Puoi gestire gli utenti attraverso i servizi della piattaforma e dell'infrastruttura {{site.data.keyword.Bluemix_notm}} dalla pagina **Utenti** relativa al tuo account. Da questa pagina, è disponibile anche un link alla pagina Directory team nel caso in cui tu voglia gestire solo l'accesso Cloud Foundry degli utenti della piattaforma alle organizzazioni e agli spazi. Tuttavia, non devi lasciare la pagina Utenti per gestire l'accesso Cloud Foundry.
{:shortdesc}

Per accedere alla pagina Utenti, dal menu {{site.data.keyword.Bluemix_notm}}, fai clic su **Gestione** &gt; **Account** &gt; **Utenti**. I proprietari dell'account eseguono tutte le operazioni sulle organizzazioni e sugli spazi, compresa la gestione degli utenti e dei loro ruoli assegnati. I gestori dell'organizzazione e i gestori dello spazio dispongono anche dell'accesso per gestire i ruoli. 

Se sei un utente aggiunto all'account di un'altra persona e vuoi visualizzare i tuoi ruoli assegnati e le tue autorizzazioni, vai a **Gestisci** &gt; **Sicurezza** &gt; **Identità e accesso** &gt; **Utenti** e fai clic sul tuo nome.

## Ruoli dell'account
{: #userrolesinfo}

A livello di account, esistono due ruoli che abilitano l'accesso a funzioni di gestione dell'account differenti:

| Ruolo dell'account | Autorizzazioni |
|----------------|---------|
|Proprietario | Un proprietario per l'account ha accesso al proprio profilo e dashboard di utilizzo e alle proprie directory di team, informazioni di fatturazione e notifiche di spesa. Dalla pagina Directory team o Utenti,il proprietario può invitare nuovi membri del team e adattare i ruoli. Il proprietario può anche aggiungere dei crediti promozionali, impostare o modificare il limite di fatturazione, impostare l'accesso al servizio e gestire organizzazioni e spazi. |
|Membro | Un membro ha accesso ai proprio limiti di fatturazione, crediti dell'account e profilo e alla propria directory team nell'intestazione {{site.data.keyword.Bluemix_notm}}. Tuttavia, nella pagina directory team, un membro può visualizzare solo i membri del team all'interno dell'account. |
{:caption="Tabella 1. Ruoli e autorizzazioni dell'account" caption-side="top"}

Tutti i nuovi utenti vengono aggiunti come membri dell'account. Puoi assegnare i ruoli organizzazione e spazio agli invitati per abilitare specifiche viste e autorizzazioni in {{site.data.keyword.Bluemix_notm}}. Ai nuovi membri del team aggiunti a un'organizzazione, con l'eccezione di un ambiente locale o dedicato, viene assegnato per impostazione predefinita il ruolo organizzazione di revisore. Per uno specifico spazio, puoi scegliere di assegnare il ruolo di sviluppatore o di revisore agli invitati. Dopo che gli invitati hanno accettato l'invito e si sono uniti a {{site.data.keyword.Bluemix_notm}}, puoi modificarne i ruoli nella pagina Utenti o Directory team.

## Ruoli Cloud Foundry
{: #cfroles}

I ruoli Cloud Foundry includono le autorizzazioni di accesso per le organizzazioni e gli spazi definiti nell'account. I seguenti ruoli possono essere assegnati a livello dell'organizzazione:

| Ruolo organizzazione | Autorizzazioni |
|-------------------|-------------|
|Gestore | I gestori dell'organizzazione possono creare, visualizzare, modificare o eliminare gli spazi nell'organizzazione, visualizzare l'utilizzo e la quota dell'organizzazione, invitare membri del team all'organizzazione, gestire chi ha accesso all'organizzazione e i loro ruoli al suo interno e gestire i domini personalizzati per l'organizzazione. |
|Gestore fatturazione | I gestori fatturazione possono visualizzare le informazioni sull'utilizzo di runtime e servizi per l'organizzazione nella pagina Dashboard di utilizzo.  |
|Revisore | I revisori organizzazione possono visualizzare il contenuto di applicazioni e servizi nell'organizzazione. I revisori possono anche visualizzare gli utenti nell'organizzazione e i ruoli ad essi assegnati, nonché la quota per l'organizzazione. Questo ruolo viene assegnato a tutti gli invitati per impostazione predefinita con l'eccezione degli ambienti locale o dedicato. |
{:caption="Tabella 2. Ruoli e autorizzazioni dell'organizzazione" caption-side="top"}

I seguenti ruoli possono essere assegnati a livello dello spazio:

| Ruolo spazio | Autorizzazioni |
|------------|-------------|
|Gestore | I gestori spazio possono aggiungere utenti esistenti e gestire i ruoli nello spazio. Il gestore spazio può anche visualizzare il numero di istanze, i bind di servizio e l'utilizzo delle risorse per ciascuna applicazione nello spazio. |
|Sviluppatore | Gli sviluppatori spazio possono creare, eliminare e gestire applicazioni e servizi nello spazio. Alcune delle attività di gestione includono la distribuzione di applicazioni, l'avvio e l'arresto di applicazioni, la rinominazione di un'applicazione, l'eliminazione di un'applicazione, la rinominazione di uno spazio, il bind o l'annullamento del bind di un servizio a un'applicazione, la visualizzazione del numero di istanze, i bind di servizi e l'utilizzo di risorse per ciascuna applicazione nello spazio. Inoltre, lo sviluppatore spazio può associare un URL interno o esterno a un'applicazione nello spazio.   |
|Revisore | I revisori spazio hanno un accesso in sola lettura a tutte le informazioni sullo spazio, quali le informazioni sul numero di istanze, i bind di servizio e l'utilizzo di risorse per ciascuna applicazione nello spazio. |
{:caption="Tabella 3. Ruoli e autorizzazioni dello spazio" caption-side="top"}

**Nota**: gli utenti a cui nello spazio è assegnato il ruolo di gestore o sviluppatore possono accedere alla variabile di ambiente VCAP_SERVICES. Tuttavia, un utente a cui è assegnato il ruolo di revisore non può accedere a VCAP_SERVICES.

## Politiche e ruoli per la gestione di identità e accesso
{: #iamusermanpol}

Ai proprietari dell'account viene assegnato automaticamente il ruolo di amministratore di accesso account per la gestione di Identità e accesso che ti consente di assegnare e gestire le politiche di servizio. Questo tipo di controllo di accesso permette l'assegnazione di politiche per ogni servizio o istanza di servizio per consentire livelli di accesso per la gestione delle risorse e degli utenti all'interno del contesto assegnato.

### Politiche di servizio

Una politica assegna uno o più ruoli a una serie di risorse utilizzando una combinazione di attributi per definire la serie di risorse applicabile. Quando assegni una politica a un utente, specifica prima il servizio da assegnare, incluso un'opzione per assegnare tutti i servizi disponibili. Quindi, puoi selezionare anche uno o più ruoli da assegnare. Potrebbero essere disponibili ulteriori opzioni di configurazione, a seconda del servizio che selezioni. 

Puoi assegnare e gestire le politiche se hai il ruolo appropriato. La seguente tabella mostra le attività di gestione della politica e il ruolo richiesto per ognuna di esse.

{: #iamui_table1}

| Azione | Ruolo richiesto |
|----------|---------|
| Creare una politica su un account | Amministratore di accesso account |
| Creare una politica su tutti i servizi in un account | Amministratore di accesso account |
| Creare una politica su tutte le istanze del servizio in un account | Amministratore di accesso account |
| Creare una politica su un servizio in un account | Amministratore di accesso account o amministratore del servizio nell'account |
| Creare un'istanza del servizio | Amministratore o editor di accesso account o amministratore o editor del servizio nell'account |
| Creare una politica su un'istanza del servizio | Amministratore di accesso account o amministratore del servizio nell'account o amministratore dell'istanza del servizio |
{: caption="Tabella 4. Attività amministrative per la gestione delle politiche dei Servizi abilitati per l'accesso e l'identità" caption-side="top"}

### Ruoli delle politiche di servizio
{: #iamusermanrol}

I ruoli sono una raccolta di azioni; le azioni che vengono associate a questi ruoli sono specifiche per servizio. Fai riferimento alla documentazione del servizio selezionato per ulteriori dettagli su quali tipi di azioni sono consentiti da ogni ruolo.

Oltre alle descrizioni dei ruoli fornite nella console, la seguente tabella fornisce gli esempi di alcune attività che gli utenti assegnati ad ogni ruolo possono eseguire a seconda del servizio selezionato. 

{: #iamui_table2}

| Ruolo | Descrizione delle azioni | Azioni di esempio|
|:-----------------|:-----------------|:-----------------|
| Visualizzatore | Esegue le azioni che non modificano lo stato; solo le azioni in lettura | <ul><li>Elenca dispositivi</li><li>Legge l'oggetto di archiviazione</li><li>Esegue query</li><li>Esegue ricerche</li></ul>|
| Editor | Esegue le azioni che modificano la stato e creano o eliminano le risorse secondarie |<ul><li>Crea o elimina le macchine virtuali</li><li>Collega spazio di archiviazione</li><li>Riavvia</li><li>Avvia o arresta</li><li>Rinomina</li></ul> |
| Amministratore | Esegue tutte le azioni, inclusa la capacità di gestire il controllo dell'accesso |<ul><li>Invita utenti</li><li>Crea o elimina le macchine virtuali</li><li>Aggiorna le politiche di accesso utente</li><li>Elenca dispositivi</li><li>Collega spazio di archiviazione</li><li>Riavvia</li><li>Avvia o arresta</li><li>Rinomina</li><li>Esegue il backup e ripristina</li></ul>|
{: caption="Tabella 5. Attività amministrative per la gestione delle politiche dei Servizi abilitati per l'accesso e l'identità" caption-side="top"}

## Autorizzazioni dell'infrastruttura
{: #infrapermissions}

Se disponi dell'accesso per assegnare i ruoli dell'infrastruttura, puoi impostare le seguenti autorizzazioni per l'utente: 

| Autorizzazione infrastruttura | Descrizione delle azioni |
|---------------------------|------------------------|
|Solo visualizzazione | Gli utenti con questa autorizzazione possono soltanto visualizzare gli elementi nel sistema.|
|Utente base | Gli utenti con questa autorizzazione possono eseguire le azioni di base nel sistema, come aggiungere un ticket e gestire i dispositivi. |
|Super utente | Gli utenti con questa autorizzazione possono eseguire tutte le azioni disponibili nel sistema. |
{:caption="Tabella 6. Autorizzazioni dell'infrastruttura" caption-side="top"}

