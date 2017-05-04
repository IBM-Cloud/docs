---

copyright:

  years: 2015, 2017
lastupdated: "2017-03-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Invito di utenti, assegnazione e gestione dell'accesso
{: #iamuserinv}

Puoi invitare gli utenti con le applicazioni, i servizi {{site.data.keyword.Bluemix_notm}} e l'infrastruttura {{site.data.keyword.Bluemix_notm}} da una sola ubicazione. Assegni l'accesso agli utenti come li inviti, assegna i ruoli, le politiche, gli account o le organizzazioni, o entrambi, a cui possono accedere. A seconda delle opzioni di accesso che sei autorizzato a gestire, puoi invitare e fornire l'accesso agli utenti nell'account o nell'organizzazione. Come proprietario di un account, puoi assegnare le opzioni di accesso al tuo account a un utente quando siete entrambi membri, indipendentemente dal ruolo.
{:shortdesc}

Per invitare gli utenti o per gestire gli inviti utente nel tuo account, dalla barra del menu, fai clic su **Gestione** &gt; **Account** &gt; **Utenti**. La finestra Utenti visualizza un elenco di utenti con i rispettivi indirizzi email e stato corrente negli account che gestisci. 

Per invitare gli utenti e gestire gli inviti in sospeso, devi essere un proprietario dell'account, un gestore dell'organizzazione o devi avere la autorizzazioni dell'infrastruttura per aggiungere gli utenti.  Puoi invitare gli utenti, annullare gli inviti e reinviare un invito in sospeso a un utente invitato. Puoi invitare un solo utente o, se stai fornendo lo stesso accesso a tutti i membri in un gruppo di utenti, puoi invitare più utenti contemporaneamente.

Per invitare gli utenti, fai clic su **Invita utenti**, specifica l'indirizzo email o l'ID IBM dell'utente e quindi aggiungili a una o più opzioni di accesso che gestisci. Devi assegnare almeno un'opzione di accesso e configurare le impostazioni per l'utente in ogni opzione di accesso che assegni. Per tutte le ulteriori opzioni di accesso che non aggiungi e configuri, viene assegnato il valore predefinito *nessun accesso*. Potresti visualizzare una delle seguenti opzioni di accesso, a seconda delle opzioni che sei autorizzato a gestire:

**Servizi abilitati per l'accesso e l'identità**
Seleziona per assegnare i servizi, le regioni, le istanze del servizio e i ruoli per gli utenti che inviti.
**Nota**:  se selezioni l'opzione **Concedi automaticamente l'accesso quando vengono aggiunti nuovi servizi**, non ti viene notificato di deselezionare ogni nuovo servizio {{site.data.keyword.Bluemix_notm}} per tale utente quando in seguito vengono aggiunti dei servizi.

**Accesso Cloud Foundry**
Seleziona per assegnare i servizi, le regioni, gli spazi e i ruoli dello spazio per gli utenti che inviti. Consulta [Ruoli utente](/docs/admin/users_roles.html#userrolesinfo) per ulteriori informazioni specifiche su queste impostazioni. Puoi aggiungere più ruoli, uno alla volta.

**Accesso all'infrastruttura**
Assegna la seguente autorizzazione dell'infrastruttura all'utente: 
<dl>
<dt>Solo visualizzazione</dt>
<dd>Gli utenti con questa autorizzazione possono soltanto visualizzare gli elementi nel sistema.</dd>
<dt>Utente base</dt>
<dd>Gli utenti con questa autorizzazione possono eseguire le azioni di base nel sistema, come aggiungere un ticket e gestire i dispositivi.</dd>
<dt>Super utente</dt>
<dd>Gli utenti con questa autorizzazione possono eseguire tutte le azioni disponibili nel sistema.</dd>
</dl>
**Nota**: le autorizzazioni reali assegnate vengono automaticamente limitate alla sottoserie di autorizzazioni di cui disponi.

Se stai fornendo a più utenti lo stesso accesso, puoi selezionare **Invita più utenti** per immettere un elenco di utenti da invitare. Separa la voci ID utente con le virgole.  

Se determini che un utente non ha bisogno dell'accesso, puoi anche annullare un invito per tutti gli utenti visualizzati in uno stato **Elaborazione** o **In sospeso** nella colonna **Stato**. Se un utente invitato non riceve un invito, puoi anche reinviare l'invito a tutti gli utenti nello stato **In sospeso**.  Queste opzioni sono disponibili per gli utenti nello stato appropriato dal menu **Azioni** nella finestra Utenti.

Per informazioni specifiche sulla configurazione dell'accesso per gli utenti, inclusi i ruoli e le politiche, consulta [Gestione accesso e account utente](/docs/admin/iamusermanage.html).
