---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}

{:shortdesc: .shortdesc}


# スターター・アプリの使用
*最終更新日: 2016 年 9 月 15 日*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}} スターター・アプリでシミュレート電気製品を作成します。{{site.data.keyword.iot_short_notm}} に接続された電気製品を製造メーカーがどのようにモニターできるのか体験します。シミュレート電気製品との手動でのやり取りによって、アラート、通知、およびアクションをトリガーします。
{:shortdesc}


## スターター・アプリを開く
{: #iot4e_openAppMain}

スターター・アプリを開く方法は、使用する {{site.data.keyword.Bluemix_notm}} コンソールのバージョンによって少し異なるため、該当のバージョンの手順を参照してください。

使用しているバージョンは、以下のオプションを探すことによって判別できます。
  - [新しい {{site.data.keyword.Bluemix_notm}}](#iot4e_openApp)。新しい {{site.data.keyword.Bluemix_notm}} エクスペリエンスを使用している場合、ヘッダー・セクションに**「Try the New Bluemix」**が表示*されません*。
  - [クラシック {{site.data.keyword.Bluemix_notm}}](#iot4e_openApp_c)。クラシック {{site.data.keyword.Bluemix_notm}} エクスペリエンスを使用している場合、ヘッダー・セクションに**「Try the New Bluemix」**が表示されます。  

**ヒント:** クラシック {{site.data.keyword.Bluemix_notm}} エクスペリエンスに切り替えるには、ヘッダー・セクションで自身のユーザー名をクリックし、スクロールダウンして**「クラシックに切り替える (Switch to Classic)」**をクリックします。新しい {{site.data.keyword.Bluemix_notm}} エクスペリエンスに切り替えるには、ヘッダー・セクションの**「Try the New Bluemix」**をクリックします。

### 新しい {{site.data.keyword.Bluemix_notm}} エクスペリエンスでスターター・アプリを開く
{: #iot4e_openApp}
1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで {{site.data.keyword.iotelectronics}} スターター・アプリケーションのタイルをクリックして、このアプリケーションを開始します。

    ![ダッシュボードの {{site.data.keyword.iotelectronics}}、新しいエクスペリエンス](images/IoT4E_bm_dashboard.png "ダッシュボードの {{site.data.keyword.iotelectronics}}、新しいエクスペリエンス")

2. ヘッダーに*「アプリは実行中です」*という状況メッセージが表示されるのを待機し、その後で**「アプリの表示」**をクリックしてスターター・アプリを表示します。  

    ![ダッシュボードの {{site.data.keyword.iotelectronics}}、新しいエクスペリエンス](images/IoT4E_view_app.png "ダッシュボードの {{site.data.keyword.iotelectronics}}、新しいエクスペリエンス")

### クラシック {{site.data.keyword.Bluemix_notm}} エクスペリエンスでスターター・アプリを開く
{: #iot4e_openApp_c}

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで {{site.data.keyword.iotelectronics}} スターター・アプリケーションのタイルをクリックして、このアプリケーションを開始します。

    ![ダッシュボードの {{site.data.keyword.iotelectronics}}、クラシック](images/IoT4E_bm_dashboard_c.png "ダッシュボードの {{site.data.keyword.iotelectronics}}、クラシック")

2. 「アプリの正常性」セクションに*「アプリは実行中です」*という状況メッセージが表示されるのを待機し、その後、メインウィンドウで、アプリケーション名の近くにある**「経路」** URL をクリックしてスターター・アプリを表示します。  

    ![ダッシュボードの {{site.data.keyword.iotelectronics}}、クラシック](images/IoT4E_view_app_c.png "ダッシュボードの {{site.data.keyword.iotelectronics}}")

## シミュレート電気製品を作成する
{: #iot4eCreateAppliances}

スターター・アプリでは、シミュレート電気製品の作成と制御を、電気製品の製造メーカーまたは消費者として行うことができます。これらのシミュレート電気製品の状況およびイベント・データは保管され、{{site.data.keyword.iot_full}} で表示することができます。

1. 次のオプションのいずれかを選択してください。
    - 電気製品の製造メーカーとして、**シミュレート電気製品の接続と管理**を行って、シミュレート電気製品を作成します。
    - 電気製品の所有者として、**接続された電気製品をリモートで制御**して、シミュレート電気製品を作成し、[サンプル・モバイル・アプリ](iotelectronics_config_mobile.html)と接続します。

    ![{{site.data.keyword.iotelectronics}} スターター・エクスペリエンス](images/IoT4E_remotely_option.png "{{site.data.keyword.iotelectronics}} スターター・エクスペリエンス")

2. **「次にシミュレート洗濯機を選択または追加します (Next, choose or add new simulated washer)」**と表記されたセクションまでスクロールし、+ アイコンをクリックします。新規洗濯機が作成されます。

    ![洗濯機の追加。](images/IoT4E_add_washer.png "洗濯機の追加")

3. 洗濯機の詳細を表示し、コマンドを発行し、障害を起こすため、洗濯機をクリックします。

  ![洗濯機の状況詳細](images/IoT4E_washer_control.png "洗濯機の状況詳細")


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
