---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Back-End-Ressourcen schützen
{: #protecting-resources}

Das {{site.data.keyword.appid_short}}-Server-SDK bietet Strategien zum Schutz von zwei Arten von Ressourcen an: APIs und Webanwendungen.
{:shortdesc}


## Auf geschützte Ressourcen von Client-SDKs zugreifen
{: #accessing}

Beim Aufrufen einer geschützten Ressource wird ggf. das Anmelde-Widget gestartet. Wenn bereits ein gültiges Token angefordert wurde, wird das Anmelde-Widget nicht gestartet. Auf die Ressource kann dann direkt zugegriffen werden.


### Das Swift-SDK verwenden
{: #requesting-swift notoc}

1. Importieren Sie BMSCore.

  ```swift
  import BMSCore
  ```
  {:pre}

2. Rufen Sie eine Anforderung für die geschützte Ressource auf.

  ```swift
  BMSClient.sharedInstance.initialize(bluemixRegion: AppID.<region>)
  BMSClient.sharedInstance.authorizationManager = AppIDAuthorizationManager(appid:AppID.sharedInstance)
  var request:Request =  Request(url: "<your protected resource url>")
  request.send(completionHandler: {(response:Response?, error:Error?) in
      //Code-Handling der Antwort hier
  })
  ```
  {:pre}


### Das Android-SDK verwenden
{: #requesting-android notoc}

1. Rufen Sie eine Anforderung für die geschützte Ressource auf.

  ```java
  BMSClient bmsClient = BMSClient.getInstance();
  bmsClient.initialize(getApplicationContext(), AppID.REGION_UK);

  AppIDAuthorizationManager appIdAuthMgr = new AppIDAuthorizationManager(AppID.getInstance())
  bmsClient.setAuthorizationManager(appIdAuthMgr);

  Request request = new Request("<your protected resource url>", Request.GET);
  request.send(this, new ResponseListener() {
  @Override
	public void onSuccess (Response response) {
     //Code-Handling der Antwort hier
  }
  @Override
	public void onFailure (Response response, Throwable t, JSONObject extendedInfo) {
      //Code-Handling des Fehlers hier
  });
  ```
  {:pre}



## Berechtigungsfilter
{: #auth-filter}

Die API-Schutzstrategie gibt eine HTTP 401-Antwort mit einer Liste von Geltungsbereichen zurück, um die Autorisierung für einen nicht authentifizierten Client anzufordern. Die Schutzstrategie der Webanwendung gibt eine HTTP 302-Umleitung zurück. Die Umleitung sendet je nach Konfiguration einen nicht authentifizierten Client zur Anmeldeseite, die vom {{site.data.keyword.appid_short_notm}}-Service gehostet wird, oder direkt zur Anmeldeseite des Identitätsproviders.



### API-Strategie
{: #api notoc}

Die API-Strategie erwartet Anforderungen, die einen Autorisierungsheader mit einem gültigen Zugriffstoken enthalten. Die Antwort kann auch ein Identitätstoken enthalten; siehe [Zugriffs- und Identitätstoken](/docs/services/appid/about.html#acess-and-identity).

Wenn ein Token ungültig oder abgelaufen ist, gibt die API-Strategie einen HTTP 401-Fehler zurück, der die folgende Information enthält: Www-Authenticate=Bearer scope="{scope}" error="{error}". Die `error`-Komponente ist optional.

Wenn die Anforderung ein gültiges Token zurückgibt, wird die Steuerung an die nächste Middleware übergeben und die Eigenschaft `appIdAuthorizationContext` wird in das Anforderungsobjekt eingefügt. Diese Eigenschaft enthält die ursprünglichen Zugriffs- und Identitätstoken sowie die decodierten Nutzdaten als einfache JSON-Objekte.


### Web-App-Strategie
{: #web notoc}

Wenn die Web-App-Strategieklasse nicht authentifizierte Versuche, auf geschützte Ressourcen zuzugreifen, aufdeckt, wird der Benutzerbrowser zur Authentifizierungsseite automatisch umgeleitet. Nach der erfolgreichen Authentifizierung kehrt der Benutzer zur Callback-URL der Webanwendung zurück. Der Service nutzt die Web-App-Strategieklasse, um die Zugriffs- und Identitätstoken anzufordern. Nach Erhalt dieser Token werden diese von der Web-App-Strategieklasse in einer HTTP-Sitzung unter `WebAppStrategy.AUTH_CONTEXT` gespeichert. Der Benutzer kann entscheiden, ob die Zugriffs- und Identitätstoken in der Anwendungsdatenbank gespeichert werden sollen.

## Berechtigungsheader
{: #auth-header}

Der Berechtigungsheader in der eingehenden Anforderung besteht aus drei Teilen, die durch Leerzeichen voneinander getrennt sind: Träger (Bearer), Zugriffstoken und ID-Token. Das Zugriffstoken ist eine verbindliche Komponente, während das ID-Token optional ist. Die erwartete Headerstruktur ist: Authorization=Bearer {access_token} [{id_token}]
