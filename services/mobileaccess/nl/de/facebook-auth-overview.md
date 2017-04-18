---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}

Der {{site.data.keyword.amafull}}-Service wird durch den {{site.data.keyword.appid_full}}-Service ersetzt.

# Benutzer mit Facebook-Berechtigungsnachweisen authentifizieren
{: #facebook-auth-overview}

Sie können den {{site.data.keyword.amafull}}-Service zum Schützen von Ressourcen durch die Verwendung von Facebook als Identitätsprovider konfigurieren. Die Benutzer Ihrer mobilen Anwendung oder Ihrer Webanwendung können ihre Facebook-Berechtigungsnachweise für die Authentifizierung nutzen.

{:shortdesc}

**Wichtig:** Sie müssen das von Facebook bereitgestellte Client-SDK nicht separat installieren. Das Facebook-SDK wird automatisch durch Abhängigkeitenmanager installiert, wenn Sie das {{site.data.keyword.amashort}}-Facebook-Client-SDK konfigurieren.

## {{site.data.keyword.amashort}}-Anforderungsablauf
{: #mca-facebook-sequence}

### Anforderungsablauf für mobilen Client

Im folgenden Diagramm wird die Integration von {{site.data.keyword.amashort}} in Facebook für die Authentifizierung über eine App eines mobilen Clients veranschaulicht.

![Anforderungsablaufdiagramm für mobilen Client](images/mca-sequence-facebook.jpg)

* Verwenden Sie das {{site.data.keyword.amashort}}-Client-SDK zum Senden einer Anforderung an Ihre Back-End-Ressourcen, die mit dem {{site.data.keyword.amashort}}-Server-SDK geschützt werden.
* Das {{site.data.keyword.amashort}}-Server-SDK erkennt eine nicht autorisierte Anforderung und gibt den Code HTTP 401 sowie den Berechtigungsbereich zurück.
* Das {{site.data.keyword.amashort}}-Client-SDK erkennt den Code HTTP 401 automatisch und startet den Authentifizierungsprozess.
* Das {{site.data.keyword.amashort}}-Client-SDK kontaktiert den {{site.data.keyword.amashort}}-Service und fordert einen Berechtigungsheader an.
* Der {{site.data.keyword.amashort}}-Service fordert den Client auf, sich zuerst bei Facebook durch die Bereitstellung einer Authentifizierungsanforderung (Challenge) zu authentifizieren.
* Das {{site.data.keyword.amashort}}-Client-SDK verwendet das Facebook-SDK, um den Authentifizierungsprozess zu starten. Nach einer erfolgreichen Authentifizierung gibt das Facebook-SDK ein Facebook-Zugriffstoken zurück.
* Das Facebook-Zugriffstoken wird als Antwort auf die Authentifizierungsanforderung (Challenge) betrachtet. Das Token wird an den {{site.data.keyword.amashort}}-Service gesendet.
* Der Service validiert die Antwort auf die Authentifizierungsanforderung mit Facebook-Servern.
* Wenn die Validierung erfolgreich ist, generiert der {{site.data.keyword.amashort}}-Service einen Berechtigungsheader und gibt diesen an das {{site.data.keyword.amashort}}-Client-SDK zurück. Der Berechtigungsheader enthält zwei Tokens: ein Zugriffstoken, das Informationen zu Zugriffsberechtigungen enthält, und ein ID-Token, das Informationen zum aktuellen Benutzer, zum Gerät und zur Anwendung enthält.
* Von diesem Punkt an haben alle Anforderungen, die durch das {{site.data.keyword.amashort}}-Client-SDK gesendet werden, einen neu abgerufenen Berechtigungsheader.
* Das {{site.data.keyword.amashort}}-Client-SDK wiederholt automatisch das Senden der ursprünglichen Anforderung, die den Berechtigungsablauf ausgelöst hat.
* Das {{site.data.keyword.amashort}}-Server-SDK extrahiert den Berechtigungsheader aus der Anforderung, validiert ihn mit dem {{site.data.keyword.amashort}}-Service und erteilt den Zugriff auf eine Back-End-Ressource.

### {{site.data.keyword.amashort}}-Anforderungsablauf für Webanwendung
{: #mca-facebook-web-sequence}

Der {{site.data.keyword.amashort}}-Anforderungsablauf für eine Webanwendung ist vergleichbar mit dem Ablauf für einen mobilen Client. {{site.data.keyword.amashort}} schützt jedoch die Webanwendung anstatt einer {{site.data.keyword.Bluemix_notm}}-Back-End-Ressource.

  * Die ursprüngliche Anforderung wird von der Webanwendung (zum Beispiel von einem Anmeldeformular) gesendet.
  * Die letzte Weiterleitung erfolgt an den geschützten Bereich der Webanwendung selbst anstatt an die geschützte Back-End-Ressource.


## Anwendung auf der Site 'Facebook for Developers' erstellen
{: #facebook-appID}

Zur Verwendung von Facebook als Identitätsprovider müssen Sie eine Anwendung auf der Site 'Facebook for Developers' erstellen. Während dieses Vorgangs wird eine Facebook-App-ID erstellt. Dabei handelt es sich um eine eindeutige ID, die von Facebook verwendet wird, um zu erkennen, welche Anwendung versucht, eine Verbindung herzustellen.

Diesen Wert benötigen Sie, um die Facebook-Authentifizierung für Ihre mobile App oder Web-App zu konfigurieren.

1. Rufen Sie die [Facebook for Developers-Website ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://developers.facebook.com){: new_window} auf.

1. Öffnen Sie die Pulldown-Liste **Meine Apps** und wählen Sie **Neue App hinzufügen** aus.

1. Geben Sie die Werte für **Anzeigename** und die E-Mail-Adresse der Kontaktperson ein und wählen Sie aus der Pulldown-Liste eine **Kategorie** aus.

1. Klicken Sie auf **Neue App-ID erstellen**.

1. Unter Umständen wird eine Sicherheitsprüfung angezeigt. Führen Sie die angeforderte Aktion durch.

1. Die Seite **Produktkonfiguration** wird angezeigt. Kopieren Sie den angezeigten Wert für **App ID**.

## Nächste Schritte
{: #next-steps}

* [Facebook-Authentifizierung für Android-Apps aktivieren](facebook-auth-android.html)
* [Facebook-Authentifizierung für iOS-Apps aktivieren (Swift-SDK)](facebook-auth-ios-swift-sdk.html)
* [Facebook-Authentifizierung für Cordova-Apps aktivieren](facebook-auth-cordova.html)
