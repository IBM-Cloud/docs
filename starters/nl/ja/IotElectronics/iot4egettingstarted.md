---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}

{:shortdesc: .shortdesc}


# {{site.data.keyword.iotelectronics}} Starter によるアプリの作成
*最終更新日: 2016 年 9 月 19 日*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}} は、接続された電気製品との通信や、その制御、分析、更新をアプリで実行できるようにする、統合エンドツーエンド・ソリューションです。スターターには、シミュレート電気製品を作成するために使用できるスターター・アプリと、それらの電気製品をモバイル・デバイスから制御するために使用できるサンプル・モバイル・アプリが含まれています。
{:shortdesc}

## 始める前に

始める前に、{{site.data.keyword.iotelectronics}} のインスタンスを {{site.data.keyword.Bluemix_notm}} 組織にデプロイする必要があります。インスタンスをデプロイすると、スターターのコンポーネント・アプリケーションおよびサービスが自動的にデプロイされます。

 [{{site.data.keyword.iotelectronics}} Starter は、](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/){{site.data.keyword.Bluemix_notm}} カタログのボイラープレート・セクションにあります。  

## {{site.data.keyword.iotelectronics}} の開始
開始するには、次のタスクを実行します。

1. {{site.data.keyword.amafull}} を構成することによって、[モバイル通信およびセキュリティーを有効にします](iotelectronics_config_mca.html)。
2. {{site.data.keyword.iotelectronics}} Starter Web アプリケーションを使用して、[シミュレート電気製品を作成します。](iot4ecreatingappliances.html)デモンストレーション目的のため、{{site.data.keyword.iotelectronics}} スターター内ではシミュレート電気製品として洗濯機が使用されています。接続する電気製品として、任意のタイプのスマート家電を選択できます。
3. サンプル・モバイル・アプリを[ダウンロードして接続します](iotelectronics_config_mobile.html)。


## 次に行うこと
{{site.data.keyword.iotelectronics}} で実行できること。

- [スターター・アプリを操作して、](iot4ecreatingappliances.html){{site.data.keyword.iot_short_notm}} に接続された電気製品を製造メーカーがどのようにモニターできるのか体験します。
- [サンプル・モバイル・アプリを操作して、](iotelectronics_config_mobile.html)電気製品の所有者が電気製品の登録および電気製品とのやり取りをどのように行うことができるのか体験します。
- [API を操作して、](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)ユーザー自身の {{site.data.keyword.iotelectronics}} アプリをどのようにカスタマイズおよび拡張できるのかを確認します。

# 関連リンク
{: #rellinks}
## API 資料
{: #api}
* [{{site.data.keyword.iotelectronics}} API](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iot_short}} API](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## コンポーネント
{: #general}

* [{{site.data.keyword.iotelectronics}} の資料](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}} の資料](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
*  [{{site.data.keyword.amashort}} の資料](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}} の資料](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## サンプル
{: #samples}
* [サンプル・モバイル・アプリ](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
