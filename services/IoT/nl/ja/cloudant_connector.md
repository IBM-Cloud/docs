---

copyright:
  years: 2016
lastupdated: "2016-09-16"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.cloudant_short_notm}} を使用したヒストリアン・サービスの接続と構成  
{: #cloudant_main}

{{site.data.keyword.cloudantfull}} サービスを {{site.data.keyword.iot_full}} に接続することによって、デバイス・データの保管とアクセスが可能になります。デバイス・データは、選択されたバケット間隔に従って、毎日、毎週、または毎月データベースに保管されます。

{{site.data.keyword.cloudant_short_notm}} を使用してデバイス・データの保管を開始するとき、3 つのデータベースが自動的に作成されます。1 つのデータベースは現在のバケット間隔に対して作成され、1 つのデータベースは後続の間隔に対して作成され、もう 1 つは構成データベースとして作成されます。設計文書は、構成データベースに追加することができ、作成時に新規データベースにコピーされます。間隔の終わりに到達すると、新しい間隔に対してデバイス・データがバケット・データベースに保管され、後続の間隔に対して新規データベースが作成されます。

デバイス・データがデータベースに送信されたら、次の 2 つの方法のいずれかで保管できます。データが有効な JSON であり、デバイス・イベントの形式が `JSON` に設定されている場合、デバイス・データは以下の形式で保管されます。

```json

{
  "_id": "78bf4380-3311-11e6-a747-d7b140d1a70a",
  "_rev": "2-d13912b7c089f060a4ba7369fa86e46f",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "json_payload",
  "format": "json",
  "timestamp": "2016-06-15T16:54:41.464+01",
  "data": {
    "a": 22
  }
}

```

デバイス・データが有効な JSON でないか、形式が `JSON` に設定されていない場合、デバイス・データは、`payload` フィールドの下に Base64 エンコード・ストリングとして以下の形式で保管されます。

```json

{
  "_id": "80f1ce10-3311-11e6-a747-d7b140d1a70a",
  "_rev": "1-bfcbf1e74389fe4188a9425c0cd2575a",
  "payload": "eHh4eHg=",
  "typeId": "t",
  "deviceType": "0",
  "eventType": "non_json_payload",
  "format": "notjson",
  "timestamp": "2016-06-15T16:54:55.217+01"
}

```

## 始めに  
{: #byb}

{{site.data.keyword.cloudant_short_notm}} を {{site.data.keyword.iot_short}} サービスに接続する前に、以下のタスクを完了してください。

- Bluemix カタログを使用して、{{site.data.keyword.iot_short_notm}} と同じ Bluemix スペースに {{site.data.keyword.cloudant_short_notm}} をセットアップします。

Bluemix 組織で開発者特権を持っていることと、Bluemix を介してサインインしていることを確認してください。Bluemix を介してサインインしていないか、この Bluemix 組織で開発者特権を持っていない場合、{{site.data.keyword.cloudant_short_notm}} や {{site.data.keyword.iot_short_notm}} のバインディングを許可することはできません。

{{site.data.keyword.cloudant_short_notm}} を接続するには、以下の手順を実行します。

1. {{site.data.keyword.iot_short}} ダッシュボードで、ナビゲーション・バーの**「拡張」** をクリックします。
2. 履歴データ・ストレージ・タイルで、**「セットアップ」**をクリックします。
2. {{site.data.keyword.iot_short}} サービスと同じ Bluemix スペース内のすべての {{site.data.keyword.cloudant_short_notm}} サービスは、履歴データ・ストレージの構成セクションにリストされます。
3. 接続する {{site.data.keyword.cloudant_short_notm}} サービスを選択します。
4. {{site.data.keyword.cloudant_short_notm}} 構成オプションを選択します。

  a. バケット間隔を選択します。バケット間隔は、デバイス・データを保管するために新規データベースを作成する頻度を制御します。新規バケットは、選択したバケット間隔を使用して、選択したタイム・ゾーンの午前 0 時に作成されます。

  b. タイム・ゾーンを選択します。デバイスにローカルな時刻ではなく、選択したタイム・ゾーンの時刻が、配置するバケット・デバイス・データを決定するために使用されます。{{site.data.keyword.cloudant_short_notm}} に送信されるデバイス・データのタイム・スタンプは、データが配置されるデータベースを決定するときに、選択したタイム・ゾーンに変換されます。

  c. データベース名を設定するためのオプションを選択します。データベース名は、`iotp_<orgID>_<dbname>_<bucket_name>` という形式で、それぞれの意味は次のとおりです。

 +  * `<orgID>` は、組織 ID です。
 +  * `<dbname>` は、`「データベース名」`フィールドで制御するデータベース名のこの部分の選択項目です。
 +  * `<bucket_name>` は、`「バケット間隔」`フィールドの選択項目によって決まるストリングです。
 +    * バケット間隔が`「日」`の場合、`<bucket_name>` は `yyyy-mm-dd` になります。例えば、2016 年 7 月 6 日のイベントであれば `2016-07-06` です。
 +    * バケット間隔が`「週」`の場合、`<bucket_name>` は `yyyy-'w'ww` になります (`'w'ww` は週の番号)。例えば、2016 年の第 3 週のイベントであれば `2016-w03` です。
 +    * バケット間隔が`「月」`の場合、`<bucket_name>` は `yyyy-mm` になります。例えば、2016 年 7 月のイベントであれば `2016-07` です。

5. **「Authorize」**をクリックします。
6. 許可ダイアログ・ボックスの**「Confirm」**をクリックします。

これで、デバイス・データが {{site.data.keyword.cloudant}} に保管されます。

## 設計文書の新規作成  
{: #design_docs}

新規設計文書は、構成データベースに入れられ、作成された各データベースにコピーされます。構成データベース名は、`iotp_<orgid>_<choice>_configuration
` であり、『開始する前に』セクションの手順 3b で説明されているデータベース名と同じパラメーターを使用します。

{{site.data.keyword.iot_short_notm}} に含まれているデフォルトの設計文書は、要約機能とは別に、現在のヒストリアンで使用可能なクエリーを実装します。

設計文書を構成データベースにさらに追加することができます。それらの設計文書は、作成時に新規バケット間隔データベースにコピーされます。設計文書を構成データベースに追加する場合は、[Cloudant API の資料](https://docs.cloudant.com/document.html)を参照してください。

<!--  # Related links
{: #rellinks}
* [Querying your {{site.data.keyword.cloudant_short_notm}}](link) -->
