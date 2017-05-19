---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Continuous Delivery について  
{: #cd_about}  

{{site.data.keyword.contdelivery_full}} は、DevOps プラクティスや業界最高レベルのツルを使用したアプリケションのビルド、テスト、デリバリを可能にします。
{:shortdesc}

{{site.data.keyword.contdelivery_short}} サビスは、以下の DevOps ワクフロをサポトします。

 * 統合された DevOps のオプン・[ツルチェン](/docs/services/ContinuousDelivery/toolchains_about.html){: new_window}を作成して、開発、デプロイメント、および運用の各タスクをサポトするツル統合を可能にできます。

  ツルチェンは統合されたツルのセットで、アプリケションを共同で開発、ビルド、デプロイ、テスト、管理するのに使用できます。{{site.data.keyword.Bluemix_notm}} サビス、オプン・ソスのツル、サド・パティのツル (GitHub、PagerDuty、Slack など) を含むツルチェンを作成して、開発や運用を反復可能にしたり、管理しやすくしたりできます。

 * 自動化された[パイプライン](/docs/services/ContinuousDelivery/pipeline_about.html){: new_window}を使用すれば、継続的なデリバリが可能になります。

  ビルド、単体テスト、デプロイメントなどを自動化します。最小限の人的介入で、反復可能な方法でビルド、テスト、デプロイします。いつでも実稼動環境で使用できるよう準備します。

 * [Web ベスの IDE](/docs/services/ContinuousDelivery/web_ide.html){: new_window} を使用して、どこからでもコドを編集してプッシュします。

  GitHub でソス管理のタスクの作成、編集、実行、デバッグ、完成を行えます。コドの編集から実稼動環境へのデプロイに、シムレスに移ります。

 * [{{site.data.keyword.DRA_short}}](/docs/services/ContinuousDelivery/di_working.html){: new_window} により品質を改善します。

  チムのコド開発とデリバリの動態について理解します。ユザとアプリケションが相互作用する方法について学びます。デタを検討して、アプリケションの運用の管理に役立てます。


## Bluemix Public と Bluemix Dedicated でのツルチェンの可用性の比較
{: #public_and_dedicated}

{{site.data.keyword.Bluemix_notm}} Public は、[http://bluemix.net ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://bluemix.net){:new_window} によってアクセスされるアプリケションを構築、実行、および管理するための、オプン・スタンダドのクラウド・ベス・プラットフォムです。{{site.data.keyword.Bluemix_notm}} Dedicated は、{{site.data.keyword.Bluemix_notm}} Public 環境とユザのネットワクの両方に安全に接続される専用 SoftLayer 環境で {{site.data.keyword.Bluemix_notm}} の機能を提供します。ユザの会社の {{site.data.keyword.Bluemix_notm}} Dedicated 環境には、{{site.data.keyword.Bluemix_notm}} Public サイトと同じツル統合が含まれていない可能性があります。

ソス・コド管理と問題のトラッキングについて、{{site.data.keyword.Bluemix_notm}} Public では一般に github.com が使用されます。{{site.data.keyword.Bluemix_notm}} Dedicated でも github.com の使用は可能ですが、通常は、ユザの会社によってインストルされたか、IBM によって管理されている {{site.data.keyword.ghe_short}} が使用されます。

{{site.data.keyword.contdelivery_short}} は、{{site.data.keyword.Bluemix_notm}} Public と {{site.data.keyword.Bluemix_notm}} Dedicated で使用可能です。ツルチェンは、{{site.data.keyword.contdelivery_short}} を {{site.data.keyword.Bluemix_notm}} Public で使用しているか、それとも {{site.data.keyword.Bluemix_notm}} Dedicated で使用しているかによって異なります。

**ヒント**: ツルチェンは米国南部地域でのみホストされます。異なる地域にアプリをデプロイするようにツルチェンが構成されている場合でも、アプリは前述の地域にデプロイされます。

|ツルチェン |{{site.data.keyword.Bluemix_notm}} Public	|{{site.data.keyword.Bluemix_notm}} Dedicated |
|:----------|:------------------------------|:------------------|
|ツル統合 		|サポトされているツル統合のリストについては、[ツル統合の構成](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}を参照してください。 		|使用可能なツル統合は、ご使用環境での {{site.data.keyword.contdelivery_short}} のセットアップ方法によって決まります。			|
|テンプレトからのツルチェンの作成		|[{{site.data.keyword.Bluemix_notm}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://console.ng.bluemix.net/devops){:new_window} にログインします。		|{{site.data.keyword.Bluemix_notm}} 上の Dedicated 環境にログインします。			|
|アプリからのツルチェンの作成		|アプリ・スタタ・コドが取り込まれた新規 GitHub リポジトリからアプリの継続的デリバリが構成されます。		|アプリ・スタタ・コドが取り込まれた新規 GitHub または GitHub Enterprise リポジトリからアプリの継続的デリバリが構成されます。		|  
|Delivery Pipeline のデプロイメント領域		|すべての {{site.data.keyword.Bluemix_notm}} Public 領域が Cloud Foundry デプロイメント・ジョブで使用可能です。 		|{{site.data.keyword.Bluemix_notm}} Dedicated 領域が使用可能です。特定の環境内での {{site.data.keyword.contdelivery_short}} のセットアップ方法に応じて、同じカスタマ・アカウント内のその他の Dedicated 領域または Local 領域も使用可能な可能性があります。		|
|Delivery Pipeline のデプロイメント・ジョブ		|すべての[ジョブ・タイプ](/docs/services/ContinuousDelivery/pipeline_about.html#deliverypipeline_jobs)が使用可能です。		|Dedicated 環境にインストルされていない {{site.data.keyword.Bluemix_notm}} サビスに依存するジョブ・タイプは、使用可能でない可能性があります。例えば、コンテナ・ビルドとコンテナ・デプロイのジョブ・タイプは、{{site.data.keyword.Bluemix_notm}} Container サビスがインストルされていない環境では使用できない可能性があります。	|
{: caption="表 1. Bluemix Dedicated と Bluemix Public のツルチェンの違い" caption-side="top"}


## ツルチェン・テンプレト
{: #templates}

[ツルチェンを作成![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/create){: new_window}するための開始点としてテンプレトを使用することができます。ツルチェン・テンプレトは、開発、デプロイメント、および運用の各タスクをサポトする特定のツル統合セットを含んでいます。

**ヒント**: ユザの会社の {{site.data.keyword.Bluemix_notm}} Dedicated 環境は、{{site.data.keyword.Bluemix_notm}} Public サイトと同じツルチェン・テンプレトを含んでいない可能性があります。{{site.data.keyword.Bluemix_notm}} Public と {{site.data.keyword.Bluemix_notm}} Dedicated の両方で使用可能なツルチェン・テンプレトは、{{site.data.keyword.Bluemix_notm}} Dedicated 上では異なるツル統合セットを含んでいる可能性があります。

一部のツルチェン・テンプレトには、{{site.data.keyword.contdelivery_short}} サビスの一部であるツル統合が組み込まれています。そのサビスのインスタンスがまだ組織にない場合は、**「作成」**をクリックしてツルチェンを作成した時に、無料で自動的にサビスが追加されます。詳細情報とご利用条件については、[Bluemix カタログ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/catalog/services/continuous-delivery/){:new_window}を参照してください。

Microservices ツルチェン・テンプレトは、Cloudant ストアによって支持されている Catalog API と Orders API を使用してアプリをデプロイします。アプリのデプロイの一部として、無料の Cloudant サビス・インスタンスが作成されます。詳細情報とご利用条件については、[Bluemix カタログ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db/){:new_window}を参照してください。

|テンプレト |説明	|
|:----------|:------------------------------|
|[Garage Method cloud-native tutorial toolchain![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fcloud-native-toolchain-tutorial){:new_window} 		|このツルチェンは、Garage Method での特徴である DevOps プラクティスを示します。このツルチェンは、継続的デリバリ、ソス管理、テストの自動化、および自動化されたモニタリングと運用について事前構成されています。このツルチェンには、Node.js Express 4 で作成されたサンプル・アプリが付属しており、このアプリはさらなる拡張が可能です。 		|
|[Microservices toolchain with {{site.data.keyword.DRA_short}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Ftoolchain-demo){:new_window} 		|このクラウド・ネイティブ・ツルチェンでは、サンプルを使用して、3 つのマイクロサビス (Catalog API、Orders API、および両方の API を呼び出す UI) からなるオンライン・ストアを作成することができます。このツルチェンは、継続的デリバリ、ソス管理、機能テスト、問題のトラッキング、オンライン編集、およびアラト通知用に事前構成されています。 		|
|[Microservices toolchain with {{site.data.keyword.DRA_short}} (v2) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fmicroservices-toolchain-hosted){:new_window} 		|このクラウド・ネイティブ・ツルチェンでは、サンプルを使用して、3 つのマイクロサビス (Catalog API、Orders API、および両方の API を呼び出す UI) からなるオンライン・ストアを作成することができます。このツルチェンは、継続的デリバリ、ソス管理、機能テスト、問題のトラッキング、オンライン編集、およびアラト通知用に事前構成されています。 		|
|[Secure container toolchain ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsecure-container-toolchain){:new_window} 		|このツルチェンを使用すると、セキュアな Docker コンテナ・アプリを開発およびデプロイできます。デフォルトで、このツルチェンではサンプル Node.js の「Hello World」アプリが使用されますが、代わりにユザ独自の GitHub リポジトリにリンクすることもできます。このツルチェンは、脆弱性アドバイザを使用した継続的デリバリ、ソス管理、問題のトラッキング、およびオンライン編集用に事前構成されています。 		|
|[Simple Cloud Foundry toolchain ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain){:new_window}		|このツルチェンを使用すると、Cloud Foundry アプリを開発およびデプロイできます。デフォルトで、このツルチェンではサンプル Node.js の「Hello world」アプリが使用されますが、代わりにユザ独自の GitHub リポジトリにリンクすることもできます。このツルチェンは、継続的デリバリ、ソス管理、問題のトラッキング、およびオンライン編集用に事前構成されています。 		|
|[Simple Cloud Foundry toolchain	(v2) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain-hosted){:new_window}	|このツルチェンを使用すると、Cloud Foundry アプリを開発およびデプロイできます。デフォルトで、このツルチェンではサンプル Node.js の「Hello World」アプリが、IBM がホストする Git リポジトリに複製されます。複製されたアプリは後から変更できます。このツルチェンは、継続的デリバリ、ソス管理、問題のトラッキング、およびオンライン編集用に事前構成されています。 		|
|[Simple Cloud Foundry toolchain with {{site.data.keyword.DRA_short}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdra-toolchain-demo){:new_window}		|このクラウド・ネイティブ・ツルチェンでは、{{site.data.keyword.DRA_short}} を使用してシンプルな Cloud Foundry アプリのデプロイメントをゲト制御できます。デフォルトで、このツルチェンではサンプル Node.js 気象アプリが使用されます。あるいは、ユザ独自の GitHub リポジトリにリンクすることもできます。 		|
|[Simple Container toolchain ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-container-toolchain){:new_window}		|このツルチェンを使用すると、Docker コンテナ・アプリを開発およびデプロイできます。デフォルトで、このツルチェンではサンプル Node.js の「Hello World」アプリが使用されますが、代わりにユザ独自の GitHub リポジトリにリンクすることもできます。このツルチェンは、継続的デリバリ、ソス管理、問題のトラッキング、およびオンライン編集用に事前構成されています。 		|
|[Delivery Insights with IBM UrbanCode Deploy ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdeliveryinsights-toolchain){:new_window}		|このツルチェンを使用すると、IBM UrbanCode Deploy からデプロイメント・メトリックを表示できます。{{site.data.keyword.DRA_short}} の「設定」ペジから DevOps Connect をダウンロドして構成することにより IBM UrbanCode Deploy と通信するには、このツルチェンを使用可能にします。 		|
|[Deployment Risk Analytics with GitHub and Jenkins ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevopsinsights-toolchain){:new_window}		|このツルチェンを使用すると、継続的統合および継続的デリバリのための Jenkins プロセスについての洞察を得ることができます。Jenkins サバを構成して、Jenkins によってジョブが実行されている時に {{site.data.keyword.DRA_short}} にデタを送信することができます。また、品質ゲトを実装して、ポリシに基づいてデプロイメントをブロックすることもできます。結果は、{{site.data.keyword.DRA_short}} の「デプロイメント・リスク」ダッシュボドで見ることができます。Jenkins で使用されているソス・リポジトリを示すように GitHub リポジトリを構成すると、変更トレサビリティが使用可能になります。  		|
|[Developer Insights and Team Dynamics with GitHub and JIRA ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevteaminsights-toolchain){:new_window}		|このツルチェンを使用すると、プロジェクトの開発リスクを探り、ソシャル・コディング分析を使用して開発者間の対話パタンを理解することができます。GitHub のソス・コドを、GitHub の問題、JIRA の問題、またはそれら両方と併せて分析できます。Developer Insights を使用して、非常にエラが発生しやすいファイルを識別し、プロジェクトがどのように DevOps プラクティスに従っているか確認します。Team Dynamics のソシャル・コディング分析は、チムが非生産的なプラクティスを修正できるように、チム・メンバ間の対話レベルを識別します。 		|
|[Build your own toolchain ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fempty-toolchain){:new_window}		|このツルチェンには、事前構成されたツルは含まれていません。ツルチェンを既に熟知している場合、独自のツルチェンをセットアップできます。 		|
{: caption="表 2. ツルチェン・テンプレト" caption-side="top"}
