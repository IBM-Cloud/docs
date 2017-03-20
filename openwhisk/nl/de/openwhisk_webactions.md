---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-27"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Webaktionen (Experimentell)
{: #openwhisk_webactions}

Webaktionen sind OpenWhisk-Aktionen mit Annotationen, durch die Sie schnell webbasierte Anwendungen erstellen können. Dies bietet Ihnen die Möglichkeit, Back-End-Logik zu programmieren, auf die Ihre Webanwendung anonym zugreifen kann, ohne einen OpenWhisk-Authentifizierungsschlüssel zu benötigen. Es liegt in der Zuständigkeit des Aktionsentwicklers, die gewünschte Authentifizierung und Autorisierung (d. h. den OAuth-Ablauf) zu implementieren.
{: shortdesc}

Aktivierungen von Webaktionen werden dem Benutzer zugeordnet, der die Aktion erstellt hat. Bei diesen Aktionen werden also die Kosten einer Aktionsaktivierung vom Aufrufer auf den Eigner der Aktion verlagert. 

**Hinweis:** Bei dieser Funktion handelt es sich derzeit um ein experimentelles Angebot, mit dem Benutzer die Möglichkeit erhalten, die Funktion früh auszuprobieren und Feedback dazu zu geben.

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

Die Annotation `web-export` bietet die Möglichkeit, die Aktion als Webaktion über eine neue REST-Schnittstelle verfügbar zu machen. Die URL ist wie folgt strukturiert: `https://{APIHOST}/api/v1/experimental/web/{QUALIFIED ACTION NAME}.{EXT}`. Der vollständig qualifizierte Name einer Aktion besteht aus drei Teilen: Namensbereich, Paketname und Aktionsname. Ein Beispiel ist `guest/demo/hello`. Der letzte Teil des URI wird als `Erweiterung` bezeichnet und ist in der Regel `.http`, obwohl auch andere Werte zulässig sind, wie später erläutert wird. Der API-Pfad für die Webaktion kann mit `curl` oder `wget` ohne API-Schlüssel verwendet werden. Er kann sogar direkt in den Browser eingegeben werden.

Probieren Sie den API-Pfad [https://${APIHOST}/api/v1/experimental/web/guest/demo/hello.http?name=Jane](https://${APIHOST}/api/v1/experimental/web/guest/demo/hello.http?name=Jane) in Ihrem Web-Browser aus. Oder versuchen Sie, die Aktion über `curl` aufzurufen:
```
curl https://openwhisk.{DomainName}/api/v1/experimental/web/guest/demo/hello.http?name=Jane
```
{: pre}
Das folgende Beispiel zeigt eine Webaktion, die eine HTTP-Umleitung durchführt:
```javascript
function main() {
  return { 
    headers: { "location": "http://openwhisk.org" }, 
    code: 302 
  }
}
```
{: codeblock}

Ein Cookie könnte wie folgt festgelegt werden:
```javascript
function main() {
  return { 
    headers: { 
      "Set-Cookie": "UserID=Jane; Max-Age=3600; Version=",
      "Content-Type": "text/html"  
    }, 
    code: 200, 
    body: "<html><body><h3>hello</h3></body></html" }
}
```
{: codeblock}

Oder es könnte `image/png` zurückgegeben werden:
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             code: 200,
             body: png };
}
```
{: codeblock}

Oder `application/json`:
```javascript
function main(params) {
    return {
        'code': 200,
        'headers':{'Content-Type':'application/json'},
        'body' : new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}

Es ist wichtig, die [Antwortgrößenbegrenzung](./openwhisk_reference.html) für Aktionen zu beachten, da eine Antwort, die die vordefinierten Systembegrenzungen überschreitet, fehlschlägt. Große Objekte sollten nicht inline über OpenWhisk gesendet werden, sondern zum Beispiel in einen Objektspeicher verlagert werden.

## HTTP-Anforderungen mit Aktionen verarbeiten
{: #openwhisk_webactions_http}

Eine OpenWhisk-Aktion, die keine Webaktion ist, erfordert eine Authentifizierung und muss mit einem JSON-Objekt antworten. Im Gegensatz dazu können Webaktionen ohne Authentifizierung aufgerufen werden und lassen sich dazu verwenden, HTTP-Handler zu implementieren, die mit verschiedenartigen Inhalten für die Elemente *headers*, *status code* und *body* antworten. Die Webaktion muss weiterhin ein JSON-Objekt zurückgeben, jedoch behandelt das OpenWhisk-System (d. h. der `Controller`) eine Webaktion anders, wenn das Ergebnis eines oder mehrere der folgenden Elemente als JSON-Eigenschaften der höchsten Ebene enthält:

- `headers`: Ein JSON-Objekt, in dem die Schlüssel Headernamen (header-names) und die Werte Zeichenfolgewerte für diese Header sind (Standardwert: keine Header).
- `code`: Ein gültiger HTTP-Statuscode (Standardwert: 200 OK).
- `body`: Eine Zeichenfolge im Klartext oder in Base64-Codierung (für Binärdaten).

Der Controller gibt die durch die Aktion angegebenen Header, sofern vorhanden, an den HTTP-Client weiter, wenn die Anforderung/Antwort-Operation beendet wird. Ganz ähnlich antwortet der Controller auch mit einem angegebenen Statuscode, wenn dieser vorhanden ist. Zuletzt wird das Body-Element als Hauptteil der Antwort übergeben. Wenn kein Inhaltstypheader (`content-type header`) in den Headern (`headers`) des Aktionsergebnisses deklariert ist, wird der Hauptteil so übergeben, als wäre er eine Zeichenfolge (was einen Fehler verursacht, wenn er dies nicht ist). Wenn der Inhaltstyp (`content-type`) definiert ist, ermittelt der Controller, ob die Antwort aus Binärdaten oder Klartext besteht, und dekodiert die Zeichenfolge bei Bedarf mit einem Base64-Dekoder. Lässt sich der Hauptteil nicht ordnungsgemäß dekodieren, wird ein Fehler an den Aufrufenden zurückgegeben.

*Hinweis:* Ein JSON-Objekt oder -Array wird wie Binärdaten behandelt und muss in Base64-Codierung codiert sein, wie im obigen Beispiel gezeigt.

## HTTP-Kontext

Eine Webaktion empfängt beim Aufruf alle verfügbaren HTTP-Anforderungsinformationen als zusätzliche Parameter zum Aktionseingabeargument. Dabei handelt es sich um folgende Informationen:

- `__ow_meta_verb`: Die HTTP-Methode der Anforderung.
- `__ow_meta_headers`: Die Anforderungsheader.
- `__ow_meta_path`: Der unabgeglichene Pfad der Anforderung (der Abgleich wird nach Verarbeitung der Aktionserweiterung beendet).

Die Anforderung darf keinen der oben aufgeführten, mit `__ow_` benannten Parameter überschreiben. Falls dies doch geschieht, schlägt die Anforderung mit dem Status 400 "Bad Request" fehl.

## Zusätzliche Features
{: #openwhisk_webactions_extra}

Webaktionen bieten einige zusätzlichen Features wie zum Beispiel:

- `Inhaltserweiterungen:` Die Anforderung muss den gewünschten Inhaltstyp durch einen der folgenden Werte angeben: `.json`, `.html`, `.text` oder `.http`. Dies geschieht dadurch, dass dem Aktionsnamen im URI eine Erweiterung hinzugefügt wird, sodass eine Aktion `/guest/demo/hello` zum Beispiel durch `/guest/demo/hello.http` angegeben wird, um eine HTTP-Antwort zu empfangen.
- `Felder aus dem Ergebnis projizieren:` Der Pfad, der auf den Aktionsnamen folgt, wird dazu verwendet, eine oder mehrere Ebenen der Antwort herauszuprojizieren. Beispiel: `/guest/demo/hello.html/body`. Dadurch kann eine Aktion, die ein Wörterverzeichnis `{body: "..." }` zurückgibt, die Eigenschaft `body` projizieren und direkt den entsprechenden Zeichenfolgewert zurückgeben. Der projizierte Pfad folgt einem absoluten Pfadmodell (wie in XPath).
- `Abfrage- und Hauptteilparameter als Eingabe:` Die Aktion empfängt Abfrageparameter und Parameter im Anforderungshauptteil. Die Rangordnung für das Zusammenfügen von Parametern sieht wie folgt aus: Paketparameter, Aktionsparameter, Abfrageparameter und Hauptteilparameter, wobei jeder dieser Parameter vorherige Werte überschreibt, wenn diese sich überschneiden. Beispiel: Der Parameter `/guest/demo/hello.http?name=Jane` übergibt das Argument `{name: "Jane"}` an die Aktion. 
- `Formulardaten:` Neben den Standarddaten vom Typ `application/json` können Webaktionen als Eingabe URL-codierte Daten vom Typ `application/x-www-form-urlencoded data` empfangen.
- `Aktivierung durch mehrere HTTP-Verben:` Eine Webaktion kann durch eine von vier HTTP-Methoden aufgerufen werden: `GET`, `POST`, `PUT` oder `DELETE`.


Im nachfolgenden Beispiel wird skizziert, wie Sie diese Features in einer Webaktion nutzen könnten. Gegeben sei eine Aktion `/guest/demo/hello` mit dem folgenden Hauptteil:
```javascript
function main(params) { 
    return { 'response': params};
}
```
{: codeblock}

Ein Aufruf der Aktion mit dem Abfrageparametername `name` und der Erweiterung `.json` zur Angabe einer JSON-Antwort, die das Feld `/response` projiziert, liefert die folgende HTTP-Antwort:
```
curl https://openwhisk.{DomainName}/api/v1/experimental/web/guest/demo/hello.json/response?name=Jane
```
{: pre}
```json
{
    "name": "Jane",
    "__ow_meta_verb": "get",
    "__ow_meta_headers": {
        "accept": "*/*",
        "user-agent": "curl/7.51.0"
    },
    "__ow_meta_path": "/response"
}
```

## Inhaltserweiterungen
{: #openwhisk_webactions_extensions}

Für den Aufruf einer Webaktion ist eine Inhaltserweiterung erforderlich. Die Erweiterungen `.json` und `.http` erfordern keinen Projektionspfad. Für die Erweiterungen `.text` und `.html` ist dies der Fall, jedoch wird aus Benutzerkomfortgründen standardmäßig angenommen, dass der Pfad dem Erweiterungsnamen entspricht. Um also eine Webaktion aufzurufen und eine `.html`-Antwort zu empfangen, muss die Aktion mit einem JSON-Objekt antworten, das eine Eigenschaft auf höchster Ebene mit dem Namen `html` enthält (oder der Antworttyp muss im explizit angegebenen Pfad enthalten sein). Dies heißt mit anderen Worten, dass die Angabe `/guest/demo/hello.html` zum Beispiel zur Angabe `/guest/demo/hello.html/html`, in der die Eigenschaft `html` explizit projiziert wird, äquivalent ist. Der vollständig qualifizierte Name der Aktion muss den entsprechenden Paketnamen enthalten, der `default` lautet, wenn die Aktion nicht in einem benannten Paket enthalten ist.


## Geschützte Parameter
{: #openwhisk_webactions_protected}

Aktionsparameter können auch geschützt und als unveränderlich behandelt werden. Um Parameter endgültig festzulegen und eine Aktion über das Web zugänglich zu machen, müssen zwei [Annotationen](/openwhisk_annotations.html) an die Aktion angehängt werden: `final` und `web-export`. Beide Annotationen müssen mit dem Wert `true` angegeben werden, damit sie wirksam sind. Bei Verwendung der vorherigen Aktionsbereitstellung werden die Annotationen wie folgt hinzugefügt:

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

Zum Inaktivieren einer Webaktion, sodass sie nicht mehr über die neue API (`https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/experimental/web/`) aufgerufen wird, genügt es, die Annotation zu entfernen oder auf `false` zu setzen.

```
wsk action update /guest/demo/hello hello.js \
      --annotation web-export false
```
{: pre}     

## Fehlerbehandlung
{: #openwhisk_webactions_errors}

Wenn eine OpenWhisk-Aktion fehlschlägt, gibt zwei verschiedene Fehlermodi. Der erste wird als *Anwendungsfehler* bezeichnet und entspricht in etwa einer abgefangenen Ausnahmebedingung: Die Aktion gibt ein JSON-Objekt zurück, das eine Eigenschaft `error` auf höchster Ebene enthält. Der zweite Modus ist ein *Entwicklerfehler*, der auftritt, wenn die Aktion einen sehr schwerwiegenden Fehler verursacht und keine Antwort zurückgibt (ähnlich wie bei einer nicht abgefangenen Ausnahmebedingung). Bei Webaktionen behandelt der Controller Anwendungsfehler wie folgt:

- Jede angegebene Pfadprojektion wird ignoriert und der Controller projiziert stattdessen die Eigenschaft `error`.
- Der Controller wendet die Inhaltsbehandlung, die durch die Aktionserweiterung impliziert wird, auf den Wert der Eigenschaft `error` an.

Entwickler müssen sich im Klaren darüber sein, wie Webaktionen möglicherweise verwendet werden, und entsprechende Fehlerantworten generieren. Beispielsweise sollte eine Webaktion, die mit der Erweiterung `.http` verwendet wird, eine HTTP-Antwort zurückgeben, wie zum Beispiel `{error: { code: 400 }`. Wenn dies nicht so gehandhabt wird, entsteht eine Diskrepanz zwischen dem durch die Erweiterung implizierten Inhaltstyp und dem Aktionsinhaltstyp in der Fehlerantwort. Eine besondere Aufmerksamkeit erfordern Webaktionen, die Sequenzen sind, damit Komponenten, die eine Sequenz bilden, bei Bedarf adäquate Fehlernachrichten generieren können.
