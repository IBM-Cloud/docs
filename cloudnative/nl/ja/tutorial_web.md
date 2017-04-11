---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Web ベーシック・スターターのエンドツーエンド・チュートリアル
{: #tutorial}

以下のエンドツーエンド・チュートリアルでは、インストールしておく必要があるツールを含め、Web ベーシック・スターターからプロジェクトを作成するための手順を段階的に説明し、その後に、プロジェクト・コードの実行手順を説明します。

## 開発者ツールのインストール
{: #dev_tools}

[前提条件の開発者ツール ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](get_code.html#prereq-dev-tools){: new_window} をインストール済みであることを確認します。


## {{site.data.keyword.dev_console}} を使用したプロジェクトの作成
{: #create-devex}

1. {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} でプロジェクトを作成します。

	1. {{site.data.keyword.dev_console}} の**「開始」**ページで**「プロジェクトの作成」**をクリックします。

		代替方法として、**「プロジェクト」**ページから**「プロジェクトの作成」**をクリックすることもできます。

	2. **「Web アプリ (Web App)」**を選択し、**「次へ」**をクリックします。

	3. **「ベーシック Web (Basic Web)」**を選択し、**「次へ」**をクリックします。

	4. プロジェクト名を入力します。このチュートリアルでは、`WebBasicProject` を使用します。   

	5. ホスト名を入力します。このチュートリアルでは、`devhost` を使用します。 

	6. 言語プラットフォームを選択します。このチュートリアルでは、`Swift` を使用します。
   
	7. **「作成」**をクリックします。

2. オプション: Data (データ) 機能を追加します。

	1. **「プロジェクト概要 (Project Overview)」**ページで、**「Data (データ)」**に対して**「表示」**をクリックします。

      代替方法として、**「機能 (Capabilities)」>「Data (データ)」**ページで**「作成」**または**「既存の追加 (Add Existing)」**を選択することもできます。

   2. サービス名を入力し、**「作成」**をクリックします。


3. プロジェクト・コードを生成します。

	1. **「プロジェクト概要 (Project Overview)」**ページで**「コードの取得 (Get the Code)」**をクリックして、言語を選択します。
   
		代替方法として、**「コード」**ページで以下をクリックすることもできます。
      
	2. **「コードの生成 (Generate Code)」**をクリックします。
   
	3. プロジェクト・コードの生成が完了したら、**「コードのダウンロード」**をクリックして、プロジェクトのアーカイブをダウンロードします。

4. オプション: 新しい言語を生成するために[プロジェクトを更新します](project_overview_page.html#update_language)。


## {{site.data.keyword.dev_cli_notm}} を使用したプロジェクトの作成
{: #create-cli}

1. [{{site.data.keyword.dev_cli_short}}](dev_cli.html) がインストールされていることを確認します。

2. 端末のプロンプトで、使用するローカル・ディレクトリーにナビゲートし、以下のコマンドを実行します。
  
	```
	bx dev create
	```
	{: codeblock}


3. プロンプトが出されたら、以下の値を入力します。

	* パターンの選択: 1 (Web)
	* スターターの選択: 1 (ベーシック Web)
	* 言語の選択: 2 (Swift)
	* プロジェクト名の入力: `WebBasicProjectCLI`
	* プロジェクトのホスト名の入力: `myhost`

4. プロジェクトにサービスを追加する場合は、該当の質問のプロンプトで `y` を入力し、残りの質問に答えます。

5. `WebBasicProjectCLI` プロジェクトが正常に保存されたら、`WebBasicProjectCLI` フォルダーにナビゲートします。

6. 独自コードの追加、プロジェクトのビルド、またはプロジェクトの実行を行います。
 
	1. 以下のコマンドを使用してプロジェクトをビルドします。
   
		```
 		bx dev build
 		```     
		{: codeblock}

	2. 以下のコマンドを使用してプロジェクトを実行します。
 
		```
		bx dev run
		```
		{: codeblock}


## Web プロジェクトの実行
{: #run}

### ローカルの場合
{: #local notoc}

1. ノードの依存関係をインストールします。

  ```
  npm install
  ```
  {: codeblock}

2. フロントエンド・コードをモジュールにバンドルします。

  ```
  node_modules/.bin/gulp
  ```
  {: codeblock}

3. サーバーをコンパイルします。

  ```
  swift build
  ```
  {: codeblock}

4. アプリケーションを実行します。

  ```
  .build/debug/WebBasicProjectCLI
  ```
  {: codeblock}

5. ブラウザーで `http://localhost:8080` を開きます。


### {{site.data.keyword.dev_cli_short}} の使用
{: #dev notoc}

1. ノードの依存関係をインストールします。

  ```
  npm install
  ```
  {: codeblock}

2. フロントエンド・コードをモジュールにバンドルします。

  ```
  gulp
  ```
  {: codeblock}

3. コンパイルを実行します。

  ```
  bx dev run
  ```
  {: codeblock}

4. ブラウザーで `http://localhost:8080` を開きます。


## Xcode でのプロジェクトの実行
{: #Xcode}

1. Xcode プロジェクトを作成します。

	Xcode で開発するには、その前に、Swift パッケージ・マネージャーを使用して Xcode プロジェクトをビルドする必要があります。
	
	```
	swift project generate-xcodeproj
	```
	{: codeblock}

2. アクティブ・ターゲットを該当の実行可能ファイルに変更します。

	次に、Xcode でプロジェクトを開き、アクティブ・ターゲットが該当の実行可能ファイルであることを確認します。オプション・キーを押したままドロップダウン・メニューをクリックすることで、目的のアクティブ実行可能ファイルを選択できます。

3. **「実行 (run)」**を押します。

4. ブラウザーで `http://localhost:8080` を開きます。

