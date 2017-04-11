---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Starteranwendung in {{site.data.keyword.Bluemix_short}} ändern
{: #modifying_starter_app}

Sie können die Starteranwendung ändern und anschließend erneut in {{site.data.keyword.Bluemix_short}} bereitstellen, um die Ergebnisse anzuzeigen.
{:shortdesc}


Eine einfache Änderung ist die Erhöhung oder Entfernung des Ereignisgrenzwerts in der Starteranwendung, damit diese länger ausgeführt wird.

1. Öffnen Sie app.js in einem Texteditor oder in einer Entwicklungsumgebung.
2. Ändern Sie die Variable 'eventTarget' oder löschen Sie diese Zeile, um den Ereignisgrenzwert ganz zu entfernen.
	 <pre><code>var eventTarget = 100;</code></pre>
3. Wenn Sie den Ereignisgrenzwert entfernen möchten, müssen Sie auch die folgende if-Anweisung löschen:
	 <pre><code>  
	if (eventCount >= eventTarget) {
		    status_step[3] = "Completed";
		    console.log("\nTarget event count has been reached.  Geospatial Analytics service will be stopped.\n");
		    callback(null, null);
		    } 
	</code></pre> 
4. Stellen Sie die geänderte Anwendung mit dem Befehl 'cf push' erneut in {{site.data.keyword.Bluemix_short}} bereit.
	 <pre><code>  
	cf push myapp
	</code></pre>
5. Geben Sie die URL oder "Route" der Anwendung in den Browser ein oder starten Sie sie im {{site.data.keyword.Bluemix_short}}-Dashboard.
