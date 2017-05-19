---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-31"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Continuous Delivery 概説
{: #cd_getting_started}

アプリケションのビルドとデプロイメントを自動化するオプン・ツルチェンが組み込まれた {{site.data.keyword.contdelivery_full}} を使用することによって、DevOps アプロチを取り入れることができます。開発、デプロイメント、運用の作業をサポトする単純なデプロイメント・ツルチェンを作成することから始めることができます。
{: shortdesc}

{{site.data.keyword.Bluemix_notm}} カタログから選択して {{site.data.keyword.contdelivery_short}} のインスタンスを作成した後、サビスにどのように取り掛かるかを選択できます。
![Continuous Delivery ウェルカム・ペジ](images/cd_landing_page.png)

 * 自動化パイプラインを使用して迅速に始めてアプリケションをデプロイするには、「パイプラインで開始 (Starting with a pipeline)」セクションで、**[「ここから開始 (Start here)](#starting_with_a_pipeline)**をクリックします。後でさらにツルを追加できます。
 * テンプレトから継続的デリバリ・ツルチェンを作成して構成するには、「ツルチェン・テンプレトから開始 (Starting from a toolchain template)」セクションで、**[「ここから開始 (Start here)」](#starting_from_a_toolchain_template)**をクリックします。ツルチェンは、パイプラインのプランニング、開発、デプロイと、アプリケションの管理のためのツルを統合したものです。ツルチェンに対していつでもツルを追加したり削除したりできます。
 * ツルチェンが既にある場合は、「ツルチェン・テンプレトから開始 (Starting from a toolchain template)」セクションで、**「ツルチェンを表示 (View your toolchains)」**をクリックします。ツルチェンの扱いについて詳しくは、[ツルチェンの使用](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}を参照してください。

**ヒント:** パイプラインはツルチェンによって管理されます。パイプラインは既存のツルチェンに追加できます。パイプラインを作成したが、既存のツルチェンがない場合は、デフォルト名のツルチェンがユザのために作成されます。ツルチェンを使用して、他のツルやサビスと統合することで、パイプラインの機能を展開できます。

##パイプラインで開始 (Starting with a pipeline)
{: #starting_with_a_pipeline}

パイプラインは、ビルドやデプロイメントなどを自動化します。自動化パイプラインを開始するには、テンプレトを選択し、GitHub リポジトリの場所を指定します。

Cloud Foundry アプリケションをデプロイするように構成された[パイプラインを作成する ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){:new_window} には、以下のステップを実行します。

1. **「Cloud Foundry」**をクリックします。
1. パイプラインに別の名前を使用する場合は、デフォルトの名前を変更します。{{site.data.keyword.Bluemix_notm}} では、パイプラインはその名前で識別されます。
1. アプリケションに別の名前を使用する場合は、デフォルトの名前を変更します。{{site.data.keyword.Bluemix_notm}} では、アプリケションはその名前で識別されます。この名前は、パイプラインのデプロイ先のアプリケションです。
1. ツルチェンがない場合は、デフォルトの名前が付いたツルチェンが作成されます。ツルチェンに別の名前を使用する場合は、名前を変更します。パイプラインはツルチェンによって管理されます。ツルチェンを使用して、他のツルやサビスと統合することで、パイプラインの機能を拡張できます。

 **ヒント**: パイプラインとツルチェンは、組織に属しています。ツルチェンを持つ組織に属していれば、これらのツルチェンの作成者でなくても使用することができます。

1. 使用するツルチェンを選択するか、作成する新しいツルチェンの名前を入力します。
1. Git プロバイダを選択します。

 **ヒント**: {{site.data.keyword.Bluemix_notm}} に GitHub へのアクセスをまだ認可していない場合は、**「認可 (Authorize)」** をクリックして GitHub の Web サイトにアクセスするよう求められます。アクティブな GitHub セッションがない場合は、ログインするよう求められます。**「アプリケションを許可 (Authorize Application)」** をクリックして、{{site.data.keyword.Bluemix_notm}} が GitHub アカウントにアクセスできるようにします。アクティブな GitHub セッションはあるものの、最近パスワドを入力していない場合は、確認のために GitHub パスワドの入力を求められることがあります。

 {{site.data.keyword.ghe_short}} リポジトリへのアクセスを許可されていない場合は、リポジトリの管理特権を持つユザに依頼して追加してもらう必要があります。{{site.data.keyword.Bluemix_notm}} Dedicated for {{site.data.keyword.ghe_short}} での許可の説明については、[{{site.data.keyword.Bluemix_notm}} Dedicated for {{site.data.keyword.ghe_short}} 入門](/docs/services/ghededicated/index.html){: new_window}を参照してください。ユザ自身が管理する {{site.data.keyword.ghe_short}} のバジョンで許可する必要がある場合は、内部プロシジャに従ってください。

   * 既存のリポジトリを使用する場合は、リポジトリのタイプとして**「リンク (Link)」**を選択します。リポジトリの場所を検索するか、選択可能なリポジトリのリストからリポジトリを選択します。

   * 空のリポジトリを作成する場合は、リポジトリ・タイプとして**「新規」**を選択します。リポジトリの名前を入力します。

   * リポジトリのクロンを作成する場合は、リポジトリのタイプに**「コピ」**を選択します。リポジトリの場所を検索するか、選択可能なリポジトリのリストからリポジトリを選択します。

   * リポジトリをフォクし、プル・リクエストで変更内容を提供できるようにする場合は、**「フォク (Fork)」**を選択します。リポジトリの場所を検索するか、選択可能なリポジトリのリストからリポジトリを選択します。

1. リポジトリを選択するか、リポジトリの URL を入力します。
1. **「作成」**をクリックします。 パイプラインが作成され、構成されて、ツルチェンの「概要」ペジに表示されます。
![パイプライン・カド](images/cd_pipeline.png)

事前構成されたステジのない[空のパイプライン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} を作成するには、以下のようにします。

1. **「カスタム」**をクリックします。
1. パイプラインに別の名前を使用する場合は、デフォルトの名前を変更します。{{site.data.keyword.Bluemix_notm}} では、パイプラインはその名前で識別されます。
1. ツルチェンがない場合は、デフォルトの名前が付いたツルチェンが作成されます。ツルチェンに別の名前を使用する場合は、名前を変更します。パイプラインはツルチェンによって管理されます。ツルチェンを使用して、他のツルやサビスと統合することで、パイプラインの機能を拡張できます。
1. 使用するツルチェンを選択するか、作成する新しいツルチェンの名前を入力します。
1. **「作成」**をクリックします。 空のパイプラインが作成され、ツルチェンの「概要」ペジ上にカドとして表されます。

##ツルチェン・テンプレトから開始 (Starting from a toolchain template)
{: #starting_from_a_toolchain_template}

[テンプレト ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン icon")](https://console.ng.bluemix.net/devops/create){: new_window} から継続的デリバリ・ツルチェンを作成して構成するには、以下のようにします。

1. **「ツルチェンの作成 (Create a Toolchain)」**ペジで、ツルチェン・テンプレトをクリックします。  
1. 作成しようとしているツルチェンの図を確認します。この図は、ツルチェン内の各ツル統合とそのライフサイクル・フェズを示しています。

 **ヒント**: 一部のツルチェン・テンプレトには、同じツル統合の複数のインスタンスが含まれています。例えば、{{site.data.keyword.Bluemix_notm}} Public の Microservices ツルチェン・テンプレトには、GitHub の 3 つのインスタンスと Delivery Pipeline の 3 つのインスタンス (3 つのマイクロサビスのそれぞれに対して 1 つずつ) が含まれています。

 次のイメジの図はその例です。ツルチェンを作成すると、ツルチェンを構成する各ツル統合がこの図に表示されます。
![ツルチェンの図](images/toolchain_diagram.png)
1. ツルチェン設定のデフォルト情報を確認します。ツルチェンの名前は、そのツルチェンを {{site.data.keyword.Bluemix_notm}} 内で識別するためのものです。別の名前を使用する場合は、ツルチェンの名前を変更します。
1. 「ツル統合 (Tool Integrations)」セクションで、ツルチェンに構成する各ツル統合を選択します。いくつかのツル統合は、構成を必要としません。ツル統合の構成については、[ツル統合の構成](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}を参照してください。
1. **「作成」**をクリックします。 以下のようにいくつかのステップが自動的に実行されて、ツルチェンがセットアップされます。セットアップされるツル統合は、どのツルチェン・テンプレトを選択したのか、また、{{site.data.keyword.Bluemix_notm}} Public と {{site.data.keyword.Bluemix_notm}} Dedicated のどちらを使用しているのかによって異なります。例えば、Microservices ツルチェンを {{site.data.keyword.Bluemix_notm}} Public で作成する場合、以下のステップが実行されます。

 * ツルチェンが作成されます。
 * Delivery Pipeline を構成した場合は、パイプラインが作成されて実行します。
 * Sauce Labs を構成した場合は、パイプラインに Sauce Labs テスト・ジョブを追加するようにツルチェンがセットアップされます。
 * PagerDuty を構成した場合は、指定した PagerDuty サビスにアラト通知を送信するようにツルチェンがセットアップされます。
 * Slack を構成した場合は、指定した Slack チャネルにデプロイメント状況に関する通知を送信するようにツルチェンがセットアップされます。
 * GitHub などのソス・コド・ツル統合を構成した場合、サンプル GitHub リポジトリが GitHub アカウントに複製されます。
