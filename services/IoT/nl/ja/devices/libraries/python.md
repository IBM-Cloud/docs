---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# デバイス開発者用の Python
{: #python}

Python を使用して、{{site.data.keyword.iot_full}} で組織と対話するデバイス・コードをビルド/開発することができます。{{site.data.keyword.iot_short_notm}} 用の Python クライアントは、MQTT や HTTP などの基礎的なプロトコルを抽象化することで、{{site.data.keyword.iot_short_notm}} 機能とのシンプルな対話を促進する API を備えています。{:shortdesc}

提供されている情報と例を使用し、Python を使用したデバイスの開発を開始します。

## Python クライアントとリソースのダウンロード
{: #python_client_download}

{{site.data.keyword.iot_short_notm}} 用の Python クライアントやその他の使用可能なリソースを利用するには、GitHub の [iot-python](https://github.com/ibm-watson-iot/iot-python) リポジトリーにアクセスし、インストール手順を実行します。

## コンストラクター
{: #constructor}

options 辞書は、{{site.data.keyword.iot_short_notm}} モジュールと対話するために使用する定義を作成します。コンストラクターはクライアント・インスタンスを作成し、以下の定義を格納する options 辞書を受け入れます。

|定義|説明 |
|:---|:---|
|`orgId`|組織 ID。|
|`type`|デバイスのタイプ。デバイスのタイプとは、特定のタスクを実行するデバイスのグループです (「weatherballoon」など)。|
|`id`|デバイスを特定するための固有の ID。通常、特定のデバイス・タイプにおいて、デバイス ID はそのデバイスの固有の ID です (シリアル番号や MAC アドレスなど)。|
|`auth-method`|認証の方式。サポートされている唯一の方式は `apikey` です。|
|`auth-token`|API キー・トークン。auth-method の値を `apikey` に設定する場合は、これも指定する必要があります。|
|`clean-session`|true または false 値。永続サブスクリプション・モードでアプリケーションを接続する場合のみ必要です。デフォルトでは、`clean-session` は true に設定されます。|

options 辞書が提供されない場合、クライアントは未登録デバイスとして {{site.data.keyword.iot_short_notm}} Quickstart サービスに接続されます。

```python

import ibmiotf.device
try:
  options = {
    "org": orgId,
    "type": deviceType,
    "id": deviceId,
    "auth-method": authMethod,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### 構成ファイルの使用

options 辞書を直接定義する代わりに、以下のコード・サンプルに示されているように、options 辞書を構成ファイルで別個に定義することもできます。

```python

import ibmiotf.device
try:
  options = ibmiotf.device.ParseConfigFile(configFilePath)
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

options 辞書を格納する構成ファイルは、以下の形式でなければなりません。

```python

[device]
org=orgID
type=deviceType
id=deviceId
auth-method=token
auth-token=token
clean-session=true/false
```

## イベントのパブリッシュ
{: #publishing_events}

イベントとは、デバイスが {{site.data.keyword.iot_short_notm}} にデータをパブリッシュするためのメカニズムのことです。デバイスはイベントの内容を制御し、送信するイベントごとに名前を割り当てます。

{{site.data.keyword.iot_short_notm}} インスタンスがイベントを受信すると、その受信イベントの資格情報によって、送信元デバイスが識別されます。そのためデバイスが、別のデバイスになりすますことはできません。

イベントは、MQTT プロトコルによって定義された 3 つのサービス品質 (QoS) レベルのいずれでもパブリッシュできます。デフォルトでは、イベントは QoS レベル `0` でパブリッシュされます。

### デフォルトのサービス品質を使用したイベントのパブリッシュ

```
client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData)
```

### イベントの QoS レベルの引き上げ

パブリッシュされるイベントの[サービス品質 (QoS) レベル](../../reference/mqtt/index.html#qos-levels)を引き上げることができます。QoS レベルが `0` より高いイベントは、追加の確認受信情報が含まれているため、パブリッシュにかかる時間が延びる可能性があります。

**注:** Quickstart フロー・モードは、QoS レベル `0` のみをサポートしています。

```
client.connect()
myQosLevel=2
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData, myQosLevel)
```
## コマンドの処理
{: #handling_commands}

デバイス・クライアントは、接続時に、このデバイスに対して指定されたコマンドに自動的にサブスクライブします。特定のコマンドを処理するには、コマンド・コールバック・メソッドを登録する必要があります。メッセージは、以下のプロパティーがある Command クラスのインスタンスとして返されます。

|プロパティー|データ・タイプ|説明|
|:---|:---|
|`command`|ストリング|コマンドを識別します。|
|`format`|ストリング|形式は任意のストリング (JSON など) となります。|
|`data`|辞書|ペイロードのデータ。最大長は 131072 バイトです。|
|`timestamp`|日時|イベントの日時。|


```python

def myCommandCallback(cmd):
  print("Command received: %s" % cmd.data)
  if cmd.command == "setInterval":
    if 'interval' not in cmd.data:
      print("Error - command is missing required information: 'interval'")
    else:
      interval = cmd.data['interval']
  elif cmd.command == "print":
    if 'message' not in cmd.data:
      print("Error - command is missing required information: 'message'")
    else:
      print(cmd.data['message'])

...
client.connect()
client.commandCallback = myCommandCallback
```

## カスタム・メッセージ形式のサポート
{: #custom_message_format}

デフォルトでは、メッセージ形式は `json` に設定されます。つまり、ライブラリーが JSON 形式の Python 辞書オブジェクトのエンコードとデコードをサポートします。メッセージの形式が `json-iotf` に設定されると、メッセージは {{site.data.keyword.iot_short_notm}} JSON ペイロードの仕様に応じてエンコードされます。独自のカスタム・メッセージ形式のサポートを追加する場合は、GitHub の[カスタム・メッセージ形式のサンプル](https://github.com/ibm-watson-iot/iot-python/tree/master/samples/customMessageFormat)を参照してください。

カスタム・エンコーダー・モジュールを作成するときは、以下の例に示されているように、デバイス・クライアントに登録する必要があります。

```python

import myCustomCodec

client.setMessageEncoderModule("custom", myCustomCodec)
client.publishEvent("status", "custom", myData)
```
イベントが不明な形式で送信されたり、デバイスが形式を認識しなかったりする場合、デバイスのライブラリーは `MissingMessageDecoderException` 条件を戻します。
