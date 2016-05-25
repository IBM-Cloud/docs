---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}}-Aktionen erstellen und aufrufen
{: #openwhisk_actions}

*Letzte Aktualisierung: 22. März 2016*

Aktionen sind statusunabhängige Code-Snippets, die auf der {{site.data.keyword.openwhisk}}-Plattform ausgeführt werden. Bei einer Aktion kann es sich um eine JavaScript-Funktion, eine Swift-Funktion oder ein angepasstes ausführbares Programm, das in einem Docker-Container enthalten ist, handeln. Eine Aktion kann zum Beispiel zum Erkennen der Gesichter auf einem Bild, zum Aggregieren einer Gruppe von API-Aufrufen oder zum Senden eines Tweets verwendet werden.
{:shortdesc}

Aktionen können explizit aufgerufen oder als Reaktion auf ein Ereignis ausgeführt werden. In beiden Fällen führt die Ausführung einer Aktion zu einem Aktivierungsdatensatz, der durch eine eindeutige Aktivierungs-ID identifiziert wird. Die Eingabe für eine Aktion und das Ergebnis einer Aktion bestehen jeweils in einem Wörterverzeichnis aus Schlüssel/Wert-Paaren, wobei der Schlüssel eine Zeichenfolge und der Wert ein gültiger JSON-Wert ist.

Aktionen können aus Aufrufen weiterer Aktionen oder aus einer definierten Folge von Aktionen bestehen.

## JavaScript-Aktionen erstellen und aufrufen
{: #openwhisk_create_action_js}

In den folgenden Abschnitten werden Sie in die Arbeit mit Aktionen in JavaScript eingeführt. Zu Beginn wird das Erstellen und Aufrufen einer einfachen Aktion erläutert. Anschließend werden die Vorgehensweisen behandelt, mit denen Sie einer Aktion Parameter hinzufügen und diese Aktion mit Parametern aufrufen, Standardparameter festlegen und diese aufrufen sowie asynchrone Aktionen erstellen. Zum Abschluss wird die Arbeit mit Aktionsfolgen beschrieben.


### Einfache JavaScript-Aktion erstellen und aufrufen
{: #openwhisk_single_action_js}

Sehen Sie sich die folgenden Schritte und Beispiele an, um Ihre erste JavaScript-Aktion zu erstellen.

1. Erstellen Sie eine JavaScript-Datei mit dem folgenden Inhalt. Für dieses Beispiel wird der Dateiname 'hello.js' verwendet.
  
  ```
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
  {: screen}

3. Listen Sie die Aktionen auf, die Sie erstellt haben:
  
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  hello       private
  ```
  {: screen}

  Die soeben erstellte Aktion `hello` wird angezeigt.

4. Nach dem Erstellen der Aktion können Sie sie in der Cloud in {{site.data.keyword.openwhisk_short}} mit dem Befehl 'invoke' ausführen. Sie können Aktionen mit einem blockierenden (Flag *blocking*) oder mit einem nicht blockierenden (Flag *non-blocking*) Aufruf ausführen. Ein blockierender Aufruf wartet solange, bis die Aktion abgeschlossen ist, und gibt ein Ergebnis zurück. Im folgenden Beispiel wird der Blockierungsparameter `-blocking` verwendet:

  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
  response:
  {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

  Der Befehl gibt zwei wichtige Informationen aus:
  * Die Aktivierungs-ID (`44794bd6aab74415b4e42a308d880e5b`)
  * Das Aufrufergebnis

  Das Ergebnis ist in diesem Fall die Zeichenfolge `Hello world`, die von der JavaScript-Funktion zurückgegeben wird. Mithilfe der Aktivierungs-ID können später die Protokolle oder das Ergebnis des Aufrufs abgerufen werden.  

5. Wenn Sie das Aktionsergebnis nicht sofort benötigen, können Sie das Flag `--blocking` nicht angeben und einen nicht blockierenden Aufruf ausführen. Später können Sie das Ergebnis über die Aktivierungs-ID abrufen. Beispiel:

  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: screen}

  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```
  {
      "payload": "Hello world"
  }
  ```
  {: screen}

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
  {: screen}

### Parameter an eine Aktion übergeben
{: #openwhisk_adding_parameters_js}

Beim Aufruf können Parameter an die Aktion übergeben werden.

1. Verwenden Sie Parameter in der Aktion. Aktualisieren Sie die Datei 'hello.js' zum Beispiel mit dem folgenden Inhalt:
  
  ```
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
  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Vermont'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  Beachten Sie die Verwendung der Option `--param` zur Angabe eines Parameternamens und eines Parameterwerts sowie die Verwendung der Option `--result`, um nur das Aufrufergebnis anzuzeigen.

### Standardparameter festlegen
{: #openwhisk_binding_actions}

Aktionen können mit mehreren benannten Parameter aufgerufen werden. Die Aktion `hello` aus dem vorherigen Beispiel erwartet beispielsweise zwei Parameter: den Namen (*name*) einer Person und den Ort (*place*), aus dem sie kommt.

Anstatt nun jedes Mal alle Parameter an eine Aktion zu übergeben, können Sie bestimmte Parameter binden. Im folgenden Beispiel wird der Parameter *place* gebunden, sodass die Aktion mit dem Standardwert "Vermont" arbeitet:
 
1. Aktualisieren Sie die Aktion mit der Option `--param`, um Parameterwerte zu binden.

  ```
  wsk action update hello --param place 'Vermont'
  ```
  {: pre}

2. Rufen Sie die Aktion auf, indem Sie diesmal nur den Parameter `name` übergeben.

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  Sie stellen fest, dass Sie den Parameter "place" beim Aufruf der Aktion nicht angeben mussten. Gebundene Parameter können weiterhin durch eine entsprechende Angabe eines Parameterwerts im Aufruf überschrieben werden.

3. Rufen Sie die Aktion auf, indem Sie Werte für `name` und `place` übergeben. Der letztere Wert überschreibt den Wert, der an die Aktion gebunden ist.

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Washington, DC'
  ```
  {: pre}
  ```
  {  
      "payload": "Hello, Bernie from Washington, DC"
  }
  ```
  {: screen}

### Asynchrone Aktionen erstellen
{: #openwhisk_asynchrony_js}

JavaScript-Funktionen, deren Ausführung in einer Callback-Funktion fortgesetzt wird, müssen möglicherweise das Aktivierungsergebnis zurückgeben, wenn die Rückgabe der Funktion `main` erfolgt ist. Sie können dies durch die Verwendung der Funktionen `whisk.async()` und `whisk.done()` in Ihrer Aktion erreichen.

1. Speichern Sie den folgenden Inhalt in einer Datei mit dem Namen `asyncAction.js`.

  ```
  function main() {
      setTimeout(function() {
          return whisk.done({done: true});
      }, 20000);
      return whisk.async();
  }
  ```
  {: codeblock}

  Beachten Sie, dass die Funktion `main` sofort zurückkehrt und das der Rückgabewert `whisk.async()` angibt, dass diese Aktivierung weiterhin ausgeführt werden soll.

  Die JavaScript-Funktion `setTimeout()` wartet in diesem Beispiel 20 Sekunden ab, bevor sie die Callback-Funktion aufruft, wobei der Aufruf der Funktion `whisk.done()` angibt, dass die Aktivierung abgeschlossen ist.

2. Führen Sie die folgenden Befehle aus, um die Aktion zu erstellen und aufzurufen:

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```
  {
      "done": true
  }
  ```
  {: screen}

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
  {: screen}


  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
 ```
  {
      "start": 1455881628103,
      "end":   1455881648126,
      ...
  }
  ```
  {: screen}

  Beim Vergleich der Zeitmarken für `start` und `end` im Aktivierungsdatensatz können Sie erkennen, dass diese Aktivierung geringfügig länger als 20 Sekunden zur Ausführung benötigt hat.


### Externe API mit Aktionen aufrufen
{: #openwhisk_apicall_action}

Die bisherigen Beispiele enthielten eigenständige JavaScript-Funktionen. Sie können jedoch auch eine Aktion erstellen, die eine externe API aufruft.

Im folgenden Beispiel wird ein Yahoo Weather-Services aufgerufen, um die aktuellen Wetterbedingungen an einem bestimmten Standort abzurufen. 

1. Speichern Sie den folgenden Inhalt in einer Datei mit dem Namen `weather.js`.
  ```
    var request = require('request');
    
    function main(msg) {
        var location = msg.location || 'Vermont';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';
    
        request.get(url, function(error, response, body) {
            var condition = JSON.parse(body).query.results.channel.item.condition;
            var text = condition.text;
            var temperature = condition.temp;
            var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
            whisk.done({msg: output});
        });
    
        return whisk.async();
    }
  ```
  {: codeblock}

  Beachten Sie, dass die Aktion in diesem Beispiel die JavaScript-Bibliothek `request` verwendet, um eine HTTP-Anforderung an die Yahoo Weather-API durchzuführen, und Felder aus dem JSON-Ergebnis extrahiert. In den [Referenzinformationen](./openwhisk_reference.html#runtime_ref_runtime_environment) finden Sie detaillierte Informationen zu den Node.js-Paketen, die Sie in Ihren Aktionen verwenden können.
  
  Dieses Beispiel demonstriert außerdem den Bedarf an asynchronen Aktionen. Die Aktion gibt `whisk.async()` zurück, um anzugeben, dass das Ergebnis dieser Aktion noch nicht verfügbar ist, wenn die Funktion die Ausführung beendet. Das Ergebnis ist erst im Callback `request` verfügbar, wenn der HTTP-Aufruf abgeschlossen ist, und wird als Argument an die Funktion `whisk.done()` übergeben.

2. Führen Sie die folgenden Befehle aus, um die Aktion zu erstellen und aufzurufen:
  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location 'Brooklyn, NY'
  ```
  {: pre}
  ```
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```
  {: screen}

### Aktionsfolgen erstellen
{: #openwhisk_create_action_sequence}

Sie können eine Aktion erstellen, die eine Folge von Aktionen miteinander verkettet.

Verschiedene Dienstprogrammaktionen werden in einem Paket mit dem Namen `/whisk.system/util` bereitgestellt, die Sie zum Erstellen Ihrer ersten Folge verwenden können. Weitere Informationen zu Paketen finden Sie im Abschnitt zu [Paketen](./openwhisk_packages.html).

1. Zeigen Sie die Aktionen im Paket `/whisk.system/util` an.
  
  ```
  wsk package get --summary /whisk.system/util
  ```
  {: pre}
  ```
  package /whisk.system/util
   action /whisk.system/util/cat: Concatenate array of strings, and split lines into an array
   action /whisk.system/util/head: Filter first K array elements and discard rest
   action /whisk.system/util/date: Get current date and time
   action /whisk.system/util/sort: Sort array
  ```
  {: screen}

  Sie werden die Aktionen `cat` (Verketten) und `sort` (Sortieren) in diesem Beispiel verwenden.

2. Erstellen Sie eine Aktionsfolge, sodass das Ergebnis der einen Aktion als Argument an die nächste Aktion übergeben wird.
  
  ```
  wsk action create myAction --sequence /whisk.system/util/cat,/whisk.system/util/sort
  ```
  {: pre}

  Diese Aktionsfolge konvertiert Zeilen von Text in ein Array und sortiert die Zeilen.

3. Erstellen Sie vor dem Aufruf der Aktionsfolge eine Textdatei mit dem Namen 'haiku.txt', die einige wenige Textzeilen enthält:

  ```
  Over-ripe sushi,
  The Master
  Is full of regret.
  ```
  {: codeblock}

4. Rufen Sie die Aktion auf:
  
  ```
  wsk action invoke --blocking --result myAction --param payload "$(cat haiku.txt)"
  ```
  {: pre}
  ```
  {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
  ```
  {: screen}

  Wie leicht zu erkennen ist, sind die Zeilen im Ergebnis sortiert.

**Hinweis:** Weitere Informationen zum Aufrufen von Aktionsfolgen mit mehreren benannten Parametern finden Sie unter [Standardparameter festlegen](./openwhisk_actions.html##openwhisk_binding_actions)

## Swift-Aktionen erstellen
{: #openwhisk_actions_swift}

Das Verfahren zur Erstellung von Swift-Aktionen ist dem von JavaScript-Aktionen ähnlich. In den folgenden Abschnitten werden die Schritte zum Erstellen und Aufrufen einer einzelnen Swift-Aktion sowie zum Übergeben von Parametern an diese Aktion beschrieben.

Sie können Ihren Swift-Code auch online mithilfe der [Swift-Sandbox](https://swiftlang.ng.bluemix.net) testen, ohne Xcode auf Ihrer Maschine installieren zu müssen.

### Aktion erstellen und aufrufen
{: #openwhisk_actions_invoke_swift}

Eine Aktion ist eine einfache Swift-Funktion der höchsten Ebene. Erstellen Sie zum Beispiel eine Datei mit dem Namen `hello.swift` und dem folgenden Inhalt:

```
  func main(args: [String:Any]) -> [String:Any] {
      if let name = args["name"] as? String {
          return [ "greeting" : "Hello \(name)!" ]
      } else {
          return [ "greeting" : "Hello stranger!" ]
      }
  }
```
{: codeblock}

Beachten Sie, dass Swift-Aktionen ebenso wie JavaScript-Aktionen ein Wörterverzeichnis (Dictionary) lesen und ein Wörterverzeichns generieren.

Sie können eine {{site.data.keyword.openwhisk_short}}-Aktion mit dem Namen `helloSwift` wie folgt aus dieser Funktion erstellen:

```
wsk action create helloSwift hello.swift
```
{: pre}

Bei Verwendung der Befehlszeile und einer Swift-Quellendatei (`.swift`) brauchen
Sie nicht anzugeben, dass Sie eine Swift-Aktion (im Unterschied zu einer JavaScript-Aktion) erstellen;
das Tool bestimmt dies anhand der Dateierweiterung.

Der Aktionsaufruf für Swift-Aktionen stimmt mit dem für JavaScript-Aktionen überein:

```
wsk action invoke --blocking --result helloSwift --param name World
```
{: pre}

```
  {
      "greeting": "Hello World!"
  }
```
{: screen}

**Achtung:** Swift-Aktionen werden in einer Linux-Umgebung ausgeführt. Swift unter Linux befindet sich noch in Entwicklung und {{site.data.keyword.openwhisk_short}} arbeitet in der Regel mit dem neuesten verfügbaren Release, das jedoch nicht unbedingt stabil ist. Darüber hinaus ist es möglich, dass die mit {{site.data.keyword.openwhisk_short}} verwendete Version von Swift nicht mit den Versionen von Swift aus stabilen Releases von XCode on MacOS konsistent ist.

## Docker-Aktionen erstellen
{: #openwhisk_actions_docker}

Bei {{site.data.keyword.openwhisk_short}} Docker-Aktionen können Sie Ihre Aktionen in einer beliebigen Sprache schreiben.

Ihr Code wird in eine ausführbare Binärdatei kompiliert und in ein Docker-Image eingebettet. Das Binärprogramm interagiert mit dem System durch Eingaben über `stdin` und Ausgaben über `stdout`.

Voraussetzung ist, dass Sie über ein Docker Hub-Konto verfügen.  Rufen Sie zur Einrichtung einer kostenlosen Docker-ID und eines Kontos [Docker Hub](https://hub.docker.com){: new_window} auf.

In den nachfolgenden Anweisungen wird die Benutzer-ID "janesmith" und das Kennwort "janes_password" verwendet.  Wenn die CLI bereits eingerichtet ist, sind drei Schritte erforderlich, um eine angepasste Binärdatei zur Verwendung durch {{site.data.keyword.openwhisk_short}} einzurichten.  Anschließend kann das hochgeladene Docker-Image als Aktion verwendet werden.

1. Laden Sie das Docker-Gerüst (Skeleton) herunter. Sie können es über die CLI wie folgt herunterladen:

  ```
  wsk sdk install docker
  ```
  {: pre}
  ```
  The Docker skeleton is now installed at the current directory.
  ```
  {: screen}

  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh client          server
  ```
  {: screen}

  Das Gerüst ist eine Docker-Containervorlage, in die Sie Ihren Code in Form von angepassten Binärdateien einfügen können.

2. Richten Sie Ihre angepasste Binärdatei im Docker-Gerüst ('docherSkeleton') ein. Das Gerüst schließt bereits ein C-Programm ein, das Sie verwenden können.

  ```
  cat ./dockerSkeleton/client/example.c
  ```
  {: pre}
  {: pre}
  ```
  #include <stdio.h>
  
  int main(int argc, char *argv[]) {
      printf("Hallo %s von einem beliebigen C-Programm!\n",
             (argc == 1) ? "anonymous" : argv[1]);
  }
  ```
  {: screen}

  Sie können diese Datei nach Bedarf ändern.

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

4. Zum Erstellen einer Aktion aus einem Docker-Image anstelle einer bereitgestellten JavaScript-Datei fügen Sie `--docker` hinzu und ersetzen den Namen der JavaScript-Datei durch den Namen des Docker-Image.

  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```
  {
      "msg": "Hello Rey from arbitrary C program!\n"
  }
  ```
  {: screen}


Weitere Informationen zur Erstellung von Docker-Aktionen finden Sie im Abschnitt mit den [Referenzinformationen](./openwhisk_reference.html#openwhisk_ref_docker).


## Aktionsausgaben beobachten
{: #openwhisk_actions_polling}

{{site.data.keyword.openwhisk_short}}-Aktionen können von anderen Benutzern, als Reaktion auf verschiedene Ereignisse oder als Teil einer Aktionsfolge aufgerufen werden. In solchen Fällen kann es nützlich sein, die Aufrufe zu überwachen.

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
  {: screen}

3. Beobachten Sie das Aktivierungsprotokoll in dem Polling-Fenster:

  ```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```
  {: screen}

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
  {: screen}

2. Überprüfen Sie, ob die Aktion nicht mehr in der Liste der Aktionen angezeigt wird.
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: screen}
