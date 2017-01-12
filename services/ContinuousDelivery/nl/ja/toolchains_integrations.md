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

最終更新日: 2016 年 11 月 17 日
{: .last-updated}

開発、デプロイメント、運用のタスクをサポートするツール統合をツールチェーンの作成時に構成することや、ツール統合を追加および構成して既存のツールチェーンをカスタマイズすることができます。  
{:shortdesc}

**重要**: {{site.data.keyword.Bluemix_notm}} Public では、ツールチェーンは米国南部地域でのみ利用できます。

ツールチェーンで追加および構成できるツール統合は、{{site.data.keyword.Bluemix_notm}} Public または {{site.data.keyword.Bluemix_notm}} Dedicated のどちらを使用しているかによって異なります。{{site.data.keyword.Bluemix_notm}} Dedicated でツールチェーンを使用している場合、利用できるツール統合は、特定の環境で {{site.data.keyword.jazzhub_title}} がどのように設定されたかに応じて異なります。

*表 1. {{site.data.keyword.Bluemix_notm}} Public と Dedicated* でツールチェーンに利用できるツール統合

|ツール統合 |{{site.data.keyword.Bluemix_notm}} Public で利用可能	|{{site.data.keyword.Bluemix_notm}} Dedicated で利用可能 (環境依存)|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.deliverypipeline}} 		|はい	   	|はい  		|
|{{site.data.keyword.DRA_short}} 		|はい		|いいえ			|
|Eclipse Orion {{site.data.keyword.webide}}		|はい		|はい			|
|GitHub		|はい		|はい		|
|Dedicated GitHub Enterprise			|いいえ		|はい		|
|その他のツール			|はい		|はい		|
|PagerDuty			|はい		|はい		|
|Sauce Labs		|はい		|いいえ		|
|Slack			|はい		|はい		|

**ヒント**: {{site.data.keyword.Bluemix_notm}} Public でソース・コードでの開発を開始する場合は、{{site.data.keyword.deliverypipeline}} を構成する前に GitHub ツール統合を構成します。{{site.data.keyword.Bluemix_notm}} Dedicated でコードでの開発を開始する場合は、{{site.data.keyword.deliverypipeline}} を構成する前に {{site.data.keyword.ghe_short}} ツール統合を構成します。 


## デリバリー・パイプラインの構成
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} は、入力を取得してジョブ (ビルド、テスト、デプロイメントなど) を実行するステージのシーケンスを通して、プロジェクトの継続的デプロイメントを自動的に行います。 

アプリの継続的なビルド、テスト、デプロイメントを自動で行うように {{site.data.keyword.deliverypipeline}}を構成します。 

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Delivery Pipeline」**をクリックします。使用するテンプレートに応じて、異なるフィールドを利用できます。デフォルトのフィールド値を確認し、必要に応じてそれらの設定を変更します。
1. {{site.data.keyword.Bluemix_notm}} Public 上のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックして、「概要」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。ツールチェーンを {{site.data.keyword.Bluemix_notm}} Dedicated で使用している場合は、ダッシュボードの **「DEVOPS」**タブでツールチェーンをクリックして「ツール統合」ページを開きます。または、アプリの「概要」ページの右上隅にある**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合」**をクリックします。 
1. **「ツールの追加 (Add a Tool)」**をクリックします。
1. 「ツール統合」セクションで、**「Delivery Pipeline」**をクリックします。
1. 新しいパイプラインの名前を指定します。
1. パイプラインを使用してユーザー・インターフェースをデプロイするよう計画している場合は、**「アプリケーションの表示メニューでアプリケーションを表示する (Show apps in the VIEW APP  menu)」**チェック・ボックスを選択します。パイプラインが作成するすべてのアプリケーションが、ツールチェーンの「概要」ページの**「アプリケーションの表示 (View App)」**リストに表示されます。
1. **「統合の作成 (Create Integration)」**をクリックして、{{site.data.keyword.deliverypipeline}} をツールチェーンに追加します。
1. {{site.data.keyword.deliverypipeline}} のタイルをクリックし、パイプラインを表示して構成します。パイプラインの構成の基本を確認するには、『[パイプラインのビルドとデプロイ](/docs/services/ContinuousDelivery/pipeline_build_deploy.html){: new_window}』を参照してください。

  **ヒント**: GitHub リポジトリーまたは {{site.data.keyword.ghe_short}} リポジトリーに変更をプッシュするとパイプラインがトリガーされるようにしたい場合は、パイプラインのステージを定義する前に、ツールチェーン用に GitHub または {{site.data.keyword.ghe_short}} を構成する必要があります。パイプラインのステージには、リポジトリーの Git URL が必要です。パイプラインのステージごとに、ツールチェーンに関連付けられている GitHub または {{site.data.keyword.ghe_short}} のリポジトリーを 1 つだけ参照できます。GitHub の構成手順については、[GitHub](#github) のセクションを参照してください。Dedicated GitHub Enterprise の構成方法については、「[{{site.data.keyword.ghe_long}} 概説](/docs/services/ghededicated/index.html){: new_window}」を参照してください。
  
1. オプション: {{site.data.keyword.Bluemix_notm}} Public でツールチェーンを使用していて、Sauce Labs でアプリのテストを実行したい場合、{{site.data.keyword.deliverypipeline}} を構成して Sauce Labs テスト・ジョブを追加します。テスト・ジョブの構成手順については、『[パイプラインに SauceLabs テスト・ジョブを構成する](#config_saucelabs)』セクションを参照してください。

### パイプラインに Sauce Labs テスト・ジョブを構成する
{: #config_saucelabs}

パイプラインに Sauce Labs テスト・ジョブを構成する前に、アプリをビルドしてデプロイするためのステージを含む、正常に機能するパイプラインが存在していなければなりません。また、ツールチェーンに Sauce Labs を構成しておく必要もあります。Sauce Labs の構成手順については、[Sauce Labs](#saucelabs) のセクションを参照してください。

{{site.data.keyword.deliverypipeline}} を構成して Sauce Labs テスト・ジョブを追加します。

1. アプリのテスト・バージョンをデプロイするステージがない場合は作成します。
1. そのステージのデプロイ・ジョブの後にテスト・ジョブを追加します。同じステージに置かれたこれらのジョブは、同じ環境プロパティーのセットにアクセスできることになります。
![テスト・ジョブ
](images/toolchain_test_job.png) 

1. 次の手順で、ステージを構成します。 

  a. **「環境プロパティー (ENVIRONMENT PROPERTIES)」**タブで、CF_APP_NAME、SAUCE_USERNAME、SAUCE_ACCESS_KEY の 3 つのプロパティーを作成します。
  
  b. Sauce Labs のユーザー名とアクセス・キーを入力します。こうすることで、これらの値が外部化され、テストで利用できるようになります。
  
1. デプロイ・ジョブを構成します。「デプロイ・スクリプト」**フィールドに、コマンド `export CF_APP_NAME="$CF_APP"` を含めます。**このコマンドは、アプリ名を環境プロパティーとしてエクスポートします。
1. テスト・ジョブを構成します。次の図は、値の例を示しています。
**「サービス・インスタンス」**、**「ターゲット」**、**「組織」**、**「スペース」**の各フィールドには、使用中の Sauce Labs のユーザー名、地域、組織、スペースが取り込まれます。
![ジョブの構成](images/toolchain_configure_job.png)

  a. テスター・タイプには、**Sauce Labs** を選択します。
  
  b. サービス・インスタンスでは、ツールチェーンに Sauce Labs を構成したときに使用した Sauce Labs のユーザー名を選択します。 
  
   **ヒント**: ツールチェーンで Sauce Labs を構成したときに使用したユーザー名とアクセス・キーを確認するには、**「構成」**をクリックします。 
  
  c. **「テスト実行コマンド (Test Execution Command)」**フィールドに、テストに必要な依存関係をインストールしてテストを実行するコマンドを入力します。例えば、Node.js アプリの場合、次のようなコマンドを入力します。
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. テスト・ジョブ・ログでテストのレポートを確認する場合は、**「テスト・レポートを有効にする (Enable Test Report)」**チェック・ボックスにチェックマークを付け、「テスト結果のファイル・パターン (Test Result File Pattern)」を `test/*.xml` に設定します。
  
1. **「保存」**をクリックします。パイプラインが実行されるときには必ず Sauce Labs のテストが実行されます。

詳しくは、「[Delivery Pipeline (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}」を参照してください。


## {{site.data.keyword.DRA_short}} の追加
{: #dra}

{{site.data.keyword.DRA_full}} は、単体テスト、機能テスト、およびコード・カバレッジ・ツールからの結果を収集して分析し、コードがデプロイメント・プロセスの指定されたゲートで事前定義の基準を満たすかどうかを判断します。コードが基準を満たしていない、または基準を超えていない場合、リスク回避のために、デプロイメントが停止されます。{{site.data.keyword.DRA_short}} を、継続的デリバリー環境のセーフティー・ネットとして、または品質標準の実装および改善のための手段として使用することができます。 

 **注意**: このツール統合は、事前構成されています。構成パラメーターは不要で、再構成することはできません。
 
{{site.data.keyword.DRA_short}} を追加し、デプロイメントをモニタリングしてリリース前にリスクを洗い出すことで、{{site.data.keyword.Bluemix_notm}} のコードの品質を維持し、向上させることができます。

1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。 
1. **「ツールの追加 (Add a Tool)」**をクリックします。
1. 「ツール統合」セクションで、**「{{site.data.keyword.DRA_short}}」**
をクリックします。 
1. **「統合の作成 (Create Integration)」**をクリックします。
1. {{site.data.keyword.DRA_short}} のタイルをクリックし、基本的な手順 (基準の作成、パイプラインへの基準の接続、パイプラインの実行) を完了します。詳しくは、「[{{site.data.keyword.DRA_short}} (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/content/learn/tool_devops_insights/){: new_window}」を参照してください。


## Eclipse Orion {{site.data.keyword.webide}} の追加
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} は、ソース管理タスクを作成、編集、実行、デバッグ、完了できる Web ベースの統合環境です。編集から実行、送信、そしてデプロイまで、シームレスに行うことができます。 

 **注意**: このツール統合は、事前構成されています。構成パラメーターは不要で、再構成することはできません。
 
ソース管理タスクを完了するには、次の手順で Eclipse Orion {{site.data.keyword.webide}} ツール統合を追加します。

1. {{site.data.keyword.Bluemix_notm}} Public 上のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックして、「概要」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。ツールチェーンを {{site.data.keyword.Bluemix_notm}} Dedicated で使用している場合は、ダッシュボードの **「DEVOPS」**タブでツールチェーンをクリックして「ツール統合」ページを開きます。または、アプリの「概要」ページの右上隅にある**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合」**をクリックします。
1. **「ツールの追加 (Add a Tool)」**をクリックします。
1. 「ツール統合」セクションで、**「Eclipse Orion Web IDE」**をクリックします。 
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 新しい Eclipse Orion {{site.data.keyword.webide}} のタイルをクリックします。ワークスペースに GitHub または {{site.data.keyword.ghe_short}} のリポジトリーが取り込まれます。現行のツールチェーンと関連付けられているリポジトリーは強調表示されます。

詳細については、「[Eclipse Orion {{site.data.keyword.webide}} によるコードの編集](/docs/services/ContinuousDelivery/web_ide.html){: new_window}」を参照してください。


## GitHub の構成
{: #github}

GitHub は、Git リポジトリーの Web ベースのホスティング・サービスです。リポジトリーのローカルとリモートの両方のコピーを持つことができるので、共同作業が容易になります。 

GitHub Issues は、作業と計画のすべてを 1 つの場所に保持するトラッキング・ツールです。これは、ユーザーが重要タスクに注力できるようにユーザーの開発リポジトリーと統合されます。

GitHub を構成して、クラウドでソース・コードを管理します。

1. ツールチェーンの作成時にこのツール統合を構成する場合は、次の手順を実行します。

 a. 「構成可能な統合 (Configurable Integrations)」セクションで**「GitHub」**をクリックします。{{site.data.keyword.Bluemix_notm}} Public でツールチェーンを作成していて、 {{site.data.keyword.Bluemix_notm}} に GitHub へのアクセスをまだ認可していなければ、**「認可 (Authorize)」** をクリックして GitHub Web サイトに移動します。アクティブな GitHub セッションがない場合は、ログインするよう求められます。**「アプリケーションを許可 (Authorize Application)」** をクリックして、{{site.data.keyword.Bluemix_notm}} が GitHub アカウントにアクセスできるようにします。アクティブな GitHub セッションはあるものの、最近パスワードを入力していない場合は、確認のために GitHub パスワードの入力を求められることがあります。
 
 b. GitHub リポジトリーのデフォルトのターゲット・リポジトリーの場所を確認します。これらのリポジトリーは、サンプル・リポジトリーのクローンです。必要に応じて、ターゲット・リポジトリーの名前を変更します。
![デフォルトのターゲット・リポジトリーの場所](images/toolchain_github_config.png)
   
1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。 
1. **「ツールの追加 (Add a Tool)」**をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「GitHub」**をクリックします。
1. 既存の GitHub リポジトリーを使用する場合は、リポジトリーのタイプとして**「既存」**をクリックします。次に、URL を入力します。
1. 新しい GitHub リポジトリーを使用する場合は、その GitHub リポジトリーに付ける名前を入力し、複製またはフォークするリポジトリーの URL を入力し、リポジトリー・タイプを次のように選択します。 

 a. 空のリポジトリーを作成する場合は、**「新規」**をクリックします。 
 
 b. GitHub リポジトリーのコピーを作成する場合は、**「クローンを作成する (Clone)」**をクリックします。
 
 c. GitHub リポジトリーをフォークし、プル・リクエストで変更内容を提供できるようにする場合は、**「フォーク (Fork)」**をクリックします。
 
1. 問題のトラッキングに GitHub Issues を使用する場合は、**「GitHub Issues を使用可能にする (Enable GitHub Issues)」**チェック・ボックスにチェック・マークを付けます。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 操作する GitHub リポジトリーのタイルをクリックします。GitHub の Web サイトが開きます。そこでリポジトリーの内容を表示できます。
 
  **ヒント**:  Eclipse Orion {{site.data.keyword.webide}} の統合されたソース・コード管理ツールを使用して、GitHub リポジトリーを編集し、ワークスペースからアプリをデプロイできます。

1. GitHub Issues を有効にした場合は、GitHub Issues のタイルをクリックして開きます。

詳細については、「[GitHub (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window}」と「[GitHub Issues (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}」を参照してください。


## Dedicated GitHub Enterprise の構成
{: #configghe}

{{site.data.keyword.ghe_long}} は、オンプレミス型の Web ベースの Git リポジトリー・ホスティング・サービスです。Dedicated GitHub Enterprise は {{site.data.keyword.Bluemix_notm}} Dedicated ユーザー専用です。GitHub Issues は、作業と計画を 1 つの場所に保持するトラッキング・ツールです。これは、ユーザーが重要タスクに注力できるようにユーザーの開発リポジトリーと統合されます。Dedicated GitHub Enterprise と GitHub Issues の詳細については、「[{{site.data.keyword.ghe_long}}の概説](/docs/services/ghededicated/index.html){: new_window}」と「[GitHub Issues (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}」を参照してください。

{{site.data.keyword.ghe_short}}  をツールチェーン内の 1 つのツール統合として構成して、会社の [{{site.data.keyword.Bluemix_notm}} Dedicated](/docs/dedicated/index.html#dedicated){: new_window} インスタンス内でソース・コードを管理できるようにすることができます。

1. ツールチェーンの作成時にこのツール統合を構成する場合は、次の手順を実行します。

 a. Dedicated GitHub Enterprise に初めてログインするときは、まずその前に LDAP を使用して会社のユーザー・レジストリーからあなたのユーザー ID を {{site.data.keyword.Bluemix_notm}} Dedicated インスタンスに追加するよう、会社の地域管理者に依頼してください。{{site.data.keyword.ghe_short}} アカウントの設定の詳細については、「[{{site.data.keyword.ghe_long}}の概説](/docs/services/ghededicated/index.html){: new_window}」を参照してください。
 
 b. 「構成可能な統合 (Configurable Integrations)」セクションで**「{{site.data.keyword.ghe_short}}」**をクリックします。    
 
 c. 新しい {{site.data.keyword.ghe_short}} リポジトリーのデフォルト名を確認します。必要に応じて、新しいリポジトリーの名前を変更してください。次のイメージは、サンプル・リポジトリーのクローンとして作成されたリポジトリーの例を示しています。既存のリポジトリーを使用することも、新しいリポジトリーを使用することもできます。新しいリポジトリーを使用する場合は、空のリポジトリーを作成するか、リポジトリーのクローンを作成するか、リポジトリーをフォークすることができます。
![デフォルトのリポジトリーの場所](images/toolchain_ghe_config.png)
   
1. {{site.data.keyword.Bluemix_notm}} Public 上のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合」**をクリックします。ツールチェーンを {{site.data.keyword.Bluemix_notm}} Dedicated で使用している場合は、ダッシュボードの **「DEVOPS」**タブでツールチェーンをクリックして「ツール統合」ページを開きます。または、アプリの「概要」ページの右上隅にある**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合」**をクリックします。
1. 追加ボタン (+) をクリックします。
1. 「ツール統合」セクションで、**「{{site.data.keyword.ghe_short}}」**
をクリックします。
1. 既存の {{site.data.keyword.ghe_short}} リポジトリーを使用する場合は、そのリポジトリーの URL を入力します。リポジトリー・タイプには、**「既存」**をクリックします。
1. 新しい {{site.data.keyword.ghe_short}} リポジトリーを使用する場合は、そのリポジトリーに付ける名前を入力し、複製またはフォークするリポジトリーの URL を入力し、リポジトリー・タイプを次のように選択します。 

 a. 空のリポジトリーを作成する場合は、**「新規」**をクリックします。 
 
 b. リポジトリーのコピーを作成する場合は、**「クローンを作成する (Clone)」**をクリックします。
 
 c. リポジトリーをフォークし、プル・リクエストで変更内容を提供できるようにする場合は、**「フォーク (Fork)」**をクリックします。
 
1. 問題のトラッキングに GitHub Issues を使用する場合は、**「GitHub Issues を使用可能にする (Enable GitHub Issues)」**チェック・ボックスにチェック・マークを付けます。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 操作する {{site.data.keyword.ghe_short}} リポジトリーのタイルをクリックします。会社の [{{site.data.keyword.Bluemix_notm}} Dedicated](/docs/dedicated/index.html#dedicated){: new_window} インスタンスが開きます。そこでリポジトリーの内容を表示できます。
 
  **ヒント**:  Eclipse Orion {{site.data.keyword.webide}} の統合されたソース・コード管理ツールを使用して、{{site.data.keyword.ghe_short}} リポジトリーを編集し、ワークスペースからアプリをデプロイできます。

1. GitHub Issues を有効にした場合は、GitHub Issues のタイルをクリックします。

<!-- 8/23/2016: The GHE Dedicated content has been moved to docs-staging/services/ghededicated/index.md -->

## カスタム・ツール (その他のツール) の構成
{: #othertool}

チームがツールチェーン統合リストに含まれていないツールを使用している場合、カスタム・ツールを統合できます。 

カスタム・ツールを構成して、ツールチェーン内の他のツールとともに機能し、チームで使用できるようにします。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「その他のツール (Other Tool)」**をクリックします。
1. {{site.data.keyword.Bluemix_notm}} Public 上のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックして、「概要」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。ツールチェーンを {{site.data.keyword.Bluemix_notm}} Dedicated で使用している場合は、ダッシュボードの **「DEVOPS」**タブでツールチェーンをクリックして「ツール統合」ページを開きます。または、アプリの「概要」ページの右上隅にある**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合」**をクリックします。
1. **「ツールの追加 (Add a Tool)」**をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「その他のツール (Other Tool)」**をクリックします。
1. ツール名を入力します。

1. ツールに最も密接に関連したライフサイクル・フェーズを選択します。ライフサイクル・フェーズの選択により、「概要」ページでツールがリストされるカテゴリーが決まります。
1. アイコン URL を追加します。アイコンは、ツールの統合カードに表示されます。
1. 資料 URL を追加します。
1. ツール・インスタンス名を指定します。例: My Team Tool。
1. ツール・インスタンスの URL を追加します。ツール統合カードをクリックすると、指定したツール・インスタンスの URL が表示されます。
1. ツールの説明を追加します。
1. (拡張機能) 必要に応じて、追加のプロパティーを追加します。例えば、ご使用のツールをツールチェーンの他のツールと統合するために必要な情報または属性をリストします。  
1. **「統合の作成 (Create Integration)」**をクリックします。

## PagerDuty の構成
{: #pagerduty}

PagerDuty は、複数のモニタリング・システムのデータを単一のビューに統合します。問題が発生すると、PagerDuty はそのとき問題を修正できる最適なチーム・メンバーに通知します。チーム・メンバーが問題に応答しない場合、次の技術者または運用管理者に問題を転送するようにエスカレーションを構成できます。

パイプライン・ステージで障害が発生したときに通知を送信するように PagerDuty を構成して、問題を迅速に修正してダウン時間を削減できるようにします。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「PagerDuty」**をクリックします。
1. {{site.data.keyword.Bluemix_notm}} Public 上のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックして、「概要」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。ツールチェーンを {{site.data.keyword.Bluemix_notm}} Dedicated で使用している場合は、ダッシュボードの **「DEVOPS」**タブでツールチェーンをクリックして「ツール統合」ページを開きます。または、アプリの「概要」ページの右上隅にある**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合」**をクリックします。 
1. **「ツールの追加 (Add a Tool)」**をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「PagerDuty」**をクリックします。
1. PagerDuty アカウントと関連付けられた PagerDuty サイト名を入力します。PagerDuty アカウントがない場合は、[アカウントを登録します (新しいウィンドウでリンクが開きます)](https://signup.pagerduty.com/accounts/new){: new_window}。
1. PagerDuty アカウントの API アクセス・キーを入力します。キーを確認する方法については、[API 認証 (新しいウィンドウでリンクが開きます)](https://signup.pagerduty.com/accounts/new){: new_window} を参照してください。
1. PagerDuty サービスの名前を入力します。
1. PagerDuty の 1 次連絡先の E メール・アドレスを入力します。
1. PagerDuty の 1 次連絡先の電話番号を入力します。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. PagerDuty のタイルをクリックして、pagerduty.com にアクセスします。ツールチェーンに対してこのツール統合を構成したときに指定した、PagerDuty サービスに関連付けられているイベントを表示できます。 

詳しくは、「[PagerDuty  (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}」を参照してください。


## Sauce Labs の構成
{: #saucelabs}

Sauce Labs は、機能単体テストを実行します。{{site.data.keyword.deliverypipeline}} 内のテスト・ジョブとして Sauce Labs テスト・スイートが構成されている場合、そのテスト・スイートは、継続的デリバリー・プロセスの一環として、Web アプリまたはモバイル・アプリに対するテストを実行できます。これらのテストは、誤ったコードがデプロイされるのを防ぐためのゲートとして機能することで、プロジェクトのフロー制御に役立ちます。

複数のオペレーティング・システムおよびブラウザーで自動の機能テストを実行するよう Sauce Labs を構成することによって、ユーザーによる Web サイトやアプリケーションの使用方法をエミュレートできます。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Sauce Labs」**をクリックします。
1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。 
1. **「ツールの追加 (Add a Tool)」**をクリックします。
1. 「ツール統合」セクションで、**「Sauce Labs」**
をクリックします。
1. Sauce Labs アカウントと関連付けられたユーザー名を入力します。[ Sauce Labs アカウント・ページの上部にあるウェルカム・メッセージでユーザー名を確認できます (新しいウィンドウでリンクが開きます)](https://saucelabs.com/account){: new_window}。
1. Sauce Labs アカウントのアクセス・キーを入力します。[Sauce Labs アカウント・ページでキーを確認できます (新しいウィンドウでリンクが開きます)](https://saucelabs.com/account){: new_window}。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. Sauce Labs のタイルをクリックして saucelabs.com に移動し、ツールチェーンのテスト・アクティビティーを表示します。

 **ヒント**: Sauce Labs テスト・ジョブを {{site.data.keyword.deliverypipeline}} に追加した場合、サービス・インスタンスを選択できます。

詳しくは、「[Sauce Labs (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}」を参照してください。


## Slack の構成
{: #slack}

**重要**: パブリック Slack チャネルに投稿された通知は、チーム全員が見ることができます。投稿したコンテンツの責任は投稿者が負うことに注意してください。

Slack は、クラウド・ベースのリアルタイムでのメッセージングおよび通知のシステムです。Slack が提供する永続的なチャットは、E メールの代わりに使用できる対話性に優れたチームのコラボレーション手段になります。
専用チャネルまたは作業に直接関連する一連のチャネルで、チームと連絡を取ることができます。さらに、2 人以上のメンバー間で、チャネルやダイレクト・メッセージを使用して、ファイルとイメージを共有することもできます。ダイレクト・メッセージとチャネルでの通信は、検索できるように保存されます。 

テストやデプロイのアクティビティーなどのツールチェーンに関する通知をツール統合から受信するように Slack を構成します。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Slack」**をクリックします。
1. {{site.data.keyword.Bluemix_notm}} Public 上のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックして、「概要」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。ツールチェーンを {{site.data.keyword.Bluemix_notm}} Dedicated で使用している場合は、ダッシュボードの **「DEVOPS」**タブでツールチェーンをクリックして「ツール統合」ページを開きます。または、アプリの「概要」ページの右上隅にある**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合」**をクリックします。
1. **「ツールの追加 (Add a Tool)」**をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「Slack」**をクリックします。
1. Slack アカウントの API 認証トークンを入力します。Slack での認証には、生成されたフルアクセス・トークンを使用する必要があります。トークンを確認する方法については、[Slack 認証 (新しいウィンドウでリンクが開きます)](https://api.slack.com/web#authentication){: new_window} を参照してください。
1. 通知を送信する Slack チャネルの名前を入力します。指定したチャネルが存在しない場合は作成されます。そのチャネルがアーカイブされている場合は、再アクティブ化されます。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. Slack のタイルをクリックします。構成した Slack チャネルでツールチェーンのアクティビティーをすべて表示できます。

詳しくは、「[Slack (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}」を参照してください。


# 関連リンク

{: #rellinks}

## チュートリアルとサンプル
{: #samples}

* [最初のツールチェーンの作成と使用 (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [カスタム・ツールチェーンの作成 (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [3 つのマイクロサービスを使用したアプリケーションの作成 (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [{{site.data.keyword.Bluemix_notm}} Dedicated (Beta) でのテンプレートからのツールチェーンの作成 (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [{{site.data.keyword.Bluemix_notm}} Dedicated (ベータ) でのアプリからのツールチェーンの作成 (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## 関連リンク

{: #general}

* [マイクロサービスのツールチェーン (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [シンプルなツールチェーン (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage のメソッド (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method){:new_window}
