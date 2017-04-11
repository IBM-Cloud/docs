---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-07"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# ゲートウェイ・デバイス用の HTTP REST API
{: #api_link}


{{site.data.keyword.iot_short_notm}} HTTP REST API 資料にアクセスして、デバイスの作成、更新、削除、リストに関する情報をさらに入手するには、[{{site.data.keyword.iot_short_notm}}HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html) を参照してください。

サポートされている {{site.data.keyword.iot_short_notm}} HTTP REST API のバージョンはバージョン 2 のみです。{{site.data.keyword.iot_short_notm}} ソリューションには必ずバージョン 2 を使用してください。

## クライアント接続
{: #client_connections}

クライアント・セキュリティーの詳細と、クライアントを {{site.data.keyword.iot_short_notm}} のゲートウェイ・デバイスに接続する方法については、[{{site.data.keyword.iot_short_notm}} へのアプリケーション、デバイス、ゲートウェイの接続](../reference/security/connect_devices_apps_gw.html)を参照してください。


### 認証

すべての要求には許可ヘッダーを組み込む必要があります。基本認証が、唯一サポートされる方法です。デバイスが {{site.data.keyword.iot_short_notm}} HTTP REST API を使用して HTTP 要求を行う場合、以下の資格情報が必要です。

|資格情報|必要な入力|
|:---|:---|
|ユーザー名| `g/{orgId}/{gwType}/{gwDevId}`
|パスワード| 自動生成の認証トークン、またはゲートウェイ・デバイス登録時に手動で指定した認証トークン。

各部の意味は、次のとおりです。

**_orgId_**   
- 組織名。ホスト・ヘッダーに指定されている名前と一致する必要があります。

**_gwType_**
- ゲートウェイのタイプ。

**_gwDevId_**

- ゲートウェイのデバイス ID。

### Content-Type 要求ヘッダー

`Content-Type` 要求ヘッダーを要求に含める必要があります。以下の表に、サポート対象タイプがどのように {{site.data.keyword.iot_short_notm}} 内部フォーマットにマップされるかを示します。

|Content-Type ヘッダー|{{site.data.keyword.iot_short_notm}} での形式 |
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

## 最新イベント・キャッシュ
{: #last-event-cache}

{{site.data.keyword.iot_short_notm}} Last Event Cache API を使用して、デバイスによって送信された最新のイベントを取得することができます。この API は、デバイスがオンラインかオフラインかに関わらず機能するので、デバイスの物理的位置や使用状況に関係なくデバイスの状況を取得できます。特定のデバイスで 1 つのイベント ID について最後に記録された値を取得することもできますし、特定のデバイスで報告された各イベント ID について最後に記録された値を取得することもできます。過去 365 日以内に発生したものであれば、特定のイベントに関するデバイスの最新イベント・データを取得できます。

特定のイベント ID について最新の値を要求するには、以下のような API 要求を使用します。この要求では、「power」というイベント ID について最後に記録された値が返されます。

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events/power
```

以下のような JSON 形式で応答が返されます。

```
{
    "deviceId": "<device-id>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<device-type>"
}
```

**注:** API 応答は JSON 形式ですが、イベント・ペイロードは任意の形式で記述できます。最終イベント・キャッシュ API から返されるペイロードは base64 でエンコードされます。

1 つのデバイスで報告された各イベント ID について最新の値を要求するには、以下のような API 要求を使用します。

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events
```

応答には、そのデバイスから送信されたすべてのイベント ID が組み込まれます。以下の例では、「power」と「temperature」というイベントの値が返されます。

```
[
    {
        "deviceId": "<device-id>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<device-type>"
},
    {
        "deviceId": "<device-id>",
        "eventId": "temperature",
        "format": "json",
        "payload": "eyJpbnRlcm5hbCI6MjIsICJleHRlcm5hbCI6MTZ9",
        "timestamp": "2016-03-14T14:17:44.891+0000",
        "typeId": "<device-type>"
    }
]
```
