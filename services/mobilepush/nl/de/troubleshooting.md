---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Fehlerbehebung
{: #errors}
Letzte Aktualisierung: 11. Januar 2017
{: .last-updated}

In diesem Abschnitt finden Sie Anweisungen für die Behebung von allgemeinen Fehlern bei {{site.data.keyword.mobilepushshort}}.


### Internal server error occurred. Please contact admin. (Internal error code: PUSHD102E)

**Erläuterung**: Dieser Fehler kann auftreten, wenn Sie eine Push-Instanz vor November 2015 erstellt haben.  

**Benutzeraktion**: Um das Problem zu lösen, müssen Sie die Push-Instanz löschen und eine neue erstellen. Beachten Sie, dass Ihre Tags nicht beibehalten werden, wenn Sie die Push-Instanz löschen.


### UnauthorizedRegistration

**Erläuterung**: Chrome Web Push funktioniert mit FCM-Schlüsseln (Firebase Cloud Messaging) nicht. Wenn Sie nach dem Umzug von FCM auf GCM unter Chrome keine Web-Push-Benachrichtigung erhalten, ist der Grund hierfür, dass die Website vorher für die Funktion mit dem GCM-Projekt konfiguriert war und das neue Projekt mit FCM erstellt wurde. Die generierten Tokens, die den Browser angeben, werden vom Chrome-Browser im Cache gespeichert.

**Benutzeraktion**: Sie können dieses Problem durch Entfernen der Cookies und Zurücksetzen der Berechtigungen des Browsers lösen. Hierfür wären Berechtigungen für die Aktivierung von Push Notifications erforderlich. 


### Service workers are not supported in this browser

**Erläuterung**: Das als Teil von `BMSPushSDK.js` eingeschlossene SDK, das den Servicebearbeiter verwendet, ist nicht verfügbar. 

**Benutzeraktion**: Es wird empfohlen, einen Browser zu verwenden, der den Servicebearbeiter unterstützt. Die unterstützten Browserversionen sind Firefox ab Version 49 und Chrome ab Version 53 (64-Bit).


### SecurityError: The operation is insecure

**Erläuterung**: Dieser Fehler wird gegebenenfalls beim Aktivieren der Webkonsole in Firefox ausgegeben. Die Unterstützung für Web-Push-Benachrichtigungen im Push-Benachrichtigungsservice setzt voraus, dass die Website über das `https`-Protokoll aufgerufen wird und nicht über das `http`-Protokoll.

**Benutzeraktion**: Es wird empfohlen, beim Herstellen der Verbindung zu der Website das `https`-Protokoll im Browser anzugeben.

