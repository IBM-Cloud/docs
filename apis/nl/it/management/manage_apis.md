---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Gestisci API
{: #manage_apis}

Dopo aver integrato la tua API in modo che venga gestita e monitorata dal sistema di gestione delle API, puoi visualizzarne e modificarne le impostazioni. Se non hai integrato la tua API, devi integrarne una completando la procedura descritta in [Creazione di API dalle azioni {{site.data.keyword.openwhisk_short}}](manage_openwhisk_apis.html). 

Per gestire le impostazioni per la tua API, completa la seguente procedura:

Se hai creato una nuova API ed è già aperta nell'interfaccia, puoi ignorare i primi tre passi.

1. Seleziona l'API che vuoi gestire selezionando un'azione dal dashboard del servizio {{site.data.keyword.openwhisk_short}}, se le informazioni relative alla tua API non sono già visualizzate. 
2. Se necessario, seleziona la scheda **API**.
3. Se necessario, seleziona l'API che vuoi gestire. Quando viene stabilita una connessione, sono disponibili le seguenti selezioni che puoi visualizzare e aggiornare:
    * Riepilogo
    * Definizione
    * Condivisione
    * Explorer API
4. Seleziona lo slider Esponi API gestita per attivarlo ed esporre la tua API. Nota: se l'API non è esposta, alcune impostazioni non possono essere impostate.  

## Riepilogo delle impostazioni per le API
{: #overview_api}

La scheda Riepilogo viene selezionata per impostazione predefinita quando selezioni un'API ed è suddivisa in due sezioni:
* Proprietà - Nella sezione Proprietà puoi visualizzare le seguenti informazioni:
    * Informazioni di base sulla tua API
	* Politiche di sicurezza
	* Informazioni sul limite di frequenza
    * Dettagli di condivisione
* Sezione Analisi e registrazione - Nella sezione Analisi e registrazione puoi visualizzare le seguenti statistiche:
	* Numero di risposte e tempo medio di risposta durante l'ultimo intervallo di tempo specificato
    * Numero di chiamate API al minuto in formato grafico
    * Ultime 100 risposte nella tabella Log risposte
	
Il grafico *Risposte* mostra una rapida rappresentazione di quante risposte ha ricevuto la tua API e la suddivisione dello stato delle risposte. Questo può aiutarti a determinare se ricevi una maggioranza di risposte di errore. La maggioranza di risposte di errore può indicare che hai più traffico rispetto a quello consentito nelle impostazioni di frequenza. Passando il mouse sull'icona delle informazioni, puoi vedere una suddivisione numerica delle risposte per codice di risposta. Quelli che seguono sono dei codici di risposta comuni:
* 200  OK
* 201 Creato
* 302  Trovato
* 304  Non modificato
* 400  Richiesta non valida
* 401  Non autorizzato
* 403  Non consentito
* 500  Errore interno del server
* 503  Servizio non disponibile

La tabella Log risposte contiene i singoli dettagli delle ultime 100 risposte. Puoi ordinare le informazioni in base alle voci di una colonna selezionando l'intestazione della colonna. Puoi anche cercare specifiche voci nella tabella Log risposte utilizzando la barra *Cerca risposte*. Per visualizzare ulteriori informazioni su un evento è possibile selezionarlo oppure fare clic su **Visualizza dettagli** nell'elenco dei menu di opzioni (tre punti verticali) accanto alla voce.


## Modifica delle impostazioni dell'API
{: #settings_api}

Nella scheda **Definizione**, puoi aggiornare le informazioni di base sulla tua API. Queste informazioni includono la documentazione, il nome e l'URL di base. Utilizza la sezione Sicurezza e limite di frequenza per specificare un limite di chiamata e intervallo per assicurarsi che venga effettuata solo una certa quantità di chiamate al secondo, al minuto o all'ora. Puoi inoltre richiedere l'autenticazione per creare chiamate API per impedire l'utilizzo indesiderato dei dati o per raccogliere statistiche sull'API.

Per modificare le impostazioni per un'API, completa la seguente procedura:

1. Nel dashboard di gestione API, fai clic sulla scheda **Definizione**.
2. Puoi specificare o aggiornare il nome della tua API e importare una definizione API nella sezione Informazioni API.
3. Nella sezione Sicurezza e limite di frequenza, puoi aggiornare le seguenti politiche:
    * Richiedi chiave API - Specifica se la chiamata API può essere elaborata solo quando viene fornita la chiave API corretta. L'impostazione predefinita non richiede un'ulteriore chiave.
    * Metodo di sicurezza - Quando l'opzione di chiave API è selezionata, specifica se l'elaborazione dell'API richiede solo la chiave o se richiede sia la chiave che il segreto API. 
    * Ubicazione della chiave e del segreto API - A seconda dell'impostazione che hai scelto per il metodo, specifica in che modo le informazioni sulla sicurezza API vengono incluse nella chiamata. I Nomi chiamata specificano come vengono identificate le informazioni sulla sicurezza. 
    * Limita frequenza di chiamata API - Imposta il numero di chiamate API consentite durante un intervallo di tempo specificato, con l'opzione di impostarlo per ogni chiave. Nota che viene utilizzato un metodo di limite di frequenza di tipo burst. La frequenza media delle chiamate API viene calcolata nell'intervallo di tempo totale specificato nella frequenza. Se la frequenza delle chiamate API durante un intervallo supera la frequenza media delle chiamate, ci potrebbe essere un periodo di chiamate negate fino al limite di tempo specificato nella frequenza.   
    * Provider OAuth - Assicura che gli utenti con i parametri di sicurezza corretti possano accedere alle tue API applicando l'OAuth attraverso le credenziali di accesso di provider social come Google, Facebook, IBM e GitHub.
4. Abilita CORS - CORS (cross-origin requests) abilita alcune richieste limitate da un dominio diverso.
5. Fai clic su **Salva**.

## Condivisione delle API
{: #share_api}

Puoi condividere le API con altri utenti all'interno o all'esterno della tua organizzazione {{site.data.keyword.Bluemix_notm}}.

Quando condividi le API con altri utenti, sia all'interno che all'esterno della tua organizzazione {{site.data.keyword.Bluemix_notm}}, puoi creare delle chiavi per le tue API. Ogni API gestita supporta 5 chiavi che possono essere create e assegnate a tale API. Inviando una chiave univoca a un individuo o a un'azienda, puoi tenere traccia di alcune statistiche su come viene utilizzata questa API. Ad esempio, puoi tracciare il numero di chiamate alla tua API da parte di una determinata persona o azienda. 

Puoi anche limitare il numero di chiamate alla chiave, disabilitare una chiave o limitare le chiamate da una chiave. Ciò può essere utile durante la verifica, il bilanciamento del carico di lavoro, la monetizzazione o per affrontare alcune situazioni di sicurezza.   

1. Nel dashboard di gestione API, fai clic sulla scheda **Condivisione**.
2. Nell'area "Condivisione all'interno dell'organizzazione {{site.data.keyword.Bluemix_notm}}", seleziona **Condividi API con tutti gli utenti nell'organizzazione Bluemix** se vuoi che la tua API sia disponibile agli altri utenti con accesso alla tua organizzazione {{site.data.keyword.Bluemix_notm}}. Questa opzione deve essere selezionata per generare una chiave.
3. Fai clic su **Crea chiave API** per creare una chiave univoca per la tua API. Viene visualizzata la finestra di dialogo Crea chiave API. La chiave API viene generata automaticamente.
4. Utilizza la chiave API per determinare quale utente accederà all'API inviando a un utente una chiave univoca. Il gateway può determinare quale chiave (e cliente) sta generando la chiamata.
5. Fai clic sull'icona **Menu** (tre punti verticali) accanto alla chiave per modificare o eliminare tale chiave API. 

Nella sezione Condivisione all'esterno dell'organizzazione {{site.data.keyword.Bluemix_notm}}, puoi condividere la tua API con gli utenti che non dispongono di un account {{site.data.keyword.Bluemix_notm}}. Questo metodo di condivisione fornisce un link diretto per visualizzare le informazioni sull'API nell'Explorer API. L'API contiene un pulsante per la sua esecuzione nella vista Explorer API. Per richiedere un link per la tua API, completa la seguente procedura:

1. Nella sezione "Condivisione all'esterno dell'organizzazione {{site.data.keyword.Bluemix_notm}}", fai clic su **Crea chiave API**. Viene visualizzata la finestra di dialogo Crea chiave API.
     Nota che l'utente dispone di un segreto che tu non puoi controllare.
2. Fornisci un nome univoco per la chiave API.
3. Seleziona **Crea chiave**. 
4. Invia il link del portale API al cliente senza un account {{site.data.keyword.Bluemix_notm}}. La chiave API e il segreto (se utilizzato) vengono inclusi nel link, pertanto puoi ancora determinare quale chiave ha generato il link.
  
Il link alla documentazione API apre l'API nella scheda **Explorer API**.

## Visualizzazione e verifica con Explorer API
{: #explore_api}

Seleziona la scheda Explorer API per visualizzare l'html generato dalla tua documentazione Swagger. 

L'Explorer API mostra tutte le azioni API e la documentazione da applicare all'API. Puoi visualizzare le operazioni, le azioni e le rispettive descrizioni e verificare l'API dall'interfaccia utente. Puoi anche scaricare la documentazione Swagger per riutilizzarne il contenuto.

Per verificare l'API, completa la seguente procedura:
1. L'opzione *Esempi* è selezionata per impostazione predefinita. Questa mostra un esempio del codice per l'API selezionata.
2. Modifica, se necessario, il formato dell'esempio selezionando un linguaggio dal menu accanto al linguaggio specificato. 
3. Seleziona **Provalo**.
4. Seleziona **Richiama operazione**. 

Viene visualizzata la risposta alla richiesta.   
