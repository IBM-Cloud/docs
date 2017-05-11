---

copyright:

  years: 2015, 2017

lastupdated: "2017-04-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gestione accesso e account utente
{: #iamusermanage}

A seconda delle opzioni di accesso che sei autorizzato a gestire, puoi visualizzare e gestire gli utenti nell'account o nell'organizzazione. Come proprietario di un account, puoi gestire gli utenti in tutte le opzioni di accesso che gestisci e alle quali è assegnato l'accesso dell'utente, indipendentemente dal ruolo, nell'account corrente. Puoi assegnare, modificare e rimuovere l'accesso in tutte le opzioni di accesso che gestisci. 
{:shortdesc}

Per gestire gli utenti nel tuo account, dalla barra del menu, fai clic su **Gestione** &gt; **Account** &gt; **Utenti**. La finestra Utenti visualizza un elenco di utenti con i rispettivi indirizzi email e stato corrente negli account che gestisci. Dalla finestra Utenti, seleziona l'utente da gestire o fai clic su **Gestione utente** dal menu **Azioni**. Visualizzi la tabella dei criteri per le opzioni di accesso che puoi gestire per tale utente.

## Gestione dei servizi abilitati per l'accesso e l'identità
{: #iammanidaccser}

Se l'utente ha l'accesso assegnato a un **Servizio abilitato per l'accesso e l'identità**, puoi visualizzare le informazioni sulle politiche assegnate dalla finestra utente Gestione.  Cosa viene visualizzato per questo utente o gruppo dipende dalle politiche che sono state assegnate. Se non è stata assegnata alcuna politica, visualizzi un messaggio che richiede se desideri assegnare una politica. Se le politiche sono già state assegnate, viene quindi visualizzato un elenco delle politiche con il ruolo dell'utente o del gruppo e una descrizione degli attributi della risorsa per ogni politica. Puoi assegnare le politiche dalla pagina di assegnazione delle politiche facendo clic su **Assegna politiche del servizio**. L'opzione **Assegna politiche del servizio** è abilitata se sei autorizzato a creare le politiche. Puoi gestire le politiche esistenti facendo clic sulla politica nell'elenco o facendo clic su **Modifica politica** in **Azioni** nella riga della politica che desideri modificare.

## Gestione dell'accesso ai servizi Cloud Foundry
{: #iammancfser}

Se l'utente ha l'accesso assegnato a **Cloud Foundry**, puoi visualizzare le organizzazioni e gli spazi a cui è assegnato l'utente dalla finestra Gestione utente. Puoi rimuovere l'utente da un'organizzazione o puoi modificare il ruolo assegnato per un'organizzazione o uno spazio. Puoi aggiungere un utente a un'altra organizzazione facendo clic su **Assegna organizzazione** se sei il gestore di un'organizzazione di cui l'utente non è ancora membro. Pupo gestire i ruoli spazio e organizzazione esistenti facendo clic su **Modifica ruolo spazio** o **Modifica ruolo organizzazione** nella riga del ruolo che desideri modificare.

## Gestione delle politiche
{: #iamusermanpol}

Puoi assegnare e gestire le politiche per un utente che ha accesso ai **Servizi abilitati per l'accesso e l'identità**. Una politica assegna uno o più ruoli a una serie di risorse utilizzando una combinazione di attributi per definire la serie di risorse applicabile.

Quando assegni una politica a un utente, specifica prima il servizio da assegnare. L'elenco **Servizio** fornisce l'opzione per i servizi specificati, inclusa un'opzione per assegnare tutti i servizi disponibili. Puoi anche selezionare un ruolo, o ruoli, da assegnare.

Sono disponibili ulteriori opzioni di configurazione, a seconda del servizio che selezioni. Puoi selezionare un servizio per visualizzarne le opzioni.

Puoi restringere l'elenco delle opzioni del servizio che vengono visualizzate. Fai clic su **Specifica contesto del servizio facoltativo** per specificare ulteriori opzioni come le regioni e le istanze del servizio.  Potresti non voler specificare tutte le opzioni visualizzate, ma puoi scegliere quali configurare.

Puoi assegnare e gestire le politiche se hai il ruolo appropriato. La seguente tabella mostra le attività di gestione della politica e il ruolo richiesto per ognuna di esse.


{: #iamui_table1}

| Azione | Ruolo richiesto |
|----------|---------|
| Creare una politica su un account | Amministratore dell'account |
| Creare una politica su tutti i servizi in un account | Amministratore dell'account |
| Creare una politica su tutte le istanze del servizio in un account | Amministratore dell'account |
| Creare una politica su un servizio in un account | Amministratore dell'account o del servizio nell'account |
| Creare un'istanza del servizio | Amministratore o editor dell'account o del servizio nell'account |
| Creare una politica su un'istanza del servizio | Amministratore dell'account o del servizio nell'account o dell'istanza del servizio |
{: caption="Tabella 1. Attività amministrative per la gestione delle politiche dei **Servizi abilitati per l'accesso e l'identità**" caption-side="top"}

## Assegnazione e gestione dei ruoli
{: #iamusermanrol}

I ruoli sono una raccolta di azioni; le azioni che vengono associate a questi ruoli sono specifiche per servizio. 
Poiché le azioni sono raggruppate come ruoli, puoi utilizzare una piccola serie di ruoli definiti per supportare le azioni per tutti i servizi e risorse. Ad esempio, se hai bisogno di un amministratore di macchine virtuali, archivio e rete, puoi configurare l'utente come l'amministratore di tutte e tre modificando la destinazione della politica. Per cui dovrai configurare la politica per includere l'amministratore di macchine virtuali, di archiviazione e di rete.

Le risorse non sono create nei ruoli per cui i nuovi nomi ruolo non sono creati per ogni tipo di risorsa che viene introdotta nel sistema. Ad esempio, non hai bisogno di un ruolo da amministratore di macchine virtuali, di archiviazione e di rete per coprire la gestione delle risorse di macchine virtuali, archiviazione e rete.

In aggiunta alle descrizioni dei ruoli fornite nell'interfaccia utente, la seguente tabella fornisce gli esempi di alcune attività che gli utenti assegnati ad ogni ruolo possono eseguire.

{: #iamui_table2}

| Ruolo | Descrizione delle azioni | Azioni di esempio|
|:-----------------|:-----------------|:-----------------|
| Visualizzatore | Esegue le azioni che non modificano lo stato; solo le azioni in lettura | <ul><li>Elenca dispositivi</li><li>Legge l'oggetto di archiviazione</li><li>Esegue query</li><li>Esegue ricerche</li></ul>|
| Editor | Esegue le azioni che modificano la stato e creano o eliminano le risorse secondarie |<ul><li>Crea o elimina le macchine virtuali</li><li>Collega spazio di archiviazione</li><li>Riavvia</li><li>Avvia o arresta</li><li>Rinomina</li></ul> |
| Amministratore | Esegue tutte le azioni, inclusa la capacità di gestire il controllo dell'accesso |<ul><li>Invita utenti</li><li>Crea o elimina le macchine virtuali</li><li>Aggiorna le politiche di accesso utente</li><li>Elenca dispositivi</li><li>Collega spazio di archiviazione</li><li>Riavvia</li><li>Avvia o arresta</li><li>Rinomina</li><li>Esegue il backup e ripristina</li></ul>|
{: caption="Tabella 2. Attività amministrative per la gestione delle politiche dei **Servizi abilitati per l'accesso e l'identità**" caption-side="top"}

Per informazioni specifiche sui ruoli di accesso assegnato agli utenti per Cloud Foundry, consulta [Ruoli utente](/docs/admin/users_roles.html#userrolesinfo).

Quando aggiungi utenti, devi selezionare almeno un ruolo e puoi aggiungere più ruoli. Quando selezioni un ruolo, ne visualizzi una definizione in modo che puoi determinare il ruolo o i ruoli da fornire.  I ruoli che assegni hanno diverse opzioni di accesso ma agli stessi attributi della risorsa che specifichi.

Se hai selezionato il servizio **Cloud Foundry**, i ruoli che assegni vengono associati alle organizzazioni e agli spazi che selezioni.
