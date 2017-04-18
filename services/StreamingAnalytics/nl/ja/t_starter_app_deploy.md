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

# {{site.data.keyword.Bluemix_short}} へのスターター・アプリケーションのデプロイ
{: #starterapps_deploy}

いずれかの {{site.data.keyword.streaminganalyticsshort}} スターター・アプリケーションを {{site.data.keyword.Bluemix_short}} クラウドにプッシュしてデプロイすることができます。
{:shortdesc}

始めに、{{site.data.keyword.streaminganalyticsshort}} スターター・アプリケーションをデプロイするために、{{site.data.keyword.Bluemix_short}} の準備をします。

* [コマンド・ライン・ツールをインストールします](https://github.com/cloudfoundry/cli/releases)。
* {{site.data.keyword.Bluemix_short}} 内にアプリケーションを作成し、作成したアプリケーションに {{site.data.keyword.streaminganalyticsshort}} サービスを追加して、アプリケーションを再ステージングします。
	* Event Detection スターター・アプリケーションをデプロイするには、{{site.data.keyword.sdk4node}} ランタイムを使用してアプリケーションを作成します。
	* NYC Traffic スターター・アプリケーションをデプロイするには、Liberty for Java™ ランタイムを使用してアプリケーションを作成します。

アプリケーションに指定した名前を覚えておいてください。後で必要になります。

{{site.data.keyword.streaminganalyticsshort}} では、サービスを開始できるように、2 つのサンプル・アプリケーションを提供しています。 

Event Detection スターター・アプリケーションは、リアルタイム・ストリーム内の気象関連のデータを分析し、分析の状況と結果を表示します。このアプリケーションは {{site.data.keyword.sdk4node}} で書かれています。Event Detection スターター・アプリケーションの使用法について詳しくは、[Detect complex events in a real-time data stream](https://www.ibm.com/developerworks/library/ba-bluemix-detect-complex-events-from-data-stream-trs/index.html) を参照してください。

NYC Traffic スターター・アプリケーションは、パブリック Web サイトから交通量データを読み取って分析します。このアプリケーションは、Liberty for Java™ で書かれています。NYC Traffic スターター・アプリケーションの使用法について詳しくは、[{{site.data.keyword.streaminganalyticsfull}} Starter Application](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/) を参照してください。 

スターター・アプリケーションをダウンロードして、{{site.data.keyword.Bluemix_short}} にデプロイするには、以下の手順を実行します。

1. [Event Detection](https://hub.jazz.net/project/streamscloud/EventDetection/overview) または [NYC Traffic](https://hub.jazz.net/project/streamscloud/NYCTraffic/overview) スターター・アプリケーションをダウンロードします。
2. コマンド・ラインで、プロジェクト・ディレクトリーに移動します。
  <pre><code>cd myapp</code></pre>
 
3. {{site.data.keyword.Bluemix_short}} 内のアプリケーションに指定した名前に一致するように、プロジェクト・ディレクトリーの名前を変更します。
4. {{site.data.keyword.Bluemix_short}} に接続します。
  <pre><code>cf api https://api.DomainName</code></pre>
   
5. {{site.data.keyword.Bluemix_short}} にログインし、プロンプトが出されたら、ターゲット組織を設定します。
   <pre><code>cf login</code></pre>
    
6. アプリケーションをデプロイします。
  <pre><code>cf push myapp</code></pre>
   
7. アプリケーション概要ページ ({{site.data.keyword.Bluemix_short}} ダッシュボードからアクセス可能) に移動し、アプリケーションが正常に開始されたことを確認します。
8. アプリケーションを起動してブラウザーに表示します。アプリケーション概要ページに、アプリケーションの URL (または「ルート」) が表示されます。

これでアプリケーションは実行中になったので、サービス・ダッシュボードに移動して、{{site.data.keyword.streaminganalyticsshort}} インスタンスの状況を確認することや、トラブルシューティング用の情報を取得することができます。サービス・ダッシュボードにアクセスするには、{{site.data.keyword.Bluemix_short}} ダッシュボードに移動し、アプリケーション概要ページで {{site.data.keyword.streaminganalyticsshort}} タイルをクリックします。
