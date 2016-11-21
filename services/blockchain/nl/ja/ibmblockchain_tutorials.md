---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# サンプル・アプリとチュートリアル
{: #1stanchor}
最終更新日: 2016 年 10 月 5 日
{: .last-updated}

以下のサンプルは、アプリケーションとチェーンコードが IBM Blockchain ネットワークでどのように機能するかを示しています。ブロックチェーン・ネットワークの基礎となる Hyperledger Fabric v0.5 コードについて詳しくは、Linux Foundation Hyperledger Project の[ファブリック・ドキュメント](https://github.com/hyperledger/fabric/tree/master/docs)のセクションを参照してください。  
{:shortdesc}

チェーンコード・アプリケーションを実践で使用するには、以下の Marbles、Commercial Paper、または Car Lease のデモをすぐにデプロイできます (「Bluemix にデプロイ」ボタンをクリックします)。または、「チェーンコードへようこそ (Hello Chaincode)」チュートリアルを読み進めます。

- [![Bluemix にデプロイ](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)(https://bluemix.net/deploy/button.png)]  **Marbles**
- [![Bluemix にデプロイ](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)(https://bluemix.net/deploy/button.png)]  **Commercial Paper**
- [![Bluemix にデプロイ](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)(https://bluemix.net/deploy/button.png)]  **Car Lease**  

<br>
## 「チェーンコードへようこそ (Hello Chaincode)」チュートリアルの使用
{: #hellocc}
このチュートリアルでは、基本的なビルディング・ブロックを使用して基本的なチェーンコード・アプリケーションをコーディングする方法について説明します。ネットワーク上で交換するための汎用アセットを作成する処理チェーンコードを増分ビルドします。次に、ネットワーク API を介してチェーンコードと対話します。このチュートリアルを完了すると、以下についての質問に答えることができます。
- チェーンコードとはどのようなものですか。
- チェーンコードはどのように実装しますか。
- どんな依存関係が存在しますか。
- 主な機能は何ですか。
- さまざまな値を引数に渡す方法はどのようなものですか。
- ユーザーを自分のネットワークにセキュアな方法で登録する方法はどのようなものですか。
- チェーンコードはどのようにコンパイルしますか。
- REST API を介してチェーンコードとどのように対話できますか。

### チェーンコードとはどのようなものですか。
チェーンコードは、ユーザーがブロックチェーン・ネットワークと対話するための Go (GoLang) または Java コードです。ネットワークのトランザクションを「呼び出す」と、チェーンコードで台帳に対して値を読み書きする特定の機能を呼び出していることになります。

### 最初のチェーンコードの実装
以下のトピックに従って、IBM Blockchain on Bluemix ネットワークでチェーンコードを実装します。
#### 環境のセットアップ
1. 以下からご使用のオペレーティング・システムに適した Golang をダウンロードしてインストールします: [GoLang](https://golang.org/dl/)。
2. GOPATH を以下のように設定します。
	- $GOPATH は Go コードとプロジェクトへの**環境変数** PATH です。標準的な Go ツリーの外部でパッケージを取得、作成、インストールするには、$GOPATH を設定する必要があります。このため、$GOPATH は元の Go ツリーが常駐する $GOROOT パスに対して固有である必要があります。ディレクトリーを作成してから、そこに $GOPATH を指定します。
	- Windows では $GOPATH を以下のように設定します。
		- プロジェクトのワークスペース・ディレクトリーを作成します (C:\Users\ADMIN\Documents\GoProjects)。
		- Windows **スタート**・メニューをクリックして、「システム環境変数」を検索します。
		- **「システム環境変数の編集 (Edit the system environment variables)」**をクリックします。
		- **「拡張」**タブで、**「環境変数」**をクリックします。
		- システム環境変数 GOPATH と GOROOT を見つけます。GOPATH を作成する必要がある場合は、**「新規」**をクリックします。  
		- GOROOT と GOPATH の値は固有でなければなりません。GOROOT は Go をインストールしたときに自動生成され、C:\Go\ のようになります。
		- 作成したばかりのワークスペース・ディレクトリーに GOPATH を設定します。この例では、**GOPATH** は  **C:\Users\ADMIN\Documents\GoProjects** に設定されています。  
		- 詳しくは、コマンド `go help gopath` を実行するか、「[資料を参照する](https://golang.org/doc/install)」にアクセスします。
3. 以下のコマンドを実行して Hyperledger Faric v0.5 シム・コードを Go パスに追加します。

	```
	go get github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview/core/chaincode/shim
	```

4. **注意**: 必ず必ず上記リンクをたどって v0.5 hyperledger-archives シム・コードをインポートしてください。Bluemix バックエンドはこの同じバージョン管理方式で構築されます。したがって、シム・バージョンと Bluemix バージョンが合っていることが重要となります。

#### GitHub のセットアップ
Blockchain on Bluemix プランでは、チェーンコードを [GitHub](https://Github.com/) リポジトリーに配置する必要があります。GitHub アカウントを作成し、「[Git のセットアップ](https://help.github.com/articles/set-up-git/)」で説明されているように Git をセットアップします。GitHub をセットアップしたら、以下のステップを実行します。
1. 「[チェーンコードについて学習する](https://github.com/IBM-Blockchain/learn-chaincode)」に進み、リポジトリーを fork します。  
2. fork を $GOPATH に指定されたディレクトリーに複製します。  
3. このリポジトリーには以下の 2 つのディレクトリーが含まれています。[Start](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/start/chaincode_start.go) は、作成を開始するチェーンコードです。[Finished](https://github.com/IBM-Blockchain/learn-chaincode/blob/master/finished/chaincode_finished.go) は、最終的に作成されるチェーンコードです。
4. チェーンコードがローカル環境で作成されていることを確認します。コマンド・プロンプトを開き、`chaincode_start.go` が入っているフォルダーに移動します。以下のコマンドを入力します。

	```
	go build ./
	```
コマンドはエラーやメッセージなしで返されるはずです。
#### チェーンコード・インターフェースの実装
次のステップは、Golang コードでのチェーンコード・シム・インターフェースの実装です。3 つの主な機能は、**初期化**、**呼び出し**、および **照会** です。これら 3 つの機能はすべて、機能名とストリングの配列を入力として取りますが、これらは呼び出されるタイミングによって変化します。ブロックチェーン・ネットワーク上で交換するための汎用アセットを作成する処理チェーンコードを構築します。

### 依存関係
`import` ステートメントは、チェーンコードの作成に必要な依存関係をリストします。
1. `fmt` - デバッグ/ロギング用の `Println` が含まれます。
2. `errors` - 標準的な Go エラー形式。
3. `github.com/hyperledger/fabric/core/chaincode/shim` - Golang コードをネットワーク・ピアとインターフェース接続するコード。

### 値の引き渡し

以下のチェーンコード値が渡されます。
#### Init()
Init は、ネットワークに最初にデプロイされるときに呼び出され、チェーンコードを初期化します。この例では、`Init` を使用して、台帳で 1 つの変数の初期状態を構成します。

`chaincode_start.go` ファイルで、最初の `args` 要素をキー "hello_world" に保管するように `Init` 関数を以下のように変更します。

```go
func (t *SimpleChaincode) Init(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
	if len(args) != 1 {
		return nil, errors.New("Incorrect number of arguments. Expecting 1")
	}

	err := stub.PutState("hello_world", []byte(args[0]))
	if err != nil {
		return nil, err
	}

	return nil, nil
}
```

これは、シム関数 `stub.PutState` を使用して実行します。最初の引数は、ストリングとしてのキーであり、2 番目の引数はバイト配列としての値です。この関数は、エラーを返す場合があります (コードの検査でエラーが見つかった場合)。

#### Invoke()
トランザクション要求をチェーンに追加するために `Invoke` が呼び出されます。`Invoke` の構造は単純です。`function` 引数を受け取り、この引数に基づいてチェーンコードで Go 関数を呼び出します。

`chaincode_start.go` ファイルで、汎用の write 関数を呼び出すように `Invoke` 関数を以下のように変更します。

```go
func (t *SimpleChaincode) Invoke(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
	fmt.Println("invoke is running " + function)

	// Handle different functions
	if function == "init" {
		return t.Init(stub, "init", args)
	} else if function == "write" {
		return t.write(stub, args)
	}
	fmt.Println("invoke did not find func: " + function)

	return nil, errors.New("Received unknown function invocation")
}
```

ここで、コードは `write` を探しているので、この関数を `chaincode_start.go` ファイルに以下のように追加します。

```go
func (t *SimpleChaincode) write(stub *shim.ChaincodeStub, args []string) ([]byte, error) {
	var name, value string
	var err error
	fmt.Println("running write()")

	if len(args) != 2 {
		return nil, errors.New("Incorrect number of arguments. Expecting 2. name of the variable and value to set")
	}

	name = args[0]                            //rename for fun
	value = args[1]
	err = stub.PutState(name, []byte(value))  //write the variable into the chaincode state
	if err != nil {
		return nil, err
	}
	return nil, nil
}
```

この `write` 関数は、先ほどの `Init` の変更と同じように見えます。これで、`PutState` にキーと値を設定できます。これにより、ブロックチェーン台帳に任意のキー/値のペアを保管できるようになります。

#### Query()
`Query` は、チェーンコードの状態を照会するために呼び出され、チェーンにはブロックを追加しません。deploy 関数と invoke 関数だけが新規ブロックを追加します。`Query` を使用して、チェーンコード状態のキー/値のペアの値を読み取ります。

`chaincode_start.go` ファイルで、汎用の read 関数を呼び出すように `Query` 関数を以下のように変更します。

```go
func (t *SimpleChaincode) Query(stub *shim.ChaincodeStub, function string, args []string) ([]byte, error) {
	fmt.Println("query is running " + function)

	// Handle different functions
	if function == "read" {                            //read a variable
		return t.read(stub, args)
	}
	fmt.Println("query did not find func: " + function)

	return nil, errors.New("Received unknown function query")
}
```

ここで、コードは `read` を探しているので、この関数を `chaincode_start.go` ファイルに以下のように追加します。

```go
func (t *SimpleChaincode) read(stub *shim.ChaincodeStub, args []string) ([]byte, error) {
	var name, jsonResp string
	var err error

	if len(args) != 1 {
		return nil, errors.New("Incorrect number of arguments. Expecting name of the var to query")
	}

	name = args[0]
	valAsbytes, err := stub.GetState(name)
	if err != nil {
		jsonResp = "{\"Error\":\"Failed to get state for " + name + "\"}"
		return nil, errors.New(jsonResp)
	}

	return valAsbytes, nil
}
```

この `read` 関数は、`PutState` を補う `GetState` を使用します。このシム関数は、取得するキーの名前である 1 つのストリング引数だけを取ります。次に、この関数は値をバイト配列として `Query` に返し、Query はそれを REST ハンドラーに送信します。

#### Main()
`main` 関数は、各ピアがチェーンコードのインスタンスをデプロイするときに実行されます。この関数はチェーンコードを開始し、ピアに登録します。'main' ではコードの更新は不要です。chaincode_start.go と chaincode_finished.go のどちらのファイルの先頭にも `main` 関数が以下のように含まれます。

```go
func main() {
	err := shim.Start(new(SimpleChaincode))
	if err != nil {
		fmt.Printf("Error starting Simple chaincode: %s", err)
	}
}
```

### チェーンコードとの対話
チェーンコードをテストする最も早い方法は、ピアで REST インターフェースを使用することです。
Bluemix ダッシュボード・モニターで Swagger UI を使用することにより、追加コードを作成しなくてもデプロイ・チェーンコードを試行することができます。  

<br>
#### Swagger API
Swagger API を使用するには、以下の手順に従ってください。

1. [Bluemix](https://console.ng.bluemix.net/login) にログインし、**「ダッシュボード」**タブで作業していることを確認します。
1. IBM Blockchain サービスが含まれている同じ Bluemix「スペース」で作業していることを確認します。スペース・ナビゲーションは左側にあります。
1. 下部に**「サービス (Services)」**パネルがあります。IBM Blockchain サービスをクリックします。
1. 「IBM Blockchain へようこそ... (Welcome to the IBM Blockchain...)」メッセージが表示されます。右側の**「起動 (LAUNCH)」**ボタンをクリックします。
1. モニター・ページに 2 つの表が表示されます。下の表は空である場合があります。
	- **「ネットワーク」タブ:**
		- **ピア・ログ**は上の表にあります。**ピア 1** の行で、ファイル・アイコンをクリックしてログを表示します。この静的ビューに加えて、ページの上部近くの**「ログの表示 (View Logs)」**タブにライブの**ストリーミング・ピア・ログ**があります。
		- **チェーンコード・ログ**は下の表にあります。各チェーンコードは、デプロイ時に返されたチェーンコード・ハッシュでラベル付けされています。任意のチェーンコード行でピアを選択してから、ファイル・アイコンをクリックしてログを表示します。
	- **「API」タブ**: Swagger API の資料ページを表示します。
1. 以下の手順を実行して、セキュアな登録を実装します。`/chaincode` エンドポイントを REST インターフェースで呼び出すには、セキュアなコンテキスト ID が必要です。多くの REST 呼び出しを受け入れるには、登録された *enrollID* をサービス資格情報リストから以下のように渡す必要があります。
  - **「+ ネットワークの登録 ID (+ Network's Enroll IDs)」**をクリックして、*enrollID* 値と機密事項のリストを展開します。
  - 後で使用するために、資格情報のセットをテキスト・ファイルにコピーします。
  - 「**Registrar** API」セクションを展開します。
  - `「POST /registrar」`セクションを展開します。
  - ``Value`` フィールドに、資格情報の ``enrollID` と `enrollSecret' を指定する JSON を設定します。

  ![登録の例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/registrar.PNG "登録の例")

  *応答本文*は以下の例のようになります。

  ![登録の例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/register_response.PNG "登録例の応答本文")

`enrollID` をセットアップしたので、以下のステップでチェーンコードをデプロイ、呼び出し、照会するときにこの ID を使用できます。
### チェーンコードのデプロイ
REST インターフェースを介してチェーンコードをデプロイするには、チェーンコードをパブリックの GitHub リポジトリーに保管する必要があります。デプロイ要求をピアに送信するときに、チェーンコード・リポジトリーの URL と、チェーンコードを初期化するパラメーターを指定する必要があります。

チェーンコードを**デプロイする前に**、それがローカルで作成されていることを以下のように確認します。
1. コマンド・プロンプトを開き、`chaincode_start.go` が入っているディレクトリーを参照します。以下のコマンドを入力します。
	```
	go build ./
	```
1. 「**Chaincode** API」セクションを展開します。
1. 「`POST /chaincode`」セクションを展開します。
1. 以下のサンプルを使用して `DeploySpec` テキスト・フィールドを設定し (他のフィールドはブランクにする)、チェーンコード・リポジトリー・パスと直前の `/registrar` ステップの `enrollID` を指定します。`"path":` は `"https://github.com/johndoe/learn-chaincode/finished"` のように表示されます。これは、リポジトリー fork のパス、さらに chaincode_finished.go ファイルのパスになります。

	```
	{
		"jsonrpc": "2.0",
		"method": "deploy",
		"params": {
			"type": 1,
			"chaincodeID": {
				"path": "https://github.com/ibm-blockchain/learn-chaincode/finished"
			},
			"ctorMsg": {
				"function": "init",
				"args": [
					"hi there"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 1
	}
	```

  *応答本文*は以下の例のようになります。

  ![デプロイ例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/deploy_response.PNG "デプロイ例の応答本文")

  デプロイメントの応答には、このチェーンコードの ID が含まれます。ID は 128 文字の英数字ハッシュであり、将来の呼び出し要求または照会要求で使用できます。この ID はテキスト・エディターにコピーしておいてください。

#### 照会
`Init` 関数を使用して設定した `hello_world` キーの値に対してチェーンコードを照会します。
1. 「**Chaincode** API」セクションを展開します。
1. 「`POST /chaincode`」セクションを展開します。
1. 以下のサンプルを使用して `QuerySpec` テキスト・フィールドにデータを設定し (他のフィールドはブランクにする)、直前のデプロイメント手順のチェーンコード ID と直前の `/registrar` ステップの `enrollID` を指定します。

	```
	{
		"jsonrpc": "2.0",
		"method": "query",
		"params": {
			"type": 1,
			"chaincodeID": {
				"name": "CHAINCODE_HASH_HERE"
			},
			"ctorMsg": {
				"function": "read",
				"args": [
					"hello_world"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 2
	}
	```
  応答本文は以下の例のようになります。

  ![照会例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query_response.PNG "照会例の応答本文")

  `hello_world` の値は、直前のデプロイ呼び出しの本文によって設定された "hi there" です。

#### 呼び出し
`invoke` を使用して汎用の write 関数を呼び出します。`hello_world` の値を以下のように "go away" に変更します。
1. 「**Chaincode** API」セクションを展開します。
1. 「`POST /chaincode`」セクションを展開します。
1. 以下のサンプルを使用して `InvokeSpec` テキスト・フィールドにデータを設定し (他のフィールドはブランクにする)、直前のデプロイメント手順のチェーンコード ID と直前の `/registrar` ステップの `enrollID` を指定します。

	```
	{
		"jsonrpc": "2.0",
		"method": "invoke",
		"params": {
			"type": 1,
			"chaincodeID": {
				"name": "CHAINCODE_HASH_HERE"
			},
			"ctorMsg": {
				"function": "write",
				"args": [
					"hello_world",
					"go away"
				]
			},
			"secureContext": "user_type1_xxxxxxxxx"
		},
		"id": 3
	}
	```
  応答本文は以下の例のようになります:

  ![呼び出し例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG "呼び出し例の応答本文")

  上記の照会を再実行すると、以下の応答を受けるはずです。

  ![Query2 例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG "呼び出し例の応答")

これで、一部の基本的なチェーンコードが作成されました。  

<br>
## Marbles、Commercial Paper、Car Lease のデモの要件
{: #requirements}

以下の前提条件は、Marbles、Commercial Paper、Car Lease アプリケーションをローカルに実行するための Bluemix サービスに含まれています。Bluemix 環境は、Hyperledger Fabric を複製して以下の依存関係を提供します。

- Bluemix ID https://console.ng.bluemix.net/ (IBM Blockchain ネットワークを作成し、ピアと認証局用のサービス資格情報を提供するのに必要)
- Node.js 0.12.0+ と npm v2+
- Golang 環境 (独自のチェーンコードを作成する場合にのみ必要)

デモでは Node.js とエクスプレス・モジュールに精通している必要があります。ブロックチェーン・コンテキストにおける「チェーンコード」、「台帳」、「ピア」の概念についても理解している必要があります。「[Hyperledger Fabric 用語集](https://github.com/hyperledger/fabric/blob/master/docs/glossary.md)」を参照してください。  

<br>
## Marbles デモの使用
{: #marbles}

Marbles アプリケーションは、2 つのパーティー間での単純なアセットの転送を例示しています。このアプリケーションは、JavaScript SDK をテストし、その開発をガイドし、開発者が SDK やチェーンコードに習熟するために用意されたものです。

Web アプリケーション、SDK、チェーンコードが連携する方法については、「[Marbles チュートリアル](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md)」を参照してください。チェーンコードと IBM Blockchain にすでに精通している場合は、デモを Bluemix に[手動でデプロイ](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#)するか、「Bluemix にデプロイ」ボタンをクリックして Web アプリケーションを使用することができます。
  
[![Bluemixにデプロイ](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)(https://bluemix.net/deploy/button.png)]  

<br>
## Commercial Paper デモの使用
{: #commercialpaper}

Commercial Paper アプリケーションは、コマーシャル・ペーパーの取引ネットワークを IBM Blockchain を使用して実装する方法を示します。Commercial Paper デモは、役割とそれに対応するアクセス・レベルが参加者に割り当てられている、許可されたブロックチェーン・ネットワークを探索します。「[Commercial Paper README](https://github.com/IBM-Blockchain/cp-web#readme)」にアクセスしてこのデモのコンポーネントについて調べるか、すぐに Bluemix にデプロイして取引ネットワークを実際に表示します:   
[![Bluemix にデプロイ](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)(https://bluemix.net/deploy/button.png)]  

<br>
## Car Lease デモの使用
{: #carlease}

Car Lease アプリケーションは、自動車のライフサイクル、つまり、製造されてから一連の所有者の手に渡り、車両がスクラップされるまでを例示しています。このデモは、サーバー・サイド・プログラムには Node.js を使用し、IBM Blockchain ネットワークで実行するチェーンコードには Golang を使用します。デモには、チェーンコードの 2 つのインスタンスが含まれています。1 つは車両取り引きのルールを定義し、もう 1 つは存続期間中のすべての車両取り引きをログに記録します。どちらのチェーンコード・プログラムも JSON オブジェクトを使用してデータを保管します。「[Car Lease README](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)」にアクセスしてこのデモに関連したアプリケーション・アーキテクチャーと車両属性について調べるか、デモをすぐに Bluemix にデプロイします:   
[![Bluemix にデプロイ](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)(https://bluemix.net/deploy/button.png)]  

<br>
## 非決定論的チェーンコード
{: #ndcc}

IBM Blockchain ネットワークは決定論的なチェーンコードのみをサポートします。非決定論的なチェーンコードの使用はサポートされておらず、どのブロックチェーン・ネットワークでも重大エラーが発生します。

**非決定論的チェーンコード**とは、時間が経過しても、ノード間のブロックチェーン台帳で同じ値が付加**されない**あらゆるチェーンコードです。これとは対照的に、**決定論的チェーンコード**では、時間が経過しても、ノード間のブロックチェーン台帳で常に同じ値が付加されます。

### 決定論的チェーンコードの例
常に 1 つずつ変数の値が増分される **invoke** トランザクションは決定論的です。すべてのノードで結果は常に同じであり、差異はないためです。このトランザクションが固定値 5 に対して実行されると、付加される値はすべてのノードで常に 6 になります。決定論的なチェーンコードのネットワークの成果については、ブロックチェーン内で不一致はありません。各ノードの台帳のコピーは常に、値が (同期後に) 前の呼び出しよりも 1 大きくなっていることを示します。

### 非決定論的チェーンコードの例
ブロックチェーン変数の値を一日の始まり (00:00) からの経過秒数で増分する **invoke** トランザクションは非決定論的です。時間の経過とともにノード間で値が変化するためです。例えば、このトランザクションが固定値 5 に対して実行されるたびに、付加される値はノード間で異なります (まれに例外があります)。これは、00:00 からの経過秒数が必然的に変化するためです。この非決定論的チェーンコードのネットワーク結果は、それぞれ異なるブロックチェーンです。すべてのノードは、5 に 00:00 からの経過秒数を加えた値とは一致しません。

### ランダム性
チェーンコードは、時間が経過しても、ノード間で付加される値にランダム性がないことが求められます。何らかのランダム性が存在すると、ノード間でブロックチェーンが異なってしまい、これはネットワークで解決される必要があります。ランダム性を回避するには、並列チェーンコードが呼び出しチェーンコードからの入力値に影響を及ぼさないようにする必要があります。例えば、並列照会によってノード間の呼び出し値に差異が生じる可能性があるため、**query** トランザクションを **invoke** トランザクションと並行して実行しないでください。

### グローバル変数の使用
グローバル変数またはインスタンス変数を使用して、台帳から取得した値を保管したり、台帳に値を設定したりすると、非決定論的になる可能性があります。チェーン・コードは、チェーン・コード・コンテナーの再始動において状態を維持しないグローバル変数またはインスタンス変数に依存すべきではありません。以下の例ではグローバル変数を使用しています。`stub.PutState` 関数によって台帳に書き込まれる `key` の値は、グローバル変数から派生しています。

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### 1 つのマップ・タイプに対する反復
1 つのマップ・タイプに対する反復は、非決定論的になる可能性があります。これは、Go プログラミング言語において順序が決定論的ではないためです。以下に、`columnTypes` というマップに対する反復の例を示します。

```go
 func generateColumns(colTypes map[string]string, colKeys []bool) ([]*shim.ColumnDefinition, error) {
	var tableColumns []*shim.ColumnDefinition
	keyIndex := 0
	for k, _ := range colTypes {
		tableColumns = append(tableColumns, &shim.ColumnDefinition{k, shim.ColumnDefinition_STRING, colKeys[keyIndex]})

		keyIndex++
	}
	return tableColumns, nil
}
```

<!---## Using the Node.js SDK
{: #nodesdk}

Use the [Hyperledger fabric client SDK ](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md) library for easier interaction with an IBM Blockchain network.  The SDK, through importing packages and libraries, allows for an application developer to build Node.js applications that can invoke functionality on the blockchain network from the client side.  Member services and asset management are now pluggable components on client side applications.  See the [Enhanced Node.js SDK](etn_sdk.html) section for full documentation and application examples.--->
