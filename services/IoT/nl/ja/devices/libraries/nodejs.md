---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# デバイス開発者用の Node.js
{: #nodejs}

Node.js でクライアント・ライブラリーとサンプルを利用して、{{site.data.keyword.iot_full}} で組織と対話するデバイス・コードをビルド/開発することができます。
{:shortdesc}

提供されている情報と例を使用し、Node.js を使用したデバイスの開発を開始します。

## Node.js クライアントとリソースのダウンロード
{: #node.js_client_downloads}

{{site.data.keyword.iot_short_notm}} 用の Node.js クライアント・ライブラリーやその他の使用可能なリソースを利用するには、GitHub の [iot-nodejs ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-watson-iot/iot-nodejs){: new_window} リポジトリーにアクセスし、インストール手順を実行します。


詳しくは、以下のリソースを参照してください。

- Github の[デバイスのサンプル ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples){: new_window}
- NPM の [ibmiotf ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.npmjs.com/package/ibmiotf){: new_window} リポジトリー

## コンストラクター
{: #constructor}

コンストラクターはデバイス・クライアント・インスタンスを作成します。これは、以下の定義を格納する構成 JSON を受け入れます。

|定義 |説明 |
|:---|:---|
|`org` |組織 ID。|
|`type`  |デバイスのタイプ。通常、deviceType は、特定のタスクを実行するデバイスのグループです (例えば "weatherballoon")。|
|`id`  |デバイスの ID。通常、特定のデバイス・タイプにおいて、deviceId はそのデバイスの固有 ID です (シリアル番号や MAC アドレスなど)。|
|`auth-method`   |使用する認証の方式。現在サポートされている値は、`token` のみです。|
|`auth-token`   |デバイスを Watson IoT Platform に安全に接続するための認証トークン。このフィールドは、`auth-method` が `token` の場合に必要です。|

**注:** Quickstart サービスを使用する場合、最初の 3 つのプロパティーのみを送信する必要があります。

```
    var iotf = require("ibmiotf");
    var config = {
		"org" : "organization",
		"id" : "deviceId",
		"type" : "deviceType",
		"auth-method" : "token",
		"auth-token" : "authToken"
    };


    var deviceClient = new iotf.IotfDevice(config);
```

### 構成ファイルの使用

構成を直接渡す代わりに、以下の例に示すように、JSON 構成ファイルを使用して、必要な構成プロパティーを提供することができます。


```  
    var iotf = require("ibmiotf");
    var config = require("./device.json");
    var deviceClient = new iotf.IotfDevice(config);  
```
`device.json` 構成ファイルは、以下の形式でなければなりません。

```
	{
	  "org": "xxxxx",
	  "type": "raspi",
	  "id": "pi1",
	  "auth-method" : "token",
	  "auth-token" : "xxxxxxxxxxxxxxxx"
	}

```  

## {{site.data.keyword.iot_short_notm}} への接続
{: #connecting_to_iotp}

`connect` 関数を呼び出して、{{site.data.keyword.iot_short_notm}} に接続することができます。

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//setting the log level to debug. By default its 'warn'
	deviceClient.log.setLevel('debug');

	deviceClient.connect();

	deviceClient.on('connect', function(){
		var i=0;
		console.log("connected");
		setInterval(function function_name () {
			i++;
			deviceClient.publish('myevt', 'json', '{"value":'+i+'}', 2);
		},2000);
	});

```

{{site.data.keyword.iot_short_notm}} サービスへの接続に成功すると、デバイス・クライアントは `connect` イベントを送信します。このプロセスは、すべてのデバイス・ロジックをコールバック関数内に実装できることを意味しています。

デバイス・クライアントは、接続を失うと自動的に再接続を試みます。再接続が成功すると、クライアントは `reconnect` イベントを送信します。

## ロギング
{: #logging}

デフォルトでは、タイプが *warn* のログ・イベントのみが記録されます。ロギング・レベルを増やすか減らす場合は、log.setLevel 関数を使用します。以下のログ・レベルがサポートされています。
- trace
- debug
- info
- warn
- error

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//setting the log level to debug. By default its 'warn'
	deviceClient.log.setLevel('debug');

```


## イベントのパブリッシュ
{: #publishing_events}

イベントとは、デバイスが {{site.data.keyword.iot_short_notm}} にデータをパブリッシュするためのメカニズムのことです。デバイスはイベントの内容を制御し、送信するイベントごとに名前を割り当てます。

{{site.data.keyword.iot_short_notm}} インスタンスがイベントを受信すると、その受信イベントの資格情報によって、送信元デバイスが識別されます。そのためデバイスが、別のデバイスになりすますことはできません。

パブリッシュされるイベントのサービス品質 (QoS) レベルを引き上げることができます。QoS レベルが `0` より高いイベントは、追加の確認受信情報が含まれているため、パブリッシュにかかる時間が延びる可能性があります。

**注:** Quickstart フロー・モードは、QoS レベル `0` のみをサポートしています。


イベントは、以下のプロパティーでパブリッシュすることができます。

|プロパティー |説明|
|:---|:---|
|`eventType`  | パブリッシュされるイベントのタイプ (例えば、status または GPS)。 |  
|`eventFormat`  |イベントの形式 (例えば JSON)。 |
|`data`  | イベントのペイロード (これはバッファー・ストリングである必要があります)。 |
|`QoS`  | パブリッシュ・イベントの MQTT サービス品質。サポートされている値は 0、1、2 です。|


```
    var deviceClient = new Client.IotfDevice(config);

    deviceClient.connect();

    deviceClient.on("connect", function () {
       //publish an event at the default quality of service
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

       //publish an event at the user-defined quality of service
       var myQosLevel=2
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);
  });

```

## コマンドの処理
{: #handling_commands}

デバイス・クライアントは、接続時に、このデバイスに対するコマンドに自動的にサブスクライブします。特定のコマンドを処理するには、コマンド・コールバック関数を登録する必要があります。デバイス・クライアントは、コマンドを受け取るとコマンド・コールバック関数を呼び出します。コールバック関数には、以下のプロパティーがあります。

|プロパティー |説明|
|:---|:---|
|`commandName`  | 呼び出されたコマンドの名前を指定するストリング。 |  
|`format`  | イベントの形式を指定するストリング (例えば JSON)。 |
|`payload`  | コマンド・ペイロードのデータを指定するストリング。  |
|`topic`  | デバイスとしてパブリッシュする場合は、このトピック・ストリングにはデバイス・タイプもデバイス ID も含まれません。これらはクライアント ID から取得されます。例えば、`iot-2/evt/event_id/fmt/format_string` です。デバイスの代わりにアプリケーションまたはゲートウェイとしてパブリッシュする場合は、このトピックに、デバイス・タイプとデバイス ID を含める必要があります。例えば、`iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string` です。|


```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publish an event at the default quality of service
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("command", function (commandName,format,payload,topic) {
		if(commandName === "blink") {
			console.log(blink);
			//function to be performed for this command
			blink(payload);
		} else {
			console.log("Command not supported.. " + commandName);
		}
	});

```

## エラーの処理
{: #handling_errors}

デバイス・クライアントは、エラーを検出すると、*error* イベントを送信します。

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publish an event at the default quality of service
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("error", function (err) {
		console.log("Error : "+err);
	});
	....

```

## クライアントの切断
{: #disconnecting_client}

以下のサンプルは、クライアントを切断して接続を解放する方法を示しています。

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	client.on("connect", function () {
		//publish an event at the default quality of service
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

		//publishing event at the user-defined quality of service
		var myQosLevel=2
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);

		//disconnect the client
		client.disconnect();
	});

	....
```
