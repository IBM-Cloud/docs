---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot4auto_short}} (ベータ) 概説
{: #getting_started_iotautomotive}

最終更新日: 2016 年 7 月 29 日
{: .last-updated}

{{site.data.keyword.iot4auto_full}} は、接続先の自動車からビッグデータを取得し、それを管理および分析するために使用できる {{site.data.keyword.Bluemix_notm}} サービスです。{{site.data.keyword.iot4auto_short}} のアナリティクスは、運転動作、車両の位置、その他の興味深い自動車関連アクティビティーやイベントについての、すぐに利用できる強力な洞察を提供します。

{:shortdesc}

{{site.data.keyword.iot4auto_short}} を使用して、以下の作業を実行できます。

- 自動車プローブ・データと正規化データを分析のためにデータ・ストアに送信する
- イベントをコンテキスト・マップに注入し、特定の車両が影響を受けるイベントを取得する
- 自動車プローブ・データからの新規イベントを識別する
- 接続された車両に関する情報を取得する
- ドライバー、車両、イベント・ルール、イベント・タイプ、製造元に関する資産データを管理する


{{site.data.keyword.iot4auto_short}} サービスには、以下の {{site.data.keyword.Bluemix_notm}} サービスが含まれます。それらは別々に {{site.data.keyword.Bluemix_notm}} カタログでも用意されています。

|サービス|説明 |
|:---|:---|
|[Driver Behavior](../IotDriverInsights/index.html){:new_window}| このサービスは、ドライバーの動作を分析し、接続された車両から取得した自動車プローブ・データとコンテキスト・データから、走行の軌跡パターンを識別します。
|[Context Mapping](../IotMapInsights/index.html){:new_window}| このサービスは、マップ・マッチングや道路ネットワークでの最短経路検索など、地理情報機能を提供します。
*表 1. {{site.data.keyword.iot4auto_short}}* のサービス

自動車用デバイスおよびアプリケーションと、サービスとの統合を開始するには、まず以下のステップを実行してください。

1. [{{site.data.keyword.iot4auto_short}} について](iotautomotive_overview.html)というトピックを参照して、このサービスでサポートされる使用可能なフィーチャーとアナリティクスについて理解します。
2. [{{site.data.keyword.Bluemix_notm}} カタログ](https://console.ng.bluemix.net/catalog/labs/){:new_window}からサービスのインスタンスを追加するときに、アプリにバインドされていないことを確認し、自動生成されるテナント ID、ユーザー名、パスワード値を必ずメモします。これらの値は後で、{{site.data.keyword.iot4auto_short}} API を介してサービスにアクセスするときに必要になります。
3. ダッシュボード上のコンソールを使用して、{{site.data.keyword.iot4auto_short}} のポート、ターゲット・ホスト名、その他の設定を構成します。詳しくは、[管理](iotautomotive_admin.html)を参照してください。

{{site.data.keyword.iot4auto_short}} REST API コマンドを使用して、自動車用デバイスおよびアプリケーションをこのサービスと統合することができます。

迅速に稼働させるには、以下のステップを実行します。

1. 分析対象のイベントを送信するための `sendEvent` API 要求コマンドを使用して、イベントを注入します。
  - 要求: イベント・データと位置
2. イベントを取得するための `getEvent` API 要求コマンドを使用して、マップ・マッチングによってイベント・データが格納されたことを確認します。
  - 要求: エリア・データ (始点または終点の緯度と経度)
  - 応答: イベント・データと道路リンク ID
3.  `sendCarProbe` API 要求コマンドを使用して、分析対象の自動車プローブ・データを送信します。
  - 要求: 自動車プローブ・データと位置
4. データを取得するための `getCarProbe` API 要求コマンドを使用して、マップ・マッチングによって自動車プローブ・データが格納されたことを確認します。
  - 要求: エリア・データ (始点または終点の緯度と経度)
  - 応答: 自動車プローブ・データと道路リンク ID
5. ドライバー・データを分析します。詳しくは、[Driver Behavior](../IotDriverInsights/index.html){:new_window} を参照してください。

# 関連リンク
{: #rellinks}

## API 参照情報
{: #api}
* [{{site.data.keyword.iot4auto_short}} API 資料](http://ibm.biz/IoT4Automotive_APIdoc){:new_window}
* [Contextual Map service APIs](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}
* [Driver Behavior service APIs]( http://ibm.biz/IoTDriverBehavior_APIdoc){:new_window}


## 関連リンク
{: #general}
* [{{site.data.keyword.iotdriverinsights_short}} の使用を開始する](../IotDriverInsights/index.html){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} 概説](../IotMapInsights/index.html){:new_window}
* [{{site.data.keyword.iot_full}} の概要](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
* [Bluemix Services の新機能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [IBM developerWorks の dW Answers](https://developer.ibm.com/answers/topics/iot-for-automotive){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-for-automotive){:new_window}
