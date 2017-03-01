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


#{{site.data.keyword.streaminganalyticsshort}} の概説
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}} では {{site.data.keyword.streamsshort}} を採用しています。これは、タイプが異なるデータ・ソースから到着する情報をリアルタイムで取り込み、分析し、相互に関連付けるために使用できる、高機能の分析プラットフォームです。{{site.data.keyword.streaminganalyticsshort}} サービスのインスタンスを作成すると、{{site.data.keyword.Bluemix_short}} クラウド内で稼働する {{site.data.keyword.streamsshort}} のユーザー独自のインスタンスが得られ、{{site.data.keyword.streamsshort}} アプリケーションを実行する準備が整います。
{:shortdesc}

{{site.data.keyword.Bluemix_short}} クラウド内で稼働する {{site.data.keyword.streaminganalyticsshort}} インスタンスに、アプリケーションをデプロイすることができます。

[スターター・アプリケーション](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}を実行することで、すぐに {{site.data.keyword.streaminganalyticsshort}} を開始できます。ユーザー独自のアプリケーションをさらに開発したい場合は、{{site.data.keyword.streamsshort}} 開発環境が必要であり、SPL をクラウド対応にする必要があります。

{{site.data.keyword.streaminganalyticsshort}} を開始するには、以下のいずれかの方法を使用して、SPL または Java™ アプリケーションに関連付けられているアプリケーション・バンドル (.sab ファイル) をサブミットします。
* {{site.data.keyword.streaminganalyticsshort}} コンソールを使用する。
* {{site.data.keyword.Bluemix_short}} アプリケーションを開発し、それに {{site.data.keyword.streamsshort}} アプリケーションを追加する。
[{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220) を使用して、アプリケーションを制御します。開発環境で、SPL または Java のアプリケーションが正常に実行されることを確認します。

{{site.data.keyword.streaminganalyticsshort}} を、他の {{site.data.keyword.Bluemix_short}} サービス ({{site.data.keyword.cloudant}} および {{site.data.keyword.messagehub}} など) と連携して使用できるようになりました。稼働させる方法についての例は、[他の {{site.data.keyword.Bluemix_short}} サービスと統合するためのチュートリアル](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window}を参照してください。

{{site.data.keyword.streamsshort}} アプリケーションを開発するには、{{site.data.keyword.streamsshort}} 開発環境が必要です。{{site.data.keyword.streamsshort}} 環境が用意されていない場合は、[{{site.data.keyword.streamsshort}} 製品ページ](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)上で {{site.data.keyword.streamsshort}} Quick Start Edition を無料でダウンロードできます。

{{site.data.keyword.streamsshort}} アプリケーション開発について熟知していない場合は、学習を支援するリソースがあります。詳細については、[{{site.data.keyword.streamsshort}} Knowledge Center](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window} を参照してください。

オンプレミスで実行する SPL アプリケーションが既にある場合は、[クラウド用のアプリケーションの準備を行う](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}必要があります。

# 関連リンク
{: #rellinks}

## チュートリアルおよびサンプル
{: #samples}
* [Introduction to {{site.data.keyword.streaminganalyticsshort}}](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} SDK for Node.js™ スターター・アプリケーション](http://bit.ly/1iR1bzu){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} Liberty for Java™ スターター・アプリケーション](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/){:new_window}
* [Getting your SPL application ready for the cloud](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud){:new_window}
* [Bluemix {{site.data.keyword.streaminganalyticsshort}} 開発ガイド](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-development-guide/){:new_window}
* [追加のチュートリアル](StreamingAnalytics.html#r_integrating_cloudant_rest){:new_window}


## API リファレンス
{: #api}
* [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window}
* [{{site.data.keyword.streamsshort}} REST API を使用した {{site.data.keyword.streaminganalyticsshort}} メトリック](https://developer.ibm.com/bluemix/2016/07/25/streaming-analytics-metrics-using-rest-api/){:new_window}

## 互換性のあるランタイム
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## 関連リンク
{: #general}
* [{{site.data.keyword.streamsshort}} の資料](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [{{site.data.keyword.streamsshort}}Quick
Start Edition](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}
