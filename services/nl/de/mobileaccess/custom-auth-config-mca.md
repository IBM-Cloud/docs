---

copyright:
  years: 2015, 2016
  
---

# {{site.data.keyword.amashort}} für eine angepasste Authentifizierung konfigurieren
{: #custom-dash}
Zur Verwendung einer angepassten Authentifizierung mit Ihrer mobilen App müssen Sie den Realm einer angepassten Authentifizierung und die Basis-URL Ihres angepassten Identitätsproviders im {{site.data.keyword.amashort}}-Service-Dashboard registrieren.

## Vorbereitungen
{: #custom-dash-begin}
* Lesen Sie die Informationen in [Einführung](getting-started.html).
* Schützen Sie Ihre Back-End-Anwendung mit dem {{site.data.keyword.amashort}}-Server-SDK.  Weitere Informationen finden Sie in [Ressourcen schützen](protecting-resources.html).
* Führen Sie eine aktive Anwendung eines Identitätsproviders aus.

## Angepasste Authentifizierung im {{site.data.keyword.Bluemix}}-Dashboard konfigurieren
{: #custom-dash-config}
Verwenden Sie das {{site.data.keyword.amashort}}-Dashboard, um die angepasste Authentifizierung zu konfigurieren.

1. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix}}-Dashboard.

1. Klicken Sie auf **Mobile Systemerweiterungen** und notieren Sie die Werte für **Route** (`applicationRoute`) und **App-GUID** (`applicationGUID`). Sie benötigen diese Werte, wenn Sie das SDK initialisieren.

1. Klicken Sie auf die Kachel für {{site.data.keyword.amashort}}. Das {{site.data.keyword.amashort}}-Dashboard wird geladen.

1. Klicken Sie auf die Kachel **Angepasst**.

1. Geben Sie den **Realmnamen** und die **Basis-URL** für Ihren angepassten Identitätsprovider ein und speichern Sie die Änderungen.

## Nächste Schritte
{: #next-steps}
* [Angepasste Authentifizierung für Android konfigurieren](custom-auth-android.html)
* [Angepasste Authentifizierung für iOS konfigurieren](custom-auth-ios.html)
* [Angepasste Authentifizierung für Cordova konfigurieren](custom-auth-cordova.html)
