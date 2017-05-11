---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-4"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Continuous Delivery について  
{: #cd_about}  

{{site.data.keyword.contdelivery_full}} は、DevOps プラクティスや業界最高レベルのツールを使用したアプリケーションのビルド、テスト、デリバリーを可能にします。
{:shortdesc}

{{site.data.keyword.contdelivery_short}} サービスは、以下の DevOps ワークフローをサポートします。

 * 統合された DevOps のオープン・[ツールチェーン](/docs/services/ContinuousDelivery/toolchains_about.html){: new_window}を作成して、開発、デプロイメント、および運用の各タスクをサポートするツール統合を可能にできます。

  ツールチェーンは統合されたツールのセットで、アプリケーションを共同で開発、ビルド、デプロイ、テスト、管理するのに使用できます。{{site.data.keyword.Bluemix_notm}} サービス、オープン・ソースのツール、サード・パーティーのツール (GitHub、PagerDuty、Slack など) を含むツールチェーンを作成して、開発や運用を反復可能にしたり、管理しやすくしたりできます。

 * 自動化された[パイプライン](/docs/services/ContinuousDelivery/pipeline_about.html){: new_window}を使用すれば、継続的なデリバリーが可能になります。

  ビルド、単体テスト、デプロイメントなどを自動化します。最小限の人的介入で、反復可能な方法でビルド、テスト、デプロイします。いつでも実稼動環境で使用できるよう準備します。

 * [Web ベースの IDE](/docs/services/ContinuousDelivery/web_ide.html){: new_window} を使用して、どこからでもコードを編集してプッシュします。

  GitHub でソース管理のタスクの作成、編集、実行、デバッグ、完成を行えます。コードの編集から実稼動環境へのデプロイに、シームレスに移ります。

 * [{{site.data.keyword.DRA_short}}](/docs/services/ContinuousDelivery/di_working.html){: new_window} により品質を改善します。

  チームのコード開発とデリバリーの動態について理解します。ユーザーとアプリケーションが相互作用する方法について学びます。データを検討して、アプリケーションの運用の管理に役立てます。


## Bluemix Public と Bluemix Dedicated でのツールチェーンの可用性の比較
{: #public_and_dedicated}

{{site.data.keyword.Bluemix_notm}} Public は、[http://bluemix.net ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://bluemix.net){:new_window} によってアクセスされるアプリケーションを構築、実行、および管理するための、オープン・スタンダードのクラウド・ベース・プラットフォームです。{{site.data.keyword.Bluemix_notm}} Dedicated は、{{site.data.keyword.Bluemix_notm}} Public 環境とユーザーのネットワークの両方に安全に接続される専用 SoftLayer 環境で {{site.data.keyword.Bluemix_notm}} の機能を提供します。ユーザーの会社の {{site.data.keyword.Bluemix_notm}} Dedicated 環境には、{{site.data.keyword.Bluemix_notm}} Public サイトと同じツール統合が含まれていない可能性があります。

ソース・コード管理と問題のトラッキングについて、{{site.data.keyword.Bluemix_notm}} Public では一般に github.com が使用されます。{{site.data.keyword.Bluemix_notm}} Dedicated でも github.com の使用は可能ですが、通常は、ユーザーの会社によってインストールされたか、IBM によって管理されている {{site.data.keyword.ghe_short}} が使用されます。

{{site.data.keyword.contdelivery_short}} は、{{site.data.keyword.Bluemix_notm}} Public と {{site.data.keyword.Bluemix_notm}} Dedicated で使用可能です。ツールチェーンは、{{site.data.keyword.contdelivery_short}} を {{site.data.keyword.Bluemix_notm}} Public で使用しているか、それとも {{site.data.keyword.Bluemix_notm}} Dedicated で使用しているかによって異なります。

|ツールチェーン |{{site.data.keyword.Bluemix_notm}} Public	|{{site.data.keyword.Bluemix_notm}} Dedicated |
|:----------|:------------------------------|:------------------|
|ツール統合 		|サポートされているツール統合のリストについては、[ツール統合の構成](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}を参照してください。 		|使用可能なツール統合は、ご使用環境での {{site.data.keyword.contdelivery_short}} のセットアップ方法によって決まります。			|
|テンプレートからのツールチェーンの作成		|[{{site.data.keyword.Bluemix_notm}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://console.ng.bluemix.net/devops){:new_window} にログインします。		|{{site.data.keyword.Bluemix_notm}} 上の Dedicated 環境にログインします。			|
|アプリからのツールチェーンの作成		|アプリ・スターター・コードが取り込まれた新規 GitHub リポジトリーからアプリの継続的デリバリーが構成されます。		|アプリ・スターター・コードが取り込まれた新規 GitHub または GitHub Enterprise リポジトリーからアプリの継続的デリバリーが構成されます。		|  
|Delivery Pipeline のデプロイメント領域		|すべての {{site.data.keyword.Bluemix_notm}} Public 領域が Cloud Foundry デプロイメント・ジョブで使用可能です。 		|{{site.data.keyword.Bluemix_notm}} Dedicated 領域が使用可能です。特定の環境内での {{site.data.keyword.contdelivery_short}} のセットアップ方法に応じて、同じカスタマー・アカウント内のその他の Dedicated 領域または Local 領域も使用可能な可能性があります。		|
|Delivery Pipeline のデプロイメント・ジョブ		|すべての[ジョブ・タイプ](/docs/services/ContinuousDelivery/pipeline_about.html#deliverypipeline_jobs)が使用可能です。		|Dedicated 環境にインストールされていない {{site.data.keyword.Bluemix_notm}} サービスに依存するジョブ・タイプは、使用可能でない可能性があります。例えば、コンテナー・ビルドとコンテナー・デプロイのジョブ・タイプは、{{site.data.keyword.Bluemix_notm}} Container サービスがインストールされていない環境では使用できない可能性があります。	|
{: caption="Table 1. Differences between toolchains on {{site.data.keyword.Bluemix_notm}} Dedicated and {{site.data.keyword.Bluemix_notm}} Public" caption-side="top"}


## ツールチェーン・テンプレート
{: #templates}

[ツールチェーンを作成![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/create){: new_window}するための開始点としてテンプレートを使用することができます。ツールチェーン・テンプレートは、開発、デプロイメント、および運用の各タスクをサポートする特定のツール統合セットを含んでいます。

**ヒント**: ユーザーの会社の {{site.data.keyword.Bluemix_notm}} Dedicated 環境は、{{site.data.keyword.Bluemix_notm}} Public サイトと同じツールチェーン・テンプレートを含んでいない可能性があります。{{site.data.keyword.Bluemix_notm}} Public と {{site.data.keyword.Bluemix_notm}} Dedicated の両方で使用可能なツールチェーン・テンプレートは、{{site.data.keyword.Bluemix_notm}} Dedicated 上では異なるツール統合セットを含んでいる可能性があります。

一部のツールチェーン・テンプレートには、{{site.data.keyword.contdelivery_short}} サービスの一部であるツール統合が組み込まれています。そのサービスのインスタンスがまだ組織にない場合は、**「作成」**をクリックしてツールチェーンを作成した時に、無料で自動的にサービスが追加されます。詳細情報とご利用条件については、[Bluemix カタログ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/catalog/services/continuous-delivery/){:new_window}を参照してください。

Microservices ツールチェーン・テンプレートは、Cloudant ストアによって支持されている Catalog API と Orders API を使用してアプリをデプロイします。アプリのデプロイの一部として、無料の Cloudant サービス・インスタンスが作成されます。詳細情報とご利用条件については、[Bluemix カタログ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/catalog/services/cloudant-nosql-db/){:new_window}を参照してください。

|テンプレート |説明	|
|:----------|:------------------------------|
|[Garage Method cloud-native tutorial toolchain![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fcloud-native-toolchain-tutorial){:new_window} 		|このツールチェーンは、Garage Method での特徴である DevOps プラクティスを示します。このツールチェーンは、継続的デリバリー、ソース管理、テストの自動化、および自動化されたモニタリングと運用について事前構成されています。このツールチェーンには、Node.js Express 4 で作成されたサンプル・アプリが付属しており、このアプリはさらなる拡張が可能です。 		|
|[Microservices toolchain with {{site.data.keyword.DRA_short}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Ftoolchain-demo){:new_window} 		|このクラウド・ネイティブ・ツールチェーンでは、サンプルを使用して、3 つのマイクロサービス (Catalog API、Orders API、および両方の API を呼び出す UI) からなるオンライン・ストアを作成することができます。このツールチェーンは、継続的デリバリー、ソース管理、機能テスト、問題のトラッキング、オンライン編集、およびアラート通知用に事前構成されています。 		|
|[Microservices toolchain with {{site.data.keyword.DRA_short}} (v2) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fmicroservices-toolchain-hosted){:new_window} 		|このクラウド・ネイティブ・ツールチェーンでは、サンプルを使用して、3 つのマイクロサービス (Catalog API、Orders API、および両方の API を呼び出す UI) からなるオンライン・ストアを作成することができます。このツールチェーンは、継続的デリバリー、ソース管理、機能テスト、問題のトラッキング、オンライン編集、およびアラート通知用に事前構成されています。 		|
|[Secure container toolchain ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsecure-container-toolchain){:new_window} 		|このツールチェーンを使用すると、セキュアな Docker コンテナー・アプリを開発およびデプロイできます。デフォルトで、このツールチェーンではサンプル Node.js の「Hello World」アプリが使用されますが、代わりにユーザー独自の GitHub リポジトリーにリンクすることもできます。このツールチェーンは、脆弱性アドバイザーを使用した継続的デリバリー、ソース管理、問題のトラッキング、およびオンライン編集用に事前構成されています。 		|
|[Simple Cloud Foundry toolchain ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain){:new_window}		|このツールチェーンを使用すると、Cloud Foundry アプリを開発およびデプロイできます。デフォルトで、このツールチェーンではサンプル Node.js の「Hello world」アプリが使用されますが、代わりにユーザー独自の GitHub リポジトリーにリンクすることもできます。このツールチェーンは、継続的デリバリー、ソース管理、問題のトラッキング、およびオンライン編集用に事前構成されています。 		|
|[Simple Cloud Foundry toolchain	(v2) ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-toolchain-hosted){:new_window}	|このツールチェーンを使用すると、Cloud Foundry アプリを開発およびデプロイできます。デフォルトで、このツールチェーンではサンプル Node.js の「Hello World」アプリが、IBM がホストする Git リポジトリーに複製されます。複製されたアプリは後から変更できます。このツールチェーンは、継続的デリバリー、ソース管理、問題のトラッキング、およびオンライン編集用に事前構成されています。 		|
|[Simple Cloud Foundry toolchain with {{site.data.keyword.DRA_short}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdra-toolchain-demo){:new_window}		|このクラウド・ネイティブ・ツールチェーンでは、{{site.data.keyword.DRA_short}} を使用してシンプルな Cloud Foundry アプリのデプロイメントをゲート制御できます。デフォルトで、このツールチェーンではサンプル Node.js 気象アプリが使用されます。あるいは、ユーザー独自の GitHub リポジトリーにリンクすることもできます。 		|
|[Simple Container toolchain ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fsimple-container-toolchain){:new_window}		|このツールチェーンを使用すると、Docker コンテナー・アプリを開発およびデプロイできます。デフォルトで、このツールチェーンではサンプル Node.js の「Hello World」アプリが使用されますが、代わりにユーザー独自の GitHub リポジトリーにリンクすることもできます。このツールチェーンは、継続的デリバリー、ソース管理、問題のトラッキング、およびオンライン編集用に事前構成されています。 		|
|[Delivery Insights with IBM UrbanCode Deploy ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdeliveryinsights-toolchain){:new_window}		|このツールチェーンを使用すると、IBM UrbanCode Deploy からデプロイメント・メトリックを表示できます。{{site.data.keyword.DRA_short}} の「設定」ページから DevOps Connect をダウンロードして構成することにより IBM UrbanCode Deploy と通信するには、このツールチェーンを使用可能にします。 		|
|[Deployment Risk Analytics with GitHub and Jenkins ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevopsinsights-toolchain){:new_window}		|このツールチェーンを使用すると、継続的統合および継続的デリバリーのための Jenkins プロセスについての洞察を得ることができます。Jenkins サーバーを構成して、Jenkins によってジョブが実行されている時に {{site.data.keyword.DRA_short}} にデータを送信することができます。また、品質ゲートを実装して、ポリシーに基づいてデプロイメントをブロックすることもできます。結果は、{{site.data.keyword.DRA_short}} の「デプロイメント・リスク」ダッシュボードで見ることができます。Jenkins で使用されているソース・リポジトリーを示すように GitHub リポジトリーを構成すると、変更トレーサビリティーが使用可能になります。  		|
|[Developer Insights and Team Dynamics with GitHub and JIRA ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fdevteaminsights-toolchain){:new_window}		|このツールチェーンを使用すると、プロジェクトの開発リスクを探り、ソーシャル・コーディング分析を使用して開発者間の対話パターンを理解することができます。GitHub のソース・コードを、GitHub の問題、JIRA の問題、またはそれら両方と併せて分析できます。Developer Insights を使用して、非常にエラーが発生しやすいファイルを識別し、プロジェクトがどのように DevOps プラクティスに従っているか確認します。Team Dynamics のソーシャル・コーディング分析は、チームが非生産的なプラクティスを修正できるように、チーム・メンバー間の対話レベルを識別します。 		|
|[Build your own toolchain ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/setup/deploy?repository=https%3A%2F%2Fgithub.com%2Fopen-toolchain%2Fempty-toolchain){:new_window}		|このツールチェーンには、事前構成されたツールは含まれていません。ツールチェーンを既に熟知している場合、独自のツールチェーンをセットアップできます。 		|
{: caption="Table 2. Toolchain templates" caption-side="top"}
