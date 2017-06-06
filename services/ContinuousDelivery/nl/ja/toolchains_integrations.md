---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}    

# ツール統合の構成
{: #integrations}

開発、デプロイメント、および運用の作業をサポートするツール統合をオープン・ツールチェーンの作成時に構成するか、ツール統合を追加および構成して既存のツールチェーンをカスタマイズすることができます。  
{:shortdesc}

ツールチェーンで追加および構成できるツール統合は、{{site.data.keyword.Bluemix_notm}} Public または {{site.data.keyword.Bluemix_notm}} Dedicated のどちらを使用しているかによって異なります。{{site.data.keyword.Bluemix_notm}} Dedicated でツールチェーンを使用している場合、利用できるツール統合は、特定の環境で {{site.data.keyword.contdelivery_full}} がどのように設定されたかに応じて異なります。

|ツール統合 |{{site.data.keyword.Bluemix_notm}} Public で利用可能	|{{site.data.keyword.Bluemix_notm}} Dedicated で利用可能 (環境依存)|
|:----------|:------------------------------|:------------------|
|{{site.data.keyword.alertnotificationshort}}		|はい		|いいえ		|
|Artifactory		|はい		|いいえ		|
|Availability Monitoring		|はい		|いいえ		|
|Cloud Event Management		|はい		|いいえ		|
|{{site.data.keyword.deliverypipeline}} 		|はい	   	|はい  		|
|{{site.data.keyword.DRA_short}} 		|はい		|いいえ			|
|Eclipse Orion {{site.data.keyword.webide}}		|はい		|はい			|
|Git Repos and Issue Tracking	|はい		|いいえ		|
|GitHub and Issues		|はい		|はい		|
|Dedicated {{site.data.keyword.ghe_short}} and Issues			|いいえ		|はい		|
|Jenkins		|はい		|いいえ		|
|JIRA		|はい		|いいえ		|
|Nexus			|はい		|いいえ		|
|その他のツール			|はい		|はい		|
|PagerDuty			|はい		|はい		|
|Sauce Labs		|はい		|いいえ		|
|Slack			|はい		|はい		|
|SonarQube			|はい		|いいえ		|
{: caption="表 1. Bluemix Public および Dedicated でツールチェーンに使用可能なツール統合" caption-side="top"}

**ヒント:** {{site.data.keyword.Bluemix_notm}} Public でソース・コードでの開発を開始する場合は、{{site.data.keyword.deliverypipeline}} を構成する前に GitHub ツール統合または Git Repos and Issue Tracking ツール統合を構成してください。{{site.data.keyword.Bluemix_notm}} Dedicated でコードでの開発を開始する場合は、{{site.data.keyword.deliverypipeline}} を構成する前に {{site.data.keyword.ghe_short}} ツール統合を構成します。


## Alert Notification (試験段階) の構成
{: #alertnotification}

{{site.data.keyword.alertnotificationfull}} は、通知戦略を中央化および簡素化するために使用できる、ハイブリッド・クラウド・ベースのソリューションです。他のクラウド・ベースのアプリケーションおよびオンプレミス・アプリケーションと連携して機能します。アラートはセキュアな RESTful API を使用して {{site.data.keyword.alertnotificationshort}} に転送されます。

DevOps 処理中の問題に関する通知を受け取るように {{site.data.keyword.alertnotificationshort}} を構成します。

### 前提条件

1. {{site.data.keyword.alertnotificationshort}} アカウントをお持ちでない場合、登録して取得します。

 a. IBM マーケットプレイスで [IBM {{site.data.keyword.alertnotificationshort}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/us-en/marketplace/alert-notification){: new_window} ページを開きます。

 b. サブスクリプションを購入するか、90 日間の無料評価版に申し込みます。

1. {{site.data.keyword.alertnotificationshort}} アカウントのセットアップが終わったら、[My IBM ダッシュボード ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://myibm.ibm.com/dashboard/){: new_window} を開きます。
1. IBM {{site.data.keyword.alertnotificationshort}} の横の**「起動」**をクリックします。
1. **「API キーの管理 (Manage API Keys)」**をクリックし、**「API キーの作成 (Create API Key)」**をクリックします。
1. **「API キーの作成 (Create API Key)」**フィールドに説明を入力します。
1. **「生成 (Generate)」**をクリックします。名前およびパスワードなどの新規 API キー情報が表示されます。この情報はツール統合の構成に必要であるため、「新規 API キー (New API Key)」ウィンドウを開いたままにしておいてください。セキュリティーのため、後で API キーのパスワードを取り出すことはできません。

### Alert Notification の構成

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「{{site.data.keyword.alertnotificationshort}}」**をクリックします。
1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。  

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「{{site.data.keyword.alertnotificationshort}}」**をクリックします。

1. 使用したい {{site.data.keyword.alertnotificationshort}} API の URL を入力します。URL は {{site.data.keyword.alertnotificationshort}} サービスの「API キーの管理 (Manage API Keys)」ページで見つけることができます (例: `https://ibmnotifybm.mybluemix.net/api/alerts/v1`)。
1. {{site.data.keyword.alertnotificationshort}} の API アクセス・キーを入力します。API キー名は「新規 API キー (New API Key)」ウィンドウで確認できます。
1. API キーに対して {{site.data.keyword.alertnotificationshort}} が生成したパスワードを入力します。API キーのパスワードは「新規 API キー (New API Key)」ウィンドウで確認できます。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. ツールチェーンから、**「{{site.data.keyword.alertnotificationshort}}」**をクリックします。

詳しくは、[IBM {{site.data.keyword.alertnotificationshort}}![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/manage/tool_alert_notification/){: new_window}を参照してください。


## Artifactory の構成
{: #artifactory}

ビルド成果物を Artifactory リポジトリーに保管するように Artifactory リポジトリー・マネージャーを構成します。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Artifactory」**をクリックします。
1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。  

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「Artifactory」**をクリックします。

1. Artifactory カードをクリックしたときに開くようにしたい Artifactory リポジトリーの URL を入力します。
1. 接続先にするリポジトリーのタイプを選択します。
1. Artifactory npm レジストリーを使用する場合は、以下のステップを実行します。

 a. レジストリーと関連付けられた E メール・アドレスを入力します。

 b. レジストリーと関連付けられた認証トークンを入力します。

 c. Artifactory サーバー上のプライベート・レジストリーである Artifactory リリース・リポジトリーの URL を入力します。

 d. 複数のパブリックおよびプライベート npm レジストリーを結合するために使用する Mirror または Public レジストリーの URL を入力します。例えば、この URL は、プライベート・レジストリーと、npm グローバル・レジストリーのキャッシュの両方にアクセスできる、Artifactory サーバー上の仮想レジストリーの URL であることができます。

1. Artifactory Maven リポジトリーを使用する場合は、以下のステップを実行します。

 a. リポジトリーと関連付けられたユーザー ID を入力します。

 b. リポジトリーと関連付けられたパスワードを入力します。

 c. Artifactory サーバー上のプライベート・リリース・リポジトリーである Artifactory リリース・リポジトリーの URL を入力します。

 d. Artifactory サーバー上のプライベート・スナップショット・リポジトリーである Artifactory スナップショット・リポジトリーの URL を入力します。

 e. 複数のパブリックおよびプライベート Maven リポジトリーを結合するために使用する Mirror または Public リポジトリーの URL を入力します。例えば、この URL は、プライベート・リポジトリーと、Maven 中央リポジトリーのキャッシュの両方にアクセスできる、Artifactory サーバー上の仮想リポジトリーの URL であることができます。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. 作業対象の Artifactory リポジトリーのカードをクリックします。Artifactory の Web サイトが開きます。そこでリポジトリーの内容を表示できます。
1. オプション: {{site.data.keyword.Bluemix_notm}} Public でツールチェーンを使用していて、Artifactory を npm と共に使用してアプリをビルドしたい場合、パイプラインを構成して npm ビルド・ジョブを追加します。ビルド・ジョブの構成手順については、『[パイプラインに Artifactory npm ビルド・ジョブを構成する](#config_artifactory_npm)』セクションを参照してください。
1. オプション: {{site.data.keyword.Bluemix_notm}} Public でツールチェーンを使用していて、Artifactory を Maven と共に使用してアプリをビルドしたい場合、パイプラインを構成して Maven ビルド・ジョブを追加します。ビルド・ジョブの構成手順については、『[パイプラインに Artifactory Maven ビルド・ジョブを構成する](#config_artifactory_maven)』セクションを参照してください。

### パイプラインに Artifactory npm ビルド・ジョブを構成する
{: #config_artifactory_npm}

パイプラインに npm ビルド・ジョブを構成する前に、ビルド SCM リポジトリーを入力として使用できる作業パイプラインがなければならず、また、ツールチェーンに Artifactory を構成しておく必要もあります。Artifactory の構成手順については、[Artifactory](#artifactory) のセクションを参照してください。

{{site.data.keyword.deliverypipeline}} を構成して npm ビルド・ジョブを追加します。

1. ステージを作成し、入力を適切な SCM リポジトリーに設定します。
1. このステージでビルド・ジョブを追加します。
1. ビルド・ジョブを構成します。
  ![npm ビルド・ジョブ](images/artifactory_npm_job.png)

  a. ビルダー・タイプに**「NPM ビルド (NPM Build)」**を選択します。

  b. Artifactory ツール統合の複数インスタンスを構成した場合、npm ビルド・ジョブを構成する対象にしたい Artifactory ツール統合の名前を入力します。

  c. ツール統合タイプに**「Artifactory」**を選択します。

  d. ビルド・コマンドには、npm モジュールのビルドまたはレジストリーへのモジュールのパブリッシュを行うコマンドを入力します。次の例は、モジュールのビルドまたはパブリッシュのいずれかを行うコマンドを示します。
     ```
     npm install
     # or
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **ヒント:** レジストリーへの接続に使用した URL およびユーザー資格情報は、Artifactory ツール統合の構成設定で見つけることができます。

  e. ビルド・ジョブが Artifactory レジストリーへのパブリッシュを行い、かつ、ノード・モジュール・バージョンのフォーマットが `x.y.z-SNAPSHOT.w` である場合、**「スナップショット・モジュール・バージョンのインクリメント (Increment snapshot module version)」**チェック・ボックスにチェック・マークを付けます。ビルド・ジョブは、モジュール・バージョンを自動的に更新した後で、Artifactory レジストリーにパブリッシュします。ジョブは、npm レジストリーおよびローカル `package.json` ファイルから最高バージョンのモジュールを選択し、semver を使用してモジュール・バージョンを増やします。ビルド・ジョブは、変更を SCM リポジトリーに配信しません。

1. **「保存」**をクリックします。パイプラインが実行されると、このビルド・ジョブは Artifactory ツール統合からの構成情報を使用して npm レジストリーに接続します。

### パイプラインに Artifactory Maven ビルド・ジョブを構成する
{: #config_artifactory_maven}

パイプラインに Maven ビルド・ジョブを構成する前に、ビルド SCM リポジトリーを入力として使用できる作業パイプラインが存在している必要があり、また、ツールチェーンに Artifactory を構成しておく必要もあります。Artifactory の構成手順については、[Artifactory](#artifactory) のセクションを参照してください。

{{site.data.keyword.deliverypipeline}} を構成して Maven ビルド・ジョブを追加します。

1. ステージを作成し、入力を適切な SCM リポジトリーに設定します。
1. このステージでビルド・ジョブを追加します。
1. ビルド・ジョブを構成します。
  ![Maven ビルド・ジョブ](images/artifactory_maven_job.png)

  a. ビルダー・タイプに**「Maven ビルド (Maven Build)」**を選択します。

  b. Artifactory ツール統合の複数インスタンスを構成した場合、Maven ビルド・ジョブを構成する対象にしたい Artifactory ツール統合の名前を入力します。

  c. ツール統合タイプに**「Artifactory」**を選択します。

  d. ビルド・コマンドには、Maven モジュールのビルドまたはスナップショット・レジストリーへのモジュールのパブリッシュを行うコマンドを入力します。次の例は、モジュールのビルドまたはスナップショット・レジストリーへのモジュールのパブリッシュのいずれかを行うコマンドを示します。
     ```
     mvn -B clean package
     # or
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **ヒント:** レジストリーへの接続に使用した URL およびユーザー資格情報は、Artifactory ツール統合の構成設定で見つけることができます。

1. **「保存」**をクリックします。パイプラインが実行されると、このビルド・ジョブは Artifactory ツール統合からの構成情報を使用して Maven リポジトリーに接続します。

詳しくは、「[Artifactory ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/deliver/tool_artifactory/){: new_window}」を参照してください。


## Availability Monitoring の追加
{: #availabilitymonitoring}

{{site.data.keyword.prf_hublong}} は、ユーザーに影響が及ぶ前に、問題を切り分け、パターンを識別し、パフォーマンスを改善します。世界中の場所でアプリをテストし、Delivery Pipeline に統合し、コードを継続的に最適化する方法についての洞察を深めることができます。

**注:** このツール統合は事前構成されているため、構成パラメーターは必要ありません。このツール統合を再構成することはできません。

アプリをビルドするときに、アプリの正常性をテスト、モニター、および改善するために、{{site.data.keyword.prf_hubshort}} ツール統合を追加します。

1. DevOps ダッシュボードの「ツールチェーン」ページで、{{site.data.keyword.prf_hubshort}} を追加するツールチェーンをクリックします。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「{{site.data.keyword.prf_hubshort}}」**をクリックします。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. **「{{site.data.keyword.prf_hubshort}}」**をクリックして {{site.data.keyword.prf_hubshort}} ダッシュボードを開き、アプリを選択し、そのアプリのモニタリングを構成します。

詳しくは、[{{site.data.keyword.prf_hublong}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/manage/tool_bluemix_availability_monitoring/){: new_window} を参照してください。


## Cloud Event Management (試験段階) の追加
{: #cloudeventmanagement}

{{site.data.keyword.evtmgt_full}} は、ユーザーのサービス、アプリケーション、およびインフラストラクチャーで発生する問題の統合ビューを提供します。問題をより効率的に解決できるよう、リアルタイムのインシデント管理をセットアップできます。

**注:** このツール統合は事前構成されているため、構成パラメーターは必要ありません。これを再構成することはできません。

信頼できる運用正常性、サービス品質、および継続的改善という目標を DevOps チームが達成するのを助けるために、Cloud Event Management をツールチェーンに追加します。

1. DevOps ダッシュボードから、**「ツールチェーン」**をクリックします。Cloud Event Management を追加するツールチェーンをクリックします。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「Cloud Event Management」**をクリックします。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. ツールチェーンから、以下のツール・カードのうち任意のものをクリックします。

 * Cloud Event Management を開始するには、**「Cloud Event Management」**をクリックします。

 * 問題の通知をユーザーがいつ受け取るのかを決定するポリシーを作成するには、**「{{site.data.keyword.alertnotificationshort}}」**をクリックします。

 * Cloud Event Management で運用手順書のカタログを管理するには、**「Runbook Automation」**をクリックします。

詳しくは、[Cloud Event Management ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/manage/tool_cloud_event_mgt/){: new_window} を参照してください。


## Delivery Pipeline の構成
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} は、入力を取得してジョブ (ビルド、テスト、デプロイメントなど) を実行するステージのシーケンスを通して、プロジェクトの継続的デプロイメントを自動化します。

アプリの継続的なビルド、テスト、デプロイメントを自動化するように {{site.data.keyword.deliverypipeline}}を構成します。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「{{site.data.keyword.deliverypipeline}}」**をクリックします。使用するテンプレートに応じて、使用できるフィールドは異なります。デフォルトのフィールド値を確認し、必要に応じてそれらの設定を変更します。
1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「{{site.data.keyword.deliverypipeline}}」**をクリックします。

1. 新しいパイプラインの名前を指定します。
1. パイプラインを使用してユーザー・インターフェースをデプロイするよう計画している場合は、**「アプリケーションの表示メニューでアプリケーションを表示する (Show apps in the VIEW APP  menu)」**チェック・ボックスを選択します。パイプラインが作成するすべてのアプリケーションが、ツールチェーンの「概要」ページの**「アプリケーションの表示 (View App)」**リストに表示されます。
1. **「統合の作成 (Create Integration)」**をクリックして、{{site.data.keyword.deliverypipeline}} をツールチェーンに追加します。
1. **「{{site.data.keyword.deliverypipeline}}」**をクリックして、パイプラインを表示し、構成します。パイプラインの構成の基本を確認するには、『[パイプラインのビルドとデプロイ](/docs/services/ContinuousDelivery/pipeline_build_deploy.html){: new_window}』を参照してください。

  **ヒント:** GitHub リポジトリー、{{site.data.keyword.ghe_short}} リポジトリー、または Git リポジトリーにコミットがプッシュされるとパイプラインが自動的に実行されるようにしたい場合は、以下のステップを実行します。

   a. パイプラインのステージを定義する前に、ツールチェーン用に GitHub、{{site.data.keyword.ghe_short}}、または Git Repos and Issue Tracking を構成します。パイプラインのステージには、リポジトリーの Git URL が必要です。各パイプライン・ステージは、ツールチェーンと関連付けられた、GitHub リポジトリー、{{site.data.keyword.ghe_short}} リポジトリー、または Git リポジトリーのうち 1 つのみを参照できます。GitHub の構成手順については、[GitHub](#github) のセクションを参照してください。Dedicated {{site.data.keyword.ghe_short}} の構成方法については、『[{{site.data.keyword.ghe_long}} 概説](/docs/services/ghededicated/index.html){: new_window}』を参照してください。Git Repos and Issue Tracking の構成方法については、[Git Repos and Issue Tracking](##gitbluemix) のセクションを参照してください。

   b. Web フックを使用します。Web フックを使用しない場合、パイプラインは手動でのみ実行できます。GitHub リポジトリーまたは {{site.data.keyword.ghe_short}} リポジトリーにリンクする場合に Web フックを使用するには、管理特権が必要です。Git Repos and Issue Tracking リポジトリーにリンクするには、Master または Owner 特権が必要です。

1. オプション: {{site.data.keyword.Bluemix_notm}} Public でツールチェーンを使用していて、Sauce Labs でアプリのテストを実行したい場合、{{site.data.keyword.deliverypipeline}} を構成して Sauce Labs テスト・ジョブを追加します。テスト・ジョブの構成手順については、『[パイプラインに SauceLabs テスト・ジョブを構成する](#config_saucelabs)』セクションを参照してください。

### パイプラインに Sauce Labs テスト・ジョブを構成する
{: #config_saucelabs}

パイプラインに Sauce Labs テスト・ジョブを構成する前に、アプリをビルドしてデプロイするためのステージを含む、正常に機能するパイプラインが存在していなければなりません。また、ツールチェーンに Sauce Labs を構成しておく必要もあります。Sauce Labs の構成手順については、[Sauce Labs](#saucelabs) のセクションを参照してください。

{{site.data.keyword.deliverypipeline}} を構成して Sauce Labs テスト・ジョブを追加します。

1. アプリのテスト・バージョンをデプロイするステージがない場合は作成します。
1. そのステージで、デプロイ・ジョブの後にテスト・ジョブを追加します。これらのジョブは、同じステージに置くことにより、同じ環境プロパティーのセットにアクセスできるようになります。
   
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

   **ヒント**: ツールチェーン用に Sauce Labs を構成したときに使用したユーザー名およびアクセス・キーを表示するには、**「構成」**をクリックします。

  c. **「テスト実行コマンド (Test Execution Command)」**フィールドに、テストに必要な依存関係をインストールしてテストを実行するコマンドを入力します。例えば、Node.js アプリの場合、次のようなコマンドを入力します。
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```

    d. テスト・ジョブ・ログでテストのレポートを確認する場合は、**「テスト・レポートを有効にする (Enable Test Report)」**チェック・ボックスにチェックマークを付け、「テスト結果のファイル・パターン (Test Result File Pattern)」を `test/*.xml` に設定します。

1. **「保存」**をクリックします。パイプラインが実行されるときには必ず Sauce Labs のテストが実行されます。

詳しくは、[Delivery Pipeline ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/deliver/tool_delivery_pipeline/){: new_window} を参照してください。


## DevOps Insights (ベータ版) の追加
{: #dra}

{{site.data.keyword.DRA_full}} は、単体テスト、機能テスト、およびコード・カバレッジ・ツールからの結果を収集して分析し、コードがデプロイメント・プロセスの指定されたゲートで事前定義の基準を満たすかどうかを判断します。コードが基準を満たしていない、または基準を超えていない場合、リスク回避のために、デプロイメントが停止されます。{{site.data.keyword.DRA_short}} を、継続的デリバリー環境のセーフティー・ネットとして、または品質標準の実装および改善のための手段として使用することができます。

 **注:** このツール統合は {{site.data.keyword.Bluemix_notm}} Public でのみ使用可能です。これは事前構成されているため、構成パラメーターは必要ありません。このツール統合を再構成することはできません。

{{site.data.keyword.DRA_short}} を追加し、デプロイメントをモニタリングしてリリース前にリスクを洗い出すことで、{{site.data.keyword.Bluemix_notm}} のコードの品質を維持し、向上させることができます。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「{{site.data.keyword.DRA_short}}」**をクリックします。
1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「{{site.data.keyword.DRA_short}}」**をクリックします。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. **「{{site.data.keyword.DRA_short}}」**をクリックし、開始手順 (基準の作成、パイプラインへの基準の接続、パイプラインの実行) を完了します。

詳しくは、[{{site.data.keyword.DRA_short}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/learn/tool_devops_insights/){: new_window} を参照してください。


## Eclipse Orion Web IDE の追加
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} は、ソース管理タスクを作成、編集、実行、デバッグ、完了できる Web ベースの統合環境です。編集から実行、送信、そしてデプロイまで、シームレスに行うことができます。

 **注**: このツール統合は事前構成済みです。構成パラメーターは不要で、再構成することはできません。

ソース管理タスクを完了するには、次の手順で Eclipse Orion {{site.data.keyword.webide}} ツール統合を追加します。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Eclipse Orion {{site.data.keyword.webide}}」**をクリックします。
1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合」セクションで、**「Eclipse Orion {{site.data.keyword.webide}}」**をクリックします。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. **「Eclipse Orion {{site.data.keyword.webide}}」**をクリックします。ワークスペースに GitHub または {{site.data.keyword.ghe_short}} のリポジトリーが事前に取り込まれています。現行のツールチェーンと関連付けられているリポジトリーは強調表示されます。

詳しくは、『[ Eclipse Orion {{site.data.keyword.webide}} によるコードの編集](/docs/services/ContinuousDelivery/web_ide.html){: new_window}』および [Eclipse Orion {{site.data.keyword.webide}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/code/tool_eclipse_orion_web_ide/){: new_window} を参照してください。


## Git Repos and Issue Tracking (ベータ) の構成
{: #gitbluemix}

Git Repos and Issue Tracking ツール統合は、GitLab Community Edition (Git リポジトリー用の Web ベースのホスティング・サービス) をベースにしています。リポジトリーのローカルとリモートの両方のコピーを持つことができます。詳しくは、[Git Repos and Issue Tracking ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/help){:new_window} を参照してください。

ツールチェーンの作成時に Git Repos and Issue Tracking を構成する場合は、以下のステップを実行します。    

1. 「構成可能な統合 (Configurable Integrations)」セクションで**「Git Repos and Issue Tracking」**をクリックします。
1. Git リポジトリーのデフォルト・ターゲット・ロケーションを確認します。これらのリポジトリーは、サンプル・リポジトリーのクローンです。必要に応じて、ターゲット・リポジトリーの名前を変更します。


ツールチェーンがあり、そのツールチェーンに Git Repos and Issue Tracking を追加する場合は、以下のステップを実行します。    

1. DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックしてその「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックし、**「概要」**をクリックします。
1. **「ツールの追加 (Add a Tool)」**をクリックします。
1. 「ツール統合 (Tool Integrations)」セクションで**「Git Repos and Issue Tracking」**をクリックします。
1. リポジトリー・タイプを選択します。     

  a. 空のリポジトリーを作成する場合は、リポジトリーのタイプとして**「新規 (New)」**をクリックし、リポジトリー名を入力します。    
  b. マージ要求を通して変更内容を提供できるように Git リポジトリーをフォークする場合は、リポジトリーのタイプとして**「フォーク (Fork)」**をクリックします。ソース・リポジトリーの URL を入力します。    
  c. Git リポジトリーのコピーを作成する場合は、リポジトリーのタイプとして**「クローンを作成する (Clone)」**をクリックします。新規リポジトリー名と、ソース・リポジトリーの URL を入力します。     
  d. 既存の Git リポジトリーを使用する場合は、リポジトリーのタイプとして**「既存」**をクリックします。URL を入力します。    

1. 問題のトラッキングに Issues を使用する場合は、**「Issues を使用可能にする (Enable Issues)」**チェック・ボックスにチェック・マークを付けます。
1. コミットに対するタグおよびコメントと、コミットで参照される問題に対するラベルおよびコメントを作成することによって、コード変更のデプロイメントをトラッキングしたい場合は、**「コード変更のデプロイメントを追跡する (Track deployment of code changes)」**チェック・ボックスにチェック・マークを付けます。詳しくは、[Track where your code is deployed with toolchains ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window} を参照してください。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 作業対象の Git リポジトリーのカードをクリックします。プロジェクト概要のページが開きます。    

**注:** リンクしようとしているリポジトリーに対する Master または Owner 特権をお持ちでない場合、Web フックを使用できないので統合は制限されます。リポジトリーにコミットがプッシュされたときにパイプラインが自動的に実行されるようにするには、Web フックが必要です。Web フックがない場合、パイプラインを手動で開始する必要があります。


## GitHub and Issues の構成
{: #github}

GitHub は、Git リポジトリーの Web ベースのホスティング・サービスです。リポジトリーのローカルとリモートの両方のコピーを持つことができるので、共同作業が容易になります。

GitHub Issues は、作業と計画のすべてを 1 つの場所に保持するトラッキング・ツールです。これは、ユーザーが重要タスクに注力できるようにユーザーの開発リポジトリーと統合されます。

GitHub を構成して、クラウドでソース・コードを管理します。

1. ツールチェーンの作成時にこのツール統合を構成する場合は、次の手順を実行します。

 a. 「構成可能な統合 (Configurable Integrations)」セクションで**「GitHub」**をクリックします。{{site.data.keyword.Bluemix_notm}} Public でツールチェーンを作成していて、 {{site.data.keyword.Bluemix_notm}} に GitHub へのアクセスをまだ認可していなければ、**「認可 (Authorize)」** をクリックして GitHub Web サイトに移動します。アクティブな GitHub セッションがない場合は、ログインするよう求められます。**「アプリケーションを許可 (Authorize Application)」** をクリックして、{{site.data.keyword.Bluemix_notm}} が GitHub アカウントにアクセスできるようにします。アクティブな GitHub セッションはあるものの、最近パスワードを入力していない場合は、確認のために GitHub パスワードの入力を求められることがあります。

 b. GitHub リポジトリーのデフォルトのターゲット・リポジトリーの場所を確認します。これらのリポジトリーは、サンプル・リポジトリーのクローンです。必要に応じて、ターゲット・リポジトリーの名前を変更します。
![デフォルトのターゲット・リポジトリーの場所](images/toolchain_github_config.png)

1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「GitHub」**をクリックします。

1. 既存の GitHub リポジトリーを使用する場合は、リポジトリーのタイプとして**「既存」**をクリックし、URL を入力します。
1. 新しい GitHub リポジトリーを使用する場合は、その GitHub リポジトリーに付ける名前を入力し、複製またはフォークするリポジトリーの URL を入力し、リポジトリー・タイプを次のように選択します。

 a. 空のリポジトリーを作成する場合は、**「新規」**をクリックします。

 b. GitHub リポジトリーのコピーを作成する場合は、**「クローンを作成する (Clone)」**をクリックします。

 c. GitHub リポジトリーをフォークし、プル・リクエストで変更内容を提供できるようにする場合は、**「フォーク (Fork)」**をクリックします。

1. 問題のトラッキングに GitHub Issues を使用する場合は、**「GitHub Issues を使用可能にする (Enable GitHub Issues)」**チェック・ボックスにチェック・マークを付けます。
1. コミットに対するタグおよびコメントと、コミットで参照される問題に対するラベルおよびコメントを作成することによって、コード変更のデプロイメントをトラッキングしたい場合は、**「コード変更のデプロイメントを追跡する (Track deployment of code changes)」**チェック・ボックスにチェック・マークを付けます。詳しくは、[Track where your code is deployed with toolchains ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window} を参照してください。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 作業対象の GitHub リポジトリーのカードをクリックします。GitHub の Web サイトが開きます。そこでリポジトリーの内容を表示できます。

  **ヒント**: Eclipse Orion {{site.data.keyword.webide}} の統合ソース・コード管理ツールを使用して、GitHub リポジトリーを編集し、ワークスペースからアプリをデプロイすることができます。

1. GitHub Issues を使用可能にした場合、**「GitHub Issues」**をクリックして開きます。ツールチェーンに複数の GitHub リポジトリーが含まれれている場合でも、GitHub Issues のこのインスタンスをツールチェーン全体に使用できます。    

**注:** リンクしようとしているリポジトリーに対する管理特権をお持ちでない場合、Web フックを使用できないので統合は制限されます。リポジトリーにコミットがプッシュされたときにパイプラインが自動的に実行されるようにするには、Web フックが必要です。Web フックがない場合、パイプラインを手動で開始する必要があります。

詳しくは、[GitHub ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} および [GitHub Issues ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window} を参照してください。


## Bluemix Dedicated での GitHub Enterprise および GitHub Issues の構成
{: #configghe}

 **注:** ここで説明する手順は、{{site.data.keyword.Bluemix_notm}} Dedicated for {{site.data.keyword.ghe_short}} に適用されます。独自の管理版の {{site.data.keyword.ghe_short}} を使用している場合、内部手順によっては一部のステップが異なることがあります。

{{site.data.keyword.ghe_long}} は、オンプレミス型の Web ベースの Git リポジトリー・ホスティング・サービスです。Dedicated {{site.data.keyword.ghe_short}} は {{site.data.keyword.Bluemix_notm}} Dedicated ユーザー専用です。GitHub Issues は、作業と計画を 1 つの場所に保持するトラッキング・ツールです。これは、ユーザーが重要タスクに注力できるようにユーザーの開発リポジトリーと統合されます。Dedicated {{site.data.keyword.ghe_short}} と GitHub Issues の詳細については、「[{{site.data.keyword.ghe_long}}の概説](/docs/services/ghededicated/index.html){: new_window}」と「[GitHub Issues![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}」を参照してください。

{{site.data.keyword.ghe_short}}  をツールチェーン内の 1 つのツール統合として構成して、会社の [{{site.data.keyword.Bluemix_notm}} Dedicated](/docs/dedicated/index.html#dedicated){: new_window} インスタンス内でソース・コードを管理できるようにすることができます。

1. ツールチェーンの作成時にこのツール統合を構成する場合は、次の手順を実行します。

 a. Dedicated {{site.data.keyword.ghe_short}} に初めてログインするときは、まずその前に LDAP を使用して会社のユーザー・レジストリーから自分のユーザー ID を {{site.data.keyword.Bluemix_notm}} Dedicated インスタンスに追加するよう、会社の地域管理者に依頼してください。{{site.data.keyword.ghe_short}} アカウントの設定の詳細については、「[{{site.data.keyword.ghe_long}}の概説](/docs/services/ghededicated/index.html){: new_window}」を参照してください。

 b. 「構成可能な統合 (Configurable Integrations)」セクションで**「{{site.data.keyword.ghe_short}}」**をクリックします。    

 c. 新しい {{site.data.keyword.ghe_short}} リポジトリーのデフォルト名を確認します。必要に応じて、新しいリポジトリーの名前を変更してください。次のイメージは、サンプル・リポジトリーのクローンとして作成されたリポジトリーの例を示しています。既存のリポジトリーを使用することも、新しいリポジトリーを使用することもできます。新しいリポジトリーを使用する場合は、空のリポジトリーを作成するか、リポジトリーのクローンを作成するか、リポジトリーをフォークすることができます。
![デフォルトのリポジトリーの場所](images/toolchain_ghe_config.png)

1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「{{site.data.keyword.ghe_short}}」**をクリックします。

1. 既存の {{site.data.keyword.ghe_short}} リポジトリーを使用する場合は、そのリポジトリーの URL を入力します。リポジトリー・タイプには、**「既存」**をクリックします。
1. 新しい {{site.data.keyword.ghe_short}} リポジトリーを使用する場合は、そのリポジトリーに付ける名前を入力し、複製またはフォークするリポジトリーの URL を入力し、リポジトリー・タイプを次のように選択します。

 a. 空のリポジトリーを作成する場合は、**「新規」**をクリックします。

 b. リポジトリーのコピーを作成する場合は、**「クローンを作成する (Clone)」**をクリックします。

 c. リポジトリーをフォークし、プル・リクエストで変更内容を提供できるようにする場合は、**「フォーク (Fork)」**をクリックします。

1. 問題のトラッキングに GitHub Issues を使用する場合は、**「GitHub Issues を使用可能にする (Enable GitHub Issues)」**チェック・ボックスにチェック・マークを付けます。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 作業対象の {{site.data.keyword.ghe_short}} リポジトリーのカードをクリックします。会社の {{site.data.keyword.ghe_short}} リポジトリーが開きます。

  **ヒント**: Eclipse Orion {{site.data.keyword.webide}} の統合ソース・コード管理ツールを使用して、{{site.data.keyword.ghe_short}} リポジトリーを編集し、ワークスペースからアプリをデプロイすることができます。

1. GitHub Issues を使用可能にした場合、**「GitHub Issues」**をクリックします。ツールチェーンに複数の GitHub リポジトリーが含まれれている場合でも、GitHub Issues のこのインスタンスをツールチェーン全体に使用できます。    

**注:** リンクしようとしているリポジトリーに対する管理特権をお持ちでない場合、Web フックを使用できないので統合は制限されます。リポジトリーにコミットがプッシュされたときにパイプラインが自動的に実行されるようにするには、Web フックが必要です。Web フックがない場合、パイプラインを手動で開始する必要があります。


## Jenkins の構成
{: #jenkins}

Jenkins は、ソフトウェアを継続的にビルドおよびテストする、サーバー・ベースのオープン・ソースのツールであり、継続的統合および継続的デリバリーの履行をサポートします。

**重要**: Jenkins ツール統合を作成する前に、Jenkins サーバーを用意する必要があります。

Jenkins ツール統合を使用すれば、Jenkins ジョブ通知をツールチェーン内の他のツール (Slack や PagerDuty など) に送信できます。デプロイメントでコードをトレースするために、デプロイメント・メッセージを Git コミットや関連 Git/JIRA 問題に追加できます。また、デプロイメントを「ツールチェーン接続」ページに表示することもできます。テスト結果を {{site.data.keyword.DRA_short}} に送信し、自動化された品質ゲートを追加し、デプロイメント・リスクをトラッキングすることができます。

アプリの継続的なビルド、テスト、デプロイメントを自動化するために Jenkins を構成します。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Jenkins」**をクリックします。
1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。  

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「Jenkins」**をクリックします。

1. ツールチェーン内の Jenkins カードでこのツール統合に対して表示したい名前を入力します。
1. ツールチェーンから Jenkins カードをクリックしたときに開くようにしたい Jenkins サーバーの URL を入力します。
1. 生成されたツールチェーン Web フックをコピーします。
1. Jenkins サーバーで、以下のステップを実行します。

 a. [Cloud Foundry CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} をインストールします。

 b. 以下のいずれかのコマンドを入力することによって、IBM Cloud DevOps Cloud Foundry プラグインをインストールします。

  * Mac OS: `cf install-plugin https://icd.ng.bluemix.net/icd_darwin_amd64`

  * Linux または Docker: `cf install-plugin https://icd.ng.bluemix.net/icd_linux_amd64`

 c. DevOps Insights および Notifications 用の IBM Cloud DevOps Jenkins プラグインをインストールおよび構成します。詳しくは、[プラグインのインストールおよび構成](/docs/services/DevOpsInsights/insights_risk.html#integrate_jenkins){: new_window}を参照してください。

 d. ツールチェーンに通知を送信するようにしたいジョブごとに、以下のステップを実行します。

  * **「このプロジェクトはパラメーター化される (This project is parameterized)」**チェック・ボックスにチェック・マークを付けます。

  * `ICD_WEBHOOK_URL` ストリング・パラメーターを追加します。

  * 生成されたツールチェーン Web フックを貼り付けます。
 ![Web フック URL](images/jenkins_webhook_url.png)

  * IBM Cloud DevOps - Webhook Notification のビルド後アクションを追加し、**「ジョブ完了 (Job Completed)」**チェック・ボックスにチェック・マークを付けます。
 ![ビルド後アクション](images/jenkins_postbuild_action.png)  

 e. デプロイ・ジョブで、以下のステップを実行します。

  * `ICD_WEBHOOK_URL`、`CF_API`、`CF_ORG`、`CF_SPACE`、および `CF_APP` ストリング・パラメーターを追加します。以下の例は、各ストリング・パラメーターの追加方法を示します。
 ![Webhook URL ストリング・パラメーター](images/jenkins_set_webhook_url.png)
 ![CFI API ストリング・パラメーター](images/jenkins_set_cfapi.png)
 ![CFI ORG ストリング・パラメーター](images/jenkins_set_cforg.png)
 ![CFI SPACE ストリング・パラメーター](images/jenkins_set_cfspace.png)
 ![CFI APP ストリング・パラメーター](images/jenkins_set_cfapp.png)

  * `CF_CREDS_USR` ユーザー名変数および `CF_CREDS_PSW` パスワード変数を使用して、Cloud Foundry CLI のバインディングを構成します。
 ![Cloud Foundry CLI バインディング](images/jenkins_config_bindings.png)  

  * **「ビルド (Build)」**フィールドに以下のコマンドを入力してログインし、IBM Cloud DevOps Cloud Foundry プラグインを使用してアプリケーション・デプロイ可能マッピングを、Git コミット追跡可能性を有効にしてツールチェーンに送信します。
 ![ビルド・コマンド](images/jenkins_build_commands.png)    

  * **「ビルド (Build)」**フィールドに `cf icd --create-connection $ICD_WEBHOOK_URL $CF_APP` コマンドを入力して、アプリケーション・デプロイ可能マッピングをツールチェーンに送信します。    

 f. 変更を保存し、Jenkins ツール統合の「統合の構成 (Configure the Integration)」ページに戻ります。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. ツールチェーンから、**「Jenkins」**をクリックして Jenkins サーバーを表示します。  

詳しくは、[Jenkins ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/deliver/tool_jenkins/){: new_window} を参照してください。


## JIRA の構成
{: #jira}

JIRA は、ユーザーのソフトウェアに関連する問題およびバグを追跡するツールです。Jenkins または {{site.data.keyword.deliverypipeline}} によってデプロイメントが実行されるたびに、JIRA ツール統合はプロジェクトの問題を更新します。JIRA ツール統合で問題をトラッキングするには、コミット・メッセージ内で JIRA Smart Commits を使用する必要があります。JIRA Smart Commits について詳しくは、[Using Smart Commits ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://confluence.atlassian.com/fisheye/using-smart-commits-298976812.html){: new_window} を参照してください。

品質コードの計画、追跡、および配信のために、JIRA を構成します。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「JIRA」**をクリックします。
1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。  

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「JIRA」**をクリックします。

1. JIRA プロジェクトがあり、それに接続したい場合、JIRA タイプとして**「既存」**をクリックします。

 a. JIRA プロジェクトの JIRA プロジェクト・キーを入力します。プロジェクト・キーは JIRA プロジェクトの URL に含まれています。

 b. JIRA インスタンスのベース API URL を入力します。API URL は、JIRA インスタンスのヘッダーで見つけることができます。**「管理」**アイコンをクリックし、**「システム」**をクリックします。

 c. オプション: JIRA ユーザー名を入力します。ユーザー名が必要となるのは、プライベート JIRA インスタンスに接続する場合、または、パブリック・インスタンスに接続し、かつ、トレーサビリティー情報を受け取りたい場合に限ります。

 d. オプション: JIRA パスワードを入力します。パスワードが必要となるのは、プライベート JIRA インスタンスに接続する場合、または、パブリック・インスタンスに接続し、かつ、トレーサビリティー情報を受け取りたい場合に限ります。

 e. 参照される問題に対するラベルおよびコメントを作成することによってプロジェクトに関するコード変更のデプロイメントをトラッキングするには、**「コード変更のデプロイメントを追跡する (Track deployment of code changes)」**チェック・ボックスにチェック・マークを付けます。JIRA Smart Commit を使用して、GitHub コミットの JIRA 問題を参照するようにしてください。このオプションが選択されていない場合、JIRA ツール統合はすべてのコミットを無視します。

1. JIRA プロジェクトを作成する場合、JIRA タイプとして**「新規 (New)」**を選択します。

 a. 新規プロジェクトに使用する JIRA プロジェクト・キーを入力します。このキーは、プロジェクト URL 内で固有 ID として使用されます。

 b. JIRA プロジェクトの名前を入力します。

 c. JIRA インスタンスのベース API URL を入力します。API URL は、JIRA インスタンスのヘッダーで見つけることができます。**「管理」**アイコンをクリックし、**「システム」**をクリックします。

 d. このプロジェクトに使用したい JIRA プロジェクト・リーダーのユーザー名を入力します。JIRA プロジェクト・リーダーとして指定される個人は、JIRA でプロジェクト・リーダー許可を持っている必要があります。

 e. JIRA のこのインスタンスの管理者のユーザー名を入力します。

 f. JIRA のこのインスタンスの管理者のパスワードを入力します。

 g. 参照される問題に対するラベルおよびコメントを作成することによってプロジェクトに関するコード変更のデプロイメントをトラッキングするには、**「コード変更のデプロイメントを追跡する (Track deployment of code changes)」**チェック・ボックスにチェック・マークを付けます。JIRA Smart Commit を使用して、GitHub コミットの JIRA 問題を参照するようにしてください。このオプションが選択されていない場合、JIRA ツール統合はすべてのコミットを無視します。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. ツールチェーンから**「JIRA」**をクリックして、接続する JIRA プロジェクトのダッシュボードを表示します。

詳しくは、[JIRA ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/code/tool_jira/){: new_window} を参照してください。


## Nexus の構成
{: #nexus}

ビルド成果物を Nexus リポジトリーに保管するように Nexus リポジトリー・マネージャーを構成します。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Nexus」**をクリックします。
1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。  

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「Nexus」**をクリックします。

1. Nexus ツール統合のこのインスタンスの名前を入力します。
1. ツールチェーンから Nexus カードをクリックしたときに開くようにしたい Nexus リポジトリーの URL を入力します。
1. 接続先にするリポジトリーのタイプを選択します。
1. **「npm レジストリー」**を選択した場合は、以下のステップを実行します。

 a. レジストリーと関連付けられた E メール・アドレスを入力します。

 b. レジストリーと関連付けられた認証トークンを入力します。

 c. Nexus サーバー上のプライベート・レジストリーである Nexus リリース・リポジトリーの URL を入力します。

 d. 複数のパブリックおよびプライベート npm レジストリーを結合するために使用する Mirror または Public レジストリーの URL を入力します。例えば、この URL は、プライベート・レジストリーと、npm グローバル・レジストリーのキャッシュの両方にアクセスできる、Nexus サーバー上の仮想レジストリーの URL であることができます。

1. **「Maven リポジトリー」**を選択した場合は、以下のステップを実行します。

 a. リポジトリーと関連付けられたユーザー ID を入力します。

 b. リポジトリーと関連付けられたパスワードを入力します。

 c. Nexus サーバー上のプライベート・リリース・リポジトリーである Nexus リリース・リポジトリーの URL を入力します。

 d. Nexus サーバー上のプライベート・スナップショット・リポジトリーである Nexus スナップショット・リポジトリーの URL を入力します。

 e. 複数のパブリックおよびプライベート Maven リポジトリーを結合するために使用する Mirror または Public リポジトリーの URL を入力します。例えば、この URL は、プライベート・リポジトリーと、Maven 中央リポジトリーのキャッシュの両方にアクセスできる、Nexus サーバー上の仮想リポジトリーの URL であることができます。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. 作業対象の Nexus リポジトリーのカードをツールチェーンからクリックします。Nexus の Web サイトが開きます。そこでリポジトリーの内容を表示できます。
1. オプション: {{site.data.keyword.Bluemix_notm}} Public でツールチェーンを使用していて、Nexus を npm と共に使用してアプリをビルドしたい場合、パイプラインを構成して npm ビルド・ジョブを追加します。ビルド・ジョブの構成手順については、『[パイプラインに Nexus npm ビルド・ジョブを構成する](#config_nexus_npm)』セクションを参照してください。
1. オプション: {{site.data.keyword.Bluemix_notm}} Public でツールチェーンを使用していて、Nexus を Maven と共に使用してアプリをビルドしたい場合、パイプラインを構成して Maven ビルド・ジョブを追加します。ビルド・ジョブの構成手順については、『[パイプラインに Nexus Maven ビルド・ジョブを構成する](#config_nexus_maven)』セクションを参照してください。

### パイプラインに Nexus npm ビルド・ジョブを構成する
{: #config_nexus_npm}

パイプラインに npm ビルド・ジョブを構成する前に、ビルド SCM リポジトリーを入力として使用できる作業パイプラインが存在している必要があり、また、ツールチェーンに Nexus を構成しておく必要もあります。Nexus の構成手順については、[Nexus](#nexus) のセクションを参照してください。

{{site.data.keyword.deliverypipeline}} を構成して npm ビルド・ジョブを追加します。

1. ステージを作成し、入力を適切な SCM リポジトリーに設定します。
1. このステージでビルド・ジョブを追加します。
1. ビルド・ジョブを構成します。
  ![npm ビルド・ジョブ](images/nexus_npm_job.png)

  a. ビルダー・タイプに**「NPM ビルド (NPM Build)」**を選択します。

  b. Nexus ツール統合の複数インスタンスを構成した場合、npm ビルド・ジョブを構成する対象にしたい Nexus ツール統合の名前を入力します。

  c. ツール統合タイプに**「Nexus」**を選択します。

  d. ビルド・コマンドには、npm モジュールのビルドまたはレジストリーへのモジュールのパブリッシュを行うコマンドを入力します。次の例は、モジュールのビルドまたはパブリッシュのいずれかを行うコマンドを示します。
     ```
     npm install
     # or
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **ヒント:** レジストリーへの接続に使用した URL およびユーザー資格情報は、Nexus ツール統合の構成設定で見つけることができます。
  e. ビルド・ジョブが Nexus レジストリーへのパブリッシュを行い、かつ、ノード・モジュール・バージョンのフォーマットが `x.y.z-SNAPSHOT.w` である場合、**「スナップショット・モジュール・バージョンのインクリメント (Increment snapshot module version)」**チェック・ボックスにチェック・マークを付けます。ビルド・ジョブは、モジュール・バージョンを自動的に更新した後で、Nexus レジストリーにパブリッシュします。ビルド・ジョブは、npm レジストリーおよびローカル `package.json` ファイルから最高バージョンのモジュールを選択し、semver を使用してモジュール・バージョンを増やします。ビルド・ジョブは、変更を SCM リポジトリーに配信しません。

1. **「保存」**をクリックします。パイプラインが実行されると、このビルド・ジョブは Nexus ツール統合からの構成情報を使用して npm レジストリーに接続します。

### パイプラインに Nexus Maven ビルド・ジョブを構成する
{: #config_nexus_maven}

パイプラインに Maven ビルド・ジョブを構成する前に、ビルド SCM リポジトリーを入力として使用できる作業パイプラインが存在している必要があり、また、ツールチェーンに Nexus を構成しておく必要もあります。Nexus の構成手順については、[Nexus](#nexus) のセクションを参照してください。

{{site.data.keyword.deliverypipeline}} を構成して Maven ビルド・ジョブを追加します。

1. ステージを作成し、入力を適切な SCM リポジトリーに設定します。
1. このステージでビルド・ジョブを追加します。
1. ビルド・ジョブを構成します。
  ![Maven ビルド・ジョブ](images/nexus_maven_job.png)

  a. ビルダー・タイプに**「Maven ビルド (Maven Build)」**を選択します。

  b. Nexus ツール統合の複数インスタンスを構成した場合、Maven ビルド・ジョブを構成する対象にしたい Nexus ツール統合の名前を入力します。

  c. ツール統合タイプに**「Nexus」**を選択します。

  d. ビルド・コマンドには、Maven モジュールのビルドまたはスナップショット・レジストリーへのモジュールのパブリッシュを行うコマンドを入力します。次の例は、モジュールのビルドまたはパブリッシュのいずれかを行うコマンドを示します。
     ```
     mvn -B clean package
     # or
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **ヒント:** レジストリーへの接続に使用した URL およびユーザー資格情報は、Nexus ツール統合の構成設定で見つけることができます。
1. **「保存」**をクリックします。パイプラインが実行されると、このビルド・ジョブは Nexus ツール統合からの構成情報を使用して Maven リポジトリーに接続します。

詳しくは、[Nexus ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/deliver/tool_nexus/){: new_window} を参照してください。


## カスタム・ツール (その他のツール) の構成
{: #othertool}

チームがツールチェーン統合リストに含まれていないツールを使用する場合、カスタム・ツールを統合できます。

カスタム・ツールを構成して、ツールチェーン内の他のツールとともに機能し、チームで使用できるようにします。

1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで、**「その他のツール (Other Tool)」**をクリックします。

1. ツール名を入力します。

1. ツールに最も密接に関連したライフサイクル・フェーズを選択します。この選択によって、「概要」ページでツールがリストされるカテゴリーが決まります。
1. アイコン URL を追加します。このアイコンがツール統合のカードに表示されます。
1. 資料 URL を追加します。
1. ツール・インスタンス名を指定します。例: My Team Tool。
1. ツール・インスタンスの URL を追加します。ツール統合のカードがクリックされると、この URL が開きます。
1. ツールの説明を追加します。
1. (上級) 必要に応じて、さらにプロパティーを追加します。例えば、ご使用のツールをツールチェーンの他のツールと統合するために必要な情報または属性をリストします。  
1. **「統合の作成 (Create Integration)」**をクリックします。

詳しくは、[Introducing custom tool integration for {{site.data.keyword.Bluemix_notm}} toolchains ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2016/10/custom-tool-integration-with-bluemix-toolchains/){: new_window} を参照してください。


## PagerDuty の構成
{: #pagerduty}

PagerDuty は、複数のモニタリング・システムのデータを単一のビューに統合します。問題が発生すると、PagerDuty によって、その時点で問題の修正に最適なチーム・メンバーに確実に通知が送信されます。チーム・メンバーが問題に応答しない場合、次の技術者または運用管理者に問題を転送するようにエスカレーションを構成できます。

パイプライン・ステージで障害が発生したときに通知を送信するように PagerDuty を構成して、問題を迅速に修正してダウン時間を削減できるようにします。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「PagerDuty」**をクリックします。
1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「PagerDuty」**をクリックします。

1. PagerDuty アカウントの API アクセス・キーを入力します。PagerDuty アカウントをお持ちでない場合は、[登録して取得 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://signup.pagerduty.com/accounts/new){: new_window} してください。キーを確認する方法については、[Generating an API Key ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://support.pagerduty.com/hc/en-us/articles/202829310-Generating-an-API-Key){: new_window} を参照してください。
1. PagerDuty サービスの名前を入力します。
1. PagerDuty の 1 次連絡先の E メール・アドレスを入力します。
1. PagerDuty の 1 次連絡先の電話番号を入力します。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. **「PagerDuty」**をクリックして pagerduty.com にアクセスします。ツールチェーンに対してこのツール統合を構成したときに指定した PagerDuty サービスに関連付けられているイベントを表示できます。

詳しくは、「[PagerDuty ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}」を参照してください。


## Sauce Labs の構成
{: #saucelabs}

Sauce Labs は、機能単体テストを実行します。{{site.data.keyword.deliverypipeline}} 内のテスト・ジョブとして Sauce Labs テスト・スイートが構成されている場合、そのテスト・スイートは、継続的デリバリー・プロセスの一環として、Web アプリまたはモバイル・アプリに対するテストを実行できます。これらのテストは、誤ったコードがデプロイされるのを防ぐためのゲートとして機能することで、プロジェクトに対して非常に有益なフロー制御を提供します。

 **注:** このツール統合は {{site.data.keyword.Bluemix_notm}} Public でのみ使用可能です。

複数のオペレーティング・システムおよびブラウザーで自動化された機能テストを実行するように Sauce Labs を構成することによって、ユーザーがどのように Web サイトやアプリケーションを使用するのかをエミュレートできます。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Sauce Labs」**をクリックします。
1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「Sauce Labs」**をクリックします。

1. Sauce Labs アカウントと関連付けられたユーザー名を入力します。[ Sauce Labs アカウント・ページの上部にあるウェルカム・メッセージでユーザー名を確認できます ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://saucelabs.com/account){: new_window}。
1. Sauce Labs アカウントのアクセス・キーを入力します。[Sauce Labs アカウント・ページでキーを確認できます ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://saucelabs.com/account){: new_window}。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. **「Sauce Labs」**をクリックして saucelabs.com に移動し、ツールチェーンのテスト・アクティビティーを表示します。

 **ヒント**: Sauce Labs テスト・ジョブを {{site.data.keyword.deliverypipeline}} に追加した場合、サービス・インスタンスを選択できます。

詳しくは、「[Sauce Labs ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/deliver/tool_sauce_labs/){: new_window}」を参照してください。


## Slack の構成
{: #slack}

**重要**: パブリック Slack チャネルに送信される通知は、チームの全員が見ることができます。投稿したコンテンツの責任は投稿者が負うことに注意してください。

Slack は、クラウド・ベースのリアルタイムでのメッセージングおよび通知のシステムです。Slack が提供する永続的なチャットは、E メールの代わりに使用できる対話性に優れたチームのコラボレーション手段になります。
専用チャネルまたは作業に直接関連する一連のチャネルで、チームと連絡を取ることができます。さらに、2 人以上のメンバー間で、チャネルやダイレクト・メッセージを使用して、ファイルとイメージを共有することもできます。ダイレクト・メッセージとチャネルでの通信は、検索できるように保存されます。

テストやデプロイのアクティビティーなどのツールチェーンに関する通知をツール統合から受信するように Slack を構成します。

1. ツールチェーン作成時にこのツール統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Slack」**をクリックします。
1. 既存のツールチェーンにこのツール統合を追加する場合は、DevOps ダッシュボードの**「ツールチェーン」**ページでそのツールチェーンをクリックして「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「Slack」**をクリックします。

1. 着信 Web フックとして Slack によって生成された Slack Web フック URL を入力します。Slack チャネルがツール統合からツールチェーンに関する通知を受け取るためには Slack Web フック URL が必要です。Web フックを作成または確認する方法については、[Incoming Webhooks ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://api.slack.com/incoming-webhooks){: new_window} を参照してください。

 **ヒント:** Slack チャネルがツール統合からツールチェーンについての通知を受け取れるようにするために API キーを使用している場合は、代わりに Web フックを使用するように構成を更新する必要があります。

1. 通知を送信する Slack チャネルの名前を入力します。このチャネルは存在していなければならず、Slack チームでアクティブである必要があります。
1. Slack チームの URL ホスト名を入力します。これは、チーム URL 内の `.slack.com` の前にある語または句です。例えば、チーム URL が `https://team.slack.com` の場合、ホスト名は `team` です。
1. **「統合の作成 (Create Integration)」**をクリックします。

 **ヒント:** 指定した Slack チャネルおよびチームに到達できない場合、Slack カードに `Setup Failed` エラーが表示されます。`Setup Failed` メッセージの上に移動し、**「再構成 (Reconfigure)」**をクリックしてください。Slack Web フック URL、Slack チャネル、および Slack チームの URL ホスト名に、有効な構成パラメーターを使用していることを確認してください。必要に応じて設定を更新し、**「統合の保存」**をクリックします。

1. **「Slack」**をクリックします。構成した Slack チャネルでツールチェーンのアクティビティーをすべて表示できます。

詳しくは、[Slack ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window} を参照してください。


## SonarQube の構成
{: #sonarqube}

SonarQube は、ソース・コードの全体的な正常性と品質の概要を提供し、新しいコード内で見つかった問題を強調表示します。コード・アナライザーは、20 を超えるコーディング言語において、NULL ポインター間接参照などの注意を要するバグ、論理エラー、リソース・リークを検出します。

以下のようにして、ソース・コードの品質を継続的に分析および測定するように SonarQube を構成します。

1. DevOps ダッシュボードから、**「ツールチェーン」**をクリックします。SonarQube を追加するツールチェーンをクリックします。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。  

 a. **「ツールの追加 (Add a Tool)」**をクリックします。

 b. 「ツール統合 (Tool Integrations)」セクションで**「SonarQube」**をクリックします。

1. SonarQube ツール統合のこのインスタンスの名前を入力します。
1. ツールチェーンから SonarQube カードをクリックしたときに開くようにしたい SonarQube インスタンスの URL を入力します。
1. オプション: SonarQube サーバーへの接続に使用するユーザー名を入力します。

 **ヒント:** ユーザー名の指定が必要なのは、SonarQube サーバーへの接続にパスワードを使用する場合のみです。接続に認証トークンを使用する場合は、このフィールドを空のままにしてください。

1. SonarQube サーバーへの接続に使用するパスワードまたは認証トークンを入力します。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. ツールチェーンから**「SonarQube」**をクリックして、接続する SonarQube インスタンスのダッシュボードを表示します。

詳しくは、[SonarQube ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/learn/tool_sonarqube/){: new_window} を参照してください。
