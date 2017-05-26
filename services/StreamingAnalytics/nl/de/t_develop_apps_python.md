---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Python-Anwendungen für {{site.data.keyword.streaminganalyticsshort}} entwickeln
{: #t_develop_apps_python}

Sie können jetzt Python-Anwendungen in IBM Data Science Experience (DSX) oder in Ihrer lokalen Python-Entwicklungsumgebung entwickeln und diese Anwendungen in {{site.data.keyword.streaminganalyticsshort}} bereitstellen.
{:shortdesc}

Entwickeln Sie Python-Anwendungen und stellen Sie sie in der {{site.data.keyword.Bluemix_short}}-Cloud bereit, indem Sie den {{site.data.keyword.streaminganalyticsshort}}-Service verwenden. Verwenden Sie dazu eine der folgenden Methoden:


## Streams-Python-Anwendungen in DSX entwickeln
{: #t_develop_python_dsx}

Wenn Sie nicht über eine Python-Entwicklungsumgebung verfügen, besteht der einfachste Einstieg darin, dass Sie die Notebooks in DSX verwenden und Python-Beispielanwendungen für den {{site.data.keyword.streaminganalyticsshort}}-Service erstellen. Mit diesen Notebooks stehen die Schritte und Codebeispiele zur Verfügung, mit denen einfache Python-Anwendungen für den {{site.data.keyword.streaminganalyticsshort}}-Service innerhalb der DSX-Python-Umgebung erstellt und bereitgestellt werden können. 

* [Hello World!](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca9c6e8): Erstellen Sie als ersten Schritt eine einfache 'Hello World!'-Anwendung und stellen Sie dann die Anwendung in einer Instanz des {{site.data.keyword.streaminganalyticsshort}}-Service bereit. 

* [Demo über Gesundheitswesen](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039cad29a6): Erstellen Sie eine Anwendung, die Streaming-Daten aus einem Feed aufnimmt und analysiert und dann die Daten im Notebook visualisiert. Schließlich übergeben Sie diese Anwendung an die {{site.data.keyword.streaminganalyticsshort}}-Serviceinstanz.

* [Demo zum neuronalen Netz](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca60bb7): Erstellen Sie ein Beispieldataset, erstellen Sie ein Modell für die Beispieldaten, verwenden Sie dieses Modell in einer Streaming-Anwendung, visualisieren Sie die Streaming-Daten und übergeben Sie die Streaming-Anwendung schließlich an den {{site.data.keyword.streaminganalyticsshort}}-Service.

## Anwendungen in der lokalen Python-Umgebung entwickeln
 {: #t_develop_python_api}

 Mit der [{{site.data.keyword.streamsshort}}-Python-Anwendungs-API](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features), die im 'streamsx'-Paket enthalten ist, können Sie Streamverarbeitungsanwendungen mithilfe von aufrufbaren Python-Klassen und -Funktionen erstellen. Dann verwenden Sie die Python-Anwendungs-API, um die Anwendung zu definieren und an den Service zu übergeben.

Führen Sie zuerst die Schritte im Lernprogramm [Entwicklung für den {{site.data.keyword.streaminganalyticsshort}}-Service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) aus, um eine Beispielanwendung in der lokalen Python-Umgebung zu erstellen und diese im {{site.data.keyword.streaminganalyticsshort}}-Service bereitzustellen.
