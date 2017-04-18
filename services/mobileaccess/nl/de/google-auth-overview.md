---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-04-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

**Wichtig: Der Service {{site.data.keyword.amafull}} wird durch den Service {{site.data.keyword.appid_full}} ersetzt.**


# Benutzer mit Google-Berechtigungsnachweisen authentifizieren
{: #google-auth}

Sie können den {{site.data.keyword.amafull}}-Service zum Schutz von Ressourcen konfigurieren und Google als Identitätsprovider verwenden. Die Benutzer Ihrer mobilen Anwendung oder Ihrer Webanwendung können dann ihre Google-Berechtigungsnachweise für die Authentifizierung nutzen.
{:shortdesc}

**Wichtig:** Sie müssen das von Google bereitgestellte Client-SDK nicht separat installieren. Das Google-SDK wird automatisch durch Abhängigkeitenmanager installiert, wenn Sie das {{site.data.keyword.amashort}}-Client-SDK konfigurieren.

## {{site.data.keyword.amashort}}-Anforderungsablauf
{: #google-auth-overview}

### Anforderungsablauf für Client

Im folgenden Diagramm wird die Integration von {{site.data.keyword.amashort}} in Google für die Authentifizierung veranschaulicht.

![Anforderungsablaufdiagramm für Client](images/mca-sequence-google.jpg)

* Verwenden Sie das {{site.data.keyword.amashort}}-SDK zum Senden einer Anforderung an ihre Back-End-Ressourcen, die mit dem {{site.data.keyword.amashort}}-Server-SDK geschützt werden.
* Das {{site.data.keyword.amashort}}-Server-SDK erkennt die nicht autorisierte Anforderung und gibt den Code HTTP 401 sowie den Berechtigungsbereich zurück.
* Das {{site.data.keyword.amashort}}-Client-SDK erkennt den Code HTTP 401 automatisch und startet den Authentifizierungsprozess.
* Das {{site.data.keyword.amashort}}-Client-SDK kontaktiert den {{site.data.keyword.amashort}}-Service und fordert einen Berechtigungsheader an.
* Der {{site.data.keyword.amashort}}-Service fordert den Client auf, sich zuerst bei Google durch die Bereitstellung einer Authentifizierungsanforderung (Challenge) zu authentifizieren.
* Das {{site.data.keyword.amashort}}-Client-SDK verwendet das Google-SDK, um den Authentifizierungsprozess zu starten. Nach einer erfolgreichen Authentifizierung gibt das Google-SDK ein Google-Zugriffstoken zurück.
* Das Google-Zugriffstoken wird als Antwort auf die Authentifizierungsanforderung (Challenge) betrachtet. Das Token wird an den {{site.data.keyword.amashort}}-Service gesendet.
* Der Service validiert die Antwort auf die Authentifizierungsanforderung mit Google-Servern.
* Wenn die Validierung erfolgreich ist, generiert der {{site.data.keyword.amashort}}-Service einen Berechtigungsheader und gibt diesen an das {{site.data.keyword.amashort}}-Client-SDK zurück. Der Berechtigungsheader enthält zwei Tokens: ein Zugriffstoken, das Informationen zu Zugriffsberechtigungen enthält, und ein ID-Token, das Informationen zum aktuellen Benutzer, zum Gerät und zur Anwendung enthält.
* Von diesem Punkt an haben alle Anforderungen, die durch das {{site.data.keyword.amashort}}-Client-SDK gesendet werden, einen neu abgerufenen Berechtigungsheader.
* Das {{site.data.keyword.amashort}}-Client-SDK wiederholt automatisch das Senden der ursprünglichen Anforderung, die den Berechtigungsablauf ausgelöst hat.
* Das {{site.data.keyword.amashort}}-Server-SDK extrahiert den Berechtigungsheader aus der Anforderung, validiert ihn mit dem {{site.data.keyword.amashort}}-Service und erteilt den Zugriff auf eine Back-End-Ressource.


### Anforderungsablauf für Mobile Client Access-Webanwendung
{: #mca-google-web-sequence}
Der {{site.data.keyword.amashort}}-Anforderungsablauf für eine Webanwendung ist vergleichbar mit dem Ablauf für einen mobilen Client. {{site.data.keyword.amashort}} schützt jedoch die Webanwendung anstatt einer {{site.data.keyword.Bluemix_notm}}-Back-End-Ressource.

  * Die ursprüngliche Anforderung wird von der Webanwendung (zum Beispiel von einem Anmeldeformular) gesendet.
  * Die letzte Weiterleitung erfolgt an den geschützten Bereich der Webanwendung selbst anstatt an die geschützte Back-End-Ressource.



## Nächste Schritte
{: #google-auth-nextsteps}

* [Google-Authentifizierung für Android-Apps aktivieren](google-auth-android.html)
* [Google-Authentifizierung für iOS-Apps aktivieren (Swift-SDK)](google-auth-ios-swift-sdk.html)
* [Google-Authentifizierung für Cordova-Apps aktivieren](google-auth-cordova.html)
