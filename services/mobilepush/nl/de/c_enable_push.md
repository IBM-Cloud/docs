---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Benachrichtigungen für mobile Geräte aktivieren
{: #c_enable_push-notifications}
Letzte Aktualisierung: 18. Januar 2017
{: .last-updated}

Stellen Sie sicher, dass die im Abschnitt [Berechtigungsnachweise für einen Benachrichtigungsprovider konfigurieren](t__main_push_config_provider.html) angegebenen Schritte durchgeführt wurden.

In diesem Abschnitt wird beschrieben, wie Sie Ihre Clientanwendungen - mobile oder Web-Browser-Anwendungen und auch Chrome-Apps und Erweiterungen - für den Empfang von Push-Benachrichtigungen aktivieren, wie Sie grundlegende Benachrichtigungen erstellen, wie Sie das SDK oder Plug-in abrufen und initialisieren und wie Sie Ihr Gerät oder Ihren Browser für den Empfang von Push-Benachrichtigungen registrieren. Sie können auch die [REST-API](t_restapi.html) verwenden, um Ihre mobilen Anwendungen und Web-Browser-Anwendungen für den Empfang von Push-Benachrichtigungen zu aktivieren.

**Hinweis**: Für Registrierungen von Geräten, Browsern, Chrome-Apps und Erweiterungen pflegt der {{site.data.keyword.mobilepushshort}}-Service eine eindeutige Referenz auf Tokens, die von Benachrichtigungsprovidern ausgegeben werden
(APNs für Apple bzw. FCM für Google). Der Benachrichtigungsprovider des {{site.data.keyword.mobilepushshort}}-Service kann diese Tokens aus diversen Gründen inaktivieren. 

Ein Beispiel wäre die Inaktivierung bei der Deinstallation einer App auf dem Gerät. Bei einem Szenario, bei dem der Versuch unternommen wird, eine Benachrichtigung auf Grundlage der Providerantwort über die Inaktivierung des Geräts zuzustellen, entfernt der {{site.data.keyword.mobilepushshort}}-Service die Geräte- oder Web-Browserregistrierungen. Dadurch werden wiederum nachfolgende Versuche, die Benachrichtigung an diese inaktivierten Geräte zu senden, blockiert.
