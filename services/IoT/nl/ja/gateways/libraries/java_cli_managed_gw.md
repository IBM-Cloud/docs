---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-12-06"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java を使用した管理対象ゲートウェイの開発
{: #java_cli_managed_gw}

ゲートウェイは、それらに接続されているデバイスを管理する上で重要な役割を果たします。デバイスの多くはたいへん基本的なものであり、デバイス管理機能を備えていません。そのため、それらの基本的なデバイスはゲートウェイから管理する必要があります。{{site.data.keyword.iot_full}} で、管理対象ゲートウェイは、接続されているデバイスを管理することができ、ファームウェア、ロケーション、診断の更新などのデバイス管理機能を提供できるゲートウェイです。
{:shortdesc}

{{site.data.keyword.iot_short}} Java™ クライアント・ライブラリーと提供されている情報を使用することによって、ゲートウェイを管理対象ゲートウェイに変換する Java コードを開発できます。ゲートウェイをデバイス管理サービスに接続してデバイス管理操作を実行するための Java コードの開発に役立つサンプルも提供されています。

## デバイス管理サービス
{: #dm_service}

{{site.data.keyword.iot_short}} デバイス管理 (DM) サービスは、接続されているデバイスを管理するためのデバイス管理機能をゲートウェイに提供します。

管理対象ゲートウェイが実行するデバイス管理エージェントは、そのゲートウェイを介して {{site.data.keyword.iot_short}} に接続されているすべてのデバイスのプロキシーの役目をします。

### デバイス管理エージェント

ゲートウェイを介して間接的に {{site.data.keyword.iot_short}} に接続されるデバイスは、ゲートウェイ・デバイスによってサポートされているさまざまな接続プロトコルを使用できます。

`ManagedGateway` インスタンスは、デバイス管理アクティビティーへの参加、エラー・コード、ログ、ロケーション、ファームウェアの更新、デバイス・アクションなど、1 つ以上のデバイス管理アクションを実行するためのメソッドのリストを提供するデバイス管理エージェントです。

ゲートウェイ上のデバイス管理エージェントは、接続されているデバイスの接続プロトコルを変換して処理することにより、{{site.data.keyword.iot_short}} がそのデバイスを管理できるようにします。デバイス管理エージェントにより、ゲートウェイは、接続されたデバイスと {{site.data.keyword.iot_short}} の間の見えないトンネル以上の機能を果たすことができます。例えば、ゲートウェイに接続されたデバイスがファームウェアをダウンロードできない場合、ゲートウェイ上のデバイス管理エージェントが以下のアクションを実行できます。
- ファームウェアをダウンロードするデバイスの要求を代行受信する
- デバイスのファームウェアをダウンロードする
- ゲートウェイにデバイス・ファームウェアを保管する

後に、デバイスでアップグレードの指示が出たら、ゲートウェイ上のデバイス管理エージェントがファームウェアをデバイスにプッシュして更新を実行できます。

## デバイス・モデルの作成
{: #create_device_model}

{{site.data.keyword.iot_short}} で、デバイス・モデルとは、デバイスとゲートウェイのメタデータと管理特性を記述したものです。デバイス・データベースは、デバイスやゲートウェイの情報のマスター・ソースです。アプリケーションや管理対象デバイスは、ロケーションの更新、ファームウェア・アップグレード・プロセスの更新、その他のタイプの更新を送信することができます。{{site.data.keyword.iot_short}} が更新を受け取ると、デバイス・データベースが更新されて、接続するアプリケーションでその情報が使用できるようになります。

{{site.data.keyword.iot_short}} Java クライアント・ライブラリーで、デバイス・モデルは `DeviceData` Java クラスによって表されます。

`DeviceData` クラスを作成するには、以下のオブジェクトを作成します。

- `DeviceInfo` (オプション)
- `DeviceLocation` (オプション。{{site.data.keyword.iot_short}} API を使用してアプリケーションが設定したロケーションについてデバイスに通知する場合にのみ必須です)
- `DeviceFirmware` (オプション)
- `DeviceMetadata` (オプション)

詳しくは、[デバイス・モデル](../../reference/device_model.html)を参照してください。

### DeviceInfo

サンプル・データを含む以下のコード・スニペットは、`DeviceInfo` オブジェクトと `DeviceMetadata` オブジェクトの作成方法を示しています。

```java
DeviceInfo deviceInfo = new DeviceInfo.Builder().
                           serialNumber("10087").
           manufacturer("IBM").
           model("7865").
           deviceClass("A").
           description("My RasPi Device").
           fwVersion("1.0.0").
           hwVersion("1.0").
           descriptiveLocation("EGL C").
           build();

/**
  * Create a DeviceMetadata object
 **/
JsonObject data = new JsonObject();
data.addProperty("customField", "customValue");
DeviceMetadata metadata = new DeviceMetadata(data);
```

以下のコード・スニペットは、直前のサンプルで作成された `DeviceInfo` オブジェクトと `DeviceMetadata` オブジェクトを使用して `DeviceData` クラスを作成する方法の概要を示しています。

```java
DeviceData deviceData = new DeviceData.Builder().
                         deviceInfo(deviceInfo).
             metadata(metadata).
             build();
```

すべてのゲートウェイおよび接続されたすべてのデバイスにはそれぞれ、{{site.data.keyword.iot_short}} の中でそのものを表す独自の `DeviceData` クラス定義が必要です。ゲートウェイの場合、`DeviceData` クラスは、`ManagedGateway` インスタンスの構成処理の一部としてライブラリーに渡されます。接続されたデバイスの場合、`DeviceData` クラスは、`sendDeviceManageRequest()` オブジェクトの一部としてライブラリーに渡されます。

## ManagedGateway コンストラクター
{: #construct_managed_gateway}

`ManagedGateway` は、ゲートウェイを、それ自体のためまたは接続されたデバイスのために 1 つ以上のデバイス管理操作を実行できる管理対象ゲートウェイとして {{site.data.keyword.iot_short}} に接続する Java クラスです。`ManagedGateway` インスタンスは、ゲートウェイ・イベントのパブリッシュ、デバイス・イベントの接続、アプリケーションからのコマンドの listen などといった通常のゲートウェイ操作を行うためにも使用できます。`ManagedGateway` インスタンスは、デバイス管理エージェントです。

`ManagedGateway` クラスでは、コンストラクター 1 とコンストラクター 2 という 2 つの異なるコンストラクターが、異なるユーザー・パターンをサポートしています。

### コンストラクター 1

コンストラクター 1 は、以下のすべてのプロパティーを含む `DeviceData` クラスを受け入れて、`ManagedGateway` インスタンスを構成します。

| プロパティー     |説明     |
|----------------|----------------|
|`Organization-ID` |組織 ID。|
|`Gateway-Type` |ゲートウェイ・デバイスのタイプ。|
|`Gateway-ID` |ゲートウェイ・デバイスの ID。|
|`Authentication-Method`|認証の方式。サポートされている唯一の方式は "token" です。|
|`Authentication-Token`|API 鍵トークン。|
|`auth-key`   |オプションの API キー。auth-method の値を `apikey` に設定する場合は、これを指定する必要があります。|
|`auth-token`   |API キー・トークン。auth-method の値を `apikey` に設定する場合は、これも指定する必要があります。 |
|`clean-session`|true または false 値。永続サブスクリプション・モードでゲートウェイを接続する場合のみ必要です。デフォルトでは、`clean-session` は `true` に設定されます。|
|`Port`|接続先のポート番号。8883 か 443 のいずれかを指定してください。ポート番号を指定しない場合、クライアントは、デフォルトのポート番号 8883 で {{site.data.keyword.iot_short_notm}} に接続します。|
|`WebSocket`|true または false 値。Web ソケットを使用してゲートウェイを接続する場合のみ必要です。|
|`MaxInflightMessages`  |接続の処理中メッセージの最大数を設定します。デフォルト値は 100 です。|
|`Automatic-Reconnect`  |true か false の値。切断状態になったデバイスを自動的に {{site.data.keyword.iot_short_notm}} に再接続する場合は、これを指定する必要があります。デフォルト値は false です。|
|`Disconnected-Buffer-Size`|クライアントの切断中にメモリー内に保管できるメッセージの最大数。デフォルト値は 5000 です。|

**注:** 永続サブスクリプション・モードでゲートウェイを接続するには、`clean-session` を `false` に設定します。`clean-session` プロパティーについて詳しくは、[MQTT 資料](../../reference/mqtt/index.html#subscription-buffers-and-clean-session)の『サブスクリプション・バッファーとクリーン・セッション』のセクションを参照してください。

以下のコードは、`ManagedGateway` インスタンスの作成方法を示しています。

```java
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Gateway-Type", "iotsample-arduino");
options.setProperty("Gateway-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
```

### コンストラクター 2

コンストラクター 2 は、`DeviceData` オブジェクトと MQTT クライアント・インスタンスを受け入れて、`ManagedGateway` インスタンスを構成します。コンストラクター 2 の場合は、インスタンス内の `DeviceData` オブジェクトにデバイス・タイプとデバイス ID が含まれている必要もあります。以下のコード・サンプルに示すとおりです。

```java
// Code that constructs either a synchronous or asynchronous MQTT client instance of mqttClient.
.....

// Code that constructs the DeviceData object
DeviceData deviceData = new DeviceData.Builder().
                         typeId("Gateway-Type").
                         deviceId("Gateway-ID").
                         deviceInfo(deviceInfo).
             metadata(metadata).
             build();

....
ManagedGateway ManagedGateway = new ManagedGateway(mqttClient, deviceData);

```

**注:** カスタム・デバイス用に開発している場合は、コンストラクター 2 を使用してください。このコンストラクターは、デバイス管理操作を活用できるように、既存の接続済み MQTT クライアント・インスタンスを使用して管理対象ゲートウェイ・インスタンスを作成するためです。すべてのデバイス機能に関して、Java クライアント・ライブラリーを使用します。

## ゲートウェイからのデバイス管理要求
{: #dm_requests}

### ゲートウェイからの管理要求の送信

デバイス管理アクティビティーに参加するようにゲートウェイに指示するためには、`sendGatewayManageRequest()` メソッドを呼び出します。以下のコード・サンプルはその方法を示しています。

```java
managedGateway.sendGatewayManageRequest(0, true, true);
```
デバイスがまだ {{site.data.keyword.iot_short}} に接続されていない場合は、管理要求が出されると、接続要求が内部的に開始します。
`sendGatewayManageRequest()` メソッドは以下のパラメーターを受け入れます。

| パラメーター     |説明     |
|----------------|----------------|
|`lifetime`|ゲートウェイが次の「デバイスを管理」要求を送信しなければならない制限時間 (秒数) です。これを過ぎると、デバイスは休止として分類されて非管理対象デバイスになります。`lifetime` フィールドが省略された場合、または 0 に設定された場合、管理対象ゲートウェイは休止になりません。`lifetime` フィールドのサポートされる最小の設定値は 3600 秒 (1 時間) です。|
|`supportFirmwareActions`|ゲートウェイがファームウェア・アクションをサポートするかどうかを決定する true または false の値です。ファームウェアの要求を処理するために、ゲートウェイはファームウェア・ハンドラーも追加する必要があります。|
|`supportDeviceActions`|ゲートウェイがデバイス・アクションをサポートするかどうかを決定する true または false の値です。リブートとファクトリー・リセット要求を処理するために、ゲートウェイはデバイス・アクション・ハンドラーも追加する必要があります。|


`ManagedGateway` インスタンスは、デバイス管理アクティビティーへの参加、エラー・コード、ログ、ロケーション、ファームウェアの更新、デバイス・アクションなど、1 つ以上のデバイス管理アクションを実行するためのメソッドのリストを提供するデバイス管理エージェントです。

### 接続されたデバイスからの管理要求の送信

ゲートウェイの背後に接続されたデバイスがゲートウェイ上のデバイス管理アクティビティーに参加できるようにするには、`sendDeviceManageRequest()` メソッドを呼び出します。

`sendDeviceManageRequest()` メソッドは、接続されたデバイスの詳細情報と、`lifetime`、`supportFirmwareActions`、`supportDeviceActions` の各パラメーターを受け入れます。ゲートウェイは、多重定義の `sendDeviceManageRequest()` メソッドを使用して、接続されたデバイスの `DeviceData` オブジェクトを定義することもできます。

#### 接続されたデバイスからの管理要求の送信例

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, lifetime, true, true);
```

### ゲートウェイからの管理解除要求の送信

ゲートウェイを管理する必要がなくなったときは、ゲートウェイ上のデバイス管理アクティビティーを停止するために、`sendGatewayUnmanageRequet()` メソッドを呼び出します。`sendGatewayUnmanageRequet()` が呼び出されると、{{site.data.keyword.iot_short}} はそのゲートウェイに対するデバイス管理要求をそれ以上は新しく送信しなくなり、ゲートウェイからのデバイス管理要求は **Manage** 要求を除いてすべて拒否されます。ゲートウェイの背後にあるデバイスからの要求は拒否されません。

#### ゲートウェイからの管理解除要求の送信例

```java
managedGateway.sendGatewayUnmanageRequet();
```

### 接続されたデバイスからの管理解除要求の送信

ゲートウェイの背後にあるデバイスを管理する必要がなくなったとき、接続されたデバイスを管理対象状態から非管理対象状態に移行させるために、ゲートウェイから `sendDeviceUnmanageRequet()` メソッドを呼び出すことができます。`sendDeviceUnmanageRequet()` が呼び出されると、{{site.data.keyword.iot_short}} はデバイスに対するデバイス管理要求をそれ以上は新しく送信しなくなり、**Manage** 要求を除く、接続されたデバイスのためのゲートウェイからのデバイス管理要求はすべて拒否されます。

#### 接続されたデバイスからの管理解除要求の送信例

```java
managedGateway.sendDeviceUnmanageRequet();
```

## 位置の更新
{: #location_updates}

### ゲートウェイ・ロケーションの更新情報の送信

ゲートウェイ位置を判別できるゲートウェイは、ロケーションの変更を {{site.data.keyword.iot_short}} に通知することができます。ゲートウェイは、多重定義されたいずれかの `updateLocation()` メソッドを呼び出して、デバイスのロケーションを更新することができます。

```java
    // update the location with latitude, longitude, and elevation.
int rc = managedGateway.updateGatewayLocation(30.28565, -97.73921, 10);
if(rc == 200) {
    System.out.println("Location updated successfully!");
} else {
System.err.println("Failed to update the location!");
    }
```

### 接続されたデバイスのロケーションの更新情報の送信

ゲートウェイは、対応する `updateDeviceLocation()` デバイス・メソッドを呼び出して、接続されているデバイスのロケーションを更新できます。多重定義されたメソッドを使用して、`measuredDateTime` メソッドを指定できます。  

```java
// update the location of the attached device with latitude, longitude, and elevation
int rc = managedGateway.updateDeviceLocation(typeId, deviceId, 30.28565, -97.73921, 10);
```
ロケーションの更新について詳しくは、[デバイス管理要求](../../devices/device_mgmt/index.html#/update-location#update-location)を参照してください。## エラー・コードの処理
{: #errors}

### ゲートウェイ・エラー・コードの作成と削除

ゲートウェイは、{{site.data.keyword.iot_short}} にエラー状況の変更を通知することができます。ゲートウェイは `addErrorCode()` メソッドを呼び出して、現在のエラー・コードを {{site.data.keyword.iot_short}} に追加できます。

```java
int rc = managedGateway.addGatewayErrorCode(300);
```

以下に示すように、ゲートウェイのエラー・コードは `clearErrorCodes()` メソッドを呼び出すことで {{site.data.keyword.iot_short}} から消去できます。

```java
int rc = managedGateway.clearGatewayErrorCodes();
```

### 接続されたデバイスのエラー・コードの作成と削除

ゲートウェイは対応するデバイス・メソッドを呼び出して、接続されたデバイスのエラー・コードを追加したり消去したりすることができます。

```java
int rc = managedGateway.addDeviceErrorCode(typeId, deviceId, 300);
rc = managedGateway.clearDeviceErrorCodes(typeId, deviceId);
```

### ゲートウェイ・ログ・メッセージの作成と削除

ゲートウェイは、新しいログ・エントリーを追加することによって、{{site.data.keyword.iot_short}} に変更を通知することができます。ログ・エントリーには以下の項目が含まれます。

- メッセージ・ストリング
- タイム・スタンプ
- 重大度
- オプションで、Base64 エンコード・バイナリー診断データ

ゲートウェイは `addGatewayLog()` メソッドを呼び出して、ログ・メッセージを送信できます。以下のサンプルはその方法を示しています。

```java
// An example Log event
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addGatewayLog(message, timestamp, severity);
```

ログ・メッセージは、`clearLogs()` メソッドを呼び出すことによって、{{site.data.keyword.iot_short}} から消去できます。

```java
rc = managedGateway.clearGatewayLogs();
```

### 接続されたデバイスのログの作成と削除

同様に、ゲートウェイは対応するデバイス・メソッドを呼び出して、接続されたデバイスのログを作成したり消去したりすることができます。以下のコード・サンプルにはその方法を示しています。

```java

// An example log event:
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addDeviceLog(typeId, deviceId, message, timestamp, severity);
```

接続されたデバイスのログを消去するには、接続されたデバイスの詳細を指定して `clearDeviceLogs()` メソッドを呼び出します。以下のコード・サンプルはその方法を示しています。

```java
int rc = managedGateway.clearDeviceLogs(typeId, deviceId);
```

ゲートウェイまたはデバイス診断操作の目的は、ゲートウェイやデバイスのエラー情報を提供することです。{{site.data.keyword.iot_short}} へのデバイスの接続に関連した診断情報は提供されません。

診断操作について詳しくは、[デバイス管理要求](../../devices/device_mgmt/index.html#/update-location#update-location)を参照してください。

## ファームウェアの更新と操作
{: #firmware}

ファームウェア更新プロセスは、2 つの別個のアクションに分かれています。

- ファームウェアのダウンロード
- ファームウェアの更新

ゲートウェイは、ゲートウェイそれ自体とゲートウェイに接続されているデバイスの両方のファームウェア・アクションをサポートするために、次のアクティビティーを行う必要があります。

1. オプション: `DeviceFirmware` オブジェクトの構成。
2. サーバーへのファームウェア・アクション・サポートについての情報の通知。
3. ファームウェア・アクション・ハンドラーの作成。
4. `ManagedGateway` へのハンドラーの追加。

### ステップ 1: `DeviceFirmware` オブジェクトの構成

ゲートウェイはファームウェア・アクションを行うため、オプションでゲートウェイそれ自体とゲートウェイに接続されたデバイスのために `DeviceFirmware` オブジェクトを構成し、それを `DeviceData` オブジェクトに追加することができます。以下のサンプルはその方法を示しています。

```java
DeviceFirmware firmware = new DeviceFirmware.Builder().
			version("Firmware.version").
            name("Firmware.name").
            url("Firmware.url").
            verifier("Firmware.verifier").
            state(FirmwareState.IDLE).
            build();

  DeviceData deviceData = new DeviceData.Builder().
               deviceInfo(deviceInfo).
             deviceFirmware(firmware).
            metadata(metadata).
            build();

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
managedGateway.connect();
```

接続されたデバイスのためには、管理要求を送信する際に、構成した `DeviceData` オブジェクトをライブラリーに渡すことができます。以下のコード・サンプルはその方法を示しています。

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, lifetime, supportFirmwareActions, supportDeviceActions);
```

`DeviceFirmware` オブジェクトは、ゲートウェイまたは接続されたデバイスの現在のファームウェアを表し、ファームウェア・ダウンロード・アクションとファームウェア更新アクションの状況を {{site.data.keyword.iot_short}} に報告するために使用されます。この `DeviceFirmware` オブジェクトがゲートウェイによって構成されていない場合、ライブラリーは空のオブジェクトを作成して、その状況を {{site.data.keyword.iot_short}} に報告します。

### ステップ 2: サーバーへのファームウェア・アクション・サポートについての情報の通知

サーバーがファームウェア要求を開始するには、ゲートウェイやゲートウェイに接続されているデバイスで、ファームウェア・アクション・フラグを true に設定する必要があります。この変更は、管理要求で `supportFirmwareActions` パラメーターに true の値を渡すことによって行うことができます。

ゲートウェイは、以下のメソッドを呼び出して、ファームウェア・サポートについての情報をサーバーに通知できます。
```java
managedGateway.sendGatewayManageRequest(3600, true, false);
```

同様に、ゲートウェイは対応するデバイス・メソッドを呼び出して、接続されているデバイスのファームウェア・サポート情報を通知できます。

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, 3600, true, false);
```

サポート情報がデバイス管理サーバーに通知されると、サーバーは、ゲートウェイ自体のためまたはその背後にあるデバイスのためのファームウェア・アクションをゲートウェイに転送します。

### ステップ 3: ファームウェア・アクション・ハンドラーの作成

ファームウェア・アクションをサポートするために、ゲートウェイでハンドラーを作成し、それを `managedGateway` に追加する必要があります。ハンドラーは、`DeviceFirmwareHandler` クラスを拡張し、以下のメソッドを実装する必要があります。

```java
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**注**: ファームウェアのダウンロードや更新の要求を転送するゲートウェイと接続されているデバイスの両方のために 1 つだけハンドラーをライブラリーに追加する必要があります。実装では、複数のファームウェア要求を同時に処理するために、スレッドまたはスレッド・プールを作成する必要があります。

スレッド・プール・ハンドラーの実装のサンプルは、[Gateway samples GutHub repository](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java) 内にあります。

### `downloadFirmware` のサンプル実装

実装では、`DeviceFirmware` オブジェクトを使用して、ファームウェアをダウンロードし、ダウンロードの状況をレポートするためのロジックを追加する必要があります。ファームウェア・ダウンロード操作が正常に完了した場合は、ファームウェアの状態を 'DOWNLOADED' に設定して、
`UpdateStatus` プロパティーを 'SUCCESS' に設定する必要があります。

ファームウェアのダウンロード中にエラーが発生した場合は、状態を 'IDLE' に設定し、`updateStatus` プロパティーを以下のいずれかのエラー状況値に設定する必要があります。

- OUT_OF_MEMORY
- CONNECTION_LOST
- INVALID_URI

以下のコード・サンプルは、ファームウェア・ダウンロードの実装の例を示しています。

**重要:** ここに示すコード・サンプルには、スレッド・プールのセクションは含まれていません。ファームウェア・ハンドラーの完全な実装のサンプルは、 [IBM Java ゲトウェイ・サンプル GitHub リポジトリリ](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java)にあります。

```java
public void downloadFirmware(DeviceFirmware deviceFirmware) {
	boolean success = false;
    URL firmwareURL = null;
    URLConnection urlConnection = null;

    try {
			firmwareURL = new URL(deviceFirmware.getUrl());
        urlConnection = firmwareURL.openConnection();
        if(deviceFirmware.getName() != null) {
            downloadedFirmwareName = deviceFirmware.getName();
        } else {
            // use the time stamp as the name
			downloadedFirmwareName = "firmware_" +new Date().getTime()+".deb";
		}

		File file = new File(downloadedFirmwareName);
		BufferedInputStream bis = new BufferedInputStream(urlConnection.getInputStream());
		BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(file.getName()));

		int data = bis.read();
        if(data != -1) {
            bos.write(data);
            byte[] block = new byte[1024];
            while (true) {
                int len = bis.read(block, 0, block.length);
                if(len != -1) {
                    bos.write(block, 0, len);
                } else {
                    break;
                }
            }
            bos.close();
            bis.close();
            success = true;
        } else {
            //There is no data to read, so set an error
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
        }
    } catch(MalformedURLException me) {
        // Invalid URL, so set the status to reflect the same,
        deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
    } catch (IOException e) {
        deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.CONNECTION_LOST);
    } catch (OutOfMemoryError oom) {
        deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
    }

    if(success == true) {
        deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
        deviceFirmware.setState(FirmwareState.DOWNLOADED);
    } else {
        deviceFirmware.setState(FirmwareState.IDLE);
    }
}
```

管理対象ゲートウェイでは、ダウンロードしたファームウェア・イメージの整合性をベリファイヤーを使用して検査し、その状況を {{site.data.keyword.iot_short}} に報告することができます。ベリファイヤーは、以下の段階でゲートウェイが設定できます。

- 開始中、'DeviceFirmware' オブジェクトが作成されるとき
- アプリケーションが 'downloadFirmware' 要求を実行依頼するとき

#### 例

```java
private boolean verifyFirmware(File file, String verifier) throws IOException {
	FileInputStream fis = null;
    String md5 = null;
    try {
        fis = new FileInputStream(file);
        md5 = org.apache.commons.codec.digest.DigestUtils.md5Hex(fis);
        System.out.println("Downloaded Firmware MD5 sum:: "+ md5);
    } catch (FileNotFoundException e) {
        e.printStackTrace();
    } catch (IOException e) {
        e.printStackTrace();
    } finally {
        fis.close();
    }
    if(verifier.equals(md5)) {
        System.out.println("Firmware verification successful");
		return true;
	}
	System.out.println("Download firmware checksum verification failed."
			+ "Expected "+verifier + " found "+md5);
    return false;
}
```

コード全体を示すサンプルは、ゲートウェイ管理サンプル [GatewayFirmwareHandlerSample](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java) にあります。

### `updateFirmware` のサンプル実装

実装では、別のスレッドを作成し、`DeviceFirmware` オブジェクトを使用してダウンロード済みのファームウェアをインストールして更新の状況をレポートするためのロジックを追加する必要があります。ファームウェア更新操作が正常に完了した場合は、ファームウェアの状態を 'IDLE' に設定して、`updateStatus` 値を 'SUCCESS' に設定する必要があります。

ファームウェア更新中にエラーが発生した場合は、`updateStatus` 値を以下のいずれかのエラー状況値に設定する必要があります。

* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE

以下のコード・サンプルは、Raspberry Pi デバイスのファームウェア更新を実装する方法を示しています。

```java
public void updateFirmware(DeviceFirmware deviceFirmware) {
	try {
			ProcessBuilder pkgInstaller = null;
        Process p = null;
        pkgInstaller = new ProcessBuilder("sudo", "dpkg", "-i", downloadedFirmwareName);
        boolean success = false;
        try {
            p = pkgInstaller.start();
            boolean status = waitForCompletion(p, 5);
            if(status == false) {
                p.destroy();
                deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
                return;
            }
            System.out.println("Firmware Update command "+status);
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
            deviceFirmware.setState(FirmwareState.IDLE);
        } catch (IOException e) {
            e.printStackTrace();
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
        } catch (InterruptedException e) {
            e.printStackTrace();
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
        }
    } catch (OutOfMemoryError oom) {
        deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
    }
}
```

完全なコードは、[ゲトウェイ・サンプル GitHub リポジトリリ](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java)の `GatewayFirmwareHandlerSample` サンプルにあります。

### ステップ 4: `ManagedGateway` へのハンドラーの追加

ハンドラーが作成したら、それを `ManagedGateway` インスタンスに追加して、{{site.data.keyword.iot_short}} からファームウェア・アクション要求が出されたときに Java クライアント・ライブラリーが対応するメソッドを呼び出すようにする必要があります。

```java
GatewayFirmwareHandlerSample fwHandler = new GatewayFirmwareHandlerSample();
mgdGateway.addFirmwareHandler(fwHandler);
```

ファームウェア・アクションについて詳しくは、[デバイス管理要求](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/requests.html#/firmware-actions#firmware-actions)を参照してください。

## デバイス・アクション
{: #dev_actions}

{{site.data.keyword.iot_short}} は、以下のデバイス・アクションをサポートしています。

- リブート
- 工場出荷時設定にリセット

ゲートウェイは、ゲートウェイそれ自体とゲートウェイの背後にあるデバイスのデバイス・アクションをサポートするために、次のアクティビティーを行う必要があります。

1. サーバーへのデバイス・アクション・サポートについての情報の通知。
2. デバイス・アクション・ハンドラーの作成。
3. `ManagedGateway` へのハンドラーの追加。

### ステップ 1: サーバーへのデバイス・アクション・サポートについての情報の通知

ゲートウェイとゲートウェイに接続されたデバイスに対してリブート・アクションやファクトリー・リセット・アクションを行うには、まずゲートウェイがサポートについての情報を {{site.data.keyword.iot_short}} に通知する必要があります。このアクションは、**Manage** 要求の送信時に、`supportDeviceActions` パラメーターに true の値を渡すことによって行うことができます。

ゲートウェイは、以下のメソッドを呼び出して、デバイス・アクションのサポートについての情報をサーバーに通知できます。

```java
// Last parameter represents the device action support
managedGateway.sendGatewayManageRequest(3600, true, true);
```

ゲートウェイは対応するデバイス・メソッドを呼び出して、接続されているデバイスがデバイス・アクションをサポートしていることを通知できます。

```java
// Last parameter represents the device action support
managedGateway.sendDeviceManageRequest(typeId, deviceId, 0, true, true);
```

サポート情報がデバイス管理サーバーに通知されると、サーバーはデバイス・アクション要求をデバイスに転送します。

### ステップ 2: デバイス・アクション・ハンドラーの作成

デバイス・アクションをサポートするために、ゲートウェイでハンドラーを作成し、それを `managedGateway` インスタンスに追加する必要があります。ハンドラーは、`DeviceActionHandler` クラスを拡張し、以下のメソッドを実装する必要があります。

```java
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**注:** デバイス・アクション要求を転送するゲートウェイと接続されているデバイスの両方のために 1 つだけハンドラーをライブラリーに追加する必要があります。実装では、複数のデバイス・アクション要求を同時に処理するために、スレッドまたはスレッド・プールを作成する必要があります。スレッド・プールを使用するハンドラー実装のサンプルは、[iot-gateway-samples GitHub リポジトリー](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java)にあります。

### `handleReboot` のサンプル実装

実装では、別のスレッドを作成し、`DeviceAction` オブジェクトを使用してゲートウェイと接続されているデバイスをリブートし、リブートの状況をレポートするためのロジックを追加する必要があります。要求を受け取った後、ゲートウェイはサポートまたは失敗についての情報をサーバーに通知してからでなければ、実際のリブートに進むことはできません。サンプルがデバイスをリブートできない場合や、リブート中に他のエラーが発生した場合には、ゲートウェイがオプションのメッセージで状況を更新できます。以下のコード・サンプルは、Raspberry Pi デバイスのリブートの実装例を示しています。

```java
public void handleReboot(DeviceAction action) {
	ProcessBuilder processBuilder = null;
    Process p = null;
    processBuilder = new ProcessBuilder("sudo", "shutdown", "-r", "now");
    boolean status = false;
    try {
        p = processBuilder.start();
        // wait for say 2 minutes before giving it up
        status = waitForCompletion(p, 2);
    } catch (IOException e) {
        action.setMessage(e.getMessage());
    } catch (InterruptedException e) {
        action.setMessage(e.getMessage());
    }
    if(status == false) {
        action.setStatus(DeviceAction.Status.FAILED);
    }
}
```

スレッド・プールを使用するハンドラーの実装サンプルの完全版は、[iot-gateway-samples GitHub リポジトリー](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java)にあります。


### `handleFactoryReset` のサンプル実装

実装では、別のスレッドを作成し、DeviceAction オブジェクトを使用してゲートウェイと接続されたデバイスを工場出荷時設定にリセットし、リセットの状況をレポートするためのロジックを追加する必要があります。要求を受け取った後、ゲートウェイはサポートまたは失敗についての情報をサーバーに通知してからでなければ、実際のリセットに進むことはできません。以下のコード・サンプルは、基本的なファクトリー・リセットの実装の例を示しています。

```java
public void handleFactoryReset(DeviceAction action) {
	try {
			// code to perform Factory reset
    } catch (IOException e) {
        action.setMessage(e.getMessage());
    }
    if(status == false) {
        action.setStatus(DeviceAction.Status.FAILED);
    }
}
```

### ステップ 3: `ManagedGateway` へのハンドラーの追加

ハンドラーが作成したら、それを `ManagedGateway` インスタンスに追加して、ゲートウェイまたは接続されたデバイスのためのデバイス・アクションの要求が {{site.data.keyword.iot_short}} から出されたときに、Java クライアント・ライブラリーが対応するメソッドを呼び出すようにする必要があります。

```java
GatewayActionHandlerSample actionHandler = new GatewayActionHandlerSample();
mgdGateway.addDeviceActionHandler(actionHandler);
```

デバイス・アクションについて詳しくは、[デバイス管理要求](../../devices/device_mgmt/requests.html#/device-actions-reboot#device-actions-reboot)を参照してください。

## デバイス属性変更の listen
{: #listen_device_attributes}

Java クライアント・ライブラリーは、{{site.data.keyword.iot_short}} から更新要求が出されるたびに、対応するオブジェクトを更新します。このような更新要求は、アプリケーションから直接開始されるか、{{site.data.keyword.iot_short}} REST API を使用してファームウェア更新により間接的に開始されます。ライブラリーは、これらの属性を更新するだけでなく、デバイス属性が更新されたときにそのことをゲートウェイに通知するためのメカニズムも提供します。

このタイプの操作によって更新できる属性は、ゲートウェイや接続されているデバイスのロケーション、メタデータ、デバイス情報、およびファームウェアです。

属性の変更に関する通知を受けるために、ゲートウェイは、対象のオブジェクトにプロパティー変更リスナーを追加する必要があります。以下のコード・サンプルはその方法を示しています。

```java
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

また、ゲートウェイは、通知を受け取るために `propertyChange()` メソッドを実装する必要もあります。以下の実装のサンプルにはその概要が示されています。

```java
public void propertyChange(PropertyChangeEvent evt) {
	if(evt.getNewValue() == null) {
        return;
	}
	Object value = (Object) evt.getNewValue();
		switch(evt.getPropertyName()) {
		case "metadata":
            DeviceMetadata metadata = (DeviceMetadata) value;
            System.out.println("Received an updated metadata -- "+ metadata);
            break;

        case "location":
            DeviceLocation location = (DeviceLocation) value;
            System.out.println("Received an updated location -- "+ location);
            break;

        case "deviceInfo":
            DeviceInfo info = (DeviceInfo) value;
            System.out.println("Received an updated device info -- "+ info);
            break;

        case "mgmt.firmware":
            DeviceFirmware firmware = (DeviceFirmware) value;
            System.out.println("Received an updated device firmware -- "+ firmware);
            break;
    }
}
```

デバイス属性の更新について詳しくは、[デバイス管理要求](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/index.html#/update-device-attributes#update-device-attributes)を参照してください。

## サンプル
{: #samples}

ゲートウェイとゲートウェイの背後にあるデバイスを {{site.data.keyword.iot_short_notm}} インスタンスに接続するために利用できるサンプルがいくつか用意されています。これらのサンプルは {{site.data.keyword.iot_short_notm}} Java クライアント・ライブラリーを使用しており、[ゲトウェイ・サンプル GitHub リポジトリリ](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples)に置かれています。

## レシピ
{: #recipes}

Rasberry Pi デバイスを管理対象ゲートウェイとして {{site.data.keyword.iot_short_notm}} に接続し、接続されたデバイスを管理する方法を示すレシピについては、[Raspberry Pi as a managed gateway in {{site.data.keyword.iot_short_notm}} ](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/)を参照してください。

このレシピは、{{site.data.keyword.iot_short_notm}} のデバイス管理プロトコルを使用して、ゲートウェイとして機能し、デバイスのリブートやスケッチ・プログラムの追加などのデバイス管理操作を実行する Raspberry Pi デバイスから、Arduino Uno デバイスを管理する方法を説明しています。
