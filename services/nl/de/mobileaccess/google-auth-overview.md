---

copyright:
  years: 2015, 2016

---
{:screen:  .screen}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}

# Benutzer mit Google-Berechtigungsnachweisen authentifizieren
{: #google-auth}

*Letzte Aktualisierung: 15. Juni 2016*

Sie können den {{site.data.keyword.amashort}}-Service zum Schutz von Ressourcen konfigurieren und Google als Identitätsprovider verwenden. Die Benutzer Ihrer mobilen Anwendung können dann ihre Google-Berechtigungsnachweise für die Authentifizierung nutzen.
{:shortdesc}

**Wichtig:** Sie müssen das Google-SDK nicht separat installieren. Das Google-SDK wird automatisch durch Abhängigkeitenmanager installiert, wenn Sie das {{site.data.keyword.amashort}}-Client-SDK konfigurieren.

## {{site.data.keyword.amashort}}-Ablauf
{: #google-auth-overview}

Im folgenden vereinfachten Diagramm wird die Integration von {{site.data.keyword.amashort}} in Google für die Authentifizierung veranschaulicht.

![Bild](images/mca-sequence-google.jpg)

1. Verwenden Sie das {{site.data.keyword.amashort}}-SDK zum Senden einer Anforderung an ihre Back-End-Ressourcen, die mit dem {{site.data.keyword.amashort}}-Server-SDK geschützt werden.
* Das {{site.data.keyword.amashort}}-Server-SDK erkennt die nicht autorisierte Anforderung und gibt den Code HTTP 401 sowie den Berechtigungsbereich zurück.
* Das {{site.data.keyword.amashort}}-Client-SDK erkennt den Code HTTP 401 automatisch und startet den Authentifizierungsprozess.
* Das {{site.data.keyword.amashort}}-Client-SDK kontaktiert den {{site.data.keyword.amashort}}-Service und fordert die Ausgabe eines Berechtigungsheaders an.
* Der {{site.data.keyword.amashort}}-Service fordert den Client auf, sich zuerst bei Google durch die Bereitstellung einer Authentifizierungsanforderung (Challenge) zu authentifizieren.
* Das {{site.data.keyword.amashort}}-Client-SDK verwendet das Google-SDK, um den Authentifizierungsprozess zu starten. Nach einer erfolgreichen Authentifizierung gibt das Google-SDK ein Google-Zugriffstoken zurück.
* Das Google-Zugriffstoken wird als Antwort auf die Authentifizierungsanforderung (Challenge) betrachtet. Das Token wird an den {{site.data.keyword.amashort}}-Service gesendet.
* Der Service validiert die Antwort auf die Authentifizierungsanforderung mit Google-Servern.
* Wenn die Validierung erfolgreich ist, generiert der {{site.data.keyword.amashort}}-Service einen Berechtigungsheader und gibt diesen an das {{site.data.keyword.amashort}}-Client-SDK zurück. Der Berechtigungsheader enthält zwei Tokens: ein Zugriffstoken, das Informationen zu Zugriffsberechtigungen enthält, und ein ID-Token, das Informationen zum aktuellen Benutzer, zum Gerät und zur Anwendung enthält.
* Von diesem Punkt an haben alle Anforderungen, die durch das {{site.data.keyword.amashort}}-Client-SDK gesendet werden, einen neu abgerufenen Berechtigungsheader.
* Das {{site.data.keyword.amashort}}-Client-SDK wiederholt automatisch das Senden der ursprünglichen Anforderung, die den Berechtigungsablauf ausgelöst hat.
* Das {{site.data.keyword.amashort}}-Server-SDK extrahiert den Berechtigungsheader aus der Anforderung, validiert ihn mit dem {{site.data.keyword.amashort}}-Service und erteilt den Zugriff auf eine Back-End-Ressource.



## Nächste Schritte
{: #google-auth-nextsteps}

* [Google-Authentifizierung für Android-Apps aktivieren](google-auth-android.html)
* [Google-Authentifizierung für iOS-Apps aktivieren (Swift-SDK)](google-auth-ios-swift-sdk.html)
* [Google-Authentifizierung für iOS-Apps aktivieren (Objective-C-SDK)](google-auth-ios.html)
* [Google-Authentifizierung für Cordova-Apps aktivieren](google-auth-cordova.html)

