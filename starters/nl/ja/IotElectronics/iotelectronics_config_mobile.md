---

copyright:
  years: 2016

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# モバイル・アプリの使用
{: #iot4e_using_mobile}
*最終更新日: 2016 年 9 月 19 日*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}} モバイル・アプリの使用を開始して、アラートの受信、コマンドの送信、接続された電気製品の状況のチェックをどのように実行できるか確認します。
{:shortdesc}

## 始める前に

モバイル・アプリを使用するには、事前に以下のタスクを実行する必要があります。
  - {{site.data.keyword.iotelectronics}} スターターのインスタンスを {{site.data.keyword.Bluemix_notm}} 組織にデプロイします。スターターのインスタンスをデプロイすると、スターターのコンポーネント・アプリケーションおよびサービスが自動的にデプロイされます。
  - {{site.data.keyword.amafull}} を構成することによって、[モバイル通信およびセキュリティーを有効にします](iotelectronics_config_mca.html)。

## モバイル・アプリの開始
モバイル・アプリの使用を始めるには、次の手順に従ってください。
1. モバイル・デバイスに[モバイル・アプリをダウンロードします](#iot4e_downloadmobile)。
2. [モバイル・アプリを {{site.data.keyword.iotelectronics}} 環境に接続し](#iot4e_connecting_mobile)、電気製品を登録します。


 ### モバイル・アプリをダウンロードする
 {: #iot4e_downloadmobile}
モバイル・アプリを入手するには、Apple App Store からデバイス上にダウンロードしてインストールします。デバイス上で App Store を開き、「ibm iot」を検索します。**「IBM IoT for Electronics」**を選択してインストールします。

 別の方法として、[iTunes](https://itunes.apple.com/us/app/ibm-iot-for-electronics/id1103404928?ls=1&mt=8) を利用してデバイス上にインストールすることもできます。


### モバイル・アプリを接続する
{: #iot4e_connecting_mobile}

モバイル・アプリを環境に接続し、電気製品を登録するには、以下の手順を実行します。

1. {{site.data.keyword.itoelectronics}} スターター・アプリを開きます。手順については、『[スターター・アプリを開く](iot4ecreatingappliances.html#iot4e_openAppMain)』を参照してください。

2. **「接続された電気製品をリモート制御する (Remotely control your connected appliances)」**を選択します。

    ![{{site.data.keyword.iotelectronics}} スターター・エクスペリエンス](images/IoT4E_remotely_option.png "{{site.data.keyword.iotelectronics}} スターター・エクスペリエンス")

3. **「次にシミュレート洗濯機を選択または追加します (Next, choose or add new simulated washer)」**と表記されたセクションまでスクロールし、+ アイコンをクリックすることによって、1 つ以上の洗濯機を作成します。新規洗濯機が作成されます。

    ![洗濯機の追加](images/IoT4E_add_washer.png "洗濯機の追加")

4.	接続 QR コードまでスクロールし、モバイル・デバイスを使用してそれをスキャンします。接続 QR コードは、**「アプリを環境に接続するために、この QR コードのスキャンが必要になります (To connect the app to the environment, you'll be asked to scan this QR Code)」**と表記されたセクションにあります。

  ![接続 QR コード。](images/iot4e_mobile_connect_QR.png "{{site.data.keyword.iotelectronics}} 接続 QR コード")

5. モバイル・デバイス上で、ログイン資格情報を入力します。ユーザー ID とパスワードの長さに制限はありません。後のセッションのために、ログイン資格情報を忘れないようにしてください。これで、モバイル・デバイスは {{site.data.keyword.iotelectronics}} 環境に登録済みになり、個々の電気製品を登録する準備ができました。

6. コンピューター上で、シミュレート洗濯機までスクロールし、それをクリックしてそのデータと電気製品 QR コードを表示します。

  ![洗濯機の選択。](images/IoT4E_mobile_washer_QR.png "洗濯機の選択。")

7.	モバイル・デバイスで洗濯機の QR コードをスキャンします。洗濯機は登録され、モバイル・デバイスにこの洗濯機の状況が表示されます。

#### 次に行うこと
モバイル・デバイスを使用して、アラートを表示し、洗濯機を制御することができるようになりました。以下のステップを実行して、それを試してみてください。
  - コンピューター上で、ボードの障害や強い振動など、洗濯機の問題を選択します。この問題により、アラートがモバイル・デバイスに送信されます。
  - モバイル・デバイス上で、**「洗濯の開始 (Start wash)」**をクリックして洗濯機を始動します。各洗濯サイクルを進んでいくのにつれて洗濯機の状況が変化するのをコンピューター上で見ることができます。
