---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# API-Gateway (experimentell)
{: #openwhisk_apigateway}

[Webaktionen](openwhisk_webactions.html) werden freigegeben, damit sie allgemein verfügbar sind.

Mittels Webaktionen können Sie eine Aktion mit anderen HTTP-Methoden als POST und ohne den Berechtigungs-API-Schlüssel der Aktion aufrufen.

Aufgrund des Benutzerfeedbacks wurde für den Build von OpenWhisk-Aktionen, die zur Behandlung von HTTP-Ereignissen geeignet sind, das Programmiermodell mit Webaktionen gewählt.

Ein Großteil der API-Gateway-Funktionalität wurde in Webaktionen zusammengefasst. Webaktionen ermöglichen Ihnen die Behandlung jedweder HTTP-Anforderungen und die Rückgabe von HTTP-Antworten aus der Webaktion heraus, wobei Sie jederzeit die vollständige Kontrolle behalten.

Eine überarbeitete API-Gateway-Integration für OpenWhisk wird in Kürze verfügbar sein. Sie wird so konfiguriert sein, dass Ihre Webaktionen von ihr weitergeleitet und hierbei mit API-Gateway-Funktionen wie beispielsweise Ratenbegrenzung, OAuth-Tokenvalidierung, API-Schlüsseln und anderem ausgestattet werden. Schauen Sie sich das Video zur [Erstellung und Steuerung von APIs](https://youtu.be/XT9KwWTnnzo) an. 

**Hinweis:** Die APIs, die Sie mit `wsk api-experimental` erstellt haben, können weiterhin verwendet werden. Sie sollten jedoch Ihre APIs nach und nach in Webaktionen migrieren.

## Konfiguration der OpenWhisk-CLI
{: #openwhisk_apigateway_cli}
Diese experimentelle Funktion funktioniert nur mit dem neuen OpenWhisk-Authentifizierungsmodell. Dabei besitzt jeder Namensbereich nun einen eindeutigen zugeordneten Authentifizierungsschlüssel.
Befolgen Sie die Anweisungen unter [CLI konfigurieren](https://console.ng.bluemix.net/openwhisk/cli), um zu erfahren, wie der Authentifizierungsschlüssel für Ihren jeweiligen Namensbereich festgelegt wird.

## OpenWhisk-Aktionen verfügbar machen
{: #openwhisk_apigateway_hello}

Mit dem folgenden Befehl wird eine einfache Aktion verfügbar gemacht, die bereits mit OpenWhisk vorinstalliert wurde.

```
wsk api-experimental create /hello /echo get /whisk.system/utils/echo
```
{: pre}
```
ok: created api /echo GET for action /whisk.system/utils/echo
https://21ef035.api-gw.mybluemix.net/hello/echo
```
{: screen}
Beim Verfügbarmachen der Aktion `echo` über die HTTP-Methode **GET** wird eine neue URL generiert.

Mit dem folgenden Befehl wird eine HTTP-Anforderung an die URL gesendet.
```
curl https://21ef035.api-gw.mybluemix.net/hello/echo?marco=polo
```
{: pre}
Dadurch wird die Aktion `echo` aufgerufen, sodass eine JSON-Zeichenfolge mit den gesendeten Parametern zurückgegeben wird.
```
{
  "marco":"polo"
}
```
{: screen}

Sie können Parameter über einfache Abfrageparameter oder einen Anforderungshauptteil an die Aktion übergeben.

### Mehrere Aktionen verfügbar machen
{: #openwhisk_apigateway_actions}

Mit dem folgenden Befehl soll eine Gruppe von Aktionen für einen Buchklub für Ihre Freunde verfügbar gemacht werden.
Mit den folgenden Aktionen können das Back-End für den Buchklub implementieren:

| Aktion | HTTP-Methode | Beschreibung |
| ----------- | ----------- | ------------ |
| getBooks    | GET | Zum Abrufen von Buchdetails  |
| postBooks   | POST | Zum Hinzufügen eines Buches |
| putBooks    | PUT | Zum Aktualisieren von Buchdetails |
| deleteBooks | DELETE | Zum Löschen eines Buches |

Mit dem folgenden Befehl wird eine API für den Buchklub mit dem Namen `Book Club` erstellt. `/club` ist dabei der HTTP-URL-Basispfad und `books` die zugehörige Ressource.
```
wsk api-experimental create -n "Book Club" /club /books get getBooks
wsk api-experimental create /club /books post postBooks
wsk api-experimental create /club /books put putBooks
wsk api-experimental create /club /books delete deleteBooks
```
{: pre}

Beachten Sie, dass die erste mit dem Basispfad `/club` verfügbar gemachte Aktion die API-Bezeichnung mit dem Namen `Book Club` abruft. Andere unter `/club` verfügbar gemachte Aktionen werden `Book Club` zugeordnet.

Mit dem folgenden Befehl werden alle im vorherigen Beispiel verfügbar gemachten Aktionen aufgelistet.

```
wsk api-experimental list
```
{: pre}
```
ok: apis
Action                   Verb          API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

Mit dem folgenden Befehl wird das neue Buch `JavaScript: The Good Parts` mit der HTTP-Methode **POST** hinzugefügt.
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": "success"
}
```
{: screen}

Mit dem folgenden Befehl wird eine Liste der Bücher mit der Aktion `getBooks` über die HTTP-Methode **GET** abgerufen.
```
curl -X GET https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### Konfiguration exportieren
Mit dem folgenden Befehl wird die API `Book Club` in eine Datei exportiert, die als Basis zum erneuten Erstellen der APIs mit einer Datei als Eingabe verwendet werden kann. 
```
wsk api-experimental get "Book Club" > club-swagger.json
```
{: pre}

Mit dem folgenden Befehl wird die Swagger-Datei getestet, indem zuerst alle verfügbar gemachten URLs unter einem gemeinsamen Basispfad gelöscht werden.
Sie können alle verfügbar gemachten URLs entweder mit dem Basispfad `/club` oder mit der API-Namensbezeichnung `Book Club` löschen:
```
wsk api-experimental delete /club
```
{: pre}
```
ok: deleted API /club
```
{: screen}

Mit dem folgenden Befehl wird die API `Book Club` mit der Datei `club-swagger.json` wiederhergestellt.
```
wsk api-experimental create --config-file club-swagger.json
```
{: pre}
```
ok: created api /books delete for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books get for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books post for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books put for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

Mit dem folgenden Befehl wird überprüft, ob die API erneut erstellt wurde.
```
wsk api-experimental list /club
```
{: pre}
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

- **Hinweis:** Bei dieser Funktion handelt es sich derzeit um ein experimentelles Angebot, mit dem Benutzer die Möglichkeit erhalten, die Funktion früh auszuprobieren und Feedback dazu zu geben. Das folgende Feedback ist bereits eingegangen:
  - Keine Möglichkeit, die HTTP-Zugriffssteuerung für CORS (Cross-Origin Resource Sharing) anzupassen. Derzeit sind die generierten API-Antwortheader so konfiguriert, dass jeder HTTP-Wert für 'verb' oder 'origin' möglich ist (d. h. *). Die folgenden Header werden immer zurückgegeben:
    - Access-Control-Allow-Origin: *
    - Access-Control-Allow-Headers: Authorization, Content-Type
    - Access-Control-Allow-Methods: GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS
  - Für Anforderungen und Antworten wird nur der Inhaltstyp `application/json` unterstützt.
  - Es gibt keine programmierte Möglichkeit, die Antwort über die OpenWhisk-Aktion zu steuern.
  - Alle OpenWhisk-Aktionen werden über öffentlichen Zugriff verfügbar gemacht. Es gibt keine Möglichkeit, einen angepassten API-Schlüssel zu konfigurieren.
  - Pfadparameter werden nicht unterstützt, sondern nur Abfrageparameter und Anforderungshauptteile.
  - Wenn die API ohne API-Name erstellt wird, ergibt sich der Name aus dem Basispfad und kann nicht geändert werden.
  - Wenn APIs über eine Eingabedatei erneut erstellt werden sollen, müssen die APIs zunächst gelöscht werden.
  - Beim Exportieren von APIs, die Ihren OpenWhisk-API-Schlüssel enthalten, sind diese Informationen vertraulich und die Erstellung anhand einer Vorlage ist nicht verfügbar.
