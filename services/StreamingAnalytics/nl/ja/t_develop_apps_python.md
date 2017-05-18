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

# {{site.data.keyword.streaminganalyticsshort}} 用の Python アプリケーションの開発
{: #t_develop_apps_python}

IBM Data Science Experience (DSX) またはローカル Python 開発環境で Python アプリケーションを開発し、そのアプリケーションを {{site.data.keyword.streaminganalyticsshort}} にデプロイできるようになっています。
{:shortdesc}

以下のいずれかの方法によって、{{site.data.keyword.streaminganalyticsshort}} サービスを使用して、{{site.data.keyword.Bluemix_short}} クラウドに Python アプリケーションを開発およびデプロイできます。


## DSX での Streams Python アプリケーションの開発
{: #t_develop_python_dsx}

Python 開発環境がない場合は、DSX のノートブックを使用し、{{site.data.keyword.streaminganalyticsshort}} サービス用のサンプル Python アプリケーションを作成するのが、最も簡単な開始方法です。該当するノートブックでは、DSX Python 環境内で {{site.data.keyword.streaminganalyticsshort}} サービスのシンプルな Python アプリケーションを作成およびデプロイするためのステップおよびコード・サンプルが提供されます。

* [Hello World!](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca9c6e8): 開始点としてシンプルな Hello World! アプリケーションを作成し、そのアプリケーションを {{site.data.keyword.streaminganalyticsshort}} サービスのインスタンスにデプロイします。

* [医療のデモ](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039cad29a6): フィードからのストリーミング・データを取り込んで分析してから、ノートブックでデータを視覚化するアプリケーションを作成します。最終的に、このアプリケーションを {{site.data.keyword.streaminganalyticsshort}} サービス・インスタンスにサブミットします。

* [ニューラル・ネットワークのデモ](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca60bb7): サンプル・データ・セットを作成し、サンプル・データ用のモデルを作成し、ストリーミング・アプリケーションでそのモデルを使用し、ストリーミング・データを視覚化し、最後にそのストリーミング・アプリケーションを {{site.data.keyword.streaminganalyticsshort}} サービスにサブミットします。

## ローカル Python 環境でのアプリケーションの開発
 {: #t_develop_python_api}

  streamsx パッケージに含まれている [{{site.data.keyword.streamsshort}} Python Application API](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features) により、Python 呼び出し可能クラスまたは関数を使用して、ストリーム処理アプリケーションを作成できます。その後、Python Application API を使用して、アプリケーションを定義してサービスにサブミットします。

『[Developing for the {{site.data.keyword.streaminganalyticsshort}} service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html)』チュートリアルのステップに従って、ローカル Python 環境でサンプル・アプリケーションを作成して {{site.data.keyword.streaminganalyticsshort}} サービスにデプロイすることで、開始します。
