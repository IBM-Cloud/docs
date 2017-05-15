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

# Accesso ad altre funzioni di gestione delle API
{: #upgrade}

La gestione delle API ti consente di controllare le frequenze di chiamata, applicare l'OAuth e visualizzare le analisi. Puoi avere un maggiore controllo sulla gestione delle API effettuando l'aggiornamento al servizio {{site.data.keyword.apiconnect_full}}. Il servizio {{site.data.keyword.apiconnect_short}} fornisce una più ampia scelta di politiche di sicurezza e un maggiore controllo sui limiti di frequenza. Oltre a questo, sarai in grado di configurare un Portale sviluppatori completamente personalizzabile in modo da poter socializzare le tue API e coinvolgere la community di sviluppatori. Altri vantaggi: 
* Gestione del ciclo di vita
* API composite
* Integrazione dei servizi Web
* Mediazione dei protocolli
* Generazione di API da uno schema
* Sviluppo di microservizi

La migrazione al servizio {{site.data.keyword.apiconnect_short}} è semplice e non è necessario ricreare alcuna API gestita tramite la Gestione API.

## Migrazione delle API a {{site.data.keyword.apiconnect_short}}
{: #migrate_api}

Se decidi di effettuare l'aggiornamento a {{site.data.keyword.apiconnect_full}}, dovrai migrare le tue API da Gestione API al servizio {{site.data.keyword.apiconnect_short}} completando la seguente procedura per ciascuna delle tue API: 

1. Scarica il documento Swagger per l'API da Gestione API.
    1. Apri la tua applicazione e seleziona **Gestione API**.
	2. Seleziona la scheda **Explorer API**. Viene visualizzato un elenco delle tue API correlate a tale progetto.
    2. Scarica il documento Swagger per la tua API selezionando l'icona accanto al nome dell'API.
2. Crea e prepara l'istanza {{site.data.keyword.apiconnect_short}}. 
    1. Crea un'istanza del servizio {{site.data.keyword.apiconnect_short}} dal catalogo {{site.data.keyword.Bluemix_notm}}.
	2. Seleziona il tuo piano.
	3. Seleziona **+Aggiungi** per creare un catalogo.
	4. Immetti un nome di visualizzazione e un nome per il tuo catalogo e seleziona quindi **Aggiungi**.
	5. Seleziona il catalogo che hai creato.
3. Importa il documento Swagger nella tua istanza {{site.data.keyword.apiconnect_short}} completando la seguente procedura:
	1. Dal dashboard del servizio {{site.data.keyword.apiconnect_short}}, seleziona **Passa a... (>>)** > **Bozze** nel menu.
	2. Seleziona la scheda API.
	3. Seleziona **+Aggiungi** > **Importa API da un file o URL**.
	4. Trova e seleziona il file Swagger che hai scaricato da Gestione API. Seleziona **Apri**.
	5. Seleziona **Importa** per importare la tua API nel servizio {{site.data.keyword.apiconnect_short}}.
4. Specifica le impostazioni per la tua API.
    1. Seleziona **Crea prodotto**.
	2. Seleziona il prodotto che hai creato per visualizzarne le impostazioni.
	3. Imposta il limite di frequenza per l'API.
	4. Imposta il livello per l'API.
5. Se necessario, aggiungi l'endpoint per l'API.
    1. Seleziona l'API.
	2. Seleziona la scheda Assembla.
	3. Aggiungi l'endpoint, se non è già stato specificato.
	
 Dopo aver migrato le tue API, sarai in grado di accedere a tutte le funzioni di gestione delle API aprendo il tile del servizio {{site.data.keyword.apiconnect_short}} o tramite il dashboard {{site.data.keyword.Bluemix_notm}}. 

 
