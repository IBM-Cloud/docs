---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Fehlerbehebung
{: #errors}
Letzte Aktualisierung: 07. Dezember 2016
{: .last-updated}

In diesem Abschnitt finden Sie Anweisungen für die Behebung von allgemeinen Fehlern bei {{site.data.keyword.mobilepushshort}}.


### Internal server error occurred. Please contact admin. (Internal error code: PUSHD102E)

**Erläuterung**: Dieser Fehler kann auftreten, wenn Sie eine Push-Instanz vor November 2015 erstellt haben.  

**Benutzeraktion**: Um das Problem zu lösen, müssen Sie die Push-Instanz löschen und eine neue erstellen. Beachten Sie, dass Ihre Tags nicht beibehalten werden, wenn Sie die Push-Instanz löschen.


### UnauthorizedRegistration

**Erläuterung**: Chrome Web Push funktioniert mit FCM-Schlüsseln (Firebase Cloud Messaging) nicht. Wenn Sie nach dem Umzug von FCM auf GCM unter Chrome keine Web-Push-Benachrichtigung erhalten, ist der Grund hierfür, dass die Website vorher für die Funktion mit dem GCM-Projekt konfiguriert war und das neue Projekt mit FCM erstellt wurde. Die generierten Tokens, die den Browser angeben, werden vom Chrome-Browser im Cache gespeichert.

**Benutzeraktion**: Sie können dieses Problem durch Entfernen der Cookies und Zurücksetzen der Berechtigungen des Browsers lösen. Hierfür wären Berechtigungen für die Aktivierung von Push Notifications erforderlich. 

