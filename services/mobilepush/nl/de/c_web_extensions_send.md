---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Einfache Benachrichtigungen an Chrome Apps and Extensions senden 
{: #web_extensions_notifications}
Letzte Aktualisierung: 11. Januar 2017
{: .last-updated}

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
  
## Nächste Schritte
  {: #next_steps_tags}

Nachdem Sie einfache Benachrichtigungen erfolgreich eingerichtet haben, können Sie tagbasierte Benachrichtigungen und erweiterte Optionen konfigurieren.

Fügen Sie diese {{site.data.keyword.mobilepushshort}}-Service-Features zur App hinzu.
Informationen zur Verwendung tagbasierter Benachrichtigungen finden Sie in [Tagbasierte Benachrichtigungen](c_tag_basednotifications.html). Informationen zur Verwendung erweiterter Benachrichtigungsoptionen finden Sie in [Erweiterte Benachrichtigungen](t_advance_badge_sound_payload.html).
