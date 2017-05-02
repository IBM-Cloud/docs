---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Chrome-Apps und Erweiterungen für den Empfang von Push-Benachrichtigungen aktivieren
{: #web_notifications}
Letzte Aktualisierung: 12. April 2017
{: .last-updated}

Sie können Google Chrome-Apps und Erweiterungen für den Empfang von {{site.data.keyword.mobilepushshort}} aktivieren. Stellen Sie sicher, dass die im Abschnitt [Berechtigungsnachweise für einen Benachrichtigungsprovider konfigurieren](t__main_push_config_provider.html) angegebenen Schritte durchgeführt wurden.

## Client-SDK für Push-Benachrichtigungen installieren
{: #web_install}

In diesem Thema wird die Vorgehensweise zum Installieren und Verwenden des Client-JavaScript-Push-SDK für die weitere Entwicklung Ihrer Chrome-Apps und Erweiterungen beschrieben.

### Initialisierung in Google Chrome-Apps und Erweiterungen
{: #initialize_google_extn_app}

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



### Push-SDK initialisieren 
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

### Chrome-Apps und Erweiterungen registrieren
{: #web_register}

Verwenden Sie die API `register()`, um das Gerät beim {{site.data.keyword.mobilepushshort}}-Service zu registrieren. Für die Registrierung von Google Chrome aus fügen Sie den API-Schlüssel für Firebase Cloud Messaging (FCM) sowie die URL der Website im Bluemix-Dashboard für die Webkonfiguration des {{site.data.keyword.mobilepushshort}}-Service hinzu. Weitere Informationen finden Sie in [Berechtigungsnachweise für einen Benachrichtigungsprovider konfigurieren](t__main_push_config_provider.html).  

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


## Einfache Benachrichtigungen an Chrome Apps and Extensions senden 
{: #web_extensions_notifications}

Nach dem Entwickeln Ihrer Anwendungen können Sie Push-Benachrichtigungen senden. 

1. Wählen Sie **Benachrichtigungen senden** aus und erstellen Sie eine Nachricht, indem Sie **Webbenachrichtigungen** als Option für **Senden an** auswählen. 
2. Geben Sie im Feld **Nachricht** die Nachricht an, die gesendet werden soll.
3. Sie können auswählen, optionale Einstellungen anzugeben:
  - **Benachrichtigungstitel**: Dies ist der Text, der als Kopfzeile des Nachrichtenalerts angezeigt würde.
  - **URL des Benachrichtigungssymbols**: Falls Ihre Nachricht mit einem App-Benachrichtigungssymbol gesendet werden muss, stellen Sie den Link zu Ihrem Symbol in dem Feld zur Verfügung.
  - **Collapse key** (Schlüssel ausblenden): Ausgeblendete Schlüssel sind den Benachrichtigungen angehängt. Wenn mehrere Benachrichtigungen nacheinander mit demselben ausgeblendeten Schlüssel eintreffen, während das Gerät offline ist, werden die Benachrichtigungen ausgeblendet. Wenn ein Gerät wieder online ist, empfängt es Benachrichtigungen vom FCM/GCM-Server und zeigt nur die aktuellste Benachrichtigung an, die denselben ausgeblendeten Schlüssel aufweist. Falls der ausgeblendete Schlüssel nicht definiert ist, werden sowohl die neuen als auch die alten Nachrichten für die künftige Bereitstellung gespeichert.
  - **Time to live** (Lebensdauer): Dieser Wert wird in Sekunden angegeben. Falls dieser Parameter nicht angegeben ist, speichert der FCM/GCM-Server die Nachricht für vier Wochen und versucht, diese zu übermitteln. Die Gültigkeit läuft nach vier Wochen ab. Der mögliche Wertebereich liegt zwischen 0 und 2.419.200 Sekunden.
  - **Delay when idle**: (Verzögerung bei Inaktivität): Durch das Festlegen dieses Werts auf `true` wird der FCM/GCM-Server angewiesen, die Benachrichtigung nicht auszuliefern, wenn das Gerät inaktiv ist. Legen Sie für diesen Wert `false` fest, um die Übermittlung der Benachrichtigung sicherzustellen, auch wenn das Gerät inaktiv ist.
  - **Additional payload** (Zusätzliche Nutzdaten): Gibt die angepassten Werte für Nutzdaten für Ihre Benachrichtigungen an.

Die folgende Abbildung zeigt die Chrome Apps and Extensions-Benachrichtigungsoptionen im Dashboard an.

  ![Anzeige 'Benachrichtigungen'](images/push_chrome_extns.jpg)
  
### Nächste Schritte
{: #next_steps_tags}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie diese {{site.data.keyword.mobilepushshort}}-Service-Features zur App hinzu.
Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html). Informationen zur Verwendung erweiterter Benachrichtigungsoptionen finden Sie in [Erweiterte Benachrichtigungen](t_advance_badge_sound_payload.html).



