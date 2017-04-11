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

#Java を使用した {{site.data.keyword.iot_short_notm}} でのゲートウェイの開発
{: #java_cli_gw}

デバイスを {{site.data.keyword.iot_full}} 上の組織に直接接続できない場合、Java™ を使用してゲートウェイを構築してカスタマイズできます。ゲートウェイ開発を簡単に始められるように、{{site.data.keyword.iot_short_notm}} に対応した Java クライアント・ライブラリー、資料、サンプルが用意されています。
{:shortdesc}

## Java クライアントとリソースのダウンロード
{: #java_client_download}

{{site.data.keyword.iot_short_notm}} 用の Java クライアント・ライブラリーとサンプルを利用するには、GitHub の [iot-java](https://github.com/ibm-watson-iot/iot-java) リポジトリーにアクセスし、インストール手順を実行します。

## コンストラクター
{: #constructor}

コンストラクターは、ゲートウェイ・クライアント・インスタンスを作成し、以下の定義を格納する `Properties` オブジェクトを受け入れます。

|定義 |説明 |
|:----|:----|
|`org`|組織 ID に設定する必要がある必須の値。Quickstart フローを使用する場合は、`quickstart` を指定します。|
|`domain`|メッセージング・エンドポイント URL (オプション)。ドメインの値を指定しない場合、URL はデフォルトの `internetofthings.ibmcloud.com` になります。これは {{site.data.keyword.iot_short_notm}} 実動サーバーです。|
|`type`|ゲートウェイのタイプを指定する必須の値。|
|`id` |ゲートウェイの固有の ID を指定する必須の値。|
|`auth-method`|使用する認証の方式。サポートされている唯一の方式は `token` です。|
|`auth-token`|ゲートウェイを {{site.data.keyword.iot_short_notm}} にセキュア接続するための API キー認証トークン。|
|`clean-session`|true または false の値。永続サブスクリプション・モードでゲートウェイを接続する場合のみ必要です。デフォルトでは、`clean-session` は true に設定されます。|
|`WebSocket`|true または false の値。Web ソケットを使用してゲートウェイを接続する場合のみ必要です。|
|`Port`|接続先のポート番号。8883 か 443 のいずれかを指定してください。ポート番号を指定しない場合、クライアントは、デフォルトのポート番号 8883 で {{site.data.keyword.iot_short_notm}} に接続します。|
|`MaxInflightMessages`|接続の処理中メッセージの最大数を設定します。デフォルト値は 100 です。|
|`Automatic-Reconnect`|true か false の値。切断状態になったゲートウェイを自動的に {{site.data.keyword.iot_short_notm}} に再接続する場合は、これを指定する必要があります。デフォルト値は false です。|
|`Disconnected-Buffer-Size`|クライアントの切断中にメモリー内に保管できるメッセージの最大数。デフォルト値は 5000 です。|

**注:** 永続サブスクリプション・モードでゲートウェイを接続するには、`clean-session` を `false` に設定します。クリーン・セッションについて詳しくは、[MQTT 資料](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)の『サブスクリプション・バッファーとクリーン・セッション』のセクションを参照してください。

`Properties` オブジェクトによって、{{site.data.keyword.iot_short_notm}} モジュールとの対話に使用する定義が作成されます。

次のコード・サンプルは、ゲートウェイ・クライアント・インスタンスを構成する方法を示しています。

```java
Properties options = new Properties();
options.setProperty("org", "<Your organization ID>");
options.setProperty("type", "<The gateway device type>");
options.setProperty("id", "The gateway device ID");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "API token");
GatewayClient gwClient = new GatewayClient(options);

```


### 構成ファイルの使用

ゲートウェイ・インスタンスを作成する際に `Properties` オブジェクトを直接使用する代わりに、ゲートウェイのプロパティーの名前と値のペアを含む構成ファイルを使用できます。構成ファイルを使用してゲートウェイの `Properties` オブジェクトを構築するには、次のコード形式を使用します。

```Java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
...
```

構成ファイルの内容は、次の形式でなければなりません。

```java
[Gateway]
org=$orgId
domain=$domain
typ=$myGatewayDeviceType
id=$myGatewayDeviceId
auth-method=token
auth-token=$token

```

## {{site.data.keyword.iot_short_notm}} への接続
{: #connecting_to_iotp}

{{site.data.keyword.iot_short_notm}} に接続するには、`connect()` 関数を使用します。`connect()` 関数には、`autoRetry` というオプションのブール値パラメーターが含まれています。このパラメーターは、MQTT 例外 (MqttException) 接続が失敗したときにライブラリーが再接続を試みるかどうかを決定します。デフォルトでは、`autoRetry` は true に設定されます。渡されたデバイス登録の詳細に誤りがあったために MqttSecurityException 接続の障害が発生した場合は、`autoRetry` が true に設定されていても、ライブラリーは再接続を試行しません。

`connect()` 関数を呼び出す前に、`setKeepAliveInterval(int)` メソッドを使用して MQTT のキープアライブ間隔を設定することもできます。`setKeepAliveInterval(int)` の値は、秒単位で指定します。このメソッドで、送受信されるメッセージとメッセージの間隔の最大時間を定義できます。`setKeepAliveInterval(int)` 値が指定された場合、クライアントは、サーバーが使用不能になったことを、TCP/IP タイムアウト期間の終わりに達するのを待たずに検出できます。クライアントは、それぞれのキープアライブ間隔期間中に少なくとも 1 つのメッセージがネットワークを通過するかどうかを確認します。タイムアウト期間中に受け取るデータ関連メッセージがゼロであれば、クライアントは、小さな `ping` メッセージを送信してサーバーに応答してもらいます。`setKeepAliveInterval(int)` は、デフォルトで 60 秒に設定されます。クライアントでキープアライブ処理機能を無効にする場合は、`setKeepAliveInterval(int)` の値を 0 に設定します。

```java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient.connect();
```

接続が失敗したときに行われる再試行の回数を制御するには、connect(int numberOfTimesToRetry) 多重定義関数を使用します。

```java
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient .connect(10);
```

ゲートウェイ・クライアントが {{site.data.keyword.iot_short_notm}} に正常に接続されると、ゲートウェイは、ゲートウェイ自体のイベントをパブリッシュしてコマンドをサブスクライブすることも、ゲートウェイにアタッチされたデバイスの代わりに同じことをすることもできます。

## ゲートウェイの背後のデバイスの登録
{: #register_device_gateway}

自動的に、または API を使用してコードを開発することによって、{{site.data.keyword.iot_short_notm}} インスタンスに接続されたゲートウェイの背後のデバイスを登録できます。

### デバイスの自動登録
ゲートウェイがその接続されたデバイスのイベントをパブリッシュしたり、コマンドをサブスクライブしたりするたびに、デバイスを {{site.data.keyword.iot_short_notm}} に自動的に登録できます。

### API デバイスの登録
{{site.data.keyword.iot_short_notm}} API を使用して、ゲートウェイの背後のデバイスを {{site.data.keyword.iot_short_notm}} インスタンスに登録することもできます。

{{site.data.keyword.iot_short_notm}} API を使用した開発を簡素化するには、api() メソッドを呼び出して API クライアント・インスタンスを開始します。この概要を次のコード・サンプルに示します。

```java
import com.ibm.iotf.client.api.APIClient;
....

GatewayClient gwClient = new GatewayClient(props);
gwClient.connect();

APIClient api = gwClient.api();
```
API クライアントのハンドルを受け取ったら、ゲートウェイへのデバイスの登録を開始できます。この概要を次のコード・サンプルに示します。
```java
gwClient.connect();

  String deviceToBeAdded = "{\"deviceId\": \"" + DEVICE_ID +
					"\",\"authToken\": \"qwer123\"}";

    JsonParser parser = new JsonParser();
    JsonElement input = parser.parse(deviceToBeAdded);
    JsonObject response = this.gwClient.api().registerDeviceUnderGateway(DEVICE_TYPE, gwDeviceId, gwDeviceType, input);

```

ゲートウェイの背後のデバイスが登録されるとき、そのデバイスは `gwDeviceId` 属性と `gwDeviceType` 属性の値でゲートウェイと関連付けられます。

## イベントのパブリッシュ
{: #publish_events}

イベントとは、ゲートウェイおよびデバイスが {{site.data.keyword.iot_short_notm}} にデータをパブリッシュするためのメカニズムのことです。ゲートウェイまたはデバイスはイベントの内容を制御し、送信するイベントごとに名前を割り当てます。ゲートウェイは、ゲートウェイ自体のイベントをパブリッシュすることも、ゲートウェイを経由して接続しているデバイスの代わりにイベントをパブリッシュすることもできます。

{{site.data.keyword.iot_short_notm}} インスタンスがイベントを受信すると、その受信イベントの資格情報によって、送信元ゲートウェイが識別されます。そのためゲートウェイが、別のデバイスになりすますことはできません。

イベントは、MQTT プロトコルによって定義された 3 つの[サービス品質 (QoS) レベル](../../reference/mqtt/index.html#qos-levels)のいずれでもパブリッシュできます。デフォルトでは、イベントは QoS=0 でパブリッシュされます。

### デフォルトの QoS レベルでゲートウェイ・イベントをパブリッシュするためのコード

```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event);
```

### イベントのデフォルトの QoS レベルを引き上げるためのコード

パブリッシュされるゲートウェイ・イベントの [QoS レベル](../../reference/mqtt/index.html#qos-levels)を引き上げることができます。QoS レベルが 0 より大きいイベントは、追加の確認受信情報が含まれているため、パブリッシュにかかる時間が延びる可能性があります。


```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event, 2);
```

### カスタム形式のイベントをパブリッシュするためのコード

さまざまな形式でイベントをパブリッシュできます。例えば、JSON、ストリング、バイナリーなどの形式が可能です。デフォルトでは、ライブラリーは、JSON 形式でイベントをパブリッシュしますが、別の形式のデータを指定することもできます。例えば、ストリング形式のデータをパブリッシュするには、次のコード・スニペットを使用します。

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishGatewayEvent("load", data, "text", 2);
```

**注:** 前のコード例では、イベントのペイロードをストリング形式にする必要があります。

XML データはストリング形式に変換してパブリッシュできます。この概要を次のコード・サンプルに示します。

```java
status = gwClient.publishGatewayEvent("load", xmlConvertedString, "xml", 2);
```

同じように、バイナリー形式のイベントをパブリッシュする場合は、バイト配列を使用します。その概要を以下の例に示します。

```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishGatewayEvent("blink", cpuLoad , "binary", 1);
```

### デバイスからのイベントをパブリッシュするためのコード
{: #publishing_events_devices}

ゲートウェイは、元のイベントの適切なタイプ ID とデバイス ID の値を渡すことによって、ゲートウェイ経由で接続されているデバイスの代わりにイベントをパブリッシュできます。この概要を次のサンプルに示します。

```java

gwClient.connect()

//Generate the event to be published
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

    // publish the event on behalf of device
gwClient.publishDeviceEvent(deviceType, deviceId, eventName, event);
```

`publishDeviceEvent()` 多重定義メソッドを使用して、優先するサービス品質レベルでデバイス・イベントをパブリッシュします。使用されるトピック構造について詳しくは、[ゲートウェイの MQTT 接続](../mqtt.html)を参照してください。

### カスタム形式のデバイス・イベントをパブリッシュするためのコード

ゲートウェイ・イベントと同じように、デバイス・イベントもさまざまな形式でパブリッシュできます。デフォルトでは、ライブラリーは JSON 形式でデバイス・イベントをパブリッシュしますが、別の形式のデータを指定することもできます。例えば、ストリング形式のデータをパブリッシュするには、次のコード・サンプルを使用します。

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", data, "text", 2);
```

**注:** イベントのペイロードはストリング形式でなければなりません。

XML データはストリング形式に変換してパブリッシュできます。次に例を示します。

```java
status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", xmlConvertedString, "xml", 2);
```

同じように、バイナリー形式のデバイス・イベントをパブリッシュするには、バイト配列を使用します。この概要を次の例に示します。
```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishDeviceEvent(deviceType, deviceId, "blink", cpuLoad , "binary", 1);
```

## コマンドの処理
{: #handling_commands}

ゲートウェイは、ゲートウェイ自体に対するコマンドも、ゲートウェイの背後に接続されているデバイスに対するコマンドもサブスクライブできます。ゲートウェイ・クライアントは、接続時に、このゲートウェイに対するコマンドに自動的にサブスクライブします。ただし、ゲートウェイを介して接続されているデバイスに対するコマンドをサブスクライブするには、`subscribeToDeviceCommands()` 多重定義メソッドを使用します。この概要を次の例に示します。

```java
gwClient.connect()

// subscribe to commands on behalf of device
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

特定のコマンドを処理するには、`Command` コールバック・メソッドを登録する必要があります。メッセージは `Command` クラスのインスタンスとして返され、以下のプロパティーが含まれます。


| プロパティー     |データ・タイプ     | 説明|
|----------------|----------------|---------------
|`deviceType`|ストリング| コマンドを受け取るデバイスのタイプ。|
|`deviceId`|ストリング| コマンドを受け取るデバイスの ID。これはゲートウェイか、またはゲートウェイを介して接続されているデバイスのどちらかです。|
|`data`|オブジェクト| コマンド・ペイロード。|
|`format`|ストリング| コマンド・ペイロードの形式。何らかのストリングになります (例えば、JSON、バイナリー、テキストなど)。|
|`command`|ストリング|コマンドの名前。|
|`timestamp`|org.joda.time.DateTime|コマンドが送信された時点の日時。|

次のコード・サンプルは、`Command` コールバック・メソッドの実装方法の概要を示しています。

```java
import com.ibm.iotf.client.gateway.Command;
import com.ibm.iotf.client.gateway.GatewayCallback;

public class GatewayCommandCallback implements GatewayCallback, Runnable {
	// A queue to hold and process the commands
	private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

	public void processCommand(Command cmd) {
  	    queue.put(cmd);
  	}

  	public void run() {
  	    while(true) {
			Command cmd = queue.take();
  	        System.out.println("Command " + cmd.getData());

  	        // code to process the command
  	    }
  	}

  	/**
	 * If a gateway subscribes to a topic of a device or sends data on behalf of a device
	 * that the gateway does not have permission to connect to, the message or the subscription is ignored.
	 * This behavior is different compared with the behavior of applications, where the connection is terminated.
	 * The Gateway is notified on the the notification topic:
	 */
  	@Override
public void processNotification(Notification notification) {

}
  }

```
`Command` コールバックがゲートウェイ・クライアントに追加されると、サブスクライブされた基準が含まれるコマンドがパブリッシュされるたびに、`processCommand()` メソッドが呼び出されます。
次のコード・サンプルは、ゲートウェイ・クライアント・インスタンスに `Command` コールバックを追加する方法の概要を示しています。

```java
gwClient.connect()
GatewayCommandCallback callback = new GatewayCommandCallback();
gwClient.setGatewayCallback(callback);
//Subscribe to a device that is connected to the gateway
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

コマンド・サブスクリプションを制御するために、複数の多重定義メソッドが用意されています。

### ゲートウェイを介して接続されているデバイスのリスト
{: #list_devices_gw}


指定したゲートウェイ (typeId、deviceId) を介して {{site.data.keyword.iot_short_notm}} に接続されているデバイスをすべて検索するには、`getDevicesConnectedThroughGateway()` メソッドを呼び出します。

```java
gwClient.connect()
gwClient.api().getDevicesConnectedThroughGateway(gatewayType, gatewayId);
```

## サンプル
{: #samples}

ゲートウェイとゲートウェイの背後のデバイスを {{site.data.keyword.iot_short_notm}} インスタンスに接続するためのサンプルがいくつか用意されています。これらのサンプルは {{site.data.keyword.iot_short_notm}} Java クライアント・ライブラリーを使用しており、[ゲートウェイ・サンプル GitHub リポジトリー ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples){: new_window} に置かれています。

## レシピ
{: #recipes}

| レシピ     | 説明|
|----------------|----------------
|[Connecting your device as a gateway to {{site.data.keyword.iot_short_notm}} ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-gateway-to-watson-iot-platform/){: new_window}| GitHub プロジェクト。Raspberry Pi ゲートウェイとゲートウェイの背後の Arduino Uno デバイスを {{site.data.keyword.iot_short_notm}} に接続する方法に関する詳細手順です。
|[Raspberry Pi as a managed gateway in {{site.data.keyword.iot_short_notm}} ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/){: new_window}|上記のゲートウェイ・レシピの拡張。Raspberry Pi ゲートウェイを {{site.data.keyword.iot_short_notm}} 内の管理対象デバイスとして接続する方法と、デバイス管理の操作方法を説明しています。
