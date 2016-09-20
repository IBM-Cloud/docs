---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Gestione degli utenti {: #manage-users}

Progettato per la collaborazione in team, {{site.data.keyword.iotrtinsights_short}} consente agli amministratori di aggiungere ulteriori utenti per l'accesso alla console di {{site.data.keyword.iotrtinsights_short}}.
{: shortdesc}

Descrizioni dei ruoli:
- Operatore
Gli operatori eseguono direttamente il login alla console di {{site.data.keyword.iotrtinsights_short}} per monitorare il flusso di dati in tempo reale dei loro dispositivi e gruppi di dispositivi. Gli operatori possono anche attivare e disattivare regole e modificare i dashboard modificabili.  
- Amministratore
Oltre alle attività che possono essere eseguite da un operatore, gli amministratori possono aggiungere utenti, gestire layout di dashboard, aggiungere origini dati e gestire tipi di dispositivo.  
- Proprietario
Il ruolo di proprietario viene assegnato all'ID IBM che ha distribuito l'istanza del servizio {{site.data.keyword.iotrtinsights_short}} in Bluemix. Un proprietario ha gli stessi privilegi di un amministratore ma non può essere eliminato.

Per aggiungere un nuovo utente:
1. Aggiungi l'utente a {{site.data.keyword.iot_short}}.  
>**Importante:** se stai aggiungendo un utente con il ruolo di amministratore, devi anche aggiungere tale utente a {{site.data.keyword.iot_short}}.  

  1. Accedi al dashboard del servizio {{site.data.keyword.iot_short}} che è un'origine dati per il tuo servizio {{site.data.keyword.iotrtinsights_short}}.  
  2. Passa a **Accedi > Membri** e fai clic su **Aggiungi membri**.
  3. Immetti l'ID IBM per l'utente che vuoi aggiungere e fai clic su **Aggiungi membri**.
2. Aggiungi l'utente a {{site.data.keyword.iotrtinsights_short}}.
  1. Esegui il login alla console di {{site.data.keyword.iotrtinsights_short}} come un utente con il ruolo di amministratore o con il ruolo di proprietario.
  2. Vai a **Configura > Gestisci utenti**.
  3. Fai clic su **Aggiungi nuovo utente**.
  4. Immetti l'indirizzo email dell'utente che vuoi invitare, seleziona un ruolo per l'utente e fai clic su ![icona Crea](images/create.png "Icona Crea").
All'utente viene inviata una email che contiene il link della console web. Se l'indirizzo email è già associato a un ID IBM, l'utente può eseguire il login e accedere alla console direttamente. Altrimenti, all'utente viene richiesto di creare un ID IBM gratuito prima di accedere alla console.  
>**Selezione della tua istanza di Real-Time Insights:** gli utenti che hanno accesso a più istanze di Real-Time Insights come operatori o amministratori possono rapidamente spostarsi tra tali istanze. Nella console di Real-Time Insights, possono fare clic sul loro nome utente e selezionare l'istanza a cui vogliono accedere.  
