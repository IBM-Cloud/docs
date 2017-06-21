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

# クラウドへの {{site.data.keyword.streamsshort}} アプリケーションのデプロイ
{: #t_deploytocloud}

{{site.data.keyword.streamsshort}} アプリケーションを、{{site.data.keyword.Bluemix_short}} クラウドで稼働している {{site.data.keyword.streaminganalyticsshort}} インスタンスにデプロイすることができます。
{:shortdesc}

{{site.data.keyword.streamsshort}} アプリケーションは、{{site.data.keyword.streamsshort}} 環境において {{site.data.keyword.streamsshort}} Processing Language (SPL)、Java、Scala、または Python で作成されます。{{site.data.keyword.streamsshort}} 環境なしでStreams Python アプリケーションを開発できるようになりました。『[クラウドへの {{site.data.keyword.streamsshort}} Python アプリケーションのデプロイ](docs/services/StreamingAnalytics/t_deploytocloud.html#t_deploypython)』を参照してください


{{site.data.keyword.streaminganalyticsshort}} は {{site.data.keyword.streamsshort}} 開発環境をクラウドに組み込みませんが、ローカルで開発したアプリケーションをクラウドにデプロイできます。

開始する前に、{{site.data.keyword.streaminganalyticsshort}} コンソールを表示するために、ブラウザーのポップアップ・ブロッカーを無効にします。

{{site.data.keyword.streamsshort}} アプリケーションをクラウドにデプロイするには、以下の手順を実行します。

1. アプリケーションの開発とテストを行うための開発環境をセットアップします。

	{{site.data.keyword.streamsshort}} 環境を使用する場合は、{{site.data.keyword.streamsshort}} Quick Start Edition を無料でダウンロードできます。[ IBM Streams 製品ページ](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}に進み、**「ネイティブ・ソフトウェア・インストールのダウンロード (Download the native software installation)」**をクリックします。

2. 開発環境でストリーミング・アプリケーションを開発します。{{site.data.keyword.streamsshort}} 開発環境で、Streams Studio またはコマンド・ライン・ツールを使用して、アプリケーションを開発できます。

3. 開発環境で、ストリーミング・アプリケーションが正常に実行されることを確認します。
**注:** Intel プロセッサーを使用し、Red Hat Enterprise Linux (RHEL) 6.5 オペレーティング・システムまたは同等の CentOS バージョンでアプリケーションをコンパイルする必要があります。

4. SPL、Java、Scala、または Python アプリケーションに関連付けられているアプリケーション・バンドル (.sab ファイル) を、次のいずれかの方法を使用して、クラウド内のサービス・インスタンスにサブミットします。
	* {{site.data.keyword.streaminganalyticsshort}} コンソールを使用して、アプリケーション・バンドルをサブミットする。
  * {{site.data.keyword.Bluemix_short}} アプリケーションを作成し、それに {{site.data.keyword.streamsshort}} アプリケーションを追加する。{{site.data.keyword.streaminganalyticsshort}} REST API を使用して、アプリケーションを制御します。

これで、アプリケーションはクラウドにデプロイされました。{{site.data.keyword.streaminganalyticsshort}} サービスを使用して、アプリケーションをモニターできます。複数のアプリケーション (.sab ファイル) をサービス・インスタンスにサブミットすることも可能です。必要に応じていくつでもサブミットできます。

{{site.data.keyword.streamsshort}} では、アプリケーションの開発に使用できる Java™ 開発キットもいくつかサポートしています。 {{site.data.keyword.streamsshort}} での Java サポートについて詳しくは、『[アプリケーション開発用にサポートされる Java 開発キット](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}』を参照してください。

## クラウドへの {{site.data.keyword.streamsshort}} Python アプリケーションのデプロイ
{: #t_deploypython}

{{site.data.keyword.Bluemix_short}} クラウドで実行されている {{site.data.keyword.streaminganalyticsshort}} サービスに {{site.data.keyword.streamsshort}} Python アプリケーションをデプロイします。{{site.data.keyword.streamsshort}} インストール済み環境は不要です。
{:shortdesc}

streamsx パッケージに含まれている [{{site.data.keyword.streamsshort}} Python Application API](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features) により、Python アプリケーションを {{site.data.keyword.streaminganalyticsshort}} サービスにデプロイできます。{{site.data.keyword.streaminganalyticsshort}} サービス用のシンプルな Python アプリケーションを作成およびデプロイする方法の例については、『[Developing for the {{site.data.keyword.streaminganalyticsshort}} service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html)』チュートリアルを確認してください。

IBM Data Science Experience (DSX) では、Jupyter 対話式ノートブックでの Python アプリケーションのサブミットもサポートされます。詳しくは、『[{{site.data.keyword.streaminganalyticsshort}} 用の Python アプリケーションの開発](/docs/services/StreamingAnalytics/t_develop_apps_python.html)』を参照してください。
