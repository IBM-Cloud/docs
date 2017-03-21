---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Webhooks aktivieren 
{: #tag_based_notifications}
Letzte Aktualisierung: 23. Januar 2017
{: .last-updated}


Mit dem {{site.data.keyword.mobilepushshort}}-Service können Sie sich für das Empfangen von Alerts zu Informationen, die sich geändert haben, entscheiden. Änderungen an Unternehmensinformationen erzeugen Ereignisse, zu denen Sie Benachrichtigungen erhalten können, indem Sie sie als Webhook-Ereignisse registrieren. Diese Webhook-Ereignisse lösen einen Alert aus. 

Webhooks sind benutzerdefinierte Callbacks, die durch ein Ereignis ausgelöst werden, beispielsweise das Registrieren eines Geräts oder das Subskribieren eines Tags. Mit dem {{site.data.keyword.mobilepushshort}}-Service können Sie sich für die folgenden Webhook-Ereignisse registrieren: 

- **onDeviceRegister**: Ein Webhook-Ereignis wird für Geräte ausgelöst, die für Push-Operationen registriert werden.
- **onDeviceUpdate**: Ein Webhook-Ereignis wird ausgelöst, wenn Informationen zu einem registrierten Gerät aktualisiert werden.
- **onDeviceUnregister**: Ein Webhook-Ereignis wird ausgelöst, wenn die Registrierung eines Geräts aufgehoben wird. 
- **onSubscribe**: Ein Webhook-Ereignis wird ausgelöst, wenn ein Benutzer einen Tag subskribiert.
- **onUnsubscribe**: Ein Webhook-Ereignis wird ausgelöst, wenn ein Benutzer die Subskription eines Tags aufhebt.
- **onNotificationSend**: Ein Webhook-Ereignis wird für eine Benachrichtigung ausgelöst, die versandt wurde.
- **onNotificationFailure**: Ein Webhook-Ereignis wird für fehlgeschlagene Benachrichtigungen ausgelöst.


**Anmerkung**: Das Versenden von Benachrichtigungen erfolgt in Stapeln. Dieselbe Nachrichtenversendung kann mehrere Webhook-Ereignisse umfassen, wobei es sich sowohl um fehlgeschlagene als auch um erfolgreiche handeln kann. 
Die Webhook-Ereignisse haben dieselbe Nachrichten-ID (messageID) wie die versandte Nachricht. 

Weitere Informationen zu Webhooks finden Sie in der [IBM Push Notifications-REST-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobile.{DomainName}/imfpush/#/webhooks){: new_window}.
