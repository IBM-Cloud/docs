---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}}-Systemdetails
{: #openwhisk_reference}
*Letzte Aktualisierung: 14. April 2016*

Die folgenden Abschnitte enthalten weitere Details zum {{site.data.keyword.openwhisk}}-System.
{: shortdesc}

## {{site.data.keyword.openwhisk_short}}-Entitäten
{: #openwhisk_entities}

### Namensbereiche und Pakete

Aktionen, Auslöser (Triggers) und Regeln von {{site.data.keyword.openwhisk_short}} gehören in einen Namensbereich und optional in ein Paket.

Pakete können Aktionen und Feeds enthalten. Ein Paket kann kein anderes Paket enthalten, sodass eine Paketverschachtelung nicht zulässig ist. Darüber hinaus müssen Entitäten nicht in einem Paket enthalten sein.

In Bluemix entspricht ein Paar aus Organisation und Bereich einem {{site.data.keyword.openwhisk_short}}-Namensbereich. Zum Beispiel würden die Organisation `BobsOrg` und der Bereich `dev` dem {{site.data.keyword.openwhisk_short}}-Namensbereich `/BobsOrg_dev` entsprechen.

Sie können eigene Namensbereiche erstellen, wenn Sie dazu berechtigt sind. Der Namensbereich `/whisk.system` ist für Entitäten reserviert, die mit dem {{site.data.keyword.openwhisk_short}}-System verteilt werden.


### Vollständig qualifizierte Namen

Der vollständig qualifizierte Name einer Entität sieht wie folgt aus: `/Namensbereichsname[/Paketname]/Entitätsname`. Beachten Sie, dass das Zeichen `/` zum Abgrenzen von Namensbereichen, Paketen und Entitäten verwendet wird. Darüber hinaus muss Namensbereichen auch das Zeichen `/` als Präfix vorangestellt werden.

Aus Gründen des Komforts kann der Namensbereich weggelassen werden, wenn es sich um den *Standardnamensbereich* des Benutzers handelt.

Beispiel: Betrachten Sie einen Benutzer mit dem Standardnamensbereich `/myOrg`. Die folgenden Beispiele zeigen die vollständig qualifizierten Namen einer Reihe von Entitäten und ihre Aliasnamen.

| Vollständig qualifizierter Name | Alias | Namensbereich | Paket | Name |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` | - | `/whisk.system` | `cloudant` | `read` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `video` | `transcode` |
| `/myOrg/filter` | `filter` | `/myOrg` | - | `filter` |

Sie verwenden dieses Benennungsschema unter anderem zum Beispiel, wenn Sie die {{site.data.keyword.openwhisk_short}}-CLI verwenden.

### Entitätsnamen

Die Namen aller Entitäten, zu denen Aktionen, Auslöser, Regeln, Pakete und Namensbereiche gehören, sind eine Folge von Zeichen mit dem folgenden Format:

* Das erste Zeichen muss ein alphanumerisches Zeichen, eine Ziffer oder ein Unterstreichungszeichen sein.
* Die nachfolgenden Zeichen können alphanumerische Zeichen, Ziffern, Leerzeichen oder beliebige der folgenden Zeichen sein: `_`, `@`, `.`, `-`.
* Das letzte Zeichen kann kein Leerzeichen sein.

Präziser formuliert, muss der Name dem folgenden regulären Ausdruck (in Java-Metazeichensyntax) entsprechen: `\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`.


## Aktionssekmantik
{: #openwhisk_semantics}

In den folgenden Abschnitten werden Details zu {{site.data.keyword.openwhisk_short}}-Aktionen beschrieben.

### Statusunabhängigkeit

Aktionsimplementierungen sollten statusunabhängig oder *idempotent* sein. Das System setzt diese Eigenschaft zwar nicht durch, jedoch gibt es keine Garantie, dass ein Status, der von einer Aktion verwaltet wird, über Aufrufe hinweg verfügbar ist.

Darüber hinaus könnten mehrere Instanziierungen einer Aktion vorhanden sein, die jeweils einen eigenen Status haben. Ein Aktionsaufruf könnte an irgendeine dieser Instanziierungen gesendet werden.

### Aufrufeingabe und Aufrufausgabe

Die Eingabe für eine Aktion und die Ausgabe aus einer Aktion ist ein Wörterverzeichnis mit Schlüssel/Wert-Paaren. Der Schlüssel ist eine Zeichenfolge und der Wert ein gültiger JSON-Wert.

### Aufrufreihenfolge von Aktionen
{: #openwhisk_ordering}

Aufrufe einer Aktion werden nicht geordnet. Wenn der Benutzer eine Aktion zweimal über die Befehlszeile oder die REST-API aufruft, ist es möglich, dass der zweite Aufruf vor dem ersten ausgeführt wird. Wenn die Aktionen Nebeneffekte haben, werden diese möglicherweise in irgendeiner Reihenfolge beobachtet.

Darüber hinaus gibt es keine Garantie, dass Aktionen atomar ausgeführt werden. Zwei Aktionen können gleichzeitig ausgeführt werden, sodass ihre Nebeneffekte verzahnt auftreten. Alle Nebeneffekte einer gleichzeitigen Ausführung hängen von der Implementierung ab.

### Semantik des maximal einmaligen Aufrufs
{: #openwhisk_atmostonce}

Das System unterstützt maximal einen Aufruf von Aktionen.

Wenn eine Aufrufanforderung empfangen wird, zeichnet das System die Anforderung auf und sendet eine Aktivierung.

Das System gibt eine Aktivierungs-ID zurück (bei einem nicht blockierenden Aufruf), um zu bestätigen,
dass der Aufruf empfangen wurde. Beachten Sie, dass es auch bei Fehlen dieser Antwort (z. B. aufgrund
einer unterbrochenen Netzverbindung) möglich ist, dass der Aufruf empfangen wurde.

Das System versucht, die Aktion einmal aufzurufen, was zu einem der folgenden vier Ergebnisse führt:
- *success*: Der Aktionsaufruf wurde erfolgreich ausgeführt.
- *application error*: Der Aktionsaufruf war erfolgreich, jedoch hat die Aktion absichtlich einen Fehlerwert zurückzugeben, zum Beispiel weil eine Vorbedingung für die Argumente nicht erfüllt war.
- *action developer error*: Die Aktion wurde aufgerufen, aber abnormal beendet, zum Beispiel weil die Aktion eine Ausnahmebedingung nicht abgefangen hat oder weil ein Syntaxfehler vorhanden war.
- *whisk internal error*: Das System konnte die Aktion nicht aufrufen.
Das Ergebnis wird im Feld `status` des Aktivierungsdatensatzes wie im folgenden Abschnitt dokumentiert aufgezeichnet.

Jeder Aufruf, der erfolgreich empfangen wurde und der dem Benutzer möglicherweise in Rechnung gestellt wird, erhält schließlich einen Aktivierungsdatensatz.


## Aktivierungsdatensatz
{: #openwhisk_ref_activation}

Jeder Aktionsaufruf und jeder aktivierte Auslöser hat einen Aktivierungsdatensatz zur Folge.

Ein Aktivierungsdatensatz enthält die folgenden Felder:

- *activationId*: Die Aktivierungs-ID.
- *start* und *end*: Zeitmarken, die den Start und das Ende der Aktivierung aufzeichnen. Die Werte haben das [UNIX-Zeitformat](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15).
- *namespace* und `name`: Der Namensbereich und der Name der Entität.
- *logs*: Ein Array von Zeichenfolgen mit Protokollen, die durch die Aktion während ihrer Aktivierung generiert wurden. Jedes Array-Element entspricht einer Zeilenausgabe an 'stdout' oder 'stderr' durch die Aktion und enthält die Zeit und den Datenstrom der Protokollausgabe. Die Struktur sieht wie folgt aus: ```TIMESTAMP STREAM: LOG_OUTPUT```.
- *response*: Ein Wörterverzeichnis, in dem die Schlüssel `success`, `status` und `result` definiert werden:
  - *status*: Das Aktivierungsergebnis, das einen der folgenden Werte haben kann: "success", "application error", "action developer error", "whisk internal error".
  - *success*: Hat den Wert `true`, wenn und nur wenn der Status `"success"` ist.
- *result*: Ein Wörterverzeichnis, das das Aktivierungsergebnis enthält. Wenn die Aktivierung erfolgreich war, enthält es den Wert, der von der Aktion zurückgegeben wurde. Wenn die Aktivierung nicht erfolgreich war, enthält `result` garantiert den Schlüssel `error` und im Regelfall eine Erläuterung des Fehlers.


## JavaScript-Aktionen
{: #openwhisk_ref_javascript}

### Funktionsprototyp

{{site.data.keyword.openwhisk_short}}-JavaScript-Aktionen werden in einer Node.js-Laufzeit (gegenwärtig Version 0.12.9) ausgeführt.

Aktionen, die in JavaScript geschrieben sind, müssen auf eine einzige Datei beschränkt werden. Die Datei kann mehrere Funktionen enthalten, jedoch muss konventionsgemäß eine Funktion mit dem Namen `main` vorhanden sein, die aufgerufen wird, wenn die Aktion aufgerufen wird. Das folgende Beispiel zeigt eine Aktion mit mehreren Funktionen.

```
function main() {
    return { payload: helper() }
}

function helper() {
    return new Date();
}
```
{: codeblock}

Die Aktionseingabeparameter werden als JSON-Objekt an die Funktion `main` übergeben. Das Ergebnis einer erfolgreichen Aktivierung ist ebenfalls ein JSON-Objekt. Dieses Objekt wird jedoch, wie im folgenden Abschnitt beschrieben, unterschiedlich zurückgegeben, je nachdem, ob die Aktion synchron oder asynchron ausgeführt wird.


### Synchrones und asynchrones Verhalten

Es ist für JavaScript-Funktionen durchaus üblich, die Ausführung in einer Callback-Funktion fortzusetzen, auch nachdem ihre Ausführung beendet ist. Um dieser Tatsache Rechnung zu tragen, kann die Aktivierung einer JavaScript-Aktion *synchron* oder *asynchron* sein.

Die Aktivierung einer JavaScript-Aktion ist **synchron**, wenn die Funktion 'main' unter einer der folgenden Bedingungen vorhanden ist:

- Die Funktion 'main' ist vorhanden, ohne eine Anweisung ```return``` auszuführen.
- Die Funktion 'main' ist vorhanden und führt eine Anweisung ```return``` aus, die einen beliebigen Wert *mit Ausnahme von* ```whisk.async()`` zurückgibt.

Die beiden folgenden Beispiele zeigen synchrone Aktionen.

```
// Synchrone Aktion
function main() {
  return {payload: 'Hello, World!'};
}
```
{: codeblock}

```
// Aktion, bei der jeder Pfad zu einer synchronen Aktivierung führt
function main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return whisk.done();    // Gibt normale Beendigung an.
  } else if (params.payload == 2) {
    return whisk.error();   // Gibt abnormale Beendigung an.
  }
}
```
{: codeblock}

Die Aktivierung einer JavaScript-Aktion ist **asynchron**, wenn die Funktion 'main' mit einem Aufruf ```return whisk.async();``` beendet wird.  In diesem Fall nimmt das System an, dass die Aktion solange weiter ausgeführt wird, bis die Aktion eine der folgenden Anweisungen ausführt:
- ```return whisk.done();```
- ```return whisk.error();```

Das folgende Beispiel zeigt eine Aktion, die asynchron ausgeführt wird.

```
function main() {
    setTimeout(function() {
        return whisk.done({done: true});
    }, 100);
    return whisk.async();
}
```
{: codeblock}

Es ist möglich, dass eine Aktion für einige Eingaben synchron und für andere Eingaben asynchron ausgeführt wird. Beispiel:

```
  function main(params) {
      if (params.payload) {
         setTimeout(function() {
            return whisk.done({done: true});
         }, 100);
         return whisk.async();  // asynchrone Aktivierung
      }  else {
         return whisk.done();   // synchrone Aktivierung
      }
  }
```
{: codeblock}

- In diesem Fall sollte die Funktion `main` die Funktion `whisk.async()` zurückgeben. Wenn das Aktivierungsergebnis verfügbar ist, sollte die Funktion `whisk.done()` mit Übergabe des Ergebnisses als JSON-Objekt aufgerufen werden. Dies wird als *asynchrone* Aktivierung bezeichnet.

Beachten Sie, dass der Aufruf einer Aktion blockierend oder nicht blockierend sein kann, unabhängig davon, ob die Aktivierung synchron oder asynchron ist.

### Zusätzliche SDK-Methoden

Die Funktion `whisk.invoke()` ruft eine andere Aktion auf. Sie empfängt als Argument ein Wörterverzeichnis, in dem die folgenden Parameter definiert werden:

- *name*: Der vollständig qualifizierte Name der aufzurufenden Aktion.
- *parameters*: Ein JSON-Objekt, das die Eingabe für die aufgerufene Aktion darstellt. Falls nicht angegeben, wird standardmäßig ein leeres Objekt verwendet.
- *apiKey*: Der Berechtigungsschlüssel, mit dem die Aktion aufzurufen ist. Standardwert: `whisk.getAuthKey()`. 
- *blocking*: Gibt an, ob die Aktion im blockierenden oder nicht blockierenden Modus aufgerufen werden soll. Standardwert ist `false`, der einen nicht blockierenden Aufruf angibt.
- *next*: Eine optionale Callback-Funktion, die auszuführen ist, wenn der Aufruf beendet wird.

Die Signatur für `next` ist `function(error, activation)`. Dabei gilt:

- `error` ist `false`, wenn der Aufruf erfolgreich war, und ein als wahr ausgewerteter Wert, wenn der Aufruf fehlgeschlagen ist, in der Regel eine Zeichenfolge, die den Fehler beschreibt.
- Bei Fehlern kann `activation` abhängig vom Fehlermodus möglicherweise nicht definiert sein.
- Wenn `activation` definiert ist, handelt es sich um ein Wörterverzeichnis mit den folgenden Feldern:
  - *activationId*: Die Aktivierungs-ID.
  - *result*: Wenn die Aktion im blockierenden Modus aufgerufen wurde: das Aktionsergebnis als JSON-Objekt, andernfalls `undefined`.

Die Funktion `whisk.trigger()` aktiviert einen Auslöser. Sie empfängt als Argument ein JSON-Objekt mit den folgenden Parametern:

- *name*: Der vollständig qualifizierte Name des aufzurufenden Auslösers.
- *parameters*: Ein JSON-Objekt, das die Eingabe für den Auslöser darstellt. Falls nicht angegeben, wird standardmäßig ein leeres Objekt verwendet.
- *apiKey*: Der Berechtigungsschlüssel, mit dem der Auslöser aktiviert wird. Standardwert: `whisk.getAuthKey()`.
- *next*: Ein optionaler Callback, der auszuführen ist, wenn die Aktivierung des Auslösers abgeschlossen ist.

Die Signatur für `next` ist `function(error, activation)`. Dabei gilt:

- `error` ist `false`, wenn die Aktivierung des Auslösers erfolgreich war, und ein als wahr ausgewerteter Wert, wenn sie fehlgeschlagen ist, in der Regel eine Zeichenfolge, die den Fehler beschreibt.
- Bei Fehlern kann `activation` abhängig vom Fehlermodus möglicherweise nicht definiert sein.
- Wenn `activation` definiert ist, handelt es sich um ein Wörterverzeichnis, in dem ein Feld `activationId` die Aktivierungs-ID enthält.

Die Funktion `whisk.getAuthKey()` gibt den Berechtigungsschlüssel zurück, unter dem die Aktion ausgeführt wird. In der Regel müssen Sie diese Funktion nicht direkt aufrufen, weil sie implizit von den Funktionen `whisk.invoke()` und `whisk.trigger()` aufgerufen wird.

### Laufzeitumgebung
{: #openwhisk_ref_runtime_environment}

JavaScript-Aktionen werden in einer Umgebung von Node.js Version 0.12.9 ausgeführt, in der die folgenden Pakete zur Verwendung durch die Aktionen verfügbar sind:

- apn
- async
- body-parser
- btoa
- cloudant
- commander
- consul
- cookie-parser
- cradle
- errorhandler
- express
- express-session
- jade
- log4js
- merge
- moment
- mustache
- nano
- node-uuid
- oauth2-server
- process
- request
- rimraf
- semver
- serve-favicon
- socket.io
- superagent
- swagger-tools
- tmp
- watson-developer-cloud
- when
- xml2js
- xmlhttprequest
- yauzl


## Docker-Aktionen
{: #openwhisk_ref_docker}

Docker-Aktionen werden in einer vom Benutzer bereitgestellten Binärdatei in einem Docker-Container ausgeführt. Die Binärdatei wird in einem Docker-Image auf der Basis von Ubuntu 14.04 LTD ausgeführt, sodass die Binärdatei mit dieser Distribution kompatibel sein muss.

Der Aktionseingabeparameter "payload" wird als Positionsargument an das Binärprogramm übergeben und die Standardausgabe der Ausführung des Programms wird im Parameter "result" zurückgegeben.

Das Docker-Gerüst (Skeleton) ist eine bequeme Methode, {{site.data.keyword.openwhisk_short}}-kompatible Docker-Images zu erstellen. Sie können das Gerüst mit dem CLI-Befehl `wsk sdk install docker` installieren.

Das Hauptbinärprogramm muss in die Datei `dockerSkeleton/client/clientApp` kopiert werden. Alle Begleitdateien oder die Bibliothek können sich im Verzeichnis `dockerSkeleton/client` befinden.

Sie können darüber hinaus auch Kompilierungsschritte oder Abhängigkeiten einbeziehen, indem Sie die `dockerSkeleton/Dockerfile` ändern. Sie können zum Beispiel Python installieren, wenn Ihre Aktion ein Python-Script ist.


## Systembegrenzungen
{: #openwhisk_syslimits}

{{site.data.keyword.openwhisk_short}} unterliegt einigen wenigen Systembegrenzungen, wie zum Beispiel in Bezug auf die Speicherkapazität, die eine Aktion verwendet, oder auf die zulässige Anzahl von Aktionsaufrufen pro Stunde. In der folgenden Tabelle sind die Standardbegrenzungen aufgeführt.

| Begrenzung | Beschreibung | Konfigurierbar | Einheit | Standardwert |
| ----- | ----------- | ------------ | -----| ------- |
| Zeitlimit | Ein Container darf nicht länger als N Millisekunden aktiv sein. | pro Aktion |  Millisekunden | 60000 |
| Speicher | Ein Container darf nicht mehr als N MB Speicher zuordnen. | pro Aktion | MB | 256 |
| Gleichzeitig | Es ist nicht zulässig, mehr als N gleichzeitige Aufrufe pro Namensbereich zu haben. | pro Namensbereich | Anzahl | 100 |
| Minutenrate | Ein Benutzer kann nicht mehr als diese Anzahl Aktionen pro Minute aufrufen. | pro Benutzer | Anzahl | 120 |
| Stundenrate | Ein Benutzer kann nicht mehr als diese Anzahl Aktionen pro Stunde aufrufen. | pro Benutzer | Anzahl | 3600 |

### Zeitlimit pro Aktion (ms) (Standardwert: 60s)
* Das Zeitlimit N liegt im Bereich von [100ms..300000ms] und wird pro Aktion in Millisekunden festgelegt.
* Ein Benutzer kann das Limit beim Erstellen der Aktion ändern.
* Ein Container, der länger als N Millisekunden aktiv ist, wird beendet.

### Speicher pro Aktion (MB) (Standardwert: 256 MB)
* Die Speicherbegrenzung M liegt im Bereich von [128MB..512MB] und wird pro Aktion in MB festgelegt.
* Ein Benutzer kann das Limit beim Erstellen der Aktion ändern.
* Einem Container kann nicht mehr Speicher als das Limit geordnet werden.

### Anzahl gleichzeitiger Aufrufe pro Namensbereich (Anzahl) (Standardwert: 100)
* Die Anzahl der Aktivierungen, die für einen Namensbereich gleichzeitig verarbeitet werden, kann 100 nicht überschreiten.
* Die Standardbegrenzung kann von Whisk in Consul-KV-Store statisch konfiguriert werden.
* Ein Benutzer hat gegenwärtig keine Möglichkeit, die Begrenzungen zu ändern.


### Aufrufe pro Minute/Stunde (Anzahl) (Festgelegt: 120/3600)
* Die Begrenzung N der Rate ist auf 120/3600 festgelegt und begrenzt die Anzahl von Aktionsaufrufen in Fenstern von 1 Minute bzw. 1 Stunde.
* Ein Benutzer kann diese Begrenzung beim Erstellen der Aktion nicht ändern.
* Ein CLI-Aufruf, der diese Begrenzung überschreitet, empfängt einen Fehlercode, der dem Wert TOO_MANY_REQUESTS entspricht.
