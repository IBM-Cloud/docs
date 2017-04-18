---

copyright:
  year: 2016, 2017
lastupdated: "2017-03-15"

---

Der {{site.data.keyword.amafull}}-Service wird durch den {{site.data.keyword.appid_full}}-Service ersetzt.

# Facebook-Authentifizierung für Web-Apps aktivieren
{: #facebook_web}

Sie können Benutzer über Facebook für Ihre Web-App authentifizieren.

## Vorbereitungen
{: #facebook-auth-android-before}
Voraussetzungen:
* Web-App.  
* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung eines {{site.data.keyword.Bluemix_notm}}-Back-Ends finden Sie in der [Einführung](index.html).
* Facebook-Anwendungs-ID und geheimen Schlüssel der App. Weitere Informationen finden Sie in [Facebook-Anwendungs-ID vom Facebook-Entwicklerportal anfordern](https://console.{DomainName}/docs/services/mobileaccess/facebook-auth-overview.html#facebook-appID).


## Facebook-Anwendung für die Website konfigurieren
Zur Verwendung von Facebook als Identitätsprovider auf Ihrer Website müssen Sie die Website-Plattform Ihrer Facebook-Anwendung hinzufügen und sie konfigurieren.

1. Öffnen Sie Ihre Facebook-Anwendung im Facebook-Entwicklerportal (Facebook Developer Portal).
1. Notieren Sie die Anwendungs-ID für Ihre App und den geheimen Schlüssel der App. Sie benötigen diese Werte beim Konfigurieren Ihres Webprojekts für die Facebook-Authentifizierung.
1. Klicken Sie auf der Seite **Settings** auf **Add Platform** und wählen Sie die Option **Website** aus.
1. Speichern Sie die Änderungen.
1. Klicken Sie in der Seitenleiste auf **Facebook Login**.
1. Geben Sie den Callback-Endpunkt des Autorisierungsservers im Feld **Valid OAuth redirect URIs** ein: https://imf-newauthserver.bluemix.net/oauth/{bluemix_app_guid}/callback. Speichern Sie die Änderungen.




# {{site.data.keyword.amashort}} für die Facebook-Authentifizierung konfigurieren
Nachdem Sie über eine Facebook-Anwendungs-ID und den geheimen Schlüssel der App verfügen und Ihre Facebook-Anwendung zur Bedienung von Web-Clients konfiguriert haben, können Sie die Facebook-Authentifizierung im {{site.data.keyword.Bluemix_notm}}-Dashboard aktivieren.

1. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard.
1. Klicken Sie auf die Kachel für {{site.data.keyword.amashort}}. Das {{site.data.keyword.amashort}}-Dashboard wird geladen.
1. Klicken Sie auf die Kachel für Facebook.
1. Geben Sie die Facebook-Anwendungs-ID und den geheimen Schlüssel der App ein und speichern Sie die Eingaben.




## Mobile Client Access für Facebook-Webauthentifizierung verwenden

Gehen Sie wie folgt vor, um den Autorisierungsprozess zu starten:

1. Leiten Sie von Ihrer Web-App zum folgenden Endpunkt des Autorisierungsservers weiter: https://imf-newauthserver.bluemix.net/oauth/v2/authorization.

1. Fügen Sie die folgenden Abfrageparameter hinzu:
   ```
    response_type='authorization_code'
    client_id= <bluemix_app_guid>
    redirect_uri= <uri für Weiterleitung nach Empfang des Autorisierungscodes>
    scope= 'openid'
    state= <state>
    ```


  Der Parameter `state` ist momentan nicht im Gebrauch und kann leer gelassen werden.
  Der Parameter `redirect_uri` entspricht dem uri für die Weiterleitung nach erfolgreicher oder fehlgeschlagener Authentifizierung bei Facebook.

1. Nach der Weiterleitung zum Autorisierungsendpunkt wird ein Anmeldeformular von  
Facebook angezeigt. Geben Sie den Benutzernamen und das Kennwort für die Weiterleitung an den `redirect_uri` ein.
   Die nach der Weiterleitung zurückgegebene Antwort enthält den Autorisierungscode in den Abfrageparametern.

1. Senden Sie eine `POST`-Anforderung an den Token-Endpunkt des Autorisierungsservers:

  https://imf-newauthserver.bluemix.net/oauth/v2/token

  Verwenden Sie dabei die folgenden Abfrageparameter:
  ```
  grant_type='authorization_code'
  client_id= <bluemix_app_guid>
  code= <authorization code>
  ```
Der Parameter `redirect_uri` muss mit dem `redirect_uri` aus Schritt 2 übereinstimmen.
Der Wert `code` ist der in der Antwort am Ende von Schritt 3 empfangene Autorisierungscode.
Sie müssen diese `POST`-Anforderung innerhalb von 10 Minuten senden, da der Autorisierungscode maximal 10 Minuten gültig ist.

  Der Antwortteil von `POST` sollte das `access_token` und das `id_token` in Base64-Codierung enthalten.

## Authentifizierung testen
Nun können Sie mit dem Senden von Anforderungen an Ihre geschützten Ressourcen beginnen.
Alle Anforderungen an geschützte Ressourcen sollten das `access_token` im Headerfeld für die Autorisierungsanforderung enthalten.
