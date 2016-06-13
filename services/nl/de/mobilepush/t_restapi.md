---

copyright:
 years: 2015, 2016

---

# REST-APIs verwenden
{: #push-api-rest}

Sie können eine REST-API (REST = Representational State Transfer; API = Application Program Interface) für Push-Benachrichtigungen verwenden. Sie können auch das Software Development Kit (SDK) und die [Push-API](https://mobile.{DomainName}/imfpushrestapidocs/) verwenden, um Ihre Clientanwendungen weiter zu entwickeln.



- Geräteregistrierungen
- Registrierungen
- Nachrichten
- Subskriptionen
- Tags

Gehen Sie wie folgt vor, um die Basis-URL für die REST-API abzurufen:

1. Erstellen Sie eine Back-End-Anwendung im Abschnitt 'Boilerplates' des Bluemix®-Katalogs, mit der der Push-Service automatisch an diese Anwendung gebunden wird. Wenn Sie bereits eine Back-End-App erstellt haben, stellen Sie sicher, dass Sie die App an Push Notifications Service binden. 

1. Navigieren Sie auf der Hauptseite des Bluemix-Dashboards zum Bereich **Anwendungen** und klicken Sie auf Ihre App.

3. Klicken Sie auf 'Mobile Optionen'. Die Werte für die Route und für die App-GUID werden oben auf der Detailseite für Ihre App angezeigt.



## Sprachenheader akzeptieren
{: #push-api-rest-accept}

Der Header für das Akzeptieren der Sprache gibt an, welche Sprache für die Fehlernachrichten zu verwenden sind, die die Ausgabe der [Push-REST-API](https://mobile.{DomainName}/imfpushrestapidocs/){: new_window} bilden. Folgende Sprachen werden für die Fehlernachrichten unterstützt: vereinfachtes Chinesisch, traditionelles Chinesisch, Englisch (US), Deutsch, Französisch, Italienisch, Japanisch, Koreanisch, Portugiesisch und Spanisch.

## appSecret
{: #push-api-rest-secret}

Wenn eine Anwendung an Push Notifications gebunden wird, generiert der Service einen eindeutigen Schlüssel (appSecret) und übergibt ihn an den Antwortheader. Wenn Sie die REST-API von IBM® Push Notifications for Bluemix verwenden, finden Sie in der REST-API-Referenz Informationen dazu, welche APIs Sie schützen müssen. Informationen zur REST-API finden Sie in der REST-API-Referenz.

Der Antwortheader muss 'appSecret' enthalten. Andernfalls gibt der Server den Fehlercode 401 ('Unauthorized Error') zurück. Wenn die Push-Benachrichtigung einer Anwendung hinzugefügt wird, wird eine bestimmte App-ID erstellt. Als Teil der Antwort erhalten Sie einen Header mit der Bezeichnung 'appSecret', der zum Erstellen von Tags oder zum Senden von Nachrichten verwendet wird. Die Operation wird über Services im Katalog oder in der Boilerplate ausgeführt.

Gehen Sie wie folgt vor, um den Wert 'appSecret' abzurufen:

1. Klicken Sie auf den *App-Namen*, der an den Push-Service gebunden ist.
2. Klicken Sie auf den Link **Berechtigungsnachweise anzeigen**, um 'appSecret' (App-ID) anzuzeigen.

In der Anzeige **Berechtigungsnachweise anzeigen** werden Informationen zu 'AppSecret' angezeigt:

```
{
 "imfpush_Dev": [
   {
     "name": "testapp1",
     "label": "imfpush_Dev",
     "plan": "Basic",
     "credentials": {
       "url": "http://imfpush.ng.bluemix.net/imfpush/v1/apps/b615b280-b37e-4042-8815-38a758f234e2",
       "admin_url": "//mobile.ng.bluemix.net/imfpushdashboard/?appGuid=b615b280-b37e-4042-8815-38a758f234e2",
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04"  
       }
   }
 ]
}
``` 

##Filter für Push-REST-APIs
{: #push-api-rest-filters}

In Filtern wird ein Suchkriterium definiert, das Daten beschränkt, die von einer GET-API durch Push zurückgegeben werden. Wenden Sie die Filter auf das Ergebnis der Abrufoperation (Get) an, die Sie filtern möchten. Der Filter beschränkt die Anzahl der Einträge, die in das Ergebnis eingeschlossen werden. Sie können beispielsweise einen Filter verwenden, um einen Tag zu suchen, dessen Name mit 'test' beginnt. Sie können einen Filter unter Verwendung der folgenden Syntax generieren.

**name**
Der Name des Feldes, auf das der Filter angewendet wird.

**operator**
Entweder == (Exakte Übereinstimmung) oder =@ (Enthält Teilzeichenfolge); dadurch wird die zu verwendende Filterübereinstimmung beschrieben.

**expression**
Die Werte, die in das Ergebnis einzuschließen sind.

Wenn ein Komma und ein Backslash in einem Ausdruck (expression) angezeigt werden, muss der Backslash mit Escapezeichen verwendet werden.

Bei der Verwendung mehrerer Filter können diese mithilfe der Logik AND und OR kombiniert werden.\

- Verwenden Sie bei der Logik AND mehrere Filter in der Abfrage.
- Verwenden Sie bei der Logik OR innerhalb des Filterausdrucks ein Komma (,).
- Bei Verwendung beider Logiken (AND und OR) kann eine einzelne Abfrage beide Logiken aufweisen. Jeder Filter wird jedoch einzeln ausgewertet, bevor eine Kombination der Filter im Ausdruck AND erfolgt.

Für die GET-API des Geräts werden folgende Kombinationen unterstützt:
-Der Name ist das Feld 'platform'.
- Der Operator (außer für 'platform') kann == oder =@ lauten.
- Für 'platform' muss der Operator == lauten. Wird der Operator =@ verwendet, kann es sich bei dem Wert um eine Teilzeichenfolge handeln.
- Wenn == verwendet wird, muss es sich bei dem Wert um eine Zeichenfolge handeln, die genau übereinstimmt.

Für die GET-API der Subskription werden folgende Kombinationen unterstützt:

- Bei dem Namen kann es sich um das Feld 'tagName' oder das Feld 'deviceId' handeln.
- Der Operator (außer für 'platform') kann == oder =@ lauten.
- Für 'platform' muss der Operator == lauten.
- Wird der Operator =@ verwendet, kann es sich bei dem Wert um eine Teilzeichenfolge handeln. Wenn der Operator == verwendet wird, muss es sich bei dem Wert um eine Zeichenfolge handeln, die genau übereinstimmt.
- Für die GET-API des Tags werden folgende Kombinationen unterstützt:
- Der Name kann das Feld 'name' oder 'description' sein.
- Wird der Operator =@ verwendet, kann es sich bei dem Wert um eine Teilzeichenfolge handeln.
- Wenn == verwendet wird, muss es sich bei dem Wert um eine Zeichenfolge handeln, die genau übereinstimmt.
