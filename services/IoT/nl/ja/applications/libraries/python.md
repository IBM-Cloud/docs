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


# アプリケーション開発者用の Python
{: #python}


Python を使用して、{{site.data.keyword.iot_full}} の組織と対話するアプリケーションをビルドし、作成できます。{{site.data.keyword.iot_short_notm}} 用の Python クライアントは、MQTT や HTTP などの基礎的なプロトコルを抽象化することで、{{site.data.keyword.iot_short_notm}} 機能とのシンプルな対話を促進する API を備えています。

{:shortdesc}

Python を使用したアプリケーションの開発を始められるように情報やサンプルが用意されているので活用してください。

## Python クライアントとリソースのダウンロード
{: #python_client_download}

{{site.data.keyword.iot_short_notm}} 用の Python クライアントや、提供されている他のリソースを利用するには、[iot-python](https://github.com/ibm-messaging/iot-python) リポジトリーに移動し、インストール手順を実行します。

## コンストラクター
{: #constructor}

options 辞書は、{{site.data.keyword.iot_short_notm}} モジュールと対話するために使用する定義を作成します。コンストラクターはクライアント・インスタンスを作成し、以下の定義を格納する options 辞書を受け入れます。

|定義|説明 |
|:-----|:-----|
|`orgId`|組織 ID。|
|`appId`|組織内のアプリケーション固有の ID。|
|`auth-method`|認証の方式。サポートされている唯一の方式は `apikey` です。|
|`auth-key`|オプションの API キー。auth-method の値を `apikey` に設定する場合は、これを指定する必要があります。|
|`auth-token`|API キー・トークン。auth-method の値を `apikey` に設定する場合は、これも指定する必要があります。|
|`clean-session`|true または false 値。永続サブスクリプション・モードでアプリケーションを接続する場合のみ必要です。デフォルトでは、`clean-session` は true に設定されます。|


options 辞書が提供されない場合、クライアントは未登録デバイスとして {{site.data.keyword.iot_short_notm}} Quickstart サービスに接続されます。

```python

import ibmiotf.application
try:
  options = {
    "org": organization,
    "id": appId,
    "auth-method": authMethod,
    "auth-key": authKey,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### 構成ファイルの使用


options 辞書を使用しない場合は、options 辞書を格納する構成ファイルを、次のコード形式で含める必要があります。

```python

import ibmiotf.application
try:
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException as e:
...
```
このアプリケーション構成ファイルは、次の形式にする必要があります。

```python

[application]
org=orgId
id=myApplication
auth-method=apikey
auth-key=key
auth-token=token
clean-session=true/false

```

## API 呼び出し
{: #api_calls}

API クライアントの各メソッドは、次のいずれかの応答を返します。

- 成功した場合には、有効な JSON またはブール値の応答
- 成功しなかった場合には、IoTFCReSTException 例外

API 呼び出しが失敗した理由についての詳細を取得したり、操作が部分的に成功したかどうかを判断したりするために、アプリケーションで例外応答のプロパティーを解析することができます。IoTFCReSTException 例外応答には、次のプロパティーが含まれています。

|プロパティー|説明|
|:---|:---|
|`httpcode`|HTTP 状況コード。|
|`message`|失敗した理由が含まれている例外メッセージ。|
|`response`|部分的な応答が含まれている JSON エレメント。存在しない場合、この値は Null に設定されます。|

## デバイス・イベントのサブスクライブ
{: #subscribe_device_events}

イベントとは、デバイスが {{site.data.keyword.iot_short_notm}} インスタンスにデータをパブリッシュするためのメカニズムのことです。デバイスはイベントの内容を制御し、送信するイベントごとに名前を割り当てます。

{{site.data.keyword.iot_short_notm}} インスタンスがイベントを受信すると、その受信イベントの資格情報によって、送信元デバイスが識別されます。そのためデバイスが、別のデバイスになりすますことは不可能です。

デフォルトでは、アプリケーションは、すべての接続デバイスのすべてのイベントをサブスクライブします。deviceType、deviceId、event、msgFormat の各パラメーターを使用して、サブスクリプションの範囲を制御できます。単一のクライアントで複数のサブスクリプションをサポートできます。次のコード・サンプルは、deviceType、deviceId、event、msgFormat の各パラメーターを使用してサブスクリプションの範囲を定義する方法を示しています。


### すべてのデバイスのすべてのイベントをサブスクライブする


```python

import ibmiotf.application
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents()
```

### 特定のタイプに属するすべてのデバイスのすべてのイベントをサブスクライブする


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType)
```

### すべてのデバイスの特定のイベントをサブスクライブする


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(event=myEvent)
```

### 複数の異なるデバイスの特定のイベントをサブスクライブする

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, event=myEvent)
client.subscribeToDeviceEvents(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId, event=myEvent)
```

### JSON フォーマットでパブリッシュされたすべてのイベントをサブスクライブする

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, msgFormat="json")
```

## デバイスからのイベントの処理
{: #handling_events_devices}

サブスクリプションで受信したイベントを処理するには、イベント・コールバック・メソッドを登録する必要があります。メッセージは、以下の Event クラスのインスタンスとして返されます。

|プロパティー|データ・タイプ|説明|
|:---|:---|
|`event.device`|ストリング|組織内のすべてのタイプのデバイスにおいて対象デバイスを一意に識別します。|
|`event.deviceType`|ストリング|デバイス・タイプを識別します。通常、deviceType は、特定のタスクを実行するデバイスのグループです (例えば "weatherballoon")。|
|`event.deviceId`|ストリング|デバイスの ID を示します。通常、特定のデバイス・タイプにおいて、deviceId はそのデバイスの固有 ID です (シリアル番号や MAC アドレスなど)。|
|`event.event`|ストリング|通常、特定の複数のイベントをグループ化するために使用します (「status」、「warning」、「data」など)。
|`event.format`|ストリング|形式は任意のストリング (JSON など) となります。
|`event.data`|辞書|メッセージ・ペイロードのデータ。最大長は 131072 バイトです。
|`event.timestamp`|日時|イベントの日時|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  def myEventCallback(event):
      str = "%s event '%s' received from device [%s]: %s"
      print(str % (event.format, event.event, event.device, json.dumps(event.data)))

...
client.connect()
client.deviceEventCallback = myEventCallback
client.subscribeToDeviceEvents()
```


## デバイス状況のサブスクライブ
{: #subscribe_device_status}


デフォルトでは、デバイス状況をサブスクライブすると、すべての接続デバイスの状況更新を受信します。タイプと ID のパラメーターを使用して、サブスクリプションの範囲を制御できます。単一のクライアントで複数のサブスクリプションをサポートできます。

### すべてのデバイスの状況更新をサブスクライブする


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus()
```

### 特定のタイプのすべてのデバイスの状況更新をサブスクライブする


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType)
```

### 2 つの異なるデバイスの状況更新をサブスクライブする


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType, deviceId=myDeviceId)
client.subscribeToDeviceStatus(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId)
```

## デバイスからの状況更新の処理
{: #handling_device_updates}

状況イベント

サブスクリプションで受信した状況更新を処理するには、イベント・コールバック・メソッドを登録する必要があります。メッセージは、Status クラスのインスタンスとして返されます。

状況イベントには、`Connect` イベントと `Disconnect` イベントの 2 つのタイプがあります。すべての状況イベントには、次のプロパティーが含まれています。

|プロパティー|データ・タイプ|
|:---|:---|
|`status.clientAddr`|ストリング|
|`status.protocol`|ストリング|
|`status.clientId`|ストリング|
|`status.user`|ストリング|
|`status.time`|日時|
|`status.action`|ストリング|
|`status.connectTime`|日時|
|`status.port`|整数|


`status.action` プロパティーによって、状況イベントのタイプが `Connect` と `Disconnect` のどちらであるかを判別できます。

`Disconnect` 状況イベントには、次の追加のプロパティーが含まれています。

|プロパティー|データ・タイプ|
|:---|:---|
|`status.writeMsg`|整数|
|`status.readMsg`|整数|
|`status.reason`|ストリング|
|`status.readBytes`|整数|
|`status.writeBytes`|整数|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

def myStatusCallback(status):

  if status.action == "Disconnect":
    str = "%s - device %s - %s (%s)"
    print(str % (status.time.isoformat(), status.device, status.action, status.reason))
    else:
      print("%s - %s - %s" % (status.time.isoformat(), status.device, status.action))
  ...
client.connect()
client.deviceStatusCallback = myStatusCallback
client.subscribeToDeviceStstus()
```


## デバイスからのイベントのパブリッシュ
{: #publishing_device_events}

アプリケーションは、デバイスからパブリッシュされたかのようにイベントをパブリッシュすることができます。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent(myDeviceType, myDeviceId, "status", "json", myData)
```


## デバイスへのコマンドのパブリッシュ
{: #publishing_commands_devices}


アプリケーションは、接続デバイスにコマンドをパブリッシュできます。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
commandData={'rebootDelay' : 50}
client.publishCommand(myDeviceType, myDeviceId, "reboot", "json", myData)
```


## 組織の詳細
{: #org_details}

アプリケーションは `getOrganizationDetails()` メソッドを使用して、組織の構成に関する詳細情報を取得できます。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    orgDetail = client.api.getOrganizationDetails()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

要求と応答のモデル、および HTTP 状況コードについては、[{{site.data.keyword.iot_short_notm}} API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html) の『Organization Configuration』セクションを参照してください。


## デバイスの一括操作
{: #bulk_device_ops}

アプリケーションで一括操作を使用して、複数のデバイスを同時に取得、追加、削除できます。

照会パラメーター、要求と応答のモデル、HTTP 状況コードのリストについては、[{{site.data.keyword.iot_short_notm}} API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/) の『Bulk Operations』セクションを参照してください。


### デバイス情報の取得

`getAllDevices()` メソッドを使用すると、一括デバイス情報を取得できます。このメソッドは、組織内のすべての登録デバイスに関する情報を取得します。要求は 1 つあたり最大で 512 KB にすることができます。

応答には、アプリケーションに必要なパラメーターが含まれています。応答に含まれている辞書結果を使用して、返されたデバイスの配列を取得できます。応答に含まれている他のパラメーターは、追加の呼び出しを行う場合に必要になります。例えば、`_bookmark` 要素を使用して結果をページ送りすることができます。最初の要求はブックマークを指定せずに送信します。そして、応答で返されたブックマークを取得し、次のページを要求するときにそのブックマークを指定します。これを、結果セットの最後まで繰り返します (ブックマークが返されなくなったら、結果セットの最後です)。他のパラメーターについては、すべての要求で同じ値を使用する必要があります。そうしないと未定義の結果になります。


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceList = client.api.getAllDevices()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```
### 複数のデバイスの追加


`addMultipleDevices()` メソッドを使用すると、1 つ以上のデバイスを {{site.data.keyword.iot_short_notm}} 組織に追加できます。要求は、512 KB 以下にする必要があります。応答には、デバイスごとに生成された認証トークンが含まれています。認証トークンを失って取得できなくなった場合に備えて、認証トークンのコピーを作成してください。


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
  deviceList = client.api.addMultipleDevices(listOfDevicesToAdd)
except IoTFCReSTException as e:
  print("ERROR [" + e.httpcode + "] " + e.message)
```

### 複数のデバイスの削除


`deleteMultipleDevices()` メソッドを使用すると、{{site.data.keyword.iot_short_notm}} 組織から複数のデバイスを削除できます。
要求は、512 KB 以下にする必要があります。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToDelete = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
      deviceList = client.api.deleteMultipleDevices(listOfDevicesToDelete)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## デバイス・タイプの操作
{: #device_type_ops}

組織で作成したデバイス・タイプを、デバイスを追加するためのテンプレートを作成するときに使用できます。{{site.data.keyword.iot_short_notm}} API の機能を使用して、アプリケーションで組織内のデバイス・タイプのリスト表示、作成、削除、表示、更新を行えます。

照会パラメーター、要求と応答のモデル、HTTP 状況コードについては、[{{site.data.keyword.iot_short_notm}} API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html) 資料の『Device types』セクションを参照してください。


### すべてのデバイス・タイプの取得

`getAllDeviceTypes()` メソッドを使用すると、{{site.data.keyword.iot_short_notm}} 組織内に存在するすべてのデバイス・タイプを取得できます。
応答に含まれている辞書結果を使用して、返されたデバイスの配列を取得できます。応答に含まれている他のパラメーターは、追加の呼び出しを行う場合に必要になります。例えば、`_bookmark` 要素を使用して結果をページ送りすることができます。最初の要求はブックマークを指定せずに送信します。そして、応答で返されたブックマークを取得し、次のページを要求するときにそのブックマークを指定します。この処理を、結果セットの最後まで繰り返します (ブックマークが返されなくなったら、結果セットの最後です)。他のパラメーターについては、すべての要求で同じ値を使用する必要があります。そうしないと未定義の結果になります。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

 listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
   options = {'_limit' : 2}
   deviceTypeList = client.api.getAllDeviceTypes(options)
except IoTFCReSTException as e:
   print("ERROR [" + e.httpcode + "] " + e.message)

```

### デバイス・タイプの追加

`addDeviceType()` メソッドを使用すると、{{site.data.keyword.iot_short_notm}} インスタンスにデバイス・タイプを登録できます。要求ごとに、まずはデバイス情報を定義し、次に、そのタイプのすべてのデバイスに適用するデバイス・メタデータ要素を定義する必要があります。デバイス情報の要素は、シリアル番号、製造元、モデル、クラス、説明、ファームウェア、ハードウェア・バージョン、ロケーションの説明など、複数の変数から構成されます。メタデータ要素は、ユーザーが定義できるカスタムの変数と値から構成されます。


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2"
  }

try:
      deviceType = client.api.addDeviceType(deviceType = "myDeviceType", description = "My first device type", deviceInfo = info, metadata = meta)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### デバイス・タイプの削除


`deleteDeviceType()` メソッドを使用すると、{{site.data.keyword.iot_short_notm}} 組織のデバイス・タイプを削除できます。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
      success = client.api.deleteDeviceType("myDeviceType")
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### 特定のデバイス・タイプの情報の取得


`getDeviceType()` メソッドを使用すると、特定のデバイス・タイプの情報を取得できます。取得するデバイス・タイプの `typeId` をパラメーターとして指定する必要があります。

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceTypeInfo = client.api.getDeviceType("myDeviceType")
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

### デバイス・タイプの更新


`updateDeviceType()` メソッドを使用すると、データ・タイプのプロパティーを変更できます。`updateDeviceType()` メソッドを使用する場合は、まず、更新するデバイス・タイプの `typeId` を指定し、次に、以下の要素を指定します。

- `description`
- `deviceInfo`
- `metadata`

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2",
      "customField3": "customValue3"
  }

try:
      updatedDeviceTypeInfo = client.api.updateDeviceType("myDeviceType", "New description", deviceInfo, metadata)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## デバイス操作
{: #device_ops}

API で利用できるデバイス操作には、{{site.data.keyword.iot_short_notm}} 組織内のデバイスのリスト作成、追加、削除、表示、更新、ロケーションの表示、デバイス管理情報の表示などがあります。


照会パラメーター、要求と応答のモデル、HTTP 状況コードについては、[{{site.data.keyword.iot_short_notm}} API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html) の『Device』セクションを参照してください。


### 特定のデバイス・タイプのデバイスの取得

`retrieveDevices()` メソッドを使用すると、次の例に示すように、{{site.data.keyword.iot_short_notm}} インスタンスの組織内の特定のデバイス・タイプに属するすべてのデバイスを取得できます。


```python

   print("\nRetrieving All existing devices")
   print("Retrieved Devices = ", apiCli.retrieveDevices(deviceTypeId))
```

応答に含まれている辞書結果を使用して、返されたデバイスの配列を取得できます。応答に含まれている他のパラメーターは、追加の呼び出しを行う場合に必要になります。例えば、*_bookmark* 要素を使用して結果をページ送りすることができます。最初の要求はブックマークを指定せずに送信します。そして、応答で返されたブックマークを取得し、次のページを要求するときにそのブックマークを指定します。これを、結果セットの最後まで繰り返します (ブックマークが返されなくなったら、結果セットの最後です)。他のパラメーターについては、すべての要求で同じ値を使用する必要があります。そうしないと未定義の結果になります。

*_bookmark* または他の条件を渡すには、多重定義メソッドを使用する必要があります。多重定義メソッドは、次の例に示すように、辞書形式のパラメーターを受け取ります。

```python
response = apiClient.retrieveDevices("iotsample-arduino", parameters);
```

上記のコード・サンプルは、デバイス ID で応答をソートし、ブックマークを使用して結果をページ送りします。

### デバイスの追加


デバイスを {{site.data.keyword.iot_short_notm}} 組織に追加するには、`registerDevice()` メソッドを使用します。`registerDevice()` メソッドは、単一のデバイスを {{site.data.keyword.iot_short_notm}} 組織に追加します。デバイスを追加するときには、次のパラメーターを指定できます。

|パラメーター|要件|説明
|:---|:---|
|`deviceTypeId`|オプション|デバイスにデバイス・タイプを割り当てます。デバイス・タイプで定義されている変数と、`deviceInfo` 変数で定義した変数が矛盾している場合は、デバイス固有の変数が優先されます。|
|`deviceId`|必須||
|`authToken`|オプション|指定しない場合は、認証トークンが生成されて応答に含められます。|
|`deviceInfo`|オプション|シリアル番号、製造元、モデル、デバイス・クラス、説明、ロケーションの説明、ファームウェア、ハードウェア・バージョンなどの複数の変数が含まれます。|
|`metadata`|オプション|カスタム・フィールドの値文字列のペア ([デバイス・タイプを追加するためのサンプル・コード](#sample_device_type)に大まかに示しています)。|
|`location`|オプション|経度、緯度、高度、精度、measuredDateTime 変数が含まれます。|

これらのパラメーターの詳細や、応答形式、応答コードについては、[API 資料](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Devices/post_device_types_typeId_devices)を参照してください。

`registerDevice()` メソッドを使用する場合は、必須の deviceID パラメーターと、デバイスに応じて必要なオプションのパラメーターを定義してから、選択したパラメーターを使用してメソッドを呼び出します。

### デバイス・タイプを追加するためのサンプル・コード
{: #sample_device_type}

Python(.py) スクリプト・ファイルのコンストラクター・コードの後に、次のコードを挿入します。このサンプルでは、deviceId、authToken、metadata、deviceInfo、location の各パラメーターを定義してデバイス・タイプを追加する方法を示しています。

```python

deviceId = "200020002000"
authToken = "password"
metadata = {"customField1": "customValue1", "customField2": "customValue2"}
deviceInfo = {"serialNumber": "001", "manufacturer": "Blueberry", "model": "abc1", "deviceClass": "A", "descriptiveLocation" : "Bangalore", "fwVersion" : "1.0.1", "hwVersion" : "12.01"}
location = {"longitude" : "12.78", "latitude" : "45.90", "elevation" : "2000", "accuracy" : "0", "measuredDateTime" : "2015-10-28T08:45:11.662Z"}

apiCli.registerDevice(deviceTypeId, deviceId, metadata, deviceInfo, location)
```
### デバイスの削除

`deleteDevice()` メソッドを使用して、{{site.data.keyword.iot_short_notm}} 組織上の組織からデバイスを削除できます。`deleteDevice()` メソッドを使用してデバイスを削除する場合は、deviceTypeId パラメーターと deviceId パラメーターを指定する必要があります。

次のコード・サンプルは、このメソッドに必要なフォーマットの概要を示しています。

```python
apiCli.deleteDevice(deviceTypeId, deviceId)
```

### デバイスの取得

`getDevice()` メソッドを使用して、{{site.data.keyword.iot_short_notm}} 上の組織からデバイスを取得できます。`getDevice()` メソッドを使用してデバイスの詳細を取得する場合は、deviceTypeId パラメーターと deviceId パラメーターを指定する必要があります。

次のコード・サンプルは、このメソッドに必要なフォーマットを大まかに示しています。

```python
apiCli.getDevice(deviceTypeId, deviceId)
```

### すべてのデバイスの取得

`getAllDevices()` メソッドを使用して、{{site.data.keyword.iot_short_notm}} 上の組織のすべてのデバイスを取得できます。

```python
apiCli.getAllDevices({'typeId' : deviceTypeId})
```

### デバイスの更新

デバイスの 1 つ以上のプロパティーを変更するには、`updateDevice()` メソッドを使用します。

deviceInfo パラメーターまたは metadata パラメーターを使用して、任意のプロパティーを更新できます。デバイス・プロパティーを更新するには、`updateDevice()` メソッドを呼び出す前に deviceInfo パラメーターを定義します。status パラメーターには、`alert`: True を含める必要があります。alert プロパティーは、デバイスのエラー・コードを {{site.data.keyword.iot_short_notm}} ユーザー・インターフェースに表示するかどうかを制御します。デフォルトでは、`enabled`: True に設定されます。次のコード・サンプルに大まかに示します。

```python
status = { "alert": { "enabled": True }  }
apiCli.updateDevice(deviceTypeId, deviceId, metadata2, deviceInfo, status)
```

### deviceInfo プロパティーを更新するためのサンプル・コード

次のコード・サンプルでは、特定のデバイスを指定してから、deviceInfo パラメーターの複数のプロパティーを更新します。

```python
status = { "alert": { "enabled": True } }
deviceInfo = {descriptiveLocation: "London", hwVersion: "2.0.1", fwVersion: "2.5.1"}
apiCli.updateDevice("MyDeviceType", "200020002000", deviceInfo, status)
```

### ロケーション情報の取得


`getDeviceLocation()` メソッドを使用して、デバイスのロケーション情報を取得できます。ロケーション・データを取得するために必要なパラメーターは、deviceTypeId と deviceId です。

```python
apiClient.getDeviceLocation("iotsample-arduino", "arduino01")
```  

このメソッドの応答には、経度、緯度、高度、精度、measuredTimeStamp、updatedTimeStamp のプロパティーが含まれます。

### ロケーション情報の更新


`updateDeviceLocation()` メソッドを使用して、デバイスのロケーション情報を変更できます。デバイス・プロパティーを更新する場合と同様に、適用する変更内容を、deviceLocation パラメーターに定義する必要があります。次のコード・サンプルは、特定のデバイスのロケーション・データを変更する方法を示しています。

```python
deviceLocation = { "longitude": 0, "latitude": 0, "elevation": 0, "accuracy": 0, "measuredDateTime": "2015-10-28T08:45:11.673Z"}
apiCli.updateDeviceLocation(deviceTypeId, deviceId, deviceLocation)
```

日付を指定しない場合は、現在の日時が使用されます。


### 管理情報の取得


`getDeviceManagementInformation()` メソッドを使用して、デバイスのデバイス管理情報を取得できます。応答には、最後のアクティビティーが行われた日時、デバイスの休止状況 (True/False)、デバイスとファームウェアの操作のサポート、ファームウェア・データが含まれています。応答内容を示す包括的なリストについては、関連する API 資料を参照してください。

次のコード・サンプルは、deviceId が「00aabbccde03」に、deviceTypeId が「iotsample-arduino」に設定されているデバイスのデバイス管理情報を返します。

```
apiCli.getDeviceManagementInformation("iotsample-arduino", "00aabbccde03")
```

## デバイスの診断操作
{: #device_diag_ops}

デバイスの診断操作を使用して、トラブルシューティングとログ管理のための次の作業を実施できます。
- ログの消去
- デバイスのすべてのログまたは特定のログの取得
- ログ情報の追加
- ログの削除
- エラー・コードの消去
- デバイス・エラー・コードの取得
- エラー・コードの追加

照会モデルと応答モデル、応答コード、照会パラメーターについて詳しくは、[API 資料](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html) {{site.data.keyword.iot_short_notm}} API 資料を参照してください。

### 診断ログの取得


`getAllDiagnosticLogs()` メソッドを使用して、特定のデバイスのすべての診断ログを取得できます。`getAllDiagnosticLogs()` メソッドには、deviceTypeId パラメーターと deviceId パラメーターが必要です。

```python
apiCli.getAllDiagnosticLogs(deviceTypeId, deviceId)
```

このメソッドの応答モデルには、ログ ID、メッセージ、重大度、データ、タイム・スタンプのプロパティーが含まれています。

### デバイスの診断ログの消去


`clearAllDiagnosticLogs()` メソッドを使用して、特定のデバイスのすべての診断ログを削除できます。必須パラメーターは、deviceTypeId と deviceId です。いったん削除したログ・ファイルはリカバリーできないため、削除操作は慎重に行ってください。

```python
apiCli.clearAllDiagnosticLogs(deviceTypeId, deviceId)
```

### 診断ログの追加


`addDiagnosticLog()` メソッドを使用して、デバイスの診断ログにエントリーを追加できます。新しいエントリーを追加すると、ログのプルーニングが実行されることがあります。日付を指定しない場合は、現在の日時がエントリーに追加されます。このメソッドを使用するには、次の変数を使用して 'logs' パラメーターを定義する必要があります。


|変数|要件|説明|
|:---|:---|:---|
|`message`|必須|追加する診断メッセージを含めます。|
|`severity`|オプション|診断ログの重大度を示します。0、1、2 (通知、警告、エラーの各カテゴリーに対応) のいずれかに設定できます。|
|`data`|オプション|診断データを含めます。|
|`timestamp`|オプション|ログ・エントリーの日時を ISO8601 形式で含めます。ただし、指定しない場合は、現在の日時が使用されます。|


このほかに、このメソッドに必要なパラメーターは、デバイスの deviceTypeId 値と deviceId 値です。

次のコード・サンプルは、`addDiagnosticLog()` メソッドの例を示しています。

```python
logs = { "message": "MessageContent", "severity": 0, "data": "LogData"}
apiCli.addDiagnosticLog(deviceTypeId, deviceId, logs)
```

### 特定の診断ログの取得


`getDiagnosticLog()` メソッドを使用すると、指定したデバイスに関する特定の診断ログを、ログ ID に基づいて取得できます。このメソッドに必要なパラメーターは、deviceTypeId、deviceId、logId です。

```python
apiCli.getDiagnosticLog(deviceTypeId, deviceId, logId)
```

### 診断ログの削除


`deleteDiagnosticLog()` メソッドを使用して、特定の診断ログを削除できます。診断ログを指定するために、deviceTypeId、deviceId、logID の各パラメーターを指定する必要があります。

```python
apiCli.deleteDiagnosticLog(deviceTypeId, deviceId, logId)
```

### デバイス・エラー・コードの取得


`getAllDiagnosticErrorCodes()` メソッドを使用して、特定のデバイスに関連付けられているすべての診断エラー・コードを取得できます。

```python
apiCli.getAllDiagnosticErrorCodes(deviceTypeId, deviceId)
```

### 診断エラー・コードの消去


`clearAllErrorCodes()` メソッドを使用して、特定のデバイスに関連付けられているエラー・コードのリストを消去できます。リストは単一のエラー・コード、ゼロに置き換えられます。

```python
apiCli.clearAllErrorCodes(deviceTypeId, deviceId)
```

### 単一の診断エラー・コードの追加


`addErrorCode()` メソッドを使用して、特定のデバイスに関連付けられているエラー・コードのリストにエラー・コードを 1 つ追加できます。新しいエントリーを追加すると、リストのプルーニングが実行されることがあります。このメソッドに必要なパラメーターは、deviceTypeId、deviceId、errorCode です。errorCode パラメーターには、次の変数が含まれます。

- errorCode: この変数は必須で、整数として設定する必要があります。この変数は、作成するエラー・コードの番号を設定します。
- timestamp: この変数はオプションであり、ログのエントリーの日付と時刻を ISO8601 形式で含めます。この変数を含めない場合は、自動的に現在の日付と時刻を使用して追加されます。

```python
errorCode = { "errorCode": 1234, "timestamp": "2015-10-29T05:43:57.112Z" }
apiCli.addErrorCode(deviceTypeId, deviceId, errorCode)
```

## 接続の問題判別
{: #connection_problem_determination}

`getDeviceConnectionLogs()` メソッドを使用して、特定のデバイスの接続ログ・イベントをリストできます。接続ログ・イベントを使用すると、デバイスと {{site.data.keyword.iot_short_notm}} サービスの間の接続の問題を診断するのに役立ちます。これらのエントリーには、成功した接続、失敗した接続試行、意図的な切断、サーバーから開始された切断イベントが記録されています。

```
apiCli.getDeviceConnectionLogs(deviceTypeId, deviceId)
```

応答には、ログ・メッセージとタイム・スタンプを含むログ・エントリーのリストが含まれます。
