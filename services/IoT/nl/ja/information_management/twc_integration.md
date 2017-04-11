---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# デバイスでの The Weather Company からのデータの使用
{: #weathercompany}

The Weather Company の統合により、気象データを既存の {{site.data.keyword.iot_short_notm}} デバイスに結合できます。
{:shortdesc}

API を使用して「ロケーションの更新」要求が出されるか、デバイス管理メッセージを使用してデバイスでそのロケーションが既に設定されている場合、The Weather Company からの気象データがデバイスの詳細ビューに表示されます。

**重要:** 管理対象デバイスだけがデバイス側でロケーションを設定できます。非管理対象デバイスでは、すべて API を使用して手動でロケーションを設定する必要があります。デバイス・ロケーションの設定について詳しくは、[「ロケーションの更新」要求](../../devices/device_mgmt/index.html#update-location)を参照してください。

### The Weather Company 用の REST API
The Weather Company 用の REST API にアクセスする場合は、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window} の資料の『Device Location Weather』のセクションを参照してください。

### 気象データの表示

特定のデバイス・ロケーションの気象データを取得して表示するには、以下のようにします。
1. **「デバイス」**ペインで目的のデバイスをクリックします。
2. 詳細なデバイス・ビューで、**「拡張 (Extensions)」**セクションまでスクロールダウンします。  
以下の気象データがリストされます。
 - 現在の天気。
 - 現在の温度。
 - 予想最高気温と最低気温。
 - 相対湿度。
 - 気圧。
 - 視程。
 - 風速。
 - 風向き。
 - 緯度。
 - 経度。

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->
