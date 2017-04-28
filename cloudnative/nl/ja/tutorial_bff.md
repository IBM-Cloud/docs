---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# BFF ベーシック・スターターのエンドツーエンド・チュートリアル
{: #tutorial}

以下のエンドツーエンド・チュートリアルでは、インストールしておく必要があるツールを含め、BFF ベーシック・スターターからプロジェクトを作成するための手順を段階的に説明し、その後に、プロジェクト・コードの実行手順を説明します。

プロジェクトを作成するには、Web ベースの [{{site.data.keyword.dev_console}}](#create-devex) を使用する方法と、コマンド駆動型 [{{site.data.keyword.dev_cli_notm}}](#create-cli) を使用する方法があります。

## 開発者ツールのインストール
{: #dev_tools}

[前提条件の開発者ツール ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](get_code.html#prereq-dev-tools){: new_window} をインストール済みであることを確認します。


## {{site.data.keyword.dev_console}} を使用したプロジェクトの作成
{: #create-devex}

1. {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} でプロジェクトを作成します。

	1. {{site.data.keyword.dev_console}} 内の [**「開始」** ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/developer/getting-started/) ページから**「プロジェクトの作成」**をクリックします。

		代替方法として、**「プロジェクト」**ページから**「プロジェクトの作成」**をクリックすることもできます。

	2. **「Backend for Frontend」**を選択して**「次へ」**をクリックします。

	3. **「ベーシック・バックエンド (Basic Backend)」**を選択し、**「次へ」**をクリックします。

	4. プロジェクト名を入力します。このチュートリアルでは、`BFFProject` を使用します。   

	5. 固有のホスト名を入力してください。このチュートリアルでは、`devhost` を使用します。 

	6. 言語プラットフォームを選択します。このチュートリアルでは、`Node` を使用します。
   
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

4. ダウンロードされたプロジェクトの処理を開始します。

	1. アーカイブされたファイルを解凍します。
	
	2. 新規プロジェクト・ディレクトリーにナビゲートします。
	
	3. {{site.data.keyword.dev_cli_notm}} を使用して処理を続行します。

5. オプション: 新しい言語を生成するために[プロジェクトを更新します](project_overview_page.html#update_language)。


## {{site.data.keyword.dev_cli_notm}} を使用したプロジェクトの作成
{: #create-cli}

1. [{{site.data.keyword.dev_cli_short}}](dev_cli.html) がインストールされていることを確認します。

2. 端末のプロンプトで、使用するローカル・ディレクトリーにナビゲートし、以下のコマンドを実行します。
  
	```
	bx dev create
	```
	{: codeblock}
	
3. プロンプトが出されたら、以下の値を入力します。

	* パターンの選択: 3 (Backend for Frontend)
	* スターターの選択: 1 (ベーシック・バックエンド)
	* 言語の選択: 1 (Node)
	* プロジェクト名の入力: `BFFProjectCLI`
	* プロジェクトのホスト名の入力: `myhost`

4. プロジェクトにサービスを追加する場合は、該当の質問のプロンプトで `y` を入力し、残りの質問に答えます。

5. `BFFProjectCLI` が正常に保存されたら、`BFFProjectCLI` フォルダーにナビゲートします。

6. 独自のコードを追加し、プロジェクトを実行します。
 
	1. 以下のコマンドを使用してプロジェクトを実行します。

 		```
		bx dev run
		```
		{: codeblock}


## BFF プロジェクトの実行
{: #running-bff}

### ローカルの場合
{: #bff-local}

1. サーバーをコンパイルします。

  ```
  swift build
  ```
  {: codeblock}

2. アプリケーションを実行します。例えば、アプリケーションの名前が `MyServer` の場合、以下のようにします。

  ```
  .build/debug/MyServer
  ```
  {: codeblock}

3. `curl http://localhost:8080` により、サーバーで curl を実行できます。


### Bluemix プラグインを使用する場合
{: #using-blumix}

1. コンパイルを実行します。

	```
	bx dev run
	```
	{: codeblock}

2. 以下により、サーバーで curl を実行できます。
  
	```
	curl http://localhost:8080
	```
	{: codeblock}
