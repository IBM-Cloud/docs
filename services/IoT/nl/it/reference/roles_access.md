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

# Livelli di accesso per i ruoli utente

Le seguenti tabelle mostrano il livello di accesso per ogni ruolo dell'utente.

Le tabelle mostrano i livelli di accesso per:
- [Operazioni del dispositivo ](#user-device-ops)
- [Operazioni di log ](#user-log-ops)
- [Operazioni cache ](#user-cache-ops)
<!-- [Historian Operations](#user-historian) -->
- [Operazioni dell'organizzazione ](#user-org-ops)
- [Operazioni di controllo dell'accesso ](#user-access-ops)
- [Operazioni di analisi ](#user-analytics-ops)
- [Operazioni di terze parti](#user-third-party)  
<!-- - [Risk Management Operations](#user-risk-mgt) -->

## Autorizzazioni del ruolo utente {: #user-roles}

### Operazioni del dispositivo {: #user-device-ops}

Operazioni del dispositivo ||| Ruoli utente|||
:--------: | -------------|-------------|---------------|-----|---
           | **Amministratore** | **Operatore** | **Sviluppatore** | **Analista** | **Lettore**
Creazione, aggiornamento o eliminazione dispositivi | X | X | X | - | -
Visualizzazione dispositivi | X | X | X | X | X
Attivazione dispositivo | X | X | X | - | -
Pubblicazione di un evento | - | - | - | - | -
Sottoscrizione a un evento | X | X | X | X | X
Pubblicazione di un comando | X | X | X | - | -
Sottoscrizione a un comando | - | - | - | - | -
Avvio dell'azione di gestione del dispositivo | X | X | X | - | -
Visualizzazione azioni di gestione del dispositivo | X | X | X | X | X
Annullamento azioni di gestione del dispositivo | X | X | X | - | -
Gestione dei bundle dell'azione di gestione del dispositivo | X | X | X | - | -
Creazione, aggiornamento o eliminazione dei tipi di dispositivo | X | X | X | - | -
Visualizzazione tipi di dispositivo | X | X | X | X | X
Gestione log di diagnostica | X | X | X | - | -
Visualizzazione log di diagnostica | X | X | X | - | -

### Operazioni di log {: #user-log-ops}

Operazioni di log ||| Ruoli utente|||
:--------: | -------------|-------------|---------------|-----|---
           | **Amministratore** | **Operatore** | **Sviluppatore** | **Analista** | **Lettore**
Visualizzazione log del server | X | X | X | X | X

### Operazioni cache {: #user-cache-ops}

Operazioni cache ||| Ruoli utente|||
:--------: | -------------|-------------|---------------|-----|---
           | **Amministratore** | **Operatore** | **Sviluppatore** | **Analista** | **Lettore**
Visualizzazione dati live (cache evento) | X | X | X | X | X
Gestione dei dati live (cache evento) | X	| X | X |	X	| -

### Operazioni dell'organizzazione {: #user-org-ops}

Operazioni dell'organizzazione ||| Ruoli utente|||
:--------: | -------------|-------------|---------------|-----|---
           | **Amministratore** | **Operatore** | **Sviluppatore** | **Analista** | **Lettore**
Configurazione dei parametri di archiviazione|	X| - |-|-|-
Configurazione del provider di autenticazione|	X|-|-|-|-				
Creazione, visualizzazione, aggiornamento, eliminazione della configurazione email	|X|-|-|-|-				
Visualizzazione dei provider di posta IoTP disponibili	|X|	X|-|-|-			
Creazione, visualizzazione, aggiornamento, eliminazione dei template dell'email	|X	|X	|-|-|-		
Creazione, aggiornamento, eliminazione degli utenti	|X|	X|-|-|-
Visualizzazione utenti	|X|	X|	X|	X|-
Creazione, aggiornamento, eliminazione degli inviti utente|	X	|X	| -|-|-
Visualizzazione degli inviti utente	|X	|X	|- |- |-
Completamento dell'invito	|X|	X|	X|	X|	X
Creazione, aggiornamento, eliminazione delle chiavi API	|X	|X	| -|-|-
Visualizzazione delle chiavi API	|X	|X	|- |- |-		
Visualizzazione delle informazioni sull'utilizzo dell'organizzazione	|X	|X	| -|-|-		

### Operazioni di controllo dell'accesso {: #user-access-ops}

Operazioni di controllo dell'accesso ||| Ruoli utente|||
:--------: | -------------|-------------|---------------|-----|---
           | **Amministratore** | **Operatore** | **Sviluppatore** | **Analista** | **Lettore**
Visualizzazione delle proprietà degli utenti, inclusi i diritti di accesso	|X|	X|	X|	X| -
Visualizzazione delle proprie proprietà utente, inclusi i diritti di accesso	|X|	X|	X|	X|	X
Gestione degli utenti, inclusi i diritti di accesso	|X	|X	|-|-|-
Visualizzazione delle proprietà della chiave API, inclusi i diritti di accesso|	X|	X|	X|	X|-
Visualizzazione delle proprie proprietà della chiave API, inclusi i diritti di accesso	|-|	-|	-| -| -		
Creazione, aggiornamento, eliminazione della chiave API, inclusi i diritti di accesso	|X	|X	|-|-|-
Visualizzazione delle proprietà del dispositivo, inclusi i diritti di accesso	|X|	X|	X|	X|	X
Visualizzazione delle proprie proprietà del dispositivo, inclusi i diritti di accesso	|-	|- |- |- |-
Creazione, aggiornamento, eliminazione del dispositivo, inclusi i diritti di accesso	|X|	X|	X|	-| -
Visualizzazione dei ruoli	|X	|X	|X	|X	|X
Creazione, aggiornamento, eliminazione dei ruoli personalizzati	|X	|X |- |- |-
Visualizzazione delle operazioni*	|X	|X	|X	|X	|X

### Operazioni di analisi {: #user-analytics-ops}

Operazioni di analisi ||| Ruoli utente|||
:--------: | -------------|-------------|---------------|-----|---
           | **Amministratore** | **Operatore** | **Sviluppatore** | **Analista** | **Lettore**
Visualizzazione delle regole di analisi|	X|	X|	X|	X|	X
Gestione delle regole di analisi|	X|	X|	X|	X| -
Visualizzazione delle azioni di analisi|	X|	X|	X|	X|	X
Gestione delle azioni di analisi|	X|	X|	X|	X| -
Visualizzazione degli avvisi di analisi|	X|	X|	X|	X|	X
Visualizzazione degli schemi del messaggio di analisi|	X|	X|	X|	X|	X
Gestione degli schemi del messaggio di analisi|	X|	X|	X|	X| -

### Operazioni del servizio di terze parti {: #user-third-party}

Operazioni del servizio di terze parti ||| Ruoli utente|||
:--------: | -------------|-------------|---------------|-----|---
           | **Amministratore** | **Operatore** | **Sviluppatore** | **Analista** | **Lettore**
Elaborazione delle notifiche batch da una piattaforma esterna	|X|	X	|X |-|-
Elaborazione delle notifiche batch e loro invio alla piattaforma esterna	|X|	X	|X| -| -
Pubblicazione di un evento per un dispositivo	|X|	X	|X|	- |-
Sottoscrizione a eventi da un dispositivo	|X	|X	|X |-| -
Configurazione di un URL di callback per la piattaforma esterna	|X	|X	|X|	-| -
Configurazione del livello di sottoscrizione della piattaforma esterna|	X|	X|	X |- |-
Ottenimento dello stato di integrità dal connector	|X|	X	|X	|- |-
Verifica se un sistema esterno è attivo e convalida delle credenziali	|X	|X|	X	|- |-
