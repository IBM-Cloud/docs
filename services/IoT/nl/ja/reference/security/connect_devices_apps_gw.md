---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-19"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} へのアプリケーション、デバイス、ゲートウェイの接続
{: #connect_devices_apps_gw}

アプリケーション、デバイス、ゲートウェイは、MQTT プロトコルを使用して {{site.data.keyword.iot_full}} に接続できます。デバイスは、HTTP REST API を使用して {{site.data.keyword.iot_short_notm}} に接続することもできます。
{: shortdesc}


## クライアント接続 URL
{: #client_connect_url}

デバイス、アプリケーション、ゲートウェイの各クライアントを {{site.data.keyword.iot_short_notm}} インスタンスに接続するには、次の接続 URL を使用します。

### メッセージング・アドレス

<pre class="pre"><var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com</pre>
{: codeblock}

### HTTP REST API 接続 URL

<pre class="pre">https://<var class="keyword varname">orgId</var>.internetofthings.ibmcloud.com/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**注**
- *orgId* は、サービス・インスタンスを登録したときに生成された固有の組織 ID です。
- デバイスまたはアプリケーションを Quickstart サービスに接続する場合は、*orgId* 値に 'quickstart' を指定します。

## ポート・セキュリティー
{: #client_port_security}

必須のポートが開いており、通信に使用可能であることを確認してください。ポート 8883 と 443 は、TLS と MQTT プロトコルと HTTP プロトコルを使用したセキュア接続をサポートします。ポート 1883 は、MQTT プロトコルと HTTP プロトコルを使用した非セキュア接続をサポートします。次の表に、接続タイプとそれに関連するポート番号に関する情報の要約を示します。   

|接続タイプ |ポート番号|
|:---|:---|
|非セキュア|1883|
|セキュア|8883|
|セキュア|443|

MQTT は、TCP と WebSockets でサポートされています。MQTT クライアントは接続の際に適切な資格情報を使用します (例えば、デバイスの場合はデバイス認証トークン、アプリケーションの場合は API キーとトークンを使用します)。非セキュア・ポート 1883 に MQTT メッセージングを行うとこれらの資格情報が非暗号化テキストで送信されるため、代わりにセキュアな代替ポート 8883 または 443 を必ず使用してください。セキュア・ポートを介して送信される場合、TLS 資格情報は必ず暗号化されます。Python MQTT ライブラリーの tls_set() メソッドを使用して、アプリケーションで忘れずに TLS を有効にしてください。そうしないと、データが保護されずに送信される可能性があります。

ポート 8883 または 443 でセキュアな MQTT メッセージングを使用すると、今までより新しいクライアント・ライブラリーは {{site.data.keyword.iot_short_notm}} によって提供される証明書を自動的に信頼します。クライアント環境がこれに該当しない場合、[messaging.pem](https://github.com/ibm-messaging/iot-python/blob/master/src/ibmiotf/messaging.pem) から完全な証明書チェーンをダウンロードして使用することができます。


## TLS 要件
{: #tls_requirements}

一部の Transport Layer Security (TLS) クライアント・ライブラリーは、ワイルドカードを含むドメインをサポートしません。ライブラリーを正常に変更できない場合は、証明書の検査を無効にしてください。

TLS 要件は、MQTT プロトコルと HTTP プロトコルのどちらを使用して {{site.data.keyword.iot_short_notm}} に接続しているかによって異なります。以下のセクションに、デフォルトのサーバー証明書を使用する場合にサポートされる暗号スイートを示します。独自のクライアント証明書を使用する場合、サポートされる暗号スイートは、使用する証明書によって異なります。

### MQTT 接続の TLS 要件

{{site.data.keyword.iot_short_notm}} には、TLS v1.2 と以下の暗号スイートが必要です。


- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_256_GCM_SHA384

### HTTP 接続の TLS 要件

デフォルトのサーバー証明書を使用している場合、{{site.data.keyword.iot_short_notm}} では、TLS v1、TLS v1.1、または TLS v1.2 と、以下の暗号スイートが必要です。


- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_256_GCM_SHA384


## MQTT クライアント認証
{: #mqtt_authentication}

**重要:** MQTT クライアントごとに固有のクライアント ID が必要です。既に接続済みのクライアント ID を使用して組織内のクライアントを接続しようとすると、最初の接続が切断されます。

デバイスとゲートウェイが {{site.data.keyword.iot_short_notm}} に直接接続している場合、それらが接続されていることを示す状況アイコンがダッシュボードに表示されます。デバイスがゲートウェイを介して間接的に接続している場合は、ゲートウェイ経由で接続しているデバイスをダッシュボードが認識しないため、そのデバイスは切断されていると表示されます。

### MQTT クライアント ID

デバイス、アプリケーション、ゲートウェイが正常に認証されるようにするため、次のクライアント ID と形式を使用して各 MQTT クライアントを定義します。

|クライアント・タイプ |ID|MQTT ID 形式|
|:---|:---|:---|
|アプリケーション|a|<pre class="pre">a:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|スケーラブルなアプリケーション|A|<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|デバイス|d|<pre class="pre">d:<var class="keyword varname">orgId</var>:<var class="keyword varname">deviceType</var>:<var class="keyword varname">deviceId</var></pre>|
|ゲートウェイ|g|<pre class="pre">g:<var class="keyword varname">orgId</var>:<var class="keyword varname">typeId</var>:<var class="keyword varname">deviceId</var></pre>|

各部の意味は、次のとおりです。
- *orgId* は、サービスを登録したときに生成された 6 文字の固有の組織 ID です。
- *appId* は、クライアント固有のユーザー定義ストリング ID です。
- *deviceId* は、すべてのタイプを対象とする、デバイスまたはゲートウェイを一意に識別するための ID で、シリアル番号のようなものです。
- *device_type* は、接続中のデバイスのタイプを表す識別子で、型式番号のようなものです。
- *typeId* は、接続中のゲートウェイのタイプを表す識別子で、型式番号のようなものです。

*appId*、*type_id*、*device_type*、*device_id* の値は、36 文字以下でなければなりません。以下の文字だけを含めることができます。
- 英数字 (a-z、A-Z、0-9)
- ダッシュ ( - )
- 下線 ( _ )
- ドット ( . )

**注:**
- Quickstart サービスに接続すると、認証は不要になります。
- 接続する前にアプリケーションを登録する必要はありません。


### MQTT を使用したアプリケーションの接続

{{site.data.keyword.iot_short_notm}} アプリケーションでは、組織への接続に API キーを必要とします。API キーを登録するとトークンが生成されます。このトークンはこの API キーとともに使用する必要があります。

以下に、API キーのコードの例を示します。

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}

以下に、標準的な認証トークンの例を示します。

```
 MP$08VKz!8rXwnR-Q*
```

API キーを使用して MQTT 接続を行うときには、以下の要件を満たしていることを確認してください。

- MQTT クライアント ID が次の形式である。a:*orgId*:*appId*
- MQTT ユーザー名が API キーである。例、a-*orgId*-a84ps90Ajs
- MQTT パスワードが認証トークンである。例、*MP$08VKz!8rXwnR-Q*

詳しくは、[アプリケーションの MQTT 接続](../../applications/mqtt.html)を参照してください。

### デバイス認証

#### ユーザー名
{{site.data.keyword.iot_short_notm}} サービスは、デバイスに対するトークン・ベースの認証のみをサポートします。そのため、各デバイスの有効なユーザー名は 1 つだけとなります。
値を `use-token-auth` にすると、ゲートウェイまたはデバイスの認証トークンが MQTT 接続のパスワードとして使用されることをサービスに対して指示することになります。

詳しくは、[デバイスの MQTT 接続](../../devices/mqtt.html)を参照してください。

#### パスワード
クライアントがトークン・ベースの認証を使用している場合は、デバイス認証トークンをすべての MQTT 接続のパスワードとして送信してください。
