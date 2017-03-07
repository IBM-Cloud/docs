---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.messagehub}} を使用したヒストリアン・サービスの接続と構成  
{: #messagehub_main}

{{site.data.keyword.messagehub_full}} を {{site.data.keyword.iot_short}} に接続すると、履歴データ・ストレージ用のスケーラブルで高スループットのメッセージ・バスが提供されます。{{site.data.keyword.messagehub}} は Apache Kafka で作成されています。これは、リアルタイムでデータ・フィードを扱うための待ち時間の少ないプラットフォームを提供する、オープン・ソースの高スループット・メッセージング・システムです。

## 始めに  
{: #byb}

{{site.data.keyword.messagehub}} を {{site.data.keyword.iot_short}} サービスに接続する前に、以下のタスクを完了してください。

- {{site.data.keyword.Bluemix_notm}} カタログを使用して、{{site.data.keyword.iot_short_notm}} と同じ {{site.data.keyword.Bluemix_notm}} スペースに {{site.data.keyword.messagehub}} をセットアップします。{{site.data.keyword.messagehub}} について詳しくは、[{{site.data.keyword.messagehub}} の概説](https://console.{DomainName}/docs/services/MessageHub/index.html)を参照してください。

- {{site.data.keyword.Bluemix_notm}} 組織で開発者特権を持っていることと、{{site.data.keyword.Bluemix_notm}} を介してサインインしていることを確認してください。{{site.data.keyword.Bluemix_notm}} を介してサインインしていないか、この {{site.data.keyword.Bluemix_notm}} 組織で開発者特権を持っていない場合、{{site.data.keyword.messagehub}} や {{site.data.keyword.iot_short_notm}} のバインディングを許可することはできません。

## 接続

履歴データ・ストレージの {{site.data.keyword.messagehub}} を接続するには、以下のようにします。

1. {{site.data.keyword.iot_short}} ダッシュボードで、ナビゲーション・バーの**「拡張」** をクリックします。
2. 履歴データ・ストレージ・タイルで、**「セットアップ」**をクリックします。
4. 接続する {{site.data.keyword.messagehub}} サービスを選択します。
  
{{site.data.keyword.iot_short}} サービスと同じ {{site.data.keyword.Bluemix_notm}} スペース内のすべての {{site.data.keyword.messagehub}} サービスは、履歴データ・ストレージの構成セクションにリストされます。
5. {{site.data.keyword.messagehub}} 構成オプションを選択します。
 1. タイム・ゾーンを選択します。
   
{{site.data.keyword.messagehub}} に送信されるデバイス・データのタイム・スタンプは、選択されたタイム・ゾーンに変換されます。
 2. デフォルトのトピックを選択します。
   
デフォルトのトピックがここで定義されている場合、デバイス・イベントがそのトピックに送信されます。より細かいトピックの割り当てを使用する場合、デフォルトのトピックをブランクのままにし、カスタム転送ルールを追加します。
 3. オプション: カスタム転送ルールを指定します。
   
デバイス・イベントを転送するための追加ルールを指定します。カスタム転送ルールと一致するイベントのみが転送されます。
   
 **注:** イベントは、複数の転送規則と一致して、複数の {{site.data.keyword.messagehub}} トピックに転送される可能性があります。
 4. オプション: トピックを構成します。
   
デフォルトの 2 つより多くのパーティションを持つトピックを作成するには、パーティション構成を指定することができます。
 5. **「完了」**をクリックします。
5. **「Authorize」**をクリックします。
6. 「許可 (Authorization)」ダイアログ・ボックスで、**「確認」**をクリックします。

これで、デバイス・データが {{site.data.keyword.messagehub}} に保管されます。
