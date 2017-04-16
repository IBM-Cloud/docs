---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Fehlernachrichten für den Service {{site.data.keyword.mobilepushshort}}
{: #errors}
Letzte Aktualisierung: 13. Februar 2017
{: .last-updated}


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

## FPWSE0001E
{: #error_fpwse0001e}

**Erläuterung**: Die Ressource, die Sie versuchen abzurufen, z. B. einen Tag oder eine Subskription, ist auf dem Server nicht verfügbar.

**Benutzeraktion**: Erstellen Sie die Ressource, die in der Nachricht aufgeführt wurde. Sie können alternativ die richtige ID für die Abfrage der Ressource bereitstellen.


## FPWSE0002E
{: #error_fpwse0002e}

**Erläuterung**: Die Ressource, die Sie zu erstellen versuchen, ist auf dem Server bereits verfügbar. Bei der Ressource kann es sich um einen Tag, eine Subskription usw. handeln.

**Benutzeraktion**: Erstellen Sie die Ressource mit einer anderen ID.


## FPWSE0003E
{: #error_fpwse0003e}

**Erläuterung**: Die vorausgesetzte Konfiguration für den {{site.data.keyword.mobilepushshort}}-Service ist unvollständig. Sie versuchen möglicherweise, APNs-Berechtigungsnachweise abzurufen, bevor sie konfiguriert sind.

**Benutzeraktion**: Stellen Sie sicher, dass der {{site.data.keyword.mobilepushshort}}-Service mit gültigen Sicherheitszertifikaten für APNs konfiguriert wurde. Weitere Informationen finden Sie im Abschnitt [Berechtigungsnachweise für APNs konfigurieren ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](t_push_provider_ios.html){: new_window}.


## FPWSE0004E
{: #error_fpwse0004e}

**Erläuterung**: Der in der Anforderung enthaltene JSON-Hauptteil ist nicht gültig.


**Benutzeraktion**: Stellen Sie sicher, dass Sie in der Anforderung eine gültige JSON-Syntax verwenden.



## FPWSE0005E
{: #error_fpwse0005e}

**Erläuterung**: Die Anforderung an den {{site.data.keyword.mobilepushshort}}-Server ist falsch oder unvollständig, da der JSON-Hauptteil nicht die Eigenschaftswerte enthält, die für die Ausführung der API-Anforderung erforderlich sind. So ist beispielsweise ein Kennwort nicht gültig oder ein Gerätetoken fehlt.


**Benutzeraktion**: Lesen Sie die Nachricht, um zu erfahren, welcher Eigenschaftswert fehlt oder nicht gültig ist, und geben Sie dann die erforderlichen Informationen an.



## FPWSE0006E
{: #error_fpwse0006e}

**Erläuterung**: Der JSON-Hauptteil der Anforderung weist Parameter auf, die vom {{site.data.keyword.mobilepushshort}}-Server nicht interpretiert werden können.


**Benutzeraktion**: Stellen Sie sicher, dass für den JSON-Hauptteil in der Anforderung das Format der Anforderung beachtet wird, das der {{site.data.keyword.mobilepushshort}}-Server erwartet. Weitere Informationen finden Sie im Abschnitt [REST-APIs ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobile.{DomainName}/imfpush/){: new_window}.



## FPWSE0007E 
{: #error_fpwse0007e}

**Erläuterung**: Die Anforderungs-URL weist eine Abfragezeichenfolge mit nicht erkannten Parametern auf. Beispiel: Wenn die Anforderung zum Löschen der Subskription andere Parameter als deviceId und tagName aufweist, kann es zu diesem Fehler kommen.


**Benutzeraktion**: Stellen Sie sicher, dass für den JSON-Hauptteil in der Anforderung das Format der Anforderung beachtet wird, das der {{site.data.keyword.mobilepushshort}}-Server erwartet. Weitere Informationen finden Sie im Abschnitt [REST-APIs ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobile.{DomainName}/imfpush/){: new_window}.



## FPWSE0008E
{: #error_fpwse0008e}

**Erläuterung**: Die Anforderungs-URL weist eine Abfragezeichenfolge mit fehlenden erforderlichen Parametern auf. Beispiel: Möglicherweise fehlen die Parameter deviceId und tagName in der Anforderung zum Löschen der Subskription.


**Benutzeraktion**: Stellen Sie sicher, dass für den JSON-Hauptteil in der Anforderung das Format der Anforderung beachtet wird, das der {{site.data.keyword.mobilepushshort}}-Server erwartet. Weitere Informationen finden Sie im Abschnitt [REST-APIs ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobile.{DomainName}/imfpush/){: new_window}.



## FPWSE0009E
{: #error_fpwse0009e}

**Erläuterung**: Es wurde versucht, Benachrichtigungen zu senden, doch bei der Anwendung sind keine Geräte registriert.

**Benutzeraktion**: Stellen Sie sicher, dass Geräte bei der Anwendung registriert wurden, bevor versucht wird, Benachrichtigungen zu senden.



## FPWSE0010E
{: #error_fpwse0010e}

**Erläuterung**: Die an den Server übergebene Anforderung führte zu einer Ausnahmebedingung. Eine der folgenden Bedingungen hat diesen Fehler möglicherweise verursacht:

- Ein von {{site.data.keyword.mobilepushshort}} genutztes internes Subsystem antwortet nicht.
- Die Anforderung führte zu einer Fehlerbedingung, die von {{site.data.keyword.mobilepushshort}} möglicherweise nicht verarbeitet werden kann.
- Für den Service {{site.data.keyword.mobilepushshort}} ist die Bearbeitung durch einen Administrator erforderlich.

**Benutzeraktion**: Wiederholen Sie die Anforderung. Wenn das Problem bestehen bleibt, wenden Sie sich an den IBM Software Support.



## FPWSE0011E
{: #error_fpwse0011e}

**Erläuterung**: Die Subskription für den Tag ist auf dem Server bereits vorhanden. Ein Beispiel wäre die Erstellung einer Subskription, die bereits existiert.

**Benutzeraktion**: Erstellen Sie eine Subskription mit einem eindeutigen Tagnamen.



## FPWSE0012E
{: #error_fpwse0012e}

**Erläuterung**: Die Subskription für den Tag ist auf dem Server nicht vorhanden. Dieser Fehler tritt auf, wenn eine Anforderung zum Abrufen oder Löschen einer nicht vorhandenen Subskription übergeben wird.


**Benutzeraktion**: Verwenden Sie in der Anforderung den richtigen Tagnamen und die richtige Geräte-ID.



## FPWSE0013E
{: #error_fpwse0013e}

**Erläuterung**: Die in der Anforderung enthaltenen JSON-Nutzdaten sind nicht gültig.


**Benutzeraktion**: Stellen Sie sicher, dass die JSON-Nutzdaten gültig sind.


## FPWSE0025E
{: #error_fpwse0025e}

**Erläuterung**: Der Server kann die Anforderung momentan nicht verarbeiten.

**Benutzeraktion**: Reichen Sie die Anforderung zu einem späteren Zeitpunkt erneut ein.


## FPWSE1007E 
{: #error_fpwse1007e}

**Erläuterung**: Der {{site.data.keyword.mobilepushshort}}-Service wurde für diese Anwendung inaktiviert. Dies kann aus abrechnungstechnischen Gründen geschehen oder die App wurde vom Administrator inaktiviert.


**Benutzeraktion**: Zum Überprüfen des Servicestatus, zum Abrufen von Fehlerbehebungsinformationen oder für Informationen zum Anfordern von Hilfe ziehen Sie die Themen zur Fehlerbehebung in der Bluemix-Dokumentation zurate.



## FPWSE1079E
{: #error_fpwse1079e}

**Erläuterung**: Der für die Abfrageoperation angegebene Offsetwert ist nicht gültig.

**Benutzeraktion**: Stellen Sie sicher, dass der Offsetwert größer-gleich null ist.



## FPWSE1080E 
{: #error_fpwse1080e}

**Erläuterung**: Der für die Abfrageoperation angegebene Größenwert ist nicht gültig.

**Benutzeraktion**: Stellen Sie sicher, dass der Größenwert über null liegt.



