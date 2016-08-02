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

*最終更新日: 2016 年 6 月 17 日*
{: .last-updated}

ツールチェーンを作成するときに開発、デプロイメント、運用の作業をサポートするツール統合を構成したり、既存のツールチェーンにツール統合を追加、構成してカスタマイズしたりできます。  
{:shortdesc}

**重要**: この機能は試験段階です。ツールチェーンは安定していない可能性があり、前のバージョンとは互換性のない変更が加えられる場合があります。実稼働環境での使用は推奨されません。ツールチェーンを使用するには、一回限りの[アクセスの要求](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}を行う必要があります。ツールチェーンは米国南部地域でのみ利用可能です。

**ヒント**: ソース・コードでの開発を開始する場合は、{{site.data.keyword.deliverypipeline}} を構成する前に、GitHub と GitHub Issues ツールを構成してください。

## Delivery Pipeline の構成
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} は、入力を取得してビルド、テスト、デプロイメントなどのジョブを実行する一連のステージによって、プロジェクトの継続的デプロイメントを自動化します。 

{{site.data.keyword.deliverypipeline}} を構成し、アプリケーションの継続的なビルド、テスト、デプロイメントを自動化します。 

1. ツールチェーンを作成しているときにこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで、**「Delivery Pipeline」**をクリックします。使用するテンプレートに応じて、異なるフィールドを利用できます。デフォルトのフィールド値を確認し、必要に応じてそれらの設定を変更します。
1. 既に存在するツールチェーンに、このツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**タブで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「Delivery Pipeline」**をクリックします。
1. 新しいパイプラインの名前を指定します。
1. パイプラインを使用してユーザー・インターフェースをデプロイしようと計画している場合は、**「表示可能なアプリケーション (Viewable App)」**チェック・ボックスにチェック・マークを付けます。パイプラインで作成されるすべてのアプリケーションが、ツールチェーンの「ツール統合 (Tool Integrations) 」ページの**「アプリの表示 (VIEW APP)」**リストに表示されます。
1. **「統合の作成 (Create Integration)」**をクリックして、{{site.data.keyword.deliverypipeline}} をツールチェーンに追加します。
1. {{site.data.keyword.deliverypipeline}} のタイルをクリックし、パイプラインを表示して構成します。パイプラインの構成方法の基本を確認するには、[パイプラインのビルドとデプロイ](../services/DeliveryPipeline/build_deploy.html){: new_window}を参照してください。

  **ヒント**: 変更を GitHub リポジトリーにプッシュしたときにパイプラインをトリガーしたい場合は、パイプラインのステージを定義する前に、ツールチェーン用の GitHub を構成しておく必要があります。パイプラインのステージには、GitHub リポジトリーの Git URL が必要です。パイプラインのステージごとに、ツールチェーンに関連付けられている GitHub リポジトリーを 1 つのみ参照できます。GitHub の構成手順については、[GitHub および GitHub Issues](#github)のセクションを参照してください。
  
1. オプション: Sauce Labs でアプリケーションのテストを実行したい場合は、Sauce Labs テスト・ジョブを追加するように {{site.data.keyword.deliverypipeline}} を構成します。テスト・ジョブの構成手順については、「[パイプラインに SauceLabs テスト・ジョブを構成する](#config_saucelabs)」セクションを参照してください。

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
  
1. デプロイ・ジョブを構成します。**「デプロイ・スクリプト (Deploy Script)」**フィールドに、コマンド「export CF_APP_NAME="$CF_APP"」を含めます。このコマンドは、アプリケーション名を環境プロパティーとしてエクスポートします。
1. テスト・ジョブを構成します。次の図は、値の例を示しています。
**「サービス・インスタンス」**、**「ターゲット」**、**「組織」**、および**「スペース」**フィールドには、現在使用している Sauce Labs のユーザー名、地域、組織、スペースが取り込まれます。
![ジョブの構成](images/toolchain_configure_job.png)

  a. テスター・タイプでは、**「Sauce Labs」**を選択します。
  
  b. サービス・インスタンスでは、ツールチェーンに Sauce Labs を構成したときに使用した Sauce Labs のユーザー名を選択します。 
  
   **ヒント**: ツールチェーンで Sauce Labs を構成したときに使用したユーザー名とアクセス・キーを確認するには、**「構成」**をクリックします。 
  
  c. **「テスト実行コマンド (Test Execution Command)」**フィールドに、テストに必要な依存関係をインストールしてテストを実行するコマンドを入力します。例えば、仮に Node.js アプリケーションをテストする場合は、次のように入力します。
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```
  
    d. テスト・ジョブ・ログでテストのレポートを確認する場合は、**「テスト・レポートを有効にする (Enable Test Report)」**チェック・ボックスにチェックマークを付け、「テスト結果のファイル・パターン (Test Result File Pattern)」を `test/*.xml` に設定します。
  
1. **「保存」**をクリックします。これで、パイプラインが実行されるときには必ず Sauce Labs のテストが実行されるようになりました。

詳しくは、「[Delivery Pipeline](https://www.ibm.com/devops/method/content/deliver/tool_build_and_deploy/){: new_window}」を参照してください。

## Deployment Risk Analytics の追加
{: #dra}

{{site.data.keyword.DRA_full}} は、単体テスト、機能テスト、およびコード・カバレッジ・ツールからの結果を収集して分析し、コードがデプロイメント・プロセスの指定されたゲートで事前定義の基準を満たすかどうかを判断します。コードが基準を満たしていない、または基準を超えていない場合、リスクがリリースされないように、デプロイメントが停止されます。継続的デリバリー環境のセーフティー・ネットとして、または品質基準を実装して向上させる方法として、Deployment Risk Analytics を使用することができます。 

 **ヒント**: このツール統合は、事前構成されています。構成パラメーターは不要で、再構成はできません。
 
Deployment Risk Analytics を追加し、デプロイメントをモニタリングしてリリース前にリスクを洗い出すことで、Bluemix のコードの品質を維持し、向上させることができます。

1. 既に存在するツールチェーンに、このツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**タブで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「Deployment Risk Analytics」**をクリックします。 
1. **「統合の作成 (Create Integration)」**をクリックします。
1. Deployment Risk Analytics のタイルをクリックし、基準を作成する、基準をパイプラインに接続する、パイプラインを実行する、という開始手順を完了させます。詳細については、「[Deployment Risk Analytics](https://www.ibm.com/devops/method/content/deliver/tool_deployment_risk_analytics/){: new_window}」を参照してください。

## Eclipse Orion {{site.data.keyword.webide}} の追加
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} は、ソース管理タスクを作成、編集、実行、デバッグ、完了できる Web ベースの統合環境です。
編集から実行、送信、そしてデプロイまで、シームレスに行うことができます。 

 **ヒント**: このツール統合は、事前構成されています。構成パラメーターは不要で、再構成はできません。
 
Eclipse Orion {{site.data.keyword.webide}} ツール統合を追加して、ソース管理タスクを完了させます。

1. 既に存在するツールチェーンに、このツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**タブで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「Eclipse Orion Web IDE」**をクリックします。 
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 新しい Eclipse Orion Web IDE のタイルをクリックします。ワークスペースに GitHub リポジトリーが取り込まれます。現在のツールチェーンに関連付けられたリポジトリーが強調表示されます。

詳しくは、「[Web IDE](https://www.ibm.com/devops/method/content/code/tool_web_ide/){: new_window}」を参照してください。


## GitHub と GitHub Issues の構成
{: #github}

GitHub は、Web ベースの Git リポジトリー・ホスティング・サービスです。リポジトリーのローカルとリモートの両方のコピーを持つことができるので、共同作業が容易になります。 

GitHub Issues は、作業と計画をすべて 1 箇所に保持するトラッキング・ツールです。開発リポジトリーに統合されるため、重要なタスクに集中できます。

GitHub と GitHub Issues を構成して、クラウドでソース・コードを管理します。

1. ツールチェーンを作成しているときにこのツール統合を構成する場合は、次の手順を実行します。

 a. 「構成可能な統合 (Configurable Integrations)」セクションで、**「GitHub」**をクリックします。GitHub へのアクセスを {{site.data.keyword.Bluemix}} に許可していない場合は、**「許可 (Authorize)」**をクリックして、GitHub の Web サイトに移動します。アクティブな GitHub セッションがない場合は、ログインを求めるプロンプトが出されます。**「アプリケーションを許可 (Authorize Application)」**をクリックして、{{site.data.keyword.Bluemix}} が GitHub アカウントにアクセスできるようにします。アクティブな GitHub セッションがあるが、最近パスワードを入力していない場合は、GitHub パスワードを入力して確認するよう求めるプロンプトが出される場合があります。
 
 b. GitHub リポジトリーのデフォルトのターゲット・リポジトリーのロケーションを確認します。これらのリポジトリーは、サンプル・リポジトリーのクローンです。必要に応じて、ターゲット・リポジトリーの名前を変更します。
![デフォルトのターゲット・リポジトリーのロケーション](images/toolchain_github_config.png)
   
1. 既に存在するツールチェーンに、このツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**タブで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「GitHub」**をクリックします。
1. 既存の GitHub リポジトリーを使用する場合は、その URL を入力します。リポジトリー・タイプで、**「リンク (Link)」**をクリックします。
1. 新しい GitHub リポジトリーを使用する場合は、GitHub リポジトリーの名前を入力し、クローン作成またはフォークするリポジトリーの URL を入力し、リポジトリーのタイプを選択します。 

 a. 空のリポジトリーを作成するには、**「新規 (New)」**を選択します。 
 
 b. GitHub リポジトリーのコピーを作成するには、**「クローンを作成する (Clone)」**を選択します。
 
 c. プル要求で変更を導くことができるよう GitHub リポジトリーをフォークするには、 **「フォーク (Fork)」**を選択します。
 
1. 問題のトラッキングに GitHub Issues を使用する場合は、**「GitHub Issues を使用可能にする (Enable GitHub Issues)」**チェック・ボックスにチェック・マークを付けます。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 作業する GitHub リポジトリーのタイルをクリックし、github.com に移動してリポジトリーのコンテンツを表示します。
 
  **ヒント**: Eclipse Orion Web IDE の統合されたソース・コード管理ツールを使用して、GitHub リポジトリーを編集し、ワークスペースからアプリケーションをデプロイできます。

1. GitHub Issues を使用可能にした場合は、GitHub Issues のタイルをクリックして、GitHub Issues に移動します。

詳しくは、[「GitHub」](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window}と[「GitHub Issues」](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}を参照してください。    

##Dedicated {{site.data.keyword.ghe_short}} の使用
{: #ghe}

{{site.data.keyword.ghe_long}} は、IBM クラウドがホストする完全に管理されたバージョンの {{site.data.keyword.ghe_short}} であり、Dedicated Bluemix 環境で利用できます。GitHub は、開発者に愛されるソーシャル・コーディング体験を提供します。[{{site.data.keyword.Bluemix_notm}}Dedicated](../dedicated/index.html#dedicated){: new_window} は、物理的に切り離されたハードウェア上に、お客様のネットワークと統合されたクラウド・コンピューティング環境を実現します。

Dedicated {{site.data.keyword.ghe_short}} は、 {{site.data.keyword.Bluemix_notm}} Dedicated のお客様のみを対象とします。

### アカウントのセットアップ 

{{site.data.keyword.ghe_short}} には、{{site.data.keyword.Bluemix_notm}} Dedicated とのシングル・サインオンが含まれています。{{site.data.keyword.ghe_short}} にログインするには、地域の管理者、または「ようこそ」E メールの URL をブラウザーに貼り付けます。URL は、`github.your-company-dedicated-name.bluemix.net` というパターンに従います。{{site.data.keyword.Bluemix_notm}} Dedicated のユーザー ID とパスワードを使用してサインインすると、{{site.data.keyword.ghe_short}} アカウントが自動的に作成されます。

**注意:** ユーザー ID が存在しないというメッセージが表示されたら、地域の管理者にユーザー ID を {{site.data.keyword.Bluemix_notm}} Dedicated のユーザー・レジストリーに追加してもらいます。地域の管理者は、[{{site.data.keyword.Bluemix_notm}} Dedicated のユーザーと権限](https://new-console.stage1.ng.bluemix.net/docs/admin/index.html#oc_useradmin){: new_window}を参照してください。

ほとんどの場合、GitHub のユーザー名は E メールの短縮名です。ただし、ピリオドなど GitHub がサポートしない文字が短縮名に含まれている場合を除きます。GitHub がサポートしない文字が短縮名に含まれている場合、その文字はダッシュに置き換えられます。     

### E メール・アドレスをアカウントに追加する

通知を受信するには、E メール・アドレスを {{site.data.keyword.ghe_short}} アカウントの設定に追加する必要があります。E メール・アドレスを追加したら、{{site.data.keyword.ghe_short}} のソーシャル・コーディング機能を利用できます。    
 
E メール・アドレスを Dedicated {{site.data.keyword.ghe_short}} アカウントに追加するには、次の手順を実行します。    
1. GitHub の任意のページの右上で、プロファイル・アイコンをクリックし、**「設定」**をクリックします。    
2. サイドバーの**「E メール」**をクリックします。    
3. E メール・アドレスを追加して、**「追加」**をクリックします。     

{: #ghe_auth}
### 認証のための個人用アクセス・トークンまたは SSH 鍵を作成する

ローカルの Git リポジトリーからの `clone` や `push` などのリモート Git 操作を実行するには、個人用アクセス・トークンまたは SSH 鍵を使用して {{site.data.keyword.ghe_short}} で認証する必要があります。HTTPS による認証は、アクセス・トークンを使用する場合にのみサポートされます。ユーザー ID とパスワードを使用してローカル・リポジトリーのクローン作成またはプッシュを行うことはできません。API 要求にも、個人用アクセス・トークンが必要です。

**注意:** 認証のために個人用アクセス・トークンまたは SSH 鍵を使用するには、ローカルに Git をセットアップする必要があります。手順については、[Git のセットアップ方法](https://help.github.com/enterprise/2.6/user/articles/set-up-git/){: new_window}を参照してください。    

個人用アクセス・トークンを作成するには、以下の手順を実行します。    
   1. GitHub の任意のページの右上で、プロファイル・アイコンをクリックし、**「設定」**をクリックします。    
   2. サイドバーの**「個人用アクセス・トークン (Personal access tokens)」**をクリックします。   
   3. **「新規トークンの生成 (Generate new token)」**をクリックします。

   4. トークンの説明を追加して、**「トークンの生成 (Generate token)」**をクリックします。
   5. トークンを安全な場所またはパスワード管理アプリケーションにコピーします。
**注意:** セキュリティー上の理由から、このページを離れた後にトークンをもう一度表示することはできません。    

HTTPS を使用したコマンド・ライン・アクセスでは、パスワードの代わりに個人用アクセス・トークンを使用します。 


SSH 鍵を作成するには、以下の手順を実行します。
   1. Git Bash (Windows) または新しいターミナル・ウィンドウ (Linux と Mac) を開きます。    
   2. 次のテキストを貼り付けます。{{site.data.keyword.ghe_short}} アカウントに追加した E メール・アドレスに置き換えてください。
   
     ``
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
     # 指定された E メールをラベルとして使用し、新しい SSH 鍵を作成します。
     公開/秘密 RSA 鍵ペアを生成します。
``


   3. 鍵を保存するファイルを指定するよう求めるプロンプトが出されたら、Enter を押してデフォルトの場所を受け入れます。
   4. プロンプトで、セキュアなパスフレーズを入力します。詳細については、[SSH 鍵パスフレーズの使用方法](https://help.github.com/enterprise/2.6/user/articles/working-with-ssh-key-passphrases/){: new_window}を参照してください。   

SSH 鍵を ssh-agent に追加します。    
   1. ssh-agent が使用可能になっていることを確認してください。Git Bash を使用して、次のコマンドを入力し、ssh-agent を使用可能にします。
      ``
      # ssh-agent をバックグラウンドで開始する
      $ eval "$(ssh-agent -s)"
      Agent pid 59566
      ``    
  
   2. 次のコマンドを入力して、SSH 鍵を ssh-agent に追加します。
      ``
      $ ssh-add ~/.ssh/id_rsa
      ``    
   3. SSH 鍵を GitHub アカウントに追加します。詳細については、[新しい SSH 鍵を GitHub アカウントに追加する方法](https://help.github.com/enterprise/2.6/user/articles/adding-a-new-ssh-key-to-your-github-account/){: new_window}を参照してください。    
   

### GitHub の組織、チーム、リポジトリーのセットアップ    

GitHub の組織をセットアップして、同じようなプロジェクトやタスクに取り組む個々のユーザー・グループを作成すると便利です。
組織内にチームを編成すると、リポジトリーへのアクセスを制御できるという追加の利点があります。詳しくは、[組織とチーム](https://help.github.com/enterprise/2.6/admin/guides/user-management/organizations-and-teams/){: new_window}を参照してください。

**注意:** GitHub の組織は、Bluemix の組織と同じではありません。

次のタスクを実行して、チームのプロジェクトをセットアップします。

   1. [組織を作成します](https://help.github.com/enterprise/2.6/user/articles/creating-a-new-organization-account/){: new_window}。
   2. [組織のリポジトリーを作成します](https://help.github.com/enterprise/2.6/user/articles/create-a-repo/){: new_window}。
   3. [組織に参加するようにユーザーを招待します](https://help.github.com/enterprise/2.6/user/articles/inviting-users-to-join-your-organization/){: new_window}。
   4. [組織の所有者権限を持たせるチーム・メンバー (1 人以上) を慎重に選択します](https://help.github.com/enterprise/2.6/user/articles/changing-a-person-s-role-to-owner/){: new_window}。    
   
  **注意:** ユーザーを組織に招待するには、それまでにそのユーザーが {{site.data.keyword.ghe_short}} に 1 回以上ログインしている必要があります。そうでない {{site.data.keyword.ghe_short}} アカウントを招待することはできません。
   
### サポートについて
回答を今すぐ入手するには、質問を [スタック・オーバーフロー](http://stackoverflow.com/questions/ask?tags=ibm-bluemix_github-enterprise){: new_window}に送信します。 

さらにサポートが必要な場合は、次のリソースを利用します。    
   1. https://ibm.biz/bluemixsupport のフォームに入力します。   
   2. Client Success Portal (https://support.ibmcloud.com/ics/support/mylogin.asp?login=bluemix) で新しいチケットを送信します。    


## PagerDuty の構成
{: #pagerduty}

PagerDuty は、複数のモニタリング・システムのデータを単一のビューに統合します。問題が発生すると、PagerDuty はそのとき問題を修正できる最適なチーム・メンバーに通知します。そのチーム・メンバーが問題に対応しない場合は、エスカレーションを構成して、2 番目のエンジニアまたは運用マネージャーに転送することができます。

パイプライン・ステージの障害が発生したときに通知を送信するよう PagerDuty を構成し、問題を迅速に修正して、ダウン時間を減少できるようにします。

1. ツールチェーンを作成しているときにこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで、**「PagerDuty」**をクリックします。
1. 既に存在するツールチェーンに、このツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**タブで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「PagerDuty」**をクリックします。
1. PagerDuty アカウントと関連付けられている PagerDuty のサイト名を入力します。PagerDuty アカウントがない場合は、 [アカウントを登録します](https://signup.pagerduty.com/accounts/new){: new_window}。
1. PagerDuty アカウントの API アクセス・キーを入力します。キーを見つける手順については、[API 認証](https://signup.pagerduty.com/accounts/new){: new_window}を参照してください。
1. PagerDuty サービスの名前を入力します。
1. PagerDuty の 1 次連絡先の E メール・アドレスを入力します。
1. PagerDuty の 1 次連絡先の電話番号を入力します。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. PagerDuty のタイルをクリックして、pagerduty.com にアクセスします。ツールチェーンに対してこのツール統合を構成したときに指定した、PagerDuty サービスに関連付けられているイベントを表示できます。 

詳しくは、[PagerDuty](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}を参照してください。


## Sauce Labs の構成
{: #saucelabs}

Sauce Labs は、機能単体テストを実行します。Sauce Labs のテスト・スイートを {{site.data.keyword.deliverypipeline}} にテスト・ジョブとして構成した場合、テスト・スイートは、継続的デリバリー・プロセスの一部として Web アプリケーションまたはモバイル・アプリケーションに対してテストを実行できます。これらのテストは、プロジェクトの重要なフロー制御を提供し、誤ったコードのデプロイメントを防ぐゲートとして機能します。

自動化された機能テストを複数のオペレーティング・システムとブラウザーで実行するように Sauce Labs を構成します。これにより、ユーザーが Web サイトまたはアプリケーションを使用する可能性がある方法をエミュレートできます。

1. ツールチェーンを作成しているときにこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで、**「Sauce Labs」**をクリックします。
1. 既に存在するツールチェーンに、このツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**タブで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。 
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「Sauce Labs」**をクリックします。
1. Sauce Labs アカウントと関連付けられているユーザー名を入力します。[ユーザー名は、Sauce Labs のアカウント・ページ上部のウェルカム・メッセージにあります](https://saucelabs.com/account){: new_window}。
1. Sauce Labs アカウントのアクセス・キーを入力します。[キーは、Sauce Labs のアカウント・ページの左下隅にあります](https://saucelabs.com/account){: new_window}。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. Sauce Labs のタイルをクリックして、saucelabs.com に移動し、ツールチェーンのテスト・アクティビティーを表示します。

 **ヒント**: Sauce Labs テスト・ジョブを {{site.data.keyword.deliverypipeline}} に追加した場合は、サービス・インスタンスを選択できます。

詳しくは、[Sauce Labs](https://www.ibm.com/devops/method/content/code/tool_sauce_labs/){: new_window}を参照してください。


## Slack の構成
{: #slack}

**重要**: Slack の公開チャネルに投稿された通知は、チームの全員に表示されます。投稿したコンテンツの責任はお客様が負うことに注意してください。

Slack は、リアルタイム・メッセージングと通知を提供するクラウド・ベースのシステムです。
Slack が提供する永続的なチャットは、E メールの代わりに使用できる対話性に優れたチームのコラボレーション手段になります。
チームとのコミュニケーションには、専用チャネルを使用することも、作業に直接関連する一連のチャネルを使用することもできます。また、チャネルを通じて、または 2 人以上のメンバーでのダイレクト・メッセージで、ファイルとイメージを共有することもできます。ダイレクト・メッセージとチャネル上の通信は保持されるため、検索することができます。 

テストやデプロイのアクティビティーなどのツールチェーンに関する通知をツール統合から受信するように Slack を構成します。

1. ツールチェーンを作成しているときにこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで、**「Slack」**をクリックします。
1. 既に存在するツールチェーンに、このツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**タブで、ツールチェーンをクリックして「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合 (Tool Integrations)」**をクリックします。
1. 追加ボタン (+) をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで、**「Slack」**をクリックします。
1. Slack アカウントの API 認証トークンを入力します。Slack での認証には、生成されたフルアクセス・トークンを使用する必要があります。トークンを見つける手順については、[Slack 認証](https://api.slack.com/web#authentication){: new_window}を参照してください。
1. 通知を送信する Slack チャネルの名前を入力します。指定したチャネルが存在しない場合は、そのチャネルが作成されます。チャネルがアーカイブされたら、再アクティブ化します。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. Slack のタイルをクリックします。構成した Slack チャネルでツールチェーンのアクティビティーをすべて表示できます。

詳しくは、[Slack](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window}を参照してください。
