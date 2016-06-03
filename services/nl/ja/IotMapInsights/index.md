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
{: #gettingstartedtemplate}
*最終更新日: 2016 年 5 月 13 日*

{{site.data.keyword.iotmapinsights_full}} によって、開発者がアプリケーションで容易に地理情報機能を使用できるようになります。例えば、世界中の道路網に基づく、マップ・マッチングや最短パス検索などがあります。
{:shortdesc}

{{site.data.keyword.iotmapinsights_short}} REST API を介して以下の機能を使用できます:

- 道路網の形状を活用する、非常に正確なマップ・マッチング。
- 交通量など、マップ上でのリアルタイム・イベントの操作。
- 交通量などのリアルタイム・イベントを考慮した動的な最短パス検索 (ルート検索)。
- マップ上での道路形状の描画に使用できる道路形状データの取得。

{{site.data.keyword.iotmapinsights_short}} サービスは、OpenStreetMap から抽出された WGS84 座標系の道路網データを使用します。車両が移動できる道路のみが分析に使用されます。

サポートされるマップ地域は、次のとおりです。

- ヨーロッパ (map_id=1)
- アフリカ (map_id=2)
- アジア (map_id=3)
- オーストラリア・オセアニア (map_id=4)
- 北アメリカ (map_id=5)
- 中央アメリカ (map_id=6)
- 南アメリカ (map_id=7)


{{site.data.keyword.iotmapinsights_short}} サービスの分析機能を使用するには、以下の手順を実行します。

## マップ・マッチングでの {{site.data.keyword.iotmapinsights_short}} の使用

1. 分析対象となる一連のロー GPS 座標データを用意します。
2. `mapMatching` REST API を使用して、時系列順のロー GPS 座標データを {{site.data.keyword.iotmapinsights_short}} サービスに送信します。オプションで、各地点の向首角を度数で設定して (北が 0、時計回りの角度)、進行方向を示すことができます。
3. `mapMatching` REST API 呼び出しの応答として、マップ・マッチングされた座標と道路リンク情報を受信します。
4. オプションで、`getLinkInformation` REST API を使用して、マップ・マッチングされた道路リンクの道路形状データを取得します。道路形状で構成された一連の座標を得るには、リンク ID を指定して `getLinkInformation` REST API を呼び出します。

## 経路検索での {{site.data.keyword.iotmapinsights_short}} の使用

1. 最短パスを取得する始点と終点を決めます。
2. `routeSearch` REST API を使用して、始点と終点の座標を {{site.data.keyword.iotmapinsights_short}} サービスに送信します。オプションで、各地点の向首角を度数で設定して (北が 0、時計回りの角度)、進行方向を示すことができます。
3. `routeSearch` REST API 呼び出しの応答として、道路リンクのリストを受信します。結果データに含まれている形状データを使用して、検出されたパスの形状をマップ上に描画できます。

## 交通イベント操作での {{site.data.keyword.iotmapinsights_short}} の使用

1. 作成する交通イベントのタイプと位置を決めます。
2. `createEvent` REST API を使用して、交通イベント情報を {{site.data.keyword.iotmapinsights_short}} サービスに送信します。
3. `createEvent` REST API 呼び出しの応答として、作成された交通イベントのイベント ID を受信します。
4. `queryEvent` REST API を使用して、特定の矩形領域内の交通イベントを検索します。オプションで、特定のイベント・タイプを指定できます。

- オプションで、`deleteEvent` REST API を使用して、有効ではなくなった交通イベントを削除します。
- オプションで、`getAffectedLinksInformation` REST API を使用して、交通イベントの影響を受けた道路の地域を取得します。


# 関連リンク
{: #rellinks}
## チュートリアルとサンプル
{: #samples}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} チュートリアル、パート 1](https://github.com/IBM-Bluemix/car-data-management){:new_window}
* [{{site.data.keyword.iotmapinsights_short}} / {{site.data.keyword.iotdriverinsights_short}} チュートリアル、パート 2](https://github.com/IBM-Bluemix/map-driver-insights){:new_window}

## API リファレンス
{: #api}

* [API 資料](http://ibm.biz/IoTContextMapping_APIdoc){:new_window}

## 関連リンク
{: #general}
* [{{site.data.keyword.iotdriverinsights_short}}](../IotDriverInsights/index.html){:new_window} 入門
* [{{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html){:new_window} 入門
* [IBM developerWorks の dW Answers](https://developer.ibm.com/answers/topics/iot-context-mapping){:new_window}
* [Stack Overflow](http://stackoverflow.com/questions/tagged/iot-context-mapping){:new_window}
* [Bluemix サービスの新機能](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}
* [OpenStreetMap](http://www.openstreetmap.org/){:new_window}

