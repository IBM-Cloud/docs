---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-01-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}  
{:codeblock: .codeblock}
{:pre: .pre}


# デバイス管理要求
{: #requests}


{{site.data.keyword.iot_full}} は、1 つ以上のデバイスに対して開始できるアクションを提供します。これらのアクションは、ダッシュボードまたは REST API を使用することによって開始できます。使用可能なアクションのタイプは、**デバイス・アクション**と**ファームウェア・アクション**です。

## ダッシュボードを使用したデバイス管理要求の開始
{: #initiating-dm-dashboard}

「デバイス」ページの**「アクション」**タブにナビゲートすることによって、ダッシュボードで要求を開始できます。**「操作の開始」**ボタンをクリックすると、アクションを選択できるダイアログ・ボックスが開きます。ここからアクション実行対象デバイスを選択し、選択したアクションがサポートする追加のパラメーターを指定します。

## REST API を使用したデバイス管理要求の開始
{: #initiating-dm-api}

次の REST API サンプルを使用して、要求を開始できます。  

`POST https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

デバイス管理要求の本体について詳しくは、[API 資料](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html)を参照してください。

## デバイス・アクション
{: #device-actions}

デバイスは、管理要求をパブリッシュするときに、デバイス・アクションをサポートすることを指定できます。デバイス・アクション要求は、デバイス・リブート・アクションとデバイス・リセット・アクションにデバイスが応答できることを {{site.data.keyword.iot_short_notm}} に示します。


## デバイス・アクション - リブート
{: #device-actions-reboot}

{{site.data.keyword.iot_short_notm}} ダッシュボードを使用するか、REST API を使用して、デバイス・リブート・アクションを開始できます。

REST API を使用してデバイス・リブートを開始するには、POST 要求を以下に対して発行します。

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

以下の情報を指定します。

- `device/reboot` アクション
- リブートするデバイスのリスト (最大 5000 デバイス)

デバイス・リブート要求の例を以下に示します。

```
{
    "action": "device/reboot",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

要求が開始されると、リブート要求の本体で指定されたすべてのデバイスに MQTT メッセージがパブリッシュされます。各デバイスは、リブート・アクションを開始できるかどうかを示す応答を送り返す必要があります。この操作を直ちに開始できる場合は、`rc` パラメーターを `202` に設定します。リブート試行が失敗した場合は、`rc` パラメーターを `500` に設定し、`message` パラメーターを適宜設定します。リブートがサポートされていない場合は、`rc` パラメーターを `501` に設定し、必要に応じて `message` パラメーターを適宜設定します。

デバイスがそのリブート後に「デバイスを管理」要求を送信したら、リブート・アクションは完了です。

### デバイス・リブート要求のトピック

サーバーはリブート要求を次のトピックでデバイスにパブリッシュします。

```
iotdm-1/mgmt/initiate/device/reboot
```

### デバイス・リブート要求のメッセージ形式


要求の形式:

```
サーバーからの着信メッセージ:

Topic: iotdm-1/mgmt/initiate/device/reboot
{
    "reqId": "string"
}
```

応答の形式:

```
デバイスからの出力メッセージ:

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```

## デバイス・アクション - 工場出荷時設定へのリセット
{: #device-actions-factory-reset}

{{site.data.keyword.iot_short_notm}} ダッシュボードを使用するか、REST API を使用して、工場出荷時設定へのリセット・アクションを開始できます。

REST API を使用してデバイスの工場出荷時設定へのリセットを開始するには、POST 要求を以下に対して発行します。

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

以下の情報を指定します。

- `device/factoryReset` アクション
- リセットするデバイスのリスト (最大 5000 デバイス)

次のサンプルは、デバイス・リセット要求の例を示しています。

```
{
    "action": "device/factoryReset",
    "devices": [
        {
            "typeId": "someType",
            "deviceId": "someId"
        }
    ]
}
```

デバイス・リセット要求が開始されると、要求の本体で指定されたすべてのデバイスに MQTT メッセージがパブリッシュされます。各デバイスは、工場出荷時設定へのリセット・アクションを開始できるかどうかを示す応答を返す必要があります。このアクションを直ちに開始できる場合は、応答コードを `202` に設定します。工場出荷時設定へのリセットの試行が失敗した場合は、`rc` パラメーターを `500` に設定し、`message` パラメーターを適宜設定します。工場出荷時設定へのリセット・アクションがサポートされていない場合は、`rc` パラメーターを `501` に設定し、必要に応じて `message` パラメーターを適宜設定します。

工場出荷時設定へのリセット後にデバイスが「デバイスを管理」要求を送信したら、工場出荷時設定へのリセット・アクションは完了です。

### 工場出荷時設定へのリセット要求のトピック

サーバーは次の要求をデバイスにパブリッシュします。

```
iotdm-1/mgmt/initiate/device/factory_reset
```


### 工場出荷時設定へのリセット要求のメッセージ形式


要求の形式:

```
次のトピックは、サーバーからの着信メッセージを示しています。

Topic: iotdm-1/mgmt/initiate/device/factory_reset
{
    "reqId": "string"
}
```

応答の形式:

```
次のトピックは、デバイスからの出力メッセージを示しています。

Topic: iotdevice-1/response
{
    "rc": "response_code",
    "message": "string",
    "reqId": "string"
}
```


## ファームウェア・アクション
{: #firmware-actions}

デバイス上の現在既知のファームウェア・レベルは、`deviceInfo.fwVersion` 属性に保管されます。`mgmt.firmware` 属性は、ファームウェア更新の実行とその状況の監視に使用されます。

**重要:** ファームウェア・アクションをサポートするためには、管理対象デバイスが `mgmt.firmware` 属性の監視をサポートしていなければなりません。

ファームウェア更新プロセスは、以下の別個のアクションに分かれています。
- ファームウェアのダウンロード
- ファームウェアの更新

ファームウェア・アクションそれぞれの状況が、デバイスの別々の属性に保管されます。 `mgmt.firmware.state` 属性は、ファームウェア・ダウンロードの状況を示します。次の表は、`mgmt.firmware.state` 属性に設定できる値を示しています。

 |値 |状態  | 意味 |
 |:---|:---|:---|
 |0  | アイドル        | デバイスは現在、ファームウェア・ダウンロードの進行中ではありません。 |  
 |1  | ダウンロード中 | デバイスは現在、ファームウェアのダウンロード中です。 |
 |2  | ダウンロード済み  | デバイスはファームウェア更新のダウンロードを正常に完了し、インストールする準備ができています。 |


`mgmt.firmware.updateStatus` 属性は、ファームウェア更新の状況を示します。`mgmt.firmware.updateStatus` 属性に使用できる値は、以下のとおりです。

|値 |状態 | 意味 |  
|:---|:---|:---|
|0 | 成功 | ファームウェアは正常に更新されました。 |
|1 | 進行中 | ファームウェア更新が開始されましたが、まだ完了していません。|
|2 | メモリー不足 | 操作中にメモリー不足の状態が検出されました。|
|3 | 接続が失われた     | ファームウェア・ダウンロード中に接続が失われました。 |
|4 | 検証失敗 | ファームウェアは検証に合格しませんでした。 |
|5 | サポートされないイメージ   | ダウンロードされたファームウェア・イメージはデバイスでサポートされていません。 |
|6 | 無効な URI         | 指定された URI からファームウェアをデバイスにダウンロードできませんでした。 |

## ファームウェア・アクション - ダウンロード
{: #firmware-actions-download}

{{site.data.keyword.iot_short_notm}} ダッシュボードを使用するか、REST API を使用して、ファームウェア・ダウンロード・アクションを開始できます。

REST API を使用してファームウェア・ダウンロードを開始するには、POST 要求を以下に対して発行します。

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

以下の情報を指定します。

- `firmware/download` アクション
- ファームウェア・イメージの URI
- イメージを受け取るデバイスのリスト (最大 5000 デバイス)
- イメージを検証するための検証ストリング (オプション)
- ファームウェア名 (オプション)
- ファームウェア・バージョン  (オプション)

次のサンプルは、以下のすべてのメッセージ例のベースとなるファームウェア・ダウンロード要求を示しています。

```
{
   "action" : "firmware/download",
   "parameters" : [{
         "name" : "uri",
         "value" : "some uri for firmware location"
      }, {
         "name" : "name",
         "value" : "some firmware name"
      }, {
         "name" : "verifier",
         "value" : "some validation code"
      }, {
         "name" : "version",
         "value" : "some firmware version"
      }
   ],
   "devices" : [{
         "typeId" : "someType",
         "deviceId" : "someId"
      }
   ]
}
```

{{site.data.keyword.iot_short_notm}} のデバイス管理サーバーは、デバイス管理プロトコルを使用して、ファームウェア・ダウンロードを開始する要求をデバイスに送信します。ダウンロード・プロセスは、以下のステップで構成されています。

1. ファームウェア詳細更新要求がトピック `iotdm-1/device/update` で送信されます。
この更新要求に基づいて、デバイスは、要求されたファームウェアが現在インストールされているファームウェアと異なるかどうかを検証できます。違いがある場合は、`rc` パラメーターを `204` に設定します。これは`変更済み`という状況を意味します。
  
次の例は、前に送信したファームウェア・ダウンロード要求例に関して予期されるメッセージと、違いが検出されたときに送信される応答を示しています。
```
   {{site.data.keyword.iot_short_notm}} からの着信要求:

   Topic: iotdm-1/device/update
   Message:
   {
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194",
      "d" : {
         "fields" : [{
               "field" : "mgmt.firmware",
               "value" : {
                  "version" : "some firmware version",
                  "name" : "some firmware name",
                  "uri" : "some uri for firmware location",
                  "verifier" : "some validation code",
                  "state" : 0,
                  "updateStatus" : 0,
                  "updatedDateTime" : ""
               }
            }
         ]
      }
   }

   デバイスからの出力応答:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 204,
      "reqId" : "f38faafc-53de-47a8-a940-e697552c3194"
   }
   ```
   この応答によって次の要求がトリガーされます。
2. ファームウェア・ダウンロード状況の監視要求 `iotdm-1/observe` が送信されます。
この監視要求によって、デバイスがファームウェア・ダウンロードを開始できる状態にあるかどうかが検査されます。直ちにダウンロードを開始できるときは、`rc` パラメーターを `200` (`Ok`) に設定し、
`mgmt.firmware.state` 属性を `0` (`アイドル`) に、`mgmt.firmware.updateStatus` 属性を `0` (`アイドル`) にそれぞれ設定します。次のコードは、{{site.data.keyword.iot_short_notm}} とデバイスの間の交換の例です。
   ```
   {{site.data.keyword.iot_short_notm}} からの着信要求:

   Topic: iotdm-1/observe
   Message:
   {
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
      "d" : {
         "fields" : [ {
            "field" : "mgmt.firmware"
            }
         ]
      }
   }

   デバイスからの出力応答:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 200,
      "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8"
   }
   ```
この交換により、最後のステップがトリガーされます。  

3. ダウンロード要求がトピック `iotdm-1/mgmt/initiate/firmware/download` で送信されます。

   ダウンロード要求は、ファームウェア・ダウンロードを開始するようデバイスに指示します。このアクションを直ちに開始できる場合は、`rc` パラメーターを `202` に設定します。次のコードは、ダウンロード開始要求の例を示しています。

   ```
   {{site.data.keyword.iot_short_notm}} からの着信要求:

   Topic: iotdm-1/mgmt/initiate/firmware/download
   Message:
   {
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }

   デバイスからの出力応答:

   Topic: iotdevice-1/response
   Message:
   {
      "rc" : 202,
      "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
   }
   ```

このようにしてファームウェア・ダウンロードが開始された後、デバイスはダウンロードの状況を {{site.data.keyword.iot_short_notm}} に報告する必要があります。デバイスは `iotdevice-1/notify` トピックにメッセージをパブリッシュすることによって状況を報告します。このメッセージでは、`mgmt.firmware.state` 属性が `1` (`ダウンロード中`) または `2` (`ダウンロード済み`) のどちらかに設定されます。
次のサンプルは、ファームウェア・ダウンロードの開始の例を示しています。

```
デバイスからの出力メッセージ:

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "123456789",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 1
             }
      } ]
   }
}


しばらくの間待機...


デバイスからの出力メッセージ:

Topic: iotdevice-1/notify
Message:
{
   "reqId" : "1234567890",
   "d" : {
      "fields" : [ {
         "field" : "mgmt.firmware",
         "value" : {
                 "state" : 2
             }
      } ]
   }
}
```



`mgmt.firmware.state` 属性が `2` に設定された通知がパブリッシュされると、`iotdm-1/cancel` トピックで要求がトリガーされます。この要求は、`mgmt.firmware` 属性の監視を取り消します。
`rc` パラメーターが `200` に設定された応答が送信されたら、ファームウェア・ダウンロードは完了です。以下に、コードの例を示します。

```
{{site.data.keyword.iot_short_notm}} からの着信要求:

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware"
         }
      ]
   }
}


デバイスからの出力メッセージ:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

以下の情報は、エラー処理に役立ちます。

- `mgmt.firmware.state` 属性が `0` (「アイドル」) でない場合は、応答コード `400` とメッセージ・テキスト (オプション) を含めたエラーを送信します。
- `mgmt.firmware.uri` 属性が設定されていない場合や有効な URI でない場合は、`rc` パラメーターを `400` に設定します。
- ファームウェア・ダウンロードの試行が失敗した場合は、`rc` パラメーターを `500` に設定し、必要に応じて `message` パラメーターを適宜設定します。
- ファームウェア・ダウンロードがサポートされていない場合は、`rc` パラメーターを `500` に設定し、必要に応じて `message` パラメーターを適宜設定します。
- デバイスが実行要求を受け取ったら、`mgmt.firmware.state` 属性を `0` (アイドル) から `1` (ダウンロード中) に変更します。
- ダウンロードが正常に完了したら、`mgmt.firmware.state` 属性を `2` (ダウンロード済み) に設定します。
- ダウンロード中にエラーが発生した場合は、`mgmt.firmware.state` 属性を `0` (アイドル) に設定し、`mgmt.firmware.updateStatus` 属性を以下のエラー状況値のいずれかに設定します。
  - 2 (メモリー不足)
  - 3 (接続が失われた)
  - 6 (無効な URI)
- ファームウェア・ベリファイヤーが設定されていれば、デバイスはファームウェア・イメージの検証を試みます。イメージ検証が失敗した場合は、`mgmt.firmware.state` 属性を `0` (アイドル) に設定し、`mgmt.firmware.updateStatus` 属性をエラー状況値 `4` (検証失敗) に設定します。

## ファームウェア・アクション - 更新
{: #firmware-actions-update}

ダウンロードされたファームウェアのインストールは、REST API を使用して POST 要求を以下に対して発行することによって開始されます。

`https://<org>.internetofthings.ibmcloud.com/api/v0002/mgmt/requests`

以下の情報を指定します。

- `firmware/update` アクション
- イメージを受け取るデバイスのリスト (同じデバイス・タイプのすべて)

次のコードは要求の例です。

```
   {
      "action" : "firmware/update",
      "devices" : [{
            "typeId" : "someType",
            "deviceId" : "someId"
         }
      ]
   }

```

ファームウェア更新の状況をモニターするために、{{site.data.keyword.iot_short_notm}} はまず、トピック `iotdm-1/observe` でオブザーバー要求をトリガーします。デバイスは、更新プロセスを開始できる状態になると、`rc` パラメーターが `200` に、`mgmt.firmware.state` 属性が `0` に、`mgmt.firmware.updateStatus` 属性が `0` にそれぞれ設定された応答を送信します。

以下に、コードの例を示します。

```
{{site.data.keyword.iot_short_notm}} からの着信要求:

Topic: iotdm-1/observe
Message:
{
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [
         {
            "field": "mgmt.firmware"
         }
      ]
   }
}

デバイスからの出力応答:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "909b477c-cd37-4bee-83fa-1d568664fbe8",
   "d" : {
      "fields" : [{
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```



ファームウェア更新が正常にダウンロードされた後、{{site.data.keyword.iot_short_notm}} のデバイス管理サーバーは、指定されたデバイスに対して、トピック `iotdm-1/mgmt/initiate/firmware/update` を使用してファームウェア・インストールを開始するよう、デバイス管理プロトコルを使用して要求します。
この操作を直ちに開始できる場合は、`rc` パラメーターを `202` に設定します。
まだファームウェアが正常にダウンロードされていない場合は、`rc` パラメーターを `400` に設定します。

以下に、コード例を示します。

```
{{site.data.keyword.iot_short_notm}} からの着信要求:

Topic: iotdm-1/mgmt/initiate/firmware/update
Message:
{
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}

デバイスからの出力応答:

Topic: iotdevice-1/response
Message:
{
   "rc" : 202,
   "reqId" : "7b244053-c08e-4d89-9ed6-6eb2618a8734"
}
```

ファームウェア更新要求を完了するために、デバイスはその `iotdevice-1/notify` トピックでパブリッシュされる状況メッセージを使用して、更新状況を {{site.data.keyword.iot_short_notm}} に報告します。
ファームウェア更新が完了したら、`mgmt.firmware.updateStatus` 属性が `0` (成功) に設定され、`mgmt.firmware.state` 属性が `0` (アイドル) に設定されます。ダウンロードされたファームウェア・イメージはその後デバイスから削除でき、`deviceInfo.fwVersion` 属性は `mgmt.firmware.version` 属性の値に設定されます。

次のコードは、通知メッセージの例を示しています。

```
デバイスからの出力メッセージ:

Topic: iotdevice-1/notify
Message:
{
   "d" : {
      "fields": [
         {
            "field" : "mgmt.firmware",
            "value" : {
               "state" : 0,
               "updateStatus" : 0
            }
         }
      ]
   }
}
```

ファームウェア更新完了通知を受け取ると、{{site.data.keyword.iot_short_notm}} は最後の要求として、`mgmt.firmware` 属性の監視を取り消す要求を `iotdm-1/cancel` トピックでトリガーします。


`rc` パラメーターが `200` に設定された応答が送信されたら、ファームウェア更新要求は完了です。以下に例を示します。

```
{{site.data.keyword.iot_short_notm}} からの着信要求:

Topic: iotdm-1/cancel
Message:
{
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f",
   "d" : {
      "fields" : [
         {
            "field" : "mgmt.firmware"
         }
      ]
   }
}


デバイスからの出力メッセージ:

Topic: iotdevice-1/response
Message:
{
   "rc" : 200,
   "reqId" : "d9ca3635-64d5-46e2-93ee-7d1b573fb20f"
}
```

エラーとプロセスの処理に役立つ情報を以下のリストに記載します。

- ファームウェア更新の試行が失敗した場合は、`rc` パラメーターを `500` に設定し、必要に応じて `message` パラメーターを設定して適切な情報が含められるようにします。
- ファームウェア更新がサポートされていない場合は、`rc` パラメーターを `501` に設定し、必要に応じて `message` パラメーターを設定して必要な情報が含められるようにします。
- `mgmt.firmware.state` 属性が `2` (ダウンロード済み) でない場合は、`rc` パラメーターが `400` に設定されたメッセージ・テキスト (オプション) が含まれたエラーを送信します。
- それ以外の場合は、`mgmt.firmware.updateStatus` 属性を `1` (進行中) に設定します。通常はこれでファームウェア・インストールが開始されます。
- ファームウェア・インストールが失敗した場合は、`mgmt.firmware.updateStatus` 属性を以下の値のいずれかに設定します。
  - `2` (メモリー不足)
  - `5` (サポートされないイメージ)


**重要:** `mgmt.firmware` 属性の一部としてリストされているすべてのパラメーターは、同時に設定する必要があります。そうすることで、`mgmt.firmware` が現在監視されている場合に、通知メッセージが 1 つだけ送信されるようにします。

## デバイス・アクションとファームウェア・アクションに関するレシピ

以下のレシピには、デバイス・アクションとファームウェア・アクションの実行に必要なフロー全体が示されています。

- [Device Management in WIoT Platform – Roll Back & Factory Reset](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/)

- [Device Initiated Firmware Update](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-device-initiated-firmware-upgrade/)

- [Platform Initiated Firmware Update](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/)

- [Platform Initiated Firmware Update with Background Execution](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-platform-initiated-firmware-upgrade/)

- [Firmware Roll Back & Factory Reset](https://developer.ibm.com/recipes/tutorials/device-management-in-wiot-platform-roll-back-factory-reset/)
