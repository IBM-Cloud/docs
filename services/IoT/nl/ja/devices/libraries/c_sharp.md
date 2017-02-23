---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-08-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# デバイス開発者のための C#
{: #c_sharp}

C# を使用して、{{site.data.keyword.iot_full}} 上で組織と対話するデバイスを構築してカスタマイズできます。C# を使用してデバイスの開発を始める場合は、提供されている情報と例を活用してください。
{:shortdesc}

## C# クライアントとリソースのダウンロード
{: #csharp_client_download}

{{site.data.keyword.iot_short_notm}} の C# クライアントおよびリソースを利用するには、GitHub の [iot-csharp](https://github.com/ibm-watson-iot/iot-csharp) リポジトリーにアクセスして、インストール手順を実行します。


## コンストラクター
{: #constructor}

コンストラクターはクライアント・インスタンスを作成し、以下の定義を格納する引数を受け入れます。

|定義 |説明 |
|:---|:---|
|`orgId`|組織 ID。|
|`deviceType`|デバイスのタイプ。|
|`deviceId` |デバイスの ID。|
|`auth-method`   |使用する認証の方式。現在サポートされている値は、`token` のみです。|
|`auth-token`   |デバイスを Watson IoT Platform に安全に接続するための認証トークン。|


指定した引数が `deviceId` と `deviceType` だけである場合、クライアントは未登録デバイスとして {{site.data.keyword.iot_short_notm}} Quickstart サービスに接続されます。クライアントがどのように {{site.data.keyword.iot_short_notm}} モジュールに接続されるかは、引数リストで定義されます。


```
namespace com.ibm.iotf.client

public DeviceClient(string orgId, string deviceType, string deviceID, string auth-method, string auth-token)
        : base(orgId, "d" + CLIENT_ID_DELIMITER + orgId + CLIENT_ID_DELIMITER + deviceType + CLIENT_ID_DELIMITER + deviceID, "use-token-auth", auth-token)
    {

    }
```

## イベントのパブリッシュ
{: #publishing-events}

デバイスは、イベントを使用して {{site.data.keyword.iot_short_notm}} インスタンスにデータをパブリッシュします。デバイスはイベントの内容を制御し、送信する各イベントに名前を割り当てます。

{{site.data.keyword.iot_short_notm}} インスタンスがイベントを受信すると、その着信イベントの資格情報によって、送信元デバイスが識別されます。そのためデバイスが、別のデバイスになりすますことはできません。

イベントは、MQTT プロトコルによって定義された 3 つの[サービス品質 (QoS) レベル](../mqtt.html#managed-devices)のいずれでもパブリッシュできます。デフォルトでは、イベントは QoS 0 でパブリッシュされます。


## デフォルトのサービス品質レベルを使用したイベントのパブリッシュ
{: #publish_event_default_qos}

```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}");
```


## ユーザー定義のサービス品質レベルを使用したイベントのパブリッシュ
{: #publish_event_user_qos}

`0` より大きい MQTT QoS レベルでパブリッシュされるイベントの場合は、受信確認情報が追加されるため、QoS レベルが `0` のイベントよりもパブリッシュに時間がかかる可能性があります。


```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}", 2);
```

## コマンドの処理
{: #handling_commands}

デバイス・クライアントは、接続時に、このデバイスに対するコマンドに自動的にサブスクライブします。特定のコマンドを処理するには、次の例に示すように、コマンド・コールバック・メソッドを登録する必要があります。

```
public static void processCommand(string cmdName, string cmdFormat, string cmdData) {
...
 }
```

```
deviceClient.connect();
deviceClient.commandCallback += processCommand;
```
次の表は、commandCallback メソッドのパラメーターを示しています。

|パラメーター|データ・タイプ|説明|
|:---|:---|
|`cmdName`|ストリング|コマンドを識別します。 |
|`cmdFormat`|ストリング|形式は任意のストリング (JSON など) となります。|
|`cmdData`|辞書|ペイロードのデータ。最大長は 131072 バイトです。|
