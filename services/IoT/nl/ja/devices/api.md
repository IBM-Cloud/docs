---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-21"
---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# デバイス用の HTTP REST API
{: #api}

**重要:** デバイス用の {{site.data.keyword.iot_full}} HTTP REST API 機能は、限定されたベータ・プログラムの一部としてのみ使用できます。今後の更新によって、この機能の現行バージョンと互換性のない変更が行われる可能性があります。この機能を試して、[ご意見をお寄せください ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html){: new_window}。

## HTTP REST API 資料へのアクセス
{: #api_link}

{{site.data.keyword.iot_short_notm}} HTTP REST API 資料にアクセスしてデバイスを組織に統合する方法に関する情報をさらに入手するには、[API](../reference/api.html) を参照してください。

サポートされている {{site.data.keyword.iot_short_notm}} HTTP REST API のバージョンはバージョン 2 のみです。{{site.data.keyword.iot_short_notm}} ソリューションには必ずバージョン 2 を使用してください。

## クライアント接続
{: #client_connections}

クライアント・セキュリティーの詳細と、クライアントを {{site.data.keyword.iot_short_notm}} のデバイスに接続する方法については、[{{site.data.keyword.iot_short_notm}} へのアプリケーション、デバイス、ゲートウェイの接続](../reference/security/connect_devices_apps_gw.html)を参照してください。

# デバイス用の HTTP REST Messaging API
{: #rest_messaging_api}

{{site.data.keyword.iot_short_notm}} HTTP Messaging API 資料にアクセスして、HTTP を使用してイベントをパブリッシュする方法に関する詳細情報を見つけるには、[{{site.data.keyword.iot_short_notm}} HTTP Messaging API ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window} を参照してください。

## イベントのパブリッシュ
{: #event_publication}

MQTT メッセージング・プロトコルの使用に加えて、HTTP REST API コマンドを使用して、HTTP を介してイベントを {{site.data.keyword.iot_short_notm}} にパブリッシュするようにデバイスを構成することもできます。

{{site.data.keyword.iot_short_notm}} に接続されているデバイスから `POST` 要求を送信するには、以下のいずれかの URL を使用します。

### 非セキュアな POST 要求
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### セキュアな POST 要求

<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**注:** デフォルト SSL ポートのポート 443 も、セキュアな HTTP API 呼び出し用に指定できます。

デバイスまたはアプリケーションを Quickstart サービスに接続している場合は、代わりに以下のいずれかの URL を使用してください。

### Quickstart への非セキュアな POST 要求
<pre class="pre"><code class="hljs">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Quickstart へのセキュアな POST 要求
<pre class="pre"><code class="hljs">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**重要事項:**
- 現在の HTTP REST API バージョンでは、HTTP メッセージングを使用してのみ、デバイス・イベントを送信できます。他のデバイス管理機能と制御機能の要求を送信するには、MQTT メッセージング・プロトコルを使用します。
- 許可 HTTP ヘッダーを変更できないときは、HTTP 接続を再使用して、同じデバイスのイベントのみをパブリッシュできます。
- ポート 443 (デフォルトの SSL ポート) は、セキュアな HTTP API 呼び出しにも指定できます。

### 認証

すべての要求には許可ヘッダーを組み込む必要があります。基本認証が、唯一サポートされる方法です。デバイスが {{site.data.keyword.iot_short_notm}} HTTP REST API を使用して HTTP 要求を行う場合、以下の資格情報が必要です。

|資格情報|必要な入力|
|:---|:---|
|ユーザー名|`use-token-auth`
|パスワード| 自動生成の認証トークン、またはデバイス登録時に手動で指定した認証トークン。


### Content-Type 要求ヘッダー

`Content-Type` 要求ヘッダーを要求に含める必要があります。以下の表に、サポート対象タイプがどのように {{site.data.keyword.iot_short_notm}} 内部フォーマットにマップされるかを示します。

|Content-Type ヘッダー |{{site.data.keyword.iot_short_notm}} での形式 |
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### サービス品質

HTTP REST メッセージングは、MQTT サービス品質における「最高 1 回」送信サービス・レベル 0 と同じように、非永続メッセージ送信を行いますが、HTTP 応答を送信する前に、要求が正しいことと、サーバーに送信可能であることを検証します。HTTP 状況コード 200 を含む応答によって、メッセージがサーバーに届いたことを確認できます。「最高 1 回」の MQTT サービス品質レベルまたは HTTP の同等機能を使用してイベント・メッセージを送信する場合、デバイスまたはアプリケーションが送信を保証するための再試行ロジックを実装している必要があります。

{{site.data.keyword.iot_short_notm}} の MQTT プロトコルおよびサービス品質レベルについて詳しくは、[MQTT メッセージング](../reference/mqtt/index.html)を参照してください。

## 最新イベント・キャッシュ
{: #last-event-cache}

{{site.data.keyword.iot_short_notm}} Last Event Cache API を使用して、デバイスによって送信された最新のイベントを取得することができます。これは、デバイスがオンラインかオフラインかに関わらず機能するので、デバイスの物理的位置や使用状況に関係なくデバイスの状況を取得できます。特定のデバイスで 1 つのイベント ID について最後に記録された値を取得することも、特定のデバイスで報告された各イベント ID について最後に記録された値を取得することもできます。過去 365 日以内に発生したものであれば、特定のイベントに関するデバイスの最新イベント・データを取得できます。

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
