---

copyright:
  years: 2015, 2017
lastupdated: "2016-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# アプリケーションの HTTP REST API
{: #api}

{{site.data.keyword.iot_full}} HTTP REST API を使用して、{{site.data.keyword.iot_short_notm}} の組織と対話するアプリケーションを作成し、カスタマイズできます。
{:shortdesc}

## 機能
{: #capabilities}

{{site.data.keyword.iot_short_notm}} HTTP REST API は、アプリケーションの以下の機能や動作をサポートします。

- 組織情報の取得
- デバイスの一括操作 (リスト表示、追加、削除)
- デバイス・タイプの操作 (リスト表示、作成、削除、詳細の表示、更新)
- デバイス操作 (リスト表示、追加、削除、詳細の表示、更新、ロケーションの表示、管理情報の表示)
- デバイス診断操作 (ログの消去、ログの取得、ログ情報の追加、ログの削除、特定のログの取得、エラー・コードの消去、デバイス・エラー・コードの取得、エラー・コードの追加)
- 接続の問題判別 (デバイス接続ログ・イベントのリスト表示)
- 最後のイベント・キャッシュ (特定のデバイスの最後のイベントの表示)
- デバイス管理要求の操作 (デバイス管理要求のリスト表示、要求の開始、要求状況の消去、要求の詳細の取得、すべての要求状況をデバイス別にリスト表示、特定のデバイスの要求状況の取得)
- 使用状況管理の操作 (使用したデータ総量の取得)
- デバイス・イベントのパブリッシュ (ベータ)
- サービス状況の照会 (組織別のサービス状況の取得)

## HTTP REST API 資料へのアクセス
{: #api_link}

{{site.data.keyword.iot_short_notm}} HTTP REST API 資料にアクセスしてアプリケーションの作成とカスタマイズを行う方法に関する情報をさらに入手するには、[API](../reference/api.html) を参照してください。

サポートされている {{site.data.keyword.iot_short_notm}} HTTP REST API のバージョンはバージョン 2 のみです。{{site.data.keyword.iot_short_notm}} ソリューションには必ずバージョン 2 を使用してください。

# アプリケーション用の HTTP Messaging API
{: #rest_messaging_api}

{{site.data.keyword.iot_short_notm}} HTTP Messaging API 資料にアクセスして、HTTP を使用してイベントをパブリッシュしたりコマンドを送信したりする方法に関する詳細情報を見つけるには、[{{site.data.keyword.iot_short_notm}} HTTP Messaging API ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window} を参照してください。

## イベントとコマンドのパブリッシュ
{: #event_command_publication}

MQTT メッセージング・プロトコルを使用するほかにも、HTTP を使用してイベントやコマンドを {{site.data.keyword.iot_short_notm}} にパブリッシュするようにアプリケーションを構成できます。そのためには、以下の HTTP REST API コマンドのいずれかを使用します。

### 無保護のイベント POST 要求
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### セキュアなイベント POST 要求
<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**注:** デフォルト SSL ポートのポート 443 も、セキュアな HTTP API 呼び出し用に指定できます。

### 無保護のコマンド POST 要求
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></code></pre>


### セキュアなコマンド POST 要求
<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></code></pre>
{: codeblock}

Quickstart サービスにデバイスまたはアプリケーションを接続している場合は、**orgId** を文字列「quickstart」に置換してください。

**注:**
- アプリケーションで 1 つの HTTP 接続を再利用してさまざまなデバイスにイベントまたはコマンドをポストすることができますが、許可 HTTP ヘッダーを変更することはできません。
- ポート 443 (デフォルトの SSL ポート) は、セキュアな HTTP API 呼び出しにも指定できます。

### 認証

すべての要求には許可ヘッダーを組み込む必要があります。基本認証が、唯一サポートされる方法です。アプリケーションは、API キーを使用して認証されます。アプリケーションが {{site.data.keyword.iot_short_notm}} HTTP REST API を使用して要求を行う場合、以下の資格情報が必要です。

```
ユーザー名 = API キー (例: a/orgId/a84ps90Ajs)
パスワード = 認証トークン
```

### Content-Type 要求ヘッダー

`Content-Type` 要求ヘッダーを要求に含める必要があります。以下の表に、サポート対象タイプがどのように {{site.data.keyword.iot_short_notm}} 内部フォーマットにマップされるかを示します。

|Content-Type ヘッダー|{{site.data.keyword.iot_short_notm}} での形式 |
|:---|:---|
|text/plain|"text"
|application/json| "json"
|application/xml | "xml"
|application/octet-stream|"bin"

### サービス品質

HTTP REST メッセージングは、MQTT サービス品質における「最高 1 回」送信サービス・レベル 0 と同じように、非永続メッセージ送信を行いますが、HTTP 応答を送信する前に、要求が正しいことと、サーバーに送信可能であることを検証します。HTTP 状況コード 200 を含む応答によって、メッセージがサーバーに届いたことを確認できます。「最高 1 回」の MQTT サービス品質レベルまたは HTTP の同等機能を使用してイベント・メッセージを送信する場合、デバイスまたはアプリケーションが送信を保証するための再試行ロジックを実装している必要があります。


{{site.data.keyword.iot_short_notm}} の MQTT プロトコルおよびサービス品質レベルについて詳しくは、[MQTT メッセージング](../reference/mqtt/index.html)を参照してください。
