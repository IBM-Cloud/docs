---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Einfache Benachrichtigungen an Web-Browser senden
{: #web_notifications}
Letzte Aktualisierung: 11. Januar 2017
{: .last-updated}

Nach dem Entwickeln Ihrer Anwendungen können Sie Push-Benachrichtigungen senden. 

1. Wählen Sie **Benachrichtigungen senden** aus und erstellen Sie eine Nachricht, indem Sie **Webbenachrichtigungen** als Option für **Senden an** auswählen. 
2. Geben Sie im Feld **Nachricht** die Nachricht an, die gesendet werden soll.
3. Sie können auswählen, optionale Einstellungen anzugeben:
  - **Benachrichtigungstitel**: Dies ist der Text, der als Kopfzeile des Nachrichtenalerts angezeigt würde.
  - **URL des Benachrichtigungssymbols**: Falls Ihre Nachricht mit einem App-Benachrichtigungssymbol gesendet werden muss, stellen Sie den Link zu Ihrem Symbol in dem Feld zur Verfügung.
  - **Lebensdauer**: Teilt dem Server die Gültigkeit der Nachrichten mit.
4. Für Web-Benachrichtigungen, die an den Browser Safari gesendet werden, sind zusätzliche Informationen erforderlich:
  - **Aktion**: Dies ist die Bezeichnung der Aktionsschaltfläche.
  - **URL-Argumente**: Die URL-Argumente, die mit dieser Benachrichtigung verwendet werden müssen. Stellen Sie sicher, dass dies in Form eines JSON-Arrays geschieht. 
 
Die folgende Abbildung zeigt die Webbenachrichtigungsoptionen im Dashboard an.

  ![Anzeige 'Benachrichtigungen'](images/DashboardWebpush.jpg)


## Nächste Schritte
  {: #next_steps_tags}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie diese Funktionen des {{site.data.keyword.mobilepushshort}}-Service Ihrer App hinzu. Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html). Informationen zur Verwendung erweiterter Benachrichtigungsoptionen finden Sie in [Erweiterte Benachrichtigungen](t_advance_badge_sound_payload.html).



