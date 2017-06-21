---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-11"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Assegnazione dell'accesso utente
{: #assignaccess}

Assegni l'accesso agli utenti nel momento in cui li inviti, assegnando loro i ruoli, le politiche e gli account o le organizzazioni, o entrambi, a cui possono accedere. A seconda delle opzioni di accesso che sei autorizzato a gestire, puoi invitare e fornire l'accesso agli utenti tra le istanze di servizio, spazio, organizzazione e account. Come proprietario di un account, puoi assegnare le opzioni di accesso al tuo account a un utente quando siete entrambi membri, indipendentemente dal ruolo. Le seguenti sezioni descrivono i tre tipi di accesso che possono essere assegnati a un utente invitato.
{:shortdesc}

## Servizi abilitati per l'accesso e l'identità

Quando inviti un nuovo utente, puoi assegnare una singola politica di servizio. Una volta che l'utente ha accettato l'invito, puoi aggiungere ulteriori politiche.

1. Dalla schermata **Invita utenti**, espandi la sezione **Servizi abilitati per l'accesso e l'identità**.
2. Seleziona **Tutti i servizi abilitati per l'accesso e l'identità** o seleziona un singolo servizio. **Nota**:  se selezioni l'opzione **Concedi automaticamente l'accesso quando vengono aggiunti nuovi servizi**, non ti viene notificato di deselezionare ogni nuovo servizio {{site.data.keyword.Bluemix_notm}} per tale utente quando in seguito vengono aggiunti dei servizi.
3. Seleziona **Tutte le regioni correnti** o una regione specifica.
4. Seleziona **Tutte le istanze del servizio correnti** o una specifica istanza del servizio.
5. Seleziona un ruolo per definire l'ambito di accesso per la politica.
6. Facoltativo: seleziona **Aggiungi ruolo** per specificare un ruolo aggiuntivo per la politica.

Consulta [Politiche e ruoli per la gestione di identità e accesso](/docs/iam/users_roles.html#iamusermanpol) per informazioni più specifiche sull'impostazione delle politiche di servizio.

## Accesso Cloud Foundry

Per impostazione predefinita, a tutti gli utenti viene concesso il ruolo di revisore organizzazione. Una volta che l'utente ha accettato l'invito, puoi aggiornare questo ruolo a gestore fatturazione, gestore organizzazione o non assegnare alcun ruolo. Durante il processo di invito, puoi assegnare più ruoli per lo spazio, uno alla volta.

1. Dalla schermata **Invita utenti**, espandi la sezione **Accesso Cloud Foundry**.
2. Seleziona un'organizzazione a cui aggiungere l'utente.
3. Seleziona **Tutte le regioni correnti** o una regione specifica.
4. Seleziona **Tutti gli spazi correnti** o uno specifico spazio.
5. Seleziona un ruolo per definire l'ambito di accesso.
6. Facoltativo: seleziona **Aggiungi ruolo** per specificare un ruolo aggiuntivo per la politica.

Consulta [Ruoli Cloud Foundry](/docs/iam/users_roles.html#cfroles) per informazioni più specifiche su questi ruoli.

## Accesso infrastruttura

Se disponi dell'autorizzazione, visualizzi l'opzione per assegnare le autorizzazioni dell'infrastruttura. Le autorizzazioni effettive assegnate vengono automaticamente limitate al sottoinsieme delle autorizzazioni di cui disponi. Per ulteriori informazioni sulle autorizzazioni e sulle azioni che l'utente può eseguire con ognuna di esse, vedi [Autorizzazioni dell'infrastruttura](/docs/iam/users_roles.html#infrapermissions).

1. Dalla schermata **Invita utenti**, espandi la sezione **Accesso infrastruttura**. 
2. Seleziona un'autorizzazione per definire l'ambito di accesso.

Per informazioni sulla configurazione dell'accesso per gli utenti dopo che sono stati aggiunti al tuo account, vedi [Gestione accesso e account utente](/docs/iam/iamusermanage.html).
