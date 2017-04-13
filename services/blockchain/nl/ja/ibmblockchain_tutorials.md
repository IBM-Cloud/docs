---

copyright:
  years: 2016
lastupdated: "2016-11-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# サンプル・アプリとチュートリアル
{: #1stanchor}


以下のサンプルは、アプリケーションとチェーンコードがテスト用の IBM Blockchain ネットワークでどのように機能するかを示しています。IBM Blockchain ネットワークの基礎になっている Hyperledger Fabric v0.6 コードの詳細については、Linux Foundation Hyperledger Project の [Fabric Docs](https://github.com/hyperledger/fabric/tree/v0.6/docs) を参照してください。  
{:shortdesc}

チェーンコード・アプリケーションの動作を実際に試してみるには、以下の Marbles、Commercial Paper、または Car Lease のデモをすぐにデプロイできます (「Bluemix にデプロイ」ボタンをクリックします)。または、「チェーンコードへようこそ (Hello Chaincode)」チュートリアルを読み進めます。

- [![Bluemix にデプロイ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  **Marbles**
- [![Bluemix にデプロイ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  **Commercial Paper**
- [![Bluemix にデプロイ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  **Car Lease**  

<br>
## チェーンコード学習チュートリアル
{: #hellocc}
このチュートリアルでは、基本的なビルディング・ブロックを使用して基本的なチェーンコード・アプリケーションをコーディングする方法について説明します。ネットワーク上で交換するための汎用アセットを作成する処理チェーンコードを増分ビルドします。次に、ネットワーク API を介してチェーンコードと対話します。このチュートリアルを完了すると、以下の質問に答えることができるようになります。
- チェーンコードとは何ですか。
- チェーンコードはどのように実装しますか。
- どのような依存関係が存在しますか。
- 主な関数には何がありますか。
- さまざまな値を引数に渡すにはどうすればよいですか。
- ユーザーを自分のネットワークにセキュアな方法で登録するにはどうすればよいですか。
- チェーンコードはどのようにコンパイルしますか。
- REST API を介してチェーンコードとどのように対話できますか。

### チェーンコードとは何ですか。
チェーンコードは、ユーザーがブロックチェーン・ネットワークと対話できるようにするための Go (Golang) コードまたは Java コードです。ネットワークのトランザクションを「呼び出す」と、台帳に対して値を読み書きする関数をチェーンコードで呼び出していることになります。  

<br>
## 開発環境のセットアップ
チェーンコードの開発を始めるには、まず、以下の依存関係と推奨ツールをインストールします。

### Git

- [Git のダウンロード・ページ](https://git-scm.com/downloads)
- [Pro Git のブック](https://git-scm.com/book/en/v2)
- [Git Desktop (Git CLI の代替ツール)](https://desktop.github.com/)

Git は、チェーンコード開発とソフトウェア開発全般に対応した高速で強力なバージョン管理ツールです。Windows 版の Git と一緒にインストールされる Git bash が、推奨されるコマンド・ライン端末です。

Git のインストールが完了したら、Git がインストールされていることを確認します。

```
$ git version
git version 2.9.0.windows.1
```

Git をインストールしたら、[GitHub](https://github.com/) で自分のアカウントを作成します。Bluemix の IBM Blockchain サービスでは、チェーンコードを GitHub リポジトリーに格納して、REST API でデプロイする必要があります。  

## Go

現在、Go は Bluemix でチェーンコードの作成に使用できる唯一の言語です。Go のインストールには、チェーンコードの作成に便利な CLI ツール・セットが含まれています。例えば、`go build` コマンドを使用すれば、チェーンコードをネットワークにデプロイする前にコンパイルできます。Go v1.6 (Hyperledger Fabric v0.6 の開発に使用されたバージョン) をインストールしてください。  

- [Go 1.6 のインストール](https://golang.org/dl/#go1.6.3)
- [Go のインストール手順](https://golang.org/doc/install)
- [Go の資料とチュートリアル](https://golang.org/doc/)

以下のコマンドを実行して、Go が正しくインストールされていることを確認してください。`go version` コマンドの出力は、オペレーティング・システムによって異なります。

```
$ go version
go version go1.6.3 windows/amd64

$ echo $GOPATH
C:\gopath
```

上の例と同じ `GOPATH` 環境変数を使用する必要はありませんが、ファイル・システムの有効なディレクトリーを使用する必要があります。チェーンコードのコンパイルを確認するために `go build` を実行すると、Go は、チェーンコードの `import` ブロックにリストされている非標準の依存関係が `$GOPATH/src` ディレクトリーにあるかどうかを調べます。GOPATH 環境変数のセットアップ方法は、[Go のインストール手順](https://golang.org/doc/install)で説明されています。  

<br>
## Hyperledger Fabric

Blockchain on Bluemix では、Hyperledger Fabric の 2 つのバージョン (v0.5 と v0.6) がサポートされています。以下で説明するように、使用するチェーンコードのバージョンは、Bluemix ネットワークの Hyperledger のバージョンに適合していなければなりません。

重要:
1. 台帳の読み書きの機能を有効にするには、チェーンコードによって Hyperledger Fabric からチェーンコード・シムをインポートしなければなりません。
2. ローカルでチェーンコードをコンパイルするには、`GOPATH` 環境変数に Hyperledger Fabric コードの場所を指定しておく必要があります。

Bluemix インスタンスで実行している Hyperledger Fabric のバージョンを確認するには、ダッシュボード・モニターの**「サービス状況」**タブをクリックします。**「リリース・ノート」**セクションまでスクロールダウンすると、`「ネットワークで使用しているバージョン (Your network is using this version)」`パネルに、実行している **Hyperledger コミット・レベル**が表示されます。

![Bluemix のバックエンドのバージョン](images/fabricversion.png "Bluemix のバックエンドのバージョン")
図 1. Hyperledger Fabric のバージョン

チェーンコードのバージョンは、チェーンコードのデプロイ先の Hyperledger Fabric のバージョンに適合していなければなりません。例えば、図 1 のネットワークでは、Hyperledger Fabric v0.6 プレビューのコードベースを複製する必要があります。いずれかのバージョンの Fabric コードベースを `$GOPATH/hyperledger/fabric` のパスに格納しておかなければなりません。

- [v0.5 Hyperledger Fabric](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview)
- [v0.6 HHyperledger Fabric](https://gerrit.hyperledger.org/r/gitweb?p=fabric.git;a=shortlog;h=refs/heads/v0.6)

Hyperledger Fabric v0.5 コードベースをインストールするには、以下の git clone コマンドを使用します。

```
# Create the parent directories on your GOPATH
mkdir -p $GOPATH/src/github.com/hyperledger
cd $GOAPTH/src/github.com/hyperledger

# Clone the appropriate release codebase into $GOPATH/src/github.com/hyperledger/fabric
# Note that the v0.5 release is a branch of the repository.  It is defined below after the -b argument
git clone -b v0.5-developer-preview https://github.com/hyperledger-archives/fabric.git
```

Hyperledger Fabric v0.6 コードベースをインストールするには、以下の git clone コマンドを使用します。

```
# The v0.6 release exists as a branch inside the Gerrit fabric repository
git clone -b v0.6 http://gerrit.hyperledger.org/r/fabric
```

Fabric が `GOPATH` に正しくインストールされていないと、チェーンコードのビルド時に以下の例のようなエラーが返されます。
```
$ go build .
chaincode_example02.go:27:2: cannot find package "github.com/hyperledger/fabric/core/chaincode/shim" in any of:
        C:\Go\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOROOT)
        C:\gopath\src\github.com\hyperledger\fabric\core\chaincode\shim (from $GOPATH)
```

### 開発パイプラインのセットアップ

以下の手順を使用して、チェーンコードの作成、ビルド、テストを行うパイプラインをセットアップできます。ローカル・マシンでチェーンコードを作成し、コンパイルを確認して、GitHub にアップロードします。その後、Fabric REST API を使用して、Bluemix ネットワークにチェーンコードをデプロイしてテストします。

1. ネットワークのバージョンに適切なバージョンの[チェーンコード学習](https://github.com/IBM-Blockchain/learn-chaincode)リポジトリーを GitHub アカウントにフォークします。v0.5 Fabric ネットワークでは v1.0 をフォークし、v0.6 Fabric ネットワークでは v2.0 をフォークしてください。リポジトリー・ページの右上の**「フォーク」**ボタンを使用するのも 1 つの方法です。フォークにより、ページの左上の**「ブランチ:」**ボタンをクリックすると表示されるすべてのブランチを含め、リポジトリー全体がローカル・マシンにコピーされます。CLI を使用してフォークする場合は、Git Bash シェルに以下のコマンドを入力します。

2. フォークを $GOPATH に複製します。

  ```bash
  cd $GOPATH
  mkdir -p src/github.com/<YOUR_GITHUB_ID_HERE>/
  cd src/github.com/<YOUR_GITHUB_ID_HERE>/
  git clone -b v1.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  OR
  git clone -b v2.0 https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode.git
  ```

  これで、ローカル・マシンにフォークのコピーが配置されました。ローカル・ファイルを変更したり追加したりしてチェーンコードを作成し、GitHub 上のフォークにプッシュしてから、ネットワーク・ピアで REST API を使用してチェーンコードをブロックチェーン・ネットワークにデプロイします。

3. このチュートリアルで使用する 2 つのバージョンのチェーンコードが用意されています。作業の開始点になるスケルトン・チェーンコードである **start** と、ビルドできる状態の完成版のチェーンコードである **finished* です。まず、ローカル環境で **start** によるビルドを確かめてみましょう。

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/start
  go build ./
  ```

**start** バージョンの learn-chaincode がエラーもメッセージも出さずにコンパイルされるはずです。そうならない場合は、前述の Go の正しいインストール手順を確認してください。

5. ローカル・チェーンコード・ファイルに変更を書き込み、更新後のファイルを GitHub フォークにプッシュします。

  ```bash
  cd $GOPATH/src/github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/
  # See what files have changed locally.  You should see chaincode_start.go
  git status
  # Stage all changes in the local repository for commit
  git add --all
  # Commit all staged changes.  Insert a short description after the -m argument
  git commit -m "Compiled my code"
  # Push local commits back to https://github.com/<YOUR_GITHUB_ID_HERE>/learn-chaincode/
  git push
  ```

#### チェーンコード・インターフェースの実装
次に、Go コードでチェーンコード・シム・インターフェースを実装します。主な関数は、**Init**、**Invoke**、**Query** の 3 つです。この 3 つの関数はどれも関数名と文字列配列を入力として取りますが、別々の時点で呼び出されます。ブロックチェーン・ネットワークで交換するために汎用アセットを作成する正常なチェーンコードができたら、開発パスは終わりです。

### 依存関係
`import` ステートメントを実行すると、チェーンコードをビルドするために必要な依存関係がリストされます。
1. `fmt` - デバッグ/ロギング用の `Println` が含まれます。
2. `errors` - 標準的な Go エラー形式。
3. `github.com/hyperledger/fabric/core/chaincode/shim` - Golang コードをネットワーク・ピアとインターフェース接続するコード。

#### Init()
チェーンコードを初めてデプロイするときには、`Init` 関数を呼び出します。名前のとおり、この関数は、チェーンコードを初期化するために使用します。この例では、`Init` によって、台帳の 1 つのキー/値ペアの初期状態を構成します。

`chaincode_start.go` ファイルで、`Init` 関数を以下のように変更して、最初の `args` 要素をキー "hello_world" に保管するようにします。

```go
func (t *SimpleChaincode) Init(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
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

この処理のために、スタブ関数 `stub.PutState` を使用します。この関数は、デプロイメント要求で送信された最初の引数を、'hello_world' キーの下に保管する値と解釈します。引数の数が誤っていたり台帳への書き込みに問題があったりしてエラーが発生すると、この関数からエラーが返されます。そうでなければ、クリーンな状態で終了し、メッセージは返されません。  

#### Invoke()
`Invoke` 関数を使用して、ブロックチェーン・ネットワークで「実際の処理」を実行するチェーンコード関数を呼び出します。Invoke 関数はトランザクションとして取り込まれ、台帳に書き込むブロックとしてグループ化されます。台帳の更新は、チェーンコードの呼び出しによって行います。`Invoke` の構造はシンプルです。関数と引数の配列を受け取ります。`Invoke` は、呼び出し要求で関数パラメーターによって渡された関数に基づき、ヘルパー関数を呼び出すか、エラーを返します。

`chaincode_start.go` ファイルで、`Invoke` 関数を以下のように変更して、汎用の write 関数を呼び出します。

```go
func (t *SimpleChaincode) Invoke(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
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

ここで、コードは `write` を探すので、write 関数を `chaincode_start.go` ファイルに追加してください。

```go
func (t *SimpleChaincode) write(stub shim.ChaincodeStubInterface, args []string) ([]byte, error) {
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
`Query` 関数を呼び出して、チェーンコードの状態を照会します。この関数によってブロックがチェーン (台帳) に追加されることはありません。deploy 関数と invoke 関数だけが新規ブロックを追加します。`Query` は、チェーンコード状態のキー/値のペアの値を読み取るために使用します。

`chaincode_start.go` ファイルで、`Query` 関数を以下のように変更して、汎用の read 関数を呼び出すようにします。

```go
func (t *SimpleChaincode) Query(stub shim.ChaincodeStubInterface, function string, args []string) ([]byte, error) {
	fmt.Println("query is running " + function)

	// Handle different functions
	if function == "read" {                            //read a variable
		return t.read(stub, args)
	}
	fmt.Println("query did not find func: " + function)

	return nil, errors.New("Received unknown function query")
}
```

ここで、コードは `read` を探すので、read 関数を `chaincode_start.go` ファイルに追加してください。

```go
func (t *SimpleChaincode) read(stub shim.ChaincodeStubInterface, args []string) ([]byte, error) {
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

この `read` 関数は、`PutState` を補う `GetState` を使用します。このシム関数は、取得するキーの名前である文字列引数を 1 つだけ取ります。次に、この関数は値をバイト配列として `Query` に返し、Query はそれを REST ハンドラーに送信します。

#### Main()
`main` 関数は、各ピアがチェーンコードのインスタンスをデプロイするときに実行されます。この関数はチェーンコードを開始し、ピアに登録します。'main' ではコードの更新は不要です。chaincode_start.go と chaincode_finished.go の両方のファイルで、以下の `main` 関数が先頭に含まれています。

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
Bluemix ダッシュボード・モニターで Swagger UI を使用することにより、追加コードを作成しなくてもチェーンコードのデプロイを試してみることができます。  

#### Swagger API
Swagger API を使用するには、以下の手順に従ってください。

1. [Bluemix](https://console.ng.bluemix.net/login) にログインし、**「ダッシュボード」**タブで作業していることを確認します。
1. IBM Blockchain サービスが含まれているのと同じ Bluemix「スペース」で作業していることを確認します。スペース・ナビゲーションは左側にあります。
1. 下部に**「サービス (Services)」**パネルがあります。IBM Blockchain サービスをクリックします。
1. 「IBM Blockchain へようこそ... (Welcome to the IBM Blockchain...)」メッセージが表示されます。右側の**「起動 (LAUNCH)」**ボタンをクリックします。
1. モニター・ページに 2 つの表が表示されます。下の表は空である場合があります。
	- **「ネットワーク」タブ:**
		- **ピア・ログ**は上の表にあります。**ピア 1** の行で、ファイル・アイコンをクリックしてログを表示します。この静的ビューに加えて、ページの上部近くの**「ログの表示 (View Logs)」**タブにライブの**ストリーミング・ピア・ログ**があります。
		- **チェーンコード・ログ**は下の表にあります。各チェーンコードは、デプロイ時に返されたチェーンコード・ハッシュでラベル付けされています。任意のチェーンコード行でピアを選択してから、ファイル・アイコンをクリックしてログを表示します。
	- **「API」タブ**: Swagger API の資料ページを表示します。
1. 以下の手順を実行して、セキュアな登録を実装します。`/chaincode` エンドポイントを REST インターフェースで呼び出すには、セキュアなコンテキスト ID が必要です。ほとんどの REST 呼び出しについて、その呼び出しが受け入れられるためには、登録された *enrollID* をサービス資格情報リストから以下のように渡す必要があります。
  - **「+ ネットワークの登録 ID (+ Network's Enroll IDs)」**をクリックして、*enrollID* 値と機密事項のリストを展開します。
  - 後で使用するために、資格情報のセットをテキスト・ファイルにコピーします。
  - **Registrar** API セクションを展開します。
  - `POST /registrar` セクションを展開します。
  - `Value` フィールドに、資格情報の `enrollID` と `enrollSecret' を指定する JSON を設定します。

  ![登録の例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/registrar.PNG "登録の例")

  *応答本文*は以下の例のようになります。

  ![登録の例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/register_response.PNG "登録例の応答本文")

`enrollID` をセットアップしたので、以下のステップでチェーンコードをデプロイ、呼び出し、照会するときにこの ID を使用できます。
### チェーンコードのデプロイ
REST インターフェースを介してチェーンコードをデプロイするには、チェーンコードをパブリックの GitHub リポジトリーに保管する必要があります。デプロイ要求をピアに送信するときに、チェーンコード・リポジトリーの URL と、チェーンコードを初期化するパラメーターを指定する必要があります。

チェーンコードを**デプロイする前に**、それがローカルでビルドできることを以下のように確認します。
1. コマンド・プロンプトを開き、`chaincode_start.go` が入っているディレクトリーを参照します。以下のコマンドを入力します。
	```
	go build ./
	```
1. **Chaincode** API セクションを展開します。
1. `POST /chaincode` セクションを展開します。
1. 以下のサンプル・コードを使用して `DeploySpec` テキスト・フィールドを設定し (他のフィールドはブランクにする)、チェーンコード・リポジトリー・パスと直前の `/registrar` ステップの `enrollID` を指定します。`"path":` は `"https://github.com/johndoe/learn-chaincode/finished"` のようになります。これは、リポジトリー fork のパス、さらに chaincode_finished.go ファイルのパスになります。

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
チェーンコードを照会し、`Init` 関数を使用して設定した `hello_world` キーの値を取得します。
1. **Chaincode** API セクションを展開します。
1. `POST /chaincode` セクションを展開します。
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
1. **Chaincode** API セクションを展開します。
1. `POST /chaincode` セクションを展開します。
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
  応答本文は以下の例のようになります。

  ![呼び出し例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/invoke_response.PNG "呼び出し例の応答本文")

  上記の照会を再実行すると、以下の応答が得られます。

  ![Query2 例](https://raw.githubusercontent.com/IBM-Blockchain/learn-chaincode/master/imgs/query2_response.PNG "呼び出し例の応答")

これで、基本的なチェーンコードの作成が完了しました。  

<br>
## デモの要件
{: #requirements}

Marbles、Commercial Paper、Car Lease の各デモ・アプリケーションを実行するには、前提条件として以下が必要です。これらは Bluemix サービスに含まれています。Bluemix 環境は、Hyperledger Fabric を複製して以下の依存関係を提供します。

- Bluemix ID https://console.ng.bluemix.net/ (IBM Blockchain ネットワークを作成し、ピアと認証局用のサービス資格情報を提供するのに必要)
- Node.js 0.12.0+ と npm v2+
- Golang 環境 (独自のチェーンコードを作成する場合にのみ必要)

これらのデモを実行するには、Node.js と express モジュールについて習熟している必要があります。ブロックチェーン・コンテキストにおける「チェーンコード」、「台帳」、「ピア」の概念についても理解している必要があります。「[Hyperledger Fabric 用語集](https://github.com/hyperledger/fabric/blob/v0.6/docs/glossary.md)」を参照してください。  

<br>
## Marbles デモ
{: #marbles}

Marbles アプリケーションは、2 つのパーティー間での単純なアセットの転送を例示しています。このアプリケーションは、JavaScript SDK をテストし、その開発をガイドし、開発者が SDK やチェーンコードに習熟するために用意されたものです。

Web アプリケーション、SDK、チェーンコードが連携する方法については、「[Marbles チュートリアル](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md)」を参照してください。チェーンコードと IBM Blockchain にすでに詳しい方は、デモを Bluemix に[手動でデプロイ](https://github.com/IBM-Blockchain/marbles/blob/master/tutorial_part1.md#)するか、「Bluemix にデプロイ」ボタンをクリックして Web アプリケーションを使用することができます。
  
[![Bluemix にデプロイ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/ibm-blockchain/marbles.git)  

<br>
## Commercial Paper デモ
{: #commercialpaper}

Commercial Paper アプリケーションは、コマーシャル・ペーパーの取引ネットワークを IBM Blockchain を使用して実装する方法を示します。Commercial Paper デモは、役割とそれに対応するアクセス・レベルが参加者に割り当てられている、許可されたブロックチェーン・ネットワークを探索します。「[Commercial Paper README](https://github.com/IBM-Blockchain/cp-web#readme)」にアクセスしてこのデモのコンポーネントについて調べるか、すぐに Bluemix にデプロイして取引ネットワークを実際に表示します:   
[![Bluemix にデプロイ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/cp-web.git)  

<br>
## Car Lease デモ
{: #carlease}

Car Lease アプリケーションは、自動車のライフサイクル、つまり、製造されてから一連の所有者の手に渡り、車両がスクラップされるまでを例示しています。このデモは、サーバー・サイド・プログラムには Node.js を使用し、IBM Blockchain ネットワークで実行するチェーンコードには Golang を使用します。デモには、チェーンコードの 2 つのインスタンスが含まれています。1 つは車両取り引きのルールを定義し、もう 1 つは存続期間中のすべての車両取り引きをログに記録します。どちらのチェーンコード・プログラムも JSON オブジェクトを使用してデータを保管します。「[Car Lease README](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)」にアクセスしてこのデモに関連したアプリケーション・アーキテクチャーと車両属性について調べるか、デモをすぐに Bluemix にデプロイします:   
[![Bluemix にデプロイ](https://bluemix.net/deploy/button.png)](https://bluemix.net/deploy?repository=https://github.com/IBM-Blockchain/car-lease-demo.git)  

<br>

<!-- comment out - moving to separate file for now jh
## Non-deterministic chaincode
{: #ndcc}

IBM Blockchain networks support deterministic chaincode only. Using non-deterministic chaincode is not supported, and will cause severe errors, on any blockchain network.

**Non-deterministic chaincode** is any chaincode that does **not** result in the same appended value, over time and across nodes, on the blockchain ledger. By contrast, **deterministic chaincode** always produces the same appended value, over time and across nodes, on the blockchain ledger.

### Deterministic chaincode example
An **invoke** transaction that always increments the value of a variable by one is deterministic, because the result is always the same, on every node, without variance. Whenever this transaction is run against a fixed value of five, for example, the appended value is always six, on every node, every time. The network outcome for deterministic chaincode is no divergence in the blockchain; the copy of the ledger on each node always indicates (after syncing) that the value is one greater than the previous invocation.

### Non-deterministic chaincode example
An **invoke** transaction that increments the value of a blockchain variable with the number of elapsed seconds since the start of the day (00:00) is non-deterministic, because over time the value will vary across nodes. Each time this transaction is run against a fixed value of five, for example, the appended value diverges across nodes (with rare exceptions), because the number of elapsed seconds since 00:00 will inevitably vary. The network outcome for this non-deterministic chaincode is divergent blockchains; all nodes will not agree on the value of five + the number of elapsed seconds since 00:00.

### Randomness
Chaincode must exhibit no randomness in the appended values, over time and across nodes. Any randomness produces divergent blockchains across nodes, which must then be resolved by the network. To avoid randomness, you must ensure that no parallel chaincode can affect the input value from invocation chaincode. For example, do not run any **query** transactions in parallel with **invoke** transactions, because parallel queries could produce variance in the invocation values across nodes.

### Using a global variable
Using a global or instance variable to store a value that was retrieved from the ledger, or to set a value on the ledger, can lead to non-determinism. Chaincode should not rely on global or instance variables that will not retain their state across restarts of a chaincode container. The following is an example that uses a global variable; the value of `key`, which is written to the ledger via the `stub.PutState` function, is derived from a global variable:

```go
//declare global variable
var INVOICE_COUNTER int64

//increment the counter and save the state
		INVOICE_COUNTER =INVOICE_COUNTER+1
		key := INVOICE+strconv.FormatInt(INVOICE_COUNTER, 10)
		ccLogger.Infof("The key formed for saving the state: %s", key)
		stub.PutState(key,[]byte(invoiceID))
```

### Iterating over a map type
Iteration over a map type can lead to non-determinism, because order is not deterministic in the Go programming language. The following is an example of iteration over the map named `columnTypes`:

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

-->


<!-- ## Using the Node.js SDK
{: #nodesdk}

Use the [Hyperledger fabric client SDK ](https://github.com/IBM-Blockchain/ibm-blockchain-js/blob/master/README.md) library for easier interaction with an IBM Blockchain network.  The SDK, through importing packages and libraries, allows for an application developer to build Node.js applications that can invoke functionality on the blockchain network from the client side.  Member services and asset management are now pluggable components on client side applications.  See the [Enhanced Node.js SDK](etn_sdk.html) section for full documentation and application examples. -->
