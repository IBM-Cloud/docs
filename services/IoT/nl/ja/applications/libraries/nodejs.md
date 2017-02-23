---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-07-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# アプリケーション開発者用の Node.js
{: #nodejs}

最終更新日: 2016 年 7 月 29 日
{: .last-updated}

Node.js のクライアント・ライブラリーとサンプルを調整して、{{site.data.keyword.iot_full}} の組織と対話するアプリケーションを作成し、カスタマイズできます。
{:shortdesc}

Node.js を使用したアプリケーションの開発を始められるように情報やサンプルが用意されているので活用してください。

## Node.js クライアントとリソースのダウンロード
{: #nodejs_client_download}

{{site.data.keyword.iot_short_notm}} 用の Node.js クライアント・ライブラリーやその他の使用可能なリソースを利用するには、GitHub の [iot-nodejs](https://github.com/ibm-watson-iot/iot-nodejs) リポジトリーにアクセスし、インストール手順を実行します。


詳しくは、以下のリソースを参照してください。
- GitHub の[アプリケーション・サンプル](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples)。
- NPM の [ibmiotf](https://www.npmjs.com/package/ibmiotf)。
- この資料の[リファレンス](#reference_nodejs)・セクション。


## コンストラクター
{: #constructor}

コンストラクターは、アプリケーション・クライアント・インスタンスを作成し、次のプロパティーを含む JSON 構成ファイルを受け入れます。

| プロパティー     |説明     |
|----------------|----------------|
|`org` |組織 ID。これは必須値です。|
|`id`  |組織内のアプリケーションの固有 ID。|
|`auth-key`   |アプリケーションを Watson IoT Platform に安全に接続するための API キー。|
|`auth-token`   |デバイスを Watson IoT Platform に安全に接続するための API キー・トークン。|
|`type`  |サブスクリプションのタイプ。共有サブスクリプションを有効にするには、`shared` を指定します。|


Quickstart を使用する場合は、最初の 2 つのプロパティーのみが必須です。

```
  var Client = require("ibmiotf");
	var appClientConfig = {
		"org" : orgId,
		"id" : appId,
		"auth-key" : apiKey,
		"auth-token" : apiToken
	}

	var appClient = new Client.IotfApplication(appClientConfig);
```


### 構成ファイルの使用


JSON プロパティーを直接渡す代わりに、次のコード・サンプルに大まかに示すように、構成ファイルを使用することもできます。

```

  var Client = require("ibmiotf");
	var appClientConfig = require("./application.json");
	var appClient = new Client.IotfApplication(appClientConfig);
```

この JSON 構成ファイルは次のフォーマットにしてください。

```
    {
	  "org": 'xxxxx',
	  "id": 'myapp',
	  "auth-key": 'a-xxxxxxx-zenkqyfiea',
	  "auth-token": 'xxxxxxxxxx'
    }
```


## {{site.data.keyword.iot_short_notm}} への接続
{: #connecting_to_iotp}

{{site.data.keyword.iot_short_notm}} に接続するには、次のように *connect* 要求を送信します。

```
  var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

	//Add your code here
	});
```

{{site.data.keyword.iot_short_notm}} サービスに正常に接続すると、アプリケーション・クライアントは `connect` イベントを送信するので、このコールバック関数の内部に任意のロジックを実装できます。



アプリケーション・クライアントは、接続が失われると自動的に再接続を試行します。再接続が成功すると、クライアントは `reconnect` イベントを送信します。



## ロギング
{: #logging}

デフォルトでは、タイプが `warn` のログ・イベントのみが記録されます。ロギング・レベルを増やすか減らす場合は、`log.setLevel` 関数を使用します。以下のログ・レベルがサポートされています。
- trace
- debug
- info
- warn
- error

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
```

## 共有サブスクリプション
{: #shared_subscriptions}

共有サブスクリプション機能を使用して、複数のアプリケーション・インスタンス間でメッセージのロード・バランシングを行うスケーラブルなアプリケーションを作成できます。ロード・バランシングを有効にするには、次の例に示すように、`type` フィールドに `shared` を設定します。

```

	var appClientConfig = {
	  org: 'xxxxx',
	  id: 'myapp',
	  "auth-key": 'a-xxxxxx-xxxxxxxxx',
	  "auth-token": 'xxxxx!xxxxxxxx',
	  "type" : "shared" // make this connection as shared subscription
	};
	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
```

## エラーの処理
{: #handling_errors}

アプリケーション・クライアントでエラーが発生すると、`error` イベントが生成されます。

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
	appClient.on("error", function (err) {
		console.log("Error : "+err);
	});
```

## デバイス・イベントのサブスクライブ
{: #subscribing_device_events}

イベントとは、デバイスが {{site.data.keyword.iot_short_notm}} インスタンスにデータをパブリッシュするためのメカニズムのことです。デバイスはイベントの内容を制御し、送信するイベントごとに名前を割り当てます。

{{site.data.keyword.iot_short_notm}} インスタンスがイベントを受信すると、その受信イベントの資格情報によって、送信元デバイスが識別されます。そのためデバイスが、別のデバイスになりすますことはできません。


デフォルトでは、アプリケーションは、すべての接続デバイスのすべてのイベントをサブスクライブします。デバイス・タイプ、デバイス ID、イベント、メッセージ・フォーマットの各パラメーターを使用して、サブスクリプションの範囲を制御できます。次のコード・サンプルは、これらのパラメーターを使用してサブスクリプションの範囲を定義する方法を示しています。

### すべてのデバイスのすべてのイベントをサブスクライブする


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents();
	});
```

### 特定のタイプに属するすべてのデバイスのすべてのイベントをサブスクライブする

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("mydeviceType");
	});
```

### すべてのデバイスの特定のイベントをサブスクライブする


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("+","+","myevent");
	});
```

### 複数の異なるデバイスの特定のイベントをサブスクライブする

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","myevent");
		appClient.subscribeToDeviceEvents("myOtherDeviceType","device02","myevent");
	});
```

### JSON フォーマットでパブリッシュされたすべてのイベントをサブスクライブする


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
```

**注**: 単一のクライアントで複数のサブスクリプションをサポートできます。

### デバイスからのイベントの処理


サブスクリプションで受信したイベントを処理するには、デバイス・イベント・コールバック・メソッドを実装します。{{site.data.keyword.iot_short_notm}} アプリケーション・クライアントは、イベント `deviceEvent` を送信します。この関数のプロパティーは、以下のとおりです。

- deviceType
- deviceId
- eventType
- format
- payload
- topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
	appClient.on("deviceEvent", function (deviceType, deviceId, eventType, format, payload) {

		console.log("Device Event from :: "+deviceType+" : "+deviceId+" of event "+eventType+" with payload : "+payload);

	});
```


## デバイス状況のサブスクライブ
{: #subscribing_device_status}

デフォルトでは、デバイス状況をサブスクライブすると、すべての接続デバイスの状況更新を受信します。タイプと ID のパラメーターを使用して、サブスクリプションの範囲を制御できます。単一のクライアントで複数のサブスクリプションをサポートできます。

### すべてのデバイスの状況更新をサブスクライブする

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus();

	});
```

### 特定のタイプのすべてのデバイスの状況更新をサブスクライブする


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType");

	});
```

### 2 つの異なるデバイスの状況更新をサブスクライブする

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
```

### デバイスからの状況更新の処理

サブスクリプションで受信した状況更新を処理するには、デバイス状況コールバック・メソッドを実装します。{{site.data.keyword.iot_short_notm}} アプリケーション・クライアントは、イベント `deviceStatus` を送信します。この関数のプロパティーは、以下のとおりです。

-   deviceType
-   deviceId
-   payload
-   topic

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
	appClient.on("deviceStatus", function (deviceType, deviceId, payload, topic) {

		console.log("Device status from :: "+deviceType+" : "+deviceId+" with payload : "+payload);

	});
```


## デバイスからのイベントのパブリッシュ
{: #publishing_device_events}


アプリケーションは、デバイスからパブリッシュされたかのようにイベントをパブリッシュすることができます。この関数には、以下のプロパティーが必要です。

-   deviceType
-   deviceId
-   eventType
-   format
-   data


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50};
		myData = JSON.stringify(myData);
		appClient.publishDeviceEvent("myDeviceType","device01", "myEvent", "json", myData);

	});
```


## デバイスへのコマンドのパブリッシュ
{: #publishing_commands_devices}

アプリケーションは、接続デバイスにコマンドをパブリッシュできます。この関数には、以下のプロパティーが必要です。

-   deviceType
-   deviceId
-   eventType
-   format
-   data

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10};
		myData = JSON.stringify(myData);
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

	});
```


## クライアントの切断
{: #disconnect_client}

以下のサンプルは、クライアントを切断し、さらに接続を解放します。

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10}
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

		appClient.disconnect();
	});
```


## リファレンス
{: #reference_nodejs}

次の表に、この Node.js 資料に記載されている関数で使用するパラメーターについて説明します。

|パラメーター|データ・タイプ|説明|
|:---|:---|
|`deviceType`|ストリング|デバイス・タイプ。通常、deviceType は、特定のタスクを実行するデバイスのグループです (例えば "weatherballoon")。|
|`deviceId`|ストリング|デバイスの ID。通常、特定のデバイス・タイプにおいて、deviceId はそのデバイスの固有 ID です (シリアル番号や MAC アドレスなど)。|
|`eventType`|ストリング|特定のイベントのグループ (「status」、「warning」、「data」など)。|
|`format`|ストリング|形式は任意のストリング (JSON など) となります。  |
|`data`|辞書|メッセージ・ペイロードのデータ。最大長は 131072 バイトです。|
|`payload`|ストリング|メッセージ・ペイロードのデータ。最大長は 131072 バイトです。|
|`topic`|ストリング|デバイスとしてパブリッシュする場合は、このトピック・ストリングにはデバイス・タイプもデバイス ID も含まれません。これらはクライアント ID から取得されます。例えば、`iot-2/evt/event_id/fmt/format_string` です。デバイスの代わりにアプリケーションまたはゲートウェイとしてパブリッシュする場合は、このトピックに、デバイス・タイプとデバイス ID を含める必要があります。例えば、`iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string` です。|
