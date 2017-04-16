---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# {{site.data.keyword.iotmapinsights_short}} 概説
{: #iotdriverinsights_index}
最終更新日: 2016 年 6 月 22 日
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} は、アプリケーションで地理情報機能を使用できるようにするための、{{site.data.keyword.Bluemix}} 上のサービスです。例えば、世界中の道路網を対象としたマップ・マッチングや最短経路検索などの機能を使用できるようになります。  
{:shortdesc}

{{site.data.keyword.iotmapinsights_short}} REST API を介して、以下のフィーチャーを使用できます。

|フィーチャー|用途...|
|:---|:---|
|非常に正確なマップ・マッピング|実際にマップされた道路網に GPS ロケーションを対応させる|
|道路形状データの取得|マップされた道路網を取得してマップ上に道路の形状を描画する|
|最短経路の動的検索|交通量などのリアルタイム・イベントを取り込んだ最短経路を検索する|
|交通イベントのリアルタイム操作|例えば交通状況などのリアルタイム・マップ・マッチング・イベントを追加して、経路計画の結果を向上させる|

## 始める前に
{: #byb}

1. [{{site.data.keyword.Bluemix_notm}} カタログ](https://console.stage1.ng.bluemix.net/catalog/services/iot-automotive/){: new_window}からサービスのインスタンスを追加するときは、そのサービス・インスタンスをアプリケーションにバインドしないようにし、自動生成されたテナント ID、ユーザー名、パスワードの値を書き留めておいてください。これらの値は、後で {{site.data.keyword.iotmapinsights_short}} API を介してサービスにアクセスする際に必要になります。

2. [OpenStreetMap](http://www.openstreetmap.org/){: new_window} をよく理解してください。  

 {{site.data.keyword.iotmapinsights_short}} サービスは、[OpenStreetMap](http://www.openstreetmap.org/){: new_window} から抽出された道路網データ (WGS84 座標系) を使用します。車が走行できる道路のみが分析に使用されます。  

 以下のマップ地域がサポートされています。

|地域|マップ ID|
|:---|:---|
|ヨーロッパ|map_id=1|
|アフリカ|map_id=2|
|アジア|map_id=3|
|オーストラリア、オセアニア|map_id=4|
|北アメリカ|map_id=5|
|中央アメリカ|map_id=6|
|南アメリカ|map_id=7|

## マップ・マッチング
{: #map_matching}
ロー GPS 座標をマップ・マッチング座標にマップするには、以下のステップを実行します。

1. 分析するロー GPS 座標のセットを用意します。
2. `mapMatching` API コマンドを使用して、ロー GPS 座標を送信します。必要に応じて、各地点の向首角を度数で設定して、進行方向を指定します。
 - 要求: ロー GPS データ
 - 応答: マップ・マッチング GPS データ、リンク ID
3. オプション: `getLinkInformation` API コマンドを使用して、道路タイプ・データを取得します。`getLinkInformation` REST API を使用して、対応する道路形状データを一連の座標として取得できます。
 - 要求: リンク ID
 - 応答: 道路タイプ

## 経路検索
{: #route_searching}

指定した起点座標と目的地座標の間の最短経路パス情報を見つけるには、以下のステップを実行します。

1. 最短経路の始点と終点を決めます。
2. `routeSearch` REST API を使用して、始点と終点の座標を送信します。
必要に応じて、各地点の向首角を度数で設定して、進行方向を指定します。
 - 要求: 起点座標と目的地座標
 - 応答: マップ・マッチング最短経路

返されたリンク形状データを使用して、見つかったパスの形状をマップ上に描画します。

## 交通イベントの追加
{: #traffic_events}

交通イベント情報を {{site.data.keyword.iotmapinsights_short}} サービスに追加するには、以下のステップを実行します。

1. 作成する交通イベントのタイプと位置を選択します。
2. `createEvent` API コマンドを使用して、イベントを注入します。
交通イベント情報を {{site.data.keyword.iotmapinsights_short}} サービスに送信します。
 - 要求: イベント情報
 - 応答: イベント ID
3. `queryEvent` REST API コマンドを使用して、イベントを検出します。
特定の四角形領域内の交通イベント、および必要に応じて特定の交通イベント・タイプを検索します。
 - 要求: 領域情報
 - 応答: イベント情報  
4. オプション: `deleteEvent` API コマンドを使用して、有効でなくなった交通イベントを削除します。
5. オプション: `getAffectedLinksInformation` API コマンドを使用して、交通イベントの影響を受けている道路の地域を取得します。

# 関連リンク
{: #rellinks}

## チュートリアルとサンプル
{: #samples}

* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} チュートリアル、パート 1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} チュートリアル、パート 2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}
* [IoT for Automotive Starter Application](https://iot-automotive-starter.mybluemix.net){:new_window}

## API リファレンス
{: #api}

* [API 資料](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}

## 関連リンク
{: #general}

* [{{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window} 概説
* [{{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window} 概説
* [IBM developerWorks の dW Answers](https://developer.ibm.com/answers/topics/iot-context-mapping){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-context-mapping){:new_window}
* [Bluemix サービスの新機能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [OpenStreetMap](http://www.openstreetmap.org/){:new_window}
* [&copy; OpenStreetMap コントリビューター](http://www.openstreetmap.org/copyright){:new_window}
* [Open Data Commons Open Database License (ODbL)](http://opendatacommons.org/licenses/odbl/){:new_window}
