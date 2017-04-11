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

#製品情報
{: #about}


{{site.data.keyword.geospatialshort_Geospatial}} サービスを使用して、指定する場所へのデバイスの出入りをモニターします。デバイスが指定の滞在時間より長く地域内に滞在しているかどうかも検出できます (ハングアウト検出)。このサービスを開始すると、それ以降、モニターはオンになり、サービスは MQTT メッセージ・ブローカーから継続的にデバイス情報を受信します。サービスを停止すると、モニターはオフになります。{:shortdesc}


IoT には、接続されたデバイスが無数にあり、その増加率は今後何年も成長していくことが予測されています。追跡する対象となるオブジェクトが多数あります。
            移動中のデバイスの場所を認識することは、以下のような多くのアプリケーションの機会を新しく生み出します。

* 特定の小売店の場所の近くにいる顧客にリアルタイムで宣伝する。
* 回避するべき地域 (例えば、事故または緊急事態が発生した場所) を車両または他の接続されたデバイスに警告する。


地理情報デバイス・モニターの使用を開始する最も簡単な方法は、[スターター・アプリケーション](https://hub.jazz.net/project/streamscloud/geo-starter/overview)を使用することです。このスターター・アプリケーションは、
{{site.data.keyword.geospatialshort_Geospatial}} サービスをその REST API を介して構成および制御する方法を示します。アプリケーション・コードを変更して、変更を {{site.data.keyword.Bluemix_notm}} 環境にプッシュして戻すこともできます。
