---

copyright:
  years: 2016

---

{:new_window: target="_blank"}

{:shortdesc: .shortdesc}


# {{site.data.keyword.iotelectronics}} Starter によるアプリの作成
*最終更新日: 2016 年 6 月 14 日*

{{site.data.keyword.iotelectronics_full}} は、接続された電気製品との通信や、その制御、分析、更新をアプリで実行できるようにする、統合エンドツーエンド・ソリューションです。Starter には、シミュレート電気製品を作成して制御するためのスターター・アプリと、その電気製品をモバイル・デバイスから制御するためのサンプル・モバイル・アプリが組み込まれています。
{:shortdesc}

**前提条件**:  
Bluemix カタログのボイラープレート・セクションから {{site.data.keyword.iotelectronics}} Starter をデプロイしておきます。これにより、{{site.data.keyword.amafull}} を含め、Starter のコンポーネント・アプリケーションおよびサービスが自動的にデプロイされます。

{{site.data.keyword.iotelectronics}} の使用を開始するには、後続の各セクションの説明に従って、以下の作業を行います。

1. {{site.data.keyword.amashort}} を構成して、サンプル・モバイル・アプリとの通信を使用可能にします。
2. {{site.data.keyword.iotelectronics}} Starter Web アプリケーションを使用して、シミュレート電気製品を作成します。
3. サンプル・モバイル・アプリをインストールして接続します。

## {{site.data.keyword.amashort}} を構成する
{: #configureMCA}
モバイル・アプリを使用するには、以下のように {{site.data.keyword.amashort}} を構成する必要があります。
1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、[{{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html) を開きます。
2. **「カスタム」**セクションで、**「構成」**を選択します。
3. 以下の認証資格情報を入力します。
  - **レルム名**: myRealm
  - **URL**: https://<*myIoT4eStarterApp*>.mybluemix.net  

    **ヒント:** URL ではセキュアな `https://` 接頭部を必ず使用してください。スターター・アプリの URL を確認するには、**「モバイル・オプション」**をクリックします。
4. 保存します。

  詳しくは、『[Configuring {{site.data.keyword.amashort}}](iotelectronics_config_mobile.html#iot4e_configureMCA)』を参照してください。

##シミュレート電気製品を作成する
シミュレート電気製品を作成するには、以下のステップを実行します。
1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、{{site.data.keyword.iotelectronics}} アプリケーションを開始します。
2. `「アプリは稼働しています」`という状況メッセージが表示されるまで待機してから、**「アプリの表示 (View App)」**をクリックしてスターター・アプリを表示します。  
3. **「接続された電気製品をリモート制御する (Remotely control your connected appliances)」**を選択します。
4. **「次にシミュレート洗濯機を選択または追加します (Next, choose or add new simulated washer)」**と表記されたセクションまでスクロールし、追加 (+) ボタンをクリックします。新規洗濯機が作成されます。

## サンプル・モバイル・アプリをインストールして接続する
サンプル・モバイル・アプリをインストールして接続するには、以下のステップを実行します。

*注*: サンプル・モバイル・アプリを使用するには iOS デバイスが必要です。

1. デバイスで App Store を開き、`「ibm iot」`を検索します。**「IBM IoT for Electronics」**を選択してインストールします。
2. スターター・アプリにある接続 QR コードをスキャンして、デバイスを組織に接続します。
3. スターター・アプリにある電気製品 QR コードをスキャンして、シミュレート電気製品を接続します。

  詳しくは、「[Connecting the mobile app to your {{site.data.keyword.iotelectronics}} environment](iotelectronics_config_mobile.html#iot4e_connecting_mobile)」を参照してください。

##次に行うこと
{{site.data.keyword.iotelectronics}} で実行できること。

- スターター・アプリを操作して、{{site.data.keyword.iot_short_notm}} に接続された電気製品を製造メーカーがどのようにモニターできるのか体験します。
- サンプル・モバイル・アプリを操作して、電気製品の所有者が電気製品の登録および電気製品とのやり取りをどのように行うことができるのか体験します。
- 手動で装置の障害を発生させて、製造メーカーと電気製品の所有者の両方に向けて、アラート、通知、アクションを起動します。
- 作動データとユーザー・データを関連付けることで、製品および装置の作動状況とそれらを操作するユーザーについて理解します。


# 関連リンク
{: #rellinks}
## API 資料
{: #api}
* [{{site.data.keyword.iotelectronics}}](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iotrtinsights_short}}](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)  
* [{{site.data.keyword.iot_short}}](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## コンポーネント
{: #general}

* [{{site.data.keyword.iotelectronics_full}} の資料](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
* [{{site.data.keyword.iotrtinsights_full}}](https://new-console.ng.bluemix.net/docs/services/iotrtinsights/iotrtinsights_overview.html)
* [{{site.data.keyword.amafull}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}}](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## サンプル
{: #samples}
* [サンプル・モバイル・アプリ](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
