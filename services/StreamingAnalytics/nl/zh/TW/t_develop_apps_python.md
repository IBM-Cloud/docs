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

# 針對 {{site.data.keyword.streaminganalyticsshort}} 開發 Python 應用程式
{: #t_develop_apps_python}

您現在可以在 IBM Data Science Experience (DSX) 或您的本端 Python 開發環境中開發 Python 應用程式，並在 {{site.data.keyword.streaminganalyticsshort}} 部署這些應用程式。
{:shortdesc}

使用 {{site.data.keyword.streaminganalyticsshort}} 服務和下列其中一個方法，開發 Python 應用程式並部署至 {{site.data.keyword.Bluemix_short}} 雲端：


## 在 DSX 中開發 Streams Python 應用程式
{: #t_develop_python_dsx}

如果您沒有 Python 開發環境，最容易開始的方法是在 DSX 中使用我們的記事本，並為 {{site.data.keyword.streaminganalyticsshort}} 服務建立範例 Python 應用程式。這些記事本提供步驟和程式碼範例，以便針對 {{site.data.keyword.streaminganalyticsshort}} 服務，在 DSX Python 環境內建立及部署簡單的 Python 應用程式：

* [Hello World!](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca9c6e8)：建立簡單的 Hello World! 應用程式以便開始，然後將應用程式部署到 {{site.data.keyword.streaminganalyticsshort}} 服務的實例。

* [Healthcare Demo](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039cad29a6)：建立應用程式來吸收並分析資訊來源的串流資料，然後在記事本中視覺化該資料。最後，將此應用程式提交至 {{site.data.keyword.streaminganalyticsshort}} 服務實例。

* [Neural Net Demo](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca60bb7)：建立範例資料集、建立範例資料的模型、在串流應用程式中使用該模型、將串流資料視覺化，最後將串流應用程式提交至 {{site.data.keyword.streaminganalyticsshort}} 服務。

## 在本端 Python 環境中開發應用程式
 {: #t_develop_python_api}

 [{{site.data.keyword.streamsshort}} Python Application API](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features)（它包含在 streamsx 套件中），能讓您使用 Python 可呼叫類別或函數建立串流處理應用程式。然後您使用 Python Application API 來定義和提交應用程式至服務。

從遵循 [Developing for the {{site.data.keyword.streaminganalyticsshort}} service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) 指導教學中的步驟開始，在您的本端 Python 環境建立範例應用程式，然後將它部署至 {{site.data.keyword.streaminganalyticsshort}} 服務。
