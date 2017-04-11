---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Paket 'Push Notifications' verwenden
{: #openwhisk_catalog_pushnotifications}

Das Paket `/whisk.system/pushnotifications` ermöglicht Ihnen die Arbeit mit einem Push-Service.

Das Paket enthält die folgende Aktion und den folgenden Feed:

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | Paket | appId, appSecret  | Arbeit mit Push-Service |
| `/whisk.system/pushnotifications/sendMessage` | Aktion | text, url, deviceIds, platforms, tagNames, gcmPayload, gcmSound, gcmCollapseKey, gcmDelayWhileIdle, gcmPriority, gcmTimeToLive, gcmSync, gcmVisibility, gcmStyleType, gcmStyleTitle, gcmStyleUrl, gcmStyleText, gcmStyleLines, apnsBadge, apnsCategory, apnsIosActionKey, apnsPayload, apnsType, apnsSound, fireFoxTitle, fireFoxIconUrl, fireFoxTimeToLive, fireFoxPayload, chromeTitle, chromeIconUrl, chromeTimeToLive, chromePayload, chromeAppExtTitle, chromeAppExtCollapseKey, chromeAppExtDelayWhileIdle, chromeAppExtIconUrl, chromeAppExtTimeToLive, chromeAppExtPayload | Push-Benachrichtigung an angegebene Geräte senden |
| `/whisk.system/pushnotifications/webhook` | Feed | events | Löst Auslöserereignisse für Geräteaktivitäten (Registrierung des Geräts, Rücknahme der Registrierung, Abonnement für Gerät, Beendigung des Abonnements) für den Push-Service aus |
Es wird empfohlen, eine Paketbindung mit den Werten `appId` und `appSecret` zu erstellen. Auf diese Weise brauchen Sie diese Berechtigungsnachweise nicht jedes Mal anzugeben, wenn Sie die Aktionen im Paket aufrufen.

## Push-Paketbindung erstellen
{: #openwhisk_catalog_pushnotifications_create}

Bei der Erstellung einer Paketbindung für Push-Benachrichtigungen müssen Sie die folgenden Parameter angeben.

-  `appId`: Die GUID für die Bluemix-App.
-  `appSecret`: Der geheime Schlüssel des Bluemix Push-Benachrichtigungsservice.

Das folgende Beispiel zeigt die Erstellung einer Paketbindung.

1. Erstellen Sie eine Bluemix-Anwendung in einem [Bluemix-Dashboard](http://console.ng.bluemix.net).

2. Initialisieren Sie den Push-Benachrichtigungsservice und binden Sie den Service an die Bluemix-Anwendung.

3. Konfigurieren Sie die [Push Notifications-Anwendung](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).
  
  Notieren Sie sich die Werte für `App GUID` und `App Secret` der von Ihnen erstellten Bluemix-App.
  
4. Erstellen Sie eine Paketbindung mit den `/whisk.system/pushnotifications`.
  
  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
  ```
  {: pre}
  
5. Prüfen Sie, ob die Paketbindung vorhanden ist.
  
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myPush private binding
  ```
  

## Push-Benachrichtigungen senden
{: #openwhisk_catalog_pushnotifications_send}

Von der Aktion `/whisk.system/pushnotifications/sendMessage` werden Push-Benachrichtigungen an registrierte Geräte gesendet. Die folgenden Parameter sind verfügbar:
- `text`: Die Benachrichtigung, die dem Benutzer angezeigt wird. Beispiel: `-p text "Hallo, OpenWhisk sendet eine Benachrichtigung"`.
- `url`: Eine optionale URL, die zusammen mit einem Alert gesendet werden kann. Beispiel: `-p url "https:\\www.w3.ibm.com"`.
- `deviceIds` Die Liste der angegebenen Geräte. Beispiel: `-p deviceIds ["deviceID1"]`.
- `platforms` Zum Senden einer Benachrichtigung an die Geräte der angegebenen Plattformen. 'A' für Apple- (iOS) Geräte und 'G' für Google- (Android) Geräte. Beispiel: `-p platforms ["A"]`.
- `tagNames` Zum Senden einer Benachrichtigung an die Geräte, die einen dieser Tags subskribiert haben. Beispiel: `-p tagNames "[\"tag1\"]" `.
- `gcmPayload`: Angepasste JSON-Nutzdaten, die als Bestandteil der Benachrichtigung gesendet werden. Beispiel: `-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`: Die Audiodatei (auf einem Gerät), die abgespielt werden soll, wenn die Benachrichtigung vom Gerät empfangen wird.
- `gcmCollapseKey`: Dieser Parameter gibt eine Gruppe aus Nachrichten an.
- `gcmDelayWhileIdle`: Wenn für diesen Parameter der Wert 'true' festgelegt wird, gibt dies an, dass die Nachricht erst gesendet werden darf, wenn das Gerät aktiv wird.
- `gcmPriority`: Legt die Priorität der Nachricht fest.
- `gcmTimeToLive`: Dieser Parameter gibt an, wie lange (in Sekunden) die Nachricht im GCM-Speicher aufbewahrt wird, wenn das Gerät offline ist.
- `gcmSync`: Durch Nachrichtenübermittlung in der Gerätegruppe kann jede App-Instanz in einer Gruppe den aktuellen Nachrichtenstatus wiedergeben.
- `gcmVisibility`: private/public - Die Sichtbarkeit dieser Benachrichtigung, die beeinflusst, wie und wann Benachrichtigungen auf einer sicheren gesperrten Anzeige sichtbar werden.
- `gcmStyleType`: Gibt den Typ von erweiterbaren Benachrichtigungen an. Mögliche Werte: `bigtext_notification`, `picture_notification`, `inbox_notification`.
- `gcmStyleTitle`: Gibt den Titel der Benachrichtigung an. Der Titel wird angezeigt, wenn die Benachrichtigung erweitert wird. Der Titel muss für alle drei erweiterbaren Benachrichtigungstypen angegeben werden.
- `gcmStyleUrl`: Eine URL, über die die Abbildung für die Benachrichtigung abzurufen ist. Muss für 'picture_notification' angegeben werden.
- `gcmStyleText`: Der große Text, der nach dem Erweitern einer Benachrichtigung mit großem Text ('bigtext_notification') angezeigt werden muss. Muss für 'bigtext_notification' angegeben werden.
- `gcmStyleLines`: Ein Array mit Zeichenfolgen, das im Posteingangsstil für eine Posteingangsbenachrichtigung ('inbox_notification') angezeigt werden soll. Muss für 'inbox_notification' angegeben werden.
- `apnsBadge`: Die Nummer, die als Markierung des Anwendungssymbols angezeigt werden soll.
- `apnsCategory`: Die Kategoriekennung, die für interaktive Push-Benachrichtigungen verwendet werden soll.
- `apnsIosActionKey`: Der Titel für den Aktionsschlüssel.
- `apnsPayload`: Angepasste JSON-Nutzdaten, die als Bestandteil der Benachrichtigung gesendet werden.
- `apnsType`: ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound`: Der Name der Audiodatei im Anwendungsbundle. Die Tonsignale dieser Datei werden als Alert abgespielt.
- `fireFoxTitle`: Gibt den Titel an, der für die WebPush Notification festgelegt werden soll.
- `fireFoxIconUrl`: Die URL des Symbols, das für die WebPush Notification festgelegt werden soll.
- `fireFoxTimeToLive`: Dieser Parameter gibt an, wie lange (in Sekunden) die Nachricht im GCM-Speicher aufbewahrt wird, wenn das Gerät offline ist.
- `fireFoxPayload`: Angepasste JSON-Nutzdaten, die als Bestandteil der Benachrichtigung gesendet werden.
- `chromeTitle`: Gibt den Titel an, der für die WebPush Notification festgelegt werden soll.
- `chromeIconUrl`: Die URL des Symbols, das für die WebPush Notification festgelegt werden soll.
- `chromeTimeToLive`: Dieser Parameter gibt an, wie lange (in Sekunden) die Nachricht im GCM-Speicher aufbewahrt wird, wenn das Gerät offline ist.
- `chromePayload`: Angepasste JSON-Nutzdaten, die als Bestandteil der Benachrichtigung gesendet werden.
- `chromeAppExtTitle`: Gibt den Titel an, der für die WebPush Notification festgelegt werden soll.
- `chromeAppExtCollapseKey`: Dieser Parameter gibt eine Gruppe aus Nachrichten an.
- `chromeAppExtDelayWhileIdle`: Wenn für diesen Parameter der Wert 'true' festgelegt wird, gibt dies an, dass die Nachricht erst gesendet werden darf, wenn das Gerät aktiv wird.
- `chromeAppExtIconUrl`: Die URL des Symbols, das für die WebPush Notification festgelegt werden soll.
- `chromeAppExtTimeToLive`: Dieser Parameter gibt an, wie lange (in Sekunden) die Nachricht im GCM-Speicher aufbewahrt wird, wenn das Gerät offline ist.
- `chromeAppExtPayload`: Angepasste JSON-Nutzdaten, die als Bestandteil der Benachrichtigung gesendet werden.

Es folgt ein Beispiel für das Senden einer Push-Benachrichtigung aus dem Paket *pushnotification*.

- Senden Sie eine Push-Benachrichtigung mithilfe der Aktion `sendMessage` in der Paketbindung ab, die Sie zuvor erstellt haben. Stellen Sie sicher, dass Sie `/myNamespace/myPush` durch Ihren Paketnamen ersetzen.
  
  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking --result  -p url https://example.com -p text "this is my message"  -p sound soundFileName -p deviceIds "[\"T1\",\"T2\"]"
  ```
  {: pre}
  ```json
  {
    "result": {
    "pushResponse": 
      {
        "messageId":"11111H",
        "message":{
          "alert":"this is my message",
          "url":""
        },
        "settings":{
          "apns":{
            "sound":"default"
          },
          "gcm":{
            "sound":"default"
            },
          "target":{
            "deviceIds":["T1","T2"]
          }
        }
      }
    },
      "status": "success",
      "success": true
  }
  ```
  

## Auslöserereignis für Aktivität des Push Notifications-Service aktivieren
{: #openwhisk_catalog_pushnotifications_fire}

Von `/whisk.system/pushnotifications/webhook` wird der Push-Service so konfiguriert, dass ein Auslöser aktiviert wird, wenn eine Gerätaktivität wie eine Geräteregistrierung bzw. die Rücknahme einer Gerätregistrierung oder ein Abonnement bzw. das Beenden eines Abonnements für eine angegebene Anwendung auftritt.

Die folgenden Parameter sind verfügbar:

- `appId:` Die GUID für die Bluemix-App.
- `appSecret:` Der geheime Schlüssel des Push Notifications-Service von Bluemix.
- `events:` Unterstützte Ereignisse sind `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe` und `onUnsubscribe`. Wenn Sie bei allen Ereignissen benachrichtigt werden möchten, verwenden Sie das Platzhalterzeichen `*`.

Das folgende Beispiel die Erstellung eines Auslösers, der jedes Mal aktiviert wird, wenn ein neues Gerät mit der Push Notifications-Serviceanwendung registriert wird.

1. Erstellen Sie eine Paketbindung, die für den Push Notifications-Service (mit Werten für 'appId' und 'appSecret') konfiguriert ist.
  
  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}
  
2. Erstellen Sie mithilfe des Feeds `myPush/webhook` einen Auslöser für den Ereignistyp `onDeviceRegister` des Push Notifications-Service.
  
  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}  
  
3. Sie könnten eine Regel erstellen, die jedes Mal eine Nachricht sendet, wenn ein neues Gerät registriert wird. Erstellen Sie eine neue Regel unter Verwendung der vorherigen Aktion und des vorherigen Auslösers.
  
  ```
  wsk rule create --enable myRule myPushTrigger sendMessage
  ```
  {: pre}
  
  Überprüfen Sie die Ergebnisse mit dem Befehl `wsk activation poll`.

  Registrieren Sie ein Gerät in Ihrer Bluemix-Anwendung und Sie können sehen, wie die Regel (`rule`), der Auslöser (`trigger`) und die Aktion (`action`) im openWhisk-Dashboard (https://console.{Domain}/openwhisk/dashboard) ausgeführt werden.

  Die Aktion sendet dann eine Push-Benachrichtigung.
  
