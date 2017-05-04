---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Hinweise für die lokale Ausführung Ihrer Node.js-Anwendung
{: #hints}

Mithilfe dieser Informationen können Sie die Ausführung Ihrer Node.js-Anwendung lokal oder in Bluemix vereinfachen.{: shortdesc}

Im folgenden Beispiel wird ein Teil der Quelle für eine **js**-Datei gezeigt:
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

Wenn die Anwendung bei diesem Code in Bluemix ausgeführt wird, enthält die Umgebungsvariable PORT den internen Portwert von Bluemix , auf dem die App für eingehende Verbindungen empfangsbereit ist. Bei lokaler Ausführung der Anwendung ist die Umgebungsvariablen PORT nicht definiert, sodass **3000** als Portnummer verwendet wird. Durch diese Schreibung können Sie die Anwendung sowohl lokal für Testzwecke als auch in Bluemix ausführen, ohne Änderungen vornehmen zu müssen.
