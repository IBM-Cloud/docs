---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Berechtigungsfilter und -header
{: #auth}

Das {{site.data.keyword.appid_short}}-Server-SDK bietet Strategien zum Schutz von zwei Arten von Ressourcen an: APIs und Webanwendungen.
{:shortdesc}


## Berechtigungsfilter
{: #auth-filter}

Die API-Schutzstrategie gibt eine HTTP 401-Antwort mit einer Liste von Geltungsbereichen zurück, um die Autorisierung für einen nicht authentifizierten Client anzufordern. Die Schutzstrategie der Webanwendung gibt eine HTTP 302-Umleitung zurück. Die Umleitung sendet je nach Konfiguration einen nicht authentifizierten Client zur Anmeldeseite, die vom {{site.data.keyword.appid_short_notm}}-Service gehostet wird, oder direkt zur Anmeldeseite des Identitätsproviders.



### API-Strategie
{: #api}

Die API-Strategie erwartet Anforderungen, die einen Autorisierungsheader mit einem gültigen Zugriffstoken enthalten. Die Antwort kann auch ein Identitätstoken enthalten; siehe [Zugriffs- und Identitätstoken](/docs/services/appid/access-identity.html#access-and-identity).

Wenn ein Token ungültig oder abgelaufen ist, gibt die API-Strategie einen HTTP 401-Fehler zurück, der die folgende Information enthält: Www-Authenticate=Bearer scope="{scope}" error="{error}". Die `error`-Komponente ist optional.

Wenn die Anforderung ein gültiges Token zurückgibt, wird die Steuerung an die nächste Middleware übergeben und die Eigenschaft `appIdAuthorizationContext` wird in das Anforderungsobjekt eingefügt. Diese Eigenschaft enthält die ursprünglichen Zugriffs- und Identitätstoken sowie die decodierten Nutzdaten als einfache JSON-Objekte.


### Web-App-Strategie
{: #web}

Wenn die Web-App-Strategieklasse nicht authentifizierte Versuche, auf geschützte Ressourcen zuzugreifen, aufdeckt, wird der Benutzerbrowser zur Authentifizierungsseite automatisch umgeleitet. Nach der erfolgreichen Authentifizierung kehrt der Benutzer zur Callback-URL der Webanwendung zurück. Der Service nutzt die Web-App-Strategieklasse, um die Zugriffs- und Identitätstoken anzufordern. Nach Erhalt dieser Token werden diese von der Web-App-Strategieklasse in einer HTTP-Sitzung unter `WebAppStrategy.AUTH_CONTEXT` gespeichert. Der Benutzer kann entscheiden, ob die Zugriffs- und Identitätstoken in der Anwendungsdatenbank gespeichert werden sollen.

## Berechtigungsheader
{: #auth-header}

Der Berechtigungsheader in der eingehenden Anforderung besteht aus drei Teilen, die durch Leerzeichen voneinander getrennt sind: Träger (Bearer), Zugriffstoken und ID-Token. Das Zugriffstoken ist eine verbindliche Komponente, während das ID-Token optional ist. Die erwartete Headerstruktur ist: Authorization=Bearer {access_token} [{id_token}]
