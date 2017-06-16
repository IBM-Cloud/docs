---

copyright:
  years: 2015, 2017
lastupdated: "2017-5-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.jazzhub_short}} プロジェクトをツールチェーンにアップグレード
{: #upgrade_projects}

{{site.data.keyword.jazzhub}} は、{{site.data.keyword.contdelivery_full}} へと進化しました。その変更の一部として、プロジェクトはツールチェーンにアップグレードされます。

ユーザーは、プロジェクトを自分でアップグレードするか、自動的にアップグレードされるのを待つことができます。最良の結果を得るためには、[前提条件](#upgrade_prereqs)を満たしたうえで、できるだけ早くプロジェクトをアップグレードして、ツールチェーンの名前やツールチェーンが作成される組織を制御できるようにしてください。
{: shortdesc}

## ツールチェーン
{: #compare_toolchains}

ツールチェーンはプロジェクトと同様ですが、以下のようないくつかの重要な違いがあります。

- プロジェクトは、1 つのリポジトリーとパイプラインしか持てません。ツールチェーンは、必要に応じていくつでもリポジトリーとパイプラインを持つことができます。
- ツールチェーンには、Slack、Sauce Labs、PagerDuty、および {{site.data.keyword.DRA_full}} などの、プロジェクトでは使用できないツールを組み込むことができます。
- ツールチェーンへのアクセスは、標準の {{site.data.keyword.Bluemix_notm}} 組織で管理されます。メンバーシップは、プロジェクト・レベルで管理されていたプロジェクトと異なり、組織レベルで維持されます。

ツールチェーンの詳細情報は、[YouTube ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://youtu.be/2SIPE1e7NJ4){: new_window}または [{{site.data.keyword.contdelivery_short}} 入門](/docs/services/ContinuousDelivery/index.html)
[![YouTube](images/CD_video.png) の外部リンク](https://youtu.be/2SIPE1e7NJ4){: new_window}で知ることができます。

## 前提条件
{: #upgrade_prereqs}

- アップグレードされたプロジェクトのツールチェーンにアクセスするには、{{site.data.keyword.Bluemix_notm}} ID が必要です。アップグレードする前に、アクティブな {{site.data.keyword.Bluemix_notm}} ID を持っていることを確認する必要があります。持っていない場合は、[登録](https://console.ng.bluemix.net/registration/)してください。
- {{site.data.keyword.jazzhub_short}} プロジェクト所有者が正しいことを確認してください。プロジェクトから作成されるツールチェーンは、その所有者の {{site.data.keyword.Bluemix_notm}} 組織の一部になります。
- アップグレードを開始する計画がある場合は、パイプラインがデプロイされるすべての組織およびスペースのメンバーであることを確認してください。プロジェクト管理者であれば誰でもアップグレードを開始できます。ただし、アップグレードを開始する管理者がパイプラインのデプロイ先のすべての組織およびスペースのメンバーでなければ、パイプラインは作成されません。アップグレードを開始する人が、ツールチェーンのリポジトリーの所有者になります。
- ツールチェーン内の Eclipse Orion {{site.data.keyword.webide}} は、プロジェクトに関連付けられた {{site.data.keyword.webide}} から分離しています。{{site.data.keyword.webide}} を使用していて、コミットされていない変更がある場合は、アップグレードする前にそれらの変更をコミットしてください。


## プロジェクトからツールチェーンへのアップグレード
{: #project_to_toolchain}

**重要:** hub.jazz.net のプロジェクトとツールチェーンはどちらも、米国南部地域でホストされます。異なる地域にアプリをデプロイするようにプロジェクトが構成されている場合でも、プロジェクトがツールチェーンにアップグレードされた後に、アプリは前述の地域にデプロイされます。

プロジェクトのアップグレード準備ができると、プロジェクトのカードおよび「概要」ページにメッセージが表示されます。

![「アップグレード準備完了 (Ready To Upgrade)」ラベルの付いたカードのイメージ](images/card-project-to-upgrade.png)

![「アップグレード時間 (Time to Upgrade)」メッセージ](images/banner-ready-to-upgrade.png)

**ヒント:** アップグレード準備ができたプロジェクトは、「マイ・プロジェクト」ページのメニューから見つけることができます。

![「アップグレードするプロジェクト (Projects To Upgrade)」メニュー項目のイメージ](images/menu-projects-to-upgrade.png)

アップグレードを開始すると、プロジェクト内のパイプライン・ステージはロックされます。ロックされたパイプライン・ステージは、実行することも変更することもできません。ツールチェーンを削除してアップグレードを元に戻すと、パイプラインはアンロックされます。

JazzHub でホストされている Git リポジトリーをプロジェクトが使用する場合は、アップグレード開始後に、ツールチェーンに移動するデータの整合性を確保するためにリポジトリーがロックされます。ツールチェーンを削除してアップグレードを元に戻すと、JazzHub 上のリポジトリーはアンロックされます。

## アップグレード・プロセスの開始
{: #start_upgrade}

アップグレード・プロセスを開始する前に、[YouTube ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://youtu.be/LSr2e3uvyLs){: new_window} で実際のアップグレード・プロセスを見ることをお勧めします。
[![YouTube への外部リンク](images/migration-video2.png)](https://youtu.be/LSr2e3uvyLs){: new_window}

プロジェクトをツールチェーンにアップグレードするには、以下のステップを実行します。

1. アップグレード・プロセスを開始するには、バナー・メッセージで**「今すぐアップグレード (upgrade now)」**をクリックします。「プロジェクト・アップグレード・ツールチェーン (Project upgrade toolchain)」ページが開きます。

   ![アップグレード・ページの例](images/project-upgrade-toolchain.png)

   アップグレード・プロセスの概要については、そのページ上の説明をお読みください。ツールチェーンには、プロジェクトのパイプラインと同じステージとジョブを含む新しいパイプラインが組み込まれます。さらに、ツールチェーンには、{{site.data.keyword.contdelivery_short}} で実行されている Eclipse Orion {{site.data.keyword.webide}} へのポインターも含まれます。

   この例では、プロジェクトは github.com のパブリック・リポジトリーを使用するため、ツールチェーンは同じ GitHub リポジトリーに接続されます。JazzHub にホストされている Git リポジトリーをプロジェクトが使用する場合、そのリポジトリーの内容は、{{site.data.keyword.contdelivery_short}} の一部である {{site.data.keyword.gitrepos}}内の新しいリポジトリーに複製されます。リポジトリーの各タイプの扱いの全詳細については、次の表を参照してください。

|プロジェクト・リポジトリー |プロジェクト・タイプ	|ツールチェーン・リポジトリー |
|:----------|:------------------------------|:------------------|
|github.com 		|プライベートまたはパブリック 		|{{site.data.keyword.Bluemix_notm}} Public と同じ github.com リポジトリー	|
|hub.jazz.net/git		|プライベートまたはパブリック 		|{{site.data.keyword.Bluemix_notm}} Public の {{site.data.keyword.gitrepos}}内の新しいリポジトリー	|
{: caption="表 1. プロジェクト・リポジトリー対ツールチェーン・リポジトリーのマッピング" caption-side="top"}

2. ツールチェーンをカスタマイズするには、次のいくつかの設定を構成できます。

   - ツールチェーンの名前を変更するには、**「名前」**フィールドを編集します。

      ![「名前」フィールド](images/name-change.png)

   - ツールチェーンを作成する {{site.data.keyword.Bluemix_notm}} 組織を変更するには、アカウント・メニューから組織を選択します。

      ![Bluemix 組織の選択機能](images/bluemix-organization-chooser.png)

   ツールチェーンは組織レベルで管理されるため、ツールチェーンにアクセスする必要があるプロジェクト・メンバーが既に存在している、またはそれらのメンバーを追加できる組織を必ず選択するようにしてください。

3. プロジェクトで Track & Plan を使用した場合は、Track & Plan データを GitHub Issues に転送できます。

   ![Track and Plan のオプション](images/upgrade-tutorial-track-and-plan.png)

   - Track & Plan データをマイグレーションするかどうかを示します。
   - デフォルトでは、Track & Plan データのすべてがマイグレーションされます。特定の照会の一部である作業項目のみをマイグレーションする場合は、その照会を指定します。
   - GitHub Issues のラベルにマップする作業項目の属性を選択します。

4. **「作成」**をクリックします。新しいツールチェーンが作成され、「概要」ページが表示されます。

   ![アップグレードされたツールチェーンの概要](images/new-toolchain-page.png)

   - GitHub リポジトリー、または関連付けられた Issue Tracker にアクセスするには、**「GitHub」**または**「Issues」**をクリックします。
   - パイプラインにアクセスするには、**「Delivery Pipeline」**をクリックします。
   - ワークスペースにチェックアウトされた、リポジトリーのコンテンツを含む {{site.data.keyword.webide}} にアクセスするには、**Eclipse Orion {{site.data.keyword.webide}}** をクリックします。

   アップグレード中にプロジェクトに戻った場合、ソース・コードを新しいリポジトリーにインポートする処理や、Track &amp; Plan 作業項目を問題としてインポートする処理がアップグレード・プロセスに含まれる場合は特に、アップグレードが進行中であることがバナー・メッセージで示されることがあります。

   ![ツールチェーンにアップグレードされているプロジェクトに関するメッセージ](images/project-being-upgraded-banner.png)

## プロジェクトの再訪
{: #revisit_projects}

これで新しいツールチェーンを使用する準備ができました。プロジェクトには「アップグレード済み」のラベルが付けられ、「概要」ページに確認メッセージが表示されます。

![「アップグレード済み」ラベルの付いたプロジェクト・カードのイメージ](images/card-upgraded-project.png)

![アップグレード済みプロジェクト](images/banner-upgraded.png)

「マイ・プロジェクト」ページのメニューから**「アップグレード済みプロジェクト (Upgraded Projects)」**を選択することにより、どのプロジェクトがアップグレードされているか確認できます。

![「アップグレード済みプロジェクト」メニュー項目のイメージ](images/menu-upgraded-projects.png)

アップグレードを元に戻す必要がある場合は、ツールチェーンを削除します。ツールチェーンの「概要」ページの**「他のアクション」**メニューからツールチェーンを削除できます。

![「他のアクション」メニューの削除アクションのイメージ](images/upgrade-tutorial-delete-toolchain.png)

プロジェクトに戻るとアップグレード・メッセージが再び表示され、準備ができたら再びアップグレードできます。

## 次のステップ
{: #upgrade_next_steps}

1. ブラウザーを最新表示し、プロジェクトの「概要」ページでプロジェクトが「このツールチェーンにアップグレードされた」というメッセージがあるかどうか調べて、アップグレードが完了したことを確認します。

   ![プロジェクトがアップグレードされたことを示すバナーのメッセージ](images/banner-upgraded.png)

   **注:** 「今すぐアップグレード」というメッセージが表示されたら、アップグレードは失敗しています。**「今すぐアップグレード (upgrade now)」**リンクをクリックして再試行してください。

   ![プロジェクトがアップグレード可能状態であることを示すバナーのメッセージ](images/banner-ready-to-upgrade.png)

2. チーム・メンバーにツールチェーンへのアクセス権限を付与します。
    - 各チーム・メンバーには、有効な {{site.data.keyword.Bluemix_notm}} アカウントが必要です。アカウントを持っていないチーム・メンバーは、[登録![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/registration){:new_window}する必要があります。
    - ツールチェーンの「管理」ページから、ツールチェーンに対するアクセス権限を組織のメンバーに付与します。ツールチェーンのアクセス制御について詳しくは、[アクセスの管理 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){:new_window} を参照してください。
    - ユーザーがツールチェーンの属する組織のメンバーでない場合は、「組織の管理」ページから、そのユーザーを組織に追加します。
組織の管理について詳しくは、[組織とスペースの管理 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](/docs/admin/orgs_spaces.html#orgsspacesusers){:new_window} を参照してください。

3. {{site.data.keyword.jazzhub_short}} プロジェクトからのツールではなく、ツールチェーンからのツールを使用します。例えば、ブラウザーからコードを編集するには、ツールチェーンから Web IDE を使用します。

4. {{site.data.keyword.gitrepos}}を使用する場合は、個人用アクセス・トークンまたは SSH 鍵を使用して認証します。SSH 鍵について詳しくは、[認証のための個人用アクセス・トークンまたは SSH 鍵の作成](/docs/services/ContinuousDelivery/git_working.html#git_authentication)を参照してください。外部 Git クライアントから https を使用して認証するには、以下のステップを実行します。
    1. {{site.data.keyword.gitrepos}}・ユーザー設定の[「Access Tokens」ページ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/profile/personal_access_tokens){:new_window} にアクセスします。
    2. スコープとして **api** を使用する個人用アクセス・トークンを作成します。
    3. [「Account」ページ ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://git.ng.bluemix.net/profile/account){:new_window} にアクセスして、{{site.data.keyword.gitrepos}}に使用しているユーザー名を見つけます。ご使用のユーザー名は「Change username」セクションにリストされ、作成する個人用リポジトリーの URL の最初の部分として示されます。
    4. 外部 Git クライアントから https を使用して {{site.data.keyword.gitrepos}}に対する認証を行うには、ユーザー名と個人用アクセス・トークンを使用します。
    5. JazzHub Git リポジトリーのローカル・リポジトリーを再使用する場合は、そのリポジトリーを {{site.data.keyword.gitrepos}}内の新しいリポジトリーに複製します。端末のシェルから、JazzHub Git リポジトリーが複製されているディレクトリーに移動します。`git remote set-url` コマンド `git remote set-url origin https://git.ng.bluemix.net/<userid>/<name-of-new-repo>` を入力します。

        **ヒント:** どのリモート URL がどのリモート名に設定されているかを確認するには、`git remote -v` コマンドを使用します。デフォルトのリモート名は `origin` です。より高度なセットアップの場合、コマンドの形式は `git remote set-url <remote-name-that-uses-jazzhub-repo> https://git.ng.bluemix.net/<userid>/<name-of-new-repo>` のようになります。

5. ツールチェーンがセットアップされ、それを使い始めたなら、そのプロジェクトが誰にも使用されないようにするために、以下のステップのすべてまたはいくつかを実行することを検討してください。
    - 使用してはならないことを示す接尾部をプロジェクト名に追加する。例えば、プロジェクトの末尾に `_DO_NOT_USE` を追加します。
    - 使用されなくなったことを示すためにプロジェクトの説明を更新し、ツールチェーンへのポインターを追加する。
    - プロジェクトからメンバーを削除する。
    - 必要がなくなったプロジェクトは削除する。

6. オプション: プロジェクトの開発成熟度、チームのプラクティス、コード・ベースの品質を探るには、ツールチェーンに IBM Cloud {{site.data.keyword.DRA_short}} を追加します。{{site.data.keyword.DRA_short}} は、開発者、チーム、デプロイメントの分析を DevOps プロジェクトに適用します。詳しくは、[{{site.data.keyword.DRA_short}} 概説](/docs/services/DevOpsInsights/index.html)を参照してください。


## トラブルシューティング
{: #upgrade_troubleshoot}

ご質問または問題がある場合は、[サポート・フォーラム](https://developer.ibm.com/answers/questions/ask/?smartspace=devops-services)にアクセスしてください。フォーラムへの投稿には、{{site.data.keyword.jazzhub_short}} プロジェクトと {{site.data.keyword.contdelivery_short}} ツールチェーンの URL を記載し、`devops-services` タグを付けてください。
