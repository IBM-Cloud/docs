---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 開始使用 {{site.data.keyword.graphfull}}
{: #gettingstartedtemplate}
前次更新：2016年7月27日
{: .last-updated}

{{site.data.keyword.graphfull}} 是完全受管理的圖形資料庫服務，可透過以 REST 為基礎的 HTTP API 介面存取。請使用它來建置需要圖形資料庫功能的行動式和 Web 應用程式。
{:shortdesc}

{{site.data.keyword.graphfull}} 是以 [Apache TinkerPop](http://tinkerpop.incubator.apache.org/)&trade;
堆疊為基礎，用來建置使用 v3 相容 API 的高效能圖形應用程式。堆疊讓您具有以熟悉環境為基礎的額外彈性及功能。使用 {{site.data.keyword.Bluemix}} 儀表板，您可以輕鬆整合
{{site.data.keyword.graphfull}} 服務與 {{site.data.keyword.Bluemix_short}} 應用程式。

您可以用兩種方式使用 {{site.data.keyword.graphfull}}：

*	使用 {{site.data.keyword.graphfull}} 簡化 API 指令。
*	使用完整 Apache TinkerPop v3 查詢語言 (Gremlin)。

{{site.data.keyword.graphfull}} 特性可以透過使用 HTTP REST 端點的方式來使用。這些端點提供輕鬆的方式，使用 HTTP 提出 API 要求並獲得結果，藉以讓您的應用程式連接並使用
{{site.data.keyword.graphfull}} 服務。請使用您所選應用程式設計語言所提供的 HTTP 函數來存取端點。
或者，您可以使用指令介面或 `curl` Script 達到相同的效果。「API 參考資料」說明 {{site.data.keyword.graphfull}}
服務提供的各種函數，以及它們的使用範例。

您的應用程式也可以針對使用 {{site.data.keyword.graphfull}} 服務的作業，使用 Apache TinkerPop
查詢語言（稱為 Gremlin）。請將 Gremlin 查詢包含在 JSON 文件中，然後將該文件傳遞到 `/gremlin` 服務端點。使用
Gremlin 搭配 {{site.data.keyword.graphfull}} 的範例提供於完整文件中。

完成這些步驟以開始使用 {{site.data.keyword.graphfull}} 服務：

1.	針對 {{site.data.keyword.graphfull}} 服務[建立實例](https://www.ng.bluemix.net/docs/services/reqnsi.html#req_instance)。
2.	記錄在實例建立時產生的三個重要值。按一下服務磚之後可以從`服務認證`標籤取得值。
	*	IBM Graph 端點：`apiURL`。
	*	服務實例使用者名稱 `username`。
	*	服務實例密碼 `password`。
3.	請在應用程式或 Script 中使用這三個重要值進行 {{site.data.keyword.graphfull}} 作業。範例提供於完整文件中。

# 相關鏈結
{: #rellinks}

## 指導教學及範例
{: #samples}

* [範例](https://ibm-graph-docs.ng.bluemix.net/examples.html){:new_window}

## API 參考資料
{: #api}

* [IBM Graph 的 REST API](https://ibm-graph-docs.ng.bluemix.net/api.html){:new_window}
* [使用 Gremlin 搭配 IBM Graph](https://ibm-graph-docs.ng.bluemix.net/api.html#gremlin-apis){:new_window}

## 相關鏈結
{: #general}

* [完整文件](https://ibm-graph-docs.ng.bluemix.net/){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/ibm-graph){:new_window}
* [Apache Tinkerpop](http://tinkerpop.incubator.apache.org/){:new_window}
