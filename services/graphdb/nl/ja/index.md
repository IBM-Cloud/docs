---

著作権:
  年: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.graphfull}} の概要
{: #gettingstartedtemplate}
最終更新日: 2016年7月27日
{: .last-updated}

{{site.data.keyword.graphfull}} は、REST ベースの HTTP API インターフェースを介してアクセス可能な、完全管理のグラフ・データベース・サービスです。
これを使用して、グラフ・データベースの機能を必要とするモバイル・アプリケーションや Web アプリケーションを構築します。
{:shortdesc}

{{site.data.keyword.graphfull}} は、[Apache TinkerPop](http://tinkerpop.incubator.apache.org/)&trade; スタックに基づいて、
v3 と互換性のある API を使用する高性能のグラフ・アプリケーションを構築します。
このスタックによって柔軟性が増し、使い慣れた環境に基づく機能が付加されます。
{{site.data.keyword.Bluemix}} ダッシュボードを使用すると、
{{site.data.keyword.graphfull}} サービスを {{site.data.keyword.Bluemix_short}} アプリケーションに容易に組み込むことができます。

以下の 2 つの方法で、{{site.data.keyword.graphfull}} の作業を行うことができます。

*	{{site.data.keyword.graphfull}} の簡易 API コマンドを使用する。
*	完全な Apache TinkerPop v3 照会言語 (Gremlin) を使用する。

{{site.data.keyword.graphfull}} の機能は、HTTP REST エンドポイントを使用することにより、API で使用可能となります。
HTTP を使用して API 要求の発行と結果の取得を行うことによって、これらのエンドポイントは、アプリケーションが {{site.data.keyword.graphfull}} サービスに容易に接続してそのサービスを使用できるようにします。
選択したアプリケーション・プログラミング言語で提供される HTTP 機能を使用して、エンドポイントにアクセスします。
あるいは、コマンド・インターフェースまたは `curl` スクリプトを使用して、同じ処理を行うこともできます。
API リファレンスには、{{site.data.keyword.graphfull}} サービスによって提供されるさまざまな機能とその使用例が説明されています。

{{site.data.keyword.graphfull}} サービスを使用するタスクのために、
Gremlin と呼ばれる Apache TinkerPop 照会言語をアプリケーションで使用することもできます。
Gremlin 照会を JSON 文書に組み込んでから、その文書を `/gremlin` サービス・エンドポイントに渡します。
Gremlin を {{site.data.keyword.graphfull}} で使用する例が、完全なドキュメンテーションに記載されています。

{{site.data.keyword.graphfull}} サービスを開始するには、以下の手順を実行します。

1.	{{site.data.keyword.graphfull}} サービスの[インスタンスを作成します](https://www.ng.bluemix.net/docs/services/reqnsi.html#req_instance)。
2.	インスタンスの作成時に生成される 3 つの重要な値を記録します。それらの値は、サービス・タイルをクリックした後に`「サービス資格情報」`タブから取得できます。
	*	IBM Graph エンドポイント: `apiURL`。
	*	サービス・インスタンスのユーザー名 `username`。
	*	サービス・インスタンスのパスワード `password`。
3.	これらの 3 つの重要な値を {{site.data.keyword.graphfull}} タスクのためにアプリケーションまたはスクリプトで使用します。使用例は、完全なドキュメンテーションに記載されています。

# 関連リンク
{: #rellinks}

## チュートリアルとサンプル
{: #samples}

* [例](https://ibm-graph-docs.ng.bluemix.net/examples.html){:new_window}

## API リファレンス
{: #api}

* [IBM Graph 用の REST API](https://ibm-graph-docs.ng.bluemix.net/api.html){:new_window}
* [Gremlin を IBM Graph で使用する方法](https://ibm-graph-docs.ng.bluemix.net/api.html#gremlin-apis){:new_window}

## 関連リンク
{: #general}

* [完全なドキュメンテーション](https://ibm-graph-docs.ng.bluemix.net/){:new_window}
* [スタック・オーバーフロー](http://stackoverflow.com/questions/tagged/ibm-graph){:new_window}
* [Apache Tinkerpop](http://tinkerpop.incubator.apache.org/){:new_window}
