---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Verfügbare Versionen
{: #available_versions}

{{site.data.keyword.Bluemix}} stellt alle [zurzeit verfügbaren Node.js-Laufzeiten](http://nodejs.org/dist/) zur Verfügung. Davon stellt IBM Versionen zur Verfügung, die Erweiterungen und Fehlerkorrekturen enthalten. Weitere Informationen finden Sie in [Neueste Aktualisierungen für das Node.js-Buildpack](/docs/runtimes/nodejs/updates.html).{: shortdesc}

Das IBM Node.js-Buildpack stellt die IBM Laufzeitversionen in den Cache. Verwenden Sie die IBM SDK for Node.js-Laufzeit also in Ihrer Anwendung, erhalten Sie eine bessere Anwendungsleistung, wenn Ihre Anwendung mit einer Push-Operation an Bluemix übertragen wird.

Verwenden Sie den Parameter **node** im Abschnitt **engines** der Datei **package.json**, um die Version der Node.js-Laufzeit anzugeben, die Sie ausführen möchten.

Verwenden Sie den Parameter **npm** im Abschnitt **engines** der Datei **package.json**, wenn Sie eine andere als die mit Node.js im Paket vorhandene Version von 'npm' verwenden müssen.  

Lesen Sie folgendes Beispiel:

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}

Für 'node' muss in der Datei **package.json** stets eine Version angegeben werden. Ist das nicht der Fall, wird die neueste Knotenversion verwendet.
