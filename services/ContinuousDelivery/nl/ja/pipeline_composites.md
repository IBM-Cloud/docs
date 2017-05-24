---

copyright:
  years: 2017
lastupdated: "2017-4-5"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 複合パイプラインでの作業 (試験段階)
{: #deliverypipeline_create_composite}

{{site.data.keyword.deliverypipeline}} の複合パイプライン・フィチャにより、関連ソフトウェア・アプリに対する反復可能な継続的統合および継続的デリバリのプロセスを管理できます。
{:shortdesc}

複合パイプラインは、ツルチェン内のアプリを管理するために作成します。{{site.data.keyword.deliverypipeline}} によってデプロイされているアプリがツルチェンに含まれている場合、ツルチェンは、Delivery Pipeline をツルチェンに追加した時、またはツルチェンから削除した時に動的に更新します。また、外部ソスから複合パイプラインにアプリを追加することもできます。

## 複合パイプラインの作成
{: #compositepipeline_create_for_toolchain}

1. Bluemix ロゴの近くのメニュから、**「サビス」>「DevOps」**をクリックします。

1. 左側のナビゲションから、**「パイプライン」**をクリックします。

2. **「詳細はこちら」**をクリックし、次に**「有効化」**をクリックして、複合パイプライン・フィチャを有効にします。複合パイプラインはユザごとに有効化されるため、作成された複合パイプラインが表示されるのは、組織内でこの試験的フィチャを選択したメンバのみになります。

2. **「作成」** > **「複合パイプライン」**をクリックします。

3. 複合パイプラインの名前を入力します。さらに、パイプラインの説明も変更できます。

4. **「ツルチェン」**リストからツルチェンを選択します。

    1. 空のツルチェンと複合パイプラインを作成するには、**「新規」**を選択します。

    2. いずれかのツルチェン用の複合パイプラインを作成するには、そのツルチェンの名前を選択します。

5. 空のツルチェンを作成したら、**「デフォルト環境の追加 (Add default environments)」**を選択します。これらのデフォルト論理環境を使用して、複合パイプラインを介したプロセス実行を制御します。

6. **「作成」**をクリックします。

構成したステジは組織内の適切なスペスに自動的にマップされ、複合パイプライン用のデプロイメント計画が作成されます。

Delivery Pipeline を含むツルチェン用の複合パイプラインを作成した場合は、そのツルチェン内のすべてのパイプラインのアプリが複合パイプラインに追加されます。Delivery Pipeline 内で構成したステジは組織内の適切なスペスに自動的にマップされ、それらの状況が表示されます。アプリ内の各ジョブの状況を表示するには、アプリを展開してください。

複合パイプライン用のデプロイメント計画も作成されます。デフォルトで、スペスのすべてのアプリのジョブは並行して実行されますが、計画内でアプリのデプロイメント順序を変更することができます。

新しいツルチェン用の複合パイプラインを作成した場合、カスタマイズ可能なデプロイメント計画が作成されます。

![各アプリを展開して、パイプライン内の各ジョブを表示](images/composite_view.png "各アプリの展開")

## デプロイメント計画の変更
{: #compositepipeline_modify_dp}

デフォルトで、複合パイプライン用のデプロイメント計画が作成されます。このデプロイメント計画は、ツルチェン内のすべての Delivery Pipeline のステジに関するすべての情報を収集します。各ステジのデプロイメント計画は表示および変更できます。

デプロイメント計画を変更するステジで、メニュをクリックし、次に**「デプロイメント計画」**をクリックします。

![デプロイメント計画を開く](images/open_deployment_plan.png "デプロイメント計画を開く")

ご使用環境のデプロイメント・タスクのリストが表示されます。

![3 つの個別のパイプラインを含む複合パイプラインのデフォルト・デプロイメント計画](images/composite_deploy_plan.png)

デプロイメント計画の変更について詳しくは、[複合パイプライン用のデプロイメント計画のカスタマイズ](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html)を参照してください。

## 個別のパイプラインの変更
{: #compositepipeline_add_job}

複合パイプラインから、個別のパイプラインを変更することができます。

1. アプリを展開します。

2. ステジのメニュから、**「構成」**をクリックします。

3. ステジに対し、ジョブの追加、変更、または削除を行います。詳しい手順については、[ジョブのステジへの追加](pipeline_build_deploy.html#deliverypipeline_add_job)を参照してください。

## 複合パイプラインでのジョブの実行
{: #compositepipeline_run_jobs}

アプリを展開してジョブを表示したら、ステジ内のすべてのジョブを手動で実行できます。アプリのスペス内の**「*ステジ* にデプロイ (Deploy to *stage*)」**アイコンをクリックします。

![単一アプリでのステジの実行](images/composite_run_stage.png)

スペス内のすべてのアプリ内のすべてのジョブを実行するには、複合パイプライン用のスペス内の**「*スペス* にデプロイ (Deploy to *space*)」**アイコンをクリックします。

![すべてのアプリでのステジの実行](images/composite_run_space.png)

ジョブは、複合青写真のデプロイメント計画に従って実行されます。

## ログの表示
{: #compositepipeline_view_logs}

ジョブのログを表示するには、そのジョブを含むアプリを展開し、ジョブをクリックします。

## IBM Bluemix DevOps Connect を使用した IBM UrbanCode Deploy との統合
{: #compositepipeline_devops_connect}

IBM Bluemix DevOps Connect は、オンプレミスの IBM&reg; UrbanCode&reg; Deploy のインストル済み環境と {{site.data.keyword.contdelivery_short}} 間の通信を調整します。DevOps Connect をインストルしたら、複合パイプラインでの IBM UrbanCode Deploy アプリの管理に使用できる統合を作成することができます。

**前提条件**

   * DevOps Connect を登録するには、IBM ID を持っている必要があります。

   * [Java&trade; Runtime Environment Version 8 Update 121 以降![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://java.com/en/download/){:new_window}がホスト・システム上にインストルされており、システム PATH 変数がそのロケションに設定されていることを確認します。

   * IBM UrbanCode Deploy からの管理許可トクンが必要です。

DevOps Connect を使用して IBM UrbanCode Deploy と統合するには、以下のステップを実行します。

1. DevOps Connect をインストルし、それを使用してユザの組織を IBM UrbanCode Deploy と統合します。

  1. 複合パイプラインで、**「アプリの追加」**をクリックします。**「管理元」**リストから、**「IBM UrbanCode Deploy」**を選択します。

  1. 統合ステップを表示します。アプリのリストが表示されたら、最初に**「アプリ」**の横の情報アイコン (![情報アイコン](/images/info.png)) をクリックし、次に**「この組織に対する IBM UrbanCode Deploy の構成 (Configure IBM UrbanCode Deploy for this organization)」**をクリックします。

  1. 「UrbanCode Deploy 統合の構成」ウィンドウで**「ダウンロド」**をクリックして DevOps Connect をダウンロドします。IBM UrbanCode Deploy にアクセスできるコンピュタ上に JAR ファイルを置きます。

  1. ウィンドウから、DevOps Connect インストル・スクリプトをコピします。このスクリプトには、DevOps Connect を開始するためのコマンドと、{{site.data.keyword.contdelivery_short}} サビスを識別するために必要な資格情報が含まれています。

  1. DevOps Connect を置いたコンピュタでコマンド・シェルを開き、コピしたスクリプトを貼り付けます。

  1. スクリプトを実行します。 DevOps Connect が始動メッセジを表示します。

1. DevOps Connect を登録します。

  1.  DevOps Connect を置いたコンピュタで、Web ブラウザを使用して DevOps Connect ダッシュボドを開きます。デフォルト URL は https://localhost:8443 です。URL を変更し、他の始動オプションの詳細を知るには、[DevOps Connect 資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/urbancode/plugindoc/urbancode-sync/ibm-urbancode-sync-utility/1-2/){:new_window} を参照してください。


1. 「IBM にサインイン」ペジに IBM ID とパスワドを入力し、**「サインイン」**をクリックします。サインインは、DevOps Connect を開始するたびに行います。

1. DevOps Connect で、IBM UrbanCode Deploy for DevOps Connect プラグインを使用して、組織と IBM UrbanCode Deploy 間の統合を作成します。

    1. 「統合」ペジで、**「新規追加」**をクリックします。

    1. **「名前」**フィルドに統合の名前を入力します。

    1. **「統合タイプ」**リストから、**「IBM UrbanCode Deploy for DevOps Connect」**を選択します。

    1. **「サバ URI」**フィルドに、IBM UrbanCode Deploy サバのパブリック URL を入力します。例えば、`https://my_UCD.example.com:8443` など。

    1. **「認証トクン」**フィルドに、IBM UrbanCode Deploy によって生成された認証トクンを入力するか貼り付けます。

    1. **「管理ユザの E メル (Admin User Email)」**フィルドに、ユザの E メル・アドレスを入力します。

    1. 統合が成功したことを確認するために、**「統合の実行」**をクリックします。DevOps Connect が、**「サバ URI」**フィルドに指定されている IBM UrbanCode Deploy インスタンスに接続します。**「認証トクン」**フィルドに貼り付けられているトクンによって DevOps Connect が許可されます。

    1. **「保存」**をクリックします。

統合が成功した場合は、IBM UrbanCode Deploy アプリを複合パイプラインに追加できます。詳細情報については、[IBM UrbanCode Deploy からのアプリの追加](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_add_apps)を参照してください。


## IBM UrbanCode Deploy からのアプリの追加
{: #compositepipeline_add_apps}

DevOps Connect を使用して IBM UrbanCode Deploy と統合されている組織のメンバは、IBM UrbanCode Deploy でアクセスできるアプリを複合パイプラインに追加できます。インストル手順については、[IBM Bluemix DevOps Connect を使用した IBM UrbanCode Deploy との統合](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_devops_connect)を参照してください。

IBM UrbanCode Deploy に接続している組織のメンバの場合、UrbanCode Deploy アプリを複合パイプラインに追加し、デプロイメント計画に組み込むアプリ・プロセスを選択し、アプリのデプロイメントをカスタマイズできます。

1. 複合パイプラインから、**「アプリの追加」**をクリックします。

2. **「管理元」**リストから、**「IBM UrbanCode Deploy」**を選択します。{{site.data.keyword.contdelivery_short}} と IBM UrbanCode Deploy との統合を最近行った場合は、サバを表示するためにブラウザの最新表示が必要な可能性があります。

3. 追加するアプリを選択し、**「続行」**をクリックします。IBM UrbanCode Deploy アプリで使用可能なすべてのアプリ・プロセスが表示されます。選択したプロセスを実行するためのエントリが、デプロイメント計画に追加されます。

4. アプリで使用するアプリ・プロセスを選択します。プロセスを見つけるには、検索オプションとフィルタ・オプションを使用します。

5. **「保存」**をクリックします。選択した各 IBM UrbanCode Deploy アプリが、複合パイプライン内のアプリとして表示されます。

6. 以下のようにして、IBM UrbanCode Deploy アプリから複合パイプラインの論理環境に環境をマップします。

    1. 論理環境名の近くのメニュから、**「論理環境の管理」**を選択します。

    ![論理環境の管理の選択](images/composite_logical_env.png)

    2. 複合パイプライン内の各アプリに対して、IBM UrbanCode Deploy に定義した環境を選択します。選択したアプリ・プロセスは、そのアプリからの環境でのみ実行されます。

    3. **「保存」**をクリックします。

    4. 使用する論理環境ごとにこれらのステップを繰り返します。
