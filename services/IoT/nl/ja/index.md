---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} の概説
{: #gettingstartedtemplate}

{{site.data.keyword.iot_full}} for {{site.data.keyword.Bluemix_notm}} には、ゲートウェイ・デバイス、デバイス管理機能、強力なアプリケーション・アクセス機能など、便利なツールキットが用意されています。{{site.data.keyword.iot_short_notm}} を使用すれば、接続先デバイスのデータを収集し、組織のリアルタイム・データに基づく分析を実行できます。
{:shortdesc}

## 始めに
{: #byb}

デバイスを接続してデータを利用する前に、{{site.data.keyword.Bluemix_notm}} アカウントを登録し、{{site.data.keyword.iot_short_notm}} サービスのインスタンスを {{site.data.keyword.Bluemix_notm}} 組織内に作成しておきます。{{site.data.keyword.iot_short_notm}} インスタンスは、[Bluemix サービス・カタログの {{site.data.keyword.iot_short_notm}} ページ](https://console.{DomainName}/catalog/services/internet-of-things-platform/)から直接作成できます。  

{{site.data.keyword.Bluemix_notm}} でアカウントに登録する方法、領域およびその他のアカウント管理設定の構成について詳しくは、[Bluemix アカウントの管理 ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://console.ng.bluemix.net/docs/admin/account.html#signup){:new_window} を参照してください。

{{site.data.keyword.iot_short_notm}} インスタンスをダッシュボードからセットアップして構成することができます。ダッシュボードを開き、{{site.data.keyword.Bluemix_notm}} の {{site.data.keyword.iot_short_notm}} サービス・インスタンスに移動し、**「ダッシュボードを起動」**をクリックします。

## 手順 1: デバイスを接続する
{: #up_and_running}

そのサービスを稼働させるために、各自の状況に応じて以下のオプションを調べてください。

   |   サービスがデプロイされている | サービスがデプロイされていない
  ------------- | -------------
  **接続するデバイスがある** | [デバイスを {{site.data.keyword.iot_short_notm}}](iotplatform_task.html#iotplatform_task) に接続します。| [Play organization demo ![外部リンク・アイコン](../../icons/launch-glyph.svg)](http://discover-iot.eu-gb.mybluemix.net/?cm_mc_uid=44491599487314618721024&cm_mc_sid_50200000=1462798151#/play){:new_window} でデバイス接続を調べます。
  **接続するデバイスがない** | [Node-RED デバイス・シミュレーターを作成して接続します](nodereddevice_sample.html){:new_window}。 | [Watson IoT Platform Starter ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://console.ng.bluemix.net/docs/starters/IoT/iot500.html){:new_window} で作業を開始します。
特定のデバイス・タイプを {{site.data.keyword.iot_short_notm}} に接続する方法について詳しくは、[developerWorks recipes ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window} を参照してください。  

デバイス接続の開発者資料については、以下のリンク先をご覧ください。
- [デバイスの MQTT 接続](devices/mqtt.html)。
- [ゲートウェイの MQTT 接続](gateways/mqtt.html)。

## 手順 2: デバイス・データを分析する
{: #analyzing_data}

デバイスが {{site.data.keyword.iot_short_notm}} に送信しているリアルタイム・データの検討を開始します。

{{site.data.keyword.iot_short_notm}} には、以下の分析ツールが組み込まれています。  
- [ボードとカード](data_visualization.html)。リアルタイムのデバイス・データを視覚化できます。
- [ルールとアクション](analytics.html)。リアルタイムのデバイス・データによって起動します。

すぐに作業を開始するためのサンプルについては、developerWorks のレシピ [Using Rules and Actions with IBM Watson IoT Platform Cloud Analytics ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){:new_window} を参照してください。

## 手順 3: デバイス・データをコンシュームするアプリケーションを作成する
{: #develop_applications}

リアルタイムと履歴のデバイス・データをコンシュームする独自のアプリケーションを作成して接続することで、{{site.data.keyword.iot_short_notm}} のデータ分析機能を拡張します。

詳しくは、以下のトピックを参照してください。   
- [アプリケーション開発者資料](applications/api.html)と [{{site.data.keyword.iot_short_notm}} API 資料](reference/rest_api.html)を調べてください。
- [{{site.data.keyword.iot_short_notm}} クライアント・ライブラリー](iot_platform_client_lib.html)を調べてください。デバイスやアプリケーションを統合して接続するコードを作成したり開発したりするためのツールやファイルが用意されています。
- {{site.data.keyword.iot_short_notm}} に [{{site.data.keyword.cloudantfull}} サービスを接続して](cloudant_connector.html)、デバイスの履歴データを格納してください。




# 関連リンク
{: #rellinks}
## チュートリアルとサンプル
{: #samples}
* [デバイス接続のレシピ ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window}
* [{{site.data.keyword.iot_short_notm}} Play organization ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://play.internetofthings.ibmcloud.com/){:new_window}
* [Connecting an Intel Galileo to the {{site.data.keyword.iot_short_notm}} ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [Connecting an ARM® mbed™ IoT Starter Kit ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [Connecting a Raspberry Pi to {{site.data.keyword.iot_short_notm}} ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## API リファレンス
{: #api}
* [{{site.data.keyword.iot_short_notm}} API 資料](../reference/rest_api.html)
* [開発者資料](developer_doc_overview.html)
