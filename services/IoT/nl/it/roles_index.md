---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Ruoli utente, applicazione e gateway

I ruoli sono serie di autorizzazioni che puoi utilizzare per concedere o restringere l'accesso a operazioni specifiche. Puoi utilizzare i ruoli per gestire le autorizzazioni per i gruppi di utenti, applicazioni e gateway.
{:shortdesc}

## Ruoli utente
{: #user_roles}

Puoi assegnare i ruoli utente quando aggiungi, inviti o registri un utente in {{site.data.keyword.iot_full}}. Puoi anche assegnare o modificare i ruoli utente in qualsiasi momento utilizzando il dashboard {{site.data.keyword.iot_short_notm}}. Per ulteriori informazioni sull'assegnazione di un ruolo ad un utente, consulta [Gestione dei ruoli utente](managing_user_roles.html).

I seguenti ruoli utente standard sono disponibili:

Ruolo utente | Descrizione
------------- | -------------
Amministratore | Un ruolo 'super-utente' che concede l'accesso a tutte le API correlate all'utente. Gli amministratori non possono accedere alle operazioni limitate ai dispositivi e alle applicazioni.
Operatore | Destinato agli utenti dell'organizzazione di front-end. Concede l'accesso alla maggior parte delle operazioni dell'organizzazione, alle operazioni di controllo dell'accesso, di terze parti e di gestione del rischio.
Sviluppatore | Concede accesso limitato alle operazioni del dispositivo, di log, di cache, storiche, di analisi e dei servizi di terze parti. Il ruolo fornisce l'accesso all'organizzazione, al controllo dell'accesso e alle operazioni di gestione del rischio.
Analista | Concede accesso alle operazioni di analisi, inclusi la creazione, l'aggiornamento e l'eliminazione di regole, azioni e schemi.
Lettore | Il ruolo utente predefinito. Concede accesso limitato alle operazioni disponibili a tutti gli utenti.

Per ulteriori informazioni sui ruoli utente, vedi [Ruoli utente](reference/roles_access.html).

## Ruoli dell'applicazione
{: #application_roles}
Puoi assegnare i ruoli dell'applicazione per concedere o revocare alle tue applicazioni l'accesso a operazioni specifiche. Tutti i ruoli dell'applicazione negano l'accesso alle seguenti operazioni:

- Tutte le operazioni di gestione del rischio
- Configurazione dei parametri di archiviazione
- Configurazione dei provider di autenticazione
- Creazione, aggiornamento o eliminazione della configurazione email

I seguenti ruoli applicazione standard sono disponibili:

Ruolo Applicazione | Descrizione
------------- | -------------
Standard | Il ruolo applicazione predefinito. Concede l'accesso alla maggior parte delle operazioni dell'applicazione ma non alle operazioni ruolo o utente.   
Operazioni | Concede l'accesso ad un'ampia gamma di operazioni, ma nega l'accesso alle operazioni di sottoscrizione o di pubblicazione.
Backend attendibile | Pensato per le applicazioni che non richiedono interazione con l'operatore dei sistemi. Nega l'accesso alle operazioni di gestione, organizzazione, ruolo o di estensione.
Processore dati | Pensato per le applicazioni che eseguono elaborazione dati e analisi. Le applicazioni del processore dati hanno accesso limitato alle operazioni di organizzazione e utente, ma hanno accesso completo alle operazioni di analisi inclusi la creazione e la gestione di regole, azioni e schemi.
Visualizzazione | Pensato per le applicazioni che sono responsabili della generazione delle visualizzazioni dei dati. Le applicazioni di visualizzazione hanno accesso alle operazioni dai dati archiviati o live e alle operazioni dashboard.
Dispositivo | Pensate per le applicazioni che hanno il ruolo di dispositivi; cioè, forniscono un'origine dei dati che viene inviata a {{site.data.keyword.iot_short_notm}} come se fosse un dispositivo. Le applicazioni dispositivo hanno soltanto un accesso limitato alle operazioni.

Per ulteriori informazioni sull'accesso alle operazioni dei ruoli dell'applicazione, vedi [Ruoli applicazione](reference/app_roles_access.html).

## Ruoli gateway
{: #gateway_roles}
I gateway hanno un numero limitato di ruoli che controllano la definizione del gateway e la capacità di registrare i dispositivi in {{site.data.keyword.iot_short_notm}}.

I seguenti ruoli gateway standard sono disponibili:

Ruolo gateway | Descrizione
------------- | -------------
Standard | Il ruolo gateway predefinito. Concede accesso limitato alle operazioni.
Privilegiato | Pensato per i gateway attendibili e consente ai gateway privilegiati di aggiungere i dispositivi a {{site.data.keyword.iot_short_notm}}. Concede l'accesso a operazioni rilevanti per aggiungere, aggiornare e gestire i dispositivi e le proprietà del dispositivo, ma non l'accesso ad altre operazioni.  

Per ulteriori informazioni sull'accesso alle operazioni dei ruoli del gateway, vedi [Ruoli del gateway](reference/gateway_roles_access.html).
