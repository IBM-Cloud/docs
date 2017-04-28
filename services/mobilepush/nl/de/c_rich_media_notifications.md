---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Rich Media-Benachrichtigungen aktivieren
{: #interactive-notifications}
Letzte Aktualisierung: 09. März 2017
{: .last-updated}


Sie können Rich Media {{site.data.keyword.mobilepushshort}} iOS 10 und höher aktivieren. Push-Benachrichtigungen können mit Audio, Video, GIFs und Bildern gesendet werden. 

Führen Sie die folgenden Schritte aus, um Ihre Anwendungen unter iOS 10 für den Empfang von Rich Push-Benachrichtigungen einzurichten:  

1. Wählen Sie in Xcode **File** > **New** > **Target** > **Notification Service Extension** aus.
2. Fügen Sie in der Methode `didReceive()` in `UNNotificationServiceExtension` den folgenden Code hinzu.
```
BMSPushRichPushNotificationOptions.didReceive(request, withContentHandler: contentHandler)
```
	
Geben Sie zum Senden einer Rich Media-Push-Benachrichtigung über das Push-Dashboard unbedingt Daten in die Felder für Nachricht, Titel, Untertitel und attachmentURL ein.
