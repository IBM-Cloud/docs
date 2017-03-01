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

#クラウドへの {{site.data.keyword.streamsshort}} アプリケーションのデプロイ
{: #t_deploytocloud}

{{site.data.keyword.streamsshort}} アプリケーションを、{{site.data.keyword.Bluemix_short}} クラウドで稼働している {{site.data.keyword.streaminganalyticsshort}} インスタンスにデプロイすることができます。
{:shortdesc}

{{site.data.keyword.streamsshort}} アプリケーションは、{{site.data.keyword.streamsshort}} 環境で {{site.data.keyword.streamsshort}} Processing Language (SPL) で書かれています。{{site.data.keyword.streamsshort}} では、アプリケーションの開発に使用できる Java™ 開発キットもいくつかサポートしています。 {{site.data.keyword.streamsshort}} での Java サポートについて詳しくは、[Supported アプリケーション開発用のサポートされる Java 開発キット](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}について参照してください。
{{site.data.keyword.streaminganalyticsshort}} は {{site.data.keyword.streamsshort}} 開発環境をクラウドに組み込みませんが、ローカルで開発したアプリケーションをクラウドにデプロイできます。

始める前に、Streaming Analytics コンソールを表示するためにブラウザーのポップアップ・ブロッカーを無効にしてください。

{{site.data.keyword.streamsshort}} アプリケーションをクラウドにデプロイするには、以下の手順を実行します。

1. アプリケーションの開発とテストを行うための {{site.data.keyword.streamsshort}} 環境をセットアップします。 

	{{site.data.keyword.streamsshort}} 環境が用意されていない場合は、{{site.data.keyword.streamsshort}} Quick Start Edition を無料でダウンロードできます。[IBM Streams 製品ページ](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}に進み、**「Download the native software installation」**をクリックします。

2. Streams Studio またはコマンド・ライン・ツールを使用して、{{site.data.keyword.streamsshort}} 環境で SPL または Java のアプリケーションを開発します。
3. 開発環境で、SPL または Java のアプリケーションが正常に実行されることを確認します。
4. SPL または Java のアプリケーションに関連付けられているアプリケーション・バンドル (.sab ファイル) を、次のいずれかの方法を使用して、クラウド内のサービス・インスタンスにサブミットします。
	* {{site.data.keyword.streaminganalyticsshort}} コンソールを使用して、アプリケーション・バンドルをサブミットする。
    * {{site.data.keyword.Bluemix_short}} アプリケーションを開発し、それに {{site.data.keyword.streamsshort}} アプリケーションを追加する。
{{site.data.keyword.streaminganalyticsshort}} REST API を使用して、アプリケーションを制御します。

これで、アプリケーションはクラウドにデプロイされました。{{site.data.keyword.streaminganalyticsshort}} サービスを使用して、アプリケーションをモニターできます。複数の SPL または Java のアプリケーション (.sab ファイル) をサービス・インスタンスにサブミットすることも可能です。必要に応じていくつでもサブミットできます。
