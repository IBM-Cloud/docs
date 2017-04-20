---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Intestazioni e filtri di autorizzazione
{: #auth}

L'SDK server {{site.data.keyword.appid_short}} fornisce le strategie per la protezione di due tipi di risorse: applicazioni web e API.
{:shortdesc}


## Filtri di autorizzazione
{: #auth-filter}

La strategia di protezione API restituisce una risposta HTTP 401 con un elenco di ambiti per ottenere l'autorizzazione per un client non autenticato. La strategia di protezione dell'applicazione web restituisce un reindirizzamento HTTP 302. Il reindirizzamento invia un client non autenticato alla pagina di accesso che è ospitata dal servizio {{site.data.keyword.appid_short_notm}} o direttamente a una pagina di accesso del provider di identità, a seconda della configurazione.



### Strategia API
{: #api}

La strategia API si attende che le richieste contengano un'intestazione di autorizzazione con un token di accesso valido. La risposta può inoltre includere un token di identità, ma non è obbligatorio; consulta [Token di identità e accesso](/docs/services/appid/access-identity.html#access-and-identity).

Se un token non è valido o è scaduto, la strategia API restituisce un errore HTTP 401 che contiene le seguenti informazioni: Www-Authenticate=Bearer scope="{scope}" error="{error}". Il componente `error` è facoltativo.

Se la richiesta restituisce un token valido, il controllo viene passato al prossimo middleware e la proprietà `appIdAuthorizationContext` viene trasmessa nell'oggetto della richiesta. Questa proprietà contiene i token di identità e di accesso originali, così come le informazioni sul payload decodificate come oggetti JSON semplici.


### Strategia applicazione web
{: #web}

Quando la classe della strategia dell'applicazione web individua dei tentativi non autenticati di accesso a una risorsa protetta, automaticamente esegue il reindirizzamento a un browser dell'utente alla pagina di autenticazione. Dopo un'autenticazione corretta, l'utente viene riportato all'URL di callback dell'applicazione web. Il servizio utilizza la classe della strategia dell'applicazione web per ottenere i token di accesso e di identità. Dopo aver ottenuto questi token, la classe della strategia dell'applicazione web li archivia in una sessione HTTP in `WebAppStrategy.AUTH_CONTEXT`. Spetta all'utente decidere se archiviare i token di accesso e di identità nel database dell'applicazione.

## Intestazione di autorizzazione
{: #auth-header}

L'intestazione di autorizzazione nella richiesta in entrata consiste di tre parti separate da spazi bianchi: Bearer, Token di accesso e ID token. Il token di accesso è un componente obbligatorio e l'ID token è facoltativo. La struttura di intestazione prevista è: Authorization=Bearer {access_token} [{id_token}]
