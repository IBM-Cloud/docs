---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Token di identità e accesso
{: #access-and-identity}

{{site.data.keyword.appid_short}} utilizza due tipi di token: accesso e identità. I token sono creati come <a href="https://jwt.io/introduction/" target="_blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>.
{:shortdesc}


## Token di accesso
{: #access-tokens}

Il token di accesso abilita la comunicazione con le [risorse di back-end](/docs/services/appid/protecting-resources.html) protette dai filtri di autorizzazione {{site.data.keyword.appid_short_notm}}. Il token è conforme alle specifiche JavaScript Object Signing and Encryption (JOSE) ed ha il seguente formato: 

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

## Token di identità
{: #identity-tokens}

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
