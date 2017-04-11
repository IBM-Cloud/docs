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

#Starteranwendungen für {{site.data.keyword.Bluemix_short}} bereitstellen
{: #starterapps_deploy}

Sie können eine der {{site.data.keyword.streaminganalyticsshort}}-Starteranwendungen
an die {{site.data.keyword.Bluemix_short}}-Cloud
übertragen und dort bereitstellen.
{:shortdesc}

Bereiten Sie {{site.data.keyword.Bluemix_short}} im Voraus für das Bereitstellen der
{{site.data.keyword.streaminganalyticsshort}}-Starteranwendungen vor:

* [Installieren Sie das Befehlszeilentool 'cf'](https://github.com/cloudfoundry/cli/releases).
* Erstellen Sie eine Anwendung in {{site.data.keyword.Bluemix_short}}, fügen Sie Ihrer Anwendung
den {{site.data.keyword.streaminganalyticsshort}}-Service hinzu und
führen Sie ein erneutes Staging der Anwendung durch:
	* Um die Starter-App 'Event Detection' bereitzustellen, erstellen Sie eine Anwendung mit der {{site.data.keyword.sdk4node}}-Laufzeitumgebung.
	* Um die Starter-App 'NYC Traffic' bereitzustellen, erstellen Sie eine Anwendung mit der Liberty for Java™-Laufzeitumgebung.

Merken Sie sich den Namen, den Sie der Anwendung geben. Sie benötigen ihn zu einem späteren Zeitpunkt wieder.

{{site.data.keyword.streaminganalyticsshort}} stellt zwei Beispielanwendungen zur Verfügung,
die Ihnen den Einstieg in die Arbeit mit dem Service erleichtern. 

Die Starteranwendung "Event Detection" analysiert wetterbezogene Daten in einem Echtzeitstream
und zeigt den Status und die Ergebnisse der Analyse an. Die Anwendung ist in {{site.data.keyword.sdk4node}} geschrieben. Nähere Informationen zur Verwendung der Starteranwendung "Event Detection" finden Sie unter
[Detect complex events in a real-time data stream](https://www.ibm.com/developerworks/library/ba-bluemix-detect-complex-events-from-data-stream-trs/index.html).

Die Starteranwendung 'NYC Traffic' liest und analysiert Verkehrsdaten von einer öffentlichen Website. Die Anwendung ist in Liberty for Java™ geschrieben. Nähere Informationen zur Verwendung der Starter-App 'NYC Traffic' finden Sie unter [{{site.data.keyword.streaminganalyticsfull}} Starter Application](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/). 

Gehen Sie wie folgt vor, um die Starteranwendung für {{site.data.keyword.Bluemix_short}}
herunterzuladen und bereitzustellen:

1. Laden Sie die Starteranwendung [Event Detection](https://hub.jazz.net/project/streamscloud/EventDetection/overview) oder [ NYC Traffic](https://hub.jazz.net/project/streamscloud/NYCTraffic/overview) herunter.
2. Wechseln Sie über die Befehlszeile in das Projektverzeichnis.
  <pre><code>cd myapp</code></pre>
 
3. Benennen Sie das Projektverzeichnis um, sodass der Name mit dem Namen übereinstimmt, den Sie Ihrer Anwendung
in {{site.data.keyword.Bluemix_short}} gegeben haben.
4. Stellen Sie eine Verbindung zu {{site.data.keyword.Bluemix_short}} her:
  <pre><code>cf api https://api.DomainName</code></pre>
   
5. Melden Sie sich bei {{site.data.keyword.Bluemix_short}} an und legen Sie Ihre Zielorganisation fest,
wenn Sie dazu aufgefordert werden:
   <pre><code>cf login</code></pre>
    
6. Stellen Sie Ihre Anwendung bereit:
  <pre><code>cf push myapp</code></pre>
   
7. Navigieren Sie zur Seite mit der Anwendungsübersicht, auf die Sie über das {{site.data.keyword.Bluemix_short}}-Dashboard gelangen, und prüfen Sie, ob Ihre Anwendung erfolgreich gestartet wurde.
8. Starten Sie Ihre Anwendung, sodass sie im Browser zu sehen ist. Die URL (oder "Route") zu Ihrer Anwendung finden Sie auf der Seite mit der Anwendungsübersicht.

Wenn Ihre App ausgeführt wird, können Sie zum Service-Dashboard wechseln, um den Status Ihrer {{site.data.keyword.streaminganalyticsshort}}-Instanz anzuzeigen und um Informationen zur Fehlerbehebung anzufordern. Um auf das Service-Dashboard zuzugreifen, wechseln Sie zum {{site.data.keyword.Bluemix_short}}-Dashboard und klicken Sie auf die {{site.data.keyword.streaminganalyticsshort}}-Kachel auf der Seite mit der Anwendungsübersicht.
