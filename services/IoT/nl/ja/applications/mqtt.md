---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# アプリケーションの MQTT 接続
{: #mqtt}

MQTT は、デバイスとアプリケーションが {{site.data.keyword.iot_full}} と通信するために使用する主要なプロトコルです。{{site.data.keyword.iot_short_notm}} アプリケーションの接続と統合に役立つように、クライアント・ライブラリー、情報、サンプルが用意されています。
{:shortdesc}

## クライアント接続
{: #client_connections}

クライアントのセキュリティーや、{{site.data.keyword.iot_short_notm}} でアプリケーションに MQTT クライアントを接続する方法については、[{{site.data.keyword.iot_short_notm}} へのアプリケーション、デバイス、ゲートウェイの接続](../reference/security/connect_devices_apps_gw.html)を参照してください。

## MQTT 認証
{: #mqtt_authentication}

{{site.data.keyword.iot_short_notm}} アプリケーションでは、組織への接続に API キーを必要とします。API キーを登録すると認証トークンが生成されます。このトークンはこの API キーとともに使用する必要があります。

以下に、標準的な API キーの例を示します。

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}


以下に、標準的な認証トークンの例を示します。

```
MP$08VKz!8rXwnR-Q*
```

API キーを使用して MQTT 接続を行うときには、以下のガイドラインが適用されていることを確認してください。

- MQTT クライアント ID が次の形式である。a:*orgId*:*appId*
- MQTT ユーザー名が API キーである (例: a-*orgId*-a84ps90Ajs)
- MQTT パスワードが認証トークンである (例: MP$08VKz!8rXwnR-Q*)


## デバイス・イベントのパブリッシュ
{: #publishing_device_events}

アプリケーションは、次のように、登録デバイスからパブリッシュされたかのようにイベントをパブリッシュすることができます。

-  Publish to topic iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

デバイスの既存のデータを {{site.data.keyword.iot_short_notm}} に送信するには、そのデータを処理して {{site.data.keyword.iot_short_notm}} にパブリッシュするアプリケーションを作成します。

**重要:** メッセージ・ペイロードは最大 131072 バイトに制限されます。この制限値を超えるメッセージは拒否されます。

### 保存メッセージ
{{site.data.keyword.iot_short_notm}} 組織には、保存された MQTT メッセージをパブリッシュする権限がありません。アプリケーション、ゲートウェイ、またはデバイスが保存メッセージを送信する場合、{{site.data.keyword.iot_short_notm}} サービスは、保存メッセージ・フラグが true に設定されている場合にそれをオーバーライドして、フラグが false に設定されている場合と同様の方法でメッセージを処理します。

## デバイス・コマンドのパブリッシュ
{: #publishing_device_commands}

アプリケーションは、次のように、登録デバイスにコマンドをパブリッシュできます。

-  Publish to topic iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

## デバイス・イベントのサブスクライブ
{: #subscribe_device_events}

アプリケーションは、次のように、1 つ以上のデバイスのイベントをサブスクライブできます。

-  Subscribe to topic iot-2/type/*device_type*/id/*device_id*/evt/*event_id*/fmt/*format_string*

**注:**  複数のタイプのイベントまたは複数のデバイスからのイベントにサブスクライブするには、次のいずれかのコンポーネントに、MQTT で「あらゆる」を意味するワイルドカード文字 (+) を使用します。

- device_type
- device_id
- event_id
- format_string

## デバイス・コマンドのサブスクライブ
{: #subscribe_device_commands}

アプリケーションは、1 つ以上のデバイスに送信されたコマンドをサブスクライブできます。次に例を示します。

-  Subscribe to topic iot-2/type/*device_type*/id/*device_id*/cmd/*command_id*/fmt/*format_string*

**注:**  複数のタイプのイベントまたは複数のデバイスからのイベントにサブスクライブするには、次のいずれかのコンポーネントに、MQTT で「あらゆる」を意味するワイルドカード文字 (+) を使用します。

-  device_type
-  device_id
-  cmd_id
-  format_string

## デバイス状況メッセージのサブスクライブ
{: #subscribe_device_status}

アプリケーションは、1 つ以上のデバイスの状況をサブスクライブしてモニターできます。次に例を示します。

-  Subscribe to topic iot-2/type/*device_type*/id/*device_id*/mon

**注:** 複数のデバイスからの更新にサブスクライブするには、次のいずれかのコンポーネントに、MQTT で「あらゆる」を意味するワイルドカード文字 (+) を使用します。

- device_type
- device_id

## アプリケーション状況メッセージのサブスクライブ
{: #subscribe_app_status}

アプリケーションは、1 つ以上のアプリケーションの状況をサブスクライブしてモニターできます。次に例を示します。

- Subscribe to topic iot-2/app/*appId*/mon

**注:** すべてのアプリケーションからの更新にサブスクライブするには、*appId* コンポーネントに、MQTT で「あらゆる」を意味するワイルドカード文字 (+) を使用します。


## Quickstart に関する制約事項
{: #quickstart_restrictions}
Quickstart サービスで使用するアプリケーション・コードを作成する場合、Quickstart では、次の機能はサポートされません。

- コマンドのパブリッシュ
- コマンドへのサブスクライブ
- **deviceType** コンポーネントまたは **appId** コンポーネントに MQTT の「any」のワイルドカード文字 (+) を使用すること
- Transport Layer Security (TLS) による MQTT 接続
- スケーラブルなアプリケーション

## スケーラブルなアプリケーション
{: #scalable_apps}

アプリケーション接続の方法を調整し、複数のアプリケーション・インスタンス間でイベント・メッセージ処理のロード・バランシングを行うことで、{{site.data.keyword.iot_short_notm}} アプリケーションのスケーラビリティーを向上させることができます。

ロード・バランシングとスケーラビリティーを最適化するために必要なクライアント数は、デプロイメントによって異なります。最適なクライアント数を決定するには、システムに対するストレス・テストが必要です。

スケーラブルなアプリケーションは、非永続サブスクリプションまたは永続性混在の共有サブスクリプション (ベータ) のいずれかとして定義されます。

### 非永続サブスクリプション
{: #shared_sub_non_durable}

ロード・バランシングを有効にする場合は、アプリケーション・サブスクリプションを非永続サブスクリプションに設定し、サブスクリプション内のクライアント ID が次の形式になるようにしてください。

<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
{: codeblock}

各部の意味は以下のとおりです。
-  文字 **A** は、クライアントがスケーラブルなアプリケーションであることを示します。
-  *orgId* は、サービスを登録したときに生成された 6 文字の固有の組織 ID です。
-  *appId* は、クライアント固有のユーザー定義ストリング ID です。この文字列に含めることができるのは、英数字 (a から z、A から Z、0 から 9)、特殊文字のダッシュ (-)、アンダースコアー (_)、ドット (.) のみです。


**重要:**
- {{site.data.keyword.iot_short_notm}} でスケーラブルなアプリケーションとして正しく指定されるように、クライアント ID の先頭は大文字 **A** にする必要があります。
- スケーラブルなアプリケーションに含まれる他のクライアントでも、同じクライアント ID を使用する必要があります。
- 非永続サブスクリプションでは、クリーン・セッション値を false (0) に設定する必要があります。

### 耐久性混合共有サブスクリプション
{: #shared_sub_mixed}

{{site.data.keyword.iot_short_notm}} サービスでは、永続性混在の共有サブスクリプションをサポートするように MQTT V3.1.1 メッセージ・プロトコル仕様が拡張されています。共有サブスクリプションでは、アプリケーションのロード・バランシングを実行できます。バックエンドのエンタープライズ・アプリケーションが、特定のトピック・スペースにパブリッシュされたメッセージの量を処理できない場合などに、共有サブスクリプションが必要になります。例えば、単一アプリケーションで処理するメッセージを多数のデバイスがパブリッシュする場合は、共有サブスクリプションのロード・バランシング機能を使用する必要があるでしょう。

永続性混在の共有サブスクリプションでは、サブスクリプション内のクライアント ID が次の形式になるようにしてください。

<pre class="pre">A:<var class="keyword varname">org</var>:<var class="keyword varname">appId</var>:<var class="keyword varname">instanceId</var></pre>
{: codeblock}

各部の意味は以下のとおりです。
- クライアント ID 内の文字 **A**、*orgId*、および *appId* は、[非永続サブスクリプション](#shared_sub_non_durable)と同じ方法で定義されます。
- *instanceID* は、36 文字以下のストリングでなければなりません。また、以下の文字だけを含めることができます。
   - 英数字 (a-z、A-Z、0-9)
   - ダッシュ ( - )
   - 下線 ( _ )
   - ドット ( . )

**重要:**
- 永続性混在の共有サブスクリプションでは、クリーン・セッション値を true (1) または false (0) のいずれかに設定できます。
- instanceId を使用して接続するクライアントは、instanceId を使用しないで接続するクライアントとは異なるサブスクリプションを使用します。そのため、永続性混在の共有サブスクリプションで複数のクライアントを接続するためには、すべてのサブスクリプションで instanceID を指定する必要があります。

**サンプル・シナリオ**

次のシナリオは、{{site.data.keyword.iot_short_notm}} で非永続のスケーラブルなアプリケーションを利用する一例です。

- クライアント 1 は、**A:abc123:myApplication** として接続し、すべてのデバイス・イベントをサブスクライブします。つまり、クライアント 1 は、パブリッシュされるデバイス・イベントの 100% を受信します。
- クライアント 2 も、**A:abc123:myApplication** として接続し、すべてのデバイス・イベントにサブスクライブします。つまり、クライアント 1 とクライアント 2 の両方の間で、パブリッシュされたすべてのイベントが共有されます。処理の負荷が、クライアント 1 とクライアント 2 の間で共有されます。
- クライアント 3 も、**A:abc123:myApplication** として接続し、すべてのデバイス・イベントにサブスクライブします。つまり、クライアント 1、クライアント 2、クライアント 3 のすべての間で、イベントの処理負荷が共有されます。
- その後、クライアント 2 とクライアント 3 がすべてのデバイス・イベントをアンサブスクライブしました。つまり、クライアント 1 のみが、パブリッシュされるすべてのデバイス・イベントを受信します。クライアント 2 とクライアント 3 はまだサービスに接続されていますが、パブリッシュされるデバイス・イベントは、クライアント 1 が 100% 受信します。
- 複数のアプリケーションで 1 つのサブスクリプションを共有する場合は、メッセージが送信順に届かないことがあります。例えば、メッセージ A が最初に送信されたのに、メッセージ A がクライアント 2 に届く前に、メッセージ B がクライアント 1 に届く場合があります。
