---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} Dedicated でのツールチェーンの使用
{: #toolchains-using_dedicated}

最終更新日: 2016 年 11 月 17 日
{: .last-updated}

ツールチェーンを使用して、日々の開発、デプロイメント、運用の作業における生産性を向上させることができます。ツールチェーンをセットアップした後、ツール統合の追加、削除、構成と、ツールチェーンへのアクセスの管理を行うことができます。
{: shortdesc}

## ツール統合の構成
{: #configuring_a_tool_integration_dedicated}

ツールチェーンを作成したときにツール統合の構成を延期した場合、そのタイルに**「構成」**ボタンが表示されます。ツールチェーンを作成したときにツール統合を構成した場合、構成設定を更新できます。

1. ダッシュボードの**「DevOps」**タブで、ツールチェーンをクリックして、その「ツール統合」ページを開きます。または、アプリの「概要」ページの右上隅の**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合」**をクリックします。
1. 最初にツール統合を構成する必要がある場合、そのタイルで**「構成」**をクリックします。

  ![構成ボタン](images/toolchain_tile_configure.png)

 ツール統合の構成が完了したら、**「統合の保存」**をクリックします。
 
1. ツール統合の構成を更新する必要がある場合、そのタイルでメニューをクリックして構成オプションにアクセスします。

  ![構成メニュー](images/toolchain_tile_menu.png)
 
 設定の更新が完了したら、**「統合の保存」**をクリックします。

## ツール統合の追加
{: #adding_a_tool_integration_dedicated}

ツールチェーンにツール統合を追加して構成することができます。

1. ダッシュボードの**「DevOps」**タブで、ツールチェーンをクリックして、その「ツール統合」ページを開きます。または、アプリの「概要」ページの右上隅の**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合」**をクリックします。
1. 追加するツール統合のリストを表示するには、追加ボタン (+) をクリックします。
1. 追加するツール統合をクリックします。
1. 必要な情報を入力し、ツール統合を構成します。 
1. **「統合の作成」**をクリックし、ツールチェーンにツール統合を追加します。

## ツール統合の削除
{: #deleting_a_tool_integration}

ツールチェーンからツール統合を削除する場合、削除を取り消すことはできません。 

1. ダッシュボードの**「DevOps」**タブで、ツールチェーンをクリックして、その「ツール統合」ページを開きます。または、アプリの「概要」ページの右上隅の**「ツールチェーンの表示」**をクリックします。次に、**「ツール統合」**をクリックします。
1. 削除するツール統合のタイルで、メニューをクリックして構成オプションにアクセスします。
1. ツールチェーンからツール統合を削除するには、**「削除」**をクリックします。
1. **「削除」**をクリックして確認します。 

## アクセスの管理
{: #managing_access_dedicated}

ツールチェーンが関連付けられた組織にユーザーを追加することにより、それらのユーザーはツールチェーンにアクセスできるようになります。各ツールチェーンは特定の組織と関連付けられており、その組織のメンバーであればどのユーザーでも、関連付けられたツールチェーンにアクセスできます。現在作業している組織を表示するには、メニュー・バーで **{{site.data.keyword.avatar}}** アイコンをクリックします。ツールチェーンの別のセットにアクセスするには、別の組織に切り替えます。

ユーザーを {{site.data.keyword.Bluemix}} 組織およびスペースに追加すると、ユーザーは {{site.data.keyword.Bluemix_notm}} ID とパスワードを使用することによって GitHub Enterprise にログインできるようになります。ユーザーがログインするときに、ユーザーのためのアカウントが作成されます。{{site.data.keyword.Bluemix_notm}} 組織およびスペースにユーザーを追加しても、それらのユーザーが GitHub Enterprise リポジトリーに自動的に追加されることはありません。リポジトリーの管理者特権を持つ者がユーザーの追加を行う必要があります。詳しくは、[Dedicated GitHub Enterprise の使用](/docs/services/ghededicated/index.html){: new_window}を参照してください。


ユーザーを追加するには、以下の手順に従います。 

1. ダッシュボードの**「DevOps」**タブで、ツールチェーンをクリックして、その「ツール統合」ページを開きます。次に、**「管理」**をクリックします。または、アプリの「概要」ページの右上隅の**「ツールチェーンの表示」**をクリックします。次に、**「管理」**をクリックします。  
1. 組織へのリンクをクリックします。 
1. 「組織の管理」ページで、**「ユーザーの招待」**をクリックし、ユーザーの E メール・アドレスを入力します。
1. {{site.data.keyword.Bluemix_notm}} 組織でユーザーを管理する拡張権限を付与する場合、**「管理者」**、**「請求管理者」**、または**「監査員」**チェック・ボックスの 1 つ以上を選択します。
1. **「招待 (INVITE)」**をクリックします。
1. **「保存」**をクリックします。

## ツールチェーンの削除
{: #deleting_a_toolchain_dedicated}

ツールチェーンを削除し、それに関連付けられたツール統合のうちどれを削除するかを指定することができます。ツールチェーンを削除すると、削除を取り消すことはできません。

1. ダッシュボードの**「DevOps」**タブで、ツールチェーンをクリックして、その「ツール統合」ページを開きます。次に、**「管理」**をクリックします。または、アプリの「概要」ページの右上隅の**「ツールチェーンの表示」**をクリックします。次に、**「管理」**をクリックします。
1. **「ツールチェーンの削除」**をクリックし、削除するツール統合を検討/調整します。
1. ツールチェーンの名前を入力し、**「削除」**をクリックして、削除を確認します。

 **ヒント**: GitHub Enterprise ツール統合を削除するときに、関連付けられている GitHub Enterprise リポジトリーは GitHub Enterprise から削除されません。リポジトリーを GitHub Enterprise から手動で削除する必要があります。


# 関連リンク
{: #rellinks}

## チュートリアルとサンプル
{: #samples}

* [最初のツールチェーンの作成と使用 (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [カスタム・ツールチェーンの作成 (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [3 つのマイクロサービスを使用したアプリケーションの作成 (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}
* [{{site.data.keyword.Bluemix_notm}} Dedicated (Beta) でのテンプレートからのツールチェーンの作成 (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_template_flow){:new_window}
* [{{site.data.keyword.Bluemix_notm}} Dedicated (ベータ) でのアプリからのツールチェーンの作成 (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/tutorials/tutorial_dedicated_toolchain_app_flow){:new_window}

## 関連リンク
{: #general}

* [マイクロサービスのツールチェーン (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [シンプルなツールチェーン (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage のメソッド (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method){:new_window}
