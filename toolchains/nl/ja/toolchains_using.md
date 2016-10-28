---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} Public でのツールチェーンの使用
{: #toolchains-using}

*最終更新日: 2016 年 8 月 12 日*
{: .last-updated}

ツールチェーンを使用して、毎日の開発、デプロイメント、および運用の作業における生産性を上げることができます。ツールチェーンをセットアップした後、ツール統合の追加、削除、または構成と、ツールチェーンへのアクセスの管理を行うことができます。
{: shortdesc}

**重要**: この機能は試験的なものです。ツールチェーンは変更される可能性があり、変更により前のバージョンとの互換性がなくなる場合もあります。実稼働環境での使用は推奨されません。ツールチェーンは「米国南部」地域でのみ使用可能です。

## ツール統合の構成
{: #configuring_a_tool_integration}

ツールチェーンを作成したときにツール統合の構成を延期した場合、ツールチェーンのタイルに**「構成」**ボタンが表示されます。ツールチェーンを作成したときにツール統合を構成した場合、構成設定を更新できます。

1. DevOps ダッシュボードの**「ツールチェーン」**タブでツールチェーンをクリックして、そのツールチェーンの「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの「継続的なデリバリー」タイルで、**「ツールチェーンの表示」**をクリックし、その後で**「ツール統合 (Tool Integrations)」**をクリックします。
1. 初めてツール統合を構成する必要がある場合、そのツール統合のタイルで**「構成」**をクリックします。

  ![「構成」ボタン](images/toolchain_tile_configure.png)

 ツール統合の構成が完了したら、**「統合の保存 (Save Integration)」**をクリックします。
 
1. ツール統合の構成を更新する必要がある場合、そのツール統合のタイルで、構成オプションにアクセスするためのメニューをクリックします。

  ![構成メニュー](images/toolchain_tile_menu.png)
 
 設定の更新が完了したら、**「統合の保存 (Save Integration)」**をクリックします。

## ツール統合の追加
{: #adding_a_tool_integration}

ツールチェーン用のツール統合を追加および構成できます。

1. DevOps ダッシュボードの**「ツールチェーン」**タブでツールチェーンをクリックして、そのツールチェーンの「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの「継続的なデリバリー」タイルで、**「ツールチェーンの表示」**をクリックし、その後で**「ツール統合 (Tool Integrations)」**をクリックします。
1. 追加するツール統合のリストを表示するため、追加ボタン (+) をクリックします。
1. 追加したいツール統合をクリックします。
1. そのツール統合を構成するための必要情報を入力します。 
1. そのツール統合をツールチェーンに追加するため、**「統合の作成 (Create Integration)」**をクリックします。

## ツール統合の削除
{: #deleting_a_tool_integration}

ツール統合をツールチェーンから削除すると、その削除を取り消すことはできません。 

1. DevOps ダッシュボードの**「ツールチェーン」**タブでツールチェーンをクリックして、そのツールチェーンの「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの「継続的なデリバリー」タイルで、**「ツールチェーンの表示」**をクリックし、その後で**「ツール統合 (Tool Integrations)」**をクリックします。
1. 削除したいツール統合のタイルで、構成オプションにアクセスするためのメニューをクリックします。
1. そのツール統合をツールチェーンから削除するため、**「削除」**をクリックします。
1. 確認のため**「削除」**をクリックします。  

## アクセスの管理
{: #managing_access}

ツールチェーンへのユーザーのアクセスを認可するには、そのツールチェーンが関連付けられた組織にユーザーを追加します。各ツールチェーンは特定の組織と関連付けられていて、その組織のメンバーであればどのユーザーでも、関連付けられたツールチェーンにアクセスできます。メニュー・バーの「**{{site.data.keyword.avatar}}**」アイコン ![「アバター」アイコン](../icons/i-avatar-icon.svg) をクリックして「アカウントとサポート」ウィジェットを開き、現在作業している組織を確認してください。別のツールチェーンのセットにアクセスするには、別の組織に切り替えてください。

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. DevOps ダッシュボードの**「ツールチェーン」**タブで、管理するツールチェーンをクリックし、**「管理」**をクリックします。あるいは、アプリの「概要」ページの「継続的なデリバリー」タイルで、**「ツールチェーンの表示」**をクリックし、その後で**「管理」**をクリックします。  
1. 組織へのリンクをクリックします。 
1. 「組織の管理」ページで、**「ユーザーの招待」**をクリックし、ユーザーの E メール・アドレスを入力します。
1. {{site.data.keyword.Bluemix_notm}} 組織内のユーザーを管理するための上級アクセス権を付与したい場合、**「管理者」**、**「請求管理者」**、および**「監査員」**チェック・ボックスのうちの 1 つ以上を選択します。
1. **「招待」**をクリックします。
1. **「保存」**をクリックします。

## ツールチェーンの削除
{: #deleting_a_toolchain}

ツールチェーンを削除し、関連付けられたツール統合のうちどれを削除するのかを指定することができます。ツールチェーンを削除すると、その削除を取り消すことはできません。

1. DevOps ダッシュボードの**「ツールチェーン」**タブで、削除するツールチェーンをクリックし、**「管理」**をクリックします。あるいは、アプリの「概要」ページの「継続的なデリバリー」タイルで、**「ツールチェーンの表示」**をクリックし、その後で**「管理」**をクリックします。
1. **「ツールチェーンの削除 (Delete Toolchain)」**をクリックし、削除しようとしているツール統合を検討または調整します。
1. 削除を確認するため、ツールチェーンの名前を入力し、**「削除」**をクリックします。  

 **ヒント**: GitHub ツール統合を削除する場合、関連付けられた GitHub リポジトリーは GitHub から削除されません。リポジトリーは手動で GitHub から削除する必要があります。
