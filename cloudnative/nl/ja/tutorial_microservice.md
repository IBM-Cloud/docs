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

# マイクロサービス・ベーシック・スターターのエンドツーエンド・チュートリアル
{: #tutorial}

以下のエンドツーエンド・チュートリアルでは、インストールしておく必要があるツールを含め、マイクロサービス・ベーシック・スターターからプロジェクトを作成するための手順を段階的に説明し、その後に、プロジェクト・コードの実行手順を説明します。

## 開発者ツールのインストール
{: #dev_tools}

[前提条件の開発者ツール ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](get_code.html#prereq-dev-tools){: new_window} をインストール済みであることを確認します。


## {{site.data.keyword.dev_console}} を使用したプロジェクトの作成
{: #create-devex}

1. {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} でプロジェクトを作成します。

	1. {{site.data.keyword.dev_console}} の**「開始」**ページで**「プロジェクトの作成」**をクリックします。

		代替方法として、**「プロジェクト」**ページから**「プロジェクトの作成」**をクリックすることもできます。

	2. **「マイクロサービス (Microservice)」**を選択し、**「次へ」**をクリックします。

	3. **「ベーシック (Basic)」**を選択し、**「次へ」**をクリックします。

	4. プロジェクト名を入力します。このチュートリアルでは、`MicroserviceProject` を使用します。   

	5. ホスト名を入力します。このチュートリアルでは、`devhost` を使用します。 
   
	6. **「作成」**をクリックします。

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

	* パターンの選択: 4 (マイクロサービス)
	* スターターの選択: 1 (ベーシック)
	* プラットフォームの選択: 3 (Java)
	* プロジェクト名の入力: `MicroserviceProjectCLI`

4. プロジェクトにサービスを追加する場合は、該当の質問のプロンプトで `y` を入力し、残りの質問に答えます。

5. `MicroserviceProjectCLI` が正常に保存されたら、`MicroserviceProjectCLI` フォルダーにナビゲートします。

6. この時点で、独自コードを追加することや、プロジェクトをビルドまたは実行することができます。
 
 
## {{site.data.keyword.dev_cli_notm}} を使用したプロジェクトの実行
{: #running-dev-plugin}

1. 現行プロジェクト・ディレクトリーでプロジェクトをビルドするには、以下のコマンドを入力します。

	```
	bx dev build
	```     
	{: codeblock}

2. 現行プロジェクト・ディレクトリーでプロジェクトをビルドして実行するには、以下のコマンドを入力します。

	```
	bx dev run
	```
	{: codeblock}	

3. 以下のようにして、サーバーで curl を使用してアプリケーションにアクセスすることができます。

	```
	curl http://localhost:8080	
	```
	{: codeblock}
