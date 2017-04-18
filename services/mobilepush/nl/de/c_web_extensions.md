---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Chrome-Apps und Erweiterungen für den Empfang von {{site.data.keyword.mobilepushshort}} aktivieren
{: #web_notifications}
Letzte Aktualisierung: 18. Januar 2017
{: .last-updated}

Sie können Google Chrome-Apps und Erweiterungen für den Empfang von {{site.data.keyword.mobilepushshort}} aktivieren. Stellen Sie sicher, dass die im Abschnitt [Berechtigungsnachweise für einen Benachrichtigungsprovider konfigurieren](t__main_push_config_provider.html) angegebenen Schritte durchgeführt wurden.

## Client-SDK für {{site.data.keyword.mobilepushshort}} installieren
{: #web_install}

In diesem Thema wird die Vorgehensweise zum Installieren und Verwenden des Client-JavaScript-Push-SDK für die weitere Entwicklung Ihrer Chrome-Apps und Erweiterungen beschrieben.

### Initialisierung in Google Chrome-Apps und Erweiterungen

Führen Sie folgende Schritte für die Installation des Javascript-SDK in Chrome-Apps und Erweiterungen aus:

Laden Sie `BMSPushSDK.js` und `manifest_Chrome_Ext.json` (für Chrome-Erweiterungen) oder `manifest_Chrome_App.json` (für Chrome-Apps) vom [Bluemix-Web-Push-SDK ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window} herunter.



- Für Chrome-Apps konfigurieren Sie die Manifestdatei:
 1. Geben Sie in der Datei `manifest_Chrome_App.json` den Namen, die Beschreibung und die Symbole an.
 2. Fügen Sie die Datei `BMSPushSDK.js` in den `app.background.scripts` hinzu.
 3. Ändern Sie die Datei `manifest_Chrome_App.json` in `manifest.json`.

- Für Chrome-Erweiterungen konfigurieren Sie die Manifestdatei:
 1. Geben Sie in der Datei `manifest_Chrome_Ext.json` den Namen, die Beschreibung und die Symbole an.
 2. Fügen Sie die Datei `BMSPushSDK.js` in den `background.scripts` hinzu.
 3. Ändern Sie die Datei `manifest_Chrome_Ext.json` in `manifest.json`.

Fügen Sie in der Datei `background.js` Folgendes hinzu, um Push-Benachrichtigungen empfangen zu können. 
```
chrome.gcm.onMessage.addListener(BMSPushBackground.onMessageReceived)
chrome.notifications.onClicked.addListener(BMSPushBackground.notification_onClicked);
chrome.notifications.onButtonClicked.addListener(BMSPushBackground.notifiation_buttonClicked); 
```
	{: codeblock}



## Push-SDK initialisieren 
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

## Chrome-Apps und Erweiterungen registrieren
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




