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
Letzte Aktualisierung: 12. April 2017
{: .last-updated}

Dieser Abschnitt enthält eine Anleitung zum Identifizieren und Beheben häufig auftretender Fehlerszenarios, die bei der Verwendung des Push Notifications-Service auftreten können.

## Häufig auftretende Push Notification-Probleme beheben
{: #troubleshooting_notification_errors}

### Internal server error occurred. Please contact admin. (Internal error code: PUSHD102E)
{: #troubleshooting_notification_internal}

**Erläuterung**: Dieser Fehler kann auftreten, wenn Sie eine Push-Instanz vor November 2015 erstellt haben.  

**Benutzeraktion**: Um das Problem zu lösen, müssen Sie die Push-Instanz löschen und eine neue erstellen. Beachten Sie, dass Ihre Tags nicht beibehalten werden, wenn Sie die Push-Instanz löschen.


### UnauthorizedRegistration
{: #troubleshooting_notification_unauth}

**Erläuterung**: Chrome Web Push funktioniert mit FCM-Schlüsseln (Firebase Cloud Messaging) nicht. Wenn Sie nach dem Umzug von FCM auf GCM unter Chrome keine Web-Push-Benachrichtigung erhalten, ist der Grund hierfür, dass die Website vorher für die Funktion mit dem GCM-Projekt konfiguriert war und das neue Projekt mit FCM erstellt wurde. Die generierten Tokens, die den Browser angeben, werden vom Chrome-Browser im Cache gespeichert.

**Benutzeraktion**: Sie können dieses Problem durch Entfernen der Cookies und Zurücksetzen der Berechtigungen des Browsers lösen. Hierfür wären Berechtigungen für die Aktivierung von Push Notifications erforderlich. 


### Service workers are not supported in this browser
{: #troubleshooting_notification_service_workers}

**Erläuterung**: Das als Teil von `BMSPushSDK.js` eingeschlossene SDK, das den Servicebearbeiter verwendet, ist nicht verfügbar. 

**Benutzeraktion**: Es wird empfohlen, einen Browser zu verwenden, der den Servicebearbeiter unterstützt. Die unterstützten Browserversionen sind Firefox ab Version 49 und Chrome ab Version 53 (64-Bit).


### SecurityError: The operation is insecure
{: #troubleshooting_notification_insecure}

**Erläuterung**: Dieser Fehler wird gegebenenfalls beim Aktivieren der Webkonsole in Firefox ausgegeben. Die Unterstützung für Web-Push-Benachrichtigungen im Push-Benachrichtigungsservice setzt voraus, dass die Website über das `https`-Protokoll aufgerufen wird und nicht über das `http`-Protokoll.

**Benutzeraktion**: Es wird empfohlen, beim Herstellen der Verbindung zu der Website das `https`-Protokoll im Browser anzugeben.


## Fehler in der Web-Push-Konfiguration beheben
{: #troubleshooting_configuration_errors}

Sie können Fehler im Zusammenhang mit der Web-Push-Konfiguration diagnostizieren, indem Sie die Datei `BMSPushSDK.js` analysieren. Diese Datei enthält Informationen zum Fehler.  

Das folgende Codebeispiel veranschaulicht das Analysieren eines Fehlers im Callback:

```
function showStatus(response) {
 if(response.statusCode == 200 || response.statusCode == 201) {
   		document.getElementById("status").innerHTML = "Response is " + response.response;
   	}
   	else if(response.statusCode == 0) {
  		if(response.response) {
  			document.getElementById("status").innerHTML = response.response;	
    		}
    		else {
    			document.getElementById("status").innerHTML = "There is a possible CORS or access issue while attempting the request.";	
   		}   		
   	}
   	else {
   		document.getElementById("status").innerHTML = "Response is " + response.response + " with the error " 
		+ response.error + " and the status code " + response.statusCode;
   	}
 	}
```
	{: codeblock}


- Wenn `applicationId` nicht ordnungsgemäß konfiguriert ist, schlägt die ursprüngliche Anforderung an den {{site.data.keyword.mobilepushshort}}-Service fehl, da 'statusCode' auf Null (0) gesetzt wird.
- Der Statuscode 200 oder 201 bezeichnet eine erfolgreiche Antwort.
- Wenn `clientSecret` ungültig ist, wird für 'statusCode' ein Antwortcode 401 festgelegt. Das Element `response.reponse` enthält eine Beschreibung des Fehlers.


## Fehlernachrichten des Push Notifications-Service beheben
{: #troubleshooting_service_errors}

Als Antwort auf REST-API-Anforderungen werden die folgenden {{site.data.keyword.mobilepushshort}}-Fehlernachrichten zurückgegeben.

Beispiele für Fehlerantworten:
```
	{
		"message": "Missing APNs credentials",
     "docUrl": "https://www.ng.bluemix.net/docs/troubleshoot/errors/mobilepush/index.html#FPWSE0003E",
     "code":   "FPWSE0003E"
	}
```
		    {: codeblock}

Weitere Informationen zu einem Fehler finden Sie in der Dokumentation zu dem jeweiligen Fehlercode.

### FPWSE0001E
{: #error_fpwse0001e}

**Erläuterung**: Die Ressource, die Sie versuchen abzurufen, z. B. einen Tag oder eine Subskription, ist auf dem Server nicht verfügbar.

**Benutzeraktion**: Erstellen Sie die Ressource, die in der Nachricht aufgeführt wurde. Sie können alternativ die richtige ID für die Abfrage der Ressource bereitstellen.


### FPWSE0002E
{: #error_fpwse0002e}

**Erläuterung**: Die Ressource, die Sie zu erstellen versuchen, ist auf dem Server bereits verfügbar. Bei der Ressource kann es sich um einen Tag, eine Subskription usw. handeln.

**Benutzeraktion**: Erstellen Sie die Ressource mit einer anderen ID.


### FPWSE0003E
{: #error_fpwse0003e}

**Erläuterung**: Die vorausgesetzte Konfiguration für den {{site.data.keyword.mobilepushshort}}-Service ist unvollständig. Sie versuchen möglicherweise, APNs-Berechtigungsnachweise abzurufen, bevor sie konfiguriert sind.

**Benutzeraktion**: Stellen Sie sicher, dass der {{site.data.keyword.mobilepushshort}}-Service mit gültigen Sicherheitszertifikaten für APNs konfiguriert wurde. Weitere Informationen finden Sie in [Berechtigungsnachweise für einen Benachrichtigungsprovider konfigurieren![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](t__main_push_config_provider.html){: new_window}.


### FPWSE0004E
{: #error_fpwse0004e}

**Erläuterung**: Der in der Anforderung enthaltene JSON-Hauptteil ist nicht gültig.


**Benutzeraktion**: Stellen Sie sicher, dass Sie in der Anforderung eine gültige JSON-Syntax verwenden.



### FPWSE0005E
{: #error_fpwse0005e}

**Erläuterung**: Die Anforderung an den {{site.data.keyword.mobilepushshort}}-Server ist falsch oder unvollständig, da der JSON-Hauptteil nicht die Eigenschaftswerte enthält, die für die Ausführung der API-Anforderung erforderlich sind. So ist beispielsweise ein Kennwort nicht gültig oder ein Gerätetoken fehlt.


**Benutzeraktion**: Lesen Sie die Nachricht, um zu erfahren, welcher Eigenschaftswert fehlt oder nicht gültig ist, und geben Sie dann die erforderlichen Informationen an.



### FPWSE0006E
{: #error_fpwse0006e}

**Erläuterung**: Der JSON-Hauptteil der Anforderung weist Parameter auf, die vom {{site.data.keyword.mobilepushshort}}-Server nicht interpretiert werden können.


**Benutzeraktion**: Stellen Sie sicher, dass für den JSON-Hauptteil in der Anforderung das Format der Anforderung beachtet wird, das der {{site.data.keyword.mobilepushshort}}-Server erwartet. Weitere Informationen finden Sie im Abschnitt [REST-APIs ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0007E 
{: #error_fpwse0007e}

**Erläuterung**: Die Anforderungs-URL weist eine Abfragezeichenfolge mit nicht erkannten Parametern auf. Beispiel: Wenn die Anforderung zum Löschen der Subskription andere Parameter als deviceId und tagName aufweist, kann es zu diesem Fehler kommen.


**Benutzeraktion**: Stellen Sie sicher, dass für den JSON-Hauptteil in der Anforderung das Format der Anforderung beachtet wird, das der {{site.data.keyword.mobilepushshort}}-Server erwartet. Weitere Informationen finden Sie im Abschnitt [REST-APIs ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0008E
{: #error_fpwse0008e}

**Erläuterung**: Die Anforderungs-URL weist eine Abfragezeichenfolge mit fehlenden erforderlichen Parametern auf. Beispiel: Möglicherweise fehlen die Parameter deviceId und tagName in der Anforderung zum Löschen der Subskription.


**Benutzeraktion**: Stellen Sie sicher, dass für den JSON-Hauptteil in der Anforderung das Format der Anforderung beachtet wird, das der {{site.data.keyword.mobilepushshort}}-Server erwartet. Weitere Informationen finden Sie im Abschnitt [REST-APIs ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobile.{DomainName}/imfpush/){: new_window}.



### FPWSE0009E
{: #error_fpwse0009e}

**Erläuterung**: Es wurde versucht, Benachrichtigungen zu senden, doch bei der Anwendung sind keine Geräte registriert.

**Benutzeraktion**: Stellen Sie sicher, dass Geräte bei der Anwendung registriert wurden, bevor versucht wird, Benachrichtigungen zu senden.



### FPWSE0010E
{: #error_fpwse0010e}

**Erläuterung**: Die an den Server übergebene Anforderung führte zu einer Ausnahmebedingung. Eine der folgenden Bedingungen hat diesen Fehler möglicherweise verursacht:

- Ein von {{site.data.keyword.mobilepushshort}} genutztes internes Subsystem antwortet nicht.
- Die Anforderung führte zu einer Fehlerbedingung, die von {{site.data.keyword.mobilepushshort}} möglicherweise nicht verarbeitet werden kann.
- Für den Service {{site.data.keyword.mobilepushshort}} ist die Bearbeitung durch einen Administrator erforderlich.

**Benutzeraktion**: Wiederholen Sie die Anforderung. Wenn das Problem bestehen bleibt, wenden Sie sich an den IBM Software Support.



### FPWSE0011E
{: #error_fpwse0011e}

**Erläuterung**: Die Subskription für den Tag ist auf dem Server bereits vorhanden. Ein Beispiel wäre die Erstellung einer Subskription, die bereits existiert.

**Benutzeraktion**: Erstellen Sie eine Subskription mit einem eindeutigen Tagnamen.



### FPWSE0012E
{: #error_fpwse0012e}

**Erläuterung**: Die Subskription für den Tag ist auf dem Server nicht vorhanden. Dieser Fehler tritt auf, wenn eine Anforderung zum Abrufen oder Löschen einer nicht vorhandenen Subskription übergeben wird.


**Benutzeraktion**: Verwenden Sie in der Anforderung den richtigen Tagnamen und die richtige Geräte-ID.



### FPWSE0013E
{: #error_fpwse0013e}

**Erläuterung**: Die in der Anforderung enthaltenen JSON-Nutzdaten sind nicht gültig.


**Benutzeraktion**: Stellen Sie sicher, dass die JSON-Nutzdaten gültig sind.


### FPWSE0025E
{: #error_fpwse0025e}

**Erläuterung**: Der Server kann die Anforderung momentan nicht verarbeiten.

**Benutzeraktion**: Reichen Sie die Anforderung zu einem späteren Zeitpunkt erneut ein.


### FPWSE1007E 
{: #error_fpwse1007e}

**Erläuterung**: Der {{site.data.keyword.mobilepushshort}}-Service wurde für diese Anwendung inaktiviert. Dies kann aus abrechnungstechnischen Gründen geschehen oder die App wurde vom Administrator inaktiviert.


**Benutzeraktion**: Zum Überprüfen des Servicestatus, zum Abrufen von Fehlerbehebungsinformationen oder für Informationen zum Anfordern von Hilfe ziehen Sie die Themen zur Fehlerbehebung in der Bluemix-Dokumentation zurate.



### FPWSE1079E
{: #error_fpwse1079e}

**Erläuterung**: Der für die Abfrageoperation angegebene Offsetwert ist nicht gültig.

**Benutzeraktion**: Stellen Sie sicher, dass der Offsetwert größer-gleich null ist.



### FPWSE1080E 
{: #error_fpwse1080e}

**Erläuterung**: Der für die Abfrageoperation angegebene Größenwert ist nicht gültig.

**Benutzeraktion**: Stellen Sie sicher, dass der Größenwert über null liegt.


