---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}}-Systemdetails
{: #openwhisk_reference}


Die folgenden Abschnitte enthalten weitere Details zum {{site.data.keyword.openwhisk}}-System.
{: shortdesc}

## {{site.data.keyword.openwhisk_short}}-Entitäten
{: #openwhisk_entities}

### Namensbereiche und Pakete
{: #openwhisk_entities_namespaces}

Aktionen, Auslöser (Triggers) und Regeln von {{site.data.keyword.openwhisk_short}} gehören in einen Namensbereich und optional in ein Paket.

Pakete können Aktionen und Feeds enthalten. Ein Paket kann kein anderes Paket enthalten, sodass eine Paketverschachtelung nicht zulässig ist. Darüber hinaus müssen Entitäten nicht in einem Paket enthalten sein.

In Bluemix entspricht ein Paar aus Organisation und Bereich einem {{site.data.keyword.openwhisk_short}}-Namensbereich. Zum Beispiel würden die Organisation `BobsOrg` und der Bereich `dev` dem {{site.data.keyword.openwhisk_short}}-Namensbereich `/BobsOrg_dev` entsprechen.

Sie können eigene Namensbereiche erstellen, wenn Sie dazu berechtigt sind. Der Namensbereich `/whisk.system` ist für Entitäten reserviert, die mit dem {{site.data.keyword.openwhisk_short}}-System verteilt werden.


### Vollständig qualifizierte Namen
{: #openwhisk_entities_fullyqual}

Der vollständig qualifizierte Name einer Entität sieht wie folgt aus: `/Namensbereichsname[/Paketname]/Entitätsname`. Beachten Sie, dass das Zeichen `/` zum Abgrenzen von Namensbereichen, Paketen und Entitäten verwendet wird. Darüber hinaus muss Namensbereichen das Zeichen `/` als Präfix vorangestellt werden.

Aus Gründen des Komforts kann der Namensbereich weggelassen werden, wenn es sich um den *Standardnamensbereich* des Benutzers handelt.

Beispiel: Betrachten Sie einen Benutzer mit dem Standardnamensbereich `/myOrg`. Die folgenden Beispiele zeigen die vollständig qualifizierten Namen einer Reihe von Entitäten und ihre Aliasnamen.

| Vollständig qualifizierter Name | Alias | Namensbereich | Paket | Name |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` |  | `/whisk.system` | `cloudant` | `read` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `video` | `transcode` |
| `/myOrg/filter` | `filter` | `/myOrg` |  | `filter` |

Sie verwenden dieses Benennungsschema unter anderem zum Beispiel, wenn Sie die {{site.data.keyword.openwhisk_short}}-CLI verwenden.

### Entitätsnamen
{: #openwhisk_entities_names}

Die Namen aller Entitäten, zu denen Aktionen, Auslöser, Regeln, Pakete und Namensbereiche gehören, sind eine Folge von Zeichen mit dem folgenden Format:

* Das erste Zeichen muss ein alphanumerisches Zeichen oder ein Unterstreichungszeichen sein. 
* Die nachfolgenden Zeichen können alphanumerische Zeichen, Leerzeichen oder die folgenden Zeichen sein: `_`, `@`, `.`, `-`.
* Das letzte Zeichen kann kein Leerzeichen sein.

Präziser formuliert, muss der Name dem folgenden regulären Ausdruck (in Java-Metazeichensyntax) entsprechen: `\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`.


## Aktionssekmantik
{: #openwhisk_semantics}

In den folgenden Abschnitten werden Details zu {{site.data.keyword.openwhisk_short}}-Aktionen beschrieben.

### Statusunabhängigkeit
{: #openwhisk_semantics_stateless}

Aktionsimplementierungen sollten statusunabhängig oder *idempotent* sein. Das System setzt diese Eigenschaft zwar nicht durch, jedoch gibt es keine Garantie, dass ein Status, der von einer Aktion verwaltet wird, über Aufrufe hinweg verfügbar ist.

Darüber hinaus könnten mehrere Instanziierungen einer Aktion vorhanden sein, die jeweils einen eigenen Status haben. Ein Aktionsaufruf könnte an irgendeine dieser Instanziierungen gesendet werden.

### Aufrufeingabe und Aufrufausgabe
{: #openwhisk_semantics_invocationio}

Die Eingabe für eine Aktion und die Ausgabe aus einer Aktion ist ein Wörterverzeichnis mit Schlüssel/Wert-Paaren. Der Schlüssel ist eine Zeichenfolge und der Wert ein gültiger JSON-Wert.

### Aufrufreihenfolge von Aktionen
{: #openwhisk_ordering}

Aufrufe einer Aktion werden nicht geordnet. Wenn der Benutzer eine Aktion zweimal über die Befehlszeile oder die REST-API aufruft, ist es möglich, dass der zweite Aufruf vor dem ersten ausgeführt wird. Wenn die Aktionen Nebeneffekte haben, werden diese möglicherweise in irgendeiner Reihenfolge beobachtet.

Darüber hinaus gibt es keine Garantie, dass Aktionen atomar ausgeführt werden. Zwei Aktionen können gleichzeitig ausgeführt werden, sodass ihre Nebeneffekte verzahnt auftreten. OpenWhisk garantiert kein bestimmtes Konsistenzmodell für Nebeneffekte bei gleichzeitiger Ausführung. Alle Nebeneffekte einer gleichzeitigen Ausführung hängen von der Implementierung ab.

### Garantien zur Aktionsausführung
{: #openwhisk_atmostonce}

Wenn eine Aufrufanforderung empfangen wird, zeichnet das System die Anforderung auf und sendet eine Aktivierung.

Das System gibt eine Aktivierungs-ID zurück (bei einem nicht blockierenden Aufruf), um zu bestätigen, dass der Aufruf empfangen wurde.
Beachten Sie, dass bei einem Netzausfall oder bei anderen Fehlern, die auftreten, bevor Sie eine HTTP-Antwort erhalten, die Anforderung von {{site.data.keyword.openwhisk_short}} empfangen und verarbeitet werden kann.

Das System versucht, die Aktion einmal aufzurufen, was zu einem der folgenden vier Ergebnisse führt:
- *success*: Der Aktionsaufruf wurde erfolgreich ausgeführt.
- *application error*: Der Aktionsaufruf war erfolgreich, jedoch hat die Aktion absichtlich einen Fehlerwert zurückzugeben, zum Beispiel weil eine Vorbedingung für die Argumente nicht erfüllt war.
- *action developer error*: Die Aktion wurde aufgerufen, aber abnormal beendet, zum Beispiel weil die Aktion eine Ausnahmebedingung nicht erkannt hat oder weil ein Syntaxfehler vorhanden war.
- *whisk internal error*: Das System konnte die Aktion nicht aufrufen.
Das Ergebnis wird im Feld `status` des Aktivierungsdatensatzes wie im folgenden Abschnitt dokumentiert aufgezeichnet.

Jeder Aufruf, der erfolgreich empfangen wurde und der dem Benutzer möglicherweise in Rechnung gestellt wird, erhält schließlich einen Aktivierungsdatensatz.

Beachten Sie, dass bei einem *Entwicklerfehler der Aktion* die Aktion teilweise ausgeführt wurde und extern sichtbare Nebeneffekte generiert hat.   Es liegt in der Verantwortung des Benutzers, zu prüfen, ob solche Nebeneffekte auftreten, und bei Bedarf eine Retry-Logik auszugeben.   Bestimmte *interne Bearbeitungsfehler* zeigen an, dass die Ausführung einer Aktion begonnen wurde, aber das System fehlgeschlagen ist, bevor der Aktionsabschluss registriert wurde.

## Aktivierungsdatensatz
{: #openwhisk_ref_activation}

Jeder Aktionsaufruf und jeder aktivierte Auslöser hat einen Aktivierungsdatensatz zur Folge.

Ein Aktivierungsdatensatz enthält die folgenden Felder:

- *activationId*: Die Aktivierungs-ID.
- *start* und *end*: Zeitmarken, die den Start und das Ende der Aktivierung aufzeichnen. Die Werte haben das [UNIX-Zeitformat](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15).
- *namespace* und `name`: Der Namensbereich und der Name der Entität.
- *logs*: Ein Array von Zeichenfolgen mit Protokollen, die durch die Aktion während ihrer Aktivierung generiert wurden. Jedes Array-Element entspricht einer Zeilenausgabe an `stdout` oder `stderr` durch die Aktion und enthält die Zeit und den Datenstrom der Protokollausgabe. Die Struktur ist wie folgt: `TIMESTAMP STREAM: LOG_OUTPUT`.
- *response*: Ein Wörterverzeichnis, in dem die Schlüssel `success`, `status` und `result` definiert werden:
  - *status*: Das Aktivierungsergebnis, das einen der folgenden Werte haben kann: "success", "application error", "action developer error", "whisk internal error".
  - *success*: Hat den Wert `true`, wenn und nur wenn der Status `"success"` ist.
- *result*: Ein Wörterverzeichnis, das das Aktivierungsergebnis enthält. Wenn die Aktivierung erfolgreich war, enthält es den Wert, der von der Aktion zurückgegeben wurde. Wenn die Aktivierung nicht erfolgreich war, enthält `result` den Schlüssel `error` und im Regelfall eine Erläuterung des Fehlers.


## JavaScript-Aktionen
{: #openwhisk_ref_javascript}

### Funktionsprototyp
{: #openwhisk_ref_javascript_fnproto}

{{site.data.keyword.openwhisk_short}}-JavaScript-Aktionen werden in einer Node.js-Laufzeit ausgeführt.

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
{: #openwhisk_ref_javascript_synchasynch}

Es ist für JavaScript-Funktionen durchaus üblich, die Ausführung in einer Callback-Funktion fortzusetzen, auch nachdem ihre Ausführung beendet ist. Um dieser Tatsache Rechnung zu tragen, kann die Aktivierung einer JavaScript-Aktion *synchron* oder *asynchron* sein.

Die Aktivierung einer JavaScript-Aktion ist **synchron**, wenn die Funktion 'main' unter einer der folgenden Bedingungen vorhanden ist:

- Die Funktion 'main' ist ohne Ausführung der Anweisung `return` vorhanden.
- Die Funktion 'main' ist vorhanden und führt die Anweisung `return` aus, die einen beliebigen Wert *mit Ausnahme eines* Promise zurückgibt.

Das folgende Beispiel zeigt eine synchrone Aktion.

```
// Aktion, bei der jeder Pfad zu einer synchronen Aktivierung führt
function main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return {payload: 'Hello, World!'};
  } else if (params.payload == 2) {
    return {error: 'payload must be 0 or 1'};
  }
}
```
{: codeblock}

Die Aktivierung einer JavaScript-Aktion ist **asynchron**, wenn die Funktion 'main' mit der Rückgabe eines  Promise beendet wird.  In diesem Fall nimmt das System an, dass die Aktion solange weiter ausgeführt wird, bis das Promise erfüllt oder abgelehnt wurde.
Beginnen Sie, indem Sie ein neues Promise-Objekt instanziieren und an eine Callback-Funktion übergeben. Der Callback verwendet zwei Argumente ('resolve' und 'reject'), die beide Funktionen sind. Der gesamte asynchrone Code geht in den Callback ein.


Das folgende Beispiel zeigt, wie ein Promise durch Aufruf der Funktion 'resolve' erfüllt wird.

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
         resolve({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

Das folgende Beispiel zeigt, wie ein Promise durch Aufruf der Funktion 'reject' zurückgewiesen wird.

```
function main(args) {
     return new Promise(function(resolve, reject) {
       setTimeout(function() {
         reject({ done: true });
       }, 100);
    })
 }
```
{: codeblock}

Es ist möglich, dass eine Aktion für einige Eingaben synchron und für andere Eingaben asynchron ausgeführt wird. Beispiel:

```
  function main(params) {
      if (params.payload) {
         // asynchronous activation
         return new Promise(function(resolve, reject) {
                setTimeout(function() {
                  resolve({ done: true });
                }, 100);
             })
      } else {
         // synchronous activation
         return {done: true};
      }
  }
```
{: codeblock}

Beachten Sie, dass der Aufruf einer Aktion blockierend oder nicht blockierend sein kann, unabhängig davon, ob die Aktivierung synchron oder asynchron ist.

### Globales JavaScript-Objekt 'whisk' wurde entfernt

Das globale Objekt `whisk` wurde entfernt. Migrieren Sie Ihre Node.js-Aktionen, um alternative Methoden zu verwenden.
Verwenden Sie für die Funktionen `whisk.invoke()` und `whisk.trigger()` die bereits installierte Clientbibliothek [openwhisk](https://www.npmjs.com/package/openwhisk).
Für `whisk.getAuthKey()` können Sie den API-Schlüsselwert aus der Umgebungsvariablen `__OW_API_KEY` abrufen.
Für `whisk.error()` können Sie ein abgelehntes Objekt des Typs 'Promise' zurückgeben (d. h. Promise.reject).

### JavaScript-Laufzeitumgebungen
{: #openwhisk_ref_javascript_environments}

JavaScript-Aktionen werden standardmäßig in einer Node.js Version 6.9.1-Umgebung ausgeführt.  Die 6.9.1-Umgebung wird außerdem für eine Aktion verwendet, wenn das Flag `--kind` bei der Erstellung oder Aktualisierung der Aktion explizit mit dem Wert 'nodejs:6' angegeben wird.
In der Node.js Version 6.9.1-Umgebung können die folgenden Pakete verwendet werden:

- apn v2.1.2
- async v2.1.4
- btoa v1.1.2
- cheerio v0.22.0
- cloudant v1.6.2
- commander v2.9.0
- consul v0.27.0
- cookie-parser v1.4.3
- cradle v0.7.1
- errorhandler v1.5.0
- glob v7.1.1
- gm v1.23.0
- lodash v4.17.2
- log4js v0.6.38
- iconv-lite v0.4.15
- marked v0.3.6
- merge v1.2.0
- moment v2.17.0
- mongodb v2.2.11
- mustache v2.3.0
- nano v6.2.0
- node-uuid v1.4.7
- nodemailer v2.6.4
- oauth2-server v2.4.1
- openwhisk v3.3.2
- pkgcloud v1.4.0
- process v0.11.9
- pug v2.0.0-beta6
- redis v2.6.3
- request v2.79.0
- request-promise v4.1.1
- rimraf v2.5.4
- semver v5.3.0
- sendgrid v4.7.1
- serve-favicon v2.3.2
- socket.io v1.6.0
- socket.io-client v1.6.0
- superagent v3.0.0
- swagger-tools v0.10.1
- tmp v0.0.31
- twilio v2.11.1
- underscore v1.8.3
- uuid v3.0.0
- validator v6.1.0
- watson-developer-cloud v2.9.0
- when v3.7.7
- winston v2.3.0
- ws v1.1.1
- xml2js v0.4.17
- xmlhttprequest v1.8.0
- yauzl v2.7.0


## Python-Laufzeitumgebungen
{: #openwhisk_ref_python_environments}

OpenWhisk unterstützt die Ausführung von Python-Aktionen mit zwei verschiedenen Laufzeitversionen. 

### Python 3-Aktionen

Python 3-Aktionen werden mit Python 3.6.1 ausgeführt. Zur Verwendung dieser Laufzeit geben Sie den Parameter `--kind python:3` in der `wsk`-Befehlszeilenschnittstelle an, wenn Sie eine Aktion erstellen oder aktualisieren.
Die folgenden Pakete sind neben den Standardbibliotheken von Python 3.6 zur Verwendung durch Python-Aktionen verfügbar: 

- aiohttp v1.3.3
- appdirs v1.4.3
- asn1crypto v0.21.1
- async-timeout v1.2.0
- attrs v16.3.0
- beautifulsoup4 v4.5.1
- cffi v1.9.1
- chardet v2.3.0
- click v6.7
- cryptography v1.8.1
- cssselect v1.0.1
- Flask v0.12
- gevent v1.2.1
- greenlet v0.4.12
- httplib2 v0.9.2
- idna v2.5
- itsdangerous v0.24
- Jinja2 v2.9.5
- kafka-python v1.3.1
- lxml v3.6.4
- MarkupSafe v1.0
- multidict v2.1.4
- packaging v16.8
- parsel v1.1.0
- pyasn1 v0.2.3
- pyasn1-modules v0.0.8
- pycparser v2.17
- PyDispatcher v2.0.5
- pyOpenSSL v16.2.0
- pyparsing v2.2.0
- python-dateutil v2.5.3
- queuelib v1.4.2
- requests v2.11.1
- Scrapy v1.1.2
- service-identity v16.0.0
- simplejson v3.8.2
- six v1.10.0
- Twisted v16.4.0
- w3lib v1.17.0
- Werkzeug v0.12
- yarl v0.9.8
- zope.interface v4.3.3

### Python 2-Aktionen

Python 2-Aktionen werden mit Python 2.7.12 ausgeführt. Dies ist die Standardlaufzeit für Python-Aktionen, sofern Sie nicht das Flag `--kind` beim Erstellen oder Aktualisieren einer Aktion angeben. Wenn Sie diese Laufzeit explizit auswählen wollen, verwenden Sie das Flag `--kind python:2`. Die folgenden Pakete sind neben der Standardbibliothek von Python 2.7 zur Verwendung durch Python 2-Aktionen verfügbar: 

- appdirs v1.4.3
- asn1crypto v0.21.1
- attrs v16.3.0
- beautifulsoup4 v4.5.1
- cffi v1.9.1
- click v6.7
- cryptography v1.8.1
- cssselect v1.0.1
- enum34 v1.1.6
- Flask v0.11.1
- gevent v1.1.2
- greenlet v0.4.12
- httplib2 v0.9.2
- idna v2.5
- ipaddress v1.0.18
- itsdangerous v0.24
- Jinja2 v2.9.5
- kafka-python v1.3.1
- lxml v3.6.4
- MarkupSafe v1.0
- packaging v16.8
- parsel v1.1.0
- pyasn1 v0.2.3
- pyasn1-modules v0.0.8
- pycparser v2.17
- PyDispatcher v2.0.5
- pyOpenSSL v16.2.0
- pyparsing v2.2.0
- python-dateutil v2.5.3
- queuelib v1.4.2
- requests v2.11.1
- Scrapy v1.1.2
- service-identity v16.0.0
- simplejson v3.8.2
- six v1.10.0
- Twisted v16.4.0
- virtualenv v15.1.0
- w3lib v1.17.0
- Werkzeug v0.12
- zope.interface v4.3.3

## Docker-Aktionen
{: #openwhisk_ref_docker}

Docker-Aktionen werden in einer vom Benutzer bereitgestellten Binärdatei in einem Docker-Container ausgeführt. Die Binärdatei wird in einem Docker-Image auf der Basis von [python:2.7.12-alpine](https://hub.docker.com/r/library/python) ausgeführt, sodass die Binärdatei mit dieser Distribution kompatibel sein muss.

Das Docker-Gerüst (Skeleton) ist eine bequeme Methode, OpenWhisk-kompatible Docker-Images zu erstellen. Sie können das Gerüst mit dem CLI-Befehl `wsk sdk install docker` installieren.

Das Hauptbinärprogramm muss sich in `/action/exec` im Container befinden. Die ausführbare Datei empfängt die Eingabeargumente über `stdin` und muss über `stdout` ein Ergebnis zurückgeben.

Sie können darüber hinaus auch Kompilierungsschritte oder Abhängigkeiten einbeziehen, indem Sie die `Dockerfile` in `dockerSkeleton` ändern.

## REST-API
{: #openwhisk_ref_restapi}

Alle Funktionen im System stehen über eine REST-API zur Verfügung. Es gibt Sammlungs- und Entitätsendpunkte für Aktionen, Auslöser, Regeln, Pakete, Aktivierungen und Namensbereiche.

Die Sammlungsendpunkte lauten wie folgt:

- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/actions`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/triggers`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/rules`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/packages`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/activations`

`openwhisk.`<span class="keyword" data-hd-keyref="DomainName">DomainName</span>` ist der OpenWhisk-API-Hostname (z. B. openwhisk.ng.bluemix.net, 172.17.0.1 usw.).

Für `{namespace}` kann das Zeichen `_` zum Angeben des *Standardnamensbereichs* (d.h. einer E-Mail-Adresse) verwendet werden.

Sie können eine GET-Anforderung für die Sammlungsendpunkte ausführen, um eine Liste der Entitäten in der Sammlung abzurufen.

Für jeden Entitätstyp gibt es Entitätsendpunkte:

- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/actions/[{packageName}/]{actionName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/triggers/{triggerName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/rules/{ruleName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/packages/{packageName}`
- `https://`openwhisk.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>`/api/v1/namespaces/{namespace}/activations/{activationName}`


Die Endpunkte für Namensbereiche und Aktivierungen unterstützen nur GET-Anforderungen. Die Endpunkte für Aktionen, Auslöser, Regeln und Pakete unterstützen GET-, PUT- und DELETE-Anforderungen. Die Endpunkte für Aktionen, Auslöser und Regeln unterstützen auch POST-Anforderungen, die zum Aufrufen von Aktionen und Auslösern sowie zum Aktivieren und Inaktivieren von Regeln verwendet werden. Weitere Details hierzu finden Sie in der [API-Referenz](https://new-console.{DomainName}/apidocs/98).

Alle APIs sind mit der HTTP-Basisauthentifizierung geschützt. Die durch einen Doppelpunkt voneinander getrennten Basic-Berechtigungsnachweise zur Authentifizierung befinden sich in der Eigenschaft `AUTH` in der `~/.wskprops`-Datei. Sie finden diese Berechtigungsnachweise auch in den [Konfigurationsschritten der Befehlszeilenschnittstelle (CLI)](./index.html#openwhisk_start_configure_cli).

Das folgende Beispiel zeigt, wie Sie mit dem Befehl 'cURL' eine Liste aller Pakete im Namensbereich `whisk.system` abrufen können:

```
curl -u USERNAME:PASSWORD https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/packages
```
{: pre}
```
[
  {
    "name": "slack",
    "binding": false,
    "publish": true,
    "annotations": [
      {
        "key": "description",
        "value": "Package that contains actions to interact with the Slack messaging service"
      }
    ],
    "version": "0.0.9",
    "namespace": "whisk.system"
  },
  ...
]
```
{: screen}

Von der OpenWhisk-API werden Anforderung/Antwort-Aufrufe von Web-Clients unterstützt. Von OpenWhisk wird auf `OPTIONS`-Anforderungen mit CORS-Headern (CORS - Cross-Origin Resource Sharing) geantwortet. Derzeit sind alle Ursprünge zulässig (d. h. Access-Control-Allow-Origin ist "`*`") und Access-Control-Allow-Header sorgen für die Autorisierung und den Inhaltstyp.

**Achtung:** Da von OpenWhisk derzeit nur ein Schlüssel pro Konto unterstützt wird, wird empfohlen, CORS nur für einfache Experimente und nicht darüber hinaus zu verwenden. Der Schlüssel müsste sonst in clientseitigen Code eingebettet werden, was ihn öffentlich zugänglich machen würde. Verwenden Sie ihn mit Sorgfalt.

## Systembegrenzungen
{: #openwhisk_syslimits}

### Aktionen
{{site.data.keyword.openwhisk_short}} unterliegt einigen wenigen Systembegrenzungen, wie zum Beispiel in Bezug auf die Speicherkapazität, die eine Aktion verwenden kann, oder auf die zulässige Anzahl von Aktionsaufrufen pro Minute.

n der folgenden Tabelle sind die Standardbegrenzungen für Aktionen aufgeführt.

| Begrenzung | Beschreibung | Konfigurierbar | Einheit | Standardwert |
| ----- | ----------- | ------------ | -----| ------- |
| Zeitlimit | Ein Container darf nicht länger als N Millisekunden aktiv sein. | pro Aktion |  Millisekunden | 60000 |
| Speicher | Ein Container darf nicht mehr als N MB Speicher zuordnen. | pro Aktion | MB | 256 |
| Protokolle | Ein Container darf nicht mehr als N MB in die Standardausgabe schreiben. | pro Aktion | MB | 10 |
| Gleichzeitig | Pro Namensbereich können nicht mehr als N aktuell ausgeführte oder in die Warteschlange für die Ausführung gestellte Aktivierungen übergeben werden. | pro Namensbereich | Anzahl | 1000 |
| Minutenrate | Pro Namensbereich können nicht mehr als N Aktivierungen pro Minute übergeben werden. | pro Benutzer | Anzahl | 5000 |
| Codegröße | Die maximale Größe des Aktionscodes. | nicht konfigurierbar, Limit pro Aktion | MB | 48 |
| Parameter | Die maximale Größe der Parameter, die angehängt werden können. | nicht konfigurierbar, Limit pro Aktion/Paket/Auslöser | MB | 1 |

### Zeitlimit pro Aktion (ms) (Standardwert: 60s)
{: #openwhisk_syslimits_timeout}
* Das Zeitlimit N liegt im Bereich von [100ms..300000ms] und wird pro Aktion in Millisekunden festgelegt.
* Ein Benutzer kann das Limit beim Erstellen der Aktion ändern.
* Ein Container, der länger als N Millisekunden aktiv ist, wird beendet.

### Speicher pro Aktion (MB) (Standardwert: 256 MB)
{: #openwhisk_syslimits_memory}
* Die Speicherbegrenzung M liegt im Bereich von [128MB..512MB] und wird pro Aktion in MB festgelegt.
* Ein Benutzer kann das Limit beim Erstellen der Aktion ändern.
* Einem Container kann nicht mehr Speicher als das Limit geordnet werden.

### Protokolle pro Aktion (MB) (Standardwert: 10 MB)
{: #openwhisk_syslimits_logs}
* Die Protokollbegrenzung N liegt im Bereich von [0MB..10MB] und wird pro Aktion festgelegt.
* Ein Benutzer kann das Limit beim Erstellen oder Aktualisieren der Aktion ändern.
* Protokolle, die das festgelegte Limit überschreiten, werden abgeschnitten. Ferner wird als letzte Ausgabe der Aktivierung eine Warnung hinzugefügt, um darauf hinzuweisen, dass die Aktivierung die festgelegte Protokollbegrenzung überschritten hat.

### Artefakt pro Aktion (MB) (Festgelegt: 48 MB)
{: #openwhisk_syslimits_artifact}
* Die maximale Codegröße für die Aktion ist 48 MB.
* Es wird empfohlen, für eine JavaScript-Aktion ein Tool zum Verketten des gesamten Quellcodes, einschließlich der Abhängigkeiten, in einer einzelnen Bundledatei zu verwenden.

### Nutzdatengröße (MB) pro Aktivierung (Festgelegt: 1 MB)
{: #openwhisk_syslimits_activationsize}
* Die maximale POST-Inhaltsgröße plus alle umgewandelten Parameter für einen Aktionsaufruf oder eine Auslöseraktivierung ist 1 MB.

### Gleichzeitige Aufrufe pro Namensbereich (Standardwert: 1000)
{: #openwhisk_syslimits_concur}
* Die Anzahl der Aktivierungen, die für einen Namensbereich entweder ausgeführt oder in die Warteschlange für die Ausführung gestellt werden, kann 1000 nicht überschreiten.
* Die Standardbegrenzung kann von Whisk in Consul-KV-Store statisch konfiguriert werden.
* Ein Benutzer hat gegenwärtig keine Möglichkeit, die Begrenzungen zu ändern.

### Aufrufe pro Minute (Festgelegt: 5000)
{: #openwhisk_syslimits_invocations}
* Die Begrenzung N der Rate ist auf 5000 festgelegt und begrenzt die Anzahl von Aktionsaufrufen in Fenstern von 1 Minute.
* Ein Benutzer kann diese Begrenzung beim Erstellen der Aktion nicht ändern.
* Ein CLI- oder API-Aufruf, der diese Begrenzung überschreitet, empfängt einen Fehlercode, der dem HTTP-Statuscode `429: TOO MANY REQUESTS` entspricht.

### Größe der Parameter (Festgelegt: 1 MB)
{: #openwhisk_syslimits_parameters}
* Das Größenlimit für die Parameter bei der Erstellung oder Aktualisierung einer Aktion, eines Pakets oder eines Auslösers ist 1 MB.
* Das Limit kann vom Benutzer nicht geändert werden.
* Eine Entität mit Parametern, die das Größenlimit überschreiten, wird bei der Erstellung oder Aktualisierung zurückgewiesen.

### Wert für 'ulimit' für offene Dateien pro Docker-Aktion (Festgelegt: 64:64)
{: #openwhisk_syslimits_openulimit}
* Die maximale Anzahl offener Dateien beträgt 64 (bezieht sich auf feste und veränderliche Grenzwerte).
* Vom Docker-Ausführungsbefehl wird das Argument `--ulimit nofile=64:64` verwendet.
* Weitere Informationen zu 'ulimit' für offene Dateien finden Sie in der Docker-Dokumentation unter [run](https://docs.docker.com/engine/reference/commandline/run).

### Wert für 'ulimit' für Prozesse pro Docker-Aktion (Festgelegt: 512:512)
{: #openwhisk_syslimits_proculimit}
* Die maximale Anzahl der für einen Benutzer verfügbaren Prozesse beträgt 512 (bezieht sich auf feste und veränderliche Grenzwerte).
* Vom Docker-Ausführungsbefehl wird das Argument `--ulimit nproc=512:512` verwendet.
* Weitere Informationen zu 'ulimit' für die maximale Anzahl an Prozessen finden Sie in der Docker-Dokumentation unter [run](https://docs.docker.com/engine/reference/commandline/run).

### Auslöser

Auslöser unterliegen einer Auslöserate pro Minute (wie in der folgenden Tabelle angegeben).

| Begrenzung | Beschreibung | Konfigurierbar | Einheit | Standardwert |
| ----- | ----------- | ------------ | -----| ------- |
| Minutenrate | Pro Namensbereich können nicht mehr als N Auslöser pro Minute aktiviert werden. | pro Benutzer | Anzahl | 5000 |

### Auslöser pro Minute (Festgelegt: 5000)
* Die Begrenzung N der Rate ist auf 5000 festgelegt und begrenzt die Anzahl von Auslösern in Fenstern von 1 Minute.
* Ein Benutzer kann diese Begrenzung beim Erstellen des Auslösers nicht ändern.
* Ein CLI- oder API-Aufruf, der diese Begrenzung überschreitet, empfängt einen Fehlercode, der dem HTTP-Statuscode `429: TOO MANY REQUESTS` entspricht.
