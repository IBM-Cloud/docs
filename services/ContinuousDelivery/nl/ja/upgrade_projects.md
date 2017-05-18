---

copyright:
  years: 2015, 2017
lastupdated: "2017-5-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.jazzhub_short}} プロジェクトをツルチェンにアップグレド
{: #upgrade_projects}

{{site.data.keyword.jazzhub}} は、{{site.data.keyword.contdelivery_full}} へと進化しました。その変更の一部として、プロジェクトはツルチェンにアップグレドされます。

ユザは、プロジェクトを自分でアップグレドするか、自動的にアップグレドされるのを待つことができます。最良の結果を得るためには、[前提条件](#upgrade_prereqs)を満たしたうえで、できるだけ早くプロジェクトをアップグレドして、ツルチェンの名前やツルチェンが作成される組織を制御できるようにしてください。
{: shortdesc}

## ツルチェン
{: #compare_toolchains}

ツルチェンはプロジェクトと同様ですが、以下のようないくつかの重要な違いがあります。

- プロジェクトは、1 つのリポジトリとパイプラインしか持てません。ツルチェンは、必要に応じていくつでもリポジトリとパイプラインを持つことができます。
- ツルチェンには、Slack、Sauce Labs、PagerDuty、および {{site.data.keyword.DRA_full}} などの、プロジェクトでは使用できないツルを組み込むことができます。
- ツルチェンへのアクセスは、標準の {{site.data.keyword.Bluemix_notm}} 組織で管理されます。メンバシップは、プロジェクト・レベルで管理されていたプロジェクトと異なり、組織レベルで維持されます。

ツルチェンの詳細情報は、[YouTube ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://youtu.be/2SIPE1e7NJ4){: new_window}または [{{site.data.keyword.contdelivery_short}} 入門](/docs/services/ContinuousDelivery/index.html)
[![YouTube](images/CD_video.png) の外部リンク](https://youtu.be/2SIPE1e7NJ4){: new_window}で知ることができます。

## 前提条件
{: #upgrade_prereqs}

- アップグレドされたプロジェクトのツルチェンにアクセスするには、{{site.data.keyword.Bluemix_notm}} ID が必要です。アップグレドする前に、アクティブな {{site.data.keyword.Bluemix_notm}} ID を持っていることを確認する必要があります。持っていない場合は、[登録](https://console.ng.bluemix.net/registration/)してください。
- {{site.data.keyword.jazzhub_short}} プロジェクト所有者が正しいことを確認してください。プロジェクトから作成されるツルチェンは、その所有者の {{site.data.keyword.Bluemix_notm}} 組織の一部になります。
- アップグレドを開始する計画がある場合は、パイプラインがデプロイされるすべての組織およびスペスのメンバであることを確認してください。プロジェクト管理者であれば誰でもアップグレドを開始できます。ただし、アップグレドを開始する管理者がパイプラインのデプロイ先のすべての組織およびスペスのメンバでなければ、パイプラインは作成されません。アップグレドを開始する人が、ツルチェンのリポジトリの所有者になります。
- ツルチェン内の Eclipse Orion {{site.data.keyword.webide}} は、プロジェクトに関連付けられた {{site.data.keyword.webide}} から分離しています。{{site.data.keyword.webide}} を使用していて、コミットされていない変更がある場合は、アップグレドする前にそれらの変更をコミットしてください。


## プロジェクトからツルチェンへのアップグレド
{: #project_to_toolchain}

**重要:** hub.jazz.net のプロジェクトとツルチェンはどちらも、米国南部地域でホストされます。異なる地域にアプリをデプロイするようにプロジェクトが構成されている場合でも、プロジェクトがツルチェンにアップグレドされた後に、アプリは前述の地域にデプロイされます。

プロジェクトのアップグレド準備ができると、プロジェクトのカドおよび「概要」ペジにメッセジが表示されます。

![「アップグレド準備完了 (Ready To Upgrade)」ラベルの付いたカドのイメジ](images/card-project-to-upgrade.png)

![「アップグレド時間 (Time to Upgrade)」メッセジ](images/banner-ready-to-upgrade.png)

**ヒント:** アップグレド準備ができたプロジェクトは、「マイ・プロジェクト」ペジのメニュから見つけることができます。

![「アップグレドするプロジェクト (Projects To Upgrade)」メニュ項目のイメジ](images/menu-projects-to-upgrade.png)

アップグレドを開始すると、プロジェクト内のパイプライン・ステジはロックされます。ロックされたパイプライン・ステジは、実行することも変更することもできません。ツルチェンを削除してアップグレドを元に戻すと、パイプラインはアンロックされます。

JazzHub でホストされている Git リポジトリをプロジェクトが使用する場合は、アップグレド開始後に、ツルチェンに移動するデタの整合性を確保するためにリポジトリがロックされます。ツルチェンを削除してアップグレドを元に戻すと、JazzHub 上のリポジトリはアンロックされます。

## アップグレド・プロセスの開始
{: #start_upgrade}

アップグレド・プロセスを開始する前に、[YouTube ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://youtu.be/LSr2e3uvyLs){: new_window} で実際のアップグレド・プロセスを見ることをお勧めします。
[![YouTube への外部リンク](images/migration-video2.png)](https://youtu.be/LSr2e3uvyLs){: new_window}

プロジェクトをツルチェンにアップグレドするには、以下のステップを実行します。

1. アップグレド・プロセスを開始するには、バナ・メッセジで**「今すぐアップグレド (upgrade now)」**をクリックします。「プロジェクト・アップグレド・ツルチェン (Project upgrade toolchain)」ペジが開きます。

   ![アップグレド・ペジの例](images/project-upgrade-toolchain.png)

   アップグレド・プロセスの概要については、そのペジ上の説明をお読みください。ツルチェンには、プロジェクトのパイプラインと同じステジとジョブを含む新しいパイプラインが組み込まれます。さらに、ツルチェンには、{{site.data.keyword.contdelivery_short}} で実行されている Eclipse Orion {{site.data.keyword.webide}} へのポインタも含まれます。

   この例では、プロジェクトは github.com のパブリック・リポジトリを使用するため、ツルチェンは同じ GitHub リポジトリに接続されます。JazzHub にホストされている Git リポジトリをプロジェクトが使用する場合、そのリポジトリの内容は、{{site.data.keyword.contdelivery_short}} の一部である {{site.data.keyword.gitrepos}}内の新しいリポジトリに複製されます。リポジトリの各タイプの扱いの全詳細については、次の表を参照してください。

|プロジェクト・リポジトリ |プロジェクト・タイプ	|ツルチェン・リポジトリ |
|:----------|:------------------------------|:------------------|
|github.com 		|プライベトまたはパブリック 		|{{site.data.keyword.Bluemix_notm}} Public と同じ github.com リポジトリ	|
|hub.jazz.net/git		|プライベトまたはパブリック 		|{{site.data.keyword.Bluemix_notm}} Public の {{site.data.keyword.gitrepos}}内の新しいリポジトリ	|
{: caption="表 1. プロジェクト・リポジトリ対ツルチェン・リポジトリのマッピング" caption-side="top"}

2. ツルチェンをカスタマイズするには、次のいくつかの設定を構成できます。

   - ツルチェンの名前を変更するには、**「名前」**フィルドを編集します。

      ![「名前」フィルド](images/name-change.png)

   - ツルチェンを作成する {{site.data.keyword.Bluemix_notm}} 組織を変更するには、アカウント・メニュから組織を選択します。

      ![Bluemix 組織の選択機能](images/bluemix-organization-chooser.png)

   ツルチェンは組織レベルで管理されるため、ツルチェンにアクセスする必要があるプロジェクト・メンバが既に存在している、またはそれらのメンバを追加できる組織を必ず選択するようにしてください。

3. プロジェクトで Track & Plan を使用した場合は、Track & Plan デタを GitHub Issues に転送できます。

   ![Track and Plan のオプション](images/upgrade-tutorial-track-and-plan.png)

   - Track & Plan デタをマイグレションするかどうかを示します。
   - デフォルトでは、Track & Plan デタのすべてがマイグレションされます。特定の照会の一部である作業項目のみをマイグレションする場合は、その照会を指定します。
   - GitHub Issues のラベルにマップする作業項目の属性を選択します。

4. **「作成」**をクリックします。新しいツルチェンが作成され、「概要」ペジが表示されます。

   ![アップグレドされたツルチェンの概要](images/new-toolchain-page.png)

   - GitHub リポジトリ、または関連付けられた Issue Tracker にアクセスするには、**「GitHub」**または**「Issues」**をクリックします。
   - パイプラインにアクセスするには、**「Delivery Pipeline」**をクリックします。
   - ワクスペスにチェックアウトされた、リポジトリのコンテンツを含む {{site.data.keyword.webide}} にアクセスするには、**Eclipse Orion {{site.data.keyword.webide}}** をクリックします。

   アップグレド中にプロジェクトに戻った場合、ソス・コドを新しいリポジトリにインポトする処理や、Track &amp; Plan 作業項目を問題としてインポトする処理がアップグレド・プロセスに含まれる場合は特に、アップグレドが進行中であることがバナ・メッセジで示されることがあります。

   ![ツルチェンにアップグレドされているプロジェクトに関するメッセジ](images/project-being-upgraded-banner.png)

## プロジェクトの再訪
{: #revisit_projects}

これで新しいツルチェンを使用する準備ができました。プロジェクトには「アップグレド済み」のラベルが付けられ、「概要」ペジに確認メッセジが表示されます。

![「アップグレド済み」ラベルの付いたプロジェクト・カドのイメジ](images/card-upgraded-project.png)

![アップグレド済みプロジェクト](images/banner-upgraded.png)

「マイ・プロジェクト」ペジのメニュから**「アップグレド済みプロジェクト (Upgraded Projects)」**を選択することにより、どのプロジェクトがアップグレドされているか確認できます。

![「アップグレド済みプロジェクト」メニュ項目のイメジ](images/menu-upgraded-projects.png)

アップグレドを元に戻す必要がある場合は、ツルチェンを削除します。ツルチェンの「概要」ペジの**「他のアクション」**メニュからツルチェンを削除できます。

![「他のアクション」メニュの削除アクションのイメジ](images/upgrade-tutorial-delete-toolchain.png)

プロジェクトに戻るとアップグレド・メッセジが再び表示され、準備ができたら再びアップグレドできます。

## 次のステップ
{: #upgrade_next_steps}

1. ブラウザを最新表示し、プロジェクトの「概要」ペジでプロジェクトが「このツルチェンにアップグレドされた」というメッセジがあるかどうか調べて、アップグレドが完了したことを確認します。

   ![プロジェクトがアップグレドされたことを示すバナのメッセジ](images/banner-upgraded.png)

   **注:** 「今すぐアップグレド」というメッセジが表示されたら、アップグレドは失敗しています。**「今すぐアップグレド (upgrade now)」**リンクをクリックして再試行してください。

   ![プロジェクトがアップグレド可能状態であることを示すバナのメッセジ](images/banner-ready-to-upgrade.png)

2. チム・メンバにツルチェンへのアクセス権限を付与します。
    - 各チム・メンバには、有効な {{site.data.keyword.Bluemix_notm}} アカウントが必要です。アカウントを持っていないチム・メンバは、[登録![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/registration){:new_window}する必要があります。
    - ツルチェンの「管理」ペジから、ツルチェンに対するアクセス権限を組織のメンバに付与します。ツルチェンのアクセス制御について詳しくは、[アクセスの管理 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){:new_window} を参照してください。
    - ユザがツルチェンの属する組織のメンバでない場合は、「組織の管理」ペジから、そのユザを組織に追加します。
組織の管理について詳しくは、[組織とスペスの管理 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/admin/orgs_spaces.html#orgsspacesusers){:new_window} を参照してください。

3. {{site.data.keyword.jazzhub_short}} プロジェクトからのツルではなく、ツルチェンからのツルを使用します。例えば、ブラウザからコドを編集するには、ツルチェンから Web IDE を使用します。

4. {{site.data.keyword.gitrepos}}を使用する場合は、個人用アクセス・トクンまたは SSH 鍵を使用して認証します。SSH 鍵について詳しくは、[認証のための個人用アクセス・トクンまたは SSH 鍵の作成](/docs/services/ContinuousDelivery/git_working.html#git_authentication)を参照してください。外部 Git クライアントから https を使用して認証するには、以下のステップを実行します。
    1. {{site.data.keyword.gitrepos}}・ユザ設定の[「Access Tokens」ペジ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/profile/personal_access_tokens){:new_window} にアクセスします。
    2. スコプとして **api** を使用する個人用アクセス・トクンを作成します。
    3. [「Account」ペジ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/profile/account){:new_window} にアクセスして、{{site.data.keyword.gitrepos}}に使用しているユザ名を見つけます。ご使用のユザ名は「Change username」セクションにリストされ、作成する個人用リポジトリの URL の最初の部分として示されます。
    4. 外部 Git クライアントから https を使用して {{site.data.keyword.gitrepos}}に対する認証を行うには、ユザ名と個人用アクセス・トクンを使用します。
    5. JazzHub Git リポジトリのロカル・リポジトリを再使用する場合は、そのリポジトリを {{site.data.keyword.gitrepos}}内の新しいリポジトリに複製します。端末のシェルから、JazzHub Git リポジトリが複製されているディレクトリに移動します。`git remote set-url` コマンド `git remote set-url origin https://git.ng.bluemix.net/<userid>/<name-of-new-repo>` を入力します。

        **ヒント:** どのリモト URL がどのリモト名に設定されているかを確認するには、`git remote -v` コマンドを使用します。デフォルトのリモト名は `origin` です。より高度なセットアップの場合、コマンドの形式は `git remote set-url <remote-name-that-uses-jazzhub-repo> https://git.ng.bluemix.net/<userid>/<name-of-new-repo>` のようになります。

5. ツルチェンがセットアップされ、それを使い始めたなら、そのプロジェクトが誰にも使用されないようにするために、以下のステップのすべてまたはいくつかを実行することを検討してください。
    - 使用してはならないことを示す接尾部をプロジェクト名に追加する。例えば、プロジェクトの末尾に `_DO_NOT_USE` を追加します。
    - 使用されなくなったことを示すためにプロジェクトの説明を更新し、ツルチェンへのポインタを追加する。
    - プロジェクトからメンバを削除する。
    - 必要がなくなったプロジェクトは削除する。

6. オプション: プロジェクトの開発成熟度、チムのプラクティス、コド・ベスの品質を探るには、ツルチェンに IBM Cloud {{site.data.keyword.DRA_short}} を追加します。{{site.data.keyword.DRA_short}} は、開発者、チム、デプロイメントの分析を DevOps プロジェクトに適用します。詳しくは、[{{site.data.keyword.DRA_short}} 概説](/docs/services/DevOpsInsights/index.html)を参照してください。


## トラブルシュティング
{: #upgrade_troubleshoot}

ご質問または問題がある場合は、[サポト・フォラム](https://developer.ibm.com/answers/questions/ask/?smartspace=devops-services)にアクセスしてください。フォラムへの投稿には、{{site.data.keyword.jazzhub_short}} プロジェクトと {{site.data.keyword.contdelivery_short}} ツルチェンの URL を記載し、`devops-services` タグを付けてください。
