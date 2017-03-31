---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-10"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Note to writers - index.md and iot4egettingstarted.md are (almost) duplicates and a change to one should be made to both. index.md appears within the product app as the getting started page. iot4egettingstarted.md appears as the top level topic in the docs toc. -->

# {{site.data.keyword.iotelectronics}} Starter によるアプリの作成

{{site.data.keyword.iotelectronics_full}} は、接続された電気製品との通信や、その制御、分析、更新をアプリで実行できるようにする、統合エンドツーエンド・ソリューションです。Starter には、シミュレート電気製品を作成するために使用できるスターター・アプリと、それらの電気製品をモバイル・デバイスから制御するために使用できるサンプル・モバイル・アプリが組み込まれています。
{:shortdesc}

## 始める前に

始める前に、{{site.data.keyword.Bluemix_notm}} 組織に {{site.data.keyword.iotelectronics}} のインスタンスをデプロイする必要があります。
インスタンスをデプロイすると、スターターのコンポーネント・アプリケーションおよびサービスが自動的にデプロイされます。

 [{{site.data.keyword.iotelectronics}} Starter](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/) は、{{site.data.keyword.Bluemix_notm}} カタログのボイラープレート・セクションにあります。

## {{site.data.keyword.iotelectronics}} の概説
開始するには、次のタスクを完了してください。

1. {{site.data.keyword.amafull}} を構成して、[モバイル通信とセキュリティーを使用可能にします](iotelectronics_config_mca.html)。
2. {{site.data.keyword.iotelectronics}} スターター Web アプリケーションを使用して、[シミュレート電気製品を作成します](iot4ecreatingappliances.html)。{{site.data.keyword.iotelectronics}} Starter 内では、デモンストレーション用のシミュレート電気製品として、洗濯機が使用されます。接続先に選択する電気製品は、どのタイプのスマート電子デバイスでもかまいません。
3. サンプル・モバイル・アプリを[ダウンロードして接続します](iotelectronics_config_mobile.html)。


## 次に行うこと
{{site.data.keyword.iotelectronics}} で実行できること。

- [スターター・アプリを操作して、](iot4ecreatingappliances.html){{site.data.keyword.iot_short_notm}} に接続された電気製品を製造メーカーがどのようにモニターできるのか体験します。
- [サンプル・モバイル・アプリを操作して、](iotelectronics_config_mobile.html)電気製品の所有者が電気製品の登録および電気製品とのやり取りをどのように行うことができるのか体験します。
- {{site.data.keyword.iot_short_notm}} で登録済み電気製品の[データを操作して管理します](iotelectronics_dashboard.html)。
- [API を操作して ![外部リンクのアイコン](../../icons/launch-glyph.svg)](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html){:new_window}、独自の {{site.data.keyword.iotelectronics}} アプリをカスタマイズして展開する方法を確認します。

# 関連リンク
{: #rellinks}
<!-- Related Links last updated 23 October 2016 - new API source -->
## API 資料
{: #api}
* [{{site.data.keyword.iotelectronics}} API ![外部リンクのアイコン](../../icons/launch-glyph.svg)](https://broker-uss-iot4e.electronics.internetofthings.ibmcloud.com/public/iot4eregistrationapi.html){:new_window}
* [{{site.data.keyword.iot_short}} API ![外部リンクのアイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/iotfoundation/recipes/api-documentation/){:new_window}


## コンポーネント
{: #general}

* [{{site.data.keyword.iotelectronics}} の資料](iotelectronics_overview.html){:new_window}
* [{{site.data.keyword.iot_full}} の資料](https://console.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
*  [{{site.data.keyword.amashort}} の資料](https://console.ng.bluemix.net/docs/services/mobileaccess/overview.html){:new_window}
* [{{site.data.keyword.sdk4nodefull}} の資料](https://console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime){:new_window}

## サンプル
{: #samples}
* [サンプル・モバイル・アプリ](https://console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html){:new_window}
