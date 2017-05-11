---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-26"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# API-Gateway
{: #openwhisk_apigateway}

OpenWhisk-Aktionen können von der Verwaltung durch das API-Management profitieren. 

Das API-Gateway fungiert als Proxy für [Webaktionen](webactions.md) und stattet diese mit zusätzlichen Funktionen aus, zu denen zum Beispiel die folgenden gehören: HTTP-Methodenrouting, Client-IDs/geheime Client-Schlüssel, Ratenbegrenzung, CORS, Anzeigen der API-Nutzung und der Antwortprotokolle und Definition von Richtlinien zur gemeinsamen Nutzung von APIs.
Weitere Informationen zur API-Gatewayfunktion finden Sie in der [Dokumentation zum API-Management](/docs/apis/management/manage_openwhisk_apis.html#manage_openwhisk_apis). 

## APIs aus OpenWhisk-Webaktionen im Browser erstellen

Mithilfe des API-Gateways können Sie eine OpenWhisk-Aktion als API verfügbar machen. Wenn Sie die API definiert haben, können Sie Sicherheits- und Ratenbegrenzungsrichtlinien anwenden, die API-Nutzung und Antwortprotokolle anzeigen und Richtlinien zur gemeinsamen Nutzung der API definieren.
Klicken Sie im OpenWhisk-Dashboard auf die Registerkarte [APIs](https://console.ng.bluemix.net/openwhisk/apimanagement). 


## APIs aus OpenWhisk-Webaktionen über die Befehlszeilenschnittstelle (CLI) erstellen

### Konfiguration der OpenWhisk-CLI

Konfigurieren Sie die OpenWhisk-CLI mit dem API-Host mit dem Befehl `wsk property set --apihost openwhisk.ng.bluemix.net`.
Um den CLI-Befehl `wsk api` verwenden zu können, muss die Datei `~/.wskprops` das Bluemix-Zugriffstoken enthalten.
Zum Abrufen des Zugriffstokens verwenden Sie den CLI-Befehl `wsk bluemix login`. Weitere Informationen zu dem Befehl können Sie durch den Befehl `wsk bluemix login -h` anzeigen. 

**Hinweis:** Wenn der Befehl fehlschlägt, weil für ihn Single Sign-on (SSO) erforderlich ist, wird diese Ausführung gegenwärtig nicht unterstützt. Als Ausweichlösung können Sie sich über die Cloud Foundry-CLI mit dem Befehl `cf login` anmelden und das Zugriffstoken aus der Konfigurationsdatei `~/.cf/config.json` im Ausgangsverzeichnis in die Datei `~/.wskprops` als Eigenschaft `APIGW_ACCESS_TOKEN="Wert des Zugriffstokens"` kopieren. Entfernen Sie beim Kopieren des Zugriffstokens das Präfix `Bearer`. 

**Hinweis:** Die APIs, die Sie mit dem Befehl `wsk api-experimental` erstellt haben, werden für einen Zeitraum noch weiter funktionieren. Sie sollten jedoch damit beginnen, Ihre APIs in Webaktionen zu migrieren und Ihre vorhandenen APIs mithilfe des neuen CLI-Befehls `wsk api` neu zu konfigurieren. 

### Erste API über die CLI erstellen

1. Erstellen Sie eine JavaScript-Datei mit dem folgenden Inhalt. Für dieses Beispiel wird der Dateiname 'hello.js' verwendet.
  ```javascript
  function main({name:name='Serverless API'}) {
      return {payload: `Hello world ${name}`};
  }
  ```
  {: codeblock}
  
2. Erstellen Sie wie folgt eine Webaktion aus der JavaScript-Funktion. Für dieses Beispiel heißt die Aktion 'hello'. Stellen Sie sicher, dass Sie das Flag `--web true` hinzufügen. 
  
  ```
  wsk action create hello hello.js --web true
  ```
  {: pre}
  ```
  ok: created action hello
  ```
  
3. Erstellen Sie eine API mit dem Basispfad `/hello` und dem Pfad `/world` sowie mit der Methode `get` und dem Antworttyp `json`. 
  
  ```
  wsk api create /hello /world get hello --response-type json
  ```
  ```
  ok: created API /hello/world GET for action /_/hello
  https://${APIHOST}:9001/api/21ef035/hello/world
  ```
  Eine neue URL wird generiert, über die die Aktion `hello` mit der HTTP-Methode **GET** verfügbar gemacht wird.
  
4. Senden Sie nun testweise eine HTTP-Anforderung an die URL. 
  
  ```
  $ curl https://${APIHOST}:9001/api/21ef035/hello/world?name=OpenWhisk
  ```
  ```json
{
  "payload": "Hello world OpenWhisk"
  }
  ```
  Die Webaktion `hello` wurde aufgerufen und hat ein JSON-Objekt zurückgegeben, das den Parameter `name` enthält, der durch einen Abfrageparameter gesendet wurde. Sie können Parameter durch einfache Abfrageparameter oder im Anforderungshauptteil übergeben. Über Webaktionen können Sie eine Aktion auf öffentlichem Wege ohne den API-Schlüssel für die OpenWhisk-Berechtigung aufrufen.
  
### Vollständige Kontrolle über die HTTP-Antwort
  
  Das Flag `--response-type` steuert die Ziel-URL der Webaktion, sodass sie durch das API-Gateway als Proxy geleitet wird. Bei Verwendung des Flags `--response-type json` wie im obigen Beispiel wird das vollständige Ergebnis der Aktion im JSON-Format zurückgegeben und der Inhaltstyp (Content-Type) des Headers automatisch auf `application/json` gesetzt. Dies ermöglicht Ihnen einen einfachen Einstieg.  
  
  Nach dem Einstieg in die Arbeit mit Webaktionen möchten Sie wahrscheinlich vollständige Kontrolle über die Eigenschaften von HTTP-Antworten wie `statusCode` oder `headers` haben und verschiedene Inhaltstypen im Hauptteil (`body`) zurückgeben. Zu diesem Zweck können Sie das Flag `--response-type http` verwenden, das die Ziel-URL der Webaktion mit der Erweiterung `http` konfiguriert. 

  Sie haben die Möglichkeit, den Code der Aktion so zu ändern, dass er mit der Rückgabe von Webaktionen mit der Erweiterung `http` konform ist, oder Sie können die Aktion in eine Sequenz einfügen, indem Sie das Ergebnis der Aktion an eine neue Aktion übergeben, die es in das ordnungsgemäße Format für eine HTTP-Antwort umsetzt. Weitere Informationen zu Antworttypen und Erweiterungen von Webaktionen finden Sie in der Dokumentation zu [Webaktionen](webactions.md). 

  Ändern Sie den Code für `hello.js`, sodass er die JSON-Eigenschaften `body`, `statusCode` und `headers` zurückgibt. 
  ```javascript
  function main({name:name='Serverless API'}) {
      return {
        body: new Buffer(JSON.stringify({payload:`Hello world ${name}`})).toString('base64'), 
        statusCode:200, 
        headers:{ 'Content-Type': 'application/json'}
      };
  }
  ```
  {: codeblock}
  Beachten Sie, dass der Hauptteil 'body' in `base64` codiert und nicht als Zeichenfolge ('string') zurückgegeben werden muss.
  
  Aktualisieren Sie die Aktion mit dem geänderten Ergebnis. 
  ```
  wsk action update hello hello.js --web true
  ```
  {: pre}
  Aktualisieren Sie die API mit dem Flag `--response-type http`.
  ```
  wsk api create /hello /world get hello --response-type http
  ```
  {: pre}
  Rufen Sie die aktualisierte API testweise auf.
  ```
  curl https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/hello/world
  ```
  {: pre}
  ```json
  {
  "payload": "Hello world Serverless API"
  }
  ```
  Sie haben nun die vollständige Kontrolle über Ihre APIs und können den Inhalt steuern, um zum Beispiel HTML zurückzugeben oder den Statuscode für bestimmte Situationen wie 'Nicht gefunden' (404) oder 'Nicht berechtigt' (401) oder sogar 'Interner Fehler' (500) festzulegen.

### Mehrere Webaktionen verfügbar machen

Nehmen Sie an, Sie möchten eine Reihe von Aktionen für einen Buchclub für Freunde verfügbar machen.
Mit den folgenden Aktionen können das Back-End für den Buchclub implementieren: 

| Aktion | HTTP-Methode | Beschreibung |
| ----------- | ----------- | ------------ |
| getBooks    | GET | Abrufen von Buchdetails  |
| postBooks   | POST | Hinzufügen eines Buches |
| putBooks    | PUT | Aktualisieren von Buchdetails |
| deleteBooks | DELETE | Löschen eines Buches |

Erstellen Sie nun eine API für den Buchclub mit dem Namen `Book Club` und HTTP-URL-Basispfad `/club` und `books` als zugehöriger Ressource. 
```
wsk api create -n "Book Club" /club /books get getBooks --response-type http
wsk api create /club /books post postBooks              --response-type http
wsk api create /club /books put putBooks                --response-type http
wsk api create /club /books delete deleteBooks          --response-type http
```

Beachten Sie, dass die erste mit dem Basispfad `/club` verfügbar gemachte Aktion die API-Bezeichnung mit dem Namen `Book Club` erhält. Alle weiteren unter `/club` verfügbar gemachten Aktionen werden `Book Club` zugeordnet. 

Listen Sie nun alle im vorherigen Beispiel verfügbar gemachten Aktionen auf. 

```
wsk api list -f
```
```
ok: APIs
Action: getBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: get
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: postBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: post
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: putBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: put
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: deleteBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: delete
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

Fügen Sie jetzt nur zum Spaß ein neues Buch mit dem Titel `JavaScript: The Good Parts` mit der HTTP-Methode **POST** hinzu. 
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": "success"
}
```

Anschließend rufen Sie eine Liste der Bücher mit der Aktion `getBooks` über die HTTP-Methode **GET** ab. 
```
curl -X GET https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### Konfiguration exportieren
Exportieren Sie die API `Book Club` in eine Datei, die als Basis zum erneuten Erstellen der APIs mit einer Datei als Eingabe verwendet werden kann.  
```
wsk api get "Book Club" > club-swagger.json
```

Testen Sie die Swagger-Datei, indem Sie zuerst alle verfügbar gemachten URLs unter einem gemeinsamen Basispfad löschen.
Sie können alle verfügbar gemachten URLs entweder über den Basispfad `/club` oder über die API-Namensbezeichnung `Book Club` löschen: 
```
wsk api delete /club
```
```
ok: deleted API /club
```
### Konfiguration ändern

Sie können die Konfiguration im OpenWhisk-Dashboard bearbeiten. Klicken Sie dazu auf die Registerkarte [APIs](https://console.ng.bluemix.net/openwhisk/apimanagement), um die Sicherheit, die Ratenbegrenzung und andere Eigenschaften festzulegen. 

### Konfiguration importieren

Stellen Sie jetzt die API `Book Club` mithilfe der Datei `club-swagger.json` wieder her. 
```
wsk api create --config-file club-swagger.json
```
```
ok: created api /books delete for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books get for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books post for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books put for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

Sie können überprüfen, ob die API erneut erstellt wurde. 
```
wsk api list /club
```
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
postBooks                 post         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
putBooks                   put         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
deleteBooks             delete         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
