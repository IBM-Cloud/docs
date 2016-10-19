---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# デバイス用の HTTP REST API
{: #api}
最終更新日: 2016 年 9 月 9 日
{: .last-updated}

**重要:** デバイス用の {{site.data.keyword.iot_full}} HTTP REST API 機能は、限定されたベータ・プログラムの一部としてのみ使用できます。今後の更新によって、この機能の現行バージョンと互換性のない変更が行われる可能性があります。この機能を試して、[ご意見をお寄せください](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html)。

## HTTP REST API へのアクセス
{: #api_link}

{{site.data.keyword.iot_short_notm}} HTTP REST API にアクセスしてデバイスを組織に統合する方法に関する情報をさらに入手するには、https://docs.internetofthings.ibmcloud.com/swagger/v0002.html をご覧ください。

サポートされている {{site.data.keyword.iot_short_notm}} HTTP REST API のバージョンはバージョン 2 のみです。{{site.data.keyword.iot_short_notm}} ソリューションには必ずバージョン 2 を使用してください。

# デバイス用の HTTP REST Messaging API
{: #rest_messaging_api}

## イベントのパブリッシュ
{: #event_publication}

MQTT メッセージング・プロトコルの使用に加えて、HTTP REST API コマンドを使用して、HTTP を介してイベントを {{site.data.keyword.iot_short_notm}} にパブリッシュするようにデバイスを構成することもできます。

{{site.data.keyword.iot_short_notm}} に接続されているデバイスから `POST` 要求を送信するには、以下のいずれかの URL を使用します。

### 非セキュアな POST 要求
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### セキュアな POST 要求
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

デバイスまたはアプリケーションを Quickstart サービスに接続している場合は、代わりに以下のいずれかの URL を使用してください。

### Quickstart への非セキュアな POST 要求
<pre class="pre">http://quickstart.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Quickstart へのセキュアな POST 要求
<pre class="pre">https://quickstart.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**重要事項:**
- 現在の HTTP REST API バージョンでは、HTTP メッセージングを使用してのみ、デバイス・イベントを送信できます。他のデバイス管理機能と制御機能の要求を送信するには、MQTT メッセージング・プロトコルを使用します。
- 許可 HTTP ヘッダーを変更できないときは、HTTP 接続を再使用して、同じデバイスのイベントのみをパブリッシュできます。

### 認証

すべての要求には許可ヘッダーを組み込む必要があります。基本認証が、唯一サポートされる方法です。デバイスが {{site.data.keyword.iot_short_notm}} HTTP REST API を使用して HTTP 要求を行う場合、以下の資格情報が必要です。

```
username = "use-token-auth"
password = Authentication token
```

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
