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

# Livelli di accesso per i ruoli gateway

Le seguenti tabelle mostrano il livello di accesso per ogni ruolo del gateway.

Le tabelle mostrano i livelli di accesso per:
- [Operazioni del dispositivo ](#gateway-device-ops)
- [Operazioni di log ](#gateway-log-ops)
- [Operazioni cache ](#gateway-cache-ops)
<!-- [Historian Operations](#gateway-historian) -->
- [Operazioni dell'organizzazione ](#gateway-org-ops)
- [Operazioni di controllo dell'accesso ](#gateway-access-ops)
- [Operazioni di analisi ](#gateway-analytics-ops)
- [Operazioni di terze parti](#gateway-third-party)  
<!-- - [Risk Management Operations](#gateway-risk-mgt) -->

## Ruoli del gateway
{: #gateway-roles}

### Operazioni del dispositivo {: #gateway-device-ops}

Operazioni del dispositivo || Ruoli del gateway|
:--------: | ---------------------|------------------------
           | **Gateway standard** | **Gateway privilegiato**
Creazione, aggiornamento o eliminazione dispositivi|-|X
Visualizzazione dispositivi|X|X
Attivazione dispositivo|-|X
Pubblicazione di un evento|X|X
Sottoscrizione a un evento|-|-
Pubblicazione di un comando|-|-
Sottoscrizione a un comando|X|X
Avvio dell'azione di gestione del dispositivo|X|X
Visualizzazione azioni di gestione del dispositivo|X|X
Annullamento azioni di gestione del dispositivo|-|-
Gestione dei bundle dell'azione di gestione del dispositivo|-|X
Creazione, aggiornamento o eliminazione dei tipi di dispositivo|-|-
Visualizzazione tipi di dispositivo|X|X
Gestione log di diagnostica|-|-
Visualizzazione log di diagnostica|-|-

### Operazioni di log {: #gateway-log-ops}

Operazioni di log || Ruoli del gateway|
:--------: | ---------------------|------------------------
           | **Gateway standard** | **Gateway privilegiato**
Visualizzazione log del server|-|-

### Operazioni cache {: #gateway-cache-ops}

Operazioni cache || Ruoli del gateway|
:--------: | ---------------------|------------------------
           | **Gateway standard** | **Gateway privilegiato**
Visualizzazione dati live (cache evento)|-|-
Gestione dei dati live (cache evento)|-|-


### Operazioni dell'organizzazione {: #gateway-org-ops}

Operazioni dell'organizzazione || Ruoli del gateway|
:--------: | ---------------------|------------------------
           | **Gateway standard** | **Gateway privilegiato**
Configurazione dei parametri di archiviazione|-|-
Configurazione del provider di autenticazione|-|-
Creazione, visualizzazione, aggiornamento o eliminazione della configurazione email|-|-
Visualizzazione dei provider di posta disponibili|-|-
Creazione, visualizzazione, aggiornamento o eliminazione dei template dell'email|-|-
Creazione, aggiornamento o eliminazione degli utenti|-|-
Visualizzazione utenti|-|-
Creazione, aggiornamento, eliminazione degli inviti utente|-|-
Visualizzazione degli inviti utente|-|-
Completamento dell'invito|-|-
Creazione, aggiornamento o eliminazione delle chiavi API|-|-
Visualizzazione delle chiavi API|-|-
Visualizzazione delle informazioni sull'utilizzo dell'organizzazione|-|-

### Operazioni di controllo dell'accesso {: #gateway-access-ops}

Operazioni di controllo dell'accesso || Ruoli del gateway|
:--------: | ---------------------|------------------------
           | **Gateway standard** | **Gateway privilegiato**
Visualizzazione delle proprietà dell'utente (inclusi i diritti di accesso)|-|-
Visualizzazione delle proprie proprietà utente (inclusi i diritti di accesso)|-|-
Gestione degli utenti (inclusi i diritti di accesso)|-|-
Visualizzazione delle proprietà della chiave API (inclusi i diritti di accesso)|-|-
Visualizzazione delle proprie proprietà della chiave API (inclusi i diritti di accesso)|-|-
Creazione, aggiornamento o eliminazione delle chiavi API (inclusi i diritti di accesso)|-|-
Visualizzazione delle proprietà del dispositivo (inclusi i diritti di accesso)|X|X
Visualizzazione delle proprie proprietà del dispositivo (inclusi i diritti di accesso)|X|X
Creazione, aggiornamento, eliminazione del dispositivo (inclusi i diritti di accesso)|-|X
Visualizzazione dei ruoli|-|-
Creazione, aggiornamento, eliminazione dei ruoli personalizzati|-|-
Visualizzazione operazioni|-|-

### Operazioni di analisi {: #gateway-analytics-ops}

Operazioni di analisi || Ruoli del gateway|
:--------: | ---------------------|------------------------|
           | **Gateway standard** | **Gateway privilegiato** |
Visualizzazione delle regole di analisi|-|-
Gestione delle regole di analisi|-|-
Visualizzazione delle azioni di analisi|-|-
Gestione delle azioni di analisi|-|-
Visualizzazione degli avvisi di analisi|-|-
Visualizzazione degli schemi del messaggio di analisi|-|-
Gestione degli schemi del messaggio di analisi|-|-

### Operazioni del servizio di terze parti {: #gateway-third-party}

Operazioni del servizio di terze parti || Ruoli del gateway|
:--------: | ---------------------|------------------------
           | **Gateway standard** | **Gateway privilegiato**
Elaborazione delle notifiche batch da una piattaforma esterna|-|-
Elaborazione delle notifiche batch e loro invio alla piattaforma esterna|-|-
Pubblicazione di un evento per un dispositivo|-|-
Sottoscrizione a eventi da un dispositivo|-|-
Configurazione di un URL di callback per la piattaforma esterna|-|-
Configurazione del livello di sottoscrizione della piattaforma esterna|-|-
Ottenimento dello stato di integrità dal connector|-|-
Verifica se un sistema esterno è attivo e convalida delle credenziali|-|-
