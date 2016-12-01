---

copyright:
 years: 2015, 2016

---

# Fehlerbehebung
{: #errors}
Letzte Aktualisierung: 08. November 2016
{: .last-updated}

In diesem Abschnitt finden Sie Anweisungen für die Behebung von allgemeinen Fehlern bei {{site.data.keyword.mobilepushshort}}.


### Internal server error occurred. Please contact admin. (Internal error code: PUSHD102E)

####Erläuterung

**Erläuterung**: Dieser Fehler kann auftreten, wenn Sie eine Push-Instanz vor November 2015 erstellt haben.  

####Benutzeraktion

**Aktion**: Um dieses Problem zu lösen, müssen Sie die Push-Instanz löschen und eine neue erstellen.

**Anmerkung**: Wenn Sie die Push-Instanz löschen, werden Ihre Tags nicht beibehalten.


### UnauthorizedRegistration

####Erläuterung

**Erläuterung**: Chrome Web Push funktioniert mit FCM-Schlüsseln (Firebase Cloud Messaging) nicht. Wenn Sie nach dem Umzug von FCM auf GCM unter Chrome keine Web-Push-Benachrichtigung erhalten, ist der Grund hierfür, dass die Website vorher für die Funktion mit dem GCM-Projekt konfiguriert war und das neue Projekt mit FCM erstellt wurde. Die generierten Tokens, die den Browser angeben, werden vom Chrome-Browser im Cache gespeichert.

**Aktion**: Sie können dieses Problem durch Entfernen der Cookies und Zurücksetzen der Berechtigungen des Browsers lösen. Hierfür wären Berechtigungen für die Aktivierung von Push Notifications erforderlich. 

