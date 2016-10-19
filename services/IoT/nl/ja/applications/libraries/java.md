---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# アプリケーション開発者用の Java
{: #java}

最終更新日: 2016 年 9 月 7 日
{: .last-updated}

Java を使用して、{{site.data.keyword.iot_full}} の組織と対話するアプリケーションを作成し、カスタマイズできます。Java を使用したアプリケーションの開発を始められるように情報やサンプルが用意されているので活用してください。
{:shortdesc}

## Java クライアントとリソースのダウンロード
{: #java_client_download}

{{site.data.keyword.iot_short_notm}} 用の Java クライアント・ライブラリーとサンプルを利用するには、GitHub の [iot-java](https://github.com/ibm-watson-iot/iot-java) リポジトリーにアクセスし、インストール手順を実行します。


## コンストラクター
{: #constructor}

コンストラクターは、クライアント・インスタンスを作成し、以下の定義を格納する `Properties` オブジェクトを受け入れます。

| 定義     |説明     |
|----------------|----------------|
|`org` |組織 ID。これは必須値です。Quickstart フローを使用する場合は、`quickstart` を指定します。|
|`id` |組織内のアプリケーション固有の ID。|
|`auth-method`  |認証方式。現在サポートされている値は、`apikey` のみです。|
|`auth-key`   |オプションの API キー。auth-method を `apikey` に設定する場合には必須です。  |
|`auth-token`   |API キー・トークン。auth-method を `apikey` に設定する場合には必須です。 |
|`clean-session`|true または false 値。永続サブスクリプション・モードでアプリケーションを接続する場合のみ必要です。デフォルトでは、`clean-session` は `true` に設定されます。|
|`shared-subscription`|ブール値。複数のアプリケーション・インスタンス間でメッセージのロード・バランシングを行うスケーラブルなアプリケーションを作成する場合は、`true` に設定します。詳しくは、[スケーラブルなアプリケーション](mqtt.html#/scalable-applications#scalable-applications)を参照してください。

`Properties` オブジェクトによって、{{site.data.keyword.iot_short_notm}} モジュールとの対話に使用する定義が作成されます。このオブジェクトのプロパティーを指定しない場合、または `quickstart` を指定した場合、クライアントは {{site.data.keyword.iot_short_notm}} Quickstart サービスに未登録のデバイスとして接続します。

以下のコード・サンプルは、ApplicationClient インスタンスを `quickstart` モードで作成する方法を示しています。

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

以下のコード・サンプルは、ApplicationClient インスタンスを登録済みフロー・モードで作成する方法を示しています。

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

`Properties` オブジェクトを直接含める代わりに、`Properties` オブジェクトの名前と値のペアを次の形式で含む構成ファイルを使用することもできます。

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
このアプリケーション構成ファイルは、次の形式にする必要があります。

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

{{site.data.keyword.iot_short_notm}} に接続するには、`connect()` 関数を使用します。`connect()` 関数には、`autoRetry` というオプションのブール値パラメーターが含まれていて、これにより、MqttException 接続に障害が発生した場合にライブラリーが再接続を試行するかどうかを指定します。デフォルトでは、`autoRetry` は true に設定されます。渡されたデバイス登録の詳細に誤りがあったために MqttSecurityException 接続の障害が発生した場合は、`autoRetry` が `true` に設定されていても、ライブラリーは再接続を試行しません。

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);

    myClient.connect();
```

{{site.data.keyword.iot_short_notm}} サービスに正常に接続できたら、アプリケーション・クライアントはデバイス・イベントやデバイス状況をサブスクライブし、デバイス・イベントやコマンドをパブリッシュできます。

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
|`event.deviceType`|ストリング|デバイス・タイプを識別します。通常、deviceType は、特定のタスクを実行するデバイスのグループです (例えば "weatherballoon")。|
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

この状況コールバックを ApplicationClient に追加すると、基準に一致するデバイスの {{site.data.keyword.iot_short_notm}} への接続が確立されたり切断されたりした場合に `processDeviceStatus()` メソッドが呼び出されます。以下のコード・サンプルは、状況コールバック・インスタンスを ApplicationClient に追加する方法を示しています。

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
アプリケーションは、他のあらゆるアプリケーション状況 (Watson IoT Platform へのアプリケーションの接続や切断など) をサブスクライブできます。以下のコード・スニペットは、組織のアプリケーション状況にサブスクライブする方法を示しています。

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
特定のアプリケーション状況へのサブスクリプションを制御するために、多重定義メソッドが用意されています。基準に一致するアプリケーションの {{site.data.keyword.iot_short_notm}} への接続が確立されたり切断されたりした場合に processApplicationStatus() メソッドが呼び出されます。


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

### HTTP によるイベントのパブリッシュ
{: #publishing_events_http}

MQTT のほかにも、HTTP を使用してデバイス・イベントを {{site.data.keyword.iot_short_notm}} にパブリッシュするようにアプリケーションを構成できます。そのためには、次の手順を実行します。

* プロパティー・ファイルを使用して ApplicationClient インスタンスを作成する
* パブリッシュする必要があるイベントを作成する
* イベント名、デバイス・タイプ、デバイス ID を指定する
* 次のコードに示すように、`publishEventOverHTTP`() メソッドを使用してイベントをパブリッシュする

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	code = myClient.publishEventOverHTTP(deviceType, deviceId, "blink", event);
```

完全なコード・サンプルを確認したい場合は、次のアプリケーション・サンプルを参照してください。

[HttpApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java)

プロパティー・ファイルの設定に基づいて、`publishEventOverHTTP()` メソッドが、Quickstart または登録されたフローでイベントをパブリッシュします。`quickstart` がプロパティー・ファイルに指定された組織 ID である場合、`publishEventOverHTTP()` メソッドはイベントをプレーン HTTP 形式で {{site.data.keyword.iot_short_notm}} Quickstart サービスにパブリッシュします。登録されている有効な組織をプロパティー・ファイルに指定した場合は、イベントのパブリッシュに必ず HTTPS が使用されるため、すべての通信が保護されます。

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


## 例
{: #examples}


-  [MQTTApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java) - デバイス・イベントをパブリッシュする方法を示すサンプル・アプリケーション。
-   [RegisteredApplicationCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java) - コマンドをデバイスにパブリッシュする方法を示すサンプル・アプリケーション。
-  [RegisteredApplicationSubscribeSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java) - デバイス・イベント、デバイス・コマンド、デバイス状況、アプリケーション状況などのさまざまなイベントをサブスクライブする方法を示すサンプル・アプリケーション。
-   [SharedSubscriptionSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java) - 複数のアプリケーション・インスタンス間でメッセージのロード・バランシングを行うスケーラブルなアプリケーションを作成する方法を示すサンプル・アプリケーション。
-  [バックアップとリストアのサンプル](https://github.com/ibm-messaging/iot-backup-restore-sample) - Cloudant NoSQL データベースのデバイス構成をバックアップおよびリストアする方法を示すサンプル。
