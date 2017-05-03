---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Offlinemodus für node.js
{: #offline_mode}

Wenn eine node.js-Anwendung mit einer Push-Operation an {{site.data.keyword.Bluemix}} übertragen wird, lädt das Buildpack SDK for Node.js in der Regel Artefakte von externen Ressourcen herunter, wie z. B. Knotenmodule von NPM.  In einigen Situationen, wie z. B. bei [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) und [Bluemix Local](/docs/local/index.html#local) möchten Sie sich ggf. nicht auf externe Sites in Bluemix verlassen oder eine explizite Kontrolle haben.  
{: shortdesc}

Das node.js-Buildpack kann auf folgende externe Sites zugreifen. In den Bluemix-Umgebungen [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) und [Bluemix Local](/docs/local/index.html#local) müssen diese Sites *in Whitelist aufgeführt* sein.

* http://nodejs.org/ kann verwendet werden, um verfügbare Knotenengine-Versionen zu ermitteln.
* https://s3pository.heroku.com wird verwendet, um Knotenengine-Versionen abzurufen, die im Buildpack nicht enthalten sind.
*  https://www.npmjs.com/package/npm und https://semver.herokuapp.com werden verwendet, um NPM-Versionen abzurufen, die im Buildpack nicht enthalten sind.
* https://iojs.org wird verwendet, um ältere Versionen des Knotens abzurufen, die entweder im Buildpack nicht enthalten oder unter https://semver.herokuapp.com nicht verfügbar sind.
* https://registry.npmjs.org wird verwendet, um Knotenmodule wie express abzurufen.

Um die Gruppe der Whitelist-Sites zu reduzieren, konfigurieren Sie Ihre Knotenanwendungen, damit eine Knotenengine-Version verwendet werden kann, die im SDK for Node.js-Buildpack enthalten ist.  Die [letzten Aktualisierungen](./updates.html) für die Gruppe von Knotenengine-Versionen sind im Buildpack enthalten.  Anschließend muss nur noch die Site https://registry.npmjs.org die Knotenmodule herunterladen.

Denken Sie daran, dass beim Installieren der neuen Versionen des SDK for Node.js-Buildpacks sich die Gruppe der verfügbaren Knotenengine-Versionen häufig zu den neueren Versionen verschieben.  Daher müssen Sie möglicherweise Ihre Knoten-App neu konfigurieren, um eine neuere Knotenengine-Version anzugeben.


## Offlineanwendungen
{: #offline_applications}

Damit nicht mehr auf https://registry.npmjs.org zugegriffen werden muss, können Sie alle Knotenmodule einbeziehen, die Ihre Anwendung innerhalb der Anwendung benötigt.  Führen Sie dazu **npm install** für alle Module aus, die Ihre Anwendung benötigt, und schließen Sie das resultierende Verzeichnis *node_modules* mit Ihrer Push-Anwendung ein.

Beachten Sie, dass Ihre Abhängigkeiten weitere Abhängigkeiten haben können, die wiederum Abhängigkeiten haben usw., aber die Datei 'package.json' kann nur Abhängigkeiten der höchsten Ebene enthalten. Wenn eine Ihrer Abhängigkeiten einen Bereich in der Datei 'package.json' verwendet und hierzu eine neue Version freigegeben wird, können die Module dann in Ihrem Verzeichnis node_modules veraltet sein. *Shrinkwrap* unterstützt Sie, alle Abhängigkeitsversionen zu sperren, damit dies nicht auftritt.  Um Shrinkwrap zu verwenden, starten Sie mit einem leeren oder bereinigten Verzeichnis node_modules und führen Sie dann im Projektstammverzeichnis Folgendes aus:
0. npm install
1. npm dedupe
2. npm shrinkwrap

Dadurch kann die Datei *package.json* geändert und *npm-shrinkwrap.json* zum Stammverzeichnis hinzugefügt werden.
Wenn Sie die Abhängigkeiten in der Datei *package.json* ändern, wiederholen Sie die Schritte *dedupe* und *shringwrap*.

## Mit einem Proxy arbeiten
{: #working_with_proxy}

In einigen Umgebungen, wie beispielsweise [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) und [Bluemix Local](/docs/local/index.html#local), kann ein Proxy konfiguriert werden. Weitere Informationen finden Sie unter [Mit einem Proxy arbeiten](/docs/manageapps/workingWithProxy.html).
