---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-28"

---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# {{site.data.keyword.deliverypipeline}} での作業 {: #pipeline-working}

ビルドと {{site.data.keyword.Bluemix}} へのデプロイメントを自動化するには、{{site.data.keyword.Bluemix_notm}} 用の {{site.data.keyword.deliverypipeline}} を使用します。
{: shortdesc}

{{site.data.keyword.deliverypipeline}} では、いくつかのビルド・タイプから選択できます。ビルド・スクリプトを指定すれば、
{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} が実行します。ビルド・システムをセットアップする必要はありません。1 回クリックするだけで、1 つ以上の {{site.data.keyword.Bluemix_notm}} スペス、Cloud Foundry のパブリック・サバ、{{site.data.keyword.Bluemix_notm}} 用の IBM コンテナの Docker コンテナに自動的にアプリをデプロイできます。

ビルド・ジョブが、アプリのソス・コドを Git リポジトリからコンパイルしてパッケジします。ビルド・ジョブは、WAR ファイルや IBM コンテナの Docker コンテナなど、デプロイ可能な成果物を作成します。また、ビルド内で単体テストを自動的に実行することができます。コミットがプッシュされるたびにビルドがトリガされるように、ビルド・ジョブを設定することができます。

デプロイメント・ジョブは、出力をビルド・ジョブから取得して、IBM コンテナや Cloud Foundry サバ ({{site.data.keyword.Bluemix_notm}} など) にデプロイします。

1 つ以上の地域やサビスにデプロイできます。例えば、1 つ以上のサビスを使用して、1 つの地域でテストし、複数の地域で実動にデプロイするよう {{site.data.keyword.deliverypipeline}} をセットアップできます。詳しくは、[地域](/docs/overview/whatisbluemix.html#ov_intro_reg){: new_window}を参照してください。

オプン・ツルチェンで複数のパイプラインを使用する場合は、複合パイプラインを作成して、1 つの場所からすべてのパイプラインのデプロイメントを管理することができます。

パイプラインの作成にはいくつか方法があり、例えば、パイプラインを既存のアプリケションに追加する方法や、既存のアプリケションなしでパイプラインを作成する方法があります。組織に {{site.data.keyword.deliverypipeline}} サビスがまだない場合は、カタログにアクセスして、{{site.data.keyword.deliverypipeline}} をクリックし、「作成」をクリックします。

既存のアプリケションのために {{site.data.keyword.deliverypipeline}} をセットアップするには、次の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} のアプリのダッシュボドで、アプリをクリックします。
1. {{site.data.keyword.Bluemix_notm}} メニュ・バのメニュから、**「サビス」**をクリックして、**「DevOps」**をクリックします。
1. **「パイプライン」**をクリックして、 **「パイプラインの作成 (Create a Pipeline)」**をクリックします。

Cloud Foundry アプリケションをデプロイするように構成された[パイプラインを作成する ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} には、以下のステップを実行します。

1. **「Cloud Foundry」**をクリックします。
1. パイプラインに別の名前を使用する場合は、デフォルトの名前を変更します。

1. アプリケションに別の名前を使用する場合は、デフォルトの名前を変更します。この名前は、パイプラインのデプロイ先のアプリケションです。
1. ツルチェンがない場合は、デフォルトの名前が付いたツルチェンが作成されます。ツルチェンに別の名前を使用する場合は、名前を変更します。ツルチェンを使用して、他のツルやサビスと統合することで、パイプラインの機能を拡張できます。ツルチェンについて詳しくは、[ツルチェンを使用した作業](/docs/services/ContinuousDelivery/toolchains_working.html){: new_window}を参照してください。

 **ヒント**: パイプラインとツルチェンは、組織に属しています。ユザが、ツルチェンを持つ組織に属している場合は、関連付けられているツルチェンのアクセス制御リストに追加してもらうことができます。ツルチェンのアクセス制御リストに追加されると、そのツルチェンと、関連付けられたすべてのパイプラインを (たとえそれらを作成していなくても) 使用できます。ツルチェンのアクセス制御について詳しくは、[アクセスの管理](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}を参照してください。

1. 使用するツルチェンを選択するか、作成する新しいツルチェンの名前を入力します。
1. Git プロバイダを選択します。

 **ヒント**: {{site.data.keyword.Bluemix_notm}} に GitHub へのアクセスをまだ認可していない場合は、**「認可 (Authorize)」** をクリックして GitHub の Web サイトにアクセスするよう求められます。アクティブな GitHub セッションがない場合は、ログインするよう求められます。**「アプリケションを許可 (Authorize Application)」** をクリックして、{{site.data.keyword.Bluemix_notm}} が GitHub アカウントにアクセスできるようにします。アクティブな GitHub セッションはあるものの、最近パスワドを入力していない場合は、確認のために GitHub パスワドの入力を求められることがあります。

   * 既存のリポジトリを使用する場合は、リポジトリのタイプとして**「リンク (Link)」**を選択します。リポジトリの場所を検索するか、選択可能なリポジトリのリストからリポジトリを選択します。

   * 空のリポジトリを作成する場合は、リポジトリ・タイプとして**「新規」**を選択します。リポジトリの名前を入力します。

   * リポジトリのクロンを作成する場合は、リポジトリのタイプに**「コピ」**を選択します。リポジトリの場所を検索するか、選択可能なリポジトリのリストからリポジトリを選択します。

   * リポジトリをフォクし、プル・リクエストで変更内容を提供できるようにする場合は、**「フォク (Fork)」**を選択します。リポジトリの場所を検索するか、選択可能なリポジトリのリストからリポジトリを選択します。

1. リポジトリを選択するか、リポジトリの URL を入力します。
1. **「作成」**をクリックします。パイプラインが作成され、構成されて、ツルチェンの「概要」ペジに表示されます。
![パイプライン・カド](images/cd_pipeline.png)
1. 複合パイプラインを含むツルチェン内にパイプラインを作成した場合、新しいパイプラインは複合パイプラインに追加されます。デプロイメント計画を変更して、新しいパイプラインのデプロイメント・タスクを含めます。[Delivery Pipeline タスクの作成](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html#tasks_pipelineCD){: new_window}を参照してください。

事前構成されたステジのない[空のパイプライン ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} を作成するには、以下のようにします。

1. **「カスタム」**をクリックします。
1. パイプラインに別の名前を使用する場合は、デフォルトの名前を変更します。

1. ツルチェンがない場合は、デフォルトの名前が付いたツルチェンが作成されます。ツルチェンに別の名前を使用する場合は、名前を変更します。ツルチェンを使用して、他のツルやサビスと統合することで、パイプラインの機能を拡張できます。
1. 使用するツルチェンを選択するか、作成する新しいツルチェンの名前を入力します。
1. **「作成」**をクリックします。空のパイプラインが作成され、ツルチェンの「概要」ペジ上にカドとして表されます。

{{site.data.keyword.deliverypipeline}} から、構成を変更したり、ビルドのステタス、デプロイされたアプリ、最近のデプロイメントを確認したり、最新のログとデプロイメントの詳細を参照したり、パイプラインを削除したりすることができます。
