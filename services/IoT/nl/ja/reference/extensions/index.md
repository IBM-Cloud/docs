---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="\_blank"}
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
Jasper 用の REST API にアクセスする場合は、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Jasper_Extension){: new_window} の資料にある Jasper 拡張のセクションを参照してください。

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
AT&T 用の REST API にアクセスする場合は、[{{site.data.keyword.iot_short_notm}} HTTP REST API![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/AT&T_Extension){: new_window} の資料にある AT&T 拡張のセクションを参照してください。

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

通知は、デバイスまたはセンサー・データでの変更によって生成されます。{{site.data.keyword.iot_short_notm}} がメッセージを処理した後、そのメッセージは {{site.data.keyword.iot_short_notm}} に直接接続されているデバイスと同じ方法でデバイス・イベント・トピックに送られます。ARM mbed プラットフォームに接続されているデバイスで発生する通知で使用されるイベント・タイプは、`notify` です。

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

ARM mbed プラットフォームに接続されているデバイスに {{site.data.keyword.iot_short_notm}} がコマンドを送信すると、デバイスは {{site.data.keyword.iot_short_notm}} に確認メッセージを送り戻します。この確認メッセージは*非同期応答*と呼ばれ、イベント・タイプ `asyncResponse` を使用します。

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
Orange 用の REST API にアクセスする場合は、[{{site.data.keyword.iot_short_notm}} HTTP REST API ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Orange_Extension){: new_window} の資料にある Orange 拡張のセクションを参照してください。

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

デバイス管理は {{site.data.keyword.iot_short_notm}} の中核となるフィーチャーですが、追加機能開発のため、拡張することができます。カスタム・デバイス管理パッケージには、有効な JSON が含まれている必要があり、少なくとも 1 つのカスタム・デバイス・アクションが定義されていなければなりません。

カスタム・デバイス管理機能について詳しくは、必要な JSON フォーマットの例を含め、[デバイス管理のカスタム拡張](../../devices/device_mgmt/custom_actions.html){: new_window}を参照してください。

### カスタム・デバイス管理パッケージの追加

カスタム・デバイス管理パッケージは、{{site.data.keyword.iot_short_notm}} ダッシュボードまたは API のいずれかを使用して追加できます。

{{site.data.keyword.iot_short_notm}} ダッシュボードを使用してカスタム・デバイス管理パッケージを追加するには、次のようにします。

1. {{site.data.keyword.iot_short_notm}} ダッシュボードで、ナビゲーション・バーから**「設定」**をクリックします。
2. **「カスタム・デバイス管理パッケージ」**をクリックします。
3. **「パッケージの追加」**ボタンをクリックします。
4. パッケージ・ファイルを選択し、**「開く」**をクリックします。

API を使用してカスタム・デバイス管理パッケージを追加する場合は、[{{site.data.keyword.iot_short_notm}} API 資料 ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} を参照してください。

## ブロック・チェーン
{: #blockchain}

{{site.data.keyword.iot_short_notm}} でブロック・チェーンを採用すると、IoT デバイスがブロック・チェーンのトランザクションにデータを提供できるようになるので、ブロック・チェーンの変更不能な台帳にデータが格納され、それをスマート・コントラクト・ビジネス・ルールで使用することができます。{{site.data.keyword.iot_short_notm}} は、デバイス・データをブロック・チェーンのスマート・コントラクトで必要なデータ・フォーマットにマップし、それをブロック・チェーン・ファブリックに渡して、ブロック・チェーン台帳に格納されるようにします。

### ブロック・チェーンでサポートされる操作
- デバイス・イベントによってスマート・コントラクト更新をトリガーする。
- スマート・コントラクト・ビジネス・ロジックを実行して、デバイス・イベント・データで台帳状態を更新する。
- モニタリング UI によりブロック・チェーン、トランザクション、台帳状態をモニターする。

### ブロック・チェーン用の構成

{{site.data.keyword.iot_short_notm}} ブロック・チェーン統合は、{{site.data.keyword.iot_short_notm}} でデフォルトではアクティブになっていないサービス・オファリングです。自分の組織でこのフィーチャーをアクティブにするには、以下の手順を実行します。
 1. {{site.data.keyword.iot_short_notm}} ダッシュボードから、**「拡張」**を選択します。
 2. **「拡張」**ページで、**「拡張の追加 (Add Extension)」**をクリックします。
 3. ブロック・チェーン拡張の横にある**「追加」**をクリックします。
 4. ブロック・チェーン・タイルで、**「セットアップ」**をクリックします。
 3. **「ブロック・チェーンのアクティブ化 (Activate Blockchain)」**セクションで、**「詳細はこちら」**リンクをクリックして [IoT Blockchain Services Offering のページ ![外部リンク・アイコン](../../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www.ibm.com/internet-of-things/iot-news/announcements/private-blockchain/){: new_window} に移動します。
 4. **「Kick-start your blockchain project」**をクリックして*「Explore the potential of IoT and Blockchain」*のフォームに記入します。  
 5. 要求が承認されると、IBM から、自分の組織のブロック・チェーン統合を有効にするよう、連絡があります。
 6. 組織の {{site.data.keyword.iot_short_notm}} ダッシュボードに戻り、[{{site.data.keyword.iot_short_notm}} ブロック・チェーン統合](../../bl_blockchain_integration.html)の手順に従ってセットアップを完了します。

<!-- ## The Weather Company
{: #weathercompany}

The Weather Company extension combines weather data with your existing {{site.data.keyword.iot_short_notm}} devices. Weather data from The Weather Company appears in the device details view if an update location request has been made by using the API, or if the device has already set its location by using a device management message.

**Note:** Only managed devices can set their own locations. All unmanaged devices must have their locations set manually by using the API. For more information on setting a device location, see [Update Location requests](../../devices/device_mgmt/index.html#update-location).

### REST APIs for The Weather Company
To access the REST API for The Weather Company, see the
Device Location Weather section in the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window} documentation.

### Weather Data

To view the weather data retrieved for a device location, find the device in the **Devices** pane and click it. In the detailed device view scroll down to the **Extensions** section. The following weather data is listed:

- Current weather.
- Current temperature.
- Predicted maximum and minimum temperature.
- Relative humidity.
- Pressure.
- Visibility.
- Wind speed.
- Wind direction.
- Latitude.
- Longitude.
-->

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->

## E メール
{: #email}

招待メールを使用して、ユーザーを {{site.data.keyword.iot_short_notm}} に追加することができます。詳しくは、[ユーザーのアクセス権限の管理](../../add_users.html)を参照してください。

招待メール機能を使用するには、SendGrid オンライン・サービスまたは Simple Mail Transfer Protocol (SMTP) サービスを使用するように E メール拡張機能を構成する必要があります。この拡張機能では、SendGrid {{site.data.keyword.Bluemix_notm}} アプリケーションを使用することもできます。

### SendGrid オンライン・サービス

SendGrid オンライン・サービスを使用するように E メール拡張機能を構成するには、以下の手順に従います。

1. SendGrid オンライン・アカウントから、許可済み API キーを取得します。
2. {{site.data.keyword.iot_short_notm}} ダッシュボードのナビゲーション・バーから**「拡張」**をクリックします。
3. **「E メール」**セクションで、**「セットアップ」**をクリックします。
4. **「SendGrid で API キーを使用」**を選択します。
5. サイト管理者の名前および E メール・アドレスと、許可済み API キーを入力します。

### SMTP サービス

SMTP サービスを使用するように E メール拡張機能を構成するには、以下の手順に従います。

1. {{site.data.keyword.iot_short_notm}} ダッシュボードのナビゲーション・バーから**「拡張」**をクリックします。
2. **「E メール」**セクションで、**「セットアップ」**をクリックします。
3. **「SMTP」**を選択します。
4. SMTP サービスの構成の詳細を入力します。

### SendGrid {{site.data.keyword.Bluemix_notm}} アプリケーション

SendGrid {{site.data.keyword.Bluemix_notm}} アプリケーションを使用するように E メール拡張機能を構成するには、以下の手順に従います。

1. ダミー・アプリケーションを作成し、SendGrid サービスをバインドします。  
構成資格情報を取得するには、SendGrid サービスをダミー・アプリに追加してバインドします。

 1. {{site.data.keyword.Bluemix_notm}} ダッシュボードから、**「サービスの作成」**をクリックします。
 2. カタログから SendGrid サービスを選択し、**「作成」**をクリックします。
 3. {{site.data.keyword.Bluemix_notm}} ダッシュボードから、{{site.data.keyword.sdk4nodefull}} アプリケーションを追加します。
 4. {{site.data.keyword.Bluemix_notm}} ダッシュボードから {{site.data.keyword.sdk4nodefull}} アプリケーションをクリックし、**「サービスまたは API のバインド」**をクリックします。
 5. SendGrid サービスを選択し、**「追加」**をクリックします。
 6. ここで、{{site.data.keyword.sdk4nodefull}} アプリケーションを再ステージングする必要があります。
2. {{site.data.keyword.iot_short_notm}} サービスを構成する準備をします。  
{{site.data.keyword.iot_short_notm}} は、{{site.data.keyword.iot_short_notm}} ダッシュボードまたは {{site.data.keyword.iot_short_notm}} API を使用して構成することができます。  
 1. {{site.data.keyword.Bluemix_notm}} ダッシュボードから、{{site.data.keyword.sdk4nodefull}} アプリケーションをクリックします。
 2. ナビゲーション・バーから**「環境変数」**をクリックします。
 3. 表示された JSON を一時テキスト・ファイルにコピーします。  
JSON は次の形式になるはずです。
```
{
  "name": "SendGridServiceName",
  "label": "user-provided",
  "credentials": {
    "password": "xxx",
    "hostname": "smtp.sendgrid.net",
    "username": "username"
  }
}
```
3. 構成データを {{site.data.keyword.iot_short_notm}} 組織に追加します。
 1. {{site.data.keyword.iot_short_notm}} ダッシュボードを開きます。
 2. ナビゲーション・バーから**「拡張」**をクリックします。
 3. **「E メール」**アイコンの下にある**「セットアップ」**をクリックします。
 4. **「SendGrid でユーザー名を使用」**を選択します。
 5. 一時テキスト・ファイル内の構成データを入力します。
 6. **「完了」**をクリックします。
