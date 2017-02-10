---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Abilitazione delle notifiche Rich Media
{: #interactive-notifications}
Ultimo aggiornamento: 11 gennaio 2017
{: .last-updated}


Puoi abilitare Rich Media {{site.data.keyword.mobilepushshort}} in iOS 10 e superiore. Le notifiche di push possono essere inviate con audio, video, GIF e immagini. 

Per configurare la tua applicazione per ricevere rich push su iOS 10, completa la procedura:  

1. In Xcode, seleziona **File** > **New** > **Target** > **Notification Service Extension**.
2. Sul metodo `didReceive()` in `UNNotificationServiceExtension`, aggiungi il codice.
```
BMSPushRichPushNotificationOptions.didReceive(request, withContentHandler: contentHandler)
```
	
Per inviare un Rich Media {{site.data.keyword.mobilepushshort}} dal dashboard Push, assicurati di specificare i campi relativi a messaggio, titolo, sottotitolo e URL allegato.
