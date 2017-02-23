---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Livelli di accesso per i ruoli applicazione

Le seguenti tabelle mostrano il livello di accesso per ogni ruolo dell'applicazione.

Le tabelle mostrano i livelli di accesso per:
- [Operazioni del dispositivo](#app-device-ops)
- [Operazioni di log](#app-log-ops)
- [Operazioni cache](#app-cache-ops)
<!-- [Historian Operations](#app-historian) -->
- [Operazioni dell'organizzazione](#app-org-ops)
- [Operazioni di controllo dell'accesso](#app-access-ops)
- [Operazioni di analisi](#app-analytics-ops)
- [Operazioni di terze parti](#app-third-party)  
<!-- - [Risk Management Operations](#app-risk-mgt) -->

## Ruoli applicazione
{: #app-roles}

### Operazioni del dispositivo {: #app-device-ops}

Operazioni del dispositivo ||| Ruoli applicazione||||
:--------: | -------------|-------------|---------------|-----|---
           | **Applicazione standard** | **Applicazione Operazioni** | **Applicazione di back-end attendibile** | **Applicazione del processore dati** | **Applicazione di visualizzazione** | **Applicazione del dispositivo**
Creazione, aggiornamento o eliminazione dispositivi|X|X|X|-|-|-
Visualizzazione dispositivi|X|X|X|X|X|-
Attivazione dispositivo|X|X|X|-|-|-
Pubblicazione di un evento|X|-|X|-|-|X
Sottoscrizione a un evento|X|X|X|X|X|X
Pubblicazione di un comando|X|X|X|X|-|-
Sottoscrizione a un comando|X|-|X|-|-|X
Avvio dell'azione di gestione del dispositivo|X|X|-|-|-|-
Visualizzazione azioni di gestione del dispositivo|X|X|-|-|-|X
Annullamento azioni di gestione del dispositivo|X|X|-|-|-|-
Gestione dei bundle dell'azione di gestione del dispositivo|X|X|-|-|-|-
Creazione, aggiornamento o eliminazione dei tipi di dispositivo|X|X|X|-|-|-
Visualizzazione tipi di dispositivo|X|X|X|X|-|-
Gestione log di diagnostica|X|X|-|-|-|X
Visualizzazione log di diagnostica|X|X|X|-|-|-

### Operazioni di log {: #app-log-ops}

Operazioni di log ||| Ruoli applicazione||||
:--------: | -------------|-------------|---------------|-----|---
           | **Applicazione standard** | **Applicazione Operazioni** | **Applicazione di back-end attendibile** | **Applicazione del processore dati** | **Applicazione di visualizzazione** | **Applicazione del dispositivo**
Visualizzazione log del server|X|X|X|-|-|-

### Operazioni cache {: #app-cache-ops}

Operazioni cache ||| Ruoli applicazione||||
:--------: | -------------|-------------|---------------|-----|---
           | **Applicazione standard** | **Applicazione Operazioni** | **Applicazione di back-end attendibile** | **Applicazione del processore dati** | **Applicazione di visualizzazione** | **Applicazione del dispositivo**
Visualizzazione dati live (cache evento)|X|X|X|X|X|X
Gestione dei dati live (cache evento)|X|X|X|X|X|X

### Operazioni dell'organizzazione {: #app-org-ops}

Operazioni dell'organizzazione ||| Ruoli applicazione||||
:--------: | -------------|-------------|---------------|-----|---
           | **Applicazione standard** | **Applicazione Operazioni** | **Applicazione di back-end attendibile** | **Applicazione del processore dati** | **Applicazione di visualizzazione** | **Applicazione del dispositivo**
Configurazione dei parametri di archiviazione|-|-|-|-|-|-
Configurazione del provider di autenticazione|-|-|-|-|-|-
Creazione, visualizzazione, aggiornamento o eliminazione della configurazione email|-|-|-|-|-|-
Visualizzazione dei provider di posta disponibili|X|X|-|-|-|-
Creazione, visualizzazione, aggiornamento o eliminazione dei template dell'email|X|X|-|-|-|-
Creazione, aggiornamento o eliminazione degli utenti|-|X|-|-|-|-
Visualizzazione utenti|X|X|-|-|-|-
Creazione, aggiornamento o eliminazione degli inviti utente|-|X|-|-|-|-
Visualizzazione degli inviti utente|X|X|-|-|-|-
Completamento dell'invito|X|X|-|-|-|-
Creazione, aggiornamento o eliminazione delle chiavi API|-|X|-|-|-|-
Visualizzazione delle chiavi API|X|X|-|-|-|-
Visualizzazione delle informazioni sull'utilizzo dell'organizzazione|X|X|-|-|-|-

### Operazioni di controllo dell'accesso {: #app-access-ops}

Operazioni di controllo dell'accesso ||| Ruoli applicazione||||
:--------: | -------------|-------------|---------------|-----|---
           | **Applicazione standard** | **Applicazione Operazioni** | **Applicazione di back-end attendibile** | **Applicazione del processore dati** | **Applicazione di visualizzazione** | **Applicazione del dispositivo**
Visualizzazione delle proprietà degli utenti, inclusi i diritti di accesso|X|X|-|-|-|-
Visualizzazione delle proprie proprietà utente, inclusi i diritti di accesso|-|-|-|-|-|-
Gestione degli utenti, inclusi i diritti di accesso|-|X|-|-|-|-
Visualizzazione delle proprietà della chiave API, inclusi i diritti di accesso|X|X|-|-|-|-
Visualizzazione delle proprie proprietà della chiave API, inclusi i diritti di accesso|X|X|X|X|X|X
Creazione, aggiornamento, eliminazione delle chiavi API, inclusi i diritti di accesso|-|X|-|-|-|-
Visualizzazione delle proprietà del dispositivo, inclusi i diritti di accesso|X|X|X|X|X|-
Visualizzazione delle proprie proprietà del dispositivo, inclusi i diritti di accesso|-|-|-|-|-|-
Creazione, aggiornamento, eliminazione del dispositivo, inclusi i diritti di accesso|X|X|X|-|-|-
Visualizzazione dei ruoli|X|X|-|-|-|-
Creazione, aggiornamento, eliminazione dei ruoli personalizzati|-|X|-|-|-|-
Visualizzazione delle operazioni*|X|X|-|-|-|-

### Operazioni di analisi {: #app-analytics-ops}

Operazioni di analisi ||| Ruoli applicazione||||
:--------: | -------------|-------------|---------------|-----|---
           | **Applicazione standard** | **Applicazione Operazioni** | **Applicazione di back-end attendibile** | **Applicazione del processore dati** | **Applicazione di visualizzazione** | **Applicazione del dispositivo**
Visualizzazione delle regole di analisi|X|X|-|X|X|-
Gestione delle regole di analisi|X|X|-|X|-|-
Visualizzazione delle azioni di analisi|X|X|-|X|X|-
Gestione delle azioni di analisi|X|X|-|X|X|-
Visualizzazione degli avvisi di analisi|X|X|-|X|X|X
Visualizzazione degli schemi del messaggio di analisi|X|X|-|X|X|-
Gestione degli schemi del messaggio di analisi|X|X|-|X|-|-

### Operazioni del servizio di terze parti {: #app-third-party}

Operazioni del servizio di terze parti ||| Ruoli applicazione||||
:--------: | -------------|-------------|---------------|-----|---
           | **Applicazione standard** | **Applicazione Operazioni** | **Applicazione di back-end attendibile** | **Applicazione del processore dati** | **Applicazione di visualizzazione** | **Applicazione del dispositivo**
Elaborazione delle notifiche batch da una piattaforma esterna|X|X|-|-|-|-
Elaborazione delle notifiche batch e loro invio alla piattaforma esterna|X|X|-|-|-|-
Pubblicazione di un evento per un dispositivo|X|X|-|-|-|-
Sottoscrizione a eventi da un dispositivo|X|X|-|-|-|-
Configurazione di un URL di callback per la piattaforma esterna|X|X|-|-|X|-
Configurazione del livello di sottoscrizione della piattaforma esterna|X|X|-|-|X|-
Ottenimento dello stato di integrità dal connector|X|X|X|-|X|-
Verifica se un sistema esterno è attivo e convalida delle credenziali|X|X|X|-|X|-
