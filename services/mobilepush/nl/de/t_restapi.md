---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# REST-APIs verwenden
{: #push-api-rest}
Letzte Aktualisierung: 16. Januar 2017
{: .last-updated}

Sie können eine REST-API (REST = Representational State Transfer; API = Application Program Interface) für Push-Benachrichtigungen verwenden. Sie können auch das SDK und die [Push-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobile.{DomainName}/imfpush/){: new_window} verwenden, um Ihre Clientanwendungen weiter zu entwickeln.

Mit der Push-REST-API können Back-End-Serveranwendungen und -Clients auf Funktionen für Push-Benachrichtigungen zugreifen.

- Geräteregistrierungen
- Registrierungen
- Nachrichten
- Subskriptionen
- Tags
- Webhooks

Führen Sie die folgenden Schritte aus, um die Basis-URL für die REST-API abzurufen:

1. Erstellen Sie im Bluemix®-Katalog im Abschnitt 'Boilerplates' eine Back-End-Anwendung. Wählen Sie dazu 'MobileFirst Services Starter' aus. Hierdurch wird der {{site.data.keyword.mobilepushshort}}-Service an die Anwendung gebunden. Sie können auch eine Serviceinstanz von Push erstellen und diese ungebunden lassen. 
1. Navigieren Sie auf der Hauptseite des Bluemix-Dashboards zum Bereich **Anwendungen** und wählen Sie dort Ihre App aus.
3. Klicken Sie auf **Mobile Systemerweiterungen**. Die Werte für die Route und für die App-GUID werden am Anfang der Detailseite für Ihre App angezeigt. In der Anzeige 'Berechtigungsnachweise anzeigen' werden Informationen über 'AppSecret' angezeigt. Für manche APIs können Sie den geheimen Anwendungsschlüssel sowie den geheimen Clientschlüssel über 'Mobile Systemerweiterungen' abrufen.

Sie können auch die Befehlszeile verwenden, um die Serviceberechtigungsnachweise abzurufen:

```
    cf create-service-key {push_instance_name} {key_name}

 cf service-key {push_instance_name} {key_name}
```
	{: codeblock}

## Sprachenheader akzeptieren
{: #push-api-rest-accept}

Der Header für das Akzeptieren der Sprache ("Accept-Language") gibt an, welche Sprache für die Fehlernachrichten verwendet werden soll, die die Ausgabe der [Push-REST-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobile.{DomainName}/imfpush/){: new_window} bilden. Folgende Sprachen werden für die Fehlernachrichten unterstützt: vereinfachtes Chinesisch, traditionelles Chinesisch, Englisch (US), Deutsch, Französisch, Italienisch, Japanisch, Koreanisch, Portugiesisch und Spanisch.

## appSecret 
{: #push-api-rest-secret}

Beim Binden einer Anwendung an {{site.data.keyword.mobilepushshort}} generiert der Service den eindeutigen Schlüssel 'appSecret' und übergibt diesen mit dem Antwortheader. Wenn Sie die REST-API von IBM {{site.data.keyword.mobilepushshort}} for Bluemix verwenden, finden Sie in der Referenz für die REST-API Informationen dazu, welche APIs geschützt werden müssen. Weitere Informationen finden Sie in der [Push-REST-API ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://mobile.{DomainName}/imfpush/){: new_window}.

Der Anforderungsheader muss 'appSecret' enthalten. Andernfalls gibt der Server den Fehlercode 401 ('Unauthorized Error') zurück. Beim Hinzufügen von {{site.data.keyword.mobilepushshort}} zu einer Anwendung wird eine spezifische App-ID erstellt. Sie erhalten als Teil der Antwort einen Header mit dem Namen 'appSecret', der für die Erstellung von Tags oder das Senden von Nachrichten verwendet wird. Diese Operation erfolgt über Services im Katalog oder in der Boilerplate.

Gehen Sie wie folgt vor, um den Wert 'appSecret' abzurufen:

1. Klicken Sie auf den *App-Namen*, der an den Push-Service gebunden ist.
2. Klicken Sie auf den Link **Berechtigungsnachweise anzeigen**, um 'appSecret' (App-ID) anzuzeigen.

In der Anzeige **Berechtigungsnachweise anzeigen** werden Informationen zu 'appSecret' angezeigt:
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
       "appSecret": "8dac71a5-2219-42b3-a9f3-dbb828ba1f04",
       }
     }
    ]
    }
```
	{: codeblock} 


##Filter für Push-REST-APIs
{: #push-api-rest-filters}

Anhand von Filtern wird ein Suchkriterium definiert, mit dem der Umfang der Daten beschränkt wird, die von einer GET-API von {{site.data.keyword.mobilepushshort}} zurückgegeben werden. Wenden Sie die Filter auf das Ergebnis der Abrufoperation (Get) an, die Sie filtern möchten. Der Filter beschränkt die Anzahl der Einträge im Ergebnis. Sie können beispielsweise einen Filter verwenden, um Tags zu suchen, deren Name mit 'test' beginnt. 

Filter können unter Verwendung der folgenden Syntax generiert werden:

**name**: Der Name des Felds, auf das der Filter angewendet wird.

**operator**: Entweder == (Exakte Übereinstimmung) oder =@ (Enthält Teilzeichenfolge); dadurch wird die zu verwendende Filterübereinstimmung beschrieben.

**expression**: Die Werte, die in das Ergebnis einzuschließen sind.

Wenn ein Komma und ein Backslash in einem Ausdruck (expression) angezeigt werden, muss der Backslash mit Escapezeichen verwendet werden.

Bei der Verwendung mehrerer Filter können diese mithilfe der Logik AND bzw. OR miteinander kombiniert werden.

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


##{{site.data.keyword.mobilepushshort}} - Antwortcodes
{: #push-api-response-codes}

Status: 405 Method Not Allowed - Es wird die passende Methode erwartet.
