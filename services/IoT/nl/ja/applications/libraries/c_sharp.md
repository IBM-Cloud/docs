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


# アプリケーション開発者用の C# 
{: #c_sharp}


C# を使用して、{{site.data.keyword.iot_full}} の組織と対話するアプリケーションを作成し、カスタマイズできます。C# を使用したアプリケーションの開発を始められるように情報やサンプルが用意されているので活用してください。
{:shortdesc}

## C# クライアントとリソースのダウンロード
{: #csharp_client_download}

{{site.data.keyword.iot_short_notm}} 用の C# クライアント・ライブラリーとサンプルを利用するには、GitHub の [iot-csharp ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://github.com/ibm-watson-iot/iot-csharp){: new_window} リポジトリーにアクセスし、インストール手順を実行します。


## コンストラクター
{: #constructor}

コンストラクターはクライアント・インスタンスを作成し、以下の定義を格納する引数を受け入れます。

|定義 |説明 |
|:---|:---|
|`orgId`   |組織 ID。|
|`appId`   |組織内のアプリケーション固有の ID。|
|`auth-key`   |アプリケーションを Watson IoT Platform に安全に接続するための API キー。|
|`auth-token`   |アプリケーションを Watson IoT Platform に安全に接続するための API キー・トークン。|

指定した引数が `appId` だけである場合、クライアントは未登録デバイスとして {{site.data.keyword.iot_short_notm}} Quickstart サービスに接続されます。クライアントがどのように {{site.data.keyword.iot_short_notm}} モジュールに接続されるかは、引数リストで定義されます。

```
ApplicationClient applicationClient = new ApplicationClient(orgId, appId, apiKey, authToken);  
applicationClient.connect();
```


## デバイス・イベントのサブスクライブ
{: #subscribe_device_events}

デバイスは、イベントを使用して {{site.data.keyword.iot_short_notm}} インスタンスにデータをパブリッシュします。デバイスはイベントの内容を制御し、送信する各イベントに名前を割り当てます。

{{site.data.keyword.iot_short_notm}} インスタンスがイベントを受信すると、その受信イベントの資格情報によって、送信元デバイスが識別されます。そのためデバイスが、別のデバイスになりすますことはできません。

デフォルトでは、アプリケーションは、すべての接続デバイスのすべてのイベントをサブスクライブします。デバイス・タイプ、デバイス ID、イベント、メッセージ・フォーマットの各パラメーターを使用して、サブスクリプションの範囲を制御できます。次のコード・サンプルは、これらのパラメーターを使用してサブスクリプションの範囲を定義する方法を示しています。

### すべてのデバイスのすべてのイベントをサブスクライブする

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents();
```

### 特定のタイプに属するすべてのデバイスのすべてのイベントをサブスクライブする

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType);
```

### すべてのデバイスの特定のイベントをサブスクライブする

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(evt);
```

###  複数の異なるデバイスの特定のイベントをサブスクライブする

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt);
```

### JSON フォーマットでパブリッシュされたすべてのイベントをサブスクライブする

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt, "json", 0);
```

**注**: 単一のクライアント・インスタンスで複数のサブスクリプションをサポートできます。

### デバイスからのイベントの処理

サブスクリプションで受信したイベントを処理するには、次の例に示すように、イベント・コールバック・メソッドを登録します。

```
public static void processEvent(String eventName, string eventFormat, string eventData) {
// Do something
}
applicationClient.connect();
applicationClient.eventCallback += processEvent;
applicationClient.subscribeToDeviceEvents();
```
イベント・コールバック・メソッドのパラメーターについて次の表で説明します。

|パラメーター|データ・タイプ|説明|
|:---|:---|
|`eventName`|ストリング|イベントを識別します。 |
|`eventFormat`|ストリング| 形式は任意のストリング (JSON など) となります。|
|`eventData`|辞書| メッセージ・ペイロードのデータ。最大長は 131072 バイトです。|


## デバイス状況のサブスクライブ
{: #subscribe_device_status}

デフォルトでは、サブスクリプションは、すべての接続デバイスの状況更新を受信するように設定されます。デバイス・タイプとデバイス ID のパラメーターを使用して、サブスクリプションの範囲を制御できます。次のコード・サンプルは、これらのパラメーターを使用してサブスクリプションの範囲を定義する方法を示しています。

### すべてのデバイスの状況更新をサブスクライブする

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus();
```

### 2 つの異なるデバイスの状況更新をサブスクライブする

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus(deviceType, deviceId);
```

**注**: 単一のクライアント・インスタンスで複数のサブスクリプションをサポートできます。

### デバイスからの状況更新の処理

サブスクリプションで受信した状況更新を処理するには、次の例に示すように、イベント・コールバック・メソッドを登録します。

```
public static void processDeviceStatus(String deviceType, string deviceId, string data)
        {
           //
        }
applicationClient.connect();
applicationClient.appStatusCallback += processAppStatus;
applicationClient.subscribeToApplicationStatus();
```

## デバイスからのイベントのパブリッシュ
{: #publish_events_devices}

アプリケーションは、デバイスからパブリッシュされたかのようにイベントをパブリッシュすることができます。

```
applicationClient.connect();
applicationClient.publishEvent(deviceType, deviceId, evt, data, 0);

```

`publishEvent()` メソッドで指定するパラメーターについて次の表で説明します。

|パラメーター|データ・タイプ|説明|
|:---|:---|
|`deviceType`|ストリング| デバイス・タイプ。通常、deviceType は、特定のタスクを実行するデバイスのグループです (例えば "weatherballoon")。|
|`deviceId`|ストリング| デバイスの ID。通常、特定のデバイス・タイプにおいて、deviceId はそのデバイスの固有 ID です (シリアル番号や MAC アドレスなど)。|
|`evt`|ストリング| イベントの名前。|
|`format`|ストリング| 形式は任意のストリング (JSON など) となります。|
|`data`|辞書| メッセージ・ペイロードのデータ。最大長は 131072 バイトです。|
|`QoS`|整数| サービス品質。有効な値は `0`、`1`、`2` です。 |


## デバイスへのコマンドのパブリッシュ
{: #publish_commands_devices}

アプリケーションは、接続デバイスにコマンドをパブリッシュできます。

```
applicationClient.connect();
applicationClient.publishCommand(deviceType, deviceId, "testcmd", "json", data, 0);
```
`publishCommand()` メソッドで指定するパラメーターについて次の表で説明します。

|パラメーター|データ・タイプ|説明|
|:---|:---|
|`deviceType`|ストリング| デバイス・タイプ。通常、deviceType は、特定のタスクを実行するデバイスのグループです (例えば "weatherballoon")。|
|`deviceId`|ストリング| デバイスの ID。通常、特定のデバイス・タイプにおいて、deviceId はそのデバイスの固有 ID です (シリアル番号や MAC アドレスなど)。|
|`command`|ストリング| コマンドの名前。|
|`format`|ストリング| 形式は任意のストリング (JSON など) となります。|
|`data`|辞書| メッセージ・ペイロードのデータ。最大長は 131072 バイトです。|
|`QoS`|整数| サービス品質。有効な値は `0`、`1`、`2` です。 |
