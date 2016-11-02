---

copyright:
years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# HFC SDK for Node.js
{: #etn_sdk}
最終更新日: 2016 年 10 月 07 日
{: .last-updated}

Hyperledger Fabric Client (HFC) SDK により、アプリケーション開発者は、ブロックチェーン・ネットワークと対話する Node.js アプリケーションを作成できるようになります。HFC SDK を利用する Node.js アプリケーションを使用して、以下のネットワーク・タスクを実行できます。
{:shortdesc}

* ユーザーを安全に登録し、エンロールする。`registrar` (登録者) 権限を持つ Web アプリケーション管理者は、Web アプリケーションに対して認証したユーザーを動的に登録し、エンロールすることができます。
* トランザクションをブロックチェーン・ネットワークにサブミットする (デプロイ、呼び出し、照会)。'auditor' (監査員) 権限がなければ、トランザクションはすべて、匿名、機密、非連結となります。
* 任意の場所 (ブロックチェーン外のデータベースなど) にあるストア依存の秘密鍵と証明書。これには、単純なキー値ストア・インターフェースの実装が必要です。

HFC SDK は API を提供します。アプリケーションは、この API を介して Hyperledger Fabric ブロックチェーン・ネットワークと対話します。これらの API は、2 つのプラグ可能コンポーネントをサポートするよう設計されています。

1. プラグ可能キー値ストア。これは、メンバーと関連付けられるキーを取得/保管するために使用されます。`chain.setKeyValStore()` メソッドは、デフォルトのファイルに基づくキー値のストア実装をオーバーライドします。ウェアハウス依存の秘密鍵に対してチェーン・キー値ストアが使用されるので、それに応じてアクセスを保護する必要があります。
2. プラグ可能メンバー・サービス。これは、メンバーを登録してエンロールするために使用されます。`chain.setMemberServices()` メソッドは、`MemberServices` のデフォルトの実装をオーバーライドします。メンバー・サービスは Hyperledger Fabric を、許可されたブロックチェーン・ネットワークとして実装します。これにより、匿名性、トランザクションの非連結性、機密性が付与されます。

オフライン方式または npm 方式を使用して、HFC SDK を Node.js アプリに組み込むことができます。
*  オフライン方式: まず、ファイルを Hyperledger Fabric ソース・ツリー (https://github.com/hyperledger/fabric/tree/master/sdk/node/lib) から Node.js アプリの `/lib` ディレクトリーにコピーします。次に、以下のコード・スニペットを追加して、アプリケーションに HFC SDK を組み込みます。

```js
var hfc = require("./lib/hfc");
```

* npm 方式: コマンド・ラインで、最初に以下のスニペットを使用して HFC SDK を npm からインストールします。

```
npm install hfc@0.5.3 
```

次に、以下のコード・スニペットでアプリケーションに HFC SDK を組み込みます。

```js
var hfc = require('hfc');
```  
<br>
## HFC オブジェクト
{: #objects}

オブジェクト階層をガイドするために、以下の HFC オブジェクト (クラスとインターフェース) の概要が示されています。

* 最上位のクラスは `Chain` です。これは、ブロックチェーン・ネットワークのクライアント表記です。HFC により、複数のネットワークと対話することが可能になります。また、必要に応じて、単一の `KeyValStore` と `MemberServices` オブジェクトを複数の `Chain` オブジェクトと共有できるようにもなります。各ブロックチェーン・ネットワークで、1 つ以上の `Peer` オブジェクトを追加します。これは、トランザクションをサブミットするために HFC が接続するエンドポイントを表します。
* `KeyValStore` インターフェースは、すべての永続データを保管/取得するために HFC によって使用されます。このデータには秘密鍵が含まれます。この秘密鍵は保護する必要があります。デフォルトの実装は、`FileKeyValStore` クラスにあるファイルに基づくバージョンです。
* `MemberServices` インターフェースは `MemberServicesImpl` クラスによって実装されます。このインターフェースは、プライバシーや非連結性、機密性など、セキュリティーや ID に関連した機能を提供します。この実装は *eCerts* (メンバー登録証明書) と *tCerts* (各メンバーのトランザクション証明書) を発行します。
* `Member` クラスは、ネットワーク上で処理を行うエンド・ユーザーや、ピア (ノード) などの他のタイプのメンバーを表します。`Member` クラス (このクラスは `MemberServices` オブジェクトと対話する) を使用して、メンバーとユーザーを*登録*および*エンロール*します。`Peer` オブジェクトに対して処理を行うことにより、'Member' クラスから直接チェーンコードをデプロイしたり、照会したり、呼び出したりすることもできます。この実装は単に、一時 `TransactionContext` オブジェクトに処理を代行します。
* `TransactionContext` クラスは、一括のデプロイ、呼び出し、照会ロジックを実装しています。各 `TransactionContext` インスタンスは、固有の tCert を `MemberServices` から受け取ります。トランザクションをサブミットする際には常にこれを使用します。同じ tCert を使用して複数のトランザクションを発行するには、Member オブジェクトから直接 `TransactionContext` オブジェクトを取得し、複数のデプロイ、呼び出し、照会操作を発行します。しかし、複数のトランザクションに対して単一の tCert を使用すると、同じ匿名ユーザーが含まれているものとして識別できるようトランザクションをリンクします。トランザクションのリンケージを避けるには、`User` または `Member` オブジェクトに対して、デプロイ、呼び出し、照会を呼び出します。  

<br>
## サンプル Node.js アプリケーション
{: #nodesample}

以下のサンプル Node.js アプリケーションは、HFC SDK API を利用して、Bluemix ブロックチェーン・ネットワークと対話します。プログラムは、スターターと HSBN の両方のブロックチェーン・ネットワーク・プランで機能し、あらゆるクライアント・サイドのオペレーティング・システムで機能します。

目的は、JavaScript アプリケーション [helloblockchain.js](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/helloblockchain.js) を使用して、チェーンコード [chaincode_example02](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/chaincode_example02.go) を Bluemix ネットワークに正常にデプロイし、その後、呼び出しと照会を行うことです。  

1. このプログラムでは、Node.js と npm JavaScript パッケージ・マネージャーが必要です。[Node.js](https://nodejs.org/en/) の最新バージョンをインストールすることで、npm が自動的に組み込まれます。  

1. 端末を開き、helloblockchain.js ソース・コードとノード・モジュールを置くディレクトリー (ワークスペース) を作成します。例えば、次のようにします。

    ```
    mkdir -p $HOME/workspace
    ```

1. 新規作成したワークスペース・フォルダーに移動し、以下のコマンドで HFC v0.5.3 をインストールします。

     ```
     cd $HOME/workspace
     npm install hfc@0.5.3
     ```

1. [helloblockchain.js](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/helloblockchain.js) プログラムをコピーし、ワークスペース・フォルダーに保存します。`/workspace` ディレクトリーは、以下のスクリーン・ショットのようになります。

   ![ノードのワークスペース](images/nodeworkspace.PNG "ノードのワークスペース")

1. まだ行っていなければ、Bluemix の[ブロックチェーン](https://console.ng.bluemix.net/catalog/services/blockchain/)・タイルにアクセスし、サービスのインスタンスを作成します。**Starter Developer** プランか **High Security Business Network** プランのいずれかを選択します (承認されている場合は、表示が ![](images/green_dot.png) になります)。**「作成」**ボタンをクリックし、JSON ファイルをコピー・アンド・ペーストすることにより**サービス資格情報**を取得します。ローカルの '/workspace' ディレクトリーに ServiceCredentials.json として保存します。JSON ペイロード全体をコピーしてください。標準エディターでは 202 行になります。**注**: Bluemix [新規コンソール](https://new-console.ng.bluemix.net/#overview)形式に対してブロックチェーン・インスタンスを実行する際、**サービス資格情報**の出力に違いが見られます。つまり、"credentials" 行がオブジェクトから削除されています。これを修正するには、以下のスニペットを ServiceCredentials.json ファイルの 2 行目に追加してください。

	```
	"credentials": {
	```

1. その後、右括弧 `}` を 202 行目に追加して、オブジェクトを閉じます。ServiceCredentials.json のレイアウトは、202 行のペイロードを残して、例 [ServiceCredentials.json](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/ServiceCredentials.json) のレイアウトをミラーリングします。Bluemix の[従来のコンソール](https://console.ng.bluemix.net/)形式から派生したブロックチェーン・インスタンスから資格情報を取得する場合、この矛盾について心配する必要はありません。以下のスクリーン・ショットは、2 つのレイアウトの違いを説明しています。前者は*新しいコンソール*を示しており、後者は*従来のコンソール*を示しています。

     ![サービス資格情報の新しいコンソール](images/servicecreds1.png "サービス資格情報の新しいコンソール")

     ![サービス資格情報](images/servicecreds.png "サービス資格情報")

1. ServiceCredentials.json を追加する際、`/workspace` ディレクトリーは、以下のスクリーン・ショットのようになります。

     ![ノードのワークスペース 2](images/nodeworkspace2.PNG "ノードのワークスペース 2")

1. プログラムが実行されると、HFC SDK は $HOME/workspace 内に `keyValStore` ディレクトリーを作成します。この `keyValStore` ディレクトリーには、各登録済みユーザーの暗号鍵が入ります。新しい Bluemix ネットワークに接続するときに `keyValStore` ディレクトリーを削除する必要はありません。Bluemix インスタンスごとに固有の `keyValStore` ディレクトリーが作成されます。
  

1. 以下に示すように、$GOPATH の下にチェーンコード・ディレクトリーを作成します。マシンでまだ $GOPATH を設定していない場合、[ここにある](https://github.com/golang/go/wiki/GOPGATH)説明に従ってください。

	```
	mkdir -p $GOPATH/src/chaincode_example02
	```

1. [chaincode_example02.go](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/chaincode_example02.go) をこの新規ディレクトリー `$GOPATH/src/chaincode_example02` にコピーします。これは、プログラムを実行した後 Bluemix ネットワークにデプロイされる実際のチェーンコードの一部です。  

1. [vendor.zip](https://github.com/IBM-Blockchain/SDK-Demo/blob/master/vendor.zip) を取得し、それを同じディレクトリー `$GOPATH/src/chaincode_example02` に保存します。vendor.zip パッケージには、Hyperledger Fabric v0.5 コードベースからのライブラリーと依存関係が含まれます。Windows で抽出した場合、デフォルトで、**C:\GOPATH\src\chaincode_example02\vendor** のようなパスが作成されます。抽出する前に、このパスから `\vendor` ディレクトリーを削除してください。そうしないと、チェーンコードのデプロイメントは失敗します。Windows では、正しいパスは次のようになります。**C:\GOPATH\src\chaincode_example02\vendor\github.com\hyperledger\fabric**
(注: `\vendor` ディレクトリー 1 つで適正です。)
Linux や OS X では、`\vendor` ディレクトリーがもう 1 つ作成されるという不規則な事態が生じることはありません。

1. $GOPATH 内にディレクトリーが作成されます。次の例のように表示されます。

    ![ノード $GOPATH](images/nodegopath.PNG "ノード $GOPATH")

1. ローカルの '/workspace' ディレクトリーから、ノード・プログラムを実行します。

	```
	node helloblockchain.js -c chaincode_example02
	```
	デバッグ・ログを有効にします。
```
	DEBUG=hfc node helloblockchain.js -c chaincode_example02
	```

	gRPC トレースを有効にします。
	```
	GRPC_TRACE=all DEBUG=hfc node helloblockchain.js -c chaincode_example02
	```

`deploy`、`invoke`、`query` トランザクションが正常に完了すると、端末に以下のメッセージが表示されます。

```
Successfully deployed chaincode: request={"fcn":"init","args":["a","100","b","200"],"certificatePath":"/certs/blockchain-cert.pem","chaincodePath":"github.com/chaincode_example02/"}, response={"uuid":"2d6ad8d6-1390-4c60-a01b-f4c301175eb7","chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","result":"TODO: get actual results; waited 120 seconds and assumed deploy was successful"}

Successfully submitted chaincode invoke transaction: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"invoke","args":["a","b","1"]}, response={"uuid":"f9a902d2-44d8-4b68-b43d-419470ba73ae"}

Successfully completed chaincode invoke transaction: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"invoke","args":["a","b","1"]}, response={"result":"waited 20 seconds and assumed invoke was successful"}

Successfully queried  chaincode function: request={"chaincodeID":"9be0a0ed3f1788e8728c8911c747d2f6d0e205fa63422dc598d498fe709b9b8d","fcn":"query","args":["a"]}, value=99
```

Starter Developer ネットワークで実行する際には、チェーンコード・コンテナーが開始するまでに 10 分ほどかかる可能性があります。しかし、いったん開始されると、ブロックチェーン・インスタンスの前提条件ファイルがホスト・マシンに保管されているので、後続のデプロイメントや呼び出しは即時に行われます。  

**「ネットワーク・コンソール (Network Console)」**から**「ブロックチェーン (Blockchain)」**タブに移動します。このビューには、helloblockchain.js プログラムがデプロイ/呼び出しトランザクションを発行するときに、ブロックチェーン台帳に付加されるブロックが表示されます。以下のスクリーン・ショットには、実行中の helloblockchain.js の結果が 2 度表示されています。デフォルトの引数は "a" と "b" です。

   ![ノードのワークスペース 3](images/nodeworkspace3.PNG "ノードのワークスペース 3")  

<br>
## トラブルシューティング
**/workspace** ディレクトリーから以下のコマンドのいずれかを発行して、**hfc@0.5.3** が実行されていることを確認します。
  * npm list | grep hfc
  * npm list -g | grep hfc  (グローバル `-g` フラグを使用してインストールされる場合)

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

共有ブロックチェーンでのユーザーとトランザクションのプライバシーは、PKI (Public Key Infrastructure) フレームワークの実装によって管理されます。認証局による PKI は、鍵やデジタル証明書の生成、配布、取り消しを管理します。PKI とメンバーシップ・サービスの技術的な仕様の詳細については、Hyperledger Fabric v0.5 [プロトコル仕様](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md)のセキュリティー・セクションで説明されています。Hyperledger Fabric PKI の基本的な考え方について、以下で説明します。

1. 登録局 (RA) は、ブロックチェーン・ネットワークへのアクセスを要求するユーザーの ID を検証します。これは、`registrar` 権限を持つユーザーが動的に行うことができます。あるいは、membersrvc.yaml ファイルを編集して手動で行うこともできます。登録プロセスは、アウト・オブ・バンドで発生し、`RegisterUser` 関数によって実行されます。RA は、登録の資格情報 `<enrollID>` と `<enrollPWD>` をユーザーに割り当てます。

2. ユーザーは、`CreateCertificatePair` 関数を使用して、登録要求を登録認証局 (ECA) に送信します。このペイロードには、ユーザーのワンタイム `<enrollPWD>`、公開署名検証鍵、公開暗号化鍵が含まれており、ユーザーの秘密署名検証鍵によって署名されます。<br><br>登録要求を受け取ると、ECA は、ユーザーの秘密暗号鍵によってのみ暗号化解除できる暗号化チャレンジをユーザーに送ります。チャレンジを暗号化解除した後、ユーザーは認証要求を再送信します。ECA は、正確に暗号化解除された応答を条件として、デジタル証明書で署名された認証済み証明書ペアを返します。<br><br>デジタル署名は、SHA-2 アルゴリズムを使用して「ダイジェスト」を生成し、認証要求 (メッセージ) を暗号的にハッシュすることによって生成されます。次いで、この「メッセージ要約」は、ECA の秘密署名鍵によって暗号化されます。その後、ネットワーク・メンバーは、ECA の公開署名鍵を暗号化解除することにより、デジタル署名を認証することができます。返される登録証明書 (eCert) のペアには、データ署名 (秘密) に対して 1 つの証明書と、データ暗号化 (公開) に対して 1 つの証明書が含まれています。この eCert ペアは、静的であり長期的なものです。これは、トランザクションに対して可視にすることも、不可視にすることもできます。

3. いずれかのブロックチェーン・ネットワークで処理を行うには、各ユーザーにトランザクション証明書 (tCerts) も必要です。登録が成功すると、ユーザーは一群の tCerts の要求をトランザクション認証局 (TCA) にサブミットします。tCert は短期的なもので、1 つのトランザクションに固有であり、API を使用してクライアントが変更することができます。ユーザーの eCert を検証した後、TCA は一群の tCerts と KeyDF_Key (鍵派生ファンクション・キー) を割り当てます。これにより、ユーザーは各自の秘密鍵を暗号化解除することができます。バッチの各 tCert で単一の KeyDF_Key を使用する場合、生成される秘密鍵の確認は各 tCert で固有です。処理を行うためには、クライアントが、暗号化解除された秘密鍵でトランザクションのペイロードを署名できなければなりません。これが行われて初めて、ピアのコンセンサスを検証するためにトランザクションはネットワークに転送されます。
