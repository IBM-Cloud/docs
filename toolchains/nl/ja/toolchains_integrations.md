---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# ツール統合の構成
{: #integrations}

最終更新日: 2016 年 10 月 18 日
{: .last-updated}

ツールチェーンを作成するときに開発、デプロイメント、運用の作業をサポートするツール統合を構成したり、既存のツールチェーンにツール統合を追加、構成してカスタマイズしたりできます。  
{:shortdesc}

**重要**: {{site.data.keyword.Bluemix_notm}} Public の場合、ツールチェーンは米国南部地域でのみ利用可能です。

ツールチェーンに追加して構成できるツール統合は、ツールチェーンを {{site.data.keyword.Bluemix_notm}} Public で使用するか {{site.data.keyword.Bluemix_notm}} Dedicated で使用するかによって異なります。
{{site.data.keyword.Bluemix_notm}} Dedicated でツールチェーンを使用している場合、利用可能なツール統合は、特定の環境で {{site.data.keyword.jazzhub_title}} がセットアップされる方法によって異なります。

*表 1. {{site.data.keyword.Bluemix_notm}} Public と Dedicated のツールチェーンで使用できるツール統合*

|ツール統合 |{{site.data.keyword.Bluemix_notm}} Public で利用可能	|{{site.data.keyword.Bluemix_notm}} Dedicated で利用可能 (環境依存)|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.deliverypipeline}} 		|可	   	|可  		|
|{{site.data.keyword.DRA_short}} 		|可		|不可			|
|Eclipse Orion {{site.data.keyword.webide}}		|可		|可			|
|GitHub		|可		|可		|
|Dedicated GitHub Enterprise			|不可		|可		|
|他のツール			|可		|可		|
|PagerDuty			|可		|可		|
|Sauce Labs		|可		|不可		|
|Slack			|可		|可		|

**ヒント**: {{site.data.keyword.Bluemix_notm}} Public でソース・コードの開発を開始する場合は、{{site.data.keyword.deliverypipeline}} を構成する前に GitHub ツール統合を構成してください。
{{site.data.keyword.Bluemix_notm}} Dedicated でコードの開発を開始する場合は、{{site.data.keyword.deliverypipeline}} を構成する前に {{site.data.keyword.ghe_short}} ツール統合または GitHub ツール統合を構成してください。 


## Delivery Pipeline の構成
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} は、入力を取得してビルド、テスト、デプロイメントなどのジョブを実行する一連のステージによって、プロジェクトの継続的デプロイメントを自動化します。 

{{site.data.keyword.deliverypipeline}} を構成し、アプリケーションの継続的なビルド、テスト、デプロイメントを自動化します。 

1. ツールチェーンを作成しているときにこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで、**「Delivery Pipeline」**をクリックします。使用するテンプレートに応じて、異なるフィールドを利用できます。デフォルトのフィールド値を確認し、必要に応じてそれらの設定を変更します。
1. {{site.data.keyword.Bluemix_notm}} Public のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの **「ツールチェーン」**ページで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。{{site.data.keyword.Bluemix_notm}} Dedicated でツールチェーンを使用する場合は、ダッシュボードの**「DEVOPS」**タブで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの右上隅にある**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「Delivery Pipeline」**をクリックします。
1. 新しいパイプラインの名前を指定します。
1. パイプラインを使用してユーザー・インターフェースをデプロイしようと計画している場合は、**「表示可能なアプリケーション (Viewable App)」**チェック・ボックスにチェック・マークを付けます。パイプラインで作成されるすべてのアプリケーションが、ツールチェーンの「ツール統合 (Tool Integrations) 」ページの**「アプリの表示 (VIEW APP)」**リストに表示されます。
1. **「統合の作成 (Create Integration)」**をクリックして、{{site.data.keyword.deliverypipeline}} をツールチェーンに追加します。
1. {{site.data.keyword.deliverypipeline}} のタイルをクリックし、パイプラインを表示して構成します。パイプラインの構成方法の基本を確認するには、[パイプラインのビルドとデプロイ (リンク先が新しいウィンドウで開きます)](../services/DeliveryPipeline/build_deploy.html){: new_window} を参照してください。

  **ヒント**: 変更を GitHub または {{site.data.keyword.ghe_short}} のリポジトリーにプッシュしたときにパイプラインをトリガーしたい場合は、パイプラインのステージを定義する前に、ツールチェーン用の GitHub または {{site.data.keyword.ghe_short}} を構成しておく必要があります。パイプラインのステージには、リポジトリーの Git URL が必要です。パイプラインのステージごとに、ツールチェーンに関連付けられている GitHub または {{site.data.keyword.ghe_short}} のリポジトリーを 1 つだけ参照できます。GitHub の構成手順については、[GitHub](#github) のセクションを参照してください。Dedicated GitHub Enterprise の構成手順については、[{{site.data.keyword.ghe_long}} の概要 (リンク先が新しいウィンドウで開きます)](../services/ghededicated/index.html){: new_window} を参照してください。
  
1. オプション: {{site.data.keyword.Bluemix_notm}} Public でツールチェーンを使用している環境で Sauce Labs によってアプリのテストを実行したい場合は、{{site.data.keyword.deliverypipeline}} を構成して Sauce Labs テスト・ジョブを追加します。テスト・ジョブの構成手順については、「[パイプラインに SauceLabs テスト・ジョブを構成する](#config_saucelabs)」セクションを参照してください。

### パイプラインに Sauce Labs テスト・ジョブを構成する
{: #config_saucelabs}

パイプラインに Sauce Labs テスト・ジョブを構成する前に、アプリケーションをビルドしてデプロイするためのステージを含む、正常に機能するパイプラインが存在していなければなりません。また、ツールチェーンに Sauce Labs を構成しておく必要もあります。Sauce Labs の構成手順については、[Sauce Labs](#saucelabs)のセクションを参照してください。

{{site.data.keyword.deliverypipeline}} を構成して Sauce Labs テスト・ジョブを追加します。

1. アプリケーションのテスト・バージョンをデプロイするステージがない場合は作成します。
1. そのステージのデプロイ・ジョブの後にテスト・ジョブを追加します。これらのジョブを同じステージに配置することで、両方のジョブで同じ環境プロパティーのセットを利用できます。
![テスト・ジョブ
](images/toolchain_test_job.png) 

1. ステージを構成します。 

  a. **「環境プロパティー (ENVIRONMENT PROPERTIES)」**タブで、CF_APP_NAME、SAUCE_USERNAME、および SAUCE_ACCESS_KEY の 3 つのプロパティーを作成します。
  
  b. Sauce Labs のユーザー名とアクセス・キーを入力します。こうすることで、これらの値を外部化し、テストで利用できるようになります。
  
1. デプロイ・ジョブを構成します。**「デプロイ・スクリプト (Deploy Script)」**フィールドに `export CF_APP_NAME="$CF_APP"` というコマンドを入力します。このコマンドは、アプリケーション名を環境プロパティーとしてエクスポートします。
1. テスト・ジョブを構成します。次の図は、値の例を示しています。
**「サービス・インスタンス」**、**「ターゲット」**、**「組織」**、**「スペース」**の各フィールドには、使用中の Sauce Labs のユーザー名、地域、組織、スペースが取り込まれます。
![ジョブの構成](images/toolchain_configure_job.png)

  a. テスター・タイプでは、**「Sauce Labs」**を選択します。
  
  b. サービス・インスタンスでは、ツールチェーンに Sauce Labs を構成したときに使用した Sauce Labs のユーザー名を選択します。 
  
   **ヒント**: ツールチェーンで Sauce Labs を構成したときに使用したユーザー名とアクセス・キーを確認するには、**「構成」**をクリックします。 
  
  c. **「テスト実行コマンド (Test Execution Command)」**フィールドに、テストに必要な依存関係をインストールしてテストを実行するコマンドを入力します。例えば、Node.js アプリをテストする場合は、次のコマンドを入力します。
     ```
npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. テスト・ジョブ・ログでテストのレポートを確認する場合は、**「テスト・レポートを有効にする (Enable Test Report)」**チェック・ボックスにチェックマークを付け、「テスト結果のファイル・パターン (Test Result File Pattern)」を `test/*.xml` に設定します。
  
1. **「保存」**をクリックします。パイプラインが実行されるときには必ず Sauce Labs のテストが実行されます。

詳しくは、[Delivery Pipeline (リンク先が新しいウィンドウで開きます)](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window} を参照してください。


## {{site.data.keyword.DRA_short}} の追加
{: #dra}

{{site.data.keyword.DRA_full}} は、単体テスト、機能テスト、およびコード・カバレッジ・ツールからの結果を収集して分析し、コードがデプロイメント・プロセスの指定されたゲートで事前定義の基準を満たすかどうかを判断します。コードが基準を満たしていない、または基準を超えていない場合、リスクがリリースされないように、デプロイメントが停止されます。継続的デリバリー環境のセーフティー・ネットとして、または品質基準を実装して向上させる方法として、{{site.data.keyword.DRA_short}} を使用できます。 

 **注記**: このツール統合は、事前構成されています。構成パラメーターは不要で、再構成はできません。
 
{{site.data.keyword.DRA_short}} を追加し、デプロイメントをモニタリングしてリリース前にリスクを洗い出すことで、{{site.data.keyword.Bluemix_notm}} のコードの品質を維持し、向上させることができます。

1. 既に存在するツールチェーンに、このツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「Deployment Risk Analytics」**をクリックします。 
1. **「統合の作成 (Create Integration)」**をクリックします。
1. {{site.data.keyword.DRA_short}} のタイルをクリックし、基準を作成する、基準をパイプラインに接続する、パイプラインを実行する、という開始手順を完了させます。詳しくは、[{{site.data.keyword.DRA_short}} (リンク先が新しいウィンドウで開きます)](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window} を参照してください。


## Eclipse Orion {{site.data.keyword.webide}} の追加
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} は、ソース管理タスクを作成、編集、実行、デバッグ、完了できる Web ベースの統合環境です。
編集から実行、送信、そしてデプロイまで、シームレスに行うことができます。 

 **注記**: このツール統合は、事前構成されています。構成パラメーターは不要で、再構成はできません。
 
ソース管理タスクを完了させるために、Eclipse Orion {{site.data.keyword.webide}} ツール統合を追加します。

1. {{site.data.keyword.Bluemix_notm}} Public のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの **「ツールチェーン」**ページで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。{{site.data.keyword.Bluemix_notm}} Dedicated でツールチェーンを使用する場合は、ダッシュボードの**「DEVOPS」**タブで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの右上隅にある**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「Eclipse Orion Web IDE」**をクリックします。 
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 新しい Eclipse Orion {{site.data.keyword.webide}} のタイルをクリックします。ワークスペースに GitHub または {{site.data.keyword.ghe_short}} のリポジトリーが取り込まれます。現在のツールチェーンに関連付けられたリポジトリーが強調表示されます。

詳しくは、[Eclipse Orion {{site.data.keyword.webide}} によるコードの編集 (リンク先が新しいウィンドウで開きます)](../toolchains/web_ide.html){: new_window} を参照してください。


## GitHub の構成
{: #github}

GitHub は、Web ベースの Git リポジトリー・ホスティング・サービスです。リポジトリーのローカルとリモートの両方のコピーを持つことができるので、共同作業が容易になります。 

GitHub Issues は、作業と計画をすべて 1 カ所に保持するトラッキング・ツールです。開発リポジトリーに統合されるため、重要なタスクに集中できます。

GitHub を構成して、クラウドでソース・コードを管理します。

1. ツールチェーンを作成しているときにこのツール統合を構成する場合は、次の手順を実行します。

 a. 「構成可能な統合 (Configurable Integrations)」セクションで、**「GitHub」**をクリックします。{{site.data.keyword.Bluemix_notm}} Public でツールチェーンを作成し、GitHub へのアクセスを {{site.data.keyword.Bluemix_notm}} に許可していない場合は、**「許可 (Authorize)」**をクリックして、GitHub の Web サイトに移動します。アクティブな GitHub セッションがない場合は、ログインを求めるプロンプトが出されます。**「アプリケーションを許可 (Authorize Application)」**をクリックして、{{site.data.keyword.Bluemix_notm}} が GitHub アカウントにアクセスできるようにします。アクティブな GitHub セッションがあるが、最近パスワードを入力していない場合は、確認のために GitHub パスワードを入力するよう求めるプロンプトが出される場合があります。
 
 b. GitHub リポジトリーのデフォルトのターゲット・リポジトリーのロケーションを確認します。これらのリポジトリーは、サンプル・リポジトリーのクローンです。必要に応じて、ターゲット・リポジトリーの名前を変更します。
![デフォルトのターゲット・リポジトリーのロケーション](images/toolchain_github_config.png)
   
1. 既に存在するツールチェーンに、このツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「GitHub」**をクリックします。
1. 既存の GitHub リポジトリーを使用する場合は、その URL を入力します。リポジトリー・タイプで、**「リンク (Link)」**をクリックします。
1. 新しい GitHub リポジトリーを使用する場合は、GitHub リポジトリーの名前を入力し、クローン作成またはフォークするリポジトリーの URL を入力し、リポジトリーのタイプを選択します。 

 a. 空のリポジトリーを作成するには、**「新規 (New)」**をクリックします。 
 
 b. GitHub リポジトリーのコピーを作成するには、**「クローンを作成する (Clone)」**をクリックします。
 
 c. プル要求により変更を提出できるように GitHub リポジトリーをフォークするには、**「フォーク (Fork)」**をクリックします。
 
1. 問題のトラッキングに GitHub Issues を使用する場合は、**「GitHub Issues を使用可能にする (Enable GitHub Issues)」**チェック・ボックスにチェック・マークを付けます。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 操作する GitHub リポジトリーのタイルをクリックします。GitHub の Web サイトが開きます。そこでリポジトリーの内容を表示できます。
 
  **ヒント**: Eclipse Orion {{site.data.keyword.webide}} の統合されたソース・コード管理ツールを使用して、GitHub リポジトリーを編集し、ワークスペースからアプリをデプロイできます。

1. GitHub Issues を有効にした場合は、GitHub Issues のタイルをクリックして開きます。

詳しくは、[GitHub (リンク先が新しいウィンドウで開きます)](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} と [GitHub Issues (リンク先が新しいウィンドウで開きます)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window} を参照してください。


## Dedicated GitHub Enterprise の構成
{: #configghe}

{{site.data.keyword.ghe_long}} は、オンプレミス型の Web ベースの Git リポジトリー・ホスティング・サービスです。Dedicated GitHub Enterprise は {{site.data.keyword.Bluemix_notm}} Dedicated ユーザー専用です。GitHub Issues は、作業と計画を 1 カ所に保持するトラッキング・ツールです。開発リポジトリーに統合されるため、重要なタスクに集中できます。Dedicated GitHub Enterprise と GitHub Issues の詳細については、[Dedicated GitHub Enterprise の使い方 (リンク先が新しいウィンドウで開きます)](../services/ghededicated/index.html){: new_window} と [GitHub Issues (リンク先が新しいウィンドウで開きます)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window} を参照してください。

{{site.data.keyword.ghe_short}} をツールチェーンのツール統合として構成すれば、会社の [{{site.data.keyword.Bluemix_notm}} Dedicated (リンク先が新しいウィンドウで開きます)](../dedicated/index.html#dedicated){: new_window} インスタンスでソース・コードを管理できます。

1. ツールチェーンを作成しているときにこのツール統合を構成する場合は、次の手順を実行します。

 a. Dedicated GitHub Enterprise に初めてログインする前に、LDAP を使用して会社のユーザー・レジストリーからあなたのユーザー ID を {{site.data.keyword.Bluemix_notm}} Dedicated インスタンスに追加するよう、会社の地域管理者に依頼してください。{{site.data.keyword.ghe_short}} アカウントの設定については、[Dedicated GitHub Enterprise の使い方 (リンク先が新しいウィンドウで開きます)](../services/ghededicated/index.html){: new_window} を参照してください。
 
 b. 「構成可能な統合 (Configurable Integrations)」セクションで、**「{{site.data.keyword.ghe_short}}」**をクリックします。    
 
 c. 新しい {{site.data.keyword.ghe_short}} リポジトリーのデフォルト名を確認します。必要に応じて新しいリポジトリーの名前を変更してください。以下の画像は、サンプル・リポジトリーから複製したリポジトリーの例です。既存のリポジトリーを使用することも、新しいリポジトリーを使用することもできます。新しいリポジトリーを使用する場合は、空のリポジトリーを作成するか、リポジトリーのクローンを作成するか、リポジトリーをフォークします。![リポジトリーのデフォルトの場所](images/toolchain_ghe_config.png)
   
1. {{site.data.keyword.Bluemix_notm}} Public のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの **「ツールチェーン」**ページで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。{{site.data.keyword.Bluemix_notm}} Dedicated でツールチェーンを使用する場合は、ダッシュボードの**「DEVOPS」**タブで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの右上隅にある**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「{{site.data.keyword.ghe_short}}」**をクリックします。
1. 既存の {{site.data.keyword.ghe_short}} リポジトリーを使用する場合は、そのリポジトリーの URL を入力します。リポジトリーのタイプとして、**「既存」**をクリックしてください。
1. 新しい {{site.data.keyword.ghe_short}} リポジトリーを使用する場合は、そのリポジトリーの名前を入力し、クローンを作成またはフォークする対象のリポジトリーの URL を入力し、リポジトリーのタイプを選択します。 

 a. 空のリポジトリーを作成するには、**「新規 (New)」**をクリックします。 
 
 b. リポジトリーのコピーを作成するには、**「クローンを作成する (Clone)」**をクリックします。
 
 c. プル要求により変更を提出できるようにリポジトリーをフォークするには、**「フォーク (Fork)」**をクリックします。
 
1. 問題のトラッキングに GitHub Issues を使用する場合は、**「GitHub Issues を使用可能にする (Enable GitHub Issues)」**チェック・ボックスにチェック・マークを付けます。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 操作する {{site.data.keyword.ghe_short}} リポジトリーのタイルをクリックします。会社の [{{site.data.keyword.Bluemix_notm}} Dedicated (リンク先が新しいウィンドウで開きます)](../dedicated/index.html#dedicated){: new_window} インスタンスが開きます。そこでリポジトリーの内容を表示できます。
 
  **ヒント**: Eclipse Orion {{site.data.keyword.webide}} の統合されたソース・コード管理ツールを使用して、{{site.data.keyword.ghe_short}} リポジトリーを編集し、ワークスペースからアプリをデプロイできます。

1. GitHub Issues を有効にした場合は、GitHub Issues のタイルをクリックします。

<!-- 8/23/2016: The GHE Dedicated content has been moved to docs-staging/services/ghededicated/index.md -->

## カスタム・ツール (他のツール) の構成
{: #othertool}

チームが、ツールチェーン統合リストに含まれていないツールを使用する場合、カスタム・ツールを統合できます。 

カスタム・ツールを構成し、それがツールチェーンで他のツールと連携し、チームで利用可能になるようにします。
1. ツールチェーンを作成しているときにこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで、**「他のツール (Other Tool)」**をクリックします。

1. 既に存在するツールチェーンに、このツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「他のツール (Other Tool)」**をクリックします。
1. ツール名を入力します。
1. ツールに最も関連の強いライフサイクル・フェーズを選択します。ライフサイクル・フェーズの選択は、「ツールチェーン統合 (Toolchains Integrations)」ページのどのカテゴリーの下に
ツールがリストされるかを決定します。
1. アイコンの URL を追加します。アイコンは、ご使用のツールの統合カードに表示されます。
1. 資料 URL を追加します。
1. ツール・インスタンス名を指定します。例えば: マイ・チーム・ツール。
1. ツール・インスタンスの URL を追加します。ツール統合カードをクリックすると、ツール・インスタンス用にリストした URL に移動します。
1. ツールの説明を追加します。
1. (拡張機能) 必要に応じて、追加のプロパティーを追加します。例えば、ツールチェーンの他のツールと統合するために、ご使用のツールに必要な情報または属性をリストします。  
1. **「統合の作成 (Create Integration)」**をクリックします。

## PagerDuty の構成
{: #pagerduty}

PagerDuty は、複数のモニタリング・システムのデータを単一のビューに統合します。問題が発生すると、PagerDuty はそのとき問題を修正できる最適なチーム・メンバーに通知します。そのチーム・メンバーが問題に対応しない場合は、エスカレーションを構成して、2 番目のエンジニアまたは運用マネージャーに転送することができます。

パイプライン・ステージの障害が発生したときに通知を送信するよう PagerDuty を構成し、問題を迅速に修正して、ダウン時間を減少できるようにします。

1. ツールチェーンを作成しているときにこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで、**「PagerDuty」**をクリックします。
1. 既に存在するツールチェーンに、このツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「PagerDuty」**をクリックします。
1. PagerDuty アカウントと関連付けられている PagerDuty のサイト名を入力します。PagerDuty アカウントがない場合は、[アカウントを登録します (リンク先が新しいウィンドウで開きます)](https://signup.pagerduty.com/accounts/new){: new_window}。
1. PagerDuty アカウントの API アクセス・キーを入力します。キーを確認する方法については、[API 認証 (リンク先が新しいウィンドウで開きます)](https://signup.pagerduty.com/accounts/new){: new_window} を参照してください。
1. PagerDuty サービスの名前を入力します。
1. PagerDuty の 1 次連絡先の E メール・アドレスを入力します。
1. PagerDuty の 1 次連絡先の電話番号を入力します。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. PagerDuty のタイルをクリックして、pagerduty.com にアクセスします。ツールチェーンに対してこのツール統合を構成したときに指定した、PagerDuty サービスに関連付けられているイベントを表示できます。 

詳しくは、[PagerDuty (リンク先が新しいウィンドウで開きます)](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window} を参照してください。


## Sauce Labs の構成
{: #saucelabs}

Sauce Labs は、機能単体テストを実行します。Sauce Labs のテスト・スイートを {{site.data.keyword.deliverypipeline}} にテスト・ジョブとして構成した場合、テスト・スイートは、継続的デリバリー・プロセスの一部として Web アプリケーションまたはモバイル・アプリケーションに対してテストを実行できます。これらのテストは、プロジェクトの重要なフロー制御を提供し、誤ったコードのデプロイメントを防ぐゲートとして機能します。

自動化された機能テストを複数のオペレーティング・システムとブラウザーで実行するように Sauce Labs を構成します。これにより、ユーザーが Web サイトまたはアプリケーションを使用する可能性がある方法をエミュレートできます。

1. ツールチェーンを作成しているときにこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで、**「Sauce Labs」**をクリックします。
1. 既に存在するツールチェーンに、このツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「Sauce Labs」**をクリックします。
1. Sauce Labs アカウントと関連付けられているユーザー名を入力します。[Sauce Labs アカウント・ページの上部にあるウェルカム・メッセージでユーザー名を確認できます (リンク先が新しいウィンドウで開きます)](https://saucelabs.com/account){: new_window}。
1. Sauce Labs アカウントのアクセス・キーを入力します。[Sauce Labs アカウント・ページでキーを確認できます (リンク先が新しいウィンドウで開きます)](https://saucelabs.com/account){: new_window}。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. Sauce Labs のタイルをクリックして、saucelabs.com に移動し、ツールチェーンのテスト・アクティビティーを表示します。

 **ヒント**: Sauce Labs テスト・ジョブを {{site.data.keyword.deliverypipeline}} に追加した場合は、サービス・インスタンスを選択できます。

詳しくは、[Sauce Labs (リンク先が新しいウィンドウで開きます)](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window} を参照してください。


## Slack の構成
{: #slack}

**重要**: Slack の公開チャネルに投稿された通知は、チームの全員に表示されます。投稿したコンテンツの責任はお客様が負うことに注意してください。

Slack は、リアルタイム・メッセージングと通知を提供するクラウド・ベースのシステムです。
Slack が提供する永続的なチャットは、E メールの代わりに使用できる対話性に優れたチームのコラボレーション手段になります。
チームとのコミュニケーションには、専用チャネルを使用することも、作業に直接関連する一連のチャネルを使用することもできます。また、チャネルを通じて、または 2 人以上のメンバーでのダイレクト・メッセージで、ファイルとイメージを共有することもできます。ダイレクト・メッセージとチャネル上の通信は保持されるため、検索することができます。 

テストやデプロイのアクティビティーなどのツールチェーンに関する通知をツール統合から受信するように Slack を構成します。

1. ツールチェーンを作成しているときにこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで、**「Slack」**をクリックします。
1. 既に存在するツールチェーンに、このツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「Slack」**をクリックします。
1. Slack アカウントの API 認証トークンを入力します。Slack での認証には、生成されたフルアクセス・トークンを使用する必要があります。トークンを確認する方法については、[Slack 認証 (リンク先が新しいウィンドウで開きます)](https://api.slack.com/web#authentication){: new_window} を参照してください。
1. 通知を送信する Slack チャネルの名前を入力します。指定したチャネルが存在しない場合は、そのチャネルが作成されます。チャネルがアーカイブされたら、再アクティブ化します。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. Slack のタイルをクリックします。構成した Slack チャネルでツールチェーンのアクティビティーをすべて表示できます。

詳しくは、[Slack (リンク先が新しいウィンドウで開きます)](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window} を参照してください。








