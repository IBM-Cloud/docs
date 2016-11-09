---

copyright:
 years: 2015, 2016

---

# Push Notifications aktivieren
{: #c_enable_push-notifications}
Letzte Aktualisierung: 17. Oktober 2016
{: .last-updated}

Sie können Anwendungen für den Empfang von Push-Benachrichtigungen an Ihre Geräte aktivieren.

In diesem Abschnitt wird beschrieben, wie Sie Ihre Clientanwendungen - mobile oder Web-Browser-Anwendungen und auch Chrome-Apps und Erweiterungen - für den Empfang von Push-Benachrichtigungen aktivieren, wie Sie grundlegende Benachrichtigungen erstellen, wie Sie das SDK oder Plug-in abrufen und initialisieren und wie Sie Ihr Gerät oder Ihren Browser für den Empfang von Push-Benachrichtigungen registrieren. Sie können auch die [REST-API](t_restapi.html) verwenden, um Ihre mobilen Anwendungen und Web-Browser-Anwendungen für den Empfang von Push-Benachrichtigungen zu aktivieren.

Hinweis: Für Registrierungen von Geräten, Browsern und Chrome-Apps und Erweiterungen pflegt der {{site.data.keyword.mobilepushshort}}-Service eine eindeutige Referenz auf Tokens, die von Benachrichtigungsprovidern ausgegeben werden (APNs für Apple bzw. GCM für Google). Der Benachrichtigungsprovider des {{site.data.keyword.mobilepushshort}}-Service kann diese Tokens aus diversen Gründen inaktivieren. 

Ein Beispiel wäre die Inaktivierung bei der Deinstallation einer App auf dem Gerät. Bei einem Szenario, bei dem der Versuch unternommen wird, eine Benachrichtigung auf Grundlage der Providerantwort über die Inaktivierung des Geräts zuzustellen, entfernt der {{site.data.keyword.mobilepushshort}}-Service die Geräte- oder Web-Browserregistrierungen. Dadurch werden wiederum nachfolgende Versuche, die Benachrichtigung an diese inaktivierten Geräte zu senden, blockiert.
