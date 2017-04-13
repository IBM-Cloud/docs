---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-31"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# HFC SDK for Node.js
{: #etn_sdk}


Hyperledger Fabric Client (HFC) SDK を使用することにより、アプリケーション開発者は、ブロックチェーン・ネットワークと対話する Node.js アプリケーションを作成することができます。HFC SDK を利用する Node.js アプリケーションを使用して、以下のネットワーク・タスクを実行できます。
{:shortdesc}

* ユーザーを安全に登録し、エンロールする。`registrar` (登録者) 権限を持つ Web アプリケーション管理者は、Web アプリケーションに対して認証したユーザーを動的に登録し、エンロールすることができます。
* トランザクションをブロックチェーン・ネットワークにサブミットする (デプロイ、呼び出し、照会)。'auditor' (監査員) 権限がなければ、トランザクションはすべて、匿名、機密、非連結となります。
* 任意の場所 (ブロックチェーン外のデータベースなど) に、機密性の高い秘密鍵と証明書を保管する。これには、単純なキー値ストア・インターフェースの実装が必要です。

HFC SDK は API を提供します。アプリケーションは、この API を介して Hyperledger Fabric ブロックチェーン・ネットワークと対話します。これらの API は、2 つのプラグ可能コンポーネントをサポートするよう設計されています。

1. プラグ可能キー値ストア。これは、メンバーと関連付けられるキーを取得/保管するために使用されます。`chain.setKeyValStore()` メソッドは、デフォルトのファイルに基づくキー値ストア実装をオーバーライドします。このチェーン・キー値ストアは機密性の高い秘密鍵の保管に使用されるので、アクセスを適切に保護する必要があります。
2. プラグ可能メンバー・サービス。これは、メンバーを登録してエンロールするために使用されます。`chain.setMemberServices()` メソッドは、`MemberServices` のデフォルトの実装をオーバーライドします。メンバー・サービスは Hyperledger Fabric を、許可されたブロックチェーン・ネットワークとして実装します。これにより、匿名性、トランザクションの非連結性、機密性が付与されます。

オフライン方式または npm 方式を使用して、HFC SDK を Node.js アプリに組み込むことができます。
*  オフライン方式: まず、ファイルを Hyperledger Fabric ソース・ツリー (https://github.com/hyperledger/fabric/tree/v0.6/sdk/node/lib) から Node.js アプリの `/lib` ディレクトリーにコピーします。次に、以下のコード・スニペットを追加して、アプリケーションに HFC SDK を組み込みます。

```js
var hfc = require("./lib/hfc");
```

* npm 方式: コマンド・ラインで、最初に以下のスニペットを使用して HFC SDK を npm からインストールします。

```
npm install hfc@0.6.5
```

次に、以下のコード・スニペットでアプリケーションに HFC SDK を組み込みます。

```js
var hfc = require('hfc');
```  
<br>
## HFC オブジェクト
{: #objects}

オブジェクト階層について説明するために、 HFC オブジェクト (クラスとインターフェース) を以下で概説します。

* 最上位のクラスは `Chain` です。これは、ブロックチェーン・ネットワークのクライアント表記です。HFC を使用する場合、複数のネットワークと対話することができ、また、必要に応じて、単一の `KeyValStore` と `MemberServices` オブジェクトを複数の `Chain` オブジェクトと共有することができます。各ブロックチェーン・ネットワークで、1 つ以上の `Peer` オブジェクトを追加します。これは、トランザクションをサブミットするために HFC が接続するエンドポイントを表します。
* `KeyValStore` インターフェースは、すべての永続データを保管/取得するために HFC によって使用されます。このデータには秘密鍵が含まれます。この秘密鍵は保護する必要があります。デフォルトの実装は、`FileKeyValStore` クラスにあるファイルに基づくバージョンです。
* `MemberServices` インターフェースは `MemberServicesImpl` クラスによって実装されます。このインターフェースは、プライバシーや非連結性、機密性など、セキュリティーや ID に関連した機能を提供します。この実装は *eCerts* (メンバー登録証明書) と *tCerts* (各メンバーのトランザクション証明書) を発行します。
* `Member` クラスは、ネットワーク上で処理を行うエンド・ユーザーや、ピア (ノード) などの他のタイプのメンバーを表します。`Member` クラス (このクラスは `MemberServices` オブジェクトと対話する) を使用して、メンバーとユーザーを*登録*および*エンロール*します。`Peer` オブジェクトに対して処理を行うことにより、'Member' クラスから直接チェーンコードをデプロイしたり、照会したり、呼び出したりすることもできます。この実装は単に、一時 `TransactionContext` オブジェクトに処理をデリゲートします。
* `TransactionContext` クラスは、一括のデプロイ、呼び出し、照会ロジックを実装します。各 `TransactionContext` インスタンスは、固有の tCert を `MemberServices` から受け取ります。トランザクションをサブミットする際には常にこれを使用します。同じ tCert を使用して複数のトランザクションを発行するには、Member オブジェクトから直接 `TransactionContext` オブジェクトを取得し、複数のデプロイ、呼び出し、照会操作を発行します。しかし、複数のトランザクションに対して単一の tCert を使用すると、同じ匿名ユーザーが含まれているものとして識別できるようトランザクションをリンクします。トランザクションのリンケージを避けるには、`User` または `Member` オブジェクトに対して、デプロイ、呼び出し、照会を呼び出します。  

<br>

## サンプル Node.js アプリケーション
{: #nodesample}

以下のサンプル Node.js アプリケーションは、HFC SDK API を利用して、Bluemix ブロックチェーン・ネットワークと対話します。プログラムは、スターターと HSBN の両方のブロックチェーン・ネットワーク・プランで機能し、あらゆるクライアント・サイドのオペレーティング・システムで機能します。

目的は、JavaScript アプリケーション [helloblockchain.js](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/helloblockchain.js) を使用してチェーンコード [chaincode_example02](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/src/chaincode/chaincode_example02.go) を Bluemix ネットワークに正常にデプロイしてから、呼び出しと照会を実行することです。  

1. このプログラムでは、Node.js と npm JavaScript パッケージ・マネージャーの両方が必要です。[Node.js](https://nodejs.org/en/) の最新バージョンをインストールすることで、npm が自動的に組み込まれます。  

1. 端末を開き、このデモのソース・コードを置くディレクトリー (ワークスペース) を作成します。例えば、次のようにします。

    ```
    mkdir -p $HOME/workspace
    ```

1. 新しく作成したディレクトリーに移動し、[SDK-Demo](https://github.com/IBM-Blockchain/SDK-Demo) リポジトリーを複製します。`git clone` コマンドを実行する前に、使用している OS 用の適切なバージョンの [Git](https://git-scm.com/downloads) をインストール済みであることを確認します。

     ```
     cd $HOME/workspace
     git clone https://github.com/IBM-Blockchain/SDK-Demo.git
     ```
ネットワークで Hyperledger Fabric v0.5 が実行されている場合は、複製後に次のようにして v0.5 ブランチをチェックアウトします。

     ```
     cd $HOME/workspace/SDK-Demo
     git checkout v0.5
     ```

1. 次は、ブロックチェーン・インスタンスのサービス資格情報を使用する必要があります。

1. まだ行っていなければ、Bluemix の[ブロックチェーン](https://console.ng.bluemix.net/catalog/services/blockchain/)・タイルにアクセスし、サービスのインスタンスを作成します。**Starter Developer** プランか **High Security Business Network** プランのいずれかを選択します。ネットワークを設定したら** 「作成」**ボタンをクリックします。サービス・ダッシュボードが開きます。ページの上部の**「サービス資格情報」**タブをクリックし、ネットワークのピアとユーザーのエンロール・データにアクセスします。**注**: HSBN ネットワークの場合は、サービス資格情報が自動生成されないことがあります。**「新しい資格情報 (New Credential)」**ボタンをクリックすると、新しいウィンドウが開きます。そのウィンドウの下部の**「追加」**をクリックしてください。これにより、サービス資格情報を含む JSON ペイロードが設定されます。

1. 新しい資格情報を指定して、SDK-Demo リポジトリーを複製したときに受け取った ServiceCredentials.json ファイルを更新します。

1. プログラムを実行すると、HFC SDK によって $HOME/workspace/SDK-Demo 内に `keyValStore-<network-id>` ディレクトリーが作成されます。この `keyValStore-<network-id>` ディレクトリーには、エンロールされた各ユーザーの暗号鍵が入れられます。Bluemix インスタンスごとに固有の `keyValStore-<network-id>` ディレクトリーが作成されるので、新しい Bluemix ネットワークに接続するときに `keyValStore` ディレクトリーを削除する必要はありません。ネットワークを削除またはリセットする場合を除き、この暗号素材を**削除しないでください**。このデータがないと、クライアントは Bluemix CA サーバーと通信できないので、エンロールが失敗します。

1. SDK-Demo フォルダーから、ノード・プログラムを実行します。

	```
	node helloblockchain.js
	```
	デバッグ・ログを有効にします。
```
	DEBUG=hfc node helloblockchain.js
	```

	gRPC トレースを有効にします。
	```
	GRPC_TRACE=all DEBUG=hfc node helloblockchain.js
	```

`deploy`、`invoke`、`query` トランザクションが正常に完了すると、端末に以下のメッセージが表示されます。

```
Successfully deployed chaincode: request={"fcn":"init","args":["a","100","b","200"],"certificatePath":"/certs/blockchain-cert.pem","chaincodePath":"github.com/chaincode_example02/"}, response={"uuid":"2d6ad8d6-1390-4c60-a01b-f4c301175eb7","chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","result":"TODO: get actual results; waited 120 seconds and assumed deploy was successful"}

Successfully submitted chaincode invoke transaction: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"invoke","args":["a","b","1"]}, response={"uuid":"f9a902d2-44d8-4b68-b43d-419470ba73ae"}

Successfully completed chaincode invoke transaction: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"invoke","args":["a","b","1"]}, response={"result":"waited 20 seconds and assumed invoke was successful"}

Successfully queried  chaincode function: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"query","args":["a"]}, value=99
```

**注**: チェーンコードのソース・コードは、SDK-Demo リポジトリー内の **src/chaincode** フォルダーの下に保持されます。このフォルダーには、Hyperledger Fabric コードベースのライブラリーと依存関係が入った **/vendor** フォルダー**も**含まれています。現在のチェーンコード・ファイル chaincode_example02.go を独自のチェーンコードに置き換える場合も、必ず、**/vendor** フォルダーを保持してください。ピアでユーザーのチェーンコードを正常にコンパイルしてコンテナーを作成するために、これらの依存関係が必要になります。また、依存ライブラリーがある場合は、必ず、それらを **/vendor** フォルダーの下に追加してください。

Starter Developer ネットワークで実行する場合は、デプロイメントが正常に行われてチェーンコード・コンテナーが開始されるまでに長時間かかる可能性があります。しかし、いったん開始されると、前提条件ファイルはブロックチェーン・インスタンスのホスト・マシンに保管されているので、後続のデプロイメントや呼び出しは即時に行われます。  

**「ネットワーク・コンソール (Network Console)」**から**「ブロックチェーン (Blockchain)」**タブに移動します。このビューには、helloblockchain.js プログラムがデプロイ/呼び出しトランザクションを発行するときに、ブロックチェーン台帳に付加されるブロックが表示されます。以下のスクリーン・ショットには、実行中の helloblockchain.js の結果が 2 度表示されています。デフォルトの引数は "a" と "b" です。

   ![ノードのワークスペース 3](images/nodeworkspace3.PNG "ノードのワークスペース 3")  

<br>

## トラブルシューティング
**/workspace** ディレクトリーから以下のコマンドのいずれかを発行して、**hfc@0.5.4** か **hfc@0.6.5** が実行されていることを確認します。
  * npm list | grep hfc
  * npm list -g | grep hfc  (グローバル `-g` フラグを使用してインストールされる場合)

v0.5 ブランチを使用するネットワークには、旧バージョンの 0.5.4 の HFC が必要です。

照会メッセージを受け取る場合は、以下の手順に従います。

  ```
Failed to query chaincode, function: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"query","args":["a"]}, error={"error":{"status":"FAILURE","msg":{"type":"Buffer","data":[69,114,114,111,114,58,70,97,105,108,101,100,32,116,111,32,108,97,117,110,99,104,32,99,104,97,105,110,99,111,100,101,32,115,112,101,99,40,112,114,101,109,97,116,117,114,101,32,101,120,101,99,117,116,105,111,110,32,45,32,99,104,97,105,110,99,111,100,101,32,40,57,98,101,48,97,48,101,100,51,102,49,55,56,56,101,56,55,50,56,99,56,57,49,49,99,55,52,55,100,50,102,54,100,48,101,50,48,53,102,97,54,51,52,50,50,100,99,53,57,56,100,52,57,56,102,101,55,48,57,98,57,98,56,100,41,32,105,115,32,98,101,105,110,103,32,108,97,117,110,99,104,101,100,41]}},"msg":"Error:Failed to launch chaincode spec(premature execution - chaincode (9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d) is being launched)"}
  ```

Node.js アプリケーションでデプロイ待ち時間を増やします。デフォルトは 60 秒に設定されますが、コードが適切に Docker コンテナーでデプロイ、コンパイルして、実行を開始するのには、より長い時間がかかる可能性があります。デプロイの待ち時間を 120 秒に増やしてみてください。この特異な状況は、ブロックチェーン・インスタンスをホストするマシン上の共有計算リソースの結果として Starter Developer プランでのみ観察されます。

  ```js
chain.setDeployWaitTime(120);
  ```

チェーンコードがネットワークで正常にデプロイされたら、デプロイ時間をわずかな時間 (数秒程度) に減らすことができます。

ハンドシェーク・エラーを受け取る場合、別の `grpc` のバージョンを試してみてください。以下のいずれかのコマンドを使用して、grpc バージョンにアクセスすることができます。
    - `npm list | grep grpc`
    - `npm list -g | grep grpc`  



<br>
## 公開鍵と秘密鍵
{: #keys}

Hyperledger Fabric は、認証局と、基礎となる公開鍵および秘密鍵を使用して、共有ブロックチェーンで稼働するビジネスのセキュリティー要件に対応します。メンバーの ID 管理、役割管理、トランザクションのプライバシーはすべて、HFC SDK によって制御することができます。

共有ブロックチェーンでのユーザーとトランザクションのプライバシーは、PKI (Public Key Infrastructure) フレームワークの実装によって管理されます。認証局による PKI は、鍵やデジタル証明書の生成、配布、取り消しを管理します。PKI とメンバーシップ・サービスの技術的な仕様の詳細については、Hyperledger Fabric v0.6 [プロトコル仕様](http://hyperledger-fabric.readthedocs.io/en/v0.6/protocol-spec/)のセキュリティーのセクションで説明されています。Hyperledger Fabric PKI の基本的な考え方について、以下で説明します。

1. 登録局 (RA) は、ブロックチェーン・ネットワークへのアクセスを要求するユーザーの ID を検証します。これは、`registrar` 権限を持つユーザーが動的に行うことができます。あるいは、membersrvc.yaml ファイルを編集して手動で行うこともできます。登録プロセスは、アウト・オブ・バンドで発生し、`RegisterUser` 関数によって実行されます。RA は、登録の資格情報 (`<enrollID>` と `<enrollPWD>`) をユーザーに割り当てます。

2. ユーザーは、`CreateCertificatePair` 関数を使用して、登録要求を登録認証局 (ECA) に送信します。このペイロードには、ユーザーのワンタイム `<enrollPWD>`、公開署名検証鍵、公開暗号化鍵が含まれており、ユーザーの秘密署名検証鍵によって署名されます。<br><br>登録要求を受け取ると、ECA は、ユーザーの秘密暗号鍵によってのみ暗号化解除できる暗号化チャレンジをユーザーに送ります。チャレンジを暗号化解除した後、ユーザーは認証要求を再送信します。ECA は、正確に暗号化解除された応答を条件として、デジタル証明書で署名された認証済み証明書ペアを返します。<br><br>デジタル署名は、SHA-2 アルゴリズムを使用して「ダイジェスト」を生成し、認証要求 (メッセージ) を暗号的にハッシュすることによって生成されます。次いで、この「メッセージ要約」は、ECA の秘密署名鍵によって暗号化されます。その後、ネットワーク・メンバーは、ECA の公開署名鍵を暗号化解除することにより、デジタル署名を認証することができます。返される登録証明書 (eCert) のペアには、データ署名 (秘密) に対して 1 つの証明書と、データ暗号化 (公開) に対して 1 つの証明書が含まれています。この eCert ペアは、静的であり長期的なものです。これは、トランザクションに対して可視にすることも、不可視にすることもできます。

3. いずれかのブロックチェーン・ネットワークで処理を行うには、各ユーザーにトランザクション証明書 (tCerts) も必要です。登録が成功すると、ユーザーは一群の tCerts の要求をトランザクション認証局 (TCA) にサブミットします。tCert は短期的なもので、1 つのトランザクションに固有であり、API を使用してクライアントが変更することができます。ユーザーの eCert を検証した後、TCA は一群の tCerts と KeyDF_Key (鍵派生ファンクション・キー) を割り当てます。これにより、ユーザーは各自の秘密鍵を暗号化解除することができます。バッチの各 tCert で単一の KeyDF_Key を使用する場合、生成される秘密鍵の確認は各 tCert で固有です。処理を行うためには、クライアントが、暗号化解除された秘密鍵でトランザクションのペイロードに署名できなければなりません。これが行われて初めて、ピアのコンセンサスを検証するためにトランザクションはネットワークに転送されます。
