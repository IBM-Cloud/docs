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

最終更新日: 2016 年 9 月 13 日
{: .last-updated}

ツールチェーンを作成している間に、開発、デプロイメント、および運用の作業をサポートするツール統合を構成するか、または、既存のツールチェーンをカスタマイズするためにツール統合を追加および構成することができます。  
{:shortdesc}

**重要**: この機能は試験的なものです。ツールチェーンは変更される可能性があり、変更により前のバージョンとの互換性がなくなる場合もあります。実稼働環境での使用は推奨されません。{{site.data.keyword.Bluemix_notm}} Public では、ツールチェーンは「米国南部」地域でのみ使用可能です。

ご使用のツールチェーン用の追加および構成に使用可能なツール統合は、ツールチェーンを {{site.data.keyword.Bluemix_notm}} Public で使用するのか、{{site.data.keyword.Bluemix_notm}} Dedicated で使用するのかによって異なります。

*表 1. {{site.data.keyword.Bluemix_notm}} Public および Dedicated でツールチェーン用に使用可能なツール統合*

|ツール統合 |{{site.data.keyword.Bluemix_notm}} Public で使用可能	|{{site.data.keyword.Bluemix_notm}} Dedicated で使用可能|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.deliverypipeline}} 		|はい	   	|はい  		|
|{{site.data.keyword.DRA_short}} 		|はい		|いいえ			|
|Eclipse Orion {{site.data.keyword.webide}}		|はい		|はい			|
|GitHub		|はい		|いいえ		|
|Dedicated GitHub Enterprise			|いいえ		|はい		|
|PagerDuty			|はい		|いいえ		|
|Sauce Labs		|はい		|いいえ		|
|Slack			|はい		|いいえ		|

**ヒント**: {{site.data.keyword.Bluemix_notm}} Public でソース・コードを使用した開発を始める場合、GitHub ツール統合を構成し、その後で {{site.data.keyword.deliverypipeline}} を構成してください。{{site.data.keyword.Bluemix_notm}} Dedicated でコードを使用した開発を始める場合、{{site.data.keyword.ghe_short}} ツール統合を構成し、その後で {{site.data.keyword.deliverypipeline}} を構成してください。 


## デリバリー・パイプラインの構成
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} は、入力を取得してジョブ (ビルド、テスト、デプロイなど) を実行する一連のステージを通して、プロジェクトの継続的デプロイメントを自動化します。 

{{site.data.keyword.deliverypipeline}} を構成して、アプリの継続的なビルド、テスト、およびデプロイを自動化するには、次のようにします。 

1. ツールチェーン作成時にこのツール統合を構成している場合、「構成可能な統合 (Configurable Integrations)」セクションで**「Delivery Pipeline」**をクリックします。使用するテンプレートによって、使用可能なフィールドが異なることがあります。デフォルトのフィールド値を検討し、必要に応じてそれらの設定を変更します。
1. {{site.data.keyword.Bluemix_notm}} Public にツールチェーンがあり、そのツールチェーンにこのツール統合を追加しようとしている場合、DevOps ダッシュボードの**「ツールチェーン」**タブでそのツールチェーンをクリックして、そのツールチェーンの「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの「継続的なデリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。{{site.data.keyword.Bluemix_notm}} Dedicated でツールチェーンを使用している場合、ダッシュボードの**「DEVOPS」** タブでそのツールチェーンをクリックして、そのツールチェーンの「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの右上隅にある**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで**「Delivery Pipeline」**をクリックします。
1. この新規パイプラインの名前を指定します。
1. パイプラインを使用してユーザー・インターフェースをデプロイする予定の場合、**「表示可能アプリ (Viewable App)」**チェック・ボックスを選択します。パイプラインが作成するすべてのアプリが、ツールチェーンの「ツール統合 (Tool Integrations)」ページの**「アプリの表示」**リストに表示されます。
1. {{site.data.keyword.deliverypipeline}} をツールチェーンに追加するため、**「統合の作成 (Create Integration)」**をクリックします。
1. {{site.data.keyword.deliverypipeline}} のタイルをクリックしてパイプラインを表示し、構成します。パイプラインの構成の基本を理解するには、[パイプラインのビルドとデプロイ](../services/DeliveryPipeline/build_deploy.html){: new_window}を参照してください。

  **ヒント**: GitHub リポジトリーまたは {{site.data.keyword.ghe_short}} リポジトリーに変更をプッシュするとパイプラインがトリガーされるようにしたい場合は、パイプラインのステージを定義する前に、ツールチェーン用に GitHub または {{site.data.keyword.ghe_short}} を構成する必要があります。パイプライン・ステージは、リポジトリーの Git URL を必要とします。各パイプライン・ステージは、ツールチェーンと関連付けられた、GitHub リポジトリーまたは {{site.data.keyword.ghe_short}} リポジトリーのどちらか 1 つのみを参照できます。GitHub の構成方法については、『[GitHub](#github)』セクションを参照してください。Dedicated GitHub Enterprise の構成方法については、『[{{site.data.keyword.ghe_long}} 概説](../services/ghededicated/index.html){: new_window}』を参照してください。
  
1. オプション: {{site.data.keyword.Bluemix_notm}} Public でツールチェーンを使用していて、Sauce Labs でアプリのテストを実行したい場合、{{site.data.keyword.deliverypipeline}} を構成して Sauce Labs テスト・ジョブを追加します。テスト・ジョブの構成方法については、『[パイプライン内の Sauce Labs テスト・ジョブの構成](#config_saucelabs)』セクションを参照してください。

### パイプライン内の Sauce Labs テスト・ジョブの構成
{: #config_saucelabs}

パイプライン内に Sauce Labs テスト・ジョブを構成する前に、アプリをビルドおよびデプロイするステージを含んでいる作業パイプラインが必要であり、ツールチェーン用に Sauce Labs を構成する必要があります。Sauce Labs の構成方法については、『[Sauce Labs](#saucelabs)』セクションを参照してください。

{{site.data.keyword.deliverypipeline}} を構成して Sauce Labs テスト・ジョブを追加するには、次のようにします。

1. アプリのテスト版をデプロイするステージがない場合、作成します。
1. ステージ内で、デプロイ・ジョブの後にテスト・ジョブを追加します。これらのジョブは、同じステージに置かれることによって、環境プロパティーの同じセットにアクセスできます。
  ![テスト・ジョブ](images/toolchain_test_job.png) 

1. ステージを構成します。 

  a. **「環境プロパティー」**タブで、3 つのプロパティー (CF_APP_NAME、SAUCE_USERNAME、および SAUCE_ACCESS_KEY) を作成します。
  
  b. Sauce Labs ユーザー名とアクセス・キーを入力します。これを行うことによって、これらの値をテストで使用できるように外部化します。
  
1. デプロイ・ジョブを構成します。**「デプロイ・スクリプト」**フィールドに、コマンド `export CF_APP_NAME="$CF_APP"` を含めます。このコマンドは、アプリ名を 1 つの環境プロパティーとしてエクスポートします。
1. テスト・ジョブを構成します。次のイメージ中の値は例です。**「サービス・インスタンス」**、**「ターゲット」**、**「組織」**、および**「スペース」**フィールドには、使用する Sauce Labs ユーザー名、地域、組織、およびスペースが設定されています。
![ジョブの構成](images/toolchain_configure_job.png)

  a. テスター・タイプには **Sauce Labs** を選択します。
  
  b. サービス・インスタンスには、ツールチェーン用に Sauce Labs を構成したときに使用した Sauce Labs ユーザー名を選択します。 
  
   **ヒント**: ツールチェーン用に Sauce Labs を構成したときに使用したユーザー名およびアクセス・キーを表示するには、**「構成」**をクリックします。 
  
  c. **「テスト実行コマンド (Test Execution Command)」**フィールドに、テストで必要な依存関係をインストールするコマンドを入力し、テストを実行します。例えば、Node.js アプリの場合、次のようなコマンドを入力します。
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. テスト・ジョブ・ログ内でテスト・レポートを確認したい場合、**「テスト・レポートを使用可能にする」**チェック・ボックスを選択し、「テスト結果ファイル・パターン」を `test/*.xml` に設定します。
  
1. **「保存」**をクリックします。パイプラインが実行されるたびに、Sauce Labs テストが実行されます。

詳細については、『[Delivery Pipeline](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}』を参照してください。


## {{site.data.keyword.DRA_short}} の追加
{: #dra}

{{site.data.keyword.DRA_full}} は、単体テスト、機能テスト、およびコード・カバレッジ・ツールからの結果を収集および分析することによって、デプロイメント・プロセス内に指定されたいくつかのゲートで、ユーザーのコードが事前定義済みの基準を満たしているかどうかを判別します。コードが基準を満たしていなかったり、基準を上回っていたりする場合、リスクが広がるのを防御するためにデプロイメントは停止されます。{{site.data.keyword.DRA_short}} を継続的デリバリー環境のセーフティーネットとして使用したり、品質標準の実装および改善のための手段として使用したりできます。 

 **注**: このツール統合は事前構成済みです。必要な構成パラメーターはなく、再構成することはできません。
 
{{site.data.keyword.DRA_short}} を追加すると、デプロイメントのモニタリングによってリスクを前もって特定してリスクの広がりを防ぐことによって、{{site.data.keyword.Bluemix_notm}} 内のコードの品質を保守および改善できるようになります。

1. ツールチェーンが既にあり、このツール統合をそのツールチェーンに追加する場合、DevOps ダッシュボードの**「ツールチェーン」**タブでそのツールチェーンをクリックして、そのツールチェーンの「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの「継続的なデリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで**「Deployment Risk Analytics」**をクリックします。 
1. **「統合の作成 (Create Integration)」**をクリックします。
1. {{site.data.keyword.DRA_short}} のタイルをクリックし、開始手順を実行します。つまり、基準を作成し、その基準をパイプラインに接続し、パイプラインを実行します。詳しくは、「[{{site.data.keyword.DRA_short}}](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}」を参照してください。


## Eclipse Orion {{site.data.keyword.webide}} の追加
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} は、ソース制御タスクの作成、編集、実行、デバッグ、および実行を行うことのできる、Web ベースの統合環境です。編集から実行、サブミット、デプロイへと、シームレスに進んでいくことができます。 

 **注**: このツール統合は事前構成済みです。必要な構成パラメーターはなく、再構成することはできません。
 
ソース制御タスクを実行するため、次のようにして Eclipse Orion {{site.data.keyword.webide}} ツール統合を追加します。

1. {{site.data.keyword.Bluemix_notm}} Public にツールチェーンがあり、そのツールチェーンにこのツール統合を追加しようとしている場合、DevOps ダッシュボードの**「ツールチェーン」**タブでそのツールチェーンをクリックして、そのツールチェーンの「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの「継続的なデリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。{{site.data.keyword.Bluemix_notm}} Dedicated でツールチェーンを使用している場合、ダッシュボードの**「DEVOPS」** タブでそのツールチェーンをクリックして、そのツールチェーンの「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの右上隅にある**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで**「Eclipse Orion Web IDE」**をクリックします。 
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 新規 Eclipse Orion {{site.data.keyword.webide}} のタイルをクリックします。ワークスペースには、GitHub リポジトリーまたは {{site.data.keyword.ghe_short}} リポジトリーが事前設定されています。現行のツールチェーンと関連付けられているリポジトリーは強調表示されます。

詳細については、『[Eclipse Orion {{site.data.keyword.webide}} でのコード編集](../toolchains/web_ide.html){: new_window}』を参照してください。


## GitHub の構成
{: #github}

GitHub は、Git リポジトリー用の Web ベースのホスティング・サービスです。リポジトリーのローカル・コピーとリモート・コピーの両方を保有することができ、それによって共同作業が容易になります。 

GitHub Issues は、ユーザーの作業と計画をすべて一か所で保持するトラッキング・ツールです。これは、ユーザーが重要タスクに注力できるようにユーザーの開発リポジトリーと統合されます。

クラウド上でソース・コードを管理するため、次のようにして GitHub を構成します。

1. ツールチェーン作成時にこのツール統合を構成している場合、以下の手順を実行します。

 a. 「構成可能な統合 (Configurable Integrations)」セクションで**「GitHub」**をクリックします。GitHub にアクセスできるよう {{site.data.keyword.Bluemix_notm}} を認可していない場合、**「認可 (Authorize)」**をクリックして GitHub Web サイトに移動します。アクティブな GitHub セッションがない場合は、ログインするようプロンプトが出されます。**「Authorize Application」**をクリックして、{{site.data.keyword.Bluemix_notm}} がユーザーの GitHub アカウントにアクセスすることを許可します。アクティブな GitHub セッションがあるが、最近パスワードを入力していなかった場合は、確認のために GitHub パスワードを入力するようプロンプトが出されることがあります。
 
 b. GitHub リポジトリーのデフォルト・ターゲット・リポジトリー・ロケーションを検討します。それらのリポジトリーはサンプル・リポジトリーから複製されたものです。必要に応じて、ターゲット・リポジトリーの名前を変更します。
 ![デフォルト・ターゲット・リポジトリー・ロケーション](images/toolchain_github_config.png)
   
1. ツールチェーンが既にあり、このツール統合をそのツールチェーンに追加する場合、DevOps ダッシュボードの**「ツールチェーン」**タブでそのツールチェーンをクリックして、そのツールチェーンの「ツール統合  (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの「継続的なデリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで**「GitHub」**をクリックします。
1. 所有している GitHub リポジトリーがあり、それを使用したい場合は、その URL を入力します。リポジトリー・タイプには、**「リンク」**をクリックします。
1. 新規 GitHub リポジトリーを使用したい場合は、その GitHub リポジトリーに付ける名前を入力し、複製またはフォークするリポジトリーの URL を入力し、リポジトリー・タイプを次のように選択します。 

 a. 空のリポジトリーを作成するには、**「新規」**をクリックします。 
 
 b. GitHub リポジトリーのコピーを作成するには、**「複製 (Clone)」**をクリックします。
 
 c. プル要求を介して変更を提供できるように GitHub リポジトリーをフォークするには、**「フォーク (Fork)」**をクリックします。
 
1. 問題をトラッキングするために GitHub Issues を使用したい場合、**「GitHub Issues を有効にする (Enable GitHub Issues)」**チェック・ボックスを選択します。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 操作したい GitHub リポジトリーのタイルをクリックします。GitHub Web サイトが開き、そこでリポジトリーの内容を確認できます。
 
  **ヒント**: Eclipse Orion {{site.data.keyword.webide}} の統合ソース・コード管理ツールを使用して、GitHub リポジトリーを編集し、ワークスペースからアプリをデプロイすることができます。

1. GitHub Issues を有効にした場合、GitHub Issues のタイルをクリックして開きます。

詳しくは、『[GitHub](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window}』および『[GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}』を参照してください。


## Dedicated GitHub Enterprise の構成
{: #configghe}

{{site.data.keyword.ghe_long}} は、Git リポジトリー用のオンプレミスの Web ベースのホスティング・サービスです。Dedicated GitHub Enterprise は、{{site.data.keyword.Bluemix_notm}} Dedicated のお客様のみを対象としています。GitHub Issues は、ユーザーの作業と計画を一か所で保持するトラッキング・ツールです。これは、ユーザーが重要タスクに注力できるようにユーザーの開発リポジトリーと統合されます。Dedicated GitHub Enterprise および GitHub Issues について詳しくは、『[Dedicated GitHub Enterprise の使用](../services/ghededicated/index.html){: new_window}』および『[GitHub Issues](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}』を参照してください。

{{site.data.keyword.ghe_short}} をツールチェーン内の 1 つのツール統合として構成して、会社の [{{site.data.keyword.Bluemix_notm}} Dedicated](../dedicated/index.html#dedicated){: new_window} インスタンス内でソース・コードを管理できるようにすることができます。

1. ツールチェーン作成時にこのツール統合を構成している場合、以下の手順を実行します。

 a. Dedicated GitHub Enterprise に初めてログインする前に、社内の地域管理者に依頼して、社内ユーザー・レジストリーから自分のユーザー ID を {{site.data.keyword.Bluemix_notm}} Dedicated インスタンスに LDAP を使用して追加してもらってください。{{site.data.keyword.ghe_short}} アカウントのセットアップについて詳しくは、『[Dedicated GitHub Enterprise の使用](../services/ghededicated/index.html){: new_window}』を参照してください。
 
 b. 「構成可能な統合 (Configurable Integrations)」セクションで**「{{site.data.keyword.ghe_short}}」**をクリックします。    
 
 c. 新規 {{site.data.keyword.ghe_short}} リポジトリーのデフォルト名を検討します。必要な場合、この新規リポジトリーの名前を変更します。次のイメージは、サンプル・リポジトリーから複製されたリポジトリーの例を示しています。既存のリポジトリーまたは新規リポジトリーを使用することができます。新規リポジトリーを使用するには、空のリポジトリーを作成するか、リポジトリーを複製するか、またはリポジトリーをフォークします。
 ![デフォルト・リポジトリー・ロケーション](images/toolchain_ghe_config.png)
   
1. {{site.data.keyword.Bluemix_notm}} Public にツールチェーンがあり、そのツールチェーンにこのツール統合を追加しようとしている場合、DevOps ダッシュボードの**「ツールチェーン」**タブでそのツールチェーンをクリックして、そのツールチェーンの「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの「継続的なデリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。{{site.data.keyword.Bluemix_notm}} Dedicated でツールチェーンを使用している場合、ダッシュボードの**「DEVOPS」** タブでそのツールチェーンをクリックして、そのツールチェーンの「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの右上隅にある**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで**「{{site.data.keyword.ghe_short}}」**をクリックします。
1. 使用したい {{site.data.keyword.ghe_short}} リポジトリーがある場合、そのリポジトリーの URL を入力します。リポジトリー・タイプには、**「既存」**をクリックします。
1. 新規 {{site.data.keyword.ghe_short}} リポジトリーを使用したい場合、そのリポジトリーに付ける名前を入力し、複製またはフォークするリポジトリーの URL を入力し、リポジトリー・タイプを次のように選択します。 

 a. 空のリポジトリーを作成するには、**「新規」**をクリックします。 
 
 b. リポジトリーのコピーを作成するには、**「複製 (Clone)」**をクリックします。
 
 c. プル要求を介して変更を提供できるようにリポジトリーをフォークするには、**「フォーク (Fork)」**をクリックします。
 
1. 問題をトラッキングするために GitHub Issues を使用するには、**「GitHub Issues を有効にする (Enable GitHub Issues)」**チェック・ボックスを選択します。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 操作したい {{site.data.keyword.ghe_short}} リポジトリーのタイルをクリックします。会社の [{{site.data.keyword.Bluemix_notm}} Dedicated](../dedicated/index.html#dedicated){: new_window} インスタンスが開き、そこでリポジトリーの内容を確認できます。
 
  **ヒント**: Eclipse Orion {{site.data.keyword.webide}} の統合ソース・コード管理ツールを使用して、{{site.data.keyword.ghe_short}} リポジトリーを編集し、ワークスペースからアプリをデプロイすることができます。

1. GitHub Issues を有効にした場合、GitHub Issues のタイルをクリックします。

<!-- 8/23/2016: The GHE Dedicated content has been moved to docs-staging/services/ghededicated/index.md -->

## PagerDuty の構成
{: #pagerduty}

PagerDuty は、複数のモニタリング・システムからのデータを単一ビューに集約します。何らかの問題が起こったとき、PagerDuty は、その時点でその問題を解決する能力の最も高いチーム・メンバーに通知が確実に伝わるようにします。そのチーム・メンバーが問題に応答しない場合、次の技術者または運用管理者に問題を転送するようにエスカレーションを構成できます。

パイプライン・ステージでの障害発生時に通知を送信するように PagerDuty を構成して、問題を迅速に修正してダウン時間を削減できるようにします。

1. ツールチェーン作成時にこのツール統合を構成している場合、「構成可能な統合 (Configurable Integrations)」セクションで**「PagerDuty」**をクリックします。
1. ツールチェーンが既にあり、このツール統合をそのツールチェーンに追加する場合、DevOps ダッシュボードの**「ツールチェーン」**タブでそのツールチェーンをクリックして、そのツールチェーンの「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの「継続的なデリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで**「PagerDuty」**をクリックします。
1. PagerDuty アカウントと関連付けられた PagerDuty サイト名を入力します。PagerDuty アカウントをお持ちでない場合、[登録して取得](https://signup.pagerduty.com/accounts/new){: new_window}してください。
1. PagerDuty アカウントの API アクセス・キーを入力します。キーを検出する方法については、[API Authentication](https://signup.pagerduty.com/accounts/new){: new_window} を参照してください。
1. PagerDuty サービスの名前を入力します。
1. 1 次 PagerDuty 連絡先の E メール・アドレスを入力します。
1. 1 次 PagerDuty 連絡先の電話番号を入力します。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. PagerDuty のタイルをクリックして pagerduty.com に移動します。ツールチェーン用にこのツール統合を構成したときに指定した PagerDuty サービスと関連付けられたイベントを表示できます。 

詳細については、[PagerDuty](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window} を参照してください。


## Sauce Labs の構成
{: #saucelabs}

Sauce Labs は、機能についての単体テストを実行します。{{site.data.keyword.deliverypipeline}} 内のテスト・ジョブとして Sauce Labs テスト・スイートが構成されている場合、そのテスト・スイートは、継続的デリバリー・プロセスの一環として、Web アプリまたはモバイル・アプリに対するテストを実行できます。これらのテストは、誤ったコードがデプロイされるのを防ぐためのゲートとして機能することで、プロジェクトのフロー制御に役立ちます。

Sauce Labs を構成して、自動化された機能テストを複数のオペレーティング・システムおよびブラウザーで実行することによって、ユーザーによる Web サイトやアプリケーションの使用方法をエミュレートできます。

1. ツールチェーン作成時にこのツール統合を構成している場合、「構成可能な統合 (Configurable Integrations)」セクションで**「Sauce Labs」**をクリックします。
1. ツールチェーンが既にあり、このツール統合をそのツールチェーンに追加する場合、DevOps ダッシュボードの**「ツールチェーン」**タブでそのツールチェーンをクリックして、そのツールチェーンの「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの「継続的なデリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで**「Sauce Labs」**をクリックします。
1. Sauce Labs アカウントと関連付けられたユーザー名を入力します。[Sauce Labs アカウント・ページの上部のウェルカム・メッセージでユーザー名を見つける](https://saucelabs.com/account){: new_window}ことができます。
1. Sauce Labs アカウントのアクセス・キーを入力します。[Sauce Labs アカウント・ページの左下隅でキーを見つける](https://saucelabs.com/account){: new_window}ことができます。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. Sauce Labs のタイルをクリックして saucelabs.com に移動し、ツールチェーン用のテスト・アクティビティーを表示します。

 **ヒント**: Sauce Labs テスト・ジョブを {{site.data.keyword.deliverypipeline}} に追加した場合、サービス・インスタンスを選択できます。

詳細については、『[Sauce Labs](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}』を参照してください。


## Slack の構成
{: #slack}

**重要**: パブリック Slack チャネルに送信される通知は、チーム全員が見ることができます。送信内容は自身の責任であることに留意してください。

Slack は、クラウド・ベースのリアルタイムでのメッセージングおよび通知のシステムです。Slack は、チームでの共同作業のために E メールよりもさらにインタラクティブな持続的チャットを提供します。専用チャネルまたは作業に直接関連する一連のチャネルで、チームと連絡を取ることができます。また、それらのチャネルを介して、あるいは、複数のメンバー間での直接メッセージによって、ファイルおよびイメージを共有することができます。直接メッセージでの通信およびチャネルでの通信は保持され、検索できるようになっています。 

Slack を構成して、ツール統合からのツールチェーンに関する通知 (例えばテストや実装のアクティビティーなど) を受け取ります。

1. ツールチェーン作成時にこのツール統合を構成している場合、「構成可能な統合 (Configurable Integrations)」セクションで**「Slack」**をクリックします。
1. ツールチェーンが既にあり、このツール統合をそのツールチェーンに追加する場合、DevOps ダッシュボードの**「ツールチェーン」**タブでそのツールチェーンをクリックして、そのツールチェーンの「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの「継続的なデリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで**「Slack」**をクリックします。
1. Slack アカウントの API 認証トークンを入力します。Slack で認証するためには、生成されたフルアクセス・トークンを使用する必要があります。トークンを見つける方法については、[Slack の Authentication](https://api.slack.com/web#authentication){: new_window} を参照してください。
1. 通知の送信先にする Slack チャネルの名前を入力します。指定したチャネルが存在しない場合は作成されます。チャネルがアーカイブされていた場合、再アクティブ化されます。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. Slack のタイルをクリックします。構成された Slack チャネルに、ツールチェーン用のすべてのアクティビティーが表示されます。

詳細については、『[Slack](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}』を参照してください。
