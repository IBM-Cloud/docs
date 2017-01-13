---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 外部サービスの統合
{: #ref-index}

外部サービスの統合は、{{site.data.keyword.iot_full}} 組織内で、サード・パーティーまたは外部サービスからデータや操作にアクセスするためのものです。

## Jasper
{: #jasper}

Jasper は SIM デバイスの管理プラットフォームです。Jasper は {{site.data.keyword.iot_short_notm}} ダッシュボードに統合されているため、{{site.data.keyword.iot_short_notm}} 組織のダッシュボードにより Jasper デバイスを管理することが可能です。

### Jasper でサポートされる操作

当社のプラットフォームで提供されている組み込み Jasper 統合では、以下の Jasper 操作がサポートされます。

- 全体的な Jasper データの表示。
  - 表示されるのは、状況、料金プラン、過去 1 カ月間のデータ使用状況、過去 1 カ月間の SMS 使用状況、過去 1 カ月間のボイス使用状況、超過限度、追加日付、そして変更日付です。
- SIM アクティベーション状態の変更。
  - インベントリー、アクティベーション準備完了、アクティブ、非アクティブ、廃止から選択します。
- SIM 使用状況の表示。
  - 表示されるのは、サイクル開始日、請求対象と合計データ、請求対象と合計 SMS、請求対象と合計ボイスです。
  - サイクル開始日は YYYY-MM-DD の形式を使用して設定できます。
- SMS から SIM への送信。
- 料金プランの変更

以下に示す構成手順を実行すると、それ以降、Jasper 接続デバイスのデバイス・ドリルダウンの中で、サポートされている操作にアクセスできるようになります。

### Jasper 用の REST API
Jasper 用の REST API にアクセスする場合は、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Jasper_Extension) の資料にある Jasper 拡張のセクションを参照してください。

### Jasper 用の構成

Jasper サービスを {{site.data.keyword.iot_short_notm}} 組織に接続するには、まず実行する必要がある 2 つの構成ステージがあります。まず、{{site.data.keyword.iot_short_notm}} が Jasper サービスに接続されていなければならず、次に {{site.data.keyword.iot_short_notm}} デバイスが構成されていなければなりません。


1. Jasper 拡張を有効にします。Jasper と {{site.data.keyword.iot_short_notm}} 組織の統合を有効にするには、以下の手順を実行します。
  1. {{site.data.keyword.iot_short_notm}} ダッシュボードから、**「拡張」**を選択します。
  2. **「拡張」**ページで、**「拡張の追加 (Add Extension)」**をクリックします。
  3. Jasper の横にある**「追加」**をクリックします。
  4. Jasper ユーザー名、パスワード、アクセス・キー、ドメイン ID を入力します。
  5. **「完了」**をクリックします。

2. デバイスを構成します
{{site.data.keyword.iot_short_notm}} 組織と Jasper アカウントの両方に接続されているデバイスを構成することにより、Jasper からのデータを {{site.data.keyword.iot_short_notm}} ダッシュボードに表示することができます。
**重要:** Jasper 構成を「デバイスの追加」プロセスの一部として適用することはできません。Jasper で構成できるのは、それ以前に接続されているデバイスだけです。
Jasper 接続済みデバイスを構成するには、以下の手順を実行します。
 1. {{site.data.keyword.iot_short_notm}} ダッシュボードのデバイス・タブで、構成する Jasper 接続デバイスを見つけます。
 2. デバイスを選択して、*「デバイス・ドリルダウン (Device Drilldown)」*ビューを開きます。
 3. *「拡張構成」*までスクロールダウンします。
 4. 以下の JSON 形式を使用して拡張の構成を入力した後、**「変更の確認」**をクリックして構成を保存します。  

```json  
    {
        "jasper": {
            "iccid": "string"
        }
    }

```

組織が正常に構成されると、*「デバイス・ドリルダウン (Device Drilldown)」*ビューの*「拡張構成」*セクションに*「拡張」*セクションが表示されます。

## AT&T
{: #att}

### AT&T でサポートされる操作

AT&T 拡張により、以下の AT&T 操作が有効になります。

- 全体的な AT&T データの表示
  - 表示されるのは、状況、料金プラン、過去 1 カ月間のデータ使用状況、過去 1 カ月間の SMS 使用状況、過去 1 カ月間のボイス使用状況、超過限度、追加日付、そして変更日付です。
- SIM アクティベーション状態の変更。
  - インベントリー、アクティベーション準備完了、アクティブ、非アクティブ、廃止から選択します。
- SIM 使用状況の表示。
  - 表示されるのは、サイクル開始日、請求対象と合計データ、請求対象と合計 SMS、請求対象と合計ボイスです。
  - サイクル開始日は YYYY-MM-DD の形式を使用して設定できます。
- SMS から SIM への送信。
- 料金プランの変更

### AT&T 用の REST API
AT&T 用の REST API にアクセスする場合は、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/AT&T_Extension) の資料にある AT&T 拡張のセクションを参照してください。

### AT&T 用の構成

{{site.data.keyword.iot_short_notm}} 組織を AT&T に接続するには、組織の構成とデバイスの構成を完了する必要があります。

{{site.data.keyword.iot_short_notm}} プラットフォームを構成するには、以下の手順を実行します。

1. AT&T 拡張を有効にします。AT&T と {{site.data.keyword.iot_short_notm}} 組織の統合を有効にするには、以下の手順を実行します。
  1. {{site.data.keyword.iot_short_notm}} ダッシュボードから、**「拡張」**を選択します。
  2. **「拡張」**ページで、**「拡張の追加 (Add Extension)」**をクリックします。
  3. AT&T の横にある**「追加」**をクリックします。
  4. AT&T ユーザー名、パスワード、アクセス・キー、ドメイン ID を入力します。
  5. **「完了」**をクリックします。

{{site.data.keyword.iot_short_notm}} 組織と AT&T アカウントを接続するには、まず実行する必要がある 2 つの構成ステージがあります。組織の構成を実行した後、デバイスの構成を実行します。


2. デバイスを構成します
{{site.data.keyword.iot_short_notm}} 組織と AT&T アカウントの両方に接続されているデバイスを構成することにより、AT&T からのデータを {{site.data.keyword.iot_short_notm}} ダッシュボードに表示することができます。
**重要:** AT&T 構成を「デバイスの追加」プロセスの一部として適用することはできません。AT&T で構成できるのは、それ以前に接続されているデバイスだけです。
AT&T 接続済みデバイスを構成するには、以下の手順を実行します。
 1. {{site.data.keyword.iot_short_notm}} ダッシュボードのデバイス・タブで、構成する AT&T 接続デバイスを見つけます。
 2. デバイスを選択して、*「デバイス・ドリルダウン (Device Drilldown)」*ビューを開きます。
 3. *「拡張構成」*までスクロールダウンします。
 4. 以下の JSON 形式を使用して拡張の構成を入力した後、**「変更の確認」**をクリックして構成を保存します。  

```json  
    {
        "atnt": {
            "iccid": "string"
        }
    }

```

組織が正常に構成されると、*「デバイス・ドリルダウン (Device Drilldown)」*ビューの*「拡張構成」*セクションに*「拡張」*セクションが表示されます。

## ARM mbed コネクター
{: #arm}

ARM mbed コネクターを使用して、ARM mbed デバイスを {{site.data.keyword.iot_short_notm}} に接続することができます。ARM mbed 拡張を使用すると、ARM mbed ポータルと {{site.data.keyword.iot_short_notm}} は、ARM mbed ポータルからデータを送受信することができます。

### 構成のセットアップ


1. ARM mbed コネクター拡張を有効にします。ARM mbed コネクター拡張を有効にするには、以下のステップを実行します。
  1. {{site.data.keyword.iot_short_notm}} ダッシュボードから、**「設定」**を選択し、**「拡張」**にナビゲートします。
  2. **「拡張」**メニューで、**「拡張の追加 (Add Extension)」**をクリックします。
  3. ARM mbed コネクター拡張の横にある**「追加」**をクリックします。
  4. ARM mbed アクセス・キーとドメイン ID を入力します。これらは、ARM mbed ポータル (https://connector.mbed.com) を使用して確認できます。
  5. **「接続の確認 (Check Connection)」**ボタンをクリックして、資格情報が正しいことを確認します。
  6. **「完了」**をクリックします。

### ペイロード・フォーマット

ARM mbed プラットフォームでは、通知と非同期応答の 2 種類の着信メッセージがあります。{{site.data.keyword.iot_short_notm}} は、ARM mbed プラットフォームに接続されているデバイスにコマンドを送信することができます。

#### 通知

通知は、デバイスまたはセンサー・データでの変更によって生成されます。{{site.data.keyword.iot_short_notm}} は、メッセージを処理した後、{{site.data.keyword.iot_short_notm}} に直接接続されているデバイスと同じ方法でデバイス・イベント・トピックに送られます。ARM mbed プラットフォームに接続されているデバイスで発生する通知で使用されるイベント・タイプは、`notify` です。

以下のコード・サンプルは、ARM mbed プラットフォーム API によって送信される通知のペイロード形式を示しています。

```
{
  "ep":<endpoint/deviceID>,
  "path":<resource path>,
  "ct":<content type>,
  "payload":<Base64 encoded payload>,
  "max-age":<how long the payload is valid, in seconds>
}
```

#### 非同期応答

ARM mbed プラットフォームに接続されているデバイスに {{site.data.keyword.iot_short_notm}} がコマンドを送信する際、デバイスは、{{site.data.keyword.iot_short_notm}} に確認メッセージを送り戻します。この確認メッセージは*非同期応答*と呼ばれ、イベント・タイプ `asyncResponse` を使用します。

以下のコード・サンプルは、ARM mbed クラウド・サービスによって送信される非同期応答のペイロード形式を示しています。

```
{
  "id":<transaction id>,
  "status":<200 is command was sucessfully executed. Check other HTTP response codes>,
  "ct":<content type>,
  "max-age":<how long the payload is valid, in seconds>,
  "payload":<base64 encoded payload>,
  "ep":<endpoint/deviceID affected by the command>,
  "path":<resource path affected by the command>
}
```

#### ARM mbed プラットフォームへのコマンドの送信

{{site.data.keyword.iot_short_notm}} は、ARM mbed プラットフォームに接続されているデバイスにコマンドを送信することができます。ARM mbed プラットフォームに送信されるコマンドは、以下の JSON 形式を使用する必要があります。

```
{
  "method":<PUT or POST>,
  "deviceId":<endpoint/deviceId>,
  "resourceId":<resource path>,
  "payload": <Base64 encoded payload>
}
```
選択する方式には大/小文字の区別があります。リソース・パスの最初の '/' はスキップする必要があります。


ペイロードは、以下のトピックにパブリッシュする必要があります。

```
iot-2/type/<device_type>/id/<deviceId>/cmd/<command_type>/fmt/<command_format>
```


## Orange
{: #orange}

Orange 拡張を使用すると、Orange SIM カードが取り付けられた {{site.data.keyword.iot_short_notm}} 接続デバイスの SIM カード・データを表示することができます。

https://developer.ibm.com/iotplatform/2016/03/30/watson-iot-platform-integration-with-orange-beta/

### Orange でサポートされる操作

Orange SIM カードを持つ、{{site.data.keyword.iot_short_notm}} サービスに接続されたデバイスがある場合、Orange 拡張を使用することにより、以下の SIM カード・データを表示することができます。

- SIM シリアル番号
- アクティベーション状況
- 最後の状況変更
- 最後の状況リフレッシュ
- ロケーション状況

### Orange 用の REST API
Orange 用の REST API にアクセスする場合は、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Orange_Extension) の資料にある Orange 拡張のセクションを参照してください。

### Orange 用の構成

Orange 拡張を有効にするには、以下のようにします。

1. {{site.data.keyword.iot_short_notm}} ダッシュボードから、**「拡張」**を選択します。
2. **「拡張」**ページで、**「拡張の追加 (Add Extension)」**をクリックします。
3. Orange 拡張の横にある**「追加」**をクリックします。
4. Orange のユーザー名とパスワードを入力します。
6. **「完了」**をクリックします。

Orange 拡張が有効になった後、Orange SIM カードを持つ各デバイスで、Orange SIM データを表示するように構成する必要があります。

1. {{site.data.keyword.iot_short_notm}} ダッシュボードのデバイス・タブで、構成する Orange SIM デバイスを見つけます。
2. デバイスを選択し、*「拡張構成」*までスクロールダウンします。
3. 以下の JSON 形式を使用して拡張の構成を入力した後、**「変更の確認」**をクリックして構成を保存します。

```  
    {
        "orange": {
            "serialnumber": "<serial number of Orange SIM>"
        }
    }

```
組織が正常に構成されると、*「デバイス・ドリルダウン (Device Drilldown)」*ビューの*「拡張構成」*セクションに*「拡張」*セクションが表示されます。

## 履歴データ・ストレージ
{: #historical_data}

履歴データ・ストレージ拡張により、IoT データの [{{site.data.keyword.cloudantfull}}](../../cloudant_connector.html) や [{{site.data.keyword.messagehub_full}}](../../message_hub.html) など、互換性のあるメッセージ・ストレージ・サービスを検索および構成することができます。

## カスタム・デバイス管理パッケージ
{: #device_mgmt}

デバイス管理は {{site.data.keyword.iot_short_notm}} の中核となるフィーチャーですが、追加機能開発のため、拡張することができます。

デバイス管理拡張により、デバイス管理のためのカスタム機能をインストールすることができます。カスタム・デバイス管理機能について詳しくは、[デバイス管理のカスタム拡張](../../devices/device_mgmt/custom_actions.html){: new_window}を参照してください。

## ブロック・チェーン
{: #blockchain}

{{site.data.keyword.iot_short_notm}} でブロック・チェーンを採用すると、IoT デバイスがブロック・チェーンのトランザクションにデータを提供できるようになるので、ブロック・チェーンの変更不能な台帳にデータが格納され、それをスマート・コントラクト・ビジネス・ルールで使用することができます。{{site.data.keyword.iot_short_notm}} は、デバイス・データをブロック・チェーンのスマート・コントラクトで必要なデータ・フォーマットにマップし、それをブロック・チェーン・ファブリックに渡して、ブロック・チェーン台帳に格納されるようにします。

### ブロック・チェーンでサポートされる操作
- デバイス・イベントによってスマート・コントラクト更新をトリガーする。
- スマート・コントラクト・ビジネス・ロジックを実行して、デバイス・イベント・データで台帳状態を更新する。
- モニタリング UI によりブロック・チェーン、トランザクション、台帳状態をモニターする。

### ブロック・チェーン用の構成

{{site.data.keyword.iot_short_notm}} ブロック・チェーン統合は、{{site.data.keyword.iot_short_notm}} でデフォルトではアクティブになっていないサービス・オファリングです。ご使用の環境でこのフィーチャーをアクティブにするには、以下の手順を実行します。
 1. {{site.data.keyword.iot_short_notm}} ダッシュボードから、**「拡張」**を選択します。
 2. ブロック・チェーン拡張の横にある**「詳細 (Tell me more)」**リンクをクリックして、「IoT ブロック・チェーン・サービス・オファリング (IoT Blockchain Services Offering)」ページに移動します。
 3. サービス要求フォームに必要事項を記入して送信します。
サービスの承認には、通常、1 日ほどかかります。要求が承認された場合、{{site.data.keyword.iot_short_notm}} 組織でブロック・チェーン統合をアクティブにするための手順を示した E メールが送られてきます。
 5. 自分の組織の {{site.data.keyword.iot_short_notm}} ダッシュボードに戻り、セットアップを完了します。詳しくは、[{{site.data.keyword.iot_short_notm}} ブロック・チェーン統合](../../bl_blockchain_integration.html)を参照してください。

## The Weather Company
{: #weathercompany}

The Weather Company 拡張は、気象データを既存の {{site.data.keyword.iot_short_notm}} デバイスに結合します。API を使用して「ロケーションの更新」要求が出されるか、デバイス管理メッセージを使用してデバイスでそのロケーションが既に設定されている場合、The Weather Company からの気象データがデバイスの詳細ビューに表示されます。

**注:** 管理対象デバイスだけがデバイス側でロケーションを設定できます。非管理対象デバイスでは、すべて API を使用して手動でロケーションを設定する必要があります。デバイス・ロケーションの設定について詳しくは、[「ロケーションの更新」要求](../../devices/device_mgmt/index.html#update-location)を参照してください。

### The Weather Company 用の REST API
The Weather Company 用の REST API にアクセスする場合は、[{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather) の資料の『Device Location Weather』のセクションを参照してください。

### 気象データ

特定のデバイス・ロケーションに関して取得した気象データを表示するには、**「デバイス (Devices)」**ペインでデバイスを探してクリックします。詳細なデバイス・ビューで、**「拡張 (Extensions)」**セクションまでスクロールダウンします。以下の気象データがリストされます。

- 現在の天気。
- 現在の温度。
- 予想最高気温と最低気温。
- 相対湿度。
- 気圧。
- 視程。
- 風速。
- 風向き。
- 緯度。
- 経度。

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html). -->
