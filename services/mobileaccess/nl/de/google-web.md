---

copyright:
  year: 2016, 2017
lastupdated: "2017-01-08"

---

# Google-Authentifizierung für Web-Apps aktivieren
{: #google-auth-web}

Sie können Benutzer über die Google-Anmeldung für Ihre Web-App authentifizieren.


## Vorbereitungen
{: #before-you-begin}

Voraussetzungen:
* Web-App.
* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung eines {{site.data.keyword.Bluemix_notm}}-Back-Ends finden Sie in der [Einführung](index.html).

## Google-Anwendung für die Website konfigurieren
Erstellen Sie zur Verwendung von Google als Identitätsprovider ein Projekt in [Google Developer Console](https://console.developers.google.com). Zum Erstellen eines Projekts gehört das Anfordern einer Google-Client-ID und eines geheimen Schlüssels. Die Google-Client-ID und der geheime Schlüssel sind die eindeutigen Kennungen für Ihre Anwendung, die von der Google-Authentifizierung verwendet werden und zum Einrichten der {{site.data.keyword.Bluemix_notm}}-Anwendung erforderlich sind.

1. Erstellen Sie ein Projekt mithilfe der Google+-API.
1. Erstellen Sie unter Verwendung von **OAuth** Berechtigungsnachweise. Zum Erstellen der Berechtigungsnachweise müssen Sie folgende Schritte ausführen:
    * Anwendungstyp **Webanwendung** auswählen.
    * Wert für die autorisierten redirect-URIs (Authorized redirect URIs) angeben:

     https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback
1. Beenden Sie die Erstellung der Berechtigungsnachweise und notieren Sie die Google-Client-ID und den geheimen Schlüssel.


## {{site.data.keyword.amashort}} für die Google-Authentifizierung konfigurieren
Wenn Sie eine Google-Anwendungs-ID und einen geheimen Schlüssel besitzen, können Sie die Google-Authentifizierung im {{site.data.keyword.amashort}}-Dashboard aktivieren.

1. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard.
1. Klicken Sie auf die Kachel für {{site.data.keyword.amashort}}. Das {{site.data.keyword.amashort}}-Dashboard wird geladen.
1. Klicken Sie auf die Kachel für Google.
1. Geben Sie die Google-Client-ID und den geheimen Schlüssel ein und speichern Sie die Eingaben.


## {{site.data.keyword.amashort}} für Google-Webauthentifizierung verwenden
Gehen Sie wie folgt vor, um den Autorisierungsprozess zu starten:

1. Leiten Sie von Ihrer Web-App zum folgenden Endpunkt des Autorisierungsservers weiter:  
  https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  Verwenden Sie dabei die folgenden Abfrageparameter:
	```
   response_type='authorization_code'
   client_id= <bluemix_app_guid>
   redirect_uri= <uri, zu dem nach Abrufen eines Autorisierungscodes zurückgekehrt werden soll>
   scope= ‘openid’
   state= <state>
	```

  Der Parameter `state` ist momentan nicht im Gebrauch und kann leer gelassen werden.

  Der Parameter `redirect_uri` entspricht dem uri für die Weiterleitung nach erfolgreicher oder fehlgeschlagener Authentifizierung bei Google.
  Die nach der Weiterleitung zurückgegebene Antwort enthält den Autorisierungscode in den Abfrageparametern.
1. Senden Sie eine `POST`-Anforderung an den Token-Endpunkt des Autorisierungsservers:

 https://imf-newauthserver.bluemix.net/oauth/v2/token


  Verwenden Sie dabei die folgenden Abfrageparameter:

	```
  	grant_type=’authorization_code’
    client_id= < bluemix_app_guid >
    redirect_uri= <redirect_uri >
    code= <authorization code>
	```
  Der Parameter `redirect_uri` muss mit dem `redirect_uri` aus Schritt 1 übereinstimmen und der Wert für `<authorization code>` wird von der Antwort empfangen.
  Sie müssen diese `POST`-Anforderung innerhalb von 10 Minuten senden, da der Autorisierungscode maximal 10 Minuten gültig ist.

Der Antwortteil von `POST` sollte das `access_token` und das `id_token` in Base64-Codierung enthalten.

## Authentifizierung testen

Nun können Sie mit dem Senden von Anforderungen an Ihre geschützten Ressourcen beginnen.
Alle Anforderungen an geschützte Ressourcen sollten das Zugriffstoken im Headerfeld für die Autorisierungsanforderung enthalten.
