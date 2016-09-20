---

copyright:
 years: 2015, 2016

---

# Benachrichtigungen aktivieren
{: #c_enable_push-notifications}
Letzte Aktualisierung: 16. August 2016
{: .last-updated}

Sie können Anwendungen für den Empfang von Push-Benachrichtigungen von Ihren Geräten sowie für das Senden von Push-Benachrichtigungen an Ihre Geräte aktivieren.

In diesem Abschnitt wird beschrieben, wie Sie Ihre mobilen Anwendungen für den Empfang von Push-Benachrichtigungen aktivieren können, wie einfache Benachrichtigungen erstellt werden und wie das SDK bzw. das Plug-in abgerufen und initialisiert wird und wie Ihr Gerät für den Empfang von Push-Benachrichtigungen registriert wird. Sie können auch die [REST-API](t_restapi.html) verwenden, um Ihre mobilen Anwendungen für den Empfang von Push-Benachrichtigungen zu aktivieren.

Hinweis: Für Geräteregistrierungen mit Push pflegt der {{site.data.keyword.mobilepushshort}}-Service eine eindeutige Referenz auf Tokens, die von Benachrichtigungsprovidern ausgegeben werden (d. h. APNs für Apple oder GCM für Google). Der Benachrichtigungsprovider des {{site.data.keyword.mobilepushshort}}-Service kann diese Tokens aus diversen Gründen inaktivieren.  

Ein Beispiel wäre die Inaktivierung bei der Deinstallation einer App auf dem Gerät. Bei einem Szenario, bei dem der Versuch unternommen wird, eine Benachrichtigung auf Grundlage der Providerantwort über die Inaktivierung des Geräts zuzustellen, entfernt der {{site.data.keyword.mobilepushshort}}-Service die Geräteregistrierungen. Dadurch werden wiederum nachfolgende Versuche, die Benachrichtigung an diese inaktivierten Geräte zu senden, blockiert.
