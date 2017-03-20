---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}}-Aktionen erstellen und aufrufen
{: #openwhisk_actions}


Aktionen sind statusunabhängige Code-Snippets, die auf der {{site.data.keyword.openwhisk}}-Plattform ausgeführt werden. Eine Aktion kann als JavaScript-, Swift- oder Python-Funktion, als Java-Methode oder angepasstes ausführbares Programm in einem Docker-Container geschrieben werden. Eine Aktion kann zum Beispiel zum Erkennen der Gesichter auf einem Bild, zum Antworten auf eine Datenbankänderung, zum Aggregieren einer Gruppe von API-Aufrufen oder zum Senden eines Tweets verwendet werden.
{:shortdesc}
Aktionen können explizit aufgerufen oder als Reaktion auf ein Ereignis ausgeführt werden. In beiden Fällen führt jede Ausführung einer Aktion zu einem Aktivierungsdatensatz, der durch eine eindeutige Aktivierungs-ID identifiziert wird. Die Eingabe für eine Aktion und das Ergebnis einer Aktion bestehen jeweils in einem Wörterverzeichnis aus Schlüssel/Wert-Paaren, wobei der Schlüssel eine Zeichenfolge und der Wert ein gültiger JSON-Wert ist. Aktionen können außerdem aus Aufrufen weiterer Aktionen oder aus einer definierten Folge von Aktionen bestehen.

In den folgenden Abschnitten finden Sie Informationen dazu, wie Sie Aktionen in Ihrer bevorzugten Entwicklungsumgebung erstellen, aufrufen und debuggen:
* [JavaScript](#openwhisk_create_action_js)
* [Swift](#openwhisk_actions_swift)
* [Python](#openwhisk_actions_python)
* [Java](#openwhisk_actions_java)
* [Docker](#openwhisk_actions_docker)


## JavaScript-Aktionen erstellen und aufrufen
{: #openwhisk_create_action_js}

In den folgenden Abschnitten werden Sie in die Arbeit mit Aktionen in JavaScript eingeführt. Sie beginnen mit dem Erstellen und Aufrufen einer einfachen Aktion. Anschließend werden Sie einer Aktion Parameter hinzufügen und diese Aktion mit Parametern aufrufen. Als Nächstes folgt das Festlegen von Standardparametern und das Aufrufen dieser Parameter. Danach erstellen Sie asynchrone Aktionen und zum Schluss arbeiten Sie mit Aktionssequenzen.


### Einfache JavaScript-Aktion erstellen und aufrufen
{: #openwhisk_single_action_js}

Sehen Sie sich die folgenden Schritte und Beispiele an, um Ihre erste JavaScript-Aktion zu erstellen.

1. Erstellen Sie eine JavaScript-Datei mit dem folgenden Inhalt. Für dieses Beispiel wird der Dateiname 'hello.js' verwendet.

  ```javascript
  function main() {
      return {payload: 'Hello world'};
  }
  ```
  {: codeblock}
  Die JavaScript-Datei könnte noch weitere Funktionen enthalten. Allerdings muss nach allgemeiner Konvention eine Funktion mit dem Namen `main` vorhanden sein, um den Einstiegspunkt für die Aktion bereitzustellen.

2. Erstellen Sie eine Aktion aus der folgenden JavaScript-Funktion. Für dieses Beispiel heißt die Aktion 'hello'.

  ```
  wsk action create hello hello.js
  ```
  {: pre}
  ```
  ok: created action hello
  ```

3. Listen Sie die Aktionen auf, die Sie erstellt haben:

  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  hello       private
  ```
  Die soeben erstellte Aktion `hello` wird angezeigt.

4. Nach dem Erstellen der Aktion können Sie sie in der Cloud in OpenWhisk mit dem Befehl 'invoke' ausführen. Sie können Aktionen mit einem blockierenden (Flag *blocking*) oder mit einem nicht blockierenden (Flag *non-blocking*) Aufruf (d. h. Anforderung/Antwort) ausführen. Eine Anforderung für einen blockierenden Aufruf *wartet*, bis das Aktivierungsergebnis verfügbar ist. Der Wartezeitraum beträgt weniger als 60 Sekunden oder hat ein [Zeitlimit](./openwhisk_reference.html#openwhisk_syslimits), das für die Aktion konfiguriert wurde. Das Ergebnis der Aktivierung wird zurückgegeben, wenn es innerhalb des Wartezeitraums verfügbar ist. Anderenfalls fährt die Aktivierung mit der Verarbeitung weiter und eine Aktivierungs-ID wird zurückgegeben, sodass das Ergebnis wie bei nicht blockierenden Anforderungen später geprüft werden kann (weitere Tipps zur Überwachung von Aktivierungen finden Sie [hier](#watching-action-output)).

  Im folgenden Beispiel wird der Blockierungsparameter `--blocking` verwendet:
  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
  ```
  ```json
  {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```
  Der Befehl gibt zwei wichtige Informationen aus:
  * Die Aktivierungs-ID (`44794bd6aab74415b4e42a308d880e5b`)
  * Das Aufrufergebnis, wenn es innerhalb des erwarteten Wartezeitraums verfügbar ist  
  Das Ergebnis ist in diesem Fall die Zeichenfolge `Hello world`, die von der JavaScript-Funktion zurückgegeben wird. Mithilfe der Aktivierungs-ID können später die Protokolle oder das Ergebnis des Aufrufs abgerufen werden.  

5. Wenn Sie das Aktionsergebnis nicht sofort benötigen, können Sie das Flag `--blocking` nicht angeben und einen nicht blockierenden Aufruf ausführen. Später können Sie das Ergebnis über die Aktivierungs-ID abrufen. Beispiel:
  
  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 6bf1f670ee614a7eb5af3c9fde813043
  ```
  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```json
  {
      "payload": "Hello world"
  }
  ```

6. Wenn Sie vergessen, die Aktivierungs-ID zu notieren, können Sie eine Liste der Aktivierungen in der Reihenfolge von der jüngsten bis zur ältesten abrufen. Führen Sie den folgenden Befehl aus, um eine Liste Ihrer Aktivierungen abzurufen:

  ```
  wsk activation list
  ```
  {: pre}
  ```
  activations
  44794bd6aab74415b4e42a308d880e5b         hello
  6bf1f670ee614a7eb5af3c9fde813043         hello
  ```
  

### Parameter an eine Aktion übergeben
{: #openwhisk_adding_parameters_js}

Beim Aufruf können Parameter an die Aktion übergeben werden.

1. Verwenden Sie Parameter in der Aktion. Aktualisieren Sie die Datei 'hello.js' zum Beispiel mit dem folgenden Inhalt:

  ```javascript
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

  Die Eingabeparameter werden in Form eines JSON-Objektparameters an die Funktion `main` übergeben. Beachten Sie, wie die Parameter `name` und `place` in diesem Beispiel aus dem Objekt `params` abgerufen werden.

2. Aktualisieren Sie die Aktion `hello` und rufen Sie die Aktion auf, indem Sie Werte für die Parameter `name` und `place` übergeben. Beispiel:

  ```
  wsk action update hello hello.js
  ```
  {: pre}

3.  Parameter können in der Befehlszeile explizit angegeben oder in
einer Datei bereitgestellt werden, die die gewünschten Parameter enthält.

  Um Parameter direkt in der Befehlszeile zu übergeben, geben Sie für das
Flag `--param` ein Schlüssel/Wert-Paar an:
  ```
  wsk action invoke --blocking --result hello --param name Bernie --param place Vermont
  ```
  {: pre}

  Um eine Datei zu verwenden, die Parameterinhalt enthält, erstellen Sie
eine Datei mit den Parametern im JSON-Format. Anschließend muss der Dateiname an
das Flag `param-file` übergeben werden:

  Beispielparameterdatei namens 'parameters.json':
  ```json
  {
      "name": "Bernie",
      "place": "Vermont"
  }
  ```
  {: codeblock}

  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
  ```
  {: pre}

  ```json
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  Beachten Sie die Verwendung der Option `--result`,
damit nur das Aufrufergebnis angezeigt wird.

### Standardparameter festlegen
{: #openwhisk_binding_actions}

Aktionen können mit mehreren benannten Parameter aufgerufen werden. Die Aktion `hello` aus dem vorherigen Beispiel erwartet beispielsweise zwei Parameter: den Namen (*name*) einer Person und den Ort (*place*), aus dem sie kommt.

Anstatt nun jedes Mal alle Parameter an eine Aktion zu übergeben, können Sie bestimmte Parameter binden. Im folgenden Beispiel wird der Parameter *place* gebunden, sodass die Aktion mit dem Standardwert "Vermont" arbeitet:

1. Aktualisieren Sie die Aktion mit der Option
`--param`, um Parameterwerte zu binden, oder durch die
Übergabe einer Datei, die die Parameter enthält, an
`--param-file`.

  Um Standardparameter in der Befehlszeile explizit anzugeben, geben Sie
für das Flag `param` ein Schlüssel/Wert-Paar an:

  ```
  wsk action update hello --param place Vermont
  ```
  {: pre}

  Zur Übergabe von Parametern aus einer Datei muss eine Datei erstellt
werden, die den gewünschten Inhalt im JSON-Format enthält.
  Anschließend muss der Dateiname an das Flag `-param-file`
übergeben werden:

  Beispielparameterdatei namens 'parameters.json':
  ```json
  {
      "place": "Vermont"
  }
  ```
  {: codeblock}

  ```
  wsk action update hello --param-file parameters.json
  ```
  {: pre}

2. Rufen Sie die Aktion auf, indem Sie diesmal nur den Parameter `name` übergeben.

  ```
  wsk action invoke --blocking --result hello --param name Bernie
  ```
  {: pre}
  ```json
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  Sie stellen fest, dass Sie den Parameter "place" beim Aufruf der Aktion nicht angeben mussten. Gebundene Parameter können weiterhin durch eine entsprechende Angabe eines Parameterwerts im Aufruf überschrieben werden.

3. Rufen Sie die Aktion auf, indem Sie Werte für `name` und `place` übergeben. Der letztere Wert überschreibt den Wert, der an die Aktion gebunden ist.

  Verwendung des Flags `--param`:
  ```
  wsk action invoke --blocking --result hello --param name Bernie --param place "Washington, DC"
  ```
  {: pre}
  Verwendung des Flags `--param-file`:
  Datei parameters.json:
  ```json
  {
    "name": "Bernie",
    "place": "Vermont"
  }
  ```
  {: codeblock}  
  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
  ```
  {: pre}
  ```json
  {  
      "payload": "Hello, Bernie from Washington, DC"
  }
  ```

### Asynchrone Aktionen erstellen
{: #openwhisk_asynchrony_js}

JavaScript-Funktionen, die asynchron ausgeführt werden, müssen möglicherweise das Aktivierungsergebnis zurückgeben, wenn die Rückgabe der Funktion `main` erfolgt ist. Sie können dies erreichen, indem die Aktion ein Promise zurückgibt.

1. Speichern Sie den folgenden Inhalt in einer Datei mit dem Namen `asyncAction.js`.

  ```javascript
  function main(args) {
       return new Promise(function(resolve, reject) {
         setTimeout(function() {
           resolve({ done: true });
         }, 2000);
      })
   }
  ```
  {: codeblock}

  Beachten Sie, dass die Funktion `main` ein Promise zurückgibt. Dies weist darauf hin, dass die Aktivierung noch nicht abgeschlossen wurde, der Abschluss aber erwartet wird.

  Die JavaScript-Funktion `setTimeout()` wartet in
diesem Beispiel zwei Sekunden ab, bevor die Callback-Funktion aufgerufen wird.  Dies stellt den asynchronen Code dar, der in die Callback-Funktion des Promise eingeht.

  Der Callback des Promise verwendet zwei Argumente ('resolve' und 'reject'), die beide Funktionen sind.  Der Aufruf von `resolve()` erfüllt das Promise und weist darauf hin, dass die Aktivierung normal abgeschlossen wurde.

  Mit einem Aufruf von `reject()` kann das Promise zurückgewiesen und signalisiert werden, dass die Aktivierung abnormal beendet wurde.

2. Führen Sie die folgenden Befehle aus, um die Aktion zu erstellen und aufzurufen:

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```json
  {
      "done": true
  }
  ```
  Beachten Sie, dass Sie einen blockierenden Aufruf einer asynchronen Aktion ausgeführt haben.

3. Rufen Sie das Aktivierungsprotokoll ab, um zu prüfen, wie lange die Ausführung der Aktivierung gedauert hat:

  ```
  wsk activation list --limit 1 asyncAction
  ```
  {: pre}
  ```
  activations
  b066ca51e68c4d3382df2d8033265db0             asyncAction
  ```

  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
  ```json
  {
      "start": 1455881628103,
      "end":   1455881648126
  }
  ```
  Beim Vergleich der Zeitmarken für `start` und `end` im Aktivierungsdatensatz können Sie erkennen, dass diese Aktivierung geringfügig länger als zwei Sekunden zur Ausführung benötigt hat.


### Externe API mit Aktionen aufrufen
{: #openwhisk_apicall_action}

Die bisherigen Beispiele enthielten eigenständige JavaScript-Funktionen. Sie können jedoch auch eine Aktion erstellen, die eine externe API aufruft.

Im folgenden Beispiel wird ein Yahoo Weather-Services aufgerufen, um die aktuellen Wetterbedingungen an einem bestimmten Standort abzurufen.

1. Speichern Sie den folgenden Inhalt in einer Datei mit dem Namen `weather.js`.

  ```javascript
  var request = require('request');

  function main(params) {
      var location = params.location || 'Vermont';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';

      return new Promise(function(resolve, reject) {
          request.get(url, function(error, response, body) {
              if (error) {
                  reject(error);    
                }
                else {
                  var condition = JSON.parse(body).query.results.channel.item.condition;
                    var text = condition.text;
                    var temperature = condition.temp;
                    var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
                    resolve({msg: output});
                }
          });
      });
  }
  ```
  {: codeblock}

  Beachten Sie, dass die Aktion in diesem Beispiel die JavaScript-Bibliothek `request` verwendet, um eine HTTP-Anforderung an die Yahoo Weather-API durchzuführen, und Felder aus dem JSON-Ergebnis extrahiert. In den [Referenzinformationen](./openwhisk_reference.html#openwhisk_ref_javascript_environments) finden Sie detaillierte Informationen zu den Node.js-Paketen, die Sie in Ihren Aktionen verwenden können.

  Dieses Beispiel demonstriert außerdem den Bedarf an asynchronen Aktionen. Die Aktion gibt ein Promise zurück, um anzugeben, dass das Ergebnis dieser Aktion noch nicht verfügbar ist, wenn die Funktion die Ausführung beendet. Das Ergebnis ist erst im Callback `request` verfügbar, wenn der HTTP-Aufruf abgeschlossen ist, und wird als Argument an die Funktion `resolve()` übergeben.

2. Führen Sie die folgenden Befehle aus, um die Aktion zu erstellen und aufzurufen:

  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location "Brooklyn, NY"
  ```
  {: pre}
  ```json
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```


### Aktion als Node.js-Modul paketieren
{: #openwhisk_js_packaged_action}

Als Alternative zum Schreiben des gesamten Aktionscodes in einer einzigen JavaScript-Quellendatei können Sie eine Aktion als `npm`-Paket schreiben. Nehmen Sie als Beispiel ein Verzeichnis mit den folgenden Dateien:

Zunächst `package.json`:

```json
{
  "name": "my-action",
  "main": "index.js",
  "dependencies" : {
    "left-pad" : "1.1.3"
  }
}
```
{: codeblock}

Dann `index.js`:

```javascript
function myAction(args) {
    const leftPad = require("left-pad")
    const lines = args.lines || [];
    return { padded: lines.map(l => leftPad(l, 30, ".")) }
}

exports.main = myAction;
```
{: codeblock}

Beachten Sie, dass die Aktion über `exports.main` zugänglich gemacht wird; der Aktionshandler selbst kann einen beliebigen Namen haben, solange er der üblichen Signatur für die Annahme und die Rückgabe eines Objekts (oder einem `Promise` eines Objekts) entspricht. Den Node.js-Konventionen entsprechend muss diese Datei entweder den Namen `index.js` erhalten oder Sie müssen den bevorzugten Dateinamen in der Eigenschaft `main` in package.json angeben.

Gehen Sie wie folgt vor, um aus diesem Paket eine OpenWhisk-Aktion zu erstellen:

1. Installieren Sie zunächst alle Abhängigkeiten lokal.

  ```
  npm install
  ```
  {: pre}

2. Erstellen Sie ein `.zip`-Archiv, in dem alle Dateien (einschließlich aller Abhängigkeiten) enthalten sind:

  ```
  zip -r action.zip *
  ```
  {: pre}

3. Erstellen Sie die Aktion:

  ```
  wsk action create packageAction --kind nodejs:6 action.zip
  ```
  {: pre}

  Bei der Erstellung einer Aktion aus einem `.zip`-Archiv mithilfe des CLI-Tools beachten Sie, dass Sie explizit einen Wert für das Flag `--kind` angeben müssen.

4. Sie können die Aktion wie jede andere aufrufen:

  ```
  wsk action invoke --blocking --result packageAction --param lines "[\"and now\", \"for something completely\", \"different\" ]"
  ```
  {: pre}
  ```json
  {
      "padded": [
          ".......................and now",
          "......for something completely",
          ".....................different"
      ]
  }
  ```


Zum Schluss beachten Sie, dass zwar die meisten `npm`-Pakete JavaScript-Quellen mit `npm install` installieren, andere jedoch auch Binärartefakte installieren und kompilieren. Der Upload von Archivdateien unterstützt derzeit keine binären Abhängigkeiten, sondern nur JavaScript-Abhängigkeiten. Wenn im Archiv binäre Abhängigkeiten eingeschlossen sind, können Aktionsaufrufe fehlschlagen.

## Aktionssequenzen erstellen
{: #openwhisk_create_action_sequence}

Sie können eine Aktion erstellen, die eine Folge von Aktionen miteinander verkettet.

Verschiedene Dienstprogrammaktionen werden in einem Paket mit dem Namen `/whisk.system/utils` bereitgestellt, die Sie zum Erstellen Ihrer ersten Folge verwenden können. Weitere Informationen zu Paketen finden Sie im Abschnitt zu [Paketen](./openwhisk_packages.html).

1. Zeigen Sie die Aktionen im Paket `/whisk.system/utils` an.

  ```
  wsk package get --summary /whisk.system/utils
  ```
  {: pre}
  ```
  package /whisk.system/utils: Building blocks that format and assemble data
   action /whisk.system/utils/head: Extract prefix of an array
   action /whisk.system/utils/split: Split a string into an array
   action /whisk.system/utils/sort: Sorts an array
   action /whisk.system/utils/echo: Returns the input
   action /whisk.system/utils/date: Current date and time
   action /whisk.system/utils/cat: Concatenates input into a string
  ```


  Sie werden die Aktionen `split` (Aufteilen) und `sort` (Sortieren) in diesem Beispiel verwenden.

2. Erstellen Sie eine Aktionssequenz, sodass das Ergebnis der einen Aktion als Argument an die nächste Aktion übergeben wird.

  ```
  wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort
  ```
  {: pre}

  Diese Aktionssequenz konvertiert Zeilen von Text in ein Array und sortiert die Zeilen.

3. Rufen Sie die Aktion auf:

  ```
  wsk action invoke --blocking --result sequenceAction --param payload "Over-ripe sushi,\nThe Master\nIs full of regret."
  ```
  {: pre}
  ```json
  {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
  ```


  Wie leicht zu erkennen ist, sind die Zeilen im Ergebnis sortiert.

**Hinweis:** Parameter, die zwischen Aktionen in der Sequenz übergeben werden, sind explizit. Ausgenommen davon sind die Standardparameter.
Daher sind die Parameter, die der Aktionssequenz übergeben werden, nur für die erste Aktion in der Sequenz verfügbar.
Das Ergebnis der ersten Aktion in der Sequenz wird zum JSON-Eingabeobjekt für die zweite Aktion in der Sequenz usw.
Das Objekt enthält keine Parameter, die ursprünglich an die Sequenz übergeben wurden, es sei denn, die erste Aktion enthält sie explizit in ihrem Ergebnis.
Die Eingabeparameter für eine Aktion werden mit den Standardparametern der Aktion zusammengeführt. Erstere haben Vorrang und überschreiben alle übereinstimmenden Standardparameter.
Weitere Informationen zum Aufrufen von Aktionssequenzen mit mehreren benannten Parametern finden Sie unter [Standardparameter festlegen](./openwhisk_actions.html#openwhisk_binding_actions).

## Python-Aktionen erstellen
{: #openwhisk_actions_python}

Das Verfahren zur Erstellung von Python-Aktionen ist dem von JavaScript-Aktionen ähnlich. In den folgenden Abschnitten werden die Schritte zum Erstellen und Aufrufen einer einzelnen Python-Aktion sowie zum Übergeben von Parametern an diese Aktion beschrieben.

### Aktion erstellen und aufrufen
{: #openwhisk_actions_python_invoke}

Eine Aktion ist einfach eine Python-Funktion der höchsten Ebene. Das heißt, dass eine Methode mit dem Namen `main` erforderlich ist. Erstellen Sie beispielsweise eine Datei mit dem Namen `hello.py` und dem folgenden Inhalt:

```python
def main(dict):
    name = dict.get("name", "stranger")
    greeting = "Hello " + name + "!"
    print(greeting)
        return {"greeting": greeting}
```
{: codeblock}

Python-Aktionen lesen stets ein Wörterverzeichnis (Dictionary) und generieren ein Wörterverzeichnis.

Sie können eine OpenWhisk-Aktion mit dem Namen `helloPython` wie folgt aus dieser Funktion erstellen:

```
wsk action create helloPython hello.py
```
{: pre}

Bei Verwendung der Befehlszeile und einer `.py`-Quellendatei brauchen Sie nicht anzugeben, dass Sie eine Python-Aktion (im Unterschied zu einer JavaScript-Aktion) erstellen; das Tool bestimmt dies anhand der Dateierweiterung.

Der Aktionsaufruf für Python-Aktionen stimmt mit dem für JavaScript-Aktionen überein:

```
wsk action invoke --blocking --result helloPython --param name World
```
{: pre}

```json
  {
      "greeting": "Hello World!"
  }
```



## Swift-Aktionen erstellen
{: #openwhisk_actions_swift}

Das Verfahren zur Erstellung von Swift-Aktionen ist dem von JavaScript-Aktionen ähnlich. In den folgenden Abschnitten werden die Schritte zum Erstellen und Aufrufen einer einzelnen Swift-Aktion sowie zum Übergeben von Parametern an diese Aktion beschrieben.

Sie können Ihren Swift-Code auch online mithilfe der [Swift-Sandbox](https://swiftlang.ng.bluemix.net) testen, ohne Xcode auf Ihrer Maschine installieren zu müssen.

### Aktion erstellen und aufrufen
{: #openwhisk_actions_invoke_swift}

Eine Aktion ist eine einfache Swift-Funktion der höchsten Ebene. Erstellen Sie zum Beispiel eine Datei mit dem Namen `hello.swift` und dem folgenden Inhalt:

```swift
func main(args: [String:Any]) -> [String:Any] {
    if let name = args["name"] as? String {
        return [ "greeting" : "Hello \(name)!" ]
    } else {
        return [ "greeting" : "Hello stranger!" ]
    }
}
```
{: codeblock}

Swift-Aktionen lesen stets ein Wörterverzeichnis (Dictionary) und generieren ein Wörterverzeichnis.

Sie können eine {{site.data.keyword.openwhisk_short}}-Aktion mit dem Namen `helloSwift` wie folgt aus dieser Funktion erstellen:

```
wsk action create helloSwift hello.swift
```
{: pre}

Bei Verwendung der Befehlszeile und einer Swift-Quellendatei (`.swift`) brauchen Sie nicht anzugeben, dass Sie eine Swift-Aktion (im Unterschied zu einer JavaScript-Aktion) erstellen; das Tool bestimmt dies anhand der Dateierweiterung.

Der Aktionsaufruf für Swift-Aktionen stimmt mit dem für JavaScript-Aktionen überein:

```
wsk action invoke --blocking --result helloSwift --param name World
```
{: pre}

```json
  {
      "greeting": "Hello World!"
  }
```


**Achtung:** Swift-Aktionen werden in einer Linux-Umgebung ausgeführt. Swift unter Linux befindet sich noch in Entwicklung und {{site.data.keyword.openwhisk_short}} arbeitet in der Regel mit dem neuesten verfügbaren Release, das jedoch nicht unbedingt stabil ist. Darüber hinaus ist es möglich, dass die mit {{site.data.keyword.openwhisk_short}} verwendete Version von Swift nicht mit den Versionen von Swift aus stabilen Releases von XCode on MacOS konsistent ist.

## Java-Aktionen erstellen
{: #openwhisk_actions_java}

Das Verfahren zur Erstellung von Java-Aktionen ist dem von
JavaScript- und Swift-Aktionen ähnlich. In den folgenden Abschnitten werden die
Schritte zum Erstellen und Aufrufen einer einzelnen Java-Aktion sowie zum
Übergeben von Parametern an diese Aktion beschrieben.

Damit Sie Java-Dateien kompilieren, testen und archivieren können, muss
lokal eine
[JDK
8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) installiert sein.

### Aktion erstellen und aufrufen
{: #openwhisk_actions_java_invoke}

Eine Java-Aktion ist ein Java-Programm mit einer Methode namens
`main`, deren exakte Signatur wie folgt lautet:
```java
public static com.google.gson.JsonObject main(com.google.gson.JsonObject);
```
{: codeblock}

Erstellen Sie beispielsweise eine Java-Datei namens
`Hello.java` mit dem folgenden Inhalt:

```java
import com.google.gson.JsonObject;
public class Hello {
    public static JsonObject main(JsonObject args) {
        String name = "stranger";
        if (args.has("name"))
            name = args.getAsJsonPrimitive("name").getAsString();
        JsonObject response = new JsonObject();
        response.addProperty("greeting", "Hello " + name + "!");
        return response;
    }
}
```
{: codeblock}

Kompilieren Sie anschließend die Datei `Hello.java` wie folgt in einer Datei `hello.jar`:
```
javac Hello.java
```
{: pre}
```
jar cvf hello.jar Hello.class
```
{: pre}

**Hinweis:** [google-gson](https://github.com/google/gson) muss im Java-Klassenpfad (CLASSPATH) vorhanden sein, wenn Sie die Java-Datei kompilieren.

Aus dieser JAR-Datei können Sie folgendermaßen eine OpenWhisk-Aktion
namens `helloJava` erstellen:

```
wsk action create helloJava hello.jar --main Hello
```
{: pre}

Bei Verwendung der Befehlszeile und einer Swift-Quellendatei
(`.jar`) brauchen Sie nicht anzugeben, dass Sie eine
Java-Aktion erstellen; das Tool
bestimmt dies anhand der Dateierweiterung.

Sie müssen den Namen der Hauptklasse mit `--main` angeben. Mit einer infrage kommenden
Hauptklasse wird wie oben beschrieben eine statische `main`-Methode implementiert. Wenn sich die
Klasse nicht im Standardpaket befindet, verwenden Sie den vollständig qualifizierten Java-Klassennamen,
z. B. `--main com.example.MyMain`.

Der Aktionsaufruf für Java-Aktionen stimmt mit dem für
Swift- und JavaScript-Aktionen überein:

```
wsk action invoke --blocking --result helloJava --param name World
```
{: pre}

```json
  {
      "greeting": "Hello World!"
  }
```

## Docker-Aktionen erstellen
{: #openwhisk_actions_docker}

Bei {{site.data.keyword.openwhisk_short}} Docker-Aktionen können Sie Ihre Aktionen in einer beliebigen Sprache schreiben.

Ihr Code wird in eine ausführbare Binärdatei kompiliert und in ein Docker-Image eingebettet. Das Binärprogramm interagiert mit dem System durch Eingaben über `stdin` und Ausgaben über `stdout`.

Voraussetzung ist, dass Sie über ein Docker Hub-Konto verfügen.  Rufen Sie zur Einrichtung einer kostenlosen Docker-ID und eines Kontos [Docker Hub](https://hub.docker.com){: new_window} auf.

In den nachfolgenden Anweisungen wird die Docker-Benutzer-ID `janesmith` und das Kennwort `janes_password` verwendet.  Wenn die CLI bereits eingerichtet ist, sind drei Schritte erforderlich, um eine angepasste Binärdatei zur Verwendung durch {{site.data.keyword.openwhisk_short}} einzurichten. Anschließend kann das hochgeladene Docker-Image als Aktion verwendet werden.

1. Laden Sie das Docker-Gerüst (Skeleton) herunter. Sie können es über die CLI wie folgt herunterladen:

  ```
  wsk sdk install docker
  ```
  {: pre}
  ```
  The Docker skeleton is now installed at the current directory.
  ```
  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh example.c
  ```
  Das Gerüst ist eine Docker-Containervorlage, in die Sie Ihren Code in Form von angepassten Binärdateien einfügen können.

2. Richten Sie Ihre angepasste Binärdatei im Docker-Gerüst ('docherSkeleton') ein. Das Gerüst schließt bereits ein C-Programm ein, das Sie verwenden können.

  ```
  cat dockerSkeleton/example.c
  ```
  {: pre}
  ```c
  #include <stdio.h>
  int main(int argc, char *argv[]) {
      printf("This is an example log message from an arbitrary C program!\n");
      printf("{ \"msg\": \"Hello from arbitrary C program!\", \"args\": %s }",
             (argc == 1) ? "undefined" : argv[1]);
  }
  ```
  {: codeblock}

  Sie können diese Datei nach Bedarf ändern oder dem Docker-Image zusätzlichen Code und zusätzliche Abhängigkeiten hinzufügen.
  Im letzteren Fall müssen Sie ggf. die `Dockerfile` optimieren, um Ihre ausführbare Datei zu erstellen.
  Die Binärdatei muss sich im Container unter `/action/exec` befinden.

  Die Binärdatei empfängt ein einzelnes Argument von der Befehlszeile. Es handelt sich um eine Serialisierungen-Serialisierung des JSON-Objekts,
  das die Argumente für die Aktion darstellt. Das Programm gibt die Protokolle in `stdout` oder `stderr` aus.
  Die letzte Zeile der Ausgabe *muss* ein in eine Zeichenfolge konvertiertes JSON-Objekt sein, das das Aktionsergebnis darstellt.

3. Erstellen Sie das Docker-Image und laden Sie es mithilfe eines bereitgestellten Scripts hoch. Sie müssen zunächst den Befehl `docker login` zur Authentifizierung und anschließend das Script mit einem ausgewählten Imagenamen ausführen.

  ```
  docker login -u janesmith -p janes_password
  ```
  {: pre}
  ```
  cd dockerSkeleton
  ```
  {: pre}
  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  Beachten Sie, dass ein Teil der Datei 'example.c' im Rahmen des Buildprozesses für das Docker-Image kompiliert wird, sodass Sie keine C-Kompilierung auf Ihrer Maschine benötigen.
  Es wird ggf. nicht im Container ausgeführt, da die Formate nicht übereinstimmen, es sei denn, Sie kompilieren die Binärdatei auf einer kompatiblen Hostmaschine.

  Ihr Docker-Container kann jetzt als {{site.data.keyword.openwhisk_short}}-Aktion verwendet werden.

  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}

  Beachten Sie die Verwendung von `--docker`, wenn Sie eine Aktion erstellen. Es wird angenommen, dass Docker-Images auf einem Docker-Hub gehostet werden.
  Die Aktion wird wie alle anderen {{site.data.keyword.openwhisk_short}}-Aktionen aufgerufen.

  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```json
  {
      "args": {
          "payload": "Rey"
      },
      "msg": "Hello from arbitrary C program!"
  }
  ```

  Zum Aktualisieren der Docker-Aktion führen Sie buildAndPush.sh aus, um das neueste Image auf Docker Hub hochzuladen. Dies ermöglicht dem System das Extrahieren Ihres neuen Docker-Images bei der nächsten Ausführung des Codes für Ihre Aktion.
  Wenn es keine aktiven Container gibt, verwenden die Aufrufe das neue Docker-Image.
  Wenn jedoch ein aktiver Container vorhanden ist, der eine ältere Version Ihres Docker-Images verwendet, verwenden neue Aufrufe weiterhin dieses Image, solange Sie nicht den Befehl `wsk action update` ausführen. Damit wird dem System angezeigt, dass es für neue Aufrufe eine Docker-Pull-Operation ausführen muss, um Ihr neues Docker-Image abzurufen.

  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  ```
  wsk action update --docker example janesmith/blackboxdemo
  ```
  {: pre}

  Weitere Informationen zur Erstellung von Docker-Aktionen finden Sie im Abschnitt mit den [Referenzinformationen](./openwhisk_reference.html#openwhisk_ref_docker).

## Aktionsausgaben beobachten
{: #openwhisk_actions_polling}

{{site.data.keyword.openwhisk_short}}-Aktionen können von anderen Benutzern, als Reaktion auf verschiedene Ereignisse oder als Teil einer Aktionssequenz aufgerufen werden. In solchen Fällen kann es nützlich sein, die Aufrufe zu überwachen.

Sie können die Ausgabe von Aktionen, wenn sie aufgerufen werden, über die {{site.data.keyword.openwhisk_short}}-CLI beobachten.

1. Geben Sie den folgenden Befehl über eine Shell ein:
  ```
  wsk activation poll
  ```
  {: pre}

  Dieser Befehl startet eine Polling-Schleife, die kontinuierlich auf Protokolle aus Aktivierungen prüft.

2. Wechseln Sie zu einem anderen Fenster und rufen Sie eine Aktion auf:

  ```
  wsk action invoke /whisk.system/samples/helloWorld --param payload Bob
  ```
  {: pre}
  ```
  ok: invoked /whisk.system/samples/helloWorld with id 7331f9b9e2044d85afd219b12c0f1491
  ```

3. Beobachten Sie das Aktivierungsprotokoll in dem Polling-Fenster:

  ```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```

  Immer wenn Sie das Dienstprogramm 'poll' ausführen, werden die Protokolle für Aktionen, die für Sie in {{site.data.keyword.openwhisk_short}} ausgeführt werden, in Echtzeit angezeigt.

## Aktionen löschen
{: #openwhisk_delete_action}

Sie können eine Bereinigung durchführen, indem Sie Aktionen löschen, die nicht mehr verwendet werden sollen.

1. Führen Sie den folgenden Befehl zum Löschen einer Aktion aus:
  ```
  wsk action delete hello
  ```
  {: pre}
  ```
  ok: deleted hello
  ```

2. Überprüfen Sie, ob die Aktion nicht mehr in der Liste der Aktionen angezeigt wird.
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: pre}

## In der Aktionskomponente auf Aktionsmetadaten zugreifen

Die Aktionsumgebung enthält mehrere Eigenschaften, die für die aktive Aktion spezifisch sind.
Mit diesen kann die Aktion programmgestützt über die REST-API mit OpenWhisk-Assets arbeiten oder einen internen
Alarm auslösen, wenn die Aktion kurz davor ist, das zugeteilte Zeitbudget aufzubrauchen.
Auf die Eigenschaften kann über die Systemumgebung für alle unterstützten Laufzeiten zugegriffen werden:
Node.js-, Python-, Swift-, Java- und Docker-Aktionen bei Verwendung des Docker-Gerüsts für OpenWhisk.

* `__OW_API_HOST`: Der API-Host für die OpenWhisk-Bereitstellung, in der diese Aktion ausgeführt wird.
* `__OW_API_KEY`: Der API-Schlüssel für das Subjekt, das die Aktion aufruft; bei diesem Schlüssel kann es sich um einen eingeschränkten API-Schlüssel handeln.
* `__OW_NAMESPACE`: Der Namensbereich für die Aktivierung (*activation*) (möglicherweise nicht mit dem Namensbereich für die Aktion identisch).
* `__OW_ACTION_NAME`: Der vollständig qualifizierte Name der aktiven Aktion.
* `__OW_ACTIVATION_ID`: Die Aktivierungs-ID für diese aktive Aktionsinstanz.
* `__OW_DEADLINE`: Der näherungsweise berechnete Zeitpunkt, an dem diese Aktion das gesamte Zeitkontingent aufgebraucht hat (in Epoch-Millisekunden).
