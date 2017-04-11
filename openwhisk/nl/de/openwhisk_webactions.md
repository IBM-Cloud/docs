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

# Webaktionen
{: #openwhisk_webactions}

Webaktionen sind OpenWhisk-Aktionen mit Annotationen, durch die Sie schnell webbasierte Anwendungen erstellen können. Dies bietet Ihnen die Möglichkeit, Back-End-Logik zu programmieren, auf die Ihre Webanwendung anonym zugreifen kann, ohne einen OpenWhisk-Authentifizierungsschlüssel zu benötigen. Es liegt in der Zuständigkeit des Aktionsentwicklers, die gewünschte Authentifizierung und Autorisierung (d. h. den OAuth-Ablauf) zu implementieren.
{: shortdesc}

Aktivierungen von Webaktionen werden dem Benutzer zugeordnet, der die Aktion erstellt hat. Bei diesen Aktionen werden also die Kosten einer Aktionsaktivierung vom Aufrufer auf den Eigner der Aktion verlagert.

Betrachten Sie zum Beispiel die folgende JavaScript-Aktion `hello.js`:
```javascript
function main({name}) {
  var msg = 'you did not tell me who you are.';
  if (name) {
    msg = `hello ${name}!`
  }
  return {body: `<html><body><h3>${msg}</h3></body></html>`}
}
```
{: codeblock}

Sie können nun eine *Webaktion* `hello` im Paket `demo` für den Namensbereich `guest` mithilfe der Annotation `web-export` erstellen:
```
wsk package create demo
```
{: pre}
```
wsk action create /guest/demo/hello hello.js -a web-export true
```
{: pre}

Die Annotation `web-export` bietet die Möglichkeit, die Aktion als Webaktion über eine neue REST-Schnittstelle verfügbar zu machen. Die URL ist wie folgt strukturiert: `https://openwhisk.ng.bluemix.net/api/v1/web/{QUALIFIZIERTER_AKTIONSNAME}.{EXT}`. Der vollständig qualifizierte Name einer Aktion besteht aus drei Teilen: Namensbereich, Paketname und Aktionsname.

*Der vollständig qualifizierte Name der Aktion muss den entsprechenden Paketnamen enthalten, der 'default' lautet, wenn die Aktion nicht in einem benannten Paket enthalten ist.*

Ein Beispiel ist `guest/demo/hello`. Der letzte Teil des URI wird als `Erweiterung` bezeichnet und ist in der Regel `.http`, obwohl auch andere Werte zulässig sind, wie später erläutert wird. Der API-Pfad für die Webaktion kann mit `curl` oder `wget` ohne API-Schlüssel verwendet werden. Er kann sogar direkt in den Browser eingegeben werden.

Probieren Sie den API-Pfad [https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane](https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane) in Ihrem Web-Browser aus. Oder versuchen Sie, die Aktion über `curl` aufzurufen:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.http?name=Jane
```
{: pre}

Das folgende Beispiel zeigt eine Webaktion, die eine HTTP-Umleitung durchführt:
```javascript
function main() {
  return { 
    headers: { location: 'http://openwhisk.org' },
    statusCode: 302
  }
}
```
{: codeblock}  

Ein Cookie könnte wie folgt festgelegt werden:
```javascript
function main() {
  return { 
    headers: { 
      'Set-Cookie': 'UserID=Jane; Max-Age=3600; Version=',
      'Content-Type': 'text/html'
    }, 
    statusCode: 200,
    body: '<html><body><h3>hello</h3></body></html>' }
}
```
{: codeblock}

Oder es könnte `image/png` zurückgegeben werden:
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             statusCode: 200,
             body: png };
}
```
{: codeblock}

Or returns `application/json`:
```javascript
function main(params) { 
    return {
        statusCode: 200,
        headers: { 'Content-Type': 'application/json' },
        body: new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}

Es ist wichtig, die [Antwortgrößenbegrenzung](./openwhisk_reference.html) für Aktionen zu beachten, da eine Antwort, die die vordefinierten Systembegrenzungen überschreitet, fehlschlägt. Große Objekte sollten nicht inline über OpenWhisk gesendet werden, sondern zum Beispiel in einen Objektspeicher verlagert werden.

## HTTP-Anforderungen mit Aktionen verarbeiten
{: #openwhisk_webactions_http}

Eine OpenWhisk-Aktion, die keine Webaktion ist, erfordert eine Authentifizierung und muss mit einem JSON-Objekt antworten. Im Gegensatz dazu können Webaktionen ohne Authentifizierung aufgerufen werden und lassen sich dazu verwenden, HTTP-Handler zu implementieren, die mit verschiedenartigen Inhalten für die Elemente *headers*, *statusCode code* und *body* antworten. Die Webaktion muss weiterhin ein JSON-Objekt zurückgeben, jedoch behandelt das OpenWhisk-System (d. h. der `Controller`) eine Webaktion anders, wenn das Ergebnis eines oder mehrere der folgenden Elemente als JSON-Eigenschaften der höchsten Ebene enthält:

- `headers`: Ein JSON-Objekt, in dem die Schlüssel Headernamen (header-names) und die Werte Zeichenfolgewerte für diese Header sind (Standardwert: keine Header).
- `statusCode`: Ein gültiger HTTP-Statuscode (Standardwert: 200 OK).
- `body`: Eine Zeichenfolge im Klartext oder in Base64-Codierung (für Binärdaten).

Der Controller gibt die durch die Aktion angegebenen Header, sofern vorhanden, an den HTTP-Client weiter, wenn die Anforderung/Antwort-Operation beendet wird. Ganz ähnlich antwortet der Controller auch mit einem angegebenen Statuscode, wenn dieser vorhanden ist. Zuletzt wird das Body-Element als Hauptteil der Antwort übergeben. Wenn kein Inhaltstypheader (`content-type header`) in den Headern (`headers`) des Aktionsergebnisses deklariert ist, wird der Hauptteil so übergeben, als wäre er eine Zeichenfolge (was einen Fehler verursacht, wenn er dies nicht ist). Wenn der Inhaltstyp (`content-type`) definiert ist, ermittelt der Controller, ob die Antwort aus Binärdaten oder Klartext besteht, und dekodiert die Zeichenfolge bei Bedarf mit einem Base64-Dekoder. Lässt sich der Hauptteil nicht ordnungsgemäß dekodieren, wird ein Fehler an den Aufrufenden zurückgegeben.

*Hinweis:* Ein JSON-Objekt oder -Array wird wie Binärdaten behandelt und muss in Base64-Codierung codiert sein, wie im obigen Beispiel gezeigt.

## HTTP-Kontext

Alle Webaktionen empfangen beim Aufruf zusätzliche HTTP-Anforderungsinformationen als Parameter für das Aktionseingabeargument. Dabei handelt es sich um folgende Informationen:

- `__ow_method` (Typ: Zeichenfolge): Die HTTP-Methode der Anforderung. 
- `__ow_headers` (Typ: Zuordnung von Zeichenfolge zu Zeichenfolge): Die Anforderungsheader. 
- `__ow_path` (Typ: Zeichenfolge): Der unabgeglichene Pfad der Anforderung (der Abgleich wird nach Verarbeitung der Aktionserweiterung beendet). 
- `__ow_user` (Typ: Zeichenfolge): Der Namensbereich, der das für OpenWhisk authentifizierte Subjekt kennzeichnet. 
- `__ow_body` (Typ: Zeichenfolge): Die Anforderungshauptteilentität als Zeichenfolge in Base64-Codierung, wenn der Inhalt binär ist, oder andernfalls als normale Zeichenfolge.
- `__ow_query` (Typ: Zeichenfolge): Die Abfrageparameter aus der Anforderung als nicht analysierte Zeichenfolge. 

Eine Anforderung darf keinen der oben aufgeführten, mit `__ow_` benannten Parameter überschreiben. Falls dies doch geschieht, schlägt die Anforderung mit dem Status 400 "Bad Request" fehl.

Die Eigenschaft `__ow_user` ist nur vorhanden, wenn die Webaktion eine [Annotation für eine erforderliche Authentifizierung](./openwhisk_annotations.html#openwhisk_annotations_webactions) besitzt, und ermöglicht einer Webaktion die Implementierung ihrer eigenen Berechtigungsrichtlinie. Die Eigenschaft `__ow_query` ist nur dann verfügbar, wenn eine Webaktion die Verarbeitung der ['unaufbereiteten' HTTP-Anforderung](#raw-http-handling) wählt. Es handelt sich um eine Zeichenfolge, die die aus der URI analysierten Abfrageparameter (getrennt durch `&`) enthält. Die Eigenschaft `__ow_body` ist vorhanden, wenn entweder 'unaufbereitete' HTTP-Anforderungen verarbeitet werden oder wenn die HTTP-Anforderungsentität kein JSON-Objekt oder keine Formulardaten darstellt. Webaktionen empfangen andernfalls Abfrage- und Hauptteilparameter als Eigenschaften der ersten Klasse in den Aktionsargumenten. Hierbei haben Hauptteilparameter Vorrang vor Abfrageparametern, die wiederum Vorrang vor Aktions- und Paketparametern haben.

## Zusätzliche Features

Webaktionen bieten einige zusätzlichen Features wie zum Beispiel:

- `Inhaltserweiterungen:` Die Anforderung muss den gewünschten Inhaltstyp durch einen der folgenden Werte angeben: `.json`, `.html`, `.http`, `.svg` oder `.text`. Dies geschieht dadurch, dass dem Aktionsnamen im URI eine Erweiterung hinzugefügt wird, sodass eine Aktion `/guest/demo/hello` zum Beispiel durch `/guest/demo/hello.http` angegeben wird, um eine HTTP-Antwort zu empfangen. Wenn keine Erweiterung erkannt wird, wird der Einfachheit halber die Erweiterung `.http` angenommen. 
- `Felder aus dem Ergebnis projizieren:` Der Pfad, der auf den Aktionsnamen folgt, wird dazu verwendet, eine oder mehrere Ebenen der Antwort herauszuprojizieren. Beispiel: `/guest/demo/hello.html/body`. Dadurch kann eine Aktion, die ein Wörterverzeichnis `{body: "..." }` zurückgibt, die Eigenschaft `body` projizieren und direkt den entsprechenden Zeichenfolgewert zurückgeben. Der projizierte Pfad folgt einem absoluten Pfadmodell (wie in XPath).
- `Abfrage- und Hauptteilparameter als Eingabe:` Die Aktion empfängt Abfrageparameter und Parameter im Anforderungshauptteil. Die Rangordnung für das Zusammenfügen von Parametern sieht wie folgt aus: Paketparameter, Aktionsparameter, Abfrageparameter und Hauptteilparameter, wobei jeder dieser Parameter vorherige Werte überschreibt, wenn diese sich überschneiden. Beispiel: Der Parameter `/guest/demo/hello.http?name=Jane` übergibt das Argument `{name: "Jane"}` an die Aktion.
- `Formulardaten:` Neben den Standarddaten vom Typ `application/json` können Webaktionen als Eingabe URL-codierte Daten vom Typ `application/x-www-form-urlencoded data` empfangen.
- `Aktivierung durch mehrere HTTP-Verben:` Eine Webaktion kann durch eine der folgenden HTTP-Methoden aufgerufen werden: `GET`, `POST`, `PUT` `PATCH` und `DELETE` sowie `HEAD` und `OPTIONS`.
- `Verarbeitung von Nicht-JSON-Hauptteil und unaufbereiteter HTTP-Entität`: Eine Webaktion kann einen HTTP-Anforderungshauptteil akzeptieren, der kein JSON-Objekt ist, und auswählen, dass derartige Werte immer als nicht transparente Werte zu empfangen sind (einfacher Text, falls nicht binär, oder andernfalls Zeichenfolge in Base64-Codierung). 

Im nachfolgenden Beispiel wird skizziert, wie Sie diese Features in einer Webaktion nutzen könnten. Gegeben sei eine Aktion `/guest/demo/hello` mit dem folgenden Hauptteil:
```javascript
function main(params) { 
    return { response: params };
}
```

Wenn diese Aktion als Webaktion aufgerufen wird, können Sie die Antwort der Webaktion ändern, indem Sie unterschiedliche Pfade aus dem Ergebnis projizieren.
Im Folgenden wird beispielsweise das gesamte Objekt zurückgegeben und es kann festgestellt werden, welche Argumente die Aktion empfängt: 

```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json
```
{: pre}
```json
{
  "response": {
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

Mit einem Abfrageparameter: 
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

Oder Formulardaten: 
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -d "name":"Jane"
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "10",      
      "content-type": "application/x-www-form-urlencoded",      
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

Oder einem JSON-Objekt:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: application/json' -d '{"name":"Jane"}'
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",      
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

Ausschließlich zur Projektion des Namens (als Text): 
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.text/response/name?name=Jane
```
{: pre}
```
Jane
```

Aus den obigen Beispielen geht hervor, dass Abfrageparameter, Formulardaten und JSON-Objekthauptteilentitäten der Einfachheit halber als Wörterverzeichnisse behandelt werden und ihre Werte direkt als Aktionseingabeeigenschaften zugänglich sind. Dies gilt nicht für Webaktionen, die stattdessen eine direktere Verarbeitung von HTTP-Anforderungsentitäten wählen, oder wenn die Webaktion eine Entität empfängt, die kein JSON-Objekt ist. 

Das folgende Beispiel zeigt die Verwendung des Inhaltstyps 'text' im Kontext des obigen Beispiels: 
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: text/plain' -d "Jane"
```
{: pre}
```json
{
  "response": {
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "4",      
      "content-type": "text/plain",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": "",
    "__ow_body": "Jane"
  }
}
```


## Inhaltserweiterungen
{: #openwhisk_webactions_extensions}

Für den Aufruf einer Webaktion ist generell eine Inhaltserweiterung erforderlich; ist keine Erweiterung vorhanden, wird standardmäßig `.http` angenommen. Die Erweiterungen `.json` und `.http` erfordern keinen Projektionspfad. Für die Erweiterungen `.html`, `.svg` und `.text` ist dies der Fall, jedoch wird aus Benutzerkomfortgründen standardmäßig angenommen, dass der Pfad dem Erweiterungsnamen entspricht. Um also eine Webaktion aufzurufen und eine `.html`-Antwort zu empfangen, muss die Aktion mit einem JSON-Objekt antworten, das eine Eigenschaft auf höchster Ebene mit dem Namen `html` enthält (oder der Antworttyp muss im explizit angegebenen Pfad enthalten sein). Dies heißt mit anderen Worten, dass die Angabe `/guest/demo/hello.html` zum Beispiel zur Angabe `/guest/demo/hello.html/html`, in der die Eigenschaft `html` explizit projiziert wird, äquivalent ist. Der vollständig qualifizierte Name der Aktion muss den entsprechenden Paketnamen enthalten, der `default` lautet, wenn die Aktion nicht in einem benannten Paket enthalten ist.


## Geschützte Parameter
{: #openwhisk_webactions_protected}

Aktionsparameter können auch geschützt und als unveränderlich behandelt werden. Um Parameter endgültig festzulegen und eine Aktion über das Web zugänglich zu machen, müssen zwei [Annotationen](openwhisk_annotations.html) an die Aktion angehängt werden: `final` und `web-export`. Beide Annotationen müssen mit dem Wert `true` angegeben werden, damit sie wirksam sind. Bei Verwendung der vorherigen Aktionsbereitstellung werden die Annotationen wie folgt hinzugefügt:

```
wsk action create /guest/demo/hello hello.js \
      --parameter name Jane \
      --annotation final true \
      --annotation web-export true
```
{: pre}

Das Ergebnis dieser Änderungen besteht darin, dass das Element `name` an `Jane` gebunden wird und wegen der Annotation 'final' nicht durch Abfrage- oder Hauptteilparameter überschrieben werden kann. Dies schützt die Aktion gegen Abfrage- oder Hauptteilparameter, die versehentlich oder absichtlich versuchen, diesen Wert zu ändern. 

## Webaktionen inaktivieren
{: #openwhisk_webactions_disable}

Zum Inaktivieren einer Webaktion, sodass sie nicht mehr über die neue API (`https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/web/`) aufgerufen wird, genügt es, die Annotation zu entfernen oder auf `false` zu setzen.

```
wsk action update /guest/demo/hello hello.js \
      --annotation web-export false
```

## Unaufbereitete HTTP-Anforderungen verarbeiten
{: #raw-http-handling}

Eine Webaktion kann vorgeben, dass ein ankommender HTTP-Hauptteil direkt interpretiert und verarbeitet wird, ohne Weiterleitung eines JSON-Objekts an Eigenschaften der ersten Klasse, die für die Aktionseingabe verfügbar sind (z. B. `args.name` statt Parsing von `args.__ow_query`). Dies erfolgt über eine [Annotation](openwhisk_annotations.html) des Typs `raw-http`. Beim obigen Beispiel wird nun eine 'unaufbereitete' HTTP-Webaktion verwendet, die `name` sowohl als Abfrageparameter als auch als JSON-Wert im HTTP-Anforderungshauptteil empfängt: 
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane -X POST -H "Content-Type: application/json" -d '{"name":"Jane"}'
```
{: pre}
```json
{
  "response": {
    "__ow_method": "post",
    "__ow_query": "name=Jane",
    "__ow_body": "eyJuYW1lIjoiSmFuZSJ9",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"      
    },
    "__ow_path": ""
  }
}
```

In diesem Fall ist zu beachten, dass der JSON-Inhalt mit Base64 codiert ist, weil er als Binärwert behandelt wird. Die Aktion muss eine Base64-Decodierung und JSON-Analyse für diesen Wert ausführen, um das JSON-Objekt wiederherzustellen. OpenWhisk verwendet das [Spray](https://github.com/spray/spray)-Framework, um [festzustellen](https://github.com/spray/spray/blob/master/spray-http/src/main/scala/spray/http/MediaType.scala#L282), welche Inhaltstypen binär und welche Typen einfacher Text sind. 


### Verarbeitung von unaufbereiteten HTTP-Anforderungen aktivieren

Webaktionen für unaufbereitete HTTP-Anforderungen werden über die [Annotation](openwhisk_annotations.html) `raw-http` mit dem Wert `true` aktiviert.

```
wsk action create /guest/demo/hello hello.js \
      --annotation web-export true
      --annotation raw-http true
```
{: pre}

**Hinweis:** Da `raw-http` `web-export` impliziert, ist eine Verbesserung der CLI geplant, damit diese Annotationen künftig einfacher hinzugefügt (und entfernt) werden können. 


### Verarbeitung von unaufbereiteten HTTP-Anforderungen inaktivieren

Die Verarbeitung von unaufbereiteten HTTP-Anforderungen wird durch das Festlegen des Wertes `false` für die [Annotation](openwhisk_annotations.html) `raw-http` inaktiviert. 

```
wsk update create /guest/demo/hello hello.js \
      --annotation web-export true
      --annotation raw-http false
```
{: pre}

**Hinweis:** Alle Annotationen für eine einzelne Aktion müssen gleichzeitig festgelegt werden, entweder bei der Erstellung oder bei der Aktualisierung der Aktion. Grund hierfür ist eine aktuelle Einschränkung für die API und die CLI. Wird dies nicht berücksichtigt, führt dies dazu, dass alle zuvor angehängten Annotationen entfernt werden. 


## Fehlerbehandlung
{: #openwhisk_webactions_errors}

Wenn eine OpenWhisk-Aktion fehlschlägt, gibt zwei verschiedene Fehlermodi. Der erste wird als *Anwendungsfehler* bezeichnet und entspricht in etwa einer abgefangenen Ausnahmebedingung: Die Aktion gibt ein JSON-Objekt zurück, das eine Eigenschaft `error` auf höchster Ebene enthält. Der zweite Modus ist ein *Entwicklerfehler*, der auftritt, wenn die Aktion einen sehr schwerwiegenden Fehler verursacht und keine Antwort zurückgibt (ähnlich wie bei einer nicht abgefangenen Ausnahmebedingung). Bei Webaktionen behandelt der Controller Anwendungsfehler wie folgt:

- Jede angegebene Pfadprojektion wird ignoriert und der Controller projiziert stattdessen die Eigenschaft `error`.
- Der Controller wendet die Inhaltsbehandlung, die durch die Aktionserweiterung impliziert wird, auf den Wert der Eigenschaft `error` an.

Entwickler müssen sich im Klaren darüber sein, wie Webaktionen möglicherweise verwendet werden, und entsprechende Fehlerantworten generieren. Beispielsweise sollte eine Webaktion, die mit der Erweiterung `.http` verwendet wird, eine HTTP-Antwort zurückgeben, wie zum Beispiel `{error: { statusCode: 400 }`. Wenn dies nicht so gehandhabt wird, entsteht eine Diskrepanz zwischen dem durch die Erweiterung implizierten Inhaltstyp und dem Aktionsinhaltstyp in der Fehlerantwort. Eine besondere Aufmerksamkeit erfordern Webaktionen, die Sequenzen sind, damit Komponenten, die eine Sequenz bilden, bei Bedarf adäquate Fehlernachrichten generieren können.

