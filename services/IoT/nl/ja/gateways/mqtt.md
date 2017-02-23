---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# ゲートウェイの MQTT 接続
{: #mqtt}

MQTT は、デバイスとアプリケーションが {{site.data.keyword.iot_full}} と通信するために使用する主要なプロトコルです。MQTT クライアントをゲートウェイとして使用してデバイスを {{site.data.keyword.iot_short_notm}} に接続する際に役立つクライアント・ライブラリー、情報、サンプルが提供されています。
{:shortdesc}

## クライアント接続
{: #client_connections}

クライアント・セキュリティーの詳細と、MQTT クライアントをゲートウェイとして接続する方法については、[{{site.data.keyword.iot_short_notm}} へのアプリケーション、デバイス、ゲートウェイの接続](../reference/security/connect_devices_apps_gw.html)を参照してください。

## MQTT 認証
{: #authentication}
ゲートウェイやデバイスでは、{{site.data.keyword.iot_short_notm}} は MQTT トークン・ベース認証を使用します。

MQTT 認証を有効にするには、MQTT 接続を行う際にユーザー名とパスワードをサブミットします。

### ユーザー名
{: #username}

ユーザー名は、すべてのゲートウェイで同じ値 `use-token-auth` です。この値により、{{site.data.keyword.iot_short_notm}} はゲートウェイの認証トークンを使用するようになります。これは、パスワードとして指定されます。

### パスワード
{: #password}

各ゲートウェイのパスワードは、ゲートウェイが {{site.data.keyword.iot_short_notm}} に登録されたときに生成される固有の認証トークンです。

## イベントのパブリッシュ
{: #pub_events}

ゲートウェイは、ゲートウェイ自体のイベントをパブリッシュすることも、ゲートウェイを経由して接続しているデバイスの代わりにイベントをパブリッシュすることもできます。イベントをパブリッシュするには、以下のトピックを使用し、イベントの対象の起点に基づいて、適切な `typeId` と `deviceId` に置換します。

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/evt/<var class="keyword varname">eventId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}


**例**


|    |'typeID'|'deviceID'|
|:---|:---|:---|
|ゲートウェイ 1 |mygateway |gateway1 |
|デバイス 1 |mydevice |device1 |

-   ゲートウェイ 1 は、それ自体の状況イベントをパブリッシュすることができます。
      
    `iot-2/type/mygateway/id/gateway1/evt/status/fmt/json`
-   ゲートウェイ 1 は、デバイス 1 に代わって状況イベントをパブリッシュすることができます。
      
    `iot-2/type/mydevice/id/device1/evt/status/fmt/json`

**重要:** メッセージ・ペイロードは最大 131072 バイトに制限されます。この制限を超えるメッセージは拒否されます。

### 保存メッセージ
{{site.data.keyword.iot_short_notm}} 組織には、保存された MQTT メッセージをパブリッシュする権限がありません。ゲートウェイが保存メッセージを送信すると、{{site.data.keyword.iot_short_notm}} サービスは、保存メッセージのフラグが true に設定されている場合でもそのフラグをオーバーライドし、そのフラグが false に設定されている場合と同じ要領でメッセージを処理します。

## コマンドへのサブスクライブ
{: #subscribing_cmds}

ゲートウェイは、ゲートウェイ自体で指定されるコマンドにサブスクライブすることも、組織内の任意のデバイス (他のゲートウェイを含む) にサブスクライブすることもできます。コマンドにサブスクライブするには、以下のトピックを使用し、適切な `typeId` と `deviceId` に置換します。

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/cmd/<var class="keyword varname">commandId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}

`typeId`、`deviceId`、`commandId`、`formatString` で MQTT `+` ワイルドカードを使用して、複数のコマンド・ソースにサブスクライブできます。

**例:**

|デバイス |`typeId`|`deviceId`|
|:---|:---|
|ゲートウェイ 1| mygateway   | gateway1   |
|デバイス 1 | mydevice    | device1    |


-   ゲートウェイ 1 は、ゲートウェイで指定されたコマンドにサブスクライブすることができます。
      
    `iot-2/type/mygateway/id/gateway1/cmd/+/fmt/+`
-   ゲートウェイ 1 は、デバイス 1 に送信されるコマンドにサブスクライブすることができます。
      
    `iot-2/type/mydevice/id/device1/cmd/+/fmt/+`
-   ゲートウェイ 1 は、タイプ `mydevice` のデバイスに送信される任意のコマンドにサブスクライブすることができます。
       
     `iot-2/type/mydevice/id/+/cmd/+/fmt/+`

**重要:** `cleansession=false` として指定されている MQTT 持続セッションは、ゲートウェイに接続するデバイスを検索しません。デバイスがゲートウェイ A に接続し、その後にゲートウェイ B に接続した場合、デバイスが切断されている間にデバイス宛てにゲートウェイ A に対してパブリッシュされたメッセージを、ゲートウェイは受け取りません。ゲートウェイが所有するのは、ゲートウェイに接続されたデバイスではなく、MQTT クライアントとサブスクリプションです。

## ゲートウェイの自動登録
{: #auto-reg}

ゲートウェイ・デバイスは、接続されているデバイスを自動的に登録できます。ゲートウェイがメッセージをパブリッシュするか、未登録デバイスに代わってトピックにサブスクライブすると、そのデバイスは自動的に登録されます。

ゲートウェイ・デバイスからの登録要求は、保留中の要求が一度に 128 個を超えないように絞られます。多くの新規デバイスを接続しようとすると、ゲートウェイ経由でのデバイスの登録が遅れる可能性があります。

**警告**

ゲートウェイがデバイスの自動登録に失敗した場合、ゲートウェイは少しの間そのデバイスの登録を再試行しません。その間、失敗したデバイスからのメッセージやサブスクリプションはすべてドロップされます。

## ゲートウェイ通知
{: #notification}

パブリッシュ・トピックまたはサブスクライブ・トピックの検証中、あるいは自動登録中にエラーが発生した場合は、ゲートウェイ・デバイスに通知が送信されます。ゲートウェイは、`typeId` 値と `deviceId` 値を置換して、以下のトピックにサブスクライブすることにより、これらの通知を受け取ることができます。

```
iot-2/type/**typeId**/id/**deviceId**/notify
```
<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/notify</pre>
{: codeblock}

通知トピックで受け取るメッセージでは、次の形式が使用されます。

```   
{
   "Request": "<Request_Type>",
   "Time": "<Timestamp>",
   "Topic": "<Topic>",
   "Type": "<Device_Type>",
   "Id": "<Device_Id>",
   "Client": "<Client_ID>",
   "RC": "<Return_Code>",
   "Message": "<Message>"
}
```
説明
-   `Request_Type` 値は、`publish` か `subscribe` のいずれかです
-   `Timestamp` は、ISO 8601 形式の時刻です
-   `Topic` は、ゲートウェイからの要求トピックです
-   `Device_Type` は、トピックからのデバイス・タイプです
-   `Device_Id` は、トピックからのデバイス ID です
-   `Client_ID` は、要求のクライアント ID です
-   `Return_Code` は、戻りコードです
-   `Message` は、エラー・メッセージです

ゲートウェイは、以下の通知を受け取ることがあります。

-   トピックは許可されたどのトピック・ルールとも一致しません。
-   デバイス・タイプが無効です。
-   デバイス ID が無効です。
-   ゲートウェイあたりのデバイスの最大数に達しています。
-   組織でのデバイスの最大数に達しています。
-   内部エラーのためにデバイスを作成できませんでした。

## 管理対象ゲートウェイ
{: #managed_gateways}

デバイス・ライフサイクル管理のサポートはオプションです。{{site.data.keyword.iot_short_notm}} によって使用されるデバイス管理プロトコルは、ゲートウェイがイベント/コマンド制御で使用するものと同じ MQTT 接続を使用します。

### サービス品質レベルとクリーン・セッション
{: #quality_service}

管理対象ゲートウェイは、サービス品質 (QoS) レベルが 0 か 1 のメッセージをパブリッシュできます。

QoS=0 のメッセージは破棄される可能性があり、メッセージ・サーバーを再始動した後には保持されません。QoS=1 のメッセージはキューに入れられる可能性があり、メッセージ・サーバーを再始動した後にも残ります。要求がキューに入れられるかどうかは、サブスクリプションの耐久性によって異なります。サブスクリプションの耐久性は、サブスクリプションを作成した接続の `cleansession` パラメーターによって決まります。  

{{site.data.keyword.iot_short_notm}} は、メッセージのキューイングをサポートするために QoS レベルが 1 の要求をパブリッシュします。管理対象ゲートウェイが接続されていなかった間に送信されるメッセージをキューに入れるには、`cleansession` パラメーターを false に設定することにより、デバイスがクリーン・セッションを使用しないようデバイスを構成します。

**警告**

管理対象ゲートウェイが永続サブスクリプションを使用する場合、要求がタイムアウトになる前にデバイスがサービスに再接続しなければ、オフラインの間にゲートウェイに送信されるデバイス管理コマンドは、失敗した操作として報告されます。ゲートウェイが再接続すると、それらの要求はゲートウェイによって処理されます。永続サブスクリプションは、`cleansession=false` パラメーターによって指定されます。

ゲートウェイは、その背後にあるデバイスに関係なく、MQTT セッションを所有します。デバイスがゲートウェイを経由してサブスクリプション要求を送信する際、`cleansession=false` オプションが設定されているかどうかに関係なく、要求はその他のゲートウェイにローミングしません。

### トピック
{: #topics}

管理対象ゲートウェイは、{{site.data.keyword.iot_short_notm}} からの要求と応答を処理するために、以下のトピックにサブスクライブする必要があります。

-   管理対象ゲートウェイは、以下のデバイス管理応答にサブスクライブします。  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/+</pre>
{: codeblock}
-   管理対象ゲートウェイは、以下のデバイス管理要求にサブスクライブします。  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/+</pre>
{: codeblock}

管理対象ゲートウェイは、以下の応答と要求をパブリッシュします。

- デバイス管理応答は、以下でパブリッシュされます。  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/</pre>
{: codeblock}
- デバイス管理要求は、以下でパブリッシュされます。  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/</pre>
{: codeblock}

ゲートウェイは、適切な **typeId** と **deviceId** を使用して、ゲートウェイ自体のデバイス管理プロトコル・メッセージを処理することも、接続している他のデバイスの代わりにデバイス管理プロトコル・メッセージを処理することもできます。

### メッセージ形式
{: #msg_format}

すべてのメッセージは JSON 形式で送信されます。

**要求**

要求は、以下のコード・サンプルで示されるように形式設定されます。

```   
    {  "d": {...}, "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056" }
```

-   `d` は、要求に関連したデータを運びます
-   `reqId` は、要求の ID であり、応答にコピーする必要があります。応答が不要な場合は、このフィールドは使用されません。

**応答**

応答は、以下のコード・サンプルで示されるように形式設定されます。

```
    {
        "rc": 0,
        "message": "success",
        "d": {...},
        "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056"
    }
```
説明:
-   `rc` は、元の要求の結果コードです。
-   `message` は、オプション要素で、応答コードのテキスト記述が入ります。
-   `d` は、応答が伴うオプションのデータ要素です。
-   `reqId` は、元の要求の要求 ID です。要求 ID を使用して応答を要求と相関させることができるため、デバイスですべての要求 ID が固有になるようにする必要があります。{{site.data.keyword.iot_short_notm}} 要求に対する応答には、正しい `reqId` 値を含める必要があります。
