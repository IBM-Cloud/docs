---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Protezione delle risorse di back-end 
{: #protecting-resources}

L'SDK server {{site.data.keyword.appid_short}} fornisce le strategie per la protezione di due tipi di risorse: applicazioni web e API.
{:shortdesc}


## Accesso alle risorse protette dalle SDK client 
{: #accessing}

Il richiamo di una risorsa protetta avvia il widget di accesso, se necessario. Se è già stato ottenuto un token valido, il widget di accesso non viene avviato e si accede direttamente alla risorsa.


### Utilizzo dell'SDK Swift 
{: #requesting-swift notoc}

1. Importa BMSCore.

  ```swift
  import BMSCore
  ```
  {:pre}

2. Richiama una richiesta della risorsa protetta. 

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //il codice gestisce la risposta qui
  })
  ```
  {:pre}


### Utilizzo dell'SDK Android 
{: #requesting-android notoc}

1. Richiama una richiesta della risorsa protetta. 

  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
		public void onSuccess (Response response) {
     //il codice gestisce la risposta qui
  }
  @Override
		public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //il codice gestisce la risposta qui
  });
  ```
  {:pre}



## Filtri di autorizzazione
{: #auth-filter}

La strategia di protezione API restituisce una risposta HTTP 401 con un elenco di ambiti per ottenere l'autorizzazione per un client non autenticato. La strategia di protezione dell'applicazione web restituisce un reindirizzamento HTTP 302. Il reindirizzamento invia un client non autenticato alla pagina di accesso che è ospitata dal servizio {{site.data.keyword.appid_short_notm}} o direttamente a una pagina di accesso del provider di identità, a seconda della configurazione.



### Strategia API
{: #api notoc}

La strategia API si attende che le richieste contengano un'intestazione di autorizzazione con un token di accesso valido. La risposta può inoltre includere un token di identità, ma non è obbligatorio; consulta [Token di identità e accesso](/docs/services/appid/about.html#acess-and-identity).

Se un token non è valido o è scaduto, la strategia API restituisce un errore HTTP 401 che contiene le seguenti informazioni: Www-Authenticate=Bearer scope="{scope}" error="{error}". Il componente `error` è facoltativo.

Se la richiesta restituisce un token valido, il controllo viene passato al prossimo middleware e la proprietà `appIdAuthorizationContext` viene trasmessa nell'oggetto della richiesta. Questa proprietà contiene i token di identità e di accesso originali, così come le informazioni sul payload decodificate come oggetti JSON semplici.


### Strategia applicazione web
{: #web notoc}

Quando la classe della strategia dell'applicazione web individua dei tentativi non autenticati di accesso a una risorsa protetta, automaticamente esegue il reindirizzamento a un browser dell'utente alla pagina di autenticazione. Dopo un'autenticazione corretta, l'utente viene riportato all'URL di callback dell'applicazione web. Il servizio utilizza la classe della strategia dell'applicazione web per ottenere i token di accesso e di identità. Dopo aver ottenuto questi token, la classe della strategia dell'applicazione web li archivia in una sessione HTTP in `WebAppStrategy.AUTH_CONTEXT`. Spetta all'utente decidere se archiviare i token di accesso e di identità nel database dell'applicazione.

## Intestazione di autorizzazione
{: #auth-header}

L'intestazione di autorizzazione nella richiesta in entrata consiste di tre parti separate da spazi bianchi: Bearer, Token di accesso e ID token. Il token di accesso è un componente obbligatorio e l'ID token è facoltativo. La struttura di intestazione prevista è: Authorization=Bearer {access_token} [{id_token}]
