---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-21"

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.jazzhub_short}} プロジェクトをツールチェーンにアップグレード
{: #upgrade_projects}

{{site.data.keyword.jazzhub}} は、{{site.data.keyword.contdelivery_full}} へと進化しました。その変更の一部として、プロジェクトはツールチェーンにアップグレードされます。 

ユーザーは、プロジェクトを自分でアップグレードするか、自動的にアップグレードされるのを待つことができます。最良の経験のためには、できるだけ早くプロジェクトをアップグレードしてください。それにより、ツールチェーンの名前や、ツールチェーンが作成される組織を制御することができます。  
{: shortdesc}

## ツールチェーン
{: #compare_toolchains}

ツールチェーンはプロジェクトと同様ですが、以下のようないくつかの重要な違いがあります。

- プロジェクトは、1 つのリポジトリーとパイプラインしか持てません。ツールチェーンは、必要に応じていくつでもリポジトリーとパイプラインを持つことができます。
- ツールチェーンには、Slack、Sauce Labs、PagerDuty、および {{site.data.keyword.DRA_full}} などの、プロジェクトでは使用できないツールを組み込むことができます。
- ツールチェーンへのアクセスは、標準の Bluemix 組織を介して管理されます。メンバーシップは、プロジェクト・レベルで管理されていたプロジェクトと異なり、組織レベルで維持されます。

ツールチェーンの詳細情報は、[YouTube ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://youtu.be/2SIPE1e7NJ4){: new_window}または [{{site.data.keyword.contdelivery_short}} 入門](/docs/services/ContinuousDelivery/index.html)
[![YouTube](images/CD_video.png) の外部リンク](https://youtu.be/2SIPE1e7NJ4){: new_window}で知ることができます。    

## 前提条件
{: #upgrade_prereqs}    

- アップグレードされたプロジェクトのツールチェーンにアクセスするには、Bluemix ID が必要です。アップグレードする前に、アクティブな Bluemix ID を持っていることを確認する必要があります。持っていない場合は、[登録](https://console.ng.bluemix.net/registration/)してください。
- DevOps Services プロジェクトの所有者が正しいことを確認します。プロジェクトから作成されるツールチェーンは、その所有者の Bluemix 組織の一部になります。

**重要:** ツールチェーン内の Eclipse Orion {{site.data.keyword.webide}} は、プロジェクトに関連付けられている {{site.data.keyword.webide}} とは別個になります。{{site.data.keyword.webide}} を使用していて、コミットされていない変更がある場合は、アップグレードする前にそれらの変更をコミットしてください。  


## プロジェクトからツールチェーンへのアップグレード
{: #project_to_toolchain}

プロジェクトのアップグレード準備ができると、プロジェクトのカードおよび「概要」ページにメッセージが表示されます。

![「アップグレード準備完了 (Ready To Upgrade)」ラベルの付いたカードのイメージ](images/card-project-to-upgrade.png)

![「アップグレード時間 (Time to Upgrade)」メッセージ](images/banner-ready-to-upgrade.png)

**ヒント:** アップグレード準備ができたプロジェクトは、「マイ・プロジェクト」ページのメニューから見つけることができます。 

![「アップグレードするプロジェクト (Projects To Upgrade)」メニュー項目のイメージ](images/menu-projects-to-upgrade.png)

## アップグレード・プロセスの開始
{: #start_upgrade}

アップグレード・プロセスを開始する前に、実施されているプロセスを [YouTube![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://youtu.be/oaZVGveVxBg){: new_window}[![YouTube の外部リンク](images/migration-video2.png)](https://youtu.be/oaZVGveVxBg){: new_window} で視聴できます。    
プロジェクトをツールチェーンにアップグレードするには、以下のステップを実行します。

1. アップグレード・プロセスを開始するには、バナー・メッセージで**「今すぐアップグレード (upgrade now)」**をクリックします。「プロジェクト・アップグレード・ツールチェーン (Project upgrade toolchain)」ページが開きます。 

   ![アップグレード・ページの例](images/project-upgrade-toolchain.png)

   アップグレード・プロセスの概要については、そのページ上の説明をお読みください。この場合、プロジェクトでは GitHub.com のリポジトリーが使用されていたため、ツールチェーンは同じ GitHub リポジトリーに接続されます。ツールチェーンには、プロジェクトのパイプラインと同じステージとジョブを含む新しいパイプラインが組み込まれます。さらに、ツールチェーンには、{{site.data.keyword.contdelivery_short}} で実行されている Eclipse Orion {{site.data.keyword.webide}} へのポインターも含まれます。

2. ツールチェーンをカスタマイズするには、次のいくつかの設定を構成できます。

   - ツールチェーンの名前を変更するには、**「名前」**フィールドを編集します。

      ![「名前」フィールド](images/name-change.png)

   - ツールチェーンを作成する {{site.data.keyword.Bluemix_notm}} 組織を変更するには、アカウント・メニューから組織を選択します。

      ![Bluemix 組織の選択機能](images/bluemix-organization-chooser.png)

   ツールチェーンは組織レベルで管理されるため、ツールチェーンにアクセスする必要があるプロジェクト・メンバーが既に存在している、またはそれらのメンバーを追加できる組織を必ず選択するようにしてください。 
  
3. **「作成」**をクリックします。新しいツールチェーンが作成され、「概要」ページが表示されます。

   ![アップグレードされたツールチェーンの概要](images/new-toolchain-page.png)

   - GitHub リポジトリー、または関連付けられた Issue Tracker にアクセスするには、**「GitHub」**または**「Issues」**をクリックします。
   
   - パイプラインにアクセスするには、**「Delivery Pipeline」**をクリックします。  
   
   - ワークスペースにチェックアウトされた、リポジトリーのコンテンツを含む {{site.data.keyword.webide}} にアクセスするには、**Eclipse Orion {{site.data.keyword.webide}}** をクリックします。 

## プロジェクトの再訪
{: #revisit_projects}

これで新しいツールチェーンを使用する準備ができました。プロジェクトには「アップグレード済み」のラベルが付けられ、「概要」ページに確認メッセージが表示されます。

![「アップグレード済み」ラベルの付いたプロジェクト・カードのイメージ](images/card-upgraded-project.png)

![アップグレード済みプロジェクト](images/banner-upgraded.png)

「マイ・プロジェクト」ページのメニューから**「アップグレード済みプロジェクト (Upgraded Projects)」**を選択することにより、どのプロジェクトがアップグレードされているか確認できます。

![「アップグレード済みプロジェクト」メニュー項目のイメージ](images/menu-upgraded-projects.png)

アップグレードを元に戻す必要がある場合は、ツールチェーンを削除します。そして、プロジェクトの「概要」ページに戻ると、アップグレード・メッセージが再度表示され、準備ができた時に再度アップグレードすることができます。

## 次のステップ
{: #upgrade_next_steps}   

1. プロジェクトの「概要」ページのメッセージをチェックして、アップグレードが完了したことを確認します。    

   ![アップグレード済みプロジェクト](images/banner-upgraded.png)    

2. チーム・メンバーにツールチェーンへのアクセス権限を付与します。    
    - 各チーム・メンバーは、有効な Bluemix アカウントを持っている必要があります。アカウントを持っていないチーム・メンバーは、[登録![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/registration){:new_window}する必要があります。
    - ツールチェーンが属している組織にチーム・メンバーを追加します。
3. {{site.data.keyword.jazzhub_short}} プロジェクトからのツールではなく、ツールチェーンからのツールを使用します。例えば、ブラウザーからコードを編集するには、ツールチェーンから Web IDE を使用します。    

## トラブルシューティング
{: #upgrade_troubleshoot}    

ご質問または問題がある場合は、[hub@jazz.net](mailto:hub@jazz.net) に E メールを送信してください。E メールには、{{site.data.keyword.jazzhub_short}} プロジェクトと {{site.data.keyword.contdelivery_short}} ツールチェーンの URL を含めてください。

