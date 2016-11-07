---

copyright:
 years: 2015 2016

---


# Webanwendungen für den Empfang von {{site.data.keyword.mobilepushshort}} aktivieren
{: #web_notifications}
Letzte Aktualisierung: 17. Oktober 2016
{: .last-updated}

Sie können jetzt Google Chrome- und Mozilla Firefox-Webanwendungen für den Empfang von {{site.data.keyword.mobilepushshort}} aktivieren.

## Web-Browser-Client-SDK für {{site.data.keyword.mobilepushshort}} installieren
{: #web_install}

Dieses Thema beschreibt die Vorgehensweise zum Installieren und Verwenden des Client-JavaScript-Push-SDKs für die weitere Entwicklung Ihrer Web-Anwendungen.

### Initialisierung in der Google Chrome-Webanwendung

Führen Sie folgende Schritte für die Installation des Javascript-SDK in Chrome-Webanwendungen aus:

Laden Sie die Dateien `BMSPushSDK.js`, `BMSPushServiceWorker.js` und `manifest_Website.json` vom [Bluemix-Web-Push-SDK](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master) herunter.

1. Bearbeiten Sie die Datei `manifest_Website.json`.

Beim Google Chrome-Browser ändern Sie `name` in den Namen Ihrer Site. Ändern Sie `gcm_sender_id` in Ihre Absender-ID von Firebase Cloud Messaging (FCM) bzw. Google Cloud Messaging (GCM). Weitere Informationen finden Sie in der Dokumentation zu [Google](https://developers.google.com/web/fundamentals/getting-started/codelabs/push-notifications/#make_a_project_on_the_google_developer_console). Der Wert für gcm_sender_id enthält nur Ziffern.

```
 {
  "name": "YOUR_WEBSITE_NAME",
      "gcm_sender_id": "GCM_Sender_Id"
 }
```
    {: codeblock}
 
Fügen Sie für Mozilla Firefox-Browser die folgenden Werte in der Datei `manifest.json` hinzu.     Ändern Sie `name` in den Namen Ihrer Site.

```
{
  "name": "YOUR_WEBSITE_NAME"
 }
```
    {: codeblock}

2. Ändern Sie den Namen der Datei `manifest_Website.json` in `manifest.json`.
3. Fügen Sie die Dateien `BMSPushSDK.js`, `BMSPushServiceWorker.js` und `manifest.json` zu Ihrem Stammverzeichnis hinzu.
3. Schließen Sie die Datei `manifest.json` in das Tag `<head>` Ihrer HTML-Datei ein.
```
 <link rel="manifest" href="manifest.json">
```
    {: codeblock}
4. Fügen Sie das Bluemix-Web-Push-SDK von GitHub zur Webanwendung hinzu.
```
 <script src="BMSPushSDK.js" async></script>
```
    {: codeblock}

## Das Web-Push-SDK initialisieren 
{: #web_initialize}

Initialisieren Sie das Push-SDK mit den Bluemix {{site.data.keyword.mobilepushshort}}-Services `app GUID` und `app Region`.  

Zum Abrufen Ihrer App-GUID wählen Sie die Option **Konfiguration** für Ihre initialisierten Push-Services im Navigationsbereich aus und klicken auf **Mobile Systemerweiterungen**. Ändern Sie das Code-Snippet so, dass Ihre Parameter für die appGUID des Push Notifications Service von Bluemix verwendet werden.

Die `App Region` gibt den Standort an, an dem der {{site.data.keyword.mobilepushshort}}-Service gehostet ist. Sie können einen der folgenden drei Werte verwendet:

 - Für USA Dallas:	 `.ng.bluemix.net`
 - Für Großbritannien:			 `.eu-gb.bluemix.net`
 - Für Sydney:		 `.au-syd.bluemix.net`

```
 var bmsPush = new BMSPush();
    function callback(response) {
 alert(response.response)
    }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
   "clientSecret":"clientSecret of your push service"
    }
  bmsPush.initialize(params, callback)
```
	{: codeblock}

## Webanwendung registrieren
{: #web_register}

Verwenden Sie die API `register()`, um das Gerät beim {{site.data.keyword.mobilepushshort}}-Service zu registrieren. Für die Registrierung von Google Chrome aus fügen Sie den API-Schlüssel für Firebase Cloud Messaging (FCM) bzw. Google Cloud Messaging (GCM) sowie die URL der Website im Bluemix-Dashboard für die Webkonfiguration des {{site.data.keyword.mobilepushshort}}-Service hinzu. Weitere Informationen finden Sie im Abschnitt [Berechtigungsnachweise für Google Cloud Messaging (GCM) konfigurieren](t_push_provider_android.html) unter dem Thema Chrome-Konfiguration.

Für die Registrierung von Mozilla Firefox fügen Sie die URL der Website im Dashboard für die Webkonfiguration von Bluemix {{site.data.keyword.mobilepushshort}}-Service unter der Firefox-Konfiguration hinzu.

Verwenden Sie folgendes Code-Snippet, um sich beim Bluemix {{site.data.keyword.mobilepushshort}}-Service zu registrieren.
```
var bmsPush = new BMSPush();
    function callback(response) {
     alert(response.response)
    }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
   "clientSecret":"clientSecret of your push service"
    }
  bmsPush.initialize(params, callback)
    bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}

## Einfache Push-Benachrichtigungen senden
  {: #send}

Nach dem Entwickeln Ihrer Anwendungen können Sie Push-Benachrichtigungen senden. 

1. Wählen Sie **Benachrichtigungen senden** aus und erstellen Sie eine Nachricht, indem Sie **Webbenachrichtigungen** als Option für **Senden an** auswählen. 
2. Geben Sie im Feld **Nachricht** die Nachricht an, die gesendet werden soll.
3. Sie können auswählen, optionale Einstellungen anzugeben:
  - **Benachrichtigungstitel**: Dies ist der Text, der als Kopfzeile des Nachrichtenalerts angezeigt würde.
  - **URL des Benachrichtigungssymbols**: Falls Ihre Nachricht mit einem App-Benachrichtigungssymbol gesendet werden muss, stellen Sie den Link zu Ihrem Symbol in dem Feld zur Verfügung.
  - **Zusätzliche Nutzdaten**: Gibt die angepassten Werte für Nutzdaten für Ihre Benachrichtigungen an.

Die folgende Abbildung zeigt die Webbenachrichtigungesoptionen im Dashboard an.

  ![Anzeige 'Benachrichtigungen'](images/DashboardWebpush.jpg)
  
## Nächste Schritte
  {: #next_steps_tags}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie die folgenden Funktionen des {{site.data.keyword.mobilepushshort}}-Service zu Ihrer App hinzu. Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html). Informationen zur Verwendung erweiterter Benachrichtigungsoptionen finden Sie in [Erweiterte Benachrichtigungen](t_advance_badge_sound_payload.html).



