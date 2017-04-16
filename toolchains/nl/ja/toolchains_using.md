---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} Public でのツールチェーンの使い方
{: #toolchains-using}

最終更新日: 2016 年 10 月 7 日
{: .last-updated}

ツールチェーンを使用して、日常的な開発、デプロイメント、運用の作業の生産性を向上させることができます。ツールチェーンをセットアップした後、
ツール統合を追加、削除、構成して、ツールチェーンへのアクセスを管理することができます。
ツールチェーンは米国南部地域でのみ利用可能です。
{: shortdesc}

**注記**: トップ・バナーをチェックして、新しい Bluemix エクスペリエンスで作業していることを確認してください。

 * 新しい Bluemix の試行についてのメッセージが表示される場合、クラシック Bluemix エクスペリエンスで作業しています。リンクをクリックして、新しい Bluemix エクスペリエンスを開きます。
 * メッセージが表示されない場合、すでに新しい Bluemix エクスペリエンスで作業しています。

## ツール統合の構成
{: #configuring_a_tool_integration}

ツールチェーンの作成時にツール統合の構成を据え置いた場合は、**「構成」**ボタンがタイルに表示されます。ツールチェーンの作成時にツール統合を構成した場合は、その構成設定を更新できます。

1. DevOps ダッシュボードの**「ツールチェーン (Toolchains)」**ページで、ツールチェーンをクリックしてその「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックしてから、**「ツール統合 (Tool Integrations)」**をクリックします。
1. ツール統合の初回構成を行う必要がある場合は、そのツール統合のタイルで**「構成」**をクリックします。

  ![「構成」ボタン](images/toolchain_tile_configure.png)

 ツール統合の構成を完了したら、**「統合の保存 (Save Integration)」**をクリックします。
 
1. ツール統合の構成を更新する必要がある場合は、そのツール統合のタイルで、構成オプションにアクセスするためのメニューをクリックします。

  ![構成メニュー](images/toolchain_tile_menu.png)
 
 設定の更新を完了したら、**「統合の保存 (Save Integration)」**をクリックします。

## ツール統合の追加
{: #adding_a_tool_integration}

ツールチェーンにツール統合を追加して構成することができます。

1. DevOps ダッシュボードの**「ツールチェーン (Toolchains)」**ページで、ツールチェーンをクリックしてその「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックしてから、**「ツール統合 (Tool Integrations)」**をクリックします。
1. 追加するツール統合のリストを表示するために、追加ボタン (+) をクリックします。
1. 追加するツール統合をクリックします。
1. ツール統合を構成するために必要な情報を入力します。 
1. **「統合の作成 (Create Integration)」**をクリックして、ツールチェーンにツール統合を追加します。

## ツール統合の削除
{: #deleting_a_tool_integration}

ツールチェーンからツール統合を削除した場合、その削除を元に戻すことはできません。 

1. DevOps ダッシュボードの**「ツールチェーン (Toolchains)」**ページで、ツールチェーンをクリックしてその「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックしてから、**「ツール統合 (Tool Integrations)」**をクリックします。
1. 削除するツール統合のタイルで、構成オプションにアクセスするためのメニューをクリックします。
1. ツールチェーンからツール統合を削除するために、**「削除」**をクリックします。
1. **「削除」**をクリックして確認します。  

## アクセスの管理
{: #managing_access}

ユーザーにツールチェーンへのアクセス権を付与するには、ツールチェーンが関連付けられている組織にユーザーを追加します。それぞれのツールチェーンは特定の組織に関連付けられており、その組織のメンバーであるユーザーはだれでも、関連付けられたツールチェーンにアクセスできます。現在作業中の組織は、メニュー・バーに表示されます。
組織をクリックして別の組織に切り替えれば、別のツールチェーン・セットにアクセスできます。

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. DevOps ダッシュボードの**「ツールチェーン (Toolchains)」**ページで、管理対象のツールチェーンをクリックしてから、**「管理」**をクリックします。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックしてから、**「管理」**をクリックします。  
1. 組織へのリンクをクリックします。 
1. 「組織の管理」ページで、**「ユーザーの招待」**をクリックしてユーザーの E メール・アドレスを入力します。
1. {{site.data.keyword.Bluemix_notm}} の組織のユーザーを管理するための拡張権限を与える場合は、**「管理者」**、**「請求管理者」**、**「監査員」**のチェック・ボックスを 1 つ以上選択します。
1. **「招待 (INVITE)」**をクリックします。
1. **「保存」**をクリックします。

## ツールチェーンの削除
{: #deleting_a_toolchain}

ツールチェーンを削除し、関連付けられたツール統合のうちどれを削除するかを指定することができます。ツールチェーンを削除した場合、その削除を元に戻すことはできません。

1. DevOps ダッシュボードの**「ツールチェーン (Toolchains)」**ページで、削除するツールチェーンをクリックしてから、**「管理」**をクリックします。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックしてから、**「管理」**をクリックします。
1. **「ツールチェーンの削除 (Delete Toolchain)」**をクリックし、削除するツール統合を確認したり調整したりします。
1. ツールチェーンの名前を入力し、**「削除」**をクリックして削除を確認します。  

 **ヒント**: GitHub ツール統合を削除する場合、関連付けられている GitHub リポジトリーは GitHub から削除されません。リポジトリーは手動で GitHub から削除する必要があります。
