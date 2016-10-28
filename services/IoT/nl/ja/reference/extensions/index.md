---

copyright:
  years: 2015, 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 外部サービスの統合
{: #ref-index}
最終更新日: 2016 年 9 月 13 日
{: .last-updated}

外部サービスの統合は、{{site.date.keyword.iot_full}} 組織内で、サード・パーティーまたは外部サービスからデータや操作にアクセスするためのものです。

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


### Jasper 用の構成

Jasper サービスを {{site.data.keyword.iot_short_notm}} 組織に接続するには、まず実行する必要がある 2 つの構成ステージがあります。まず、{{site.data.keyword.iot_short_notm}} が Jasper サービスに接続されていなければならず、次に {{site.data.keyword.iot_short_notm}} デバイスが構成されていなければなりません。


1. Jasper 拡張を有効にします。Jasper と {{site.data.keyword.iot_short_notm}} 組織の統合を有効にするには、以下の手順を実行します。
  1. {{site.data.keyword.iot_short_notm}} ダッシュボードから、**「拡張」**を選択します。
  2. **「拡張」**ページで、**「拡張の追加 (Add Extension)」**をクリックします。
  3. AT&T の横にある**「追加」**をクリックします。
  4. AT&T ユーザー名、パスワード、アクセス・キー、ドメイン ID を入力します。
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

<!--
## ARM mbed connector
{: #arm}

The ARM mbed connector is an extension that allows you to connect your ARM mbed device to your {{site.data.keyword.iot_short_notm}}. The ARM mbed extension is allows the ARM mbed portal and the {{site.data.keyword.iot_short_notm}} to send and receive data from the ARM mbed portal.

### Setup Configuration


1. Enable the ARM mbed connector extension. To enable the ARM mbed connector extension complete the following steps:
  1. From the {{site.data.keyword.iot_short_notm}} dashboard, select **Settings** and navigate to **Extensions**.
  2. In the **Extensions** menu, click **Add Extension**.
  3. Click **Add** next to ARM mbed connector extension.
  4. Enter your ARM mbed access key and domain ID. You can find these by using the ARM mbed portal at https://connector.mbed.com.
  5. Check the credentials are correct by clicking the **Check Connection** button.
  6. Click **Done**.

### Payload Format

There are two types of incoming messages from the ARM mbed platform, notifications and asynchronous responses. The {{site.data.keyword.iot_short_notm}} can send commands to devices that are connected to the ARM mbed platform.

#### Notifications

Notifications are generated by changes in device or sensor data. After the {{site.data.keyword.iot_short_notm}} processes the message, it is to the device event topic in the same way as a device connected directly to the {{site.data.keyword.iot_short_notm}}. The event type used for notifications originating on devices connected to the ARM mbed platform is `notify`.

The following code sample shows the payload format for a notification sent by the ARM mbed platform API:

```
{
  "ep":<endpoint/deviceID>,
  "path":<resource path>,
  "ct":<content type>,
  "payload":<Base64 encoded payload>,
  "max-age":<how long the payload is valid, in seconds>
}
```

#### Asynchronous responses

When the {{site.data.keyword.iot_short_notm}} sends a command to a device connected to the ARM mbed platform, the device sends a confirmation message back to the {{site.data.keyword.iot_short_notm}}. This confirmation message is called an _asynchronous response_ and uses the event type `asyncResponse`.

The following code sample shows the payload format for an asynchronous response sent by the ARM mbed cloud service:

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

#### Sending commands to the ARM mbed platform

The {{site.data.keyword.iot_short_notm}} can send commands to devices connected to the ARM mbed platform. Commands sent to the ARM mbed platform it must use the following JSON format.

```
{
  "method":<PUT or POST>,
  "deviceId":<endpoint/deviceId>,
  "resourceId":<resource path>,
  "payload": <Base64 encoded payload>
}
```

The payload should be published to the following topic:

```
iot-2/type/<device_type>/id/<deviceId>/cmd/<command_type>/fmt/<command_format>
```
-->

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


## デバイス管理拡張
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
 1. {{site.data.keyword.iot_short_notm}} ダッシュボードから、**「設定」**を選択し、**「拡張」**にナビゲートします。
 2. ブロック・チェーン拡張の横にある**「詳細 (Tell me more)」**リンクをクリックして、「IoT ブロック・チェーン・サービス・オファリング (IoT Blockchain Services Offering)」ページに移動します。
 3. サービス要求フォームに必要事項を記入して送信します。
サービスの承認には、通常、1 日ほどかかります。要求が承認された場合、{{site.data.keyword.iot_short_notm}} 組織でブロック・チェーン統合をアクティブにするための手順を示した E メールが送られてきます。
 5. 自分の組織の {{site.data.keyword.iot_short_notm}} ダッシュボードに戻り、セットアップを完了します。詳しくは、[{{site.data.keyword.iot_short_notm}} ブロック・チェーン統合](../../bl_blockchain_integration.html)を参照してください。
