---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Informationen zu {{site.data.keyword.appid_short_notm}}
{: #about}

Entwickler können mit {{site.data.keyword.appid_full}} ihre {{site.data.keyword.Bluemix}} Apps sichern und eine Authentifizierung hinzufügen. Dazu sind nur wenige Code-Zeilen notwendig. Außerdem können benutzerspezifische Daten verwaltet werden, um personalisierte Apperfahrungen zu erstellen.
{:shortdesc}


Sie können den Service wie folgt nutzen:

* Hinzufügen einer Authentifizierung zu Ihren mobilen und Webanwendungen
* Gewährung von Zugriff auf geschützte Back-End-Ressourcen und Web-Apps
* Schutz von Node.js- und Swift-Anwendungen, die von {{site.data.keyword.Bluemix_notm}} gehostet werden
* Speichern von Benutzerdaten, wie App-Vorgaben oder Informationen aus öffentlichen sozialen Profilen
* Nutzung von gespeicherten Daten zum Erstellen personalisierter Apperfahrungen
* Schutz von Ressourcen sowohl für authentifizierte als auch anonyme Benutzer

**Hinweis**: Die implementierten Protokolle sind mit OpenID Connect (OIDC) vollständig kompatibel.


## Komponenten
{: #components}

* Dashboard - Sie können Onboarding-Beispiele herunterladen, Aktivitätenprotokolle anzeigen, verschiedene Authentifizierungstypen und Identitätsprovider konfigurieren.
* Client-SDK - Erstellen Sie mobile und Web-Apps, die mithilfe des Service eine Benutzerauthentifizierung implementieren.
    * Voraussetzungen für Android: API 25 oder höher, Java 8.x, Android SDK Tools 25.2.5 oder höher, Android SDK Platform Tools 25.0.3 oder höher, Android Build Tools Version 25.0.2
    * Voraussetzungen für iOS: iOS9 oder höher, MacOS 10.11.5, Xcode 8.2
* Server-SDK - Schützen Sie Ressourcen, die auf {{site.data.keyword.Bluemix_notm}} gehostet werden.
    * Unterstützte Laufzeiten sind Node.js und Swift.

## Architekturübersicht

![{{site.data.keyword.appid_short_notm}}-Architekturdiagramm](/images/appid_architecture.png)

Abbildung 1: {{site.data.keyword.appid_short_notm}} - Architekturdiagramm

Sie können Ihre Cloudressourcen mit dem {{site.data.keyword.appid_short_notm}}-Server-SDK schützen. Verwenden Sie die Anfrageklasse, die vom {{site.data.keyword.appid_short_notm}}-Client-SDK verwendet wird, um mit Ihren geschützten Cloudressourcen zu kommunizieren.

* Das Server-SDK erkennt eine nicht autorisierte Anforderung und gibt den Code HTTP 401 für die Berechtigungsanforderung (Challenge) zurück.
* Das Client-SDK erkennt die Berechtigungsanforderung (Challenge) mit dem Code HTTP 401 und startet automatisch den Authentifizierungsprozess anhand der Identitätsprovider-Konfiguration.
* Die Authentifizierung wird anhand der aktuellen konfigurieren Identitätsprovidern durchgeführt.
* Nach der erfolgreichen Authentifizierung gibt der Service die Autorisierungs- und Identitätstoken zurück.
* Das Client-SDK fügt das Berechtigungstoken automatisch der ursprünglichen Anforderung hinzu und sendet die Anforderung erneut an die Cloudressource.
* Das Server-SDK extrahiert das Zugriffstoken aus der Anforderung und validiert es mit {{site.data.keyword.appid_short_notm}}.
Zugriff wird gewährt und die Antwort wird an die Anwendung zurückgegeben.


## Anforderungsablauf
{: #request}

Das folgende Diagramm zeigt, wie eine Anforderung aus dem Client-SDK an Ihre Back-End-Anwendung und an Identitätsprovider geleitet wird.

![{{site.data.keyword.appid_short_notm}}-Anforderungsablauf](/images/appidflow.png)


* Verwenden Sie das {{site.data.keyword.appid_short_notm}}-Client-SDK zum Senden einer Anforderung an Ihre Back-End-Ressourcen, die mit dem {{site.data.keyword.appid_short_notm}}-Server-SDK geschützt werden.
* Das {{site.data.keyword.appid_short_notm}}-Server-SDK erkennt eine nicht autorisierte Anforderung und gibt einen HTTP 401- und Berechtigungsbereich zurück.
* Das Client-SDK erkennt HTTP 401 automatisch und startet den Authentifizierungsprozess.
* Wenn das Client-SDK Kontakt mit dem Service aufnimmt, gibt das Server-SDK das Anmeldewidget zurück, falls mehr als ein Identitätsprovider konfiguriert ist. {{site.data.keyword.appid_short_notm}} ruft den Identitätsprovider auf und präsentiert das Anmeldeformular für diesen Provider oder gibt einen Bewilligungscode zurück, mit dem die Authentifizierung ohne konfigurierte Identitätsprovider möglich ist.
* {{site.data.keyword.appid_short_notm}} fordert die Client-App auf, sich durch die Bereitstellung einer Authentifizierungsanforderung (Challenge) zu authentifizieren.
* Ist Facebook oder Google konfiguriert und meldet sich der Benutzer an, wird die Authentifizierung durch den jeweiligen Identitätsprovider-OAuth-Ablauf verarbeitet.
* Wenn die Authentifizierung mit demselben Bewilligungscode beendet wird, wird der Code an den Tokenendpunkt gesendet. Der Endpunkt gibt zwei Tokens zurück: ein Zugriffstoken und eine Identitätstoken. Von diesem Punkt an haben alle Anforderungen, die mit dem Client-SDK gesendet werden, einen neu abgerufenen Berechtigungsheader.
* Das Client-SDK wiederholt automatisch das Senden der ursprünglichen Anforderung, die den Berechtigungsablauf ausgelöst hat.
* Das Server-SDK extrahiert den Berechtigungsheader aus der Anforderung, validiert den Header mit dem Service und erteilt den Zugriff auf eine Back-End-Ressource.

## Zugriffs- und Identitätstoken
{: #access-and-identity}

{{site.data.keyword.appid_short}} verwendet zwei Typen von Token: Zugriffs- und Identitätstoken. Die Token sind als <a href="https://jwt.io/introduction/" target="_blank">JSON-Web-Token <img src="../../icons/launch-glyph.svg" alt="Symbol für externen Link"></a> formatiert.


### Zugriffstoken
{: #access-tokens notoc}

Das Zugriffstoken ermöglicht die Kommunikation mit Ressourcen, die von den {{site.data.keyword.appid_short_notm}}-Berechtigungsfiltern geschützt werden; weitere Informationen hierzu finden Sie im Abschnitt [Back-End-Ressourcen schützen](/docs/services/appid/protecting-resources.html).
Das Token entspricht den JavaScript Object Signing and Encryption (JOSE)-Spezifikationen und hat das folgende Format:

```
Header: {

    "typ": "JOSE", // Headertyp, je nach Spezifikation

    "alg": "RS256", // Algorithmus, je nach Spezifikation

}
Payload: {

    "iss": "", // Aussteller, der AppID-Server, der dieses Token ausgegeben hat. StringOrURL

    "sub": "", // Betreff, zu dem dieses Token ausgegeben wurde. Wahrscheinlich userId

    "aud": "", // Zielgruppe, für die dieses Token bestimmt ist. OAuth2 client_id.

    "exp: "", // Ablauf Zeitmarke, Epochenzeit

    "iat": "", // bei Zeitmarke ausgegeben, Epochenzeit

    "tenant": "xxx", tenantId der AppID, für die das Token ausgegeben wurde

    "auth_by": "appid_anon / appid_facebook / appid_google",

    "scope": "", // Umfang, für den das Token ausgegeben wurde

}
```
{:screen}

### Identitätstoken
{: #identity-tokens notoc}

Das Identitätstoken enthält Informationen über den Benutzer, einschließlich Name, E-Mail-Adresse, Geschlecht, Foto und Ort.

```
Header: {

    "typ": "JOSE", // Headertyp, je nach Spezifikation

    "alg": "RS256", // Algorithmus, je nach Spezifikation

}
Payload: {

    "iss": "", // Aussteller, der AppID-Server, der dieses Token ausgegeben hat. StringOrURL

    "sub": "", // Betreff, zu dem dieses Token ausgegeben wurde. userid der AppID.

    "aud": "", // Zielgruppe, für die dieses Token bestimmt ist. OAuth2 client_id.

    "exp: "", // Ablauf Zeitmarke, Epochenzeit

    "iat": "", // bei Zeitmarke ausgegeben, Epochenzeit

    "tenant": "xxx", // tenantId der AppID, für die das Token ausgegeben wurde

    "name": "John Smith", // vollständiger Benutzername wie von IDP bereitgestellt, obligatorisch,

    "email": "js@mail.com", // E-Mail-Adresse des Benutzers, wie von IDP bereitgestellt, wenn verfügbar,

    "gender", "male", // Geschlecht des Benutzers, wie von IDP bereitgestellt, wenn verfügbar,

    "locale": "en", // Ländereinstellung des Benutzers, wie von IDP bereitgestellt, wenn verfügbar

    "picture": "https://url.to.photo", // URL zum Benutzerfoto, wenn verfügbar

    "auth_by": "appid_facebook/appid_google", // Name des IDP, der für die Authentifizierung verwendet wird, obligatorisch

    "identities": [

        "provider: "appid_facebook/appid_google", // obligatorisch

        "id": "unique user id as reported by IDP", // obligatorisch

        "profile": { ... } // JSON-Objekt, das von IDP zurückgegeben wird, obligatorisch

      },

      {...}, {...} // weitere verknüpfte Identitäten

    ],

    "oauth_client":{

      "type": "serverapp/mobileapp from client registration", // obligatorisch

      "name": "client_name as reported during client registration", // obligatorisch

      "software_id": "software_id as reported during client registration", // obligatorisch

      "software_version": "software_version as reported during client registration", // obligatorisch

      "device_id": "device_id from client registration", //nur mobil

      "device_model": "device_model from client registration", //nur mobil

      "device_os": "device_os from client registration", //nur mobil

    }

}
```
{:screen}


## Überblick über Identitätsprovider
{: #identity-providers-overview}

Sie können in Ihren mobilen Anwendungen sowie in Ihren Webanwendungen folgende Identitätsprovider verwenden:

* **Facebook** - Ihre Benutzer melden sich bei der mobilen oder Web-App mit ihren Facebook-Berechtigungsnachweisen an.
* **Google** - Ihre Benutzer melden sich bei der mobilen oder Web-App mit ihren Google+-Berechtigungsnachweisen an.
<!--* **Custom** - Bring your own identity provider. The identity providers should be compliant with OIDC. -->

## Standardkonfiguration verwenden
{: #default-configuration}

{{site.data.keyword.appid_short_notm}} stellt eine Standardkonfiguration bereit, wenn Sie Ihre Identitätsprovider erstmalig einrichten. Die Standardkonfiguration können Sie nur im Entwicklungsmodus verwenden. Diese Berechtigungsnachweise sind pro Identitätsprovider auf 100 Benutzer pro {{site.data.keyword.appid_short_notm}}-Instanz und pro Tag beschränkt. Bevor Sie Ihre Anwendung veröffentlichen, aktualisieren Sie die Standardkonfiguration mit Ihren eigenen Berechtigungsnachweisen. Informationen zum Aktualisieren Ihrer Konfiguration finden Sie im Abschnitt [Identitätsprovider konfigurieren](/docs/services/appid/identity-providers.html).
