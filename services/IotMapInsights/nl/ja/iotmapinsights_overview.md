---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# {{site.data.keyword.iotmapinsights_short}} について
{: #iotmapinsights_overview}
最終更新日: 2016 年 7 月 20 日
{: .last-updated}

{{site.data.keyword.iotmapinsights_full}} は、静的な道路網データと動的なイベント・データに高速アクセスするための、{{site.data.keyword.Bluemix_notm}} 上のサービスです。{{site.data.keyword.iotmapinsights_short}} は、道路網のための地理情報ツールも提供します。これらのツールを使用して、地理情報機能とアプリケーションを統合することができます。
{:shortdesc}

{{site.data.keyword.iotmapinsights_short}} サービスは、以下のフィーチャーを提供します。

- 静的なマップ・データ
- 動的なイベント・データ
- 地理情報ツール

{{site.data.keyword.iotmapinsights_short}} サービスは、処理用のサービス・メモリー・キャッシュに保管されている [OpenStreetMap](http://www.openstreetmap.org/){: new_window} 道路網データを収集して使用します。

OpenStreetMap からのデータは、OpenStreetMap Foundation (OSMF) による Open Data Common Open Database License (ODbL) のもとで使用可能になります。詳しくは、「[OpenStreetMap 著作権とライセンス](http://www.openstreetmap.org/copyright){: new_window}」を参照してください。

## 静的なマップ・データ
{: #static_map_data_query}

この製品の主なフィーチャーの 1 つは、アプリケーションで使用する詳細な道路情報を取得できることです。Link Query REST API インターフェースを使用して、静的なマップ道路属性データをリンク ID で照会できます。{{site.data.keyword.iotmapinsights_short}} の[マップ・マッチング](#map_matching)機能を使用して、必要なリンク ID パラメーターを識別できます。

返されるデータには、要求されたリンク ID に関する以下の情報が含まれます。

- 道路のタイプ
- 道路の長さ
- 詳細形状ポイントの配列
- 隣接ノードと隣接リンクに関する情報

詳細な道路リンク情報を照会して、返された隣接リンク情報を的確に使用することにより、アプリケーションは道路リンク網を全探索することができます。

## 動的なイベント・データ
{: #dynamic_event_data}

静的なマップ・データに加えて、現実の道路状況には当然、交通渋滞や道路工事などの動的なイベントも存在します。{{site.data.keyword.iotmapinsights_short}} を使用して、経路計画の目的で交通イベントを作成、管理し、[影響を受けるリンク検索](#link_search)と組み合わせることができます。

### イベントの注入と削除
{: #inject_event}

{{site.data.keyword.iotmapinsights_short}} サービスのイベント注入 REST API を使用して、特定の道路リンクに置かれるマップ・オブジェクト・モデルの形式の交通イベントを、動的に注入したり削除したりすることができます。各イベントには、GPS 座標、開始時刻、イベント・タイプ、イベント期間、影響を受ける道路長など、基本的な属性が含まれます。

イベント削除 REST API インターフェースを使用して、古くなったイベントをマップから削除できます。

### イベント照会
{: #query_event}

イベント照会 REST API を使用して、ある特定の地理的領域内のすべての動的イベントに関する詳細情報を取得できます。経度と緯度で範囲を指定して地域別に照会でき、返されるターゲット・イベントの数を絞り込むためのイベント属性を組み込むことができます。

## 地理情報ツール
{: #geospatial_tools}

{{site.data.keyword.iotmapinsights_short}} 地理情報ツールが提供するマップ・マッチングと経路検索の機能を使用して、アプリケーションを拡張できます。

### マップ・マッチング
{: #map_matching}

アプリケーションでマップ・マッチング REST API インターフェースを使用することにより、実デバイスの GPS 座標を [OpenStreetMap](http://www.openstreetmap.org/){: new_window} 道路網データにマップして、不正確な GPS データの位置精度を高めることができます。また、位置に基づいた道路属性に関する情報を受け取ることもできます。アプリケーションはマップ・マッチング REST API を使用して、ロー GPS データ・ポイントを道路リンク上の一致したポイントに合わせることができます。

マップ・マッチング REST API インターフェースは、1 つのポイントの緯度および経度の GPS 座標データを受信し、マップで一致したポイントを返します。このマップ・マッチング・ポイントは特定期間内のそれぞれの車の履歴データを考慮に入れて分析され、最も可能性の高いポイントがリアルタイムで検出されます。位置の履歴データがないポイントの場合、マップ・マッチング・インターフェースは、道路リンク上の、要求された GPS ポイントから最も近いポイントを返します。

### 経路検索
{: #route_search}

地理情報機能を使用するアプリケーションの基本的なフィーチャーの 1 つは、2 地点間の最短経路を見つけ出せることです。  

{{site.data.keyword.iotmapinsights_short}} サービスの経路検索 REST API インターフェースは、始点 GPS 座標と終点 GPS 座標間の最短経路を計算します。受信した座標は、マップ・マッチング機能を使用してマップの最も近いリンクにマッチングされ、これらのマップ・マッチング・ポイント間の最短パスが計算されます。

### 影響を受けるリンク検索
{: #link_search}

道路上でイベントが発生すると、それがさまざまな道路リンクに影響する可能性があります。REST API を使用して、影響を受けるリンクを検索することができます。また、車がイベントに遭遇する可能性のある道路リンクを見つけ出すこともできます。この検索では、車からイベントまでの距離だけでなく、道路リンク網の接続形態も考慮に入れられます。
