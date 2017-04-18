---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

Der {{site.data.keyword.amafull}}-Service wird durch den {{site.data.keyword.appid_full}}-Service ersetzt.

# Angepasste Authentifizierung für Web-App
{: #custom-web}

Sie können Ihrer Web-App eine angepasste Authentifizierung hinzufügen.

## Vorbereitungen
{: #before-you-begin}

Voraussetzungen:
* Eine Web-App mit dem Endpunkt `/apps/:Guid/<RealmName>/handleChallengeAnswer`, der
bei erfolgreicher Authentifizierung eine Benutzeridentität zurückgibt. Folgende JSON-Struktur der Benutzeridentität sollte gegeben sein:

   ```json
  userIdentity: {
  userName: <username>,
  displayName: <displayName>;
 };
```
* Instanz einer {{site.data.keyword.Bluemix_notm}}-Anwendung, die durch den {{site.data.keyword.amashort}}-Service geschützt ist. Weitere Informationen zur Erstellung eines {{site.data.keyword.Bluemix_notm}}-Back-Ends finden Sie in der [Einführung](index.html).



## {{site.data.keyword.amashort}}-App für angepasste Authentifizierung konfigurieren


1. Öffnen Sie Ihre App im {{site.data.keyword.Bluemix_notm}}-Dashboard.
1. Klicken Sie auf die Kachel für {{site.data.keyword.amashort}}. Das {{site.data.keyword.amashort}}-Dashboard wird geladen.
1. Klicken Sie auf die Kachel 'Angepasst'.
1. Geben Sie das **angepasste Realm**, die **angepasste Identitätsprovider-URL** und den **Weiterleitungs-URI** an. Klicken Sie auf 'Speichern'.

## {{site.data.keyword.amashort}} für angepasste Webauthentifizierung verwenden

Gehen Sie wie folgt vor, um den Autorisierungsprozess zu starten:

1. Leiten Sie von Ihrer Web-App zum folgenden Endpunkt des Autorisierungsservers weiter:

    https://imf-newauthserver.bluemix.net/oauth/v2/authorization

  Verwenden Sie dabei die folgenden Abfrageparameter:
   ```
   response_type=’authorization_code’
   client_id= <bluemix\_app\_guid>
   redirect_uri= <uri für die Weiterleitung nach Abrufen eines Autorisierungscodes>
   scope= ‘openid’
   state= <state>
   ```

    Der Parameter `state` ist momentan nicht im Gebrauch und kann leer gelassen werden.

    Der Parameter `redirect_uri` legt die Weiterleitung nach erfolgreicher oder fehlgeschlagener Authentifizierung Ihres angepassten Identitätsproviders fest.

1. Nach der Weiterleitung zum Autorisierungsendpunkt wird ein Anmeldeformular angezeigt. Geben Sie den Benutzernamen und das Kennwort ein, um die Authentifizierung bei Ihrem Identitätsprovider einzuleiten
und eine Weiterleitung an den `redirect_uri`.
Die nach erfolgreicher Authentifizierung zurückgegebene Antwort enthält den Autorisierungscode in den Anforderungsabfrageparametern.

4. Senden Sie eine `POST`-Anforderung an den Token-Endpunkt des Autorisierungsservers:

 https://imf-newauthserver.bluemix.net/*oauth/v2/token

 Verwenden Sie dabei die folgenden Abfrageparameter:
 ```
 grant_type = 'authorization_code'
 client_id = <bluemix_app_guid>
 redirect_uri = <redirect_uri>
 code = <authorization code>
 ```
  Der Parameter `redirect_uri` muss mit dem `redirect_uri` aus Schritt 1 übereinstimmen. Der Autorisierungscode wurde von der Anforderung in Schritt 2 zurückgegeben.

  Sie müssen diese `POST`-Anforderung innerhalb von 10 Minuten senden, da der Autorisierungscode maximal 10 Minuten gültig ist.

Der Antwortteil von `POST` enthält das *access_token* und das
*id_token* in Base64-Codierung.

## Authentifizierung testen


Nun können Sie mit dem Senden von Anforderungen an Ihre geschützten Ressourcen beginnen.
Alle Anforderungen an geschützte Ressourcen sollten das `access_token` enthalten.
Senden Sie das Zugriffstoken im Headerfeld für die `Autorisierungsanforderung`.
