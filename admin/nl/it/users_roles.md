---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestione dei membri dei team e dei ruoli
{: #userroles}
*Ultimo aggiornamento: 16 maggio 2016*

Dalla pagina **Directory team** per il tuo account, puoi gestire i membri dei team esistenti e i loro ruoli nella tua organizzazione e nei tuoi spazi, oltre che invitare nuovi membri del team.Per accedere alla directory team per il tuo account, vai all'icona **Account e supporto** ![icona Account e supporto](../admin/images/account_support.svg) &gt; **Account** &gt; *il_nome_del_tuo_account* &gt; **Directory team**.
{:shortdesc}

I proprietari degli account eseguono tutte le operazioni sulle organizzazioni e sugli spazi, compresa la gestione dei membri dei team e dei loro ruoli assegnati. I gestori dell'organizzazione dispongono di un accesso che consente loro di invitare membri del team e gestire i ruoli. I gestori dello spazio possono utilizzare la pagina
**Gestisci organizzazioni** per aggiungere i membri dell'account esistenti allo spazio e regolare i loro ruoli. Per ulteriori informazioni sui ruoli,
consulta le seguenti informazioni.

## Ruoli
{: #userrolesinfo}

A livello di account, esistono due ruoli che abilitano l'accesso a funzioni di gestione dell'account differenti:

*Tabella 1. Ruoli dell'account e autorizzazioni*

| Ruolo dell'account | Autorizzazioni |    
|----------------|---------|
|Proprietario | Un proprietario per l'account ha accesso al proprio profilo e dashboard di utilizzo e alle proprie directory di team, informazioni di fatturazione e notifiche di spesa. Dalla pagina directory team, il proprietario può invitare nuovi membri del team e regolare i ruoli. Il proprietario può anche aggiungere dei crediti promozionali, impostare o modificare il limite di fatturazione, impostare l'accesso al servizio e gestire organizzazioni e spazi. |
|Membro | Un membro ha accesso ai proprio limiti di fatturazione, crediti dell'account e profilo e alla propria directory team nell'intestazione {{site.data.keyword.Bluemix_notm}}. Tuttavia, nella pagina directory team, un membro può visualizzare solo i membri del team all'interno dell'account. |

 Tutti i nuovi membri del team vengono aggiunti come un membro dell'account. Puoi assegnare i ruoli organizzazione e spazio agli invitati per abilitare specifiche viste e autorizzazioni in {{site.data.keyword.Bluemix_notm}}. Ai nuovi membri del team aggiunti a un'organizzazione viene assegnato per impostazione predefinita il ruolo organizzazione di revisore. Per uno specifico spazio, puoi scegliere di assegnare il ruolo di sviluppatore o di revisore agli invitati. Dopo che gli invitati hanno accettato l'invito e si sono uniti a {{site.data.keyword.Bluemix_notm}}, puoi modificarne i ruoli nella pagina **Directory team**.

I seguenti ruoli possono essere assegnati a livello dell'organizzazione:

*Tabella 2. Ruoli organizzazione e autorizzazioni*

| Ruolo organizzazione | Autorizzazioni |    
|-------------------|-------------|
|Gestore | I gestori dell'organizzazione possono creare, visualizzare, modificare o eliminare gli spazi nell'organizzazione, visualizzare l'utilizzo e la quota dell'organizzazione, invitare membri del team all'organizzazione, gestire chi ha accesso all'organizzazione e i loro ruoli al suo interno e gestire i domini personalizzati per l'organizzazione. |
|Gestore fatturazione | I gestori fatturazione possono visualizzare le informazioni sull'utilizzo di runtime e servizi per l'organizzazione nella pagina Dashboard di utilizzo.  |
|Revisore | I revisori organizzazione possono visualizzare il contenuto di applicazioni e servizi nell'organizzazione. I revisori possono anche visualizzare i membri
del team nell'organizzazione e i ruoli ad essi assegnati, nonché la quota per l'organizzazione. Questo ruolo viene assegnato a tutti gli invitati per impostazione predefinita.|

I seguenti ruoli possono essere assegnati a livello dello spazio:

*Tabella 3. Ruoli spazio e autorizzazioni*

| Ruolo spazio | Autorizzazioni |    
|------------|-------------|
|Gestore | I gestori spazio possono aggiungere membri del team esistenti e gestire i ruoli nello spazio. Il gestore spazio può anche visualizzare il numero di istanze, i bind di servizio e l'utilizzo delle risorse per ciascuna applicazione nello spazio. |
|Sviluppatore | Gli sviluppatori spazio possono creare, eliminare e gestire applicazioni e servizi nello spazio. Alcune delle attività di gestione includono la distribuzione di applicazioni, l'avvio e l'arresto di applicazioni, la rinominazione di un'applicazione, l'eliminazione di un'applicazione, la rinominazione di uno spazio, il bind o l'annullamento del bind di un servizio a un'applicazione, la visualizzazione del numero di istanze, i bind di servizi e l'utilizzo di risorse per ciascuna applicazione nello spazio. Inoltre, lo sviluppatore spazio può associare un URL interno o esterno a un'applicazione nello spazio.   |
|Revisore | I revisori spazio hanno un accesso in sola lettura a tutte le informazioni sullo spazio, quali le informazioni sul numero di istanze, i bind di servizio e l'utilizzo di risorse per ciascuna applicazione nello spazio. |

**Nota**: ai membri del team a cui nello spazio è assegnato il ruolo di gestore o sviluppatore possono accedere alla variabile di ambiente VCAP_SERVICES. Tuttavia, un membro del team a cui è assegnato il ruolo di revisore non può accedere a VCAP_SERVICES.

## Invito di membri del team
{: #inviteteammembers}

I proprietari dell'account e i gestori dell'organizzazione possono invitare i membri del team alle organizzazioni dalla pagina Invita membri del team. Quando aggiungi dei nuovi membri del team, a essi viene automaticamente assegnato i ruoli di revisore. Puoi modificare i ruoli successivamente nella pagina Directory team. Per invitare un membro del team, completa questa procedura:

<ol>
<li>Vai all'icona **Account e supporto** ![icona Account e
supporto](../admin/images/account_support.svg) &gt; Account &gt; il_nome_del_tuo_account &gt; Invita membro del team.</li>
<li>Seleziona l'organizzazione a cui vuoi invitare i membri del team.</li>
<li>Fai clic su **Avanti**.</li>
<li>Seleziona gli spazi a cui vuoi consentire l'accesso per i tuoi membri del team.</li>
<li>Seleziona il ruolo da assegnare per gli spazi selezionati nell'organizzazione.</li>
<li>Seleziona l'opzione per confermare che ti assumi la responsabilità finanziaria per tutti gli addebiti sostenuti sull'account.</li>
<li>Immetti l'indirizzo email per un singolo membro del team oppure gli indirizzi email per più membri del team:
<ul>
<li>Per aggiungere un singolo membro del team, immetti l'indirizzo email e fai clic su **Invia**.</li>
<li>Per aggiungere più di un membro del team, fai clic su **Invitali tutti in una singola operazione**. Immetti gli indirizzi email utilizzando un elenco separato da virgole, spazi o interruzioni di riga. Fai quindi clic su **Avanti** per verificare gli indirizzi email a cui inviare gli inviti e fai clic su **Invia**.</li>
</ul>
</li>
</ol>

Fai clic su **Visualizza in sospeso** per controllare se gli inviti sono in sospeso o sono stati accettati. Puoi scegliere di inviare nuovamente l'email di invito o di annullare l'invito per un invito in sospeso in qualsiasi momento.

## Modifica di ruoli
{: #editinguserroles}

I proprietari dell'account e i gestori dell'organizzazione possono modificare i ruoli di organizzazione e spazio per i membri del team esistenti nella pagina **Directory team**. 

1. Vai all'icona **Account e supporto** ![icona Account e supporto](../admin/images/account_support.svg) &gt; **Account** &gt; *il_nome_del_tuo_account* &gt; **Directory team**.
2. Individua il membro del team di cui vuoi modificare i ruoli.
3. Fai clic su **Visualizza ruoli**.
4. Seleziona o deseleziona le selezioni di ruolo dell'organizzazione per modificare l'accesso all'organizzazione per il membro del team.
5. Fai clic su **Visualizza spazi** per aggiungere o rimuovere ruoli dello spazio.
6. Seleziona o deseleziona le selezioni di ruolo dello spazio per modificare l'accesso allo spazio per il membro del team.
7. Fai clic su **Chiudi spazi**.
8. Fai clic su **Salva** alla fine della pagina.

I gestori spazio possono modificare i ruoli per i membri del team nel loro spazio nella pagina **Gestisci organizzazioni**.

1. Vai all'icona **Account e supporto** ![icona Account e supporto](../admin/images/account_support.svg) &gt; **Account** &gt; *il_nome_del_tuo_account* &gt; **Gestisci organizzazioni**.
2. Individua l'organizzazione in cui si trova il tuo spazio.
3. Fai clic su **Visualizza dettagli**.
4. Individua il tuo spazio e fai clic su **Modifica spazio**.
5. Seleziona la scheda **Utenti**.
6. Seleziona o deseleziona l'opzione di ruolo spazio per il ruolo che vuoi aggiungere al, o rimuovere dal, membro del team.
7. Fai clic su **Salva**.
