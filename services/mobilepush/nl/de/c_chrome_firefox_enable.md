---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Webanwendungen für den Empfang von Push-Benachrichtigungen aktivieren
{: #web_notifications}
Letzte Aktualisierung: 18. Januar 2017
{: .last-updated}

Sie können Google Chrome-, Mozilla Firefox- und Safari-Webanwendungen für den Empfang von Push-Benachrichtigungen aktivieren. Stellen Sie sicher, dass die im Abschnitt [Berechtigungsnachweise für einen Benachrichtigungsprovider konfigurieren](t__main_push_config_provider.html) angegebenen Schritte durchgeführt wurden.

## Web-Browser-Client-SDK für {{site.data.keyword.mobilepushshort}} installieren
{: #web_install}

Dieses Thema beschreibt die Vorgehensweise zum Installieren und Verwenden des Client-JavaScript-Push-SDKs für die weitere Entwicklung Ihrer Web-Anwendungen.

### Webanwendung initialisieren

Führen Sie folgende Schritte für die Installation des JavaScript SDK in der Google Chrome-Webanwendung aus:

Laden Sie die Dateien `BMSPushSDK.js`, `BMSPushServiceWorker.js` und `manifest_Website.json` vom [Bluemix-Web-Push-SDK](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window} herunter.

1. Bearbeiten Sie die Datei `manifest_Website.json`.
	- Beim Google Chrome-Browser ändern Sie `name` in den Namen Ihrer Site. Beispiel: `www.dailynewsupdates.com`. Ändern Sie `gcm_sender_id` in Ihre Absender-ID von Firebase Cloud Messaging (FCM) bzw. Google Cloud Messaging (GCM). Weitere Informationen finden Sie in [Absender-ID und API-Schlüssel abrufen](t_push_provider_android.html). Der Wert für gcm_sender_id enthält nur Ziffern.

		```
 			{
 			 "name": "YOUR_WEBSITE_NAME",
  			"gcm_sender_id": "GCM_Sender_Id"
			 }
		```
    		{: codeblock}
 
	- Fügen Sie für den Mozilla Firefox-Browser die folgenden Werte in der Datei `manifest_Website.json` hinzu. Geben Sie einen entsprechenden Namen (`name`) an. Dies kann der Name Ihrer Website sein.

		```
			{
 			 "name": "YOUR_WEBSITE_NAME"
			 }
		```
    		{: codeblock}

2. Ändern Sie den Namen der Datei `manifest_Website.json` in `manifest.json`.
3. Fügen Sie die Dateien `BMSPushSDK.js`, `BMSPushServiceWorker.js` und `manifest.json` zum Stammverzeichnis Ihrer Website hinzu.
3. Schließen Sie die Datei `manifest.json` in den Tag `<head>` Ihrer HTML-Datei ein.
```<link rel="manifest" href="manifest.json">
```
    {: codeblock}
4. Nehmen Sie das Web-Push-SDK von Bluemix in Ihre Webanwendung auf.
```<script src="BMSPushSDK.js" async></script>
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

``` var bmsPush = new BMSPush();
    function callback(response) {
 alert(response.response)
    }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
   "clientSecret":"clientSecret of your push service"
   "websitePushIDSafari": "Optional parameter for Safari Push Notifications only. The value should match the website Push ID provided during the server side configuration."
    }
  bmsPush.initialize(initParams, callback)
```
	{: codeblock}

**Anmerkung**: Wenn Ihre FCM-Berechtigungsnachweise für das Web-Push-SDK geändert werden, kann die Nachrichtenübermittlung für den Browser Chrome fehlschlagen. Um ein Fehlschlagen zu vermeiden, stellen Sie sicher, dass Sie `bmsPush.unRegisterDevice` aufrufen.

Wenn Sie einen falschen Parameter angeben, wird möglicherweise ein Konfigurationsfehler ausgegeben. Weitere Informationen finden Sie im Abschnitt [Web Push-Konfigurationsfehler beheben](troubleshooting_config_errors.html).

## Webanwendung registrieren
{: #web_register}

Verwenden Sie die API **register()**, um das Gerät beim {{site.data.keyword.mobilepushshort}}-Service zu registrieren. Verwenden Sie in Abhängigkeit von Ihrem Browser eine oder mehrere der folgenden Optionen.

- Für die Registrierung von Google Chrome aus fügen Sie den API-Schlüssel für Firebase Cloud Messaging (FCM) bzw. Google Cloud Messaging (GCM) sowie die URL der Website im Bluemix-Dashboard für die Webkonfiguration des {{site.data.keyword.mobilepushshort}}-Service hinzu. Weitere Informationen finden Sie im Abschnitt [Berechtigungsnachweise für Google Cloud Messaging (GCM) konfigurieren](t_push_provider_android.html) unter dem Thema Chrome-Konfiguration.

- Für die Registrierung von Mozilla Firefox fügen Sie die URL der Website im Dashboard für die Webkonfiguration von Bluemix {{site.data.keyword.mobilepushshort}}-Service unter der Firefox-Konfiguration hinzu.

Verwenden Sie folgendes Code-Snippet, um sich beim Bluemix {{site.data.keyword.mobilepushshort}}-Service zu registrieren.
```var bmsPush = new BMSPush();
    function callback(response) {
     alert(response.response)
    }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
  "clientSecret":"clientSecret of your push service"
  "websitePushIDSafari": "Optional parameter for Safari Push Notifications only. The value should match the website Push ID provided during the server side configuration."
  }
  bmsPush.initialize(params, callback)
    bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}






