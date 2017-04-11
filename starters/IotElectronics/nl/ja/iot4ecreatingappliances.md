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

# スターター・アプリの使用
{{site.data.keyword.iotelectronics_full}} スターター・アプリでシミュレート電気製品を作成します。{{site.data.keyword.iot_short_notm}} に接続された電気製品を製造メーカーがどのようにモニターできるのか体験します。シミュレート電気製品と手動で対話して、アラート、通知、アクションを起動します。
{:shortdesc}


## スターター・アプリを開く
{: #iot4e_openApp}

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、スターター・アプリケーションのタイルをクリックして {{site.data.keyword.iotelectronics}} スターター・アプリケーションを開始します。

    ![ダッシュボードの {{site.data.keyword.iotelectronics}}。](images/IoT4E_bm_dashboard.svg "ダッシュボードの {{site.data.keyword.iotelectronics}}")

2. *「アプリは稼働しています」*という状況メッセージがヘッダーに表示されるまで待機してから、**「アプリの表示 (View App)」**をクリックしてスターター・アプリを表示します。

    ![{{site.data.keyword.iotelectronics}} アプリの表示。](images/IoT4E_view_app.svg "{{site.data.keyword.iotelectronics}} アプリの表示")

## シミュレート電気製品を作成する
{: #create_sim}

スターター・アプリで、シミュレート電気製品を電気製品の製造メーカー、またはコンシューマーとして作成して制御できます。これらのシミュレート電気製品の状況とイベント・データが保管され、{{site.data.keyword.iot_full}} で確認できます。

1. 以下のオプションのいずれかを選択します。
    - **シミュレート電気製品を接続して管理する**。これは、電気製品の製造メーカーの観点でシミュレート電気製品を作成する方法です
    - **接続した電気製品をリモート制御する**。これは、電気製品の所有者の観点でシミュレート電気製品を作成して[サンプル・モバイル・アプリ](iotelectronics_config_mobile.html)に接続する方法です。

    ![{{site.data.keyword.iotelectronics}} スターターの体験](images/IoT4E_remotely_option.svg "{{site.data.keyword.iotelectronics}}スターターの体験")

2. **「次にシミュレート洗濯機を選択または追加します (Next, choose or add new simulated washer)」**と表記されたセクションまでスクロールし、「+」アイコンをクリックします。新規洗濯機が作成されます。

    ![洗濯機の追加。](images/IoT4E_add_washer.svg "洗濯機の追加")

3. 洗濯機の詳細情報を確認するには、洗濯機をクリックします。コマンドと制御パネルで、洗濯機を始動させるか別のタイプの故障をクリックして、状況の変化を確認します。モバイル・アプリから、状況の変化を確認したり洗濯機を制御したりすることもできます。

  ![洗濯機の状況の詳細。](images/IoT4E_washer_control.svg "洗濯機の状況の詳細")


# 関連リンク
{: #rellinks}

## API 資料
{: #api}
* [{{site.data.keyword.iotelectronics}} API](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iot_short}} API](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## コンポーネント
{: #general}

* [{{site.data.keyword.iotelectronics}} の資料](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}} の資料](https://console.ng.bluemix.net/docs/services/IoT/index.html)
*  [{{site.data.keyword.amashort}} の資料](https://console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}} の資料](https://console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## サンプル
{: #samples}
* [サンプル・モバイル・アプリ](https://console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
