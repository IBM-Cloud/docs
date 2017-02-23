---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-28"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
# 標準と要件
{: #standards_and_requirements}

{{site.data.keyword.iot_full}} は、メッセージングやデバイス/アプリケーション開発全般に関する標準と要件を複数サポートしています。
{:shortdesc}


<!-- ## Blockchain
{: #blockchain}

{{site.data.keyword.iot_short_notm}} supports the following versions of the Hyperledger fabric:
- 0.5

## Python
{: #python}

Support for MQTT over SSL requires at least Python v2.7.9 or v3.4, and OpenSSL v1.0.1.
-->

## MQTT
{: #mqtt}

{{site.data.keyword.iot_short_notm}} では、MQTT メッセージ・プロトコルの以下のバージョンがサポートされています。

MQTT バージョン | 注
--- | --- | ---
[3.1.1](https://www.oasis-open.org/standards#mqttv3.1.1) (推奨)  | <ul><li>OASIS 規格。<li>ISO 規格 (ISO/IEC PRF 20922) <li>V3.1 に比べてプロトコルの定義が明確になったので、さまざまなクライアントとサーバーの間の相互運用性が改善されています。<li>MQTT クライアント ID (ClientId) の最大長が、V3.1 での 23 文字から 256 文字に増えました。</br>{{site.data.keyword.iot_short_notm}} サービスでは、長いクライアント ID が必要になることがよくあります。</br>長いクライアント ID は、MQTT プロトコルのバージョンにかかわりなくサポートされています。ただし、V3.1 クライアント・ライブラリーの一部では、ClientId 値の長さが検査され、23 文字の制限が適用されます。</ul>
3.1 | MQTT V3.1 は、現在最も広く使用されているプロトコル・バージョンです。

{{site.data.keyword.iot_short_notm}} は、MQTT 規格で許可されている任意のコンテンツをサポートします。MQTT は、データを認識しないので、画像、任意のエンコード方式のテキスト、暗号化データ、ほとんどすべてのタイプのバイナリー形式データを送信できます。MQTT 規格について詳しくは、以下のリソースを参照してください。
- [MQTT.org](http://mqtt.org/)
- [HiveMQ: Introducing MQTT](http://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt)

{{site.data.keyword.iot_short_notm}} の特定のユース・ケースのメッセージ・ペイロードのサイズや形式に関する制限については、[MQTT メッセージング](mqtt/index.html)を参照してください。
