---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Informazioni su {{site.data.keyword.appid_short_notm}}
{: #about}

Con {{site.data.keyword.appid_full}} gli sviluppatori possono proteggere e aggiungere l'autenticazione alle loro applicazioni {{site.data.keyword.Bluemix}}, con poche righe di codice. Gli sviluppatori possono anche gestire i dati specifici dell'utente per creare esperienze dell'applicazione personalizzate.
{:shortdesc}


Puoi utilizzare il servizio nei seguenti modi:

* Per aggiungere l'autenticazione alle tue applicazioni mobili e web
* Per concedere l'accesso a risorse di back-end protette e alle applicazioni web
* Per proteggere le applicazioni Node.js e Swift ospitate su {{site.data.keyword.Bluemix_notm}}
* Per memorizzare i dati utente, ad esempio le preferenze dell'applicazione o le informazioni dai loro profili social pubblici
* Per utilizzare i dati memorizzati per creare esperienze dell'applicazione personalizzate
* Per proteggere le risorse per gli utenti anonimi e autenticati

**Nota**: i protocolli implementati sono completamente conformi con OpenID Connect (OIDC).


## Componenti
{: #components}

* Dashboard - Scarica gli esempi di accoglienza e integrazione, consulta i log dell'attività, configura vari tipi di autenticazione e identifica i provider
* SDK client - Crea le applicazioni mobili e web che utilizzano il servizio per implementare l'autenticazione utente
    * Prerequisiti per Android: API 25 o superiore, Java 8.x, strumenti SDK Android 25.2.5 o superiore, strumenti piattaforma SDK Android 25.0.3 o superiore, strumenti di build Android versione 25.0.2
    * Prerequisiti per iOS: iOS9 o superiore, MacOS 10.11.5, Xcode 8.2
* SDK Server - Protegge le risorse ospitate in {{site.data.keyword.Bluemix_notm}}
    * I runtime supportati sono Node.js e Swift

## Panoramica sull'architettura

![Diagramma architettura {{site.data.keyword.appid_short_notm}}](/images/appid_architecture.png)

Figura 1. Diagramma architettura {{site.data.keyword.appid_short_notm}}

Puoi proteggere le tue risorse cloud con l'SDK server {{site.data.keyword.appid_short_notm}}. Utilizza la classe di richiesta fornita dall'SDK client {{site.data.keyword.appid_short_notm}} per comunicare con le tue risorse cloud protette.

* L'SDK server rileva una richiesta non autorizzata e restituisce la richiesta di verifica dell'autorizzazione HTTP 401.
* L'SDK client rileva la richiesta di verifica dell'autorizzazione HTTP 401 e avvia automaticamente il processo di autenticazione basato sulla configurazione dei provider di identità.
* Viene tentata l'autenticazione in base ai provider di identità correntemente configurati.
* Dopo una corretta autenticazione, il servizio restituisce i token di identità e autorizzazione.
* L'SDK client aggiunge automaticamente il token di autorizzazione alla richiesta originale e reinvia la richiesta alla risorsa cloud.
* L'SDK server estrae il token di accesso dalla richiesta e lo convalida con {{site.data.keyword.appid_short_notm}}.
L'accesso viene concesso e la risposta viene restituita all'applicazione.


## Flusso della richiesta
{: #request}

Il seguente diagramma descrive in che modo una richiesta fluisce dall'SDK client ai tuoi provider di identità e all'applicazione di back-end. 

![Flusso della richiesta {{site.data.keyword.appid_short_notm}}](/images/appidflow.png)


* Usa l'SDK client {{site.data.keyword.appid_short_notm}} per effettuare una richiesta alle tue risorse di back-end protette con l'SDK server {{site.data.keyword.appid_short_notm}}.
* L'SDK server {{site.data.keyword.appid_short_notm}} rileva una richiesta non autorizzata e restituisce il codice HTTP 401 e l'ambito di autorizzazione. 
* L'SDK client rileva automaticamente l'HTTP 401 e avvia il processo di autenticazione. 
* Quando l'SDK client contatta il servizio, l'SDK server restituisce il widget di accesso se è configurato più di un provider di identità. {{site.data.keyword.appid_short_notm}} richiama il provider di identità e presenta il modulo di accesso per tale provider o restituisce un codice concesso che permette l'autenticazione se non è stato configurato alcun provider di identità.
* {{site.data.keyword.appid_short_notm}} chiede all'applicazione client di autenticarsi fornendo una richiesta di verifica dell'autenticazione.
* Se sono configurati Facebook o Google e l'utente accede, l'autenticazione viene gestita dal flusso OAuth del provider di identità corrispondente.
* Se l'autenticazione termina con lo stesso codice concesso, il codice viene inviato all'endpoint del token. L'endpoint restituisce due token: un token di accesso e un token di identità. Da questo punto in avanti, tutte le richieste effettuate con l'SDK client hanno un'intestazione di autorizzazione di nuova acquisizione. 
* L'SDK client reinvia automaticamente la richiesta originale che ha attivato il flusso di autorizzazione. 
* L'SDK server estrae l'intestazione di autorizzazione dalla richiesta, convalida l'intestazione con il servizio e concede l'accesso a una risorsa di back-end. 

## Token di identità e accesso
{: #access-and-identity}

{{site.data.keyword.appid_short}} utilizza due tipi di token: accesso e identità. I token sono creati come <a href="https://jwt.io/introduction/" target="_blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.


### Token di accesso
{: #access-tokens notoc}

Il token di accesso abilita le comunicazioni con le risorse protette dai filtri di autorizzazione {{site.data.keyword.appid_short_notm}}, consulta [Protezione delle risorse di back-end](/docs/services/appid/protecting-resources.html).
Il token è conforme alle specifiche JavaScript Object Signing and Encryption (JOSE) ed ha il seguente formato:

```
Intestazione: {

    "typ": "JOSE", // tipo di intestazione, in base alla specifica

    "alg": "RS256", // algoritmo, in base alla specifica

}
Payload: {

    "iss": "", // emittente, il server AppID che ha emesso il token. StringOrURL

    "sub": "", // soggetto, chi ha emesso questo token. Molto probabilmente userId

    "aud": "", // pubblico, a chi è destinato questo token. OAuth2 client_id.

    "exp: "", // data/ora di scadenza, ora di eliminazione

    "iat": "", // emesso nella data/ora, ora di eliminazione

    "tenant": "xxx", il AppID tenantId per cui è stato emesso il token

    "auth_by": "appid_anon / appid_facebook / appid_google",

    "scope": "", // i motivi per cui è stato emesso questo token

}
```
{:screen}

### Token di identità
{: #identity-tokens notoc}

l token di identità contiene informazioni sull'utente, inclusi nome, e-mail, sesso, foto e posizione.

```
Intestazione: {

    "typ": "JOSE", // tipo di intestazione, in base alla specifica

    "alg": "RS256", // algoritmo, in base alla specifica

}
Payload: {

    "iss": "", // emittente, il server AppID che ha emesso il token. StringOrURL

    "sub": "", // soggetto, chi ha emesso questo token. AppID userid.

    "aud": "", // pubblico, a chi è destinato questo token. OAuth2 client_id.

    "exp: "", // data/ora di scadenza, ora di eliminazione

    "iat": "", // emesso nella data/ora, ora di eliminazione

    "tenant": "xxx", // AppID tenantId per cui è stato emesso il token

    "name": "John Smith", // il nome completo dell'utente come riportato da IDP, obbligatorio,

    "email": "js@mail.com", // l'email dell'utente come riportato da IDP, solo se disponibile,

    "gender", "male", // il sesso dell'utente come riportato da IDP, solo se disponibile,

    "locale": "en", // la locale dell'utente come riportato da IDP, solo se disponibile

    "picture": "https://url.to.photo", // URL alla foto dell'utente, solo se disponibile

    "auth_by": "appid_facebook/appid_google", // il nome del IDP utilizzato per l'autenticazione, obbligatorio

    "identities": [

        "provider: "appid_facebook/appid_google", // obbligatorio

        "id": "unique user id as reported by IDP", // obbligatorio

        "profile": { ... } // l'oggetto JSON restituito da IDP,  obbligatorio

      },

      {...}, {...} // ulteriori identità collegate

    ],

    "oauth_client":{

      "type": "serverapp/mobileapp from client registration", // obbligatorio

      "name": "client_name as reported during client registration", // obbligatorio

      "software_id": "software_id as reported during client registration", // obbligatorio

      "software_version": "software_version as reported during client registration", // obbligatorio

      "device_id": "device_id from client registration", //solo mobile

      "device_model": "device_model from client registration", //solo mobile

      "device_os": "device_os from client registration", //solo mobile

    }

}
```
{:screen}


## Panoramica sui provider di identità
{: #identity-providers-overview}

Puoi utilizzare i seguenti provider di identità nelle tue applicazioni mobili e web: 

* **Facebook** - I tuoi utenti accedono all'applicazione mobile o web con le loro credenziali Facebook.
* **Google** -  I tuoi utenti accedono all'applicazione mobile o web con le loro credenziali Google+.
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## Utilizzo della configurazione predefinita
{: #default-configuration}

{{site.data.keyword.appid_short_notm}} fornisce una configurazione predefinita quando configuri per la prima volta i tuoi provider di identità. Puoi utilizzare la configurazione predefinita solo nella modalità di sviluppo. Per ogni provider di identità, queste credenziali sono limitate a 100 utenti per istanza {{site.data.keyword.appid_short_notm}} al giorno. Prima di pubblicare la tua applicazione, aggiorna la configurazione predefinita con le tue proprie credenziali. Per aggiornare la tua configurazione, consulta [Configurazione dei provider di identità](/docs/services/appid/identity-providers.html). 
