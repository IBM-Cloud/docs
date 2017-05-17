---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# データとデバイスの管理
{: #iot4e_dashboard}
{{site.data.keyword.iotelectronics}} ダッシュボードでは、登録済みのデバイスのデータを確認したり、{{site.data.keyword.iot_full}} のデバイスとユーザーを管理したりします。
{:shortdesc}

{{site.data.keyword.iotelectronics}} ダッシュボードを使って、次のことを行えます。
- 組織内で登録済みの電気製品を確認する
- ユーザーを電気製品にマップする
- 一括処理を実行する (多数の電気製品の追加や削除)
- 電気製品のデータを抽出する

## ダッシュボードを開く
{: #iot4e_opendashboard}

**重要:** ダッシュボードを初めて使用する場合は、その前に[ダッシュボードを有効にする](#iot4e_enabledashboard)必要があります。

ダッシュボードを開く方法
1. {{site.data.keyword.Bluemix_notm}} ダッシュボードを開いて、{{site.data.keyword.iot_short_notm}} サービスの名前をクリックします。  

    **ヒント:** サービス名は、末尾が `iotf-service` で、「サービス・オファリング」列に*「Internet of Things Platform」*と記述されています。
2. 「ようこそ」ページで、**「起動 (Launch)」**をクリックします。
3. メニューから、**「電機 (Electronics)」**を選択します。

## ダッシュボードを有効にする方法
{: #iot4e_enabledashboard}

以下の手順を実行して、{{site.data.keyword.iot_full}} 内の {{site.data.keyword.iotelectronics}} ダッシュボードを有効にします。

  **注:** 始める前に、{{site.data.keyword.Bluemix_notm}} 組織に {{site.data.keyword.iotelectronics}} Starter のインスタンスをデプロイする必要があります。Starter のインスタンスをデプロイすると、{{site.data.keyword.iot_short_notm}} など、コンポーネント・アプリケーションとサービスが自動的にデプロイされます。

1. {{site.data.keyword.iot_short_notm}} API キーに新しい役割を追加します。
  1. {{site.data.keyword.Bluemix_notm}} ダッシュボードを開いて、{{site.data.keyword.iot_short_notm}} サービスの名前をクリックします。  

    **ヒント:** サービス名は、末尾が `iotf-service` で、「サービス・オファリング」列に*「Internet of Things Platform」*と記述されています。
  2. 「ようこそ」ページで、**「起動 (Launch)」**をクリックします。
  3. メニューから、**「アプリ」** ![アプリ・アイコン](images/IOT_Icons_apps2.svg "「アプリ」アイコン") を選択し、次に API キーの横にある編集アイコン ![編集アイコン](images/IOT_Icons_Edit_Active_50.svg "編集アイコン") をクリックします。
  4. **「役割をさらに追加 (Add another role)」**をクリックし、**「操作アプリケーション (Operations Application)」**を選択します。
  5. **「保存」**をクリックします。

    ![API の役割](images/IoT4E_API_roles.svg "API の役割")

2. {{site.data.keyword.iot_short_notm}} 組織 ID、API キー、認証コードを見つけます。
  1. {{site.data.keyword.Bluemix_notm}} ダッシュボードに戻ります。
  2. {{site.data.keyword.iotelectronics}} アプリケーションを開きます。

    **ヒント:** アプリケーションは、{{site.data.keyword.Bluemix_notm}} ダッシュボードの「アプリケーション」セクションにあります。経路ではなく名前をクリックしてください。
  3. **「ランタイム」**をクリックしてから**「環境変数」**を選択して、環境変数を表示します。
  4. `iotf-service` と表記されたセクションまでスクロールします。次の値をコピーします。これらは、次の手順で必要になります。

    - `org` - {{site.data.keyword.iot_short_notm}} 組織 ID
    - `apiKey` - {{site.data.keyword.iot_short_notm}} API キー
    - `apiToken` - {{site.data.keyword.iot_short_notm}} 認証トークン  

    ![API 認証資格情報](images/IoT4E_IoTFcred.svg "API 認証資格情報")

3. {{site.data.keyword.iot_short_notm}} 資格情報を {{site.data.keyword.iotelectronics}} サービスに入力します。

  1. {{site.data.keyword.Bluemix_notm}} ダッシュボードに戻ります。
  2. サービス名をクリックして {{site.data.keyword.iotelectronics}} サービスを開きます。

    **ヒント:** サービス名は、末尾が `ibmiotforelectronics` で、「サービス・オファリング」列に*「IoT for Electronics」*と記述されています。
  3. 「ようこそ」ページで、前の手順で見つけた API キー、認証トークン、組織 ID を入力します。
  4. **「更新」**をクリックして入力した内容を保存します。

    ![プラットフォームの構成](images/IoT4E_Platform_config.svg "プラットフォームの構成")

4. これで、{{site.data.keyword.iot_short_notm}} で [{{site.data.keyword.iotelectronics}} ダッシュボードを開く](#iot4e_opendashboard)ことができます。
