---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# アプリケーション開発者用の Java
{: #java}


Java™ を使用して、{{site.data.keyword.iot_full}} の組織と対話するアプリケーションを作成し、カスタマイズできます。アプリケーション開発を簡単に始められるように、{{site.data.keyword.iot_short_notm}} に対応した Java クライアント・ライブラリー、資料、サンプルが用意されています。

{:shortdesc}

## Java クライアントとリソースのダウンロード
{: #java_client_download}

最終更新日: 2016 年 10 月 25 日
{: .last-updated}

{{site.data.keyword.iot_short_notm}} 用の Java クライアント・ライブラリーとサンプルを利用するには、GitHub の [iot-java](https://github.com/ibm-watson-iot/iot-java) リポジトリーにアクセスし、インストール手順を実行します。


## コンストラクター
{: #constructor}

コンストラクターは、クライアント・インスタンスを作成し、以下の定義を格納する `Properties` オブジェクトを受け入れます。

| 定義     |説明     |
|----------------|----------------|
|`org` |組織 ID に設定する必要がある必須の値。Quickstart フローを使用する場合は、`quickstart` を指定します。|
|`id` |組織内のアプリケーション固有の ID。|
|`auth-method`  |認証の方式。サポートされている唯一の方式は `apikey` です。|
|`auth-key`   |オプションの API キー。auth-method の値を `apikey` に設定する場合は、これを指定する必要があります。|
|`auth-token`   |API キー・トークン。auth-method の値を `apikey` に設定する場合は、これも指定する必要があります。 |
|`clean-session`|true または false 値。永続サブスクリプション・モードでアプリケーションを接続する場合のみ必要です。デフォルトでは、`clean-session` は `true` に設定されます。|
|`Port`|接続先のポート番号。8883 か 443 のいずれかを指定してください。ポート番号を指定しない場合、クライアントは、デフォルトのポート番号 8883 で {{site.data.keyword.iot_short_notm}} に接続します。|
|`MaxInflightMessages`  |接続の処理中メッセージの最大数を設定します。デフォルト値は 100 です。|
|`Automatic-Reconnect`  |true か false の値。切断状態になったデバイスを自動的に {{site.data.keyword.iot_short_notm}} に再接続する場合は、これを指定する必要があります。デフォルト値は false です。|
|`Disconnected-Buffer-Size`|クライアントの切断中にメモリー内に保管できるメッセージの最大数。デフォルト値は 5000 です。|
|`shared-subscription`|ブール値。複数のアプリケーション・インスタンス間でメッセージのロード・バランシングを行うスケーラブルなアプリケーションを作成する場合は、true に設定する必要があります。詳しくは、[スケーラブルなアプリケーション](../mqtt.html#scalable_apps)を参照してください。

`Properties` オブジェクトによって、{{site.data.keyword.iot_short_notm}} モジュールとの対話に使用する定義が作成されます。このオブジェクトのプロパティーを指定しない場合、または `quickstart` を指定した場合、クライアントは {{site.data.keyword.iot_short_notm}} Quickstart サービスに未登録のデバイスとして接続します。

以下のコード・サンプルは、アプリケーション・クライアント (`ApplicationClient`) インスタンスを `quickstart` モードで作成する方法を示しています。

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

以下のコード・サンプルは、アプリケーション・クライアント (`ApplicationClient`) インスタンスを登録済みフロー・モードで作成する方法を示しています。

```
    Properties options = new Properties();
    options.put("org", "uguhsp");
    options.put("id", "app" + (Math.random() * 10000));
    options.put("Authentication-Method","apikey");
    options.put("API-Key", "<API-Key>");
    options.put("Authentication-Token", "<Authentication-Token>");

    ApplicationClient myClient = new ApplicationClient(options);
```

### 構成ファイルの使用

`Properties` オブジェクトを直接含める代わりに、`Properties` オブジェクトの名前と値のペアを指定した構成ファイルを使用することができます。以下のコード・サンプルにその概要を示します。

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
指定されたアプリケーション構成ファイルは、次の形式にする必要があります。

```
    [application]
    org=$orgId
    id=$myApplication
    auth-method=apikey
    auth-key=$key
    auth-token=$token
    enable-shared-subscription=true|false
```

## {{site.data.keyword.iot_short_notm}} への接続
{: #connecting_to_iotp}

{{site.data.keyword.iot_short_notm}} に接続するには、`connect()` 関数を使用します。`connect()` 関数には、`autoRetry` というオプションのブール値パラメーターが含まれています。このパラメーターで、MqttException 接続障害が発生した場合にライブラリーが再接続を試行するかどうかを指定できます。デフォルトでは、`autoRetry` は true に設定されます。渡されたデバイス登録の詳細に誤りがあったために MqttSecurityException 接続の障害が発生した場合は、`autoRetry` が true に設定されていても、ライブラリーは再接続を試行しません。

`connect()` 関数を呼び出す前に、`setKeepAliveInterval(int)` メソッドを使用して MQTT のキープアライブ間隔を設定することもできます。`setKeepAliveInterval(int)` の値は、秒単位で指定します。このメソッドで、送受信されるメッセージとメッセージの間隔の最大時間を定義できます。このメソッドを使用すると、クライアントは、TCP/IP タイムアウト期間の終了を待たずに、サーバーが使用不能になったことを検出できます。クライアントは、それぞれのキープアライブ間隔の期間中に少なくとも 1 つのメッセージがネットワークを通過するかどうかを確認します。タイムアウト期間中に受け取るデータ関連メッセージがゼロであれば、クライアントは、小さな `ping` メッセージを送信してサーバーに応答してもらいます。`setKeepAliveInterval(int)` は、デフォルトで 60 秒に設定されます。クライアントでキープアライブ処理機能を無効にする場合は、`setKeepAliveInterval(int)` の値を 0 に設定します。

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    myClient.setKeepAliveInterval(120);
    myClient.connect();
```

接続障害が発生した場合の再試行の数を制御するために、myClient.connect() 関数で整数を指定してください。以下のコード・スニペットに概要を示します。

```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(10);
```

アプリケーション・クライアントは、{{site.data.keyword.iot_short_notm}} サービスに正常に接続してから、デバイスのイベントと状況にサブスクライブできます。また、デバイスのイベントとコマンドをパブリッシュすることも可能です。

## デバイス・イベントのサブスクライブ
{: #subscribing_device_events}

イベントとは、デバイスが {{site.data.keyword.iot_short_notm}} にデータをパブリッシュするためのメカニズムのことです。デバイスはイベントの内容を制御し、送信するイベントごとに名前を割り当てます。

{{site.data.keyword.iot_short_notm}} インスタンスがイベントを受信すると、その受信イベントの資格情報によって、送信元デバイスが識別されます。そのためデバイスが、別のデバイスになりすますことはできません。


デフォルトでは、アプリケーションは、すべての接続デバイスのすべてのイベントをサブスクライブします。デバイス・タイプ、デバイス ID、イベント、メッセージ・フォーマットの各パラメーターを使用して、サブスクリプションの範囲を制御できます。次のコード・サンプルは、これらのパラメーターを使用してサブスクリプションの範囲を定義する方法を示しています。

### すべてのデバイスのすべてのイベントをサブスクライブする


```
    myClient.connect();
    myClient.subscribeToDeviceEvents();
```
### 特定のタイプに属するすべてのデバイスのすべてのイベントをサブスクライブする


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino");
```

### 特定のデバイスのすべてのイベントをサブスクライブする


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee");
```
### 複数の異なるデバイスの特定のイベントをサブスクライブする

```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent");
    myClient.subscribeToDeviceEvents("iotsample-arduino", "10aabbccddee", "myEvent");
```
### JSON フォーマットでパブリッシュされたイベントをサブスクライブする


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent", "json", 0);
```

**注**: 単一のクライアントで複数のサブスクリプションをサポートできます。

## デバイスからのイベントの処理
{: #handling_device_events}

サブスクリプションで受信したイベントを処理するには、イベント・コールバック・メソッドを登録します。メッセージは、以下のパラメーターを持つ Event クラスのインスタンスとして返されます。

|パラメーター|データ・タイプ|説明|
|:---|:---|
|`event.device`|ストリング|組織内のすべてのタイプのデバイスにおいて対象デバイスを一意に識別します。|
|`event.deviceType`|ストリング|デバイス・タイプを識別します。通常、deviceType は、特定のタスクを実行するデバイスのグループです (例えば、"weatherballoon" などのデバイス・タイプを指定できます)。|
|`event.deviceId`|ストリング|デバイスの ID を示します。通常、特定のデバイス・タイプにおいて、deviceId はそのデバイスの固有 ID です (シリアル番号や MAC アドレスなど)。|
|`event.event`|ストリング|通常、特定の複数のイベントをグループ化するために使用します (「status」、「warning」、「data」など)。|
|`event.format`|ストリング|形式は任意のストリング (JSON など) となります。  |
|`event.data`|辞書|メッセージ・ペイロードのデータ。最大長は 131072 バイトです。|
|`event.timestamp`|日時|イベントの日時|


以下のコードは、イベント・コールバックの実装例を示しています。

```
  import com.ibm.iotf.client.app.Event;
  import com.ibm.iotf.client.app.EventCallback;
  import com.ibm.iotf.client.app.Command;

  import java.util.concurrent.BlockingQueue;
  import java.util.concurrent.LinkedBlockingQueue;

  /**
    * A sample Event callback class that processes the device events in a separate thread.
    *
    */
   class MyEventCallback implements EventCallback, Runnable {

	// A queue to hold and process the Events for smooth handling of MQTT messages
	private BlockingQueue<Event> evtQueue = new LinkedBlockingQueue<Event>();

	public void processEvent(Event e) {
		try {
			evtQueue.put(e);
		} catch (InterruptedException e1) {
			e1.printStackTrace();
		}
	}

	@Override
	public void processCommand(Command cmd) {
		System.out.println("Command received:: " + cmd);
	}

	@Override
	public void run() {
		while(true) {
			Event e = null;
			try {
				e = evtQueue.take();
				// In this example, the only output is the event
				System.out.println("Event:: " + e.getDeviceId() + ":" + e.getEvent() + ":" + e.getPayload());
			} catch (InterruptedException e1) {
				// Ignore the Interuppted exception, retry
				continue;
			}
		}
	}
    }
```

このイベント・コールバックを ApplicationClient に追加すると、サブスクリプションと一致するイベントがパブリッシュされた場合に `processEvent()` メソッドが呼び出されます。次のコード・スニペットは、イベント・コールバックを ApplicationClient インスタンスに追加する方法を示しています。



```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceEvents();
```

デバイス・イベントのサブスクライブと同様に、アプリケーションはデバイスに送信されるコマンドをサブスクライブできます。以下のコード・サンプルは、組織内のすべてのデバイスに対するすべてのコマンドをサブスクライブする方法を示しています。

```

    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceCommands();
```

コマンド・サブスクリプションを制御するために、複数の多重定義メソッドが用意されています。コマンド・サブスクリプションと一致するデバイスにコマンドが送信されると、`processCommand()` メソッドが呼び出されます。


## デバイス状況のサブスクライブ
{: #subscribing_device_status}

アプリケーションは、デバイス・イベントをサブスクライブする場合と同様に、デバイス状況 ({{site.data.keyword.iot_short_notm}} との接続の確立や切断など) をサブスクライブできます。デフォルトでは、このサブスクリプションは、すべての接続デバイスの状況更新をサブスクライブします。デバイス・タイプとデバイス ID のパラメーターを使用して、サブスクリプションの範囲を制御できます。次のコード・サンプルは、これらのパラメーターを使用してサブスクリプションの範囲を定義する方法を示しています。

### すべてのデバイスの状況更新をサブスクライブする

```
    myClient.connect();
    myClient.subscribeToDeviceStatus();
```

### 特定のタイプのすべてのデバイスの状況更新をサブスクライブする


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino");
```

### 2 つの異なるデバイスの状況更新をサブスクライブする


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino", "00aabbccddee");
    myClient.subscribeToDeviceStatus("iotsample-arduino", "10aabbccddee");
```

**注**: 単一のクライアントで複数のサブスクリプションをサポートできます。

## デバイスからの状況更新の処理
{: #handling_device_status_updates}

サブスクリプションで受信した状況更新を処理するには、状況イベント・コールバック・メソッドを登録する必要があります。状況イベント `Connect` と `Disconnect` の場合、メッセージは、以下のパラメーターを持つ Status クラスのインスタンスとして返されます。


| パラメーター     |データ・タイプ     |
|----------------|----------------|
|`status.clientAddr` |string|
|`status.protocol`  |string|
|`status.clientId`   |string|
|`status.user`   |string|
|`status.time`   |java.util.Date|
|`status.action` |string|
|`status.connectTime`   |java.util.Date|
|`status.port`|integer|

以下のプロパティーは、状況イベントが `Disconnect` である場合にのみ設定されます。

| プロパティー     |データ・タイプ     |
|----------------|----------------|
|`status.writeMsg` |integer|
|`status.readMsg`  |integer|
|`status.reason`   |string|
|`status.readBytes`   |integer|
|`status.writeBytes`   |integer|


以下のコード・サンプルは、状況コールバックの実装例を示しています。

```

  private static class MyStatusCallback implements StatusCallback {

      public void processApplicationStatus(ApplicationStatus status) {
          System.out.println("Application Status = " + status.getPayload());
      }

      public void processDeviceStatus(DeviceStatus status) {
          if(status.getAction() == "Disconnect") {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction()
                                  + "  reason: " + status.getReason());
          } else {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction());
          }
      }
  }
```

この状況コールバックをアプリケーション・クライアントに追加すると、基準に一致するデバイスの {{site.data.keyword.iot_short_notm}} への接続が確立されたり切断されたりした場合に `processDeviceStatus()` メソッドが呼び出されます。以下のコード・サンプルは、状況コールバック・インスタンスをアプリケーション・クライアントに追加する方法を示しています。

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
アプリケーションは、他のあらゆるアプリケーション状況 ({{site.data.keyword.iot_short_notm}} へのアプリケーションの接続や切断など) をサブスクライブできます。以下のコード・スニペットは、{{site.data.keyword.iot_short_notm}} 組織のアプリケーション状況にサブスクライブする方法を示しています。

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
特定のアプリケーション状況へのサブスクリプションを制御するために、多重定義メソッドが用意されています。基準に一致するアプリケーションの {{site.data.keyword.iot_short_notm}} への接続が確立されたり切断されたりした場合に `processApplicationStatus()` メソッドが呼び出されます。


## デバイスからのイベントのパブリッシュ
{: #publishing_events_devices}

以下のコード・サンプルは、アプリケーションが、デバイスからパブリッシュされたかのようにイベントをパブリッシュする方法を示しています。

```

    myClient.connect()

    //Generate the event to be published
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

    // publish the event on behalf of device
    myClient.publishEvent(deviceType, deviceId, "blink", event);
```


さまざまな形式でイベントをパブリッシュできます。例えば、JSON、ストリング、バイナリーなどの形式が可能です。デフォルトでは、ライブラリーは、JSON 形式でイベントをパブリッシュしますが、別の形式のデータを指定することもできます。例えば、ストリング形式のデータをパブリッシュする場合は、以下のコード・スニペットを使用します。

```
    myClient.connect();
    String data = "cpu:"+60;
    status = myClient.publishEvent("load", data, "text", 2);
```
**注:** 前のコード例では、イベントのペイロードをストリング形式にする必要があります。

XML データは、ストリングに変換して以下のようにパブリッシュできます。

```
    status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

同じように、バイナリー形式のイベントをパブリッシュする場合は、バイト配列を使用します。その概要を以下の例に示します。

```
    myClient.connect();
    byte[] cpuLoad = new byte[] {60, 35, 30, 25};
    status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### HTTP によるイベントのパブリッシュ
{: #publishing_events_http}

MQTT のほかにも、HTTP を使用してデバイス・イベントを {{site.data.keyword.iot_short_notm}} にパブリッシュするようにアプリケーションを構成することもできます。HTTP を介してデバイス・イベントをパブリッシュする手順の概要を以下に示します。

1. プロパティー・ファイルを使用して ApplicationClient インスタンスを作成する。
2. パブリッシュする必要があるイベントを作成する。
3. イベント名、デバイス・タイプ、デバイス ID を指定する。
4. `publishEventOverHTTP`() メソッドを使用してイベントをパブリッシュする。以下にコード例を示します。

```
    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	boolean status = myClient.publishApplicationEventforDeviceOverHTTP(deviceId, deviceType, "blink", event, ContentType.json);
```

コード・サンプル全体を確認するには、[HttpApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java) というアプリケーションのサンプルを参照してください。

プロパティー・ファイルの設定に基づいて、`publishEventOverHTTP()` メソッドが、Quickstart または登録されたフローでイベントをパブリッシュします。プロパティー・ファイルで組織 ID として `quickstart` を指定すると、`publishEventOverHTTP()` メソッドは、{{site.data.keyword.iot_short_notm}} Quickstart サービスにプレーン HTTP 形式でイベントをパブリッシュします。登録されている有効な組織をプロパティー・ファイルに指定した場合は、イベントのパブリッシュに必ず HTTPS が使用されるため、すべての通信が保護されます。

HTTP プロトコルによる配信は「最高 1 回」の送信です。これは、MQTT プロトコルのサービス品質レベル「最高 1 回」(QoS 0) に似ています。「最高 1 回」の送信を使用してイベントをパブリッシュする場合、アプリケーションはエラー発生時の再試行ロジックを実装する必要があります。


## デバイスへのコマンドのパブリッシュ
{: #publishing_commands_devices}

アプリケーションは、次の例に示すように、接続デバイスにコマンドをパブリッシュできます。

```

    myClient.connect()

    //Generate the event to be published
    JsonObject data = new JsonObject();
    data.addProperty("name", "stop-rotation");
    data.addProperty("delay",  0);

    //Registered flow allows 0, 1 and 2 QoS
    myAppClient.publishCommand(deviceType, deviceId, "stop", data);
```

### HTTP を使用したコマンドのパブリッシュ
{: #publishing_commands_http}

MQTT のほかにも、HTTP を使用してコマンドを接続先のデバイスにパブリッシュするようにアプリケーションを構成することともできます。HTTP を使用してデバイス・イベントをパブリッシュする手順の概要を以下に示します。

1. プロパティー・ファイルを使用して ApplicationClient インスタンスを作成する
2. パブリッシュする必要があるコマンドを作成する
3. コマンド名、デバイス・タイプ、デバイス ID を指定する
4. 次のコードに示すように、`publishCommandOverHTTP`() メソッドを使用してコマンドをパブリッシュする

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	// Generate a JSON object of the event to be published
	JsonObject event = new JsonObject();
	event.addProperty("reboot", 5);

	boolean response = myClient.publishCommandOverHTTP("execute", event);
```

コード・サンプル全体を確認するには、[HttpCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpCommandPublish.java) というアプリケーションのサンプルを参照してください。

HTTP プロトコルによる配信は「最高 1 回」の送信です。これは、MQTT プロトコルのサービス品質レベル「最高 1 回」(QoS 0) に似ています。「最高 1 回」の送信を使用してコマンドをパブリッシュする場合、アプリケーションはエラー発生時の再試行ロジックを実装する必要があります。詳しくは、[アプリケーションの HTTP REST API](../api.html)を参照してください。


## サンプル
{: #samples}

-  [MQTTApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java) - デバイス・イベントをパブリッシュする方法を示すサンプル・アプリケーション。
-   [RegisteredApplicationCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java) - コマンドをデバイスにパブリッシュする方法を示すサンプル・アプリケーション。
-  [RegisteredApplicationSubscribeSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java) - デバイス・イベント、デバイス・コマンド、デバイス状況、アプリケーション状況などのさまざまなイベントをサブスクライブする方法を示すサンプル・アプリケーション。
-   [SharedSubscriptionSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java) - 複数のアプリケーション・インスタンス間でメッセージのロード・バランシングを行うスケーラブルなアプリケーションを作成する方法を示すサンプル・アプリケーション。
-  [Backup-restore-sample](https://github.com/ibm-messaging/iot-backup-restore-sample) - {{site.data.keyword.cloudant}}のデバイス構成をバックアップおよびリストアする方法を示すサンプル。
