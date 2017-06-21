---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# SMS とボイス・メッセージの有効化
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} では、SMS とボイス・メッセージを有効にする Twilio との統合をサポートしています。Twilio はサード・パーティーのアプリケーションで、{{site.data.keyword.Bluemix_notm}} ダッシュボードにインストールできます。
{: shortdesc}

## 前提条件
ボイス・メッセージを有効にするには、認可済みの Twilio アカウントと Twilio の着信電話番号が必要です。Twilio の無料アカウントを使用する場合、電話やメッセージを受信するには、電話番号を認可する必要もあります。詳しくは、[Twilio の資料![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://support.twilio.com/hc/en-us/articles/223136107-How-does-Twilio-s-Free-Trial-work-){:new_window} を参照してください。

## Twilio インスタンスの作成と構成
1. Twilio インスタンスを、{{site.data.keyword.iotinsurance_short}} をインストールした場所と同じ {{site.data.keyword.Bluemix_notm}} 組織およびスペースに作成します。
    1. [{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net) にログインします。
    2. **「カタログ」**タブを選択します。
    3. サービス・カタログの「モバイル」セクションを見つけて、**「Twilio」**をクリックします。

    **ヒント:** Twilio のページに直接移動するには、[こちら![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/catalog/services/twilio/){: new_window} をクリックします。
    {: tip}

    4. Twilio のページで、次のように資格情報を入力してアプリケーションをバインドします。

      1. サービス名として `Twilio-00` と入力します。**重要:** {{site.data.keyword.iotinsurance_short}} に正常に接続するには、`Twilio-00` を使用する必要があります。

      2. Twilio の資格情報を入力します。

      3. **「接続」**メニューで、Twilio インスタンスを {{site.data.keyword.iotinsurance_short}} にバインドするための iot4i-action-engine アプリケーションを選択します。

      4. **「作成」**をクリックします。  

    Twilio アプリケーションがご使用の環境にインストールされます。iot4i-action-engine アプリケーションを再ステージまたは再始動してバインドを有効にするようにメッセージが出されます。今すぐ再始動することも、次の手順で新しい環境変数を追加してから再始動することもできます。

2. iot4i-action-egine コンポーネント用に TWILIO_FROM_NUMBER という環境変数を作成します。
    1. Bluemix ダッシュボードから、iot4i-action-engine アプリケーションを開きます。
    2. **「ランタイム」**を選択し、**「環境変数」**をクリックします。
    3. **「ユーザー定義」**セクションで、**「追加」**をクリックします。
    4. 「名前」列に `TWILIO_FROM_NUMBER` と入力し、「値」列に Twilio 音声および SMS 対応の番号を入力します。
    5. **「保存」**をクリックします。

3. 「経路」ボタンの横にある「再始動」アイコンをクリックして、iot4i-action-engine アプリケーションを再始動します。

## シールドへの SMS および音声アクションの追加

SMS および音声の機能をシールドに追加するには、以下のアクションをシールド定義に追加する必要があります。
  - `send-sms`
  - `phone-call`

アクションのリストが含まれるシールドの例については、[サンプル・シールドの作成例![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/blob/master/bl/shield.js){:new_window} を参照してください。この例では、`email` および `pushios` 各アクションが含まれるアクションのリストに、SMS アクションおよび音声アクションを追加できます。

シールド作成に関する詳細については、[シールド・ツールキットの使用](iotinsurance_shield_toolkit.html)を参照してください。
