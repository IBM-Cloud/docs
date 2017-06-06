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

{{site.data.keyword.deliverypipeline}} の複合パイプライン・フィーチャーにより、関連ソフトウェア・アプリに対する反復可能な継続的統合および継続的デリバリーのプロセスを管理できます。
{:shortdesc}

複合パイプラインは、ツールチェーン内のアプリを管理するために作成します。{{site.data.keyword.deliverypipeline}} によってデプロイされているアプリがツールチェーンに含まれている場合、ツールチェーンは、Delivery Pipeline をツールチェーンに追加した時、またはツールチェーンから削除した時に動的に更新します。また、外部ソースから複合パイプラインにアプリを追加することもできます。

## 複合パイプラインの作成
{: #compositepipeline_create_for_toolchain}

1. Bluemix ロゴの近くのメニューから、**「サービス」>「DevOps」**をクリックします。

1. 左側のナビゲーションから、**「パイプライン」**をクリックします。

2. **「詳細はこちら」**をクリックし、次に**「有効化」**をクリックして、複合パイプライン・フィーチャーを有効にします。複合パイプラインはユーザーごとに有効化されるため、作成された複合パイプラインが表示されるのは、組織内でこの試験的フィーチャーを選択したメンバーのみになります。

2. **「作成」** > **「複合パイプライン」**をクリックします。

3. 複合パイプラインの名前を入力します。さらに、パイプラインの説明も変更できます。

4. **「ツールチェーン」**リストからツールチェーンを選択します。

    1. 空のツールチェーンと複合パイプラインを作成するには、**「新規」**を選択します。

    2. いずれかのツールチェーン用の複合パイプラインを作成するには、そのツールチェーンの名前を選択します。

5. 空のツールチェーンを作成したら、**「デフォルト環境の追加 (Add default environments)」**を選択します。これらのデフォルト論理環境を使用して、複合パイプラインを介したプロセス実行を制御します。

6. **「作成」**をクリックします。

構成したステージは組織内の適切なスペースに自動的にマップされ、複合パイプライン用のデプロイメント計画が作成されます。

Delivery Pipeline を含むツールチェーン用の複合パイプラインを作成した場合は、そのツールチェーン内のすべてのパイプラインのアプリが複合パイプラインに追加されます。Delivery Pipeline 内で構成したステージは組織内の適切なスペースに自動的にマップされ、それらの状況が表示されます。アプリ内の各ジョブの状況を表示するには、アプリを展開してください。

複合パイプライン用のデプロイメント計画も作成されます。デフォルトで、スペースのすべてのアプリのジョブは並行して実行されますが、計画内でアプリのデプロイメント順序を変更することができます。

新しいツールチェーン用の複合パイプラインを作成した場合、カスタマイズ可能なデプロイメント計画が作成されます。

![各アプリを展開して、パイプライン内の各ジョブを表示](images/composite_view.png "各アプリの展開")

## デプロイメント計画の変更
{: #compositepipeline_modify_dp}

デフォルトで、複合パイプライン用のデプロイメント計画が作成されます。このデプロイメント計画は、ツールチェーン内のすべての Delivery Pipeline のステージに関するすべての情報を収集します。各ステージのデプロイメント計画は表示および変更できます。

デプロイメント計画を変更するステージで、メニューをクリックし、次に**「デプロイメント計画」**をクリックします。

![デプロイメント計画を開く](images/open_deployment_plan.png "デプロイメント計画を開く")

ご使用環境のデプロイメント・タスクのリストが表示されます。

![3 つの個別のパイプラインを含む複合パイプラインのデフォルト・デプロイメント計画](images/composite_deploy_plan.png)

デプロイメント計画の変更について詳しくは、[複合パイプライン用のデプロイメント計画のカスタマイズ](/docs/services/ContinuousDelivery/pipeline_deployment_plan.html)を参照してください。

## 個別のパイプラインの変更
{: #compositepipeline_add_job}

複合パイプラインから、個別のパイプラインを変更することができます。

1. アプリを展開します。

2. ステージのメニューから、**「構成」**をクリックします。

3. ステージに対し、ジョブの追加、変更、または削除を行います。詳しい手順については、[ジョブのステージへの追加](pipeline_build_deploy.html#deliverypipeline_add_job)を参照してください。

## 複合パイプラインでのジョブの実行
{: #compositepipeline_run_jobs}

アプリを展開してジョブを表示したら、ステージ内のすべてのジョブを手動で実行できます。アプリのスペース内の**「*ステージ* にデプロイ (Deploy to *stage*)」**アイコンをクリックします。

![単一アプリでのステージの実行](images/composite_run_stage.png)

スペース内のすべてのアプリ内のすべてのジョブを実行するには、複合パイプライン用のスペース内の**「*スペース* にデプロイ (Deploy to *space*)」**アイコンをクリックします。

![すべてのアプリでのステージの実行](images/composite_run_space.png)

ジョブは、複合青写真のデプロイメント計画に従って実行されます。

## ログの表示
{: #compositepipeline_view_logs}

ジョブのログを表示するには、そのジョブを含むアプリを展開し、ジョブをクリックします。

## IBM Bluemix DevOps Connect を使用した IBM UrbanCode Deploy との統合
{: #compositepipeline_devops_connect}

IBM Bluemix DevOps Connect は、オンプレミスの IBM&reg; UrbanCode&reg; Deploy のインストール済み環境と {{site.data.keyword.contdelivery_short}} 間の通信を調整します。DevOps Connect をインストールしたら、複合パイプラインでの IBM UrbanCode Deploy アプリの管理に使用できる統合を作成することができます。

**前提条件**

   * DevOps Connect を登録するには、IBM ID を持っている必要があります。

   * [Java&trade; Runtime Environment Version 8 Update 121 以降![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://java.com/en/download/){:new_window}がホスト・システム上にインストールされており、システム PATH 変数がそのロケーションに設定されていることを確認します。

   * IBM UrbanCode Deploy からの管理許可トークンが必要です。

DevOps Connect を使用して IBM UrbanCode Deploy と統合するには、以下のステップを実行します。

1. DevOps Connect をインストールし、それを使用してユーザーの組織を IBM UrbanCode Deploy と統合します。

  1. 複合パイプラインで、**「アプリの追加」**をクリックします。**「管理元」**リストから、**「IBM UrbanCode Deploy」**を選択します。

  1. 統合ステップを表示します。アプリのリストが表示されたら、最初に**「アプリ」**の横の情報アイコン (![情報アイコン](/images/info.png)) をクリックし、次に**「この組織に対する IBM UrbanCode Deploy の構成 (Configure IBM UrbanCode Deploy for this organization)」**をクリックします。

  1. 「UrbanCode Deploy 統合の構成」ウィンドウで**「ダウンロード」**をクリックして DevOps Connect をダウンロードします。IBM UrbanCode Deploy にアクセスできるコンピューター上に JAR ファイルを置きます。

  1. ウィンドウから、DevOps Connect インストール・スクリプトをコピーします。このスクリプトには、DevOps Connect を開始するためのコマンドと、{{site.data.keyword.contdelivery_short}} サービスを識別するために必要な資格情報が含まれています。

  1. DevOps Connect を置いたコンピューターでコマンド・シェルを開き、コピーしたスクリプトを貼り付けます。

  1. スクリプトを実行します。 DevOps Connect が始動メッセージを表示します。

1. DevOps Connect を登録します。

  1.  DevOps Connect を置いたコンピューターで、Web ブラウザーを使用して DevOps Connect ダッシュボードを開きます。デフォルト URL は https://localhost:8443 です。URL を変更し、他の始動オプションの詳細を知るには、[DevOps Connect 資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/urbancode/plugindoc/urbancode-sync/ibm-urbancode-sync-utility/1-2/){:new_window} を参照してください。


1. 「IBM にサインイン」ページに IBM ID とパスワードを入力し、**「サインイン」**をクリックします。サインインは、DevOps Connect を開始するたびに行います。

1. DevOps Connect で、IBM UrbanCode Deploy for DevOps Connect プラグインを使用して、組織と IBM UrbanCode Deploy 間の統合を作成します。

    1. 「統合」ページで、**「新規追加」**をクリックします。

    1. **「名前」**フィールドに統合の名前を入力します。

    1. **「統合タイプ」**リストから、**「IBM UrbanCode Deploy for DevOps Connect」**を選択します。

    1. **「サーバー URI」**フィールドに、IBM UrbanCode Deploy サーバーのパブリック URL を入力します。例えば、`https://my_UCD.example.com:8443` など。

    1. **「認証トークン」**フィールドに、IBM UrbanCode Deploy によって生成された認証トークンを入力するか貼り付けます。

    1. **「管理ユーザーの E メール (Admin User Email)」**フィールドに、ユーザーの E メール・アドレスを入力します。

    1. 統合が成功したことを確認するために、**「統合の実行」**をクリックします。DevOps Connect が、**「サーバー URI」**フィールドに指定されている IBM UrbanCode Deploy インスタンスに接続します。**「認証トークン」**フィールドに貼り付けられているトークンによって DevOps Connect が許可されます。

    1. **「保存」**をクリックします。

統合が成功した場合は、IBM UrbanCode Deploy アプリを複合パイプラインに追加できます。詳細情報については、[IBM UrbanCode Deploy からのアプリの追加](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_add_apps)を参照してください。


## IBM UrbanCode Deploy からのアプリの追加
{: #compositepipeline_add_apps}

DevOps Connect を使用して IBM UrbanCode Deploy と統合されている組織のメンバーは、IBM UrbanCode Deploy でアクセスできるアプリを複合パイプラインに追加できます。インストール手順については、[IBM Bluemix DevOps Connect を使用した IBM UrbanCode Deploy との統合](/docs/services/ContinuousDelivery/pipeline_composites.html#compositepipeline_devops_connect)を参照してください。

IBM UrbanCode Deploy に接続している組織のメンバーの場合、UrbanCode Deploy アプリを複合パイプラインに追加し、デプロイメント計画に組み込むアプリ・プロセスを選択し、アプリのデプロイメントをカスタマイズできます。

1. 複合パイプラインから、**「アプリの追加」**をクリックします。

2. **「管理元」**リストから、**「IBM UrbanCode Deploy」**を選択します。{{site.data.keyword.contdelivery_short}} と IBM UrbanCode Deploy との統合を最近行った場合は、サーバーを表示するためにブラウザーの最新表示が必要な可能性があります。

3. 追加するアプリを選択し、**「続行」**をクリックします。IBM UrbanCode Deploy アプリで使用可能なすべてのアプリ・プロセスが表示されます。選択したプロセスを実行するためのエントリーが、デプロイメント計画に追加されます。

4. アプリで使用するアプリ・プロセスを選択します。プロセスを見つけるには、検索オプションとフィルター・オプションを使用します。

5. **「保存」**をクリックします。選択した各 IBM UrbanCode Deploy アプリが、複合パイプライン内のアプリとして表示されます。

6. 以下のようにして、IBM UrbanCode Deploy アプリから複合パイプラインの論理環境に環境をマップします。

    1. 論理環境名の近くのメニューから、**「論理環境の管理」**を選択します。

    ![論理環境の管理の選択](images/composite_logical_env.png)

    2. 複合パイプライン内の各アプリに対して、IBM UrbanCode Deploy に定義した環境を選択します。選択したアプリ・プロセスは、そのアプリからの環境でのみ実行されます。

    3. **「保存」**をクリックします。

    4. 使用する論理環境ごとにこれらのステップを繰り返します。
