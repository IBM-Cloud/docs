---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-26"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}    

# ツル統合の構成
{: #integrations}

開発、デプロイメント、および運用の作業をサポトするツル統合をオプン・ツルチェンの作成時に構成するか、ツル統合を追加および構成して既存のツルチェンをカスタマイズすることができます。  
{:shortdesc}

ツルチェンで追加および構成できるツル統合は、{{site.data.keyword.Bluemix_notm}} Public または {{site.data.keyword.Bluemix_notm}} Dedicated のどちらを使用しているかによって異なります。{{site.data.keyword.Bluemix_notm}} Dedicated でツルチェンを使用している場合、利用できるツル統合は、特定の環境で {{site.data.keyword.contdelivery_full}} がどのように設定されたかに応じて異なります。

|ツル統合 |{{site.data.keyword.Bluemix_notm}} Public で利用可能	|{{site.data.keyword.Bluemix_notm}} Dedicated で利用可能 (環境依存)|
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
|その他のツル			|はい		|はい		|
|PagerDuty			|はい		|はい		|
|Sauce Labs		|はい		|いいえ		|
|Slack			|はい		|はい		|
|SonarQube			|はい		|いいえ		|
{: caption="表 1. Bluemix Public および Dedicated でツルチェンに使用可能なツル統合" caption-side="top"}

**ヒント:** {{site.data.keyword.Bluemix_notm}} Public でソス・コドでの開発を開始する場合は、{{site.data.keyword.deliverypipeline}} を構成する前に GitHub ツル統合または Git Repos and Issue Tracking ツル統合を構成してください。{{site.data.keyword.Bluemix_notm}} Dedicated でコドでの開発を開始する場合は、{{site.data.keyword.deliverypipeline}} を構成する前に {{site.data.keyword.ghe_short}} ツル統合を構成します。


## Alert Notification (試験段階) の構成
{: #alertnotification}

{{site.data.keyword.alertnotificationfull}} は、通知戦略を中央化および簡素化するために使用できる、ハイブリッド・クラウド・ベスのソリュションです。他のクラウド・ベスのアプリケションおよびオンプレミス・アプリケションと連携して機能します。アラトはセキュアな RESTful API を使用して {{site.data.keyword.alertnotificationshort}} に転送されます。

DevOps 処理中の問題に関する通知を受け取るように {{site.data.keyword.alertnotificationshort}} を構成します。

### 前提条件

1. {{site.data.keyword.alertnotificationshort}} アカウントをお持ちでない場合、登録して取得します。

 a. IBM マケットプレイスで [IBM {{site.data.keyword.alertnotificationshort}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/us-en/marketplace/alert-notification){: new_window} ペジを開きます。

 b. サブスクリプションを購入するか、90 日間の無料評価版に申し込みます。

1. {{site.data.keyword.alertnotificationshort}} アカウントのセットアップが終わったら、[My IBM ダッシュボド ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://myibm.ibm.com/dashboard/){: new_window} を開きます。
1. IBM {{site.data.keyword.alertnotificationshort}} の横の**「起動」**をクリックします。
1. **「API キの管理 (Manage API Keys)」**をクリックし、**「API キの作成 (Create API Key)」**をクリックします。
1. **「API キの作成 (Create API Key)」**フィルドに説明を入力します。
1. **「生成 (Generate)」**をクリックします。名前およびパスワドなどの新規 API キ情報が表示されます。この情報はツル統合の構成に必要であるため、「新規 API キ (New API Key)」ウィンドウを開いたままにしておいてください。セキュリティのため、後で API キのパスワドを取り出すことはできません。

### Alert Notification の構成

1. ツルチェン作成時にこのツル統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「{{site.data.keyword.alertnotificationshort}}」**をクリックします。
1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックします。次に、**「概要」**をクリックします。  

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「{{site.data.keyword.alertnotificationshort}}」**をクリックします。

1. 使用したい {{site.data.keyword.alertnotificationshort}} API の URL を入力します。URL は {{site.data.keyword.alertnotificationshort}} サビスの「API キの管理 (Manage API Keys)」ペジで見つけることができます (例: `https://ibmnotifybm.mybluemix.net/api/alerts/v1`)。
1. {{site.data.keyword.alertnotificationshort}} の API アクセス・キを入力します。API キ名は「新規 API キ (New API Key)」ウィンドウで確認できます。
1. API キに対して {{site.data.keyword.alertnotificationshort}} が生成したパスワドを入力します。API キのパスワドは「新規 API キ (New API Key)」ウィンドウで確認できます。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. ツルチェンから、**「{{site.data.keyword.alertnotificationshort}}」**をクリックします。

詳しくは、[IBM {{site.data.keyword.alertnotificationshort}}![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/manage/tool_alert_notification/){: new_window}を参照してください。


## Artifactory の構成
{: #artifactory}

ビルド成果物を Artifactory リポジトリに保管するように Artifactory リポジトリ・マネジャを構成します。

1. ツルチェン作成時にこのツル統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Artifactory」**をクリックします。
1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックします。次に、**「概要」**をクリックします。  

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「Artifactory」**をクリックします。

1. Artifactory カドをクリックしたときに開くようにしたい Artifactory リポジトリの URL を入力します。
1. 接続先にするリポジトリのタイプを選択します。
1. Artifactory npm レジストリを使用する場合は、以下のステップを実行します。

 a. レジストリと関連付けられた E メル・アドレスを入力します。

 b. レジストリと関連付けられた認証トクンを入力します。

 c. Artifactory サバ上のプライベト・レジストリである Artifactory リリス・リポジトリの URL を入力します。

 d. 複数のパブリックおよびプライベト npm レジストリを結合するために使用する Mirror または Public レジストリの URL を入力します。例えば、この URL は、プライベト・レジストリと、npm グロバル・レジストリのキャッシュの両方にアクセスできる、Artifactory サバ上の仮想レジストリの URL であることができます。

1. Artifactory Maven リポジトリを使用する場合は、以下のステップを実行します。

 a. リポジトリと関連付けられたユザ ID を入力します。

 b. リポジトリと関連付けられたパスワドを入力します。

 c. Artifactory サバ上のプライベト・リリス・リポジトリである Artifactory リリス・リポジトリの URL を入力します。

 d. Artifactory サバ上のプライベト・スナップショット・リポジトリである Artifactory スナップショット・リポジトリの URL を入力します。

 e. 複数のパブリックおよびプライベト Maven リポジトリを結合するために使用する Mirror または Public リポジトリの URL を入力します。例えば、この URL は、プライベト・リポジトリと、Maven 中央リポジトリのキャッシュの両方にアクセスできる、Artifactory サバ上の仮想リポジトリの URL であることができます。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. 作業対象の Artifactory リポジトリのカドをクリックします。Artifactory の Web サイトが開きます。そこでリポジトリの内容を表示できます。
1. オプション: {{site.data.keyword.Bluemix_notm}} Public でツルチェンを使用していて、Artifactory を npm と共に使用してアプリをビルドしたい場合、パイプラインを構成して npm ビルド・ジョブを追加します。ビルド・ジョブの構成手順については、『[パイプラインに Artifactory npm ビルド・ジョブを構成する](#config_artifactory_npm)』セクションを参照してください。
1. オプション: {{site.data.keyword.Bluemix_notm}} Public でツルチェンを使用していて、Artifactory を Maven と共に使用してアプリをビルドしたい場合、パイプラインを構成して Maven ビルド・ジョブを追加します。ビルド・ジョブの構成手順については、『[パイプラインに Artifactory Maven ビルド・ジョブを構成する](#config_artifactory_maven)』セクションを参照してください。

### パイプラインに Artifactory npm ビルド・ジョブを構成する
{: #config_artifactory_npm}

パイプラインに npm ビルド・ジョブを構成する前に、ビルド SCM リポジトリを入力として使用できる作業パイプラインがなければならず、また、ツルチェンに Artifactory を構成しておく必要もあります。Artifactory の構成手順については、[Artifactory](#artifactory) のセクションを参照してください。

{{site.data.keyword.deliverypipeline}} を構成して npm ビルド・ジョブを追加します。

1. ステジを作成し、入力を適切な SCM リポジトリに設定します。
1. このステジでビルド・ジョブを追加します。
1. ビルド・ジョブを構成します。
  ![npm ビルド・ジョブ](images/artifactory_npm_job.png)

  a. ビルダ・タイプに**「NPM ビルド (NPM Build)」**を選択します。

  b. Artifactory ツル統合の複数インスタンスを構成した場合、npm ビルド・ジョブを構成する対象にしたい Artifactory ツル統合の名前を入力します。

  c. ツル統合タイプに**「Artifactory」**を選択します。

  d. ビルド・コマンドには、npm モジュルのビルドまたはレジストリへのモジュルのパブリッシュを行うコマンドを入力します。次の例は、モジュルのビルドまたはパブリッシュのいずれかを行うコマンドを示します。
     ```
     npm install
     # or
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **ヒント:** レジストリへの接続に使用した URL およびユザ資格情報は、Artifactory ツル統合の構成設定で見つけることができます。

  e. ビルド・ジョブが Artifactory レジストリへのパブリッシュを行い、かつ、ノド・モジュル・バジョンのフォマットが `x.y.z-SNAPSHOT.w` である場合、**「スナップショット・モジュル・バジョンのインクリメント (Increment snapshot module version)」**チェック・ボックスにチェック・マクを付けます。ビルド・ジョブは、モジュル・バジョンを自動的に更新した後で、Artifactory レジストリにパブリッシュします。ジョブは、npm レジストリおよびロカル `package.json` ファイルから最高バジョンのモジュルを選択し、semver を使用してモジュル・バジョンを増やします。ビルド・ジョブは、変更を SCM リポジトリに配信しません。

1. **「保存」**をクリックします。パイプラインが実行されると、このビルド・ジョブは Artifactory ツル統合からの構成情報を使用して npm レジストリに接続します。

### パイプラインに Artifactory Maven ビルド・ジョブを構成する
{: #config_artifactory_maven}

パイプラインに Maven ビルド・ジョブを構成する前に、ビルド SCM リポジトリを入力として使用できる作業パイプラインが存在している必要があり、また、ツルチェンに Artifactory を構成しておく必要もあります。Artifactory の構成手順については、[Artifactory](#artifactory) のセクションを参照してください。

{{site.data.keyword.deliverypipeline}} を構成して Maven ビルド・ジョブを追加します。

1. ステジを作成し、入力を適切な SCM リポジトリに設定します。
1. このステジでビルド・ジョブを追加します。
1. ビルド・ジョブを構成します。
  ![Maven ビルド・ジョブ](images/artifactory_maven_job.png)

  a. ビルダ・タイプに**「Maven ビルド (Maven Build)」**を選択します。

  b. Artifactory ツル統合の複数インスタンスを構成した場合、Maven ビルド・ジョブを構成する対象にしたい Artifactory ツル統合の名前を入力します。

  c. ツル統合タイプに**「Artifactory」**を選択します。

  d. ビルド・コマンドには、Maven モジュルのビルドまたはスナップショット・レジストリへのモジュルのパブリッシュを行うコマンドを入力します。次の例は、モジュルのビルドまたはスナップショット・レジストリへのモジュルのパブリッシュのいずれかを行うコマンドを示します。
     ```
     mvn -B clean package
     # or
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **ヒント:** レジストリへの接続に使用した URL およびユザ資格情報は、Artifactory ツル統合の構成設定で見つけることができます。

1. **「保存」**をクリックします。パイプラインが実行されると、このビルド・ジョブは Artifactory ツル統合からの構成情報を使用して Maven リポジトリに接続します。

詳しくは、「[Artifactory ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/deliver/tool_artifactory/){: new_window}」を参照してください。


## Availability Monitoring の追加
{: #availabilitymonitoring}

{{site.data.keyword.prf_hublong}} は、ユザに影響が及ぶ前に、問題を切り分け、パタンを識別し、パフォマンスを改善します。世界中の場所でアプリをテストし、Delivery Pipeline に統合し、コドを継続的に最適化する方法についての洞察を深めることができます。

**注:** このツル統合は事前構成されているため、構成パラメタは必要ありません。このツル統合を再構成することはできません。

アプリをビルドするときに、アプリの正常性をテスト、モニタ、および改善するために、{{site.data.keyword.prf_hubshort}} ツル統合を追加します。

1. DevOps ダッシュボドの「ツルチェン」ペジで、{{site.data.keyword.prf_hubshort}} を追加するツルチェンをクリックします。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「{{site.data.keyword.prf_hubshort}}」**をクリックします。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. **「{{site.data.keyword.prf_hubshort}}」**をクリックして {{site.data.keyword.prf_hubshort}} ダッシュボドを開き、アプリを選択し、そのアプリのモニタリングを構成します。

詳しくは、[{{site.data.keyword.prf_hublong}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/manage/tool_bluemix_availability_monitoring/){: new_window} を参照してください。


## Cloud Event Management (試験段階) の追加
{: #cloudeventmanagement}

{{site.data.keyword.evtmgt_full}} は、ユザのサビス、アプリケション、およびインフラストラクチャで発生する問題の統合ビュを提供します。問題をより効率的に解決できるよう、リアルタイムのインシデント管理をセットアップできます。

**注:** このツル統合は事前構成されているため、構成パラメタは必要ありません。これを再構成することはできません。

信頼できる運用正常性、サビス品質、および継続的改善という目標を DevOps チムが達成するのを助けるために、Cloud Event Management をツルチェンに追加します。

1. DevOps ダッシュボドから、**「ツルチェン」**をクリックします。Cloud Event Management を追加するツルチェンをクリックします。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「Cloud Event Management」**をクリックします。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. ツルチェンから、以下のツル・カドのうち任意のものをクリックします。

 * Cloud Event Management を開始するには、**「Cloud Event Management」**をクリックします。

 * 問題の通知をユザがいつ受け取るのかを決定するポリシを作成するには、**「{{site.data.keyword.alertnotificationshort}}」**をクリックします。

 * Cloud Event Management で運用手順書のカタログを管理するには、**「Runbook Automation」**をクリックします。

詳しくは、[Cloud Event Management ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/manage/tool_cloud_event_mgt/){: new_window} を参照してください。


## Delivery Pipeline の構成
{: #deliverypipeline}

{{site.data.keyword.deliverypipeline}} は、入力を取得してジョブ (ビルド、テスト、デプロイメントなど) を実行するステジのシケンスを通して、プロジェクトの継続的デプロイメントを自動化します。

アプリの継続的なビルド、テスト、デプロイメントを自動化するように {{site.data.keyword.deliverypipeline}}を構成します。

1. ツルチェン作成時にこのツル統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「{{site.data.keyword.deliverypipeline}}」**をクリックします。使用するテンプレトに応じて、使用できるフィルドは異なります。デフォルトのフィルド値を確認し、必要に応じてそれらの設定を変更します。
1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「{{site.data.keyword.deliverypipeline}}」**をクリックします。

1. 新しいパイプラインの名前を指定します。
1. パイプラインを使用してユザ・インタフェスをデプロイするよう計画している場合は、**「アプリケションの表示メニュでアプリケションを表示する (Show apps in the VIEW APP  menu)」**チェック・ボックスを選択します。パイプラインが作成するすべてのアプリケションが、ツルチェンの「概要」ペジの**「アプリケションの表示 (View App)」**リストに表示されます。
1. **「統合の作成 (Create Integration)」**をクリックして、{{site.data.keyword.deliverypipeline}} をツルチェンに追加します。
1. **「{{site.data.keyword.deliverypipeline}}」**をクリックして、パイプラインを表示し、構成します。パイプラインの構成の基本を確認するには、『[パイプラインのビルドとデプロイ](/docs/services/ContinuousDelivery/pipeline_build_deploy.html){: new_window}』を参照してください。

  **ヒント:** GitHub リポジトリ、{{site.data.keyword.ghe_short}} リポジトリ、または Git リポジトリにコミットがプッシュされるとパイプラインが自動的に実行されるようにしたい場合は、以下のステップを実行します。

   a. パイプラインのステジを定義する前に、ツルチェン用に GitHub、{{site.data.keyword.ghe_short}}、または Git Repos and Issue Tracking を構成します。パイプラインのステジには、リポジトリの Git URL が必要です。各パイプライン・ステジは、ツルチェンと関連付けられた、GitHub リポジトリ、{{site.data.keyword.ghe_short}} リポジトリ、または Git リポジトリのうち 1 つのみを参照できます。GitHub の構成手順については、[GitHub](#github) のセクションを参照してください。Dedicated {{site.data.keyword.ghe_short}} の構成方法については、『[{{site.data.keyword.ghe_long}} 概説](/docs/services/ghededicated/index.html){: new_window}』を参照してください。Git Repos and Issue Tracking の構成方法については、[Git Repos and Issue Tracking](##gitbluemix) のセクションを参照してください。

   b. Web フックを使用します。Web フックを使用しない場合、パイプラインは手動でのみ実行できます。GitHub リポジトリまたは {{site.data.keyword.ghe_short}} リポジトリにリンクする場合に Web フックを使用するには、管理特権が必要です。Git Repos and Issue Tracking リポジトリにリンクするには、Master または Owner 特権が必要です。

1. オプション: {{site.data.keyword.Bluemix_notm}} Public でツルチェンを使用していて、Sauce Labs でアプリのテストを実行したい場合、{{site.data.keyword.deliverypipeline}} を構成して Sauce Labs テスト・ジョブを追加します。テスト・ジョブの構成手順については、『[パイプラインに SauceLabs テスト・ジョブを構成する](#config_saucelabs)』セクションを参照してください。

### パイプラインに Sauce Labs テスト・ジョブを構成する
{: #config_saucelabs}

パイプラインに Sauce Labs テスト・ジョブを構成する前に、アプリをビルドしてデプロイするためのステジを含む、正常に機能するパイプラインが存在していなければなりません。また、ツルチェンに Sauce Labs を構成しておく必要もあります。Sauce Labs の構成手順については、[Sauce Labs](#saucelabs) のセクションを参照してください。

{{site.data.keyword.deliverypipeline}} を構成して Sauce Labs テスト・ジョブを追加します。

1. アプリのテスト・バジョンをデプロイするステジがない場合は作成します。
1. そのステジで、デプロイ・ジョブの後にテスト・ジョブを追加します。これらのジョブは、同じステジに置くことにより、同じ環境プロパティのセットにアクセスできるようになります。
   
  ![テスト・ジョブ
](images/toolchain_test_job.png)

1. 次の手順で、ステジを構成します。

  a. **「環境プロパティ (ENVIRONMENT PROPERTIES)」**タブで、CF_APP_NAME、SAUCE_USERNAME、SAUCE_ACCESS_KEY の 3 つのプロパティを作成します。

  b. Sauce Labs のユザ名とアクセス・キを入力します。こうすることで、これらの値が外部化され、テストで利用できるようになります。

1. デプロイ・ジョブを構成します。「デプロイ・スクリプト」**フィルドに、コマンド `export CF_APP_NAME="$CF_APP"` を含めます。**このコマンドは、アプリ名を環境プロパティとしてエクスポトします。
1. テスト・ジョブを構成します。次の図は、値の例を示しています。
**「サビス・インスタンス」**、**「タゲット」**、**「組織」**、**「スペス」**の各フィルドには、使用中の Sauce Labs のユザ名、地域、組織、スペスが取り込まれます。
  
![ジョブの構成](images/toolchain_configure_job.png)

  a. テスタ・タイプには、**Sauce Labs** を選択します。

  b. サビス・インスタンスでは、ツルチェンに Sauce Labs を構成したときに使用した Sauce Labs のユザ名を選択します。

   **ヒント**: ツルチェン用に Sauce Labs を構成したときに使用したユザ名およびアクセス・キを表示するには、**「構成」**をクリックします。

  c. **「テスト実行コマンド (Test Execution Command)」**フィルドに、テストに必要な依存関係をインストルしてテストを実行するコマンドを入力します。例えば、Node.js アプリの場合、次のようなコマンドを入力します。
     ```
     npm install
     node_modules/grunt-cli/bin/grunt test:sauce:parallel
     ```

    d. テスト・ジョブ・ログでテストのレポトを確認する場合は、**「テスト・レポトを有効にする (Enable Test Report)」**チェック・ボックスにチェックマクを付け、「テスト結果のファイル・パタン (Test Result File Pattern)」を `test/*.xml` に設定します。

1. **「保存」**をクリックします。パイプラインが実行されるときには必ず Sauce Labs のテストが実行されます。

詳しくは、[Delivery Pipeline ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/deliver/tool_delivery_pipeline/){: new_window} を参照してください。


## DevOps Insights (ベタ版) の追加
{: #dra}

{{site.data.keyword.DRA_full}} は、単体テスト、機能テスト、およびコド・カバレッジ・ツルからの結果を収集して分析し、コドがデプロイメント・プロセスの指定されたゲトで事前定義の基準を満たすかどうかを判断します。コドが基準を満たしていない、または基準を超えていない場合、リスク回避のために、デプロイメントが停止されます。{{site.data.keyword.DRA_short}} を、継続的デリバリ環境のセフティ・ネットとして、または品質標準の実装および改善のための手段として使用することができます。

 **注:** このツル統合は {{site.data.keyword.Bluemix_notm}} Public でのみ使用可能です。これは事前構成されているため、構成パラメタは必要ありません。このツル統合を再構成することはできません。

{{site.data.keyword.DRA_short}} を追加し、デプロイメントをモニタリングしてリリス前にリスクを洗い出すことで、{{site.data.keyword.Bluemix_notm}} のコドの品質を維持し、向上させることができます。

1. ツルチェン作成時にこのツル統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「{{site.data.keyword.DRA_short}}」**をクリックします。
1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「{{site.data.keyword.DRA_short}}」**をクリックします。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. **「{{site.data.keyword.DRA_short}}」**をクリックし、開始手順 (基準の作成、パイプラインへの基準の接続、パイプラインの実行) を完了します。

詳しくは、[{{site.data.keyword.DRA_short}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/learn/tool_devops_insights/){: new_window} を参照してください。


## Eclipse Orion Web IDE の追加
{: #webide}

Eclipse Orion {{site.data.keyword.webide}} は、ソス管理タスクを作成、編集、実行、デバッグ、完了できる Web ベスの統合環境です。編集から実行、送信、そしてデプロイまで、シムレスに行うことができます。

 **注**: このツル統合は事前構成済みです。構成パラメタは不要で、再構成することはできません。

ソス管理タスクを完了するには、次の手順で Eclipse Orion {{site.data.keyword.webide}} ツル統合を追加します。

1. ツルチェン作成時にこのツル統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Eclipse Orion {{site.data.keyword.webide}}」**をクリックします。
1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合」セクションで、**「Eclipse Orion {{site.data.keyword.webide}}」**をクリックします。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. **「Eclipse Orion {{site.data.keyword.webide}}」**をクリックします。ワクスペスに GitHub または {{site.data.keyword.ghe_short}} のリポジトリが事前に取り込まれています。現行のツルチェンと関連付けられているリポジトリは強調表示されます。

詳しくは、『[ Eclipse Orion {{site.data.keyword.webide}} によるコドの編集](/docs/services/ContinuousDelivery/web_ide.html){: new_window}』および [Eclipse Orion {{site.data.keyword.webide}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/code/tool_eclipse_orion_web_ide/){: new_window} を参照してください。


## Git Repos and Issue Tracking (ベタ) の構成
{: #gitbluemix}

Git Repos and Issue Tracking ツル統合は、GitLab Community Edition (Git リポジトリ用の Web ベスのホスティング・サビス) をベスにしています。リポジトリのロカルとリモトの両方のコピを持つことができます。詳しくは、[Git Repos and Issue Tracking ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/help){:new_window} を参照してください。

ツルチェンの作成時に Git Repos and Issue Tracking を構成する場合は、以下のステップを実行します。    

1. 「構成可能な統合 (Configurable Integrations)」セクションで**「Git Repos and Issue Tracking」**をクリックします。
1. Git リポジトリのデフォルト・タゲット・ロケションを確認します。これらのリポジトリは、サンプル・リポジトリのクロンです。必要に応じて、タゲット・リポジトリの名前を変更します。


ツルチェンがあり、そのツルチェンに Git Repos and Issue Tracking を追加する場合は、以下のステップを実行します。    

1. DevOps ダッシュボドの**「ツルチェン」**ペジで、ツルチェンをクリックしてその「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックし、**「概要」**をクリックします。
1. **「ツルの追加 (Add a Tool)」**をクリックします。
1. 「ツル統合 (Tool Integrations)」セクションで**「Git Repos and Issue Tracking」**をクリックします。
1. リポジトリ・タイプを選択します。     

  a. 空のリポジトリを作成する場合は、リポジトリのタイプとして**「新規 (New)」**をクリックし、リポジトリ名を入力します。    
  b. マジ要求を通して変更内容を提供できるように Git リポジトリをフォクする場合は、リポジトリのタイプとして**「フォク (Fork)」**をクリックします。ソス・リポジトリの URL を入力します。    
  c. Git リポジトリのコピを作成する場合は、リポジトリのタイプとして**「クロンを作成する (Clone)」**をクリックします。新規リポジトリ名と、ソス・リポジトリの URL を入力します。     
  d. 既存の Git リポジトリを使用する場合は、リポジトリのタイプとして**「既存」**をクリックします。URL を入力します。    

1. 問題のトラッキングに Issues を使用する場合は、**「Issues を使用可能にする (Enable Issues)」**チェック・ボックスにチェック・マクを付けます。
1. コミットに対するタグおよびコメントと、コミットで参照される問題に対するラベルおよびコメントを作成することによって、コド変更のデプロイメントをトラッキングしたい場合は、**「コド変更のデプロイメントを追跡する (Track deployment of code changes)」**チェック・ボックスにチェック・マクを付けます。詳しくは、[Track where your code is deployed with toolchains ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window} を参照してください。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 作業対象の Git リポジトリのカドをクリックします。プロジェクト概要のペジが開きます。    

**注:** リンクしようとしているリポジトリに対する Master または Owner 特権をお持ちでない場合、Web フックを使用できないので統合は制限されます。リポジトリにコミットがプッシュされたときにパイプラインが自動的に実行されるようにするには、Web フックが必要です。Web フックがない場合、パイプラインを手動で開始する必要があります。


## GitHub and Issues の構成
{: #github}

GitHub は、Git リポジトリの Web ベスのホスティング・サビスです。リポジトリのロカルとリモトの両方のコピを持つことができるので、共同作業が容易になります。

GitHub Issues は、作業と計画のすべてを 1 つの場所に保持するトラッキング・ツルです。これは、ユザが重要タスクに注力できるようにユザの開発リポジトリと統合されます。

GitHub を構成して、クラウドでソス・コドを管理します。

1. ツルチェンの作成時にこのツル統合を構成する場合は、次の手順を実行します。

 a. 「構成可能な統合 (Configurable Integrations)」セクションで**「GitHub」**をクリックします。{{site.data.keyword.Bluemix_notm}} Public でツルチェンを作成していて、 {{site.data.keyword.Bluemix_notm}} に GitHub へのアクセスをまだ認可していなければ、**「認可 (Authorize)」** をクリックして GitHub Web サイトに移動します。アクティブな GitHub セッションがない場合は、ログインするよう求められます。**「アプリケションを許可 (Authorize Application)」** をクリックして、{{site.data.keyword.Bluemix_notm}} が GitHub アカウントにアクセスできるようにします。アクティブな GitHub セッションはあるものの、最近パスワドを入力していない場合は、確認のために GitHub パスワドの入力を求められることがあります。

 b. GitHub リポジトリのデフォルトのタゲット・リポジトリの場所を確認します。これらのリポジトリは、サンプル・リポジトリのクロンです。必要に応じて、タゲット・リポジトリの名前を変更します。
![デフォルトのタゲット・リポジトリの場所](images/toolchain_github_config.png)

1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「GitHub」**をクリックします。

1. 既存の GitHub リポジトリを使用する場合は、リポジトリのタイプとして**「既存」**をクリックし、URL を入力します。
1. 新しい GitHub リポジトリを使用する場合は、その GitHub リポジトリに付ける名前を入力し、複製またはフォクするリポジトリの URL を入力し、リポジトリ・タイプを次のように選択します。

 a. 空のリポジトリを作成する場合は、**「新規」**をクリックします。

 b. GitHub リポジトリのコピを作成する場合は、**「クロンを作成する (Clone)」**をクリックします。

 c. GitHub リポジトリをフォクし、プル・リクエストで変更内容を提供できるようにする場合は、**「フォク (Fork)」**をクリックします。

1. 問題のトラッキングに GitHub Issues を使用する場合は、**「GitHub Issues を使用可能にする (Enable GitHub Issues)」**チェック・ボックスにチェック・マクを付けます。
1. コミットに対するタグおよびコメントと、コミットで参照される問題に対するラベルおよびコメントを作成することによって、コド変更のデプロイメントをトラッキングしたい場合は、**「コド変更のデプロイメントを追跡する (Track deployment of code changes)」**チェック・ボックスにチェック・マクを付けます。詳しくは、[Track where your code is deployed with toolchains ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2017/03/track-code-deployed-toolchains/){:new_window} を参照してください。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 作業対象の GitHub リポジトリのカドをクリックします。GitHub の Web サイトが開きます。そこでリポジトリの内容を表示できます。

  **ヒント**: Eclipse Orion {{site.data.keyword.webide}} の統合ソス・コド管理ツルを使用して、GitHub リポジトリを編集し、ワクスペスからアプリをデプロイすることができます。

1. GitHub Issues を使用可能にした場合、**「GitHub Issues」**をクリックして開きます。ツルチェンに複数の GitHub リポジトリが含まれれている場合でも、GitHub Issues のこのインスタンスをツルチェン全体に使用できます。    

**注:** リンクしようとしているリポジトリに対する管理特権をお持ちでない場合、Web フックを使用できないので統合は制限されます。リポジトリにコミットがプッシュされたときにパイプラインが自動的に実行されるようにするには、Web フックが必要です。Web フックがない場合、パイプラインを手動で開始する必要があります。

詳しくは、[GitHub ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/code/tool_github/){: new_window} および [GitHub Issues ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window} を参照してください。


## Bluemix Dedicated での GitHub Enterprise および GitHub Issues の構成
{: #configghe}

 **注:** ここで説明する手順は、{{site.data.keyword.Bluemix_notm}} Dedicated for {{site.data.keyword.ghe_short}} に適用されます。独自の管理版の {{site.data.keyword.ghe_short}} を使用している場合、内部手順によっては一部のステップが異なることがあります。

{{site.data.keyword.ghe_long}} は、オンプレミス型の Web ベスの Git リポジトリ・ホスティング・サビスです。Dedicated {{site.data.keyword.ghe_short}} は {{site.data.keyword.Bluemix_notm}} Dedicated ユザ専用です。GitHub Issues は、作業と計画を 1 つの場所に保持するトラッキング・ツルです。これは、ユザが重要タスクに注力できるようにユザの開発リポジトリと統合されます。Dedicated {{site.data.keyword.ghe_short}} と GitHub Issues の詳細については、「[{{site.data.keyword.ghe_long}}の概説](/docs/services/ghededicated/index.html){: new_window}」と「[GitHub Issues![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/think/tool_github_issues/){: new_window}」を参照してください。

{{site.data.keyword.ghe_short}}  をツルチェン内の 1 つのツル統合として構成して、会社の [{{site.data.keyword.Bluemix_notm}} Dedicated](/docs/dedicated/index.html#dedicated){: new_window} インスタンス内でソス・コドを管理できるようにすることができます。

1. ツルチェンの作成時にこのツル統合を構成する場合は、次の手順を実行します。

 a. Dedicated {{site.data.keyword.ghe_short}} に初めてログインするときは、まずその前に LDAP を使用して会社のユザ・レジストリから自分のユザ ID を {{site.data.keyword.Bluemix_notm}} Dedicated インスタンスに追加するよう、会社の地域管理者に依頼してください。{{site.data.keyword.ghe_short}} アカウントの設定の詳細については、「[{{site.data.keyword.ghe_long}}の概説](/docs/services/ghededicated/index.html){: new_window}」を参照してください。

 b. 「構成可能な統合 (Configurable Integrations)」セクションで**「{{site.data.keyword.ghe_short}}」**をクリックします。    

 c. 新しい {{site.data.keyword.ghe_short}} リポジトリのデフォルト名を確認します。必要に応じて、新しいリポジトリの名前を変更してください。次のイメジは、サンプル・リポジトリのクロンとして作成されたリポジトリの例を示しています。既存のリポジトリを使用することも、新しいリポジトリを使用することもできます。新しいリポジトリを使用する場合は、空のリポジトリを作成するか、リポジトリのクロンを作成するか、リポジトリをフォクすることができます。
![デフォルトのリポジトリの場所](images/toolchain_ghe_config.png)

1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「{{site.data.keyword.ghe_short}}」**をクリックします。

1. 既存の {{site.data.keyword.ghe_short}} リポジトリを使用する場合は、そのリポジトリの URL を入力します。リポジトリ・タイプには、**「既存」**をクリックします。
1. 新しい {{site.data.keyword.ghe_short}} リポジトリを使用する場合は、そのリポジトリに付ける名前を入力し、複製またはフォクするリポジトリの URL を入力し、リポジトリ・タイプを次のように選択します。

 a. 空のリポジトリを作成する場合は、**「新規」**をクリックします。

 b. リポジトリのコピを作成する場合は、**「クロンを作成する (Clone)」**をクリックします。

 c. リポジトリをフォクし、プル・リクエストで変更内容を提供できるようにする場合は、**「フォク (Fork)」**をクリックします。

1. 問題のトラッキングに GitHub Issues を使用する場合は、**「GitHub Issues を使用可能にする (Enable GitHub Issues)」**チェック・ボックスにチェック・マクを付けます。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. 作業対象の {{site.data.keyword.ghe_short}} リポジトリのカドをクリックします。会社の {{site.data.keyword.ghe_short}} リポジトリが開きます。

  **ヒント**: Eclipse Orion {{site.data.keyword.webide}} の統合ソス・コド管理ツルを使用して、{{site.data.keyword.ghe_short}} リポジトリを編集し、ワクスペスからアプリをデプロイすることができます。

1. GitHub Issues を使用可能にした場合、**「GitHub Issues」**をクリックします。ツルチェンに複数の GitHub リポジトリが含まれれている場合でも、GitHub Issues のこのインスタンスをツルチェン全体に使用できます。    

**注:** リンクしようとしているリポジトリに対する管理特権をお持ちでない場合、Web フックを使用できないので統合は制限されます。リポジトリにコミットがプッシュされたときにパイプラインが自動的に実行されるようにするには、Web フックが必要です。Web フックがない場合、パイプラインを手動で開始する必要があります。


## Jenkins の構成
{: #jenkins}

Jenkins は、ソフトウェアを継続的にビルドおよびテストする、サバ・ベスのオプン・ソスのツルであり、継続的統合および継続的デリバリの履行をサポトします。

**重要**: Jenkins ツル統合を作成する前に、Jenkins サバを用意する必要があります。

Jenkins ツル統合を使用すれば、Jenkins ジョブ通知をツルチェン内の他のツル (Slack や PagerDuty など) に送信できます。デプロイメントでコドをトレスするために、デプロイメント・メッセジを Git コミットや関連 Git/JIRA 問題に追加できます。また、デプロイメントを「ツルチェン接続」ペジに表示することもできます。テスト結果を {{site.data.keyword.DRA_short}} に送信し、自動化された品質ゲトを追加し、デプロイメント・リスクをトラッキングすることができます。

アプリの継続的なビルド、テスト、デプロイメントを自動化するために Jenkins を構成します。

1. ツルチェン作成時にこのツル統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Jenkins」**をクリックします。
1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックします。次に、**「概要」**をクリックします。  

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「Jenkins」**をクリックします。

1. ツルチェン内の Jenkins カドでこのツル統合に対して表示したい名前を入力します。
1. ツルチェンから Jenkins カドをクリックしたときに開くようにしたい Jenkins サバの URL を入力します。
1. 生成されたツルチェン Web フックをコピします。
1. Jenkins サバで、以下のステップを実行します。

 a. [Cloud Foundry CLI ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html){: new_window} をインストルします。

 b. 以下のいずれかのコマンドを入力することによって、IBM Cloud DevOps Cloud Foundry プラグインをインストルします。

  * Mac OS: `cf install-plugin https://icd.ng.bluemix.net/icd_darwin_amd64`

  * Linux または Docker: `cf install-plugin https://icd.ng.bluemix.net/icd_linux_amd64`

 c. DevOps Insights および Notifications 用の IBM Cloud DevOps Jenkins プラグインをインストルおよび構成します。詳しくは、[プラグインのインストルおよび構成](/docs/services/DevOpsInsights/insights_risk.html#integrate_jenkins){: new_window}を参照してください。

 d. ツルチェンに通知を送信するようにしたいジョブごとに、以下のステップを実行します。

  * **「このプロジェクトはパラメタ化される (This project is parameterized)」**チェック・ボックスにチェック・マクを付けます。

  * `ICD_WEBHOOK_URL` ストリング・パラメタを追加します。

  * 生成されたツルチェン Web フックを貼り付けます。
 ![Web フック URL](images/jenkins_webhook_url.png)

  * IBM Cloud DevOps - Webhook Notification のビルド後アクションを追加し、**「ジョブ完了 (Job Completed)」**チェック・ボックスにチェック・マクを付けます。
 ![ビルド後アクション](images/jenkins_postbuild_action.png)  

 e. デプロイ・ジョブで、以下のステップを実行します。

  * `ICD_WEBHOOK_URL`、`CF_API`、`CF_ORG`、`CF_SPACE`、および `CF_APP` ストリング・パラメタを追加します。以下の例は、各ストリング・パラメタの追加方法を示します。
 ![Webhook URL ストリング・パラメタ](images/jenkins_set_webhook_url.png)
 ![CFI API ストリング・パラメタ](images/jenkins_set_cfapi.png)
 ![CFI ORG ストリング・パラメタ](images/jenkins_set_cforg.png)
 ![CFI SPACE ストリング・パラメタ](images/jenkins_set_cfspace.png)
 ![CFI APP ストリング・パラメタ](images/jenkins_set_cfapp.png)

  * `CF_CREDS_USR` ユザ名変数および `CF_CREDS_PSW` パスワド変数を使用して、Cloud Foundry CLI のバインディングを構成します。
 ![Cloud Foundry CLI バインディング](images/jenkins_config_bindings.png)  

  * **「ビルド (Build)」**フィルドに以下のコマンドを入力してログインし、IBM Cloud DevOps Cloud Foundry プラグインを使用してアプリケション・デプロイ可能マッピングを、Git コミット追跡可能性を有効にしてツルチェンに送信します。
 ![ビルド・コマンド](images/jenkins_build_commands.png)    

  * **「ビルド (Build)」**フィルドに `cf icd --create-connection $ICD_WEBHOOK_URL $CF_APP` コマンドを入力して、アプリケション・デプロイ可能マッピングをツルチェンに送信します。    

 f. 変更を保存し、Jenkins ツル統合の「統合の構成 (Configure the Integration)」ペジに戻ります。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. ツルチェンから、**「Jenkins」**をクリックして Jenkins サバを表示します。  

詳しくは、[Jenkins ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/deliver/tool_jenkins/){: new_window} を参照してください。


## JIRA の構成
{: #jira}

JIRA は、ユザのソフトウェアに関連する問題およびバグを追跡するツルです。Jenkins または {{site.data.keyword.deliverypipeline}} によってデプロイメントが実行されるたびに、JIRA ツル統合はプロジェクトの問題を更新します。JIRA ツル統合で問題をトラッキングするには、コミット・メッセジ内で JIRA Smart Commits を使用する必要があります。JIRA Smart Commits について詳しくは、[Using Smart Commits ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://confluence.atlassian.com/fisheye/using-smart-commits-298976812.html){: new_window} を参照してください。

品質コドの計画、追跡、および配信のために、JIRA を構成します。

1. ツルチェン作成時にこのツル統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「JIRA」**をクリックします。
1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックします。次に、**「概要」**をクリックします。  

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「JIRA」**をクリックします。

1. JIRA プロジェクトがあり、それに接続したい場合、JIRA タイプとして**「既存」**をクリックします。

 a. JIRA プロジェクトの JIRA プロジェクト・キを入力します。プロジェクト・キは JIRA プロジェクトの URL に含まれています。

 b. JIRA インスタンスのベス API URL を入力します。API URL は、JIRA インスタンスのヘッダで見つけることができます。**「管理」**アイコンをクリックし、**「システム」**をクリックします。

 c. オプション: JIRA ユザ名を入力します。ユザ名が必要となるのは、プライベト JIRA インスタンスに接続する場合、または、パブリック・インスタンスに接続し、かつ、トレサビリティ情報を受け取りたい場合に限ります。

 d. オプション: JIRA パスワドを入力します。パスワドが必要となるのは、プライベト JIRA インスタンスに接続する場合、または、パブリック・インスタンスに接続し、かつ、トレサビリティ情報を受け取りたい場合に限ります。

 e. 参照される問題に対するラベルおよびコメントを作成することによってプロジェクトに関するコド変更のデプロイメントをトラッキングするには、**「コド変更のデプロイメントを追跡する (Track deployment of code changes)」**チェック・ボックスにチェック・マクを付けます。JIRA Smart Commit を使用して、GitHub コミットの JIRA 問題を参照するようにしてください。このオプションが選択されていない場合、JIRA ツル統合はすべてのコミットを無視します。

1. JIRA プロジェクトを作成する場合、JIRA タイプとして**「新規 (New)」**を選択します。

 a. 新規プロジェクトに使用する JIRA プロジェクト・キを入力します。このキは、プロジェクト URL 内で固有 ID として使用されます。

 b. JIRA プロジェクトの名前を入力します。

 c. JIRA インスタンスのベス API URL を入力します。API URL は、JIRA インスタンスのヘッダで見つけることができます。**「管理」**アイコンをクリックし、**「システム」**をクリックします。

 d. このプロジェクトに使用したい JIRA プロジェクト・リダのユザ名を入力します。JIRA プロジェクト・リダとして指定される個人は、JIRA でプロジェクト・リダ許可を持っている必要があります。

 e. JIRA のこのインスタンスの管理者のユザ名を入力します。

 f. JIRA のこのインスタンスの管理者のパスワドを入力します。

 g. 参照される問題に対するラベルおよびコメントを作成することによってプロジェクトに関するコド変更のデプロイメントをトラッキングするには、**「コド変更のデプロイメントを追跡する (Track deployment of code changes)」**チェック・ボックスにチェック・マクを付けます。JIRA Smart Commit を使用して、GitHub コミットの JIRA 問題を参照するようにしてください。このオプションが選択されていない場合、JIRA ツル統合はすべてのコミットを無視します。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. ツルチェンから**「JIRA」**をクリックして、接続する JIRA プロジェクトのダッシュボドを表示します。

詳しくは、[JIRA ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/code/tool_jira/){: new_window} を参照してください。


## Nexus の構成
{: #nexus}

ビルド成果物を Nexus リポジトリに保管するように Nexus リポジトリ・マネジャを構成します。

1. ツルチェン作成時にこのツル統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Nexus」**をクリックします。
1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックします。次に、**「概要」**をクリックします。  

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「Nexus」**をクリックします。

1. Nexus ツル統合のこのインスタンスの名前を入力します。
1. ツルチェンから Nexus カドをクリックしたときに開くようにしたい Nexus リポジトリの URL を入力します。
1. 接続先にするリポジトリのタイプを選択します。
1. **「npm レジストリ」**を選択した場合は、以下のステップを実行します。

 a. レジストリと関連付けられた E メル・アドレスを入力します。

 b. レジストリと関連付けられた認証トクンを入力します。

 c. Nexus サバ上のプライベト・レジストリである Nexus リリス・リポジトリの URL を入力します。

 d. 複数のパブリックおよびプライベト npm レジストリを結合するために使用する Mirror または Public レジストリの URL を入力します。例えば、この URL は、プライベト・レジストリと、npm グロバル・レジストリのキャッシュの両方にアクセスできる、Nexus サバ上の仮想レジストリの URL であることができます。

1. **「Maven リポジトリ」**を選択した場合は、以下のステップを実行します。

 a. リポジトリと関連付けられたユザ ID を入力します。

 b. リポジトリと関連付けられたパスワドを入力します。

 c. Nexus サバ上のプライベト・リリス・リポジトリである Nexus リリス・リポジトリの URL を入力します。

 d. Nexus サバ上のプライベト・スナップショット・リポジトリである Nexus スナップショット・リポジトリの URL を入力します。

 e. 複数のパブリックおよびプライベト Maven リポジトリを結合するために使用する Mirror または Public リポジトリの URL を入力します。例えば、この URL は、プライベト・リポジトリと、Maven 中央リポジトリのキャッシュの両方にアクセスできる、Nexus サバ上の仮想リポジトリの URL であることができます。

1. **「統合の作成 (Create Integration)」**をクリックします。
1. 作業対象の Nexus リポジトリのカドをツルチェンからクリックします。Nexus の Web サイトが開きます。そこでリポジトリの内容を表示できます。
1. オプション: {{site.data.keyword.Bluemix_notm}} Public でツルチェンを使用していて、Nexus を npm と共に使用してアプリをビルドしたい場合、パイプラインを構成して npm ビルド・ジョブを追加します。ビルド・ジョブの構成手順については、『[パイプラインに Nexus npm ビルド・ジョブを構成する](#config_nexus_npm)』セクションを参照してください。
1. オプション: {{site.data.keyword.Bluemix_notm}} Public でツルチェンを使用していて、Nexus を Maven と共に使用してアプリをビルドしたい場合、パイプラインを構成して Maven ビルド・ジョブを追加します。ビルド・ジョブの構成手順については、『[パイプラインに Nexus Maven ビルド・ジョブを構成する](#config_nexus_maven)』セクションを参照してください。

### パイプラインに Nexus npm ビルド・ジョブを構成する
{: #config_nexus_npm}

パイプラインに npm ビルド・ジョブを構成する前に、ビルド SCM リポジトリを入力として使用できる作業パイプラインが存在している必要があり、また、ツルチェンに Nexus を構成しておく必要もあります。Nexus の構成手順については、[Nexus](#nexus) のセクションを参照してください。

{{site.data.keyword.deliverypipeline}} を構成して npm ビルド・ジョブを追加します。

1. ステジを作成し、入力を適切な SCM リポジトリに設定します。
1. このステジでビルド・ジョブを追加します。
1. ビルド・ジョブを構成します。
  ![npm ビルド・ジョブ](images/nexus_npm_job.png)

  a. ビルダ・タイプに**「NPM ビルド (NPM Build)」**を選択します。

  b. Nexus ツル統合の複数インスタンスを構成した場合、npm ビルド・ジョブを構成する対象にしたい Nexus ツル統合の名前を入力します。

  c. ツル統合タイプに**「Nexus」**を選択します。

  d. ビルド・コマンドには、npm モジュルのビルドまたはレジストリへのモジュルのパブリッシュを行うコマンドを入力します。次の例は、モジュルのビルドまたはパブリッシュのいずれかを行うコマンドを示します。
     ```
     npm install
     # or
     npm publish --registry "${NPM_RELEASE_URL}"
     ```
  **ヒント:** レジストリへの接続に使用した URL およびユザ資格情報は、Nexus ツル統合の構成設定で見つけることができます。
  e. ビルド・ジョブが Nexus レジストリへのパブリッシュを行い、かつ、ノド・モジュル・バジョンのフォマットが `x.y.z-SNAPSHOT.w` である場合、**「スナップショット・モジュル・バジョンのインクリメント (Increment snapshot module version)」**チェック・ボックスにチェック・マクを付けます。ビルド・ジョブは、モジュル・バジョンを自動的に更新した後で、Nexus レジストリにパブリッシュします。ビルド・ジョブは、npm レジストリおよびロカル `package.json` ファイルから最高バジョンのモジュルを選択し、semver を使用してモジュル・バジョンを増やします。ビルド・ジョブは、変更を SCM リポジトリに配信しません。

1. **「保存」**をクリックします。パイプラインが実行されると、このビルド・ジョブは Nexus ツル統合からの構成情報を使用して npm レジストリに接続します。

### パイプラインに Nexus Maven ビルド・ジョブを構成する
{: #config_nexus_maven}

パイプラインに Maven ビルド・ジョブを構成する前に、ビルド SCM リポジトリを入力として使用できる作業パイプラインが存在している必要があり、また、ツルチェンに Nexus を構成しておく必要もあります。Nexus の構成手順については、[Nexus](#nexus) のセクションを参照してください。

{{site.data.keyword.deliverypipeline}} を構成して Maven ビルド・ジョブを追加します。

1. ステジを作成し、入力を適切な SCM リポジトリに設定します。
1. このステジでビルド・ジョブを追加します。
1. ビルド・ジョブを構成します。
  ![Maven ビルド・ジョブ](images/nexus_maven_job.png)

  a. ビルダ・タイプに**「Maven ビルド (Maven Build)」**を選択します。

  b. Nexus ツル統合の複数インスタンスを構成した場合、Maven ビルド・ジョブを構成する対象にしたい Nexus ツル統合の名前を入力します。

  c. ツル統合タイプに**「Nexus」**を選択します。

  d. ビルド・コマンドには、Maven モジュルのビルドまたはスナップショット・レジストリへのモジュルのパブリッシュを行うコマンドを入力します。次の例は、モジュルのビルドまたはパブリッシュのいずれかを行うコマンドを示します。
     ```
     mvn -B clean package
     # or
     mvn -DaltDeploymentRepository="snapshots::default::${MAVEN_SNAPSHOT_URL}" deploy
     ```
  **ヒント:** レジストリへの接続に使用した URL およびユザ資格情報は、Nexus ツル統合の構成設定で見つけることができます。
1. **「保存」**をクリックします。パイプラインが実行されると、このビルド・ジョブは Nexus ツル統合からの構成情報を使用して Maven リポジトリに接続します。

詳しくは、[Nexus ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/deliver/tool_nexus/){: new_window} を参照してください。


## カスタム・ツル (その他のツル) の構成
{: #othertool}

チムがツルチェン統合リストに含まれていないツルを使用する場合、カスタム・ツルを統合できます。

カスタム・ツルを構成して、ツルチェン内の他のツルとともに機能し、チムで使用できるようにします。

1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで、**「その他のツル (Other Tool)」**をクリックします。

1. ツル名を入力します。

1. ツルに最も密接に関連したライフサイクル・フェズを選択します。この選択によって、「概要」ペジでツルがリストされるカテゴリが決まります。
1. アイコン URL を追加します。このアイコンがツル統合のカドに表示されます。
1. 資料 URL を追加します。
1. ツル・インスタンス名を指定します。例: My Team Tool。
1. ツル・インスタンスの URL を追加します。ツル統合のカドがクリックされると、この URL が開きます。
1. ツルの説明を追加します。
1. (上級) 必要に応じて、さらにプロパティを追加します。例えば、ご使用のツルをツルチェンの他のツルと統合するために必要な情報または属性をリストします。  
1. **「統合の作成 (Create Integration)」**をクリックします。

詳しくは、[Introducing custom tool integration for {{site.data.keyword.Bluemix_notm}} toolchains ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2016/10/custom-tool-integration-with-bluemix-toolchains/){: new_window} を参照してください。


## PagerDuty の構成
{: #pagerduty}

PagerDuty は、複数のモニタリング・システムのデタを単一のビュに統合します。問題が発生すると、PagerDuty によって、その時点で問題の修正に最適なチム・メンバに確実に通知が送信されます。チム・メンバが問題に応答しない場合、次の技術者または運用管理者に問題を転送するようにエスカレションを構成できます。

パイプライン・ステジで障害が発生したときに通知を送信するように PagerDuty を構成して、問題を迅速に修正してダウン時間を削減できるようにします。

1. ツルチェン作成時にこのツル統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「PagerDuty」**をクリックします。
1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「PagerDuty」**をクリックします。

1. PagerDuty アカウントの API アクセス・キを入力します。PagerDuty アカウントをお持ちでない場合は、[登録して取得 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://signup.pagerduty.com/accounts/new){: new_window} してください。キを確認する方法については、[Generating an API Key ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://support.pagerduty.com/hc/en-us/articles/202829310-Generating-an-API-Key){: new_window} を参照してください。
1. PagerDuty サビスの名前を入力します。
1. PagerDuty の 1 次連絡先の E メル・アドレスを入力します。
1. PagerDuty の 1 次連絡先の電話番号を入力します。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. **「PagerDuty」**をクリックして pagerduty.com にアクセスします。ツルチェンに対してこのツル統合を構成したときに指定した PagerDuty サビスに関連付けられているイベントを表示できます。

詳しくは、「[PagerDuty ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/manage/tool_pagerduty/){: new_window}」を参照してください。


## Sauce Labs の構成
{: #saucelabs}

Sauce Labs は、機能単体テストを実行します。{{site.data.keyword.deliverypipeline}} 内のテスト・ジョブとして Sauce Labs テスト・スイトが構成されている場合、そのテスト・スイトは、継続的デリバリ・プロセスの一環として、Web アプリまたはモバイル・アプリに対するテストを実行できます。これらのテストは、誤ったコドがデプロイされるのを防ぐためのゲトとして機能することで、プロジェクトに対して非常に有益なフロ制御を提供します。

 **注:** このツル統合は {{site.data.keyword.Bluemix_notm}} Public でのみ使用可能です。

複数のオペレティング・システムおよびブラウザで自動化された機能テストを実行するように Sauce Labs を構成することによって、ユザがどのように Web サイトやアプリケションを使用するのかをエミュレトできます。

1. ツルチェン作成時にこのツル統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Sauce Labs」**をクリックします。
1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「Sauce Labs」**をクリックします。

1. Sauce Labs アカウントと関連付けられたユザ名を入力します。[ Sauce Labs アカウント・ペジの上部にあるウェルカム・メッセジでユザ名を確認できます ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://saucelabs.com/account){: new_window}。
1. Sauce Labs アカウントのアクセス・キを入力します。[Sauce Labs アカウント・ペジでキを確認できます ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://saucelabs.com/account){: new_window}。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. **「Sauce Labs」**をクリックして saucelabs.com に移動し、ツルチェンのテスト・アクティビティを表示します。

 **ヒント**: Sauce Labs テスト・ジョブを {{site.data.keyword.deliverypipeline}} に追加した場合、サビス・インスタンスを選択できます。

詳しくは、「[Sauce Labs ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/deliver/tool_sauce_labs/){: new_window}」を参照してください。


## Slack の構成
{: #slack}

**重要**: パブリック Slack チャネルに送信される通知は、チムの全員が見ることができます。投稿したコンテンツの責任は投稿者が負うことに注意してください。

Slack は、クラウド・ベスのリアルタイムでのメッセジングおよび通知のシステムです。Slack が提供する永続的なチャットは、E メルの代わりに使用できる対話性に優れたチムのコラボレション手段になります。
専用チャネルまたは作業に直接関連する一連のチャネルで、チムと連絡を取ることができます。さらに、2 人以上のメンバ間で、チャネルやダイレクト・メッセジを使用して、ファイルとイメジを共有することもできます。ダイレクト・メッセジとチャネルでの通信は、検索できるように保存されます。

テストやデプロイのアクティビティなどのツルチェンに関する通知をツル統合から受信するように Slack を構成します。

1. ツルチェン作成時にこのツル統合を構成する場合は、「構成可能な統合 (Configurable Integrations)」セクションで**「Slack」**をクリックします。
1. 既存のツルチェンにこのツル統合を追加する場合は、DevOps ダッシュボドの**「ツルチェン」**ペジでそのツルチェンをクリックして「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックし、**「概要」**をクリックします。

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「Slack」**をクリックします。

1. 着信 Web フックとして Slack によって生成された Slack Web フック URL を入力します。Slack チャネルがツル統合からツルチェンに関する通知を受け取るためには Slack Web フック URL が必要です。Web フックを作成または確認する方法については、[Incoming Webhooks ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://api.slack.com/incoming-webhooks){: new_window} を参照してください。

 **ヒント:** Slack チャネルがツル統合からツルチェンについての通知を受け取れるようにするために API キを使用している場合は、代わりに Web フックを使用するように構成を更新する必要があります。

1. 通知を送信する Slack チャネルの名前を入力します。このチャネルは存在していなければならず、Slack チムでアクティブである必要があります。
1. Slack チムの URL ホスト名を入力します。これは、チム URL 内の `.slack.com` の前にある語または句です。例えば、チム URL が `https://team.slack.com` の場合、ホスト名は `team` です。
1. **「統合の作成 (Create Integration)」**をクリックします。

 **ヒント:** 指定した Slack チャネルおよびチムに到達できない場合、Slack カドに `Setup Failed` エラが表示されます。`Setup Failed` メッセジの上に移動し、**「再構成 (Reconfigure)」**をクリックしてください。Slack Web フック URL、Slack チャネル、および Slack チムの URL ホスト名に、有効な構成パラメタを使用していることを確認してください。必要に応じて設定を更新し、**「統合の保存」**をクリックします。

1. **「Slack」**をクリックします。構成した Slack チャネルでツルチェンのアクティビティをすべて表示できます。

詳しくは、[Slack ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/culture/tool_slack/){: new_window} を参照してください。


## SonarQube の構成
{: #sonarqube}

SonarQube は、ソス・コドの全体的な正常性と品質の概要を提供し、新しいコド内で見つかった問題を強調表示します。コド・アナライザは、20 を超えるコディング言語において、NULL ポインタ間接参照などの注意を要するバグ、論理エラ、リソス・リクを検出します。

以下のようにして、ソス・コドの品質を継続的に分析および測定するように SonarQube を構成します。

1. DevOps ダッシュボドから、**「ツルチェン」**をクリックします。SonarQube を追加するツルチェンをクリックします。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックします。次に、**「概要」**をクリックします。  

 a. **「ツルの追加 (Add a Tool)」**をクリックします。

 b. 「ツル統合 (Tool Integrations)」セクションで**「SonarQube」**をクリックします。

1. SonarQube ツル統合のこのインスタンスの名前を入力します。
1. ツルチェンから SonarQube カドをクリックしたときに開くようにしたい SonarQube インスタンスの URL を入力します。
1. オプション: SonarQube サバへの接続に使用するユザ名を入力します。

 **ヒント:** ユザ名の指定が必要なのは、SonarQube サバへの接続にパスワドを使用する場合のみです。接続に認証トクンを使用する場合は、このフィルドを空のままにしてください。

1. SonarQube サバへの接続に使用するパスワドまたは認証トクンを入力します。
1. **「統合の作成 (Create Integration)」**をクリックします。
1. ツルチェンから**「SonarQube」**をクリックして、接続する SonarQube インスタンスのダッシュボドを表示します。

詳しくは、[SonarQube ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/content/learn/tool_sonarqube/){: new_window} を参照してください。
