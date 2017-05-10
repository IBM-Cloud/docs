---

copyright:
  years: 2017
lastupdated: "2017-04-11"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Accesso a ulteriori funzioni di Gestione delle API
{: #upgrade}

Gestione delle API ti consente di controllare le frequenze delle chiamate, OAuth e di visualizzare l'analisi. Puoi avere un maggiore controllo della gestione sulle API eseguendo l'upgrade al servizio {{site.data.keyword.apiconnect_full}}. Il servizio {{site.data.keyword.apiconnect_short}} fornisce ulteriori scelte di politiche di sicurezza e un maggiore controllo sui limiti di frequenza. Oltre a ciò, potrai configurare un portale degli sviluppatori pienamente personalizzabile in modo da poter generare un'interazione per le tue API e partecipare alla community degli sviluppatori. Altri vantaggi includono:
* Gestione del ciclo di vita
* API composite
* Integrazione dei servizi web
* Mediazione del protocollo
* Generazione di API dallo schema
* Sviluppo di microservizi

La migrazione al servizio {{site.data.keyword.apiconnect_short}} è facile e non devi ricreare nessuna delle API che stai gestendo con Gestione delle API.

## Migrazione di API a {{site.data.keyword.apiconnect_short}}
{: #migrate_api}

Se decidi di eseguire l'upgrade a {{site.data.keyword.apiconnect_full}}, dovrai migrare le tue API da Gestione delle API al servizio {{site.data.keyword.apiconnect_short}} completando la seguente procedura per ciascuna delle tue API: 

1. Scarica il documento Swagger per la API da Gestione delle API.
    1. Apri la tua applicazione e seleziona **Gestione delle API**.
	2. Seleziona la scheda **Explorer API**. Viene visualizzato un elenco delle tue API correlate a tale progetto.
    2. Scarica il documento Swagger per la tua API selezionando l'icona accanto al nome della API.
2. Crea e prepara l'istanza di {{site.data.keyword.apiconnect_short}}. 
    1. Crea un'istanza del servizio {{site.data.keyword.apiconnect_short}} dal catalogo {{site.data.keyword.Bluemix_notm}}.
	2. Seleziona il tuo piano.
	3. Seleziona **+Aggiungi** per creare un catalogo.
	4. Immetti un nome di visualizzazione e il nome per il tuo catalogo e seleziona **Aggiungi**.
	5. Seleziona il catalogo che hai creato.
3. Importa il documento Swagger nella tua istanza di {{site.data.keyword.apiconnect_short}} completando la seguente procedura:
	1. Dal dashboard del servizio {{site.data.keyword.apiconnect_short}}, seleziona **Passa a... (>>)** > **Bozze** nel menu.
	2. Seleziona la scheda API.
	3. Seleziona **+Aggiungi** > **Importa API da un file o URL**.
	4. Trova e seleziona il file Swagger che hai scaricato da Gestione delle API. Seleziona **Apri**.
	5. Seleziona **Importa** per impostare la tua API nel servizio {{site.data.keyword.apiconnect_short}}.
4. Specifica le impostazioni per la tua API.
    1. Seleziona **Crea prodotto**.
	2. Seleziona il prodotto che hai creato per visualizzarne le impostazioni.
	3. Imposta il limite della frequenza per la API.
	4. Imposta il livello per la API.
5. Aggiungi l'endpoint per la API, se necessario.
    1. Seleziona la API.
	2. Seleziona la scheda Assemblaggio.
	3. Aggiungi l'endpoint, se non è già specificato.
	
 Dopo che hai migrato le tue API, potrai accedere a tutte le funzioni di Gestione delle API aprendo il tile di servizio {{site.data.keyword.apiconnect_short}} e anche tramite il dashboard {{site.data.keyword.Bluemix_notm}}. 

 
