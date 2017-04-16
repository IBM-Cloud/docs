---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-08"

---

# {{site.data.keyword.amashort}} für eine angepasste Authentifizierung konfigurieren
{: #custom-dash}


Zur Verwendung einer angepassten Authentifizierung mit Ihrer mobilen App müssen Sie den Realm einer angepassten Authentifizierung und die Basis-URL Ihres angepassten Identitätsproviders im {{site.data.keyword.amashort}}-Service-Dashboard registrieren.

## Vorbereitungen
{: #custom-dash-begin}
Voraussetzungen:
* Eine Instanz eines {{site.data.keyword.amafull}}-Service.
* Eine Anwendung eines Identitätsproviders.

## Angepasste Authentifizierung im {{site.data.keyword.amafull}}-Dashboard konfigurieren
{: #custom-dash-config}
Verwenden Sie das {{site.data.keyword.amafull}}-Dashboard, um die angepasste Authentifizierung zu konfigurieren.

1. Öffnen Sie den Service im {{site.data.keyword.amafull}}-Dashboard.
1. Aktivieren Sie auf der Registerkarte **Verwalten** die Option **Berechtigung**.
1. Erweitern Sie den Abschnitt **Angepasst**.
1. Geben Sie den **Realname** und die **angepasste Identitätsprovider-URL** ein. Der Wert für **Weiterleitungs-URIs Ihrer Webanwendung** ist nur für Webanwendungen erforderlich.

## Nächste Schritte
{: #next-steps}
* [Angepasste Authentifizierung für Android konfigurieren](custom-auth-android.html)
* [Angepasste Authentifizierung für iOS konfigurieren](custom-auth-ios-swift-sdk.html)
* [Angepasste Authentifizierung für Cordova konfigurieren](custom-auth-cordova.html)
