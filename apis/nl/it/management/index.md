---

copyright:
  years: 2017
lastupdated: "2017-04-12"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Panoramica
{: #index}

Puoi gestire le API in modo nativo in {{site.data.keyword.Bluemix}} se queste sono associate a un'azione {{site.data.keyword.openwhisk_short}} o a un elenco crescente di servizi {{site.data.keyword.Bluemix_notm}}, come il servizio {{site.data.keyword.appconserviceshort}}. La gestione delle API ti consente di controllare l'utilizzo, incrementare l'adozione e monitorare le statistiche.

Come mostrato nel seguente diagramma, la Gestione API funziona inserendo un gateway veloce e leggero davanti agli endpoint cloud esistenti. Il gateway, indicato nel diagramma come Gateway API, è responsabile di rispondere alle chiamate API in entrata dalle applicazioni. Il Gateway API fornisce un insieme completo di politiche API per la protezione, la gestione del traffico, la mediazione, l'accelerazione e il supporto di protocolli non HTTP.

![Flusso del Gateway API.](images/bluemix-native-apim-flow_ow.png "API management flow.")

Quando esponi un'API, la rendi disponibile all'utilizzo da parte di altre persone. Questo spesso significa fornire agli utenti dell'API un accesso limitato alle informazioni che si trovano sui server da te gestiti. Questo accesso consente un'esperienza clienti più semplice per gli utenti finali in quanto possono accedere alle informazioni direttamente dall'interfaccia corrente.

Ci sono dei casi in cui potresti voler controllare alcune attività sui tuoi server. Ad esempio, se in un server ci sono troppe richieste API nell'arco di un breve lasso di tempo, il server può diventare sovraccarico e arrestarsi. Per evitare situazioni come questa, puoi gestire la frequenza delle chiamate API utilizzando la Gestione API. Il gateway leggero collegato all'API traccia il numero di chiamate alla tua API e impone dei limiti su quante chiamate essa dovrà accettare. La Gestione API ti consente inoltre di tracciare il volume di chiamate API da una determinata origine registrando la sua chiave API. La chiave API è una stringa univoca che il team di sviluppo API fornisce al team di utilizzatori API che consente allo sviluppatore di monitorare le statistiche sulle chiamate generate dalle richieste del team di utilizzatori.  

Con la Gestione API {{site.data.keyword.Bluemix_notm}} sono disponibili le seguenti funzioni:
## Analisi API
{: #basic_analytics notoc}

Se vuoi monetizzare l'uso delle tue API, puoi utilizzare la funzione di analisi per tracciare l'utilizzo delle chiamate. Inoltre, puoi monitorare l'utilizzo per comprendere in che modo vengono utilizzate le tue API al fine di poter prendere decisioni mirate su come aggiornare le API per incrementare l'adozione. 

Puoi visualizzare le seguenti statistiche sulle tue API:
* Il numero di risposte e il tempo medio di risposta durante l'ultima ora o l'intervallo di tempo specificato.
* Il numero di chiamate API al minuto.
* Le ultime 100 risposte.

## Limite di frequenza per sottoscrizione (chiave API)
{: #rate_limit notoc}

Puoi imporre un limite di frequenza per gestire il numero di chiamate che le applicazioni possono effettuare alle tue API. Puoi specificare un limite di frequenza per consentire di effettuare solo uno specifico numero di chiamate al secondo, al minuto o all'ora in modo che, ad esempio, il tuo backend non venga sovraccaricato. Puoi impostare questo limite per l'API globale o per ogni chiave API. 

## OAuth
{: #oauth notoc}

Per interrompere l'utilizzo indesiderato dei dati da te forniti, puoi garantire che solo gli utenti con l'autenticazione corretta possano accedere alle tue API. Puoi controllare l'accesso alle tue API attraverso lo standard di autorizzazione OAuth. OAuth è un protocollo di autorizzazione basato su token che consente ai siti web o alle applicazioni di terze parti di accedere ai dati degli utenti senza richiedere all'utente di condividere le informazioni personali.

## CORS
{: #cors notoc}

CORS consente agli script incorporati in una pagina web di chiamare l'API tra i confini di domini. Questo si traduce in un vantaggio per l'utente dell'API in quanto consente all'API di recuperare le informazioni da un altro dominio quando viene richiamato dall'API. Senza l'abilitazione di CORS, qualsiasi recupero dei contenuti è limitato allo stesso dominio della richiesta di origine. Per ulteriori informazioni su CORS e su come implementarlo, vedi [HTTP access control (CORS) ![icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://developer.mozilla.org/en-US/docs/Web/HTTP/Access_control_CORS.html){: new_window}.

## Ulteriori opzioni di gestione API
{: #add_mgt_options notoc}

Queste funzioni per la gestione dell'API sono disponibili nella scheda Gestione API del tuo dashboard {{site.data.keyword.openwhisk_short}} o App Connect. Per soluzioni di gestione più complesse, puoi effettuare l'aggiornamento al servizio completo {{site.data.keyword.apiconnect_full}} per accedere a ulteriori funzioni come le strategie di analisi dettagliata e di creazione pacchetti per le tue API o a un portale sviluppatori per socializzare le API. Vedi [Introduzione a API Connect](https://console.ng.bluemix.net/docs/services/apiconnect/index.html){: new_window} per ulteriori informazioni sul servizio {{site.data.keyword.apiconnect_full}}.

Per ulteriori informazioni sull'aggiornamento delle API gestite in {{site.data.keyword.Bluemix_notm}} al servizio {{site.data.keyword.apiconnect_short}}, vedi [Accesso ad altre funzioni di gestione delle API](upgrade.html).

