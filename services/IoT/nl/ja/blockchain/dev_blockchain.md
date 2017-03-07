---

copyright:
  years: 2016, 2017
lastupdated: "2017-2-6"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# {{site.data.keyword.iot_short_notm}} ブロック・チェーン統合のスマート・コントラクトの作成
{: #iotblockchain_link}

{{site.data.keyword.blockchainfull}} と Hyperledger 開発環境を使用して、IBM 提供のサンプル・コントラクトを基に独自のスマート・コントラクトを作成し、テストすることができます。
{:shortdesc}

Go 言語のチェーン・コードの実行可能ファイル形式で、スマート・コントラクトを開発してデプロイします。{{site.data.keyword.iot_short_notm}} ブロック・チェーン統合を使用し、デバイス・イベント・データによってコントラクト更新とビジネス・ロジック実行をトリガーし、新しい台帳状態を各トランザクションのブロック・チェーンに書き込みます。

{{site.data.keyword.iot_short_notm}} ブロック・チェーン統合開発環境は、次のコンポーネントで構成されます。

- {{site.data.keyword.Bluemix_notm}} 組織:
  - IoT ブロック・チェーン統合が有効な状態の {{site.data.keyword.iot_short_notm}} サービス
  - {{site.data.keyword.blockchainfull_notm}} ファブリック
  - IoT デバイス・シミュレーターを実行する Node-RED アプリケーション
   

**注:** シミュレーターを実行するためにローカルにデプロイした Node-RED 環境を使用することもできます。

- ローカル環境:
  - スマート・コントラクト・チェーン・コードを開発、テストするための Hyperledger 開発環境。この環境には Go 言語が含まれています。
  - Blockchain Monitoring UI
- GitHub 環境:
  - IBM 提供のサンプル・スマート・コントラクト用 GitHub リポジトリー
  - スマート・コントラクトを {{site.data.keyword.blockchainfull_notm}} ファブリックにデプロイするための GitHub リポジトリー

次の図は、{{site.data.keyword.iot_short_notm}} ブロック・チェーン統合開発環境を示しています。
![IoT ブロック・チェーン {{site.data.keyword.iot_short_notm}} 統合アーキテクチャー。](images/architecture_contracts.svg "IoT ブロック・チェーン {{site.data.keyword.iot_short_notm}} 統合アーキテクチャー")

## 始めに

{: #byb}

{{site.data.keyword.blockchainfull_notm}} の概要と、それとブロック・チェーンの一般概念との関連性、それを使用する利点について確認します。
- [{{site.data.keyword.blockchainfull_notm}}](http://www.ibm.com/blockchain/) (IBM.com)。
- [{{site.data.keyword.blockchainfull_notm}} 資料](https://console.ng.bluemix.net/docs/services/blockchain/index.html) - {{site.data.keyword.blockchainfull_notm}} サービスの概説。
- [{{site.data.keyword.blockchainfull_notm}} API](https://ibmblockchainapi.mybluemix.net/swagger/ui.html?scheme=http&host=127.0.0.1:3000&basepath=/) -  {{site.data.keyword.blockchainfull_notm}} API の概要。
- [{{site.data.keyword.blockchainfull_notm}} for Developers](http://www.ibm.com/blockchain/for_developers.html) - ブロック・チェーンを開発環境に組み込む方法の概要 (ライブ・デモによる段階的な説明と、{{site.data.keyword.Bluemix_notm}} にデプロイして実行できるコードが含まれています)。

## サンプルのスマート・コントラクト

{: #samples}

[https://github.com/ibm-watson-iot/blockchain-samples](https://github.com/ibm-watson-iot/blockchain-samples) から多数のサンプル・コントラクトをダウンロードできます。これらのサンプル・コントラクトを土台として使用し、デプロイ可能なチェーン・コードに独自のユースケースを組み込んで開発することができます。

|サンプル・コントラクト |説明 |
|:---|:---|
|[基本: シンプル・コントラクト](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/contracts/basic/simple_contract) | ブロック・チェーンのデバイス・アセット・データを追跡して格納するための簡略版の拡張コントラクト
|[拡張: IoT 汎用サンプル・コントラクト](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/contracts/advanced/iot_sample_contract) | データ・モデルと動作に数多くの機能や**トレード・レーン**の特色を追加した拡張サンプル・コントラクト|


## {{site.data.keyword.blockchainfull_notm}} 環境の構成

{: #configure_environment}
スマート・コントラクトをデプロイしてテストする前に、自分用のブロック・チェーン環境をセットアップする必要があります。

**注:** {{site.data.keyword.iot_short_notm}} ブロック・チェーン統合は、{{site.data.keyword.blockchainfull_notm}} ファブリックと Hyperledger ファブリックの両方への接続をサポートしています。以下の例は、{{site.data.keyword.blockchainfull_notm}} を使用することを前提としています。

1. {{site.data.keyword.blockchainfull_notm}} ファブリックを作成し、構成します。
{{site.data.keyword.iot_short_notm}} ブロック・チェーン統合では、ブロック・チェーン台帳、スマート・コントラクト、一般的なブロック・チェーン・インフラストラクチャーを管理するために {{site.data.keyword.blockchainfull_notm}} ファブリックが必要です。{{site.data.keyword.Bluemix_notm}} ブロック・チェーン統合は、{{site.data.keyword.blockchainfull_notm}} を使用してチェーンを管理します。利用できる既存の {{site.data.keyword.blockchainfull_notm}} 環境がある場合は、その環境を使用できます。環境がない場合は、{{site.data.keyword.blockchainfull_notm}} インスタンスを {{site.data.keyword.Bluemix_notm}} [カタログ](https://console.ng.bluemix.net/catalog/services/blockchain/)から作成する必要があります。

  1. {{site.data.keyword.Bluemix_notm}} アカウントのダッシュボードから、**「サービスまたは API の使用」**をクリックします。
  2. サービス・カタログの「アプリケーション・サービス」セクションを見つけ、**「ブロック・チェーン」**を選択します。
     
   **ヒント:** [こちら](https://console.ng.bluemix.net/catalog/services/blockchain/)をクリックすると、{{site.data.keyword.blockchainfull_notm}} サービス・ページに直接移動できます。
  3. {{site.data.keyword.blockchainfull_notm}} サービス・ページで、「サービスの追加」選択内容を確認します。  
    - スペース - デフォルトの `dev` スペース以外のスペースがある場合は、サービスのデプロイ先が意図したスペースであることを確認してください。
    - アプリ - アンバインドのままにします。
    - サービス名 - 覚えやすいサービス名に変更することもできます。この名前は、{{site.data.keyword.Bluemix_notm}} ダッシュボードの {{site.data.keyword.blockchainfull_notm}} タイルに表示されます。
    - 選択済みプラン - 無料プランを選択します。無料プランでは、検証ピア 2 つと認証局 1 つを利用できます。
  4. **「作成」**をクリックし、{{site.data.keyword.blockchainfull_notm}} を {{site.data.keyword.Bluemix_notm}} にデプロイします。
    
最初にデプロイされるブロック・チェーンには、ピア・ノードが 2 つあります。必要に応じてさらにノードを追加できます。

4. {{site.data.keyword.iot_short_notm}} を {{site.data.keyword.blockchainfull_notm}} サービスにリンクします。  
    {{site.data.keyword.iot_short_notm}} からブロック・チェーンに書き込むには、最初にサービスをリンクする必要があります。
     1. {{site.data.keyword.Bluemix_notm}} で、ダッシュボードに移動します。
     2. {{site.data.keyword.blockchainfull_notm}} をデプロイしたスペースを選択します。
     3. **「サービス」**の下の**「ブロック・チェーン」**」リンクをクリックします。
     4. **「サービス資格情報」**タブをクリックします。
     5. サービス資格情報のセットを選択するか、**「新規資格情報」**をクリックして新しいサービス資格情報のセットを作成し、「IoT-Platform 統合」などの記述名を指定します。
     6. JSON 形式のサービス資格情報の次のパラメーターをメモします。  
      - ピア情報: `api_host` と `api_port_tls`
      - タイプ 1 (クライアント) ユーザーの情報: `username` と `secret`  

      サービス資格情報の例:
     ```json
     {
      "peers": [
      {
       "discovery_host": "fa68cbcbfcec4726932e53e2fa4f3afc-vp0.us.blockchain.ibm.com",
        "discovery_port": 30003,
        "api_host": "fa68cbcbfcec4726932e53e2fa4f3afc-vp0.us.blockchain.ibm.com",
        "api_port_tls": 5003,
        "api_port": 5003,
        "event_host": "fa68cbcbfcec4726932e53e2fa4f3afc-vp0.us.blockchain.ibm.com",
        "event_port": 31003,
        "type": "peer",
        "network_id": "fa68cbcbfcec4726932e53e2fa4f3afc",
        "container_id": "e33f08f85988bf57ccfcf34ccdb80d72489e5bfb46786b570e1a74a6679f804e",
        "id": "fa68cbcbfcec4726932e53e2fa4f3afc-vp0",
        "api_url": "http://fa68cbcbfcec4726932e53e2fa4f3afc-vp0.us.blockchain.ibm.com:5003"
    },
       ...
      ],
      "users": [
      {
       "enrollId": "user_type1_0",
        "enrollSecret": "63c58806d6",
        "affiliation": "group1",
        "username": "user_type1_0",
        "secret": "63c58806d6"
      },
       ...
       ]
      }
     }
     ```  
     **重要:** 選択するユーザーが、選択したピア以外のピアに既に登録されていてはなりません。
     7. **「ダッシュボードに戻る」**をクリックして、{{site.data.keyword.Bluemix_notm}}ダッシュボードに戻ります。
     8. {{site.data.keyword.iot_short_notm}} をデプロイしたスペースを選択します。
     9. **「サービス」**の下の**{{site.data.keyword.iot_short_notm}}** リンクをクリックします。
     10. **「起動 (Launch)」**をクリックして {{site.data.keyword.iot_short_notm}} ダッシュボードを開きます。
     11. {{site.data.keyword.iot_short_notm}} ダッシュボードのメニュー・サイド・バーから**「拡張」**を選択します。
     12. **「拡張」**ページの「ブロック・チェーン」タイルで、**「セットアップ」**をクリックするか、すでにファブリックをリンクしてある場合は ![歯車アイコン](../images/gear.png "構成") をクリックします。
     13. 「ブロック・チェーンの構成 (Configure blockchain)」セクションで**「ファブリックの追加 (Add Fabric)」**をクリックし、ファブリック情報を入力します。
    **注:** ファブリックを追加するには、ブロック・チェーン統合を有効にする必要があります。詳しくは、外部サービス統合トピックの[ブロック・チェーン](../reference/extensions/index.html#blockchain)を参照してください。
    1. **「ファブリック (Fabric)」**タブで、{{site.data.keyword.iot_short_notm}} で対象ファブリックを識別する名前を入力して、**「次へ」**をクリックします。   
    2. **「ピア (Peer)」**タブで、以下のようにピア情報を入力します。  
   <table>
   <thead>
   <tr>
   <th>パラメーター</th>
   <th>値</th>
   </tr>
   </thead>
   <tbody>
   <tr>
   <td>名前</td>
   <td>{{site.data.keyword.iot_short_notm}} で対象ピアを識別する名前を入力します。</td>
   </tr>
   <tr>
   <td>ホスト</td>
   <td>検証ピア 1 サーバーの `api_host` アドレス</td>
   </tr>
   <tr>
   <td>ポート</td>
   <td>`api_port_tls` 番号</td>
   </tr>
   <tr>
   <td>ユーザー ID</td>
   <td>ブロック・チェーンにスマート・コントラクトを登録するときに使用したユーザーの `username` ストリング。後で Simple UI を構成するときにも、このユーザー ID を使用します。</td>
   </tr>
   <tr>
   <td>秘密鍵</td>
   <td>ユーザーの `secret` ストリング。</td>
   </tr>
   <tr>
   <td>TLS の使用 (Use TLS)</td>
   <td>オンまたはオフにします。</br>{{site.data.keyword.iot_short_notm}} とファブリックのコントラクトの間の通信を暗号化する場合は、Transport Layer Security を使用します。{{site.data.keyword.blockchainfull_notm}} ファブリックに接続するときには、TLS が有効になっていなければなりません。</td>
   </tr></tbody>
   </table>  
    3. **「完了」**をクリックします。
     3. ブロック・チェーン構成のセクションで**「完了」**をクリックしてファブリック情報を保存します。    

ファブリック・テーブルに新しいファブリック接続が追加されます。  

## スマート・コントラクトの作成、テスト、デプロイ
{: #test_contracts}

これで、Go 言語で独自のスマート・コントラクト・チェーン・コードを作成し、サンドボックス環境でテストし、自分の {{site.data.keyword.blockchainfull_notm}} ファブリックにデプロイしてテストすることができます。

1. スマート・コントラクト・チェーン・コードを保管するための GitHub プロジェクトを作成します。
  
デプロイするスマート・コントラクトはパブリック GitHub リポジトリーに入れなければなりません。詳しくは、https://github.com/ を参照してください。
2.  ローカルの Hyperledger 開発テスト環境をセットアップします。
  
独自のチェーン・コードを開発してテストした後に {{site.data.keyword.blockchainfull_notm}} にデプロイするために、ローカルの開発環境をセットアップする必要があります。この環境には、コントラクトのチェーン・コードを作成するために使用する Go 言語が含まれています。
 1. 開発環境をセットアップします。
   
開発環境には、Go 言語で構築するチェーン・コードを使用してスマート・コントラクトを作成するために必要なツールが含まれています。詳しくは、Hyperledger 資料の [Setting up the development environment](https://github.com/hyperledger/fabric/blob/master/docs/dev-setup/devenv.md) を参照してください。

 2. チェーン・コード・デバッグ環境をインストールします。
    
このデバッグ環境には、{{site.data.keyword.blockchainfull_notm}} にスマート・コントラクトをデプロイする前にテストとデバッグを行うために必要なツールが用意されています。詳しくは、Hyperledger 資料の [Writing, Building, and Running Chaincode in a Development Environment](https://github.com/hyperledger/fabric/blob/master/docs/Setup/Chaincode-setup.md) を参照してください。
 3. 開発用のネットワークをセットアップします。
    
開発用のネットワークによって、スマート・コントラクトの最終テスト用に、より厳密で実動環境に近い環境を用意します。テストしてデバッグしたコントラクトを {{site.data.keyword.blockchainfull_notm}} にデプロイする前の最終テストで、この環境を使用します。詳しくは、Hyperledger 資料の [Setting Up a Network](https://github.com/hyperledger/fabric/blob/master/docs/Setup/Network-setup.md) を参照してください。

3. オプション: IBM 提供のサンプル・スマート・コントラクトをダウンロードします。
  
IBM は多数のスマート・コントラクトを提供しています。ダウンロードしてそのまま使用することも、組織の目的に合わせて変更することもできます。
  
サンプル・コントラクトをダウンロードするには、次のようにします。
 1. ブロック・チェーン・サンプル GitHub リポジトリー (https://github.com/ibm-watson-iot/blockchain-samples/) に移動します。  
 basic_contract_hyperledger フォルダーと trade_lane_contract_hyperledger フォルダーに、基本的なコントラクトとトレード・レーン・コントラクトがそれぞれ入っています。
 3. 端末で `git clone` を使用して、https://github.com/ibm-watson-iot/blockchain-samples プロジェクトを複製します。
   
 **ヒント:** プロジェクト・ページで**「ZIP のダウンロード (Download ZIP)」**をクリックして、プロジェクトの圧縮ファイルをダウンロードすることもできます。

6. スマート・コントラクトを作成してテストします。
    
{{site.data.keyword.iot_short_notm}} ブロック・チェーン統合を使用すると、チェーン・コードの実行可能ファイル形式でスマート・コントラクトを {{site.data.keyword.blockchainfull_notm}} にアップロードし、ブロック・チェーンに書き込まれたデバイス・データに対してビジネス・ロジックを実行できます。スマート・コントラクトのチェーン・コードは Go 言語で作成されます。
   
サンプル・コントラクトは、注目するイベントに関する IoT デバイス・データを、サード・パーティーと共有するために、または、改ざんできないログ・エントリーを作成するためにブロック・チェーンに書き込むことを目的としています。
2. コントラクト実行可能ファイルを作成します。
    
コントラクト・コードをブロック・チェーンにデプロイするには、その前にコントラクト・コードを実行可能ファイルに変換する必要があります。
    
  **注:** サンプル・コントラクト (sample_contract_hyperledger) は既に生成されているため、そのままデプロイできます。
    
次の手順を実行します。
   1. コマンド・ラインを開き、コントラクト・フォルダーに移動します。
   2. `go generate` コマンドを実行します。
     
このコマンドは、コード内に存在するあらゆる「go generate」コマンドを実行します。go generate は、ビルド前コードを生成できるプログラム・ツールです。IBM 提供のサンプル・コントラクトでは、go generate を使用して、コントラクト・スキーマを示す schemas.go ファイルと、sample.go コントラクト・ファイルを作成します。
     
   **重要:** schemas.go ファイルは、{{site.data.keyword.iot_short_notm}} ブロック・チェーン統合の重要なコンポーネントです。このファイルによって、プラットフォームはコントラクトが統合仕様に準拠していることを確認でき、マッパーはデバイス・イベントをマップできるコントラクト API を認識できます。
   2. `go build` コマンドを実行します。
     
このコマンドは、フォルダー名と同じ名前の実行可能ファイルを作成します。このファイルが、ブロック・チェーンにデプロイするコントラクト実行可能ファイルです。

6. Hyperledger サンドボックスでスマート・コントラクトをテストします。
    
完成したスマート・コントラクトを {{site.data.keyword.blockchainfull_notm}} にデプロイする前に、開発環境の一部としてインストールした Hyperledger サンドボックスでチェーン・コードのテストとデバッグを実行できます。  

6. スマート・コントラクト・チェーン・コードを {{site.data.keyword.blockchainfull_notm}} にデプロイします。
   
ローカルでのコントラクトのテストと検証が済んだら、そのコントラクトを {{site.data.keyword.blockchainfull_notm}} ファブリックにデプロイしてテストすることができます。
  1. コントラクトをパブリック GitHub リポジトリーにアップロードします。
    
例えば、sample.go ファイルを次の場所にアップロードします。
    
  `http://github.com/{my organization}/{my project}/`
  2. コントラクトを、前に接続したピアに登録します。
    
REST クライアント (CURL、Postman など) を使用して、登録呼び出しを送信します。登録呼び出しについて詳しくは、[POST registrar API 資料](https://ibmblockchainapi.mybluemix.net/swagger/ui.html?scheme=http&host=127.0.0.1:3000&basepath=/#!/Registrar/registerUser)を参照してください。登録するときには、次の情報を使用してください。
  <ul>
  <li>URL: `http://api_host:api_port_tls/registrar`
  <li>タイプ: POST
  <li>ヘッダー: `Content type:  application/json`
  <li>ペイロード:  
  ```json
   {  
        "enrollId": "{username}",      
        "enrollSecret": "{secret}"    
   }
   ```

  </ul>
  3. コントラクトをピアにデプロイします。
    
デプロイの呼び出しについて詳しくは、[POST devops/deploy API 資料](https://ibmblockchainapi.mybluemix.net/swagger/ui.html?scheme=http&host=127.0.0.1:3000&basepath=/#!/Devops/chaincodeDeploy)を参照してください。
    
デプロイするときには、次の情報を使用してください。  
  <ul>
  <li>URL: `http://api_host:api_port_tls/chaincode`
  <li>タイプ: POST
  <li>ヘッダー: `Accept: application/json`
  <li>ヘッダー: `Content type:  application/json`
  <li>ペイロード:  
  ```
  {
    "jsonrpc": "2.0",
    "method": "deploy",
    "params": {
        "type": 1,
        "chaincodeID":{
              "path": "http://github.com/{my organization}/{my project}/sample.go"
        },
        "ctorMsg": {
            "function":"init",
            "args":["{\"version\":\"1.0\",\"nickname\":\"sample_contract\"}"]
        },
        "secureContext": "username"
    },
    "id":1234
}
  ```  
  </ul>  
  コントラクトがファブリックにデプロイされます。  
  **重要:** 返されたコントラクト ID をメモしてください。ID は 128 文字の英数字ストリング形式です。コントラクトにデバイスをマップするときに、コントラクト ID が必要です。  

10. デバイス・データを、新しいスマート・コントラクトにマップします。
    
デバイス・データからブロック・チェーンの新しいスマート・コントラクトへの書き込みを開始するには、まず、デバイス・データをコントラクトにマップする必要があります。  
   1. {{site.data.keyword.Bluemix_notm}} で、ダッシュボードに移動します。
   2. {{site.data.keyword.iot_short_notm}} をデプロイしたスペースを選択します。
   3. **{{site.data.keyword.iot_short_notm}}** サービスをクリックします。
   4. **「起動 (Launch)」**をクリックして {{site.data.keyword.iot_short_notm}} ダッシュボードを開きます。
   5. サイド・バー・メニューで![「ブロック・チェーン」](images/platform_blockchain.png "ブロック・チェーン")をクリックして、**「ブロック・チェーン」**を選択します。
   6. **「デバイス・データのマップ (Map Device Data)」**をクリックします。
   7. ブロック・チェーンにデバイス・データを保管するデバイス・タイプと、保管するイベントのイベント名を選択します。**「次へ」**をクリックします。
   8. 前に作成したファブリックのファブリック名を選択します。**「次へ」**をクリックします。
   9. 以下の情報を入力して、**「次へ」**をクリックします。
     - 契約 ID - コントラクトをデプロイしたときに保存した 128 文字のコントラクト ID を貼り付けます。
     - 契約名 - {{site.data.keyword.iot_short_notm}} でコントラクトを識別するための名前を入力します。
     
     **ヒント:** デバイスのイベント・タイプを検索するには、**「デバイス」**ページに移動し、デバイス名をクリックしてデバイスの詳細ページを開きます。**「センサー情報」**セクションにスクロールダウンして、そのデバイスの使用可能なイベントとデータ・ポイントのリストを確認します。

   11. 使用可能なデバイス・プロパティーをコントラクト・パラメーターにマップします。
      
   **重要:** マップする各データ・ポイントのデータ・タイプが、マップ先のコントラクト・パラメーターに必要なデータ・タイプに対応していることを確認してください。
     
例えば、ストリング・タイプの「Asset ID」などのコントラクト・プロパティーは、ストリング・タイプのプロパティーにマップする必要があります。コントラクト・パラメーターの要件は、コントラクト Go コードの `type` 定義に定義されています。
     
例えば、IBM 提供の基本コントラクトには、次のコントラクト・パラメーター要件があります。
      
    <ul>
    <li>  AssetID - ストリング
<li>  Location - 地理位置情報
      
    <ul>
    <li> Latitude - float64
    <li>  Longitude - float64
    </ul>
    <li>  Temperature - float64
      
    <li>  Carrier - ストリング
       
    </ul>  
    デバイス・データをコントラクトにマップする方法について詳しくは、GitHub の「IoT Blockchain samples wiki」の [Data mapping example](https://github.com/ibm-watson-iot/blockchain-samples/wiki/Data-mapping-example) を参照してください。
   12. 要約ページで、情報が正しいことを確認します。
   13. 「ブロック・チェーン」ページに、デバイス・データとコントラクトのマッピングが示されます。

7. {{site.data.keyword.blockchainfull_notm}} でスマート・コントラクトをテストします。
  
スマート・コントラクトをテストするには、エンドツーエンドのテストを実行します。そのためには、デバイスを {{site.data.keyword.iot_short_notm}} で作成し、デバイスを {{site.data.keyword.iot_short_notm}} に接続し、IoT Blockchain をブロック・チェーン・ファブリックに接続するように構成し、{{site.data.keyword.iot_short_notm}} を、デバイス・メッセージをマップしてブロック・チェーンに格納するように構成します。{{site.data.keyword.blockchainfull_notm}} コンソールを使用すると、ブロック・チェーンを表示して、台帳内のデバイス・データを確認できます。コントラクトが readAsset() 関数をサポートしている場合には、Monitoring UI を使用してブロック・チェーンを表示し、自分のシナリオから生成されたデバイス・データが、消えずにブロック・チェーンに格納される様子を確認できます。

5. {{site.data.keyword.blockchainfull_notm}} に接続するように Monitoring UI を構成します。
   
 **ヒント:** Monitoring UI をローカル環境にインストールしていない場合には、このときにインストールすることができます。[Blockchain Monitoring UI](https://github.com/ibm-watson-iot/blockchain-samples/tree/master/applications/monitoring_ui) GitHub ディレクトリーにある Monitoring UI の README ドキュメントの手順に従ってください。  
**「CONFIGURATION」**ボタンをクリックして構成設定にアクセスします。
    
次の情報を使用して、コントラクトに接続します。
<table>
<thead>
<tr>
<th>パラメーター</th>
<th>値</th>
<th>コメント</th>
</tr>
</thead>
<tbody>
<tr>
<td>API Host and Port</td>
<td>`http://peer_URL:port`</td>
<td>{{site.data.keyword.blockchainfull_notm}} REST API のホストとポート (前に `https://` を付加したもの)。`api_host` アドレスと `api_port_tls` 番号を使用してください。</td>
</tr>
<tr>
<td>Chaincode ID</td>
<td>コントラクトを登録したときに返されたコントラクト ID。</td>
<td>コントラクト ID は、コントラクト ID のエントリーと一致する 128 文字の英数字ストリングです。  
**重要:** コントラクト ID をカット・アンド・ペーストするときに、ID にスペースが含まれないようにしてください。ID の入力に誤りがあると、ブロック・チェーン台帳のエントリーは表示されますが、アセット検索機能が正常に動作しません。
</td>
</tr>
<tr>
<td>Secure Context</td>
<td>ファブリック・ユーザー</td>
<td>このパラメーターは、{{site.data.keyword.Bluemix_notm}} 上の {{site.data.keyword.blockchainfull_notm}} インスタンスに接続するために必要です。`secureContext` エントリーを使用してください。  
**重要:** secureContext は、ファブリックの構成時に使用した `username` でなければなりません。
</td>
</tr>
<tr>
<td>Number of blocks to display</td>
<td>正の整数。デフォルト: 10</td>
<td>表示するブロック・チェーン・ブロックの数。
</td>
</tr>
</tbody>
</table>

3. Monitoring UI で、セットアップ環境が予期したとおりに動作していることを確認してください。
  
Monitoring UI コンポーネントを使用して、ブロック・チェーン・コントラクトと対話します。  
 - チェーン・コード操作  
コントラクト固有のチェーン・コード操作を予期したとおりに実行できることを確認します。例えば、基本的なコントラクトの場合は、`createAsset` 関数の実行によってブロック・チェーンにアセットが追加されることを確認します。
 - 応答ペイロード  
「チェーン・コード操作 (Chaincode Operations)」タブから REST 要求を送信した場合に、ピア要求から予期したとおりの応答が表示されることを確認します。
 - ブロック・チェーン  
リンクしたデバイスからデータを注入するか、「チェーン・コード操作 (Chaincode Operations)」コンポーネントを使用した場合に、ブロックがチェーンに追加されることを確認します。    

## 次の手順
{: #next_steps}

IBM 提供のサンプル・スマート・コントラクトをデプロイして探索しました。ただし、これらの基本的なコントラクトとトレード・レーン・コントラクトは、よく設計されたスマート・コントラクト・チェーン・コードによって実現される多くの可能性のうち、限られた少数の例を示すものにすぎません。今度は、ご自分のビジネス・シナリオを、{{site.data.keyword.blockchainfull_notm}} でチェーン・コード・コントラクトにマップしてテストしましょう。その後、IoT ブロック・チェーンを統合した {{site.data.keyword.iot_short_notm}} を使用して、デバイス・データをブロック・チェーン台帳に書き込み、そのデータに対する応答として、スマート・コントラクトとして格納されているビジネス・ロジックを実行することができます。     


ブロック・チェーンをお楽しみください。
