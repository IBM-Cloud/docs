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

#サービス管理ダッシュボード
{: #service-dashboard}


サービス管理ダッシュボードから、{{site.data.keyword.geospatialshort_Geospatial}} サービス・インスタンスの状況表示、
停止、または再始動を行うことができます。{{site.data.keyword.geospatialshort_Geospatial}} ダッシュボードの {{site.data.keyword.geospatialshort_Geospatial}} タイルをクリックすると、
サービス管理ダッシュボードに移動できます。サンプル・アプリケーションを使用していて、サービス・インスタンスがイベント限度に達して停止した場合、サービスを再始動できます。サービスを停止すると、イベント限度は除去されます。サービスを停止するまでは、イベントの受信は続けられます。サービス管理ダッシュボードには、
サービス・インスタンスの状況および統計も表示されます。{:shortdesc}

##{{site.data.keyword.geospatialshort_Geospatial}} 地域検査

{{site.data.keyword.geospatialshort_Geospatial}} は、IoT から、移動中のデバイスをモニターします。モニター対象の各デバイスは、デバイス・メッセージを送信します。デバイス・メッセージには、固有の ID と共に、そのデバイスの現在位置 (緯度と経度から成る) が含まれています。デバイス位置は、定義された各地理的地域の座標と照合して検査されます。
デバイスが特定の地域に進入、退出、または「ハングアウト」すると、サービスはイベントを生成します。

地域検査は、{{site.data.keyword.geospatialfull}} の使用量を測定するための単位として使用されます。地域に対して進入、退出、または進入と退出の両方の検出が指定されている場合、デバイス・メッセージごとに 1 回の地域検査が実行されます。地域に対してハングアウト検出が指定されている場合、デバイス・メッセージごとに 1 回の地域検査が実行されます。
地域が定義されていない場合、1 つの地域があるかのようにして、デバイス・メッセージごとに 1 回の地域検査がカウントされます。つまり、100 地域に対して検査 (進入、退出、およびハングアウト) が定義されている場合、1 つのデバイス・メ
ッセージにつき 200 回の地域検査が生成されることになります。
