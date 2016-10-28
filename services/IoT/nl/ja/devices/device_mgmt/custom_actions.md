---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# デバイス管理の拡張
{: #custom_actions}
最終更新日: 2016 年 7 月 11 日
{: .last-updated}

REST API を使用するか、{{site.data.keyword.Bluemix_notm}} で提供されるダッシュボードを使用して、デバイス管理拡張を追加することにより、目的の要件を満たすように {{site.data.keyword.iot_full}} のデバイス管理機能を拡張できます。

デフォルトでは、{{site.data.keyword.iot_short_notm}} によって以下のデバイス管理アクションが提供され、サポートされます。
- デバイスのリブート
- 工場出荷時設定にリセット
- ファームウェア・ダウンロード
- ファームウェア更新

{{site.data.keyword.iot_short_notm}} によって提供されるデフォルトのデバイス・アクションが、目的のデバイスやアプリケーションにとって不十分な場合は、デバイス管理拡張パッケージを実装することによって、追加のデバイス管理機能を開発できます。

## デバイス管理拡張パッケージ
{: #device_management_ext}

デバイス管理拡張パッケージは、デバイス管理アクションのセットを定義する JSON 文書です。これらのアクションをサポートする 1 つ以上のデバイスに対してアクションを開始できます。アクションの開始には、{{site.data.keyword.iot_short_notm}} ダッシュボードを使用するか、デバイス管理 REST API コマンドを使用します。

次のコード・サンプルは、デバイス管理拡張パッケージの標準的な形式を示しています。

```

	{
		"bundleId": "<unique identifier>",
		"displayName": {
			"<locale 0>": "<localized display name 0>"
		},
		"description": {
			"<locale 0>": "<localized description 0>"
		},
		"version": "<bundle version>",
		"provider": "<bundle provider>",
		"actions": {
			"<actionId 0>": {
				"actionDisplayName": {
					"<locale 0>": "<localized action display name 0>"
				},
				"description": {
					"<locale 0>": "<localized description>"
				},
				"parameters": [
					{
						"name": "<parameterId>",
						"value": "<regex pattern for value checking>",
						"required": false,
						"defaultValue": "<default>"
					}
				]
			}
		}
	}

```

### 拡張パッケージのプロパティー

デバイス管理拡張パッケージには、以下のプロパティーが含まれます。

|プロパティー|説明|必須
|:---|:---|:---|
|`bundleId`|デバイス管理拡張の固有 ID。|はい|
|`version`|デバイス管理拡張のバージョン・ストリング。|いいえ|
|`provider`|デバイス管理拡張のプロバイダー・ストリング。1024 文字までに制限されます。|いいえ|
|`displayName`|{{site.data.keyword.iot_short_notm}} ダッシュボードに表示される `locale`: `String` 形式のキーと値のペアから成るマップ。少なくとも 1 つのエントリーを指定する必要があります。|はい|
|`description`|{{site.data.keyword.iot_short_notm}} ダッシュボードでの表示に使用される `locale`: `String` 形式のキーと値のペアから成るマップ。定義する場合は、少なくとも 1 つのエントリーを指定する必要があります。|いいえ|
|`actions`| デバイス管理拡張に含まれるアクションを定義する `actionId`: `<action>` 形式のキーと値のペアから成るマップ。少なくとも 1 つのエントリーを指定する必要があります。|はい|

### アクションごとのプロパティー

|プロパティー|説明|必須
|:---|:---|
|`actionDisplayName`|{{site.data.keyword.iot_short_notm}} ダッシュボードに表示される `locale`: `String` 形式のキーと値のペアから成るマップ。少なくとも 1 つのエントリーを指定する必要があります。|はい|
|`description`|{{site.data.keyword.iot_short_notm}} ダッシュボードでの表示に使用される `locale`: `String` 形式のキーと値のペアから成るマップ。オプションです。少なくとも 1 つのエントリーを指定する必要があります。|いいえ|
|`parameters`|特定のアクションに許可されるパラメーターの配列。定義する場合は、少なくとも 1 つのエントリーを指定する必要があります。|いいえ|

### アクション・パラメーターごとのプロパティー

|プロパティー|説明|必須
|:---|:---|
|`name`|アクションのパラメーターの固有 ID。|はい|
|`value`|要求開始時にパラメーター値の検証に使用される正規表現。指定しなければ、検証は行われません。|いいえ|
|`required`|パラメーターが必須かどうかを決定するブール値。デフォルトでは、値は false に設定されています。 |いいえ|
|`defaultValue`|要求開始時にパラメーターが指定されていない場合に使用する値。|いいえ|

**注:** `bundleId`、`version`、`actionId`、`parameterId` の各値に使用できる文字数は 255 文字までに制限されています。また、英数字 (a-z、A-Z、0-9) と次の特殊文字だけで構成する必要があります。
 - ダッシュ (-)
 - 下線 (_)
 - ドット (.)

## REST API
{: #rest_api}

以下の {{site.data.keyword.iot_short_notm}} REST API コマンドを使用して、拡張パッケージを管理します。

- すべてのデバイス管理拡張パッケージのリストを取得する:
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- 新しいデバイス管理拡張パッケージを作成する:
  `POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`
- 特定のデバイス管理拡張パッケージを取得する:
  `GET https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- デバイス管理拡張パッケージを更新する:
  `PUT https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`
- デバイス管理拡張パッケージを削除する:
  `DELETE https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle/{bundleId}`

デバイス管理拡張パッケージ用 REST API について詳しくは、[{{site.data.keyword.iot_short_notm}} API V2](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} のドキュメントを参照してください。


##カスタム・デバイス管理アクションのサポート
{: #supporting_custom_device_management_actions}

拡張パッケージで定義されたデバイス管理アクションは、それらのアクションをサポートするデバイスだけが開始できます。デバイスは {{site.data.keyword.iot_short_notm}} に管理要求をパブリッシュするときに、サポートできるアクションのタイプを指定します。

拡張パッケージに含まれるカスタム・アクションを受け取るには、次の例に示すように、デバイスからの要求の supports オブジェクトで拡張パッケージのバンドル ID を指定する必要があります。

```
	デバイスからの出力メッセージ:

	Topic: iotdevice-1/mgmt/manage
	{
		"d": {
			"supports": {
				"deviceActions": false,
				"firmwareActions": false,
				"<bundleId>": true
			}
		},
		"reqId": "<request id>"
	}

	サーバーからの着信応答:

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "<request id>"
	}

```

デバイス管理要求について詳しくは、[デバイス管理プロトコル](index.html){: new_window}を参照してください。

## カスタム・デバイス管理アクションの開始
{: #initiating_custom_dm_actions}

カスタム・デバイス管理アクションを開始するには、次の REST API コマンドを使用します。このコマンドは、デバイス管理アクションを開始するためのデフォルト・コマンドです。

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

要求を開始するときに、以下の情報を指定する必要があります。

- `<bundleId>/<actionId>` アクション
- アクション開始対象デバイスのリスト (最大 5000 デバイスまで)
- カスタム・アクション定義で定義されたパラメーターのリスト

要求を開始するためのペイロードの形式は、以下のとおりです。

```
	{
		"action": "<bundleId>/<actionId>",
		"devices": [
			{
				"typeId": "<deviceType 0>",
				"deviceId": "<deviceId 0>"
			}
		],
		"parameters": [
			{
				"name": "<parameter0>",
				"value": "<parameter0 value>"
			}
		]
	}

```


## カスタム・デバイス管理アクションの処理
{: #handling_custom_dm_actions}

デバイスに対してカスタム・アクションが開始されると、そのデバイスに MQTT メッセージがパブリッシュされます。MQTT メッセージには、要求の一部として指定されたパラメーターが含まれます。デバイスは MQTT メッセージを受け取ると、アクションを実行するか、または現在アクションを完了できない理由を示すエラー・コードで応答します。

デバイス・アクションが正常に完了すると、デバイスは `rc` 値が `200` に設定された応答をパブリッシュします。

次の抜粋は、サーバーとデバイスの間で行われる交換の例を示しています。

```
	サーバーからの着信メッセージ:

	Topic: iotdm-1/mgmt/custom/<bundleId>/<actionId>
	{
		"d": {
			"fields": [
				{
					"field": "<parameter0>",
					"value": "<parameter0 value>"
				}
			]
		},
		"reqId": "<request id>"
	}

	... 要求されたアクションをデバイスが実行 ...

	デバイスからの出力メッセージ:

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "<request id>"
	}

```

## 例
{: #example}

次の例は、新しいデバイス管理拡張を定義して、その拡張で定義されたアクションを実行するための方法を示しています。

何社かが `exampleDeviceType` デバイスを製造しています。`exampleDeviceType` デバイス上で実行するプラグインをインストールして管理できます。`exampleDeviceType` デバイス上のプラグインをリモート管理しやすくするために、製造メーカーは通常、{{site.data.keyword.iot_short_notm}} 組織にインポートできるデバイス管理拡張を提供しています。

この例では、次の拡張 JSON 文書が使用されます。

```
	{
		"bundleId": "exampleDeviceType-actions-v1",
		"displayName": {
			"en_US": "exampleDeviceType Actions v1"
		},
		"description": {
			"en_US": "Device management actions for exampleDeviceType devices"
		},
		"version": "1.0",
		"provider": "some company",
		"actions": {
			"installPlugin": {
				"actionDisplayName": {
					"en_US": "Install Plug-in"
				},
				"description": {
					"en_US": "Install a new plug-in on the device"
				},
				"parameters": [
					{
						"name": "pluginId",
						"value": "\\w+",
						"required": true
					},
					{
						"name": "pluginURI",
						"value": "((http:\\/\\/|https:\\/\\/)(.*)+)",
						"required": true
					}
				]
			},
			"enablePlugin": {
				"actionDisplayName": {
					"en_US": "Enable Plug-in"
				},
				"description": {
					"en_US": "Enables a plug-in on the device"
				},
				"parameters": [
					{
						"name": "pluginId",
						"value": "\\w+",
						"required": true
					}
				]
			},
			"disablePlugin": {
				"actionDisplayName": {
					"en_US": "Disable Plug-in"
				},
				"description": {
					"en_US": "Disables a plug-in on the device"
				},
				"parameters": [
					{
						"name": "pluginId",
						"value": "\\w+",
						"required": true
					}
				]
			},
			"uninstallPlugin": {
				"actionDisplayName": {
					"en_US": "Uninstall Plug-in"
				},
				"description": {
					"en_US": "Uninstall a plug-in from the device"
				},
				"parameters": [
					{
						"name": "pluginId",
						"value": "\\w+",
						"required": true
					}
				]
			}
		}
	}

```
このデバイス管理拡張パッケージでは、以下のアクションが定義されています。

- **installPlugin**
- **enablePlugin**
- **disablePlugin**
- **uninstallPlugin**

拡張を追加するには、次の REST API コマンドを使用します。

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

組織 `<orgID>` に登録されているデバイスは、管理要求をパブリッシュするときに、`exampleDeviceType-actions-v1` アクションをサポートしていることを指定できます。以下に例を示します。

```
	Outgoing message from device:

	Topic: iotdevice-1/mgmt/manage
	{
		"d": {
			"supports": {
				"exampleDeviceType-actions-v1": true
			}
		},
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
デバイスは {{site.data.keyword.iot_short_notm}} から次の応答を受け取ります。

```
	Incoming message from server:

	Topic: iotdm-1/response
	{
		"rc": 200,
		"reqId": "f38faafc-53de-47a8-a940-e697552c3194"
	}

```
この時点で、`exampleIoT-exampleDeviceType-v1` 拡張で定義したデバイス・アクションを開始できます。

`installPlugin` アクションを開始するために、次のペイロードが使用されます。

```
	{
		"action": "exampleDeviceType-actions-v1/installPlugin",
		"devices": [
			{
				"typeId": "exampleDeviceType",
				"deviceId": "device0"
			},
			{
				"typeId": "exampleDeviceType",
				"deviceId": "device1"
			}
		],
		"parameters": [
			{
				"name": "pluginId",
				"value": "testPluginA"
			},
			{
				"name": "pluginURI",
				"value": "http://www.example.com/testPluginA.zip"
			}
		]
	}

```
次の REST API コマンドを使用して、要求を開始します。

`POST https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

コマンドが送信されると、`exampleDeviceType` タイプのデバイス `device0` と `device1` が、次の MQTT メッセージを受け取ります。

```
	Incoming message from server:

	Topic: iotdm-1/mgmt/custom/exampleDeviceType-actions-v1/installPlugin
	{
		"d": {
			"fields": [
				{
					"field": "pluginId",
					"value": "testPluginA"
				},
				{
					"field": "pluginURI",
					"value": "http://www.exampleiot.com/testPluginA.zip"
				}
			]
		},
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```

デバイスはそれぞれ、メッセージに基づいてアクションを取り、指定されたプラグインをインストールします。インストールが完了すると、デバイスはアクションが正常に完了したことを示すメッセージを送信します。

```
	デバイスからの出力メッセージ:

	Topic: iotdevice-1/response
	{
		"rc": 200,
		"reqId": "d38faafc-53de-47a8-a940-e697552c3194"
	}

```

この時点で、`installPlugin` デバイス管理アクションが完了します。

## API の例
{: #api_examples}

以下の API 要求を使用して、デバイスを管理します。

- 新しいデバイス管理拡張を作成する:

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- デバイス管理拡張をリストするには、以下のようにします。

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/custom/bundle`

- デバイス管理要求を開始するには、以下のようにします。

`curl -XPOST -d '<insert payload here>' -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- 進行中のまたは完了したデバイス管理要求をリストするには、以下のようにします。

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests`

- 特定のデバイス管理要求の状況を表示するには、以下のようにします。

`curl -XGET -H "Content-Type: application/json" -u "<apiKey>:<apiToken>" https://<orgID>.internetofthings.ibmcloud.com:443/api/v0002/mgmt/requests/<requestId>`
