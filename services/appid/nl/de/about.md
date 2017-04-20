---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}


# Funktionsweise
{: #about}

Sie können Informationen zu den von {{site.data.keyword.appid_short_notm}} verwendeten Komponenten, zur Architektur und zum Anforderungsablauf abrufen.
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
{: #architecture}

Mit {{site.data.keyword.appid_short_notm}} können Sie eine zusätzliche Sicherheitsstufe in Ihren Anwendungen implementieren, indem Sie es erforderlich machen, dass die Benutzer eine Anmeldung durchführen. Darüber hinaus können Sie das Server-SDK verwenden, um Ihre Back-End-Ressourcen zu schützen. 

Im folgenden Diagramm ist eine Übersicht der Funktionsweise des {{site.data.keyword.appid_short_notm}}-Service dargestellt. 

![{{site.data.keyword.appid_short_notm}}-Architekturdiagramm](/images/appid_architecture2.png)

Abbildung 1: {{site.data.keyword.appid_short_notm}} - Architekturdiagramm

<dl>
  <dt> Client-SDK</dt>
    <dd> Das Client-SDK stellt eine Anfrageklasse für die Kommunikation mit den Cloudressourcen bereit. Das Client-SDK startet den Authentifizierungsprozess automatisch, wenn es eine Berechtigungsanforderung (Challenge) feststellt. </dd>
  <dt> Bluemix</dt>
    <dd>  Das Server-SDK extrahiert das Zugriffstoken aus der Anforderung und validiert es mit {{site.data.keyword.appid_short_notm}}.
Nach der erfolgreichen Authentifizierung gibt {{site.data.keyword.appid_short_notm}} Berechtigungs- und Identitätstoken an die Anwendung zurück. </dd>
  <dt> Identitätsprovider</dt>
    <dd> Sie können Facebook, Google oder beide für die Authentifizierung Ihrer Apps konfigurieren. </dd>
</dl>


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
