---

copyright:

  years: 2015, 2016
lastupdated: "2017-03-01"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestione dell'accesso ai servizi Cloud Foundry di utenti e ruoli nella Directory team
{: #userroles}

Puoi gestire l'accesso ai servizi Cloud Foundry agli utenti della piattaforma dalla pagina Directory team del tuo account. Puoi gestire i membri del team esistenti e i loro ruoli nella tua organizzazione o nei tuoi spazi.
{:shortdesc}

Puoi accedere alla Directory team dal tuo account da un link all'inizio della nuova pagina Utenti. Per accedere alla pagina Utenti, dal menu {{site.data.keyword.Bluemix_notm}}, fai clic su **Gestione** &gt; **Account** &gt; **Utenti**.

I proprietari degli account eseguono tutte le operazioni sulle organizzazioni e sugli spazi, compresa la gestione dei membri dei team e dei loro ruoli assegnati. I gestori dell'organizzazione dispongono di un accesso che consente loro di gestire i ruoli. I gestori dello spazio possono utilizzare la pagina
**Gestisci organizzazioni** per aggiungere i membri dell'account esistenti allo spazio e regolare i loro ruoli. Per ulteriori informazioni sui ruoli,
consulta le seguenti informazioni.

## Ruoli utente
{: #userrolesinfo}

A livello di account, esistono due ruoli che abilitano l'accesso a funzioni di gestione dell'account differenti:

| Ruolo dell'account | Autorizzazioni |
|----------------|---------|
|Proprietario | Un proprietario per l'account ha accesso al proprio profilo e dashboard di utilizzo e alle proprie directory di team, informazioni di fatturazione e notifiche di spesa. Dalla pagina directory team, il proprietario può invitare nuovi membri del team e regolare i ruoli. Il proprietario può anche aggiungere dei crediti promozionali, impostare o modificare il limite di fatturazione, impostare l'accesso al servizio e gestire organizzazioni e spazi. |
|Membro | Un membro ha accesso ai proprio limiti di fatturazione, crediti dell'account e profilo e alla propria directory team nell'intestazione {{site.data.keyword.Bluemix_notm}}. Tuttavia, nella pagina directory team, un membro può visualizzare solo i membri del team all'interno dell'account. |
{:caption="Table 1. Account roles and permissions" caption-side="top"}

Tutti i nuovi membri del team vengono aggiunti come un membro dell'account. Puoi assegnare i ruoli organizzazione e spazio agli invitati per abilitare specifiche viste e autorizzazioni in {{site.data.keyword.Bluemix_notm}}. Ai nuovi membri del team aggiunti a un'organizzazione, con l'eccezione di un ambiente locale o dedicato, viene assegnato per impostazione predefinita il ruolo organizzazione di revisore. Per uno specifico spazio, puoi scegliere di assegnare il ruolo di sviluppatore o di revisore agli invitati. Dopo che gli invitati hanno accettato l'invito e si sono uniti a {{site.data.keyword.Bluemix_notm}}, puoi modificarne i ruoli nella pagina Directory team. 

I seguenti ruoli possono essere assegnati a livello dell'organizzazione:

| Ruolo organizzazione | Autorizzazioni |
|-------------------|-------------|
|Gestore | I gestori dell'organizzazione possono creare, visualizzare, modificare o eliminare gli spazi nell'organizzazione, visualizzare l'utilizzo e la quota dell'organizzazione, invitare membri del team all'organizzazione, gestire chi ha accesso all'organizzazione e i loro ruoli al suo interno e gestire i domini personalizzati per l'organizzazione. |
|Gestore fatturazione | I gestori fatturazione possono visualizzare le informazioni sull'utilizzo di runtime e servizi per l'organizzazione nella pagina Dashboard di utilizzo.  |
|Revisore | I revisori organizzazione possono visualizzare il contenuto di applicazioni e servizi nell'organizzazione. I revisori possono anche visualizzare i membri
del team nell'organizzazione e i ruoli ad essi assegnati, nonché la quota per l'organizzazione. Questo ruolo viene assegnato a tutti gli invitati per impostazione predefinita con l'eccezione degli ambienti locale o dedicato. |
{:caption="Table 2. Organization roles and permissions" caption-side="top"}

I seguenti ruoli possono essere assegnati a livello dello spazio:

| Ruolo spazio | Autorizzazioni |
|------------|-------------|
|Gestore | I gestori spazio possono aggiungere membri del team esistenti e gestire i ruoli nello spazio. Il gestore spazio può anche visualizzare il numero di istanze, i bind di servizio e l'utilizzo delle risorse per ciascuna applicazione nello spazio. |
|Sviluppatore | Gli sviluppatori spazio possono creare, eliminare e gestire applicazioni e servizi nello spazio. Alcune delle attività di gestione includono la distribuzione di applicazioni, l'avvio e l'arresto di applicazioni, la rinominazione di un'applicazione, l'eliminazione di un'applicazione, la rinominazione di uno spazio, il bind o l'annullamento del bind di un servizio a un'applicazione, la visualizzazione del numero di istanze, i bind di servizi e l'utilizzo di risorse per ciascuna applicazione nello spazio. Inoltre, lo sviluppatore spazio può associare un URL interno o esterno a un'applicazione nello spazio.   |
|Revisore | I revisori spazio hanno un accesso in sola lettura a tutte le informazioni sullo spazio, quali le informazioni sul numero di istanze, i bind di servizio e l'utilizzo di risorse per ciascuna applicazione nello spazio. |
{:caption="Table 3. Space roles and permissions" caption-side="top"}

**Nota**: ai membri del team a cui nello spazio è assegnato il ruolo di gestore o sviluppatore possono accedere alla variabile di ambiente VCAP_SERVICES. Tuttavia, un membro del team a cui è assegnato il ruolo di revisore non può accedere a VCAP_SERVICES.

## Modifica di ruoli
{: #editinguserroles}

I proprietari dell'account e i gestori dell'organizzazione possono modificare i ruoli di organizzazione e spazio per i membri del team esistenti nella pagina Directory team.

1. Individua e seleziona il membro del team di cui vuoi modificare i ruoli. 
2. Fai clic su **Visualizza ruoli**. 
3. Seleziona o deseleziona le selezioni di ruolo dello spazio per modificare l'accesso allo spazio per il membro del team.
4. Fai clic su **Salva**.

I gestori spazio possono modificare i ruoli per i membri del team nel loro spazio. 

1. Individua e seleziona il membro del team di cui vuoi modificare i ruoli. 
2. Fai clic su **Visualizza ruoli**. 
3. Fai clic su **Visualizza spazi**. 
4. Seleziona o deseleziona l'opzione di ruolo spazio per il ruolo che vuoi aggiungere al, o rimuovere dal, membro del team.
5. Fai quindi clic su **Salva**.

## Come invitare membri del team
{: #inviteteammembers}

Puoi aggiungere un utente utilizzando la finestra Directory team se l'ID utente non è un account collegato e se sei un proprietario dell'account o un gestore dell'organizzazione. Quando aggiungi dei nuovi membri del team, con l'eccezione di un ambiente locale o dedicato, a essi viene automaticamente assegnato i ruoli di revisore. Puoi modificare i ruoli successivamente nella pagina Directory team. Per invitare un membro del team, completa questa procedura:

<ol>
<li>Fai clic su **Invita un utente**. </li>
<li>Immetti l'indirizzo email per l'utente da invitare.</li>
<li>Seleziona il ruolo da assegnare per l'organizzazione. </li>
<li>Seleziona il ruolo da assegnare per uno o più spazi nell'organizzazione. </li>
<li>Seleziona l'opzione per confermare che ti assumi la responsabilità finanziaria per tutti gli addebiti sostenuti sull'account.</li>
<li>Fai clic su **Invita**. </li>
</ol>

L'utente viene aggiunto all'elenco di membri del team visualizzato per l'account. 

## Rimozione dei membri del team
{: #removingteammembers}

Se l'utente è stato aggiunto dalla Directory team e non è un account collegato, i proprietari dell'account e i gestori dell'organizzazione possono rimuovere i membri del team da un account dalla pagina Directory team. Per rimuovere un membro del team, completa la seguente procedura:

1. Individua l'utente che desideri rimuovere e fai clic sull'icona **Rimuovi utente** ![Icona Rimuovi](../icons/icon_remove_teamuser.svg).
2. Fai clic su **Rimuovi** per confermare di voler rimuovere l'utente specificato dall'account.

L'utente viene rimosso dall'elenco di membri del team visualizzato per l'account.
