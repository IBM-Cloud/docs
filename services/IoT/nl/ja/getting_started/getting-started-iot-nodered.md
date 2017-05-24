---

copyright:
  years: 2017
lastupdated: "2017-04-24"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot_short_notm}} スターターの概説
{: #gettingstartedtemplate}
<!-- Provide an appropriate ID above -->

{{site.data.keyword.iot_short_notm}} Starter GitHub プロジェクトを使用して、{{site.data.keyword.iot_full}} を開始します。Starter を使用すれば、デバイスのシミュレート、カードの作成、データの生成の作業を手早く実行したり、{{site.data.keyword.iot_short_notm}} ダッシュボードでデータの分析や表示をすぐに開始したりできます。  
{:shortdesc}

## 概説
{: #overview}  

このスターターを実行すると、以下のサービスが自動的にデプロイされ、接続が確立されます。
<dl>
<dt>**{{site.data.keyword.iot_short_notm}}**</dt>
<dd>ゲートウェイ管理、デバイス管理、アプリケーション・アクセスの機能が組み込まれている IoT Web サービス。{{site.data.keyword.iot_short_notm}} を使用すれば、接続先デバイスのデータを収集し、組織のリアルタイム・データに基づく分析を実行できます。</dd>
<dt>**{{site.data.keyword.sdk4nodefull}}**</dt>
<dd>Node-RED を実行するためのランタイム環境。</br>詳細については、[{{site.data.keyword.sdk4nodefull}}スターターの資料](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html)を参照してください。</dd>
<dd>Node-RED は、ハードウェア・デバイス、API、オンライン・サービスを、新しい興味深い方法で接続するツールです。Node-RED を使用して、シミュレートされたサーモスタットを作成し、シミュレートされたデータを {{site.data.keyword.iot_short_notm}} サービスに送信することができます。また、{{site.data.keyword.iot_short_notm}} ダッシュボードにリアルタイムでデータを表示するためのカードを作成できます。</br>詳細については、[Node-RED の資料](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered)を参照してください。</dd>
<dt>**{{site.data.keyword.cloudantfull}}**</dt><dd>Node-RED がメタデータを保管するデータベース。</dd>
</dl>

## 始めに
{: #byb}  

- 必要なアカウント  
始めに、[IBM Bluemix アカウント](https://bluemix.net/registration)が必要です。

- ヒント  
{{site.data.keyword.Bluemix_notm}} ダッシュボードと {{site.data.keyword.iot_short_notm}} ダッシュボードと Node-RED アプリケーションをブラウザーの別々のタブで開いておくと、この後のプロセスでタスク間の移動が容易になります。
<dl>
<dt>*{{site.data.keyword.Bluemix_notm}} ダッシュボード*</dt>
<dd>デプロイメントの状態を確認したり、資料を読んだり、各種ダッシュボードを起動したりします。</dd>
<dt>*{{site.data.keyword.iot_short_notm}} ダッシュボード*</dt>
<dd>デバイス・タイプを定義したり、デバイスを登録したり、着信するセンサー・データをモニターしたり、データ可視化カードを作成したり、ライブ・データ可視化を確認したりします。</dd>
<dt>*Node-RED*</dt>
<dd>デバイス・シミュレーター・フローを構成して実行したり、他のフローを使用して {{site.data.keyword.iot_short_notm}} から送られてくるデータを処理したりします。</dd>
</dl>

## 手順 1: {{site.data.keyword.iot_short_notm}} Starter をデプロイする
{: #deployStarter}

以下の手順で、Starter サンプル・アプリケーションをデプロイします。

1. スターター・アプリケーションをデプロイします。
 1. <a href="https://bluemix.net/devops/setup/deploy?repository=https://github.com/ibm-watson-iot/iot-platform-bluemix-starter"><img src="https://bluemix.net/devops/graphics/create_toolchain_button.png" height=25></a>をクリックして、Bluemix で新しい継続的デリバリー・ツールチェーンを作成します (継続的デリバリーから)。  
 **ヒント:** コマンド・ラインからデプロイする場合は、GitHub の IBM Watson IoT 組織で [{{site.data.keyword.iot_short_notm}} スターター](https://github.com/ibm-watson-iot/iot-platform-bluemix-starter)を見つけてください。
 2. プロンプトが出されたら、IBM Bluemix にログインします。
 3. 必要に応じて、スターター・アプリケーションをデプロイする Bluemix 組織を選択します。
 4. ツールチェーン名をそのまま使用するか、必要に応じて更新します。その名前はデフォルトのアプリ名になり、アプリの URL のルートとして使用されます (`<app-name>.mybluemix.net`)。
 5. **「作成」**をクリックします。  
**ヒント:** **Delivery Pipeline** タイルをクリックして、最初のデプロイメントの進行状況をモニターしてください。
 6. デプロイメントが完了したら、**「アプリの表示」** をクリックして、新しい Node-RED アプリケーションを新しいタブで開きます。
2. スターター・アプリ・サービスを見つけます。
 1. Bluemix メニューで**「ダッシュボード」**を選択します。
 2. *「すべてのサービス」*で以下のサービスを見つけます。
    - iot-starter
    - iotp-starter-cloudantNoSQLDB
 3. *「すべてのアプリ」*で以下のツールチェーンを見つけます。
    - default-toolchain-{id}}


## 手順 2: シミュレートされるデバイスを {{site.data.keyword.iot_short_notm}} で定義する
{: #definingsimdev}

以下の手順で、リビング・ルームの温度、湿度、位置をサーモスタットでモニターするシナリオをシミュレートします。

1.	{{site.data.keyword.iot_short_notm}} ダッシュボードを起動します。
  1. Bluemix ダッシュボードの*「すべてのサービス」*で、対象の {{site.data.keyword.iot_short_notm}} インスタンスの名前をクリックします。
**ヒント:** インスタンス名には通常、`iotp-starter` が入っています。
  2. **「起動」**をクリックして、{{site.data.keyword.iot_short_notm}} ダッシュボードを新しいブラウザー・タブで開きます。   
`「すべてのボード」`ページがデフォルトで表示されます。
2. デバイス・タイプを作成します。
  1.	メインメニューで**「デバイス」**を選択し、**「デバイスの追加」**をクリックします。
  2.	「デバイスの追加」ページで**「デバイス・タイプの作成」**をクリックします。
  3.	「デバイス・タイプの作成」ページで**「デバイス・タイプの作成」**をクリックします。
  4. デバイス・タイプの固有の名前 (`Thermostat` など) を入力し、**「次へ」**をクリックします。
  5. オプション: 次の 2 つのページでテンプレートとメタデータを定義するかどうかは任意です。各ページでそのまま**「次へ」**をクリックして作業をスキップしてもかまいません。
  6.	**「作成」**をクリックして、デバイス・タイプを追加します。
3.	新しく作成したデバイス・タイプを使用するデバイスを追加します。
  1. 「デバイスの追加」ページのデバイス・タイプのリストに、先ほど作成したデバイス・タイプが表示されます。**「次へ」**をクリックして、そのデバイス・タイプを使用するデバイスを追加します。
  2. 固有のデバイス ID (`LivingRoomThermo1` など) を入力します。
  3. オプション: 「デバイスの追加」ページで説明データを指定するかどうか、その次のページでデバイスのメタデータを入力するかどうかは任意です。各ページでそのまま**「次へ」**をクリックして作業をスキップしてもかまいません。
  4. 「セキュリティー」ページで**「次へ」**をクリックして、デバイスの認証トークンを生成します。
  5. 「サマリー」ページで情報が正しいことを確認してから、**「追加」**をクリックしてデバイスを追加します。前のページに戻る場合は、**「戻る」**をクリックします。
4.	「デバイス資格情報」ページに表示されている情報を書き留めます。   
シミュレーターを構成してデータを表示するために、以下の情報が必要です。
 - 組織 ID
  
 - デバイス・タイプ
 - デバイス ID
 - 認証方式
  
 - 認証トークン
  

## 手順 3: Node-RED デバイス・シミュレーターを構成して実行する  
{: #confignodered}  
Node-RED デバイス・シミュレーターで、温度と湿度の情報を組み込んだ MQTT デバイス・メッセージを {{site.data.keyword.iot_short_notm}} に送信するための構成を行います。

1. Node-RED フロー・エディターを起動します。
  1. Bluemix ダッシュボードの*「すべてのアプリ」*で、対象のツールチェーンの名前をクリックします。  
**ヒント:** ツールチェーン名には通常、`default-toolchain...` が入っています。
  2. ツールチェーン・ダッシュボードで Node-RED インスタンスを開くために、**「経路」**をクリックして、経路のリンクを選択します。  
  2. **「Go to your Node-RED flow editor」**をクリックして、エディターを開きます。
2. デバイスをデプロイします。
  1. デバイス・シミュレーター・フローで、青の**「Send to IBM IoT Platform」**ノードをダブルクリックします。
  2. 「認証」が**「Bluemix サービス」**に設定されていることを確認します。
  3. デバイスの**デバイス・タイプ**と**デバイス ID** を入力して、**「完了」**をクリックします。
  4. **「デプロイ」**をクリックして、デバイスをデプロイします。
3. Node-RED 温度モニター・フローを構成します。
  1. デバイス・シミュレーター・フローで、青の**「IBM IoT App In」**ノードをダブルクリックします。
  2. 「認証」で**「Bluemix サービス」**を選択します。
  3.	「デバイス・タイプ」、「デバイス ID」、「イベント」、「フォーマット」で、**「すべて」**を選択します。
  4.	**「完了」**をクリックします。
  5.  **「デプロイ」**をクリックして、モニターをデプロイします。
4. デバイスの接続を確認します。
  1.	{{site.data.keyword.iot_short_notm}} ダッシュボードを開きます。  
**ヒント:** {{site.data.keyword.iot_short_notm}} ダッシュボードを別のタブでまだ開いていない場合は、{{site.data.keyword.Bluemix_notm}} ダッシュボードに戻り、対象の {{site.data.keyword.iot_short_notm}} インスタンスの名前をクリックしてから、**「ダッシュボードを起動」** をクリックしてください。
  2. メインメニューで**「デバイス」**を選択します。
  3. 先ほど追加したデバイスの名前をクリックします。   
デバイス情報にデバイスの接続状況が表示されます。
  4.	Node-RED フロー・エディターで**「データの送信」**ノードをダブルクリックし、「繰り返し」の値を**「間隔」**に設定し、頻度を `3` 秒ごとに設定します。
  5. **「完了」**をクリックします。
  6. **「デプロイ」**をクリックして、変更内容をデプロイします。  
ペイロードに以下の例のようなデータ・ポイントが組み込まれます。
```
{"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
```
  7. オプション: 「デバッグ」タブを開いて、メッセージが作成されていることを確認します。
    1. 見出しセクションにあるメニューで**「表示」**を選択します。
    2. **「サイドバーの表示」**を選択します。
    3. 「デバッグ」タブをクリックして、メッセージを確認します。
  8. {{site.data.keyword.iot_short_notm}} のデバイス情報ページで、デバイスから受け取ったデータ・ポイントが「センサー情報」セクションに表示されることを確認します。


## 手順 4: {{site.data.keyword.iot_short_notm}} でライブ・データを表示するためのカードを作成する  
{: #createcards}  
{{site.data.keyword.iot_short_notm}} ダッシュボードでデバイス・データを表示するためのボードとカードを作成します。ボードとカードの詳細については、 [ボードとカードを使用したリアルタイム・データの視覚化](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html)を参照してください。

1. ボードを作成します。
  1. {{site.data.keyword.iot_short_notm}} ダッシュボードを開きます。  
  **ヒント:** {{site.data.keyword.iot_short_notm}} ダッシュボードを別のタブでまだ開いていない場合は、{{site.data.keyword.Bluemix_notm}} ダッシュボードに戻り、対象の {{site.data.keyword.iot_short_notm}} インスタンスの名前をクリックしてから、**「ダッシュボードを起動」** をクリックしてください。  
  2. シミュレートされるデバイスのカードを組み込むためのボードを作成します。
    1. 「すべてのボード」ページがまだ表示されていない場合は、{{site.data.keyword.iot_short_notm}} ダッシュボードのメインメニューで**「ボード」**を選択し、**「新規ボードの作成」**をクリックします。
    2. ボードの名前 (`Home Environment` など) を入力し、**「次へ」**をクリックします。
    3. 次のページで**「送信」**をクリックします。  
  3. 作成したばかりのボードをクリックして開きます。
2. 温度を表示するためのカードを作成します。
  1. **「新しいカードの追加」**をクリックしてから、「デバイス」セクションで**「折れ線グラフ」**カード・タイプを選択します。
  2. デバイス・リストから対象のデバイスを選択し、**「次へ」**をクリックします。
  3. **「新規データ・セットの接続」**をクリックします。
  4. 「「値」カードの作成」ページで以下の値を選択/入力し、**「次へ」 **をクリックします。
    - イベント: 更新
    - プロパティー: temp
    - 名前: Temperature
    - タイプ: 浮動小数点
    - 単位: °C
    - 精度: 2
    - 最小: 0
    - 最大: 50
  5. 「カード・プレビュー」ページで、折れ線グラフのサイズとして**「L」**を選択し、**「次へ」**をクリックします。
  6. 「カード情報」ページで、カードの名前を **Temperature** に変更し、**「送信」**をクリックします。   
ダッシュボードに温度のカードが表示され、ライブの温度データの折れ線グラフが組み込まれます。
3. 湿度を表示するためのカードを作成します。
  1. **「新しいカードの追加」**をクリックしてから、「デバイス」セクションで**「ゲージ」**カード・タイプを選択します。
  2. リストから対象のデバイスを選択し、**「次へ」**をクリックします。
  3. **「新規データ・セットの接続」**をクリックします。
  4. 「「値」カードの作成」ページで以下の値を選択/入力し、**「次へ」 **をクリックします。イベント: 更新
     - プロパティー: humidity
     - 名前: Humidity
     - タイプ: 浮動小数点
     - 単位: %
     - 精度: 1
     - 最小: 10
     - 最大: 95
  5. 「カード・プレビュー」ページで、ゲージのサイズとして**「M」**を選択し、**「次へ」**をクリックします。
  6. 「カード情報」ページで、カードの名前を **Humidity** に変更し、**「送信」**をクリックします。   
ダッシュボードに湿度のカードが表示され、ライブの湿度データのゲージが組み込まれます。  

<!-- 4. Create a card to display location
  1. Click **Add New Card**, and then select the **Value** card type, which is located in the Devices section.
  2. Select your device from the list, then click **Next**.
  3. Click **Connect new data set**.
  4. In the Create Value Card page, select or enter the following values.
     - Event: update
     - Property: location.latitude
     - Name: Latitude
     - Type: Float
     - Unit: "°N"
     - Precision: 2
     - Min: -180
     - Max: 180
  5. Click **Connect new data set**.
  6. In the Create Value Card page, select or enter the following values and click **Next**.
     - Event: update
     - Property: location.longitude
     - Name: Longitude
     - Type: Float
     - Unit: "°E"
     - Precision: 2
     - Min: -180
     - Max: 180
  7. In the Card Preview page, select **M** as the text size, and click **Next**.
  8. In the Card Information page, change the name of the card to **Location** and click **Submit**.   
The location card appears on the dashboard and shows the live latitude and longitude of the device.-->

## 次の作業  
{: #whats-next}  
シミュレートされるデバイスが {{site.data.keyword.iot_short_notm}} にデータを送信するようになりました。引き続き IoT プロジェクトの作業を繰り返せます。
 - node-RED フローで生成されるデータがカードに表示されるのを確認します。  
Node-Red を停止するまで、Node-Red から継続的にデータが送信されます。シミュレートされるデータを停止するには、以下の手順を実行します。
    1.	Node-RED フロー・エディターでグレーの**「データの送信」**ノードをダブルクリックし、「繰り返し」の値を**「間隔」**に設定し、頻度を **3** 秒ごとに設定します。
    2. **「完了」**をクリックします。
    3. **「デプロイ」**をクリックして、変更内容をデプロイします。

 - 物理デバイスを接続します。  
[IoT レシピ](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot)を検索して、Raspberry Pi などの物理デバイスを接続し、データを {{site.data.keyword.iot_short_notm}} に送信します。

 - 視覚化オプションを検討します。  
[サンプル node.js アプリケーションをデプロイして、デバイス・データを視覚化します。](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html)

 -	Node-RED フロー・エディターをパスワードで保護します。   
デフォルトでは、だれでもエディターにアクセスしてフローを変更できます。エディターをパスワードで保護するには、以下のタスクを実行します。
    1.	{{site.data.keyword.Bluemix_notm}} ダッシュボードで、対象の Starter アプリケーションの名前をクリックして、そのアプリケーションのページを開きます。
    2. **「ランタイム」**をクリックして、「ランタイム」ページを表示します。
    3. **「環境変数」**をクリックして、「環境変数」ページを表示します。
    4. **「ユーザー定義」**セクションで**「追加」**をクリックしてから、以下のユーザー定義変数を入力します。
         -	NODE_RED_USERNAME - エディターを保護するためのユーザー名
         -	NODE_RED_PASSWORD - エディターを保護するためのパスワード
    3.	**「保存」**をクリックします。
