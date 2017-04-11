---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} でのデバイスの開発
{: #device_dev_index}

デバイスとは、インターネットに接続でき、クラウドとの間で送受信するデータが存在するすべてのものを指します。デバイスを使用して、センサー測定値などのイベント情報をクラウドに送信し、クラウド内のアプリケーションからコマンドを受け取ることができます。

デバイスは、イベントを使用して {{site.data.keyword.iot_short_notm}} にデータをパブリッシュします。デバイスはイベントの内容を制御し、送信されるイベントごとに名前を割り当てます。{{site.data.keyword.iot_short_notm}} がデバイスからイベントを受け取ると、そのイベントを受け取った接続の資格情報に基づいて、イベント送信元デバイスが判別されます。このアーキテクチャーによって、デバイスが別のデバイスの偽名を使用するのを防止できます。

デバイスをはじめ、主要な概念について詳しくは、[About Watson IoT Platform](https://console.ng.bluemix.net/docs/services/IoT/iotplatform_overview.html#watsoniotplatform_importantconcepts) を参照してください。


# {{site.data.keyword.iot_short_notm}} へのデバイスの接続
{: #device_connect}
HTTP プロトコルまたは MQTT プロトコルを使用して、デバイスを {{site.data.keyword.iot_short_notm}} に接続できます。購入を行い、確認応答を受け取る、というような要求/応答シナリオを構成する場合は、HTTP を使用します。玄関のベルが鳴るとモバイル・デバイスのアラートがトリガーされる、というようなイベント・シナリオを構成する場合は、MQTT を使用します。

デバイスを {{site.data.keyword.iot_full}} に接続するためには、その前にデバイスを組織に登録しておく必要があります。{{site.data.keyword.iot_short_notm}} にセキュア接続するには、Bluemix アカウントに登録し、各自の {{site.data.keyword.iot_short_notm}} 組織を作成する必要があります。その後、この組織の ID を使用して、デバイスを登録できます。登録されたデバイスは、例えば MAC アドレスなどの固有のデバイス ID、および、そのデバイスにのみ受け入れられる認証トークンで {{site.data.keyword.iot_short_notm}} に識別されます。セキュアに接続した後に、Bluemix を使用して独自のアプリケーションを構築します。Node-RED を使用してアプリケーション同士をワイヤリングしてみてください。

PoC (概念検証) を実行するためなどの理由でデバイスを登録せずに接続する場合は、特別な組織 ID `QuickStart` を使用して行えます。`QuickStart` は、クラウド内で実行される {{site.data.keyword.iot_short_notm}} のパブリック・サンドボックス・インスタンスです。セキュア接続する必要がない場合は、`QuickStart` を使用して、デバイスの接続性をテストしたり {{site.data.keyword.iot_short_notm}} を試したりすることができます。検証作業が完了したら、TLS と各自の認証トークンを使用して、各自の固有の組織 ID インスタンスにデバイスをセキュアに再接続します。

HTTP プロトコルを使用した {{site.data.keyword.iot_short_notm}} へのデバイスの接続について詳しくは、[デバイス用の HTTP REST API](https://console.ng.bluemix.net/docs/services/IoT/devices/api.html) を参照してください。
MQTT プロトコルを使用した {{site.data.keyword.iot_short_notm}} へのデバイスの接続について詳しくは、[デバイスの MQTT 接続](https://console.ng.bluemix.net/docs/services/IoT/devices/mqtt.html)を参照してください。


# デバイス開発の概説
{: #get_started}
既に {{site.data.keyword.iot_short_notm}} に対して使用可能になっているデバイスは、すぐに使い始めることができます。

デバイスがまだ使用可能になっていない場合は、[developerWorks](https://developer.ibm.com/recipes/) に用意されているレシピを参照してください。既存のレシピの中で対象のデバイスに適したレシピがあるかどうか調べ、そのレシピを開発の取り掛かりに活用します。独自のレシピをパブリッシュすることもできます。

対象のデバイスに適したレシピが見つからなければ、IBM からさまざまなプログラミング・ガイドと API が 提供されているので、取り掛かりの参考にできます。これらのガイドには、デバイスとアプリケーションを統合して {{site.data.keyword.iot_short_notm}} に接続するためのコードの構築と開発に役立つクライアント・ライブラリー、サンプル、情報が記載されています。現在、以下のプログラミング・ガイドが用意されています。

- Java
- Node.js
- Embedded C
- ARM mBed C++
- Python
- C#
- Node-RED

用意されているプログラミング・ガイドの詳細情報やリンクについては、[{{site.data.keyword.iot_short_notm}} 開発用のクライアント・ライブラリー](../iot_platform_client_lib.html)を参照してください。

適切な {{site.data.keyword.iot_short_notm}} プログラミング・ガイドが見つからない場合、独自のプログラムを書き、MQTT または HTTP プロトコルを使用して、デバイスを {{site.data.keyword.iot_short_notm}} に接続することができます。

MQTT は、OASIS 標準化団体によって管理されるオープン・スタンダードであり、ISO で承認された国際標準です。詳しくは、[OASIS Message Queuing Telemetry Transport ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=mqtt){: new_window} を参照してください。

次の環境を含め、さまざまなシステムに対応した各種 MQTT クライアント・ライブラリーが用意されています。
- http://www.eclipse.org/paho/
- https://github.com/mqtt/mqtt.github.io/wiki/software?id=software

MQTT について詳しくは、[MQTT メッセージング](https://console.ng.bluemix.net/docs/services/IoT/reference/mqtt/index.html?pos=3)を参照してください。
