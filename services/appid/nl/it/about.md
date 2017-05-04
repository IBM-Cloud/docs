---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Come funziona
{: #about}

Puoi imparare ulteriori informazioni sui componenti, l'architettura e il flusso della richiesta che {{site.data.keyword.appid_short_notm}} utilizza.
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
{: #architecture}

Con {{site.data.keyword.appid_short_notm}} puoi aggiungere un livello di sicurezza alle tue applicazioni richiedendo agli utenti di accedere. Puoi anche utilizzare l'SDK server per proteggere le tue risorse di backend.

Il seguente diagramma mostra una panoramica su come il servizio {{site.data.keyword.appid_short_notm}} funziona.

![Diagramma architettura {{site.data.keyword.appid_short_notm}}](/images/appid_architecture2.png)

Figura 1. Diagramma architettura {{site.data.keyword.appid_short_notm}}

<dl>
  <dt> SDK client </dt>
    <dd> L'SDK client fornisce una classe di richiesta per comunicare con le tue risorse cloud. L'SDK client avvia automaticamente il processo di autenticazione quando individua una verifica dell'autorizzazione. </dd>
  <dt> Bluemix </dt>
    <dd>  L'SDK server estrae il token di accesso dalla richiesta e lo convalida con {{site.data.keyword.appid_short_notm}}. Dopo una corretta autenticazione, {{site.data.keyword.appid_short_notm}} restituisce i token di identità e autorizzazione alla tua applicazione. </dd>
  <dt> Provider di identità </dt>
    <dd> Puoi configurare Facebook, Google o entrambi per autenticare le tue applicazioni. </dd>
</dl>


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
