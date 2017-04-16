---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# ツールチェーンでの作業
{: #toolchains_getting_started}

最終更新日: 2016 年 11 月 17 日
{: .last-updated}  

*ツールチェーン*は、開発、デプロイメント、運用の作業をサポートするツール統合のセットです。ツールチェーンの集合的な機能は、個々のツール統合を合わせたものより優れています。
{: shortdesc}

ツールチェーンは、{{site.data.keyword.Bluemix}} の Public 環境および Dedicated 環境で使用可能です。ツールチェーンの作成方法には、テンプレートを使用する方法と、アプリから作成する方法の 2 とおりがあります。{{site.data.keyword.Bluemix_notm}} Public の場合、ツールチェーンは米国南部地域でのみ利用可能です。

## ツールチェーンの概説: Public
{: #getting_started_public}

それぞれのツールチェーンは特定の組織に関連付けられており、その組織のメンバーであるユーザーはだれでも、関連付けられたツールチェーンにアクセスできます。ツールチェーンを作成する前に、そのツールチェーンを作成したい組織で作業していることを確認してください。現在作業を行なっている組織がメニュー・バーに表示されます。別の組織に切り替えるには、メニュー・バーの組織をクリックしてから、切り替え先の組織を選択します。

### テンプレートからのツールチェーンの作成   
{: #creating_a_toolchain_from_a_template}

特定のツール統合のセットを含む[ツールチェーンを作成する (新しいウィンドウでリンクが開きます)](https://console.ng.bluemix.net/devops/create){: new_window} ための開始点として、テンプレートを使用できます。テンプレートの使用方法について詳しくは、[IBM Bluemix Garage Method (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/category/tools){:new_window} を参照してください。

1. [{{site.data.keyword.Bluemix_notm}} (新しいウィンドウでリンクが開きます)](http://console.ng.bluemix.net){:new_window} にログインします。{{site.data.keyword.Bluemix_notm}} ダッシュボードが開き、組織でアクティブな {{site.data.keyword.Bluemix_notm}} スペースの概要が示されます。
1. ハンバーガー・メニュー (三本線のアイコン) から、**「サービス」**をクリックし、**「DevOps」**をクリックします。
1. DevOps ダッシュボードの**「ツールチェーン」**ページで、**「ツールチェーンの作成 (Create a Toolchain)」**をクリックします。
1. **「ツールチェーンの作成 (Create a Toolchain)」**ページで、ツールチェーン・テンプレートをクリックします。
1. 作成しようとしているツールチェーンの図を確認します。この図は、ツールチェーン内の各ツール統合とそのライフサイクル・フェーズを示しています。次のイメージの図はその例です。ツールチェーンを作成すると、ツールチェーンを構成する各ツール統合がこの図に表示されます。
![ツールチェーンの図](images/toolchain_diagram.png)

1. ツールチェーン設定のデフォルト情報を確認します。ツールチェーンの名前は、そのツールチェーンを {{site.data.keyword.Bluemix_notm}} 内で識別するためのものです。別の名前を使用する場合は、ツールチェーンの名前を変更します。  
1. 「構成可能な統合 (Configurable Integrations)」セクションで、ツールチェーンに構成する各ツール統合を選択します。いくつかのツール統合は、構成を必要としません。ツール統合の構成については、[ツール統合の構成](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}を参照してください。
1. **「作成」**をクリックします。以下のようにいくつかのステップが自動的に実行されて、ツールチェーンがセットアップされます。

 * ツールチェーンが作成されます。
 * Delivery Pipeline ツール統合を構成した場合は、パイプラインが作成されて起動します。
 * Sauce Labs ツール統合を構成した場合は、ジョブをパイプラインに追加してテストを実行するように Sauce Labs がセットアップされます。
 * PagerDuty ツール統合を構成した場合は、指定したサービスにアラート通知を送信するように PagerDuty がセットアップされます。
 * Slack ツール統合を構成した場合は、指定したチャネルにデプロイメント状況に関する通知を送信するように Slack がセットアップされます。
 * GitHub ツール統合を構成した場合は、GitHub アカウントにサンプル GitHub リポジトリーが複製されます。


### アプリからのツールチェーンの作成
{: #creating_a_toolchain_from_an_app}

アプリからツールチェーンを作成することができます。ツールチェーンは、継続的な開発、デプロイメント、モニターなどをサポートすることができ、アプリと関連付けられます。各アプリをツールチェーンと関連付けることができます。ツールチェーンの GitHub リポジトリーに変更をプッシュすると、パイプラインが自動的にアプリをビルドしてデプロイします。  

1. アプリの「概要」ページの「継続的なデリバリー」タイルで、**「有効化 (Enable)」**をクリックします。アプリ・スターター・コードが取り込まれた新規 GitHub リポジトリーからアプリの継続的デリバリーが構成されます。
1. ツールチェーン作成ページで、作成しようとしているツールチェーンの図を確認します。この図は、ツールチェーン内の各ツール統合とそのライフサイクル・フェーズを示しています。
1. ツールチェーン設定のデフォルト情報を確認します。ツールチェーンの名前は、そのツールチェーンを {{site.data.keyword.Bluemix_notm}} 内で識別するためのものです。別の名前を使用する場合は、ツールチェーンの名前を変更します。
1. 「構成可能な統合 (Configurable Integrations)」セクションで、ツールチェーンに構成する各ツール統合を選択します。いくつかのツール統合は、構成を必要としません。ツール統合の構成については、[ツール統合の構成](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}を参照してください。
1. **「作成」**をクリックします。以下のようにいくつかのステップが自動的に実行されて、ツールチェーンがセットアップされます。

 * ツールチェーンが作成されます。
 * Delivery Pipeline ツール統合を構成した場合は、パイプラインが作成されて起動します。
 * Sauce Labs ツール統合を構成した場合は、ジョブをパイプラインに追加してテストを実行するように Sauce Labs がセットアップされます。
 * PagerDuty ツール統合を構成した場合は、指定したサービスにアラート通知を送信するように PagerDuty がセットアップされます。
 * Slack ツール統合を構成した場合は、指定したチャネルにデプロイメント状況に関する通知を送信するように Slack がセットアップされます。
 * GitHub ツール統合を構成した場合は、GitHub アカウントにサンプル GitHub リポジトリーが複製されます。


## ツールチェーンの概説: Dedicated
{: #getting_started_dedicated}

それぞれのツールチェーンは特定の組織に関連付けられており、その組織のメンバーであるユーザーはだれでも、関連付けられたツールチェーンにアクセスできます。ツールチェーンを作成する前に、メニュー・バーの **{{site.data.keyword.avatar}}** アイコンをクリックして、「アカウントとサポート」ウィジェットを開き、作業中の組織を表示します。その組織が、ツールチェーンを作成する対象の組織ではない場合、別の組織に切り替えます。

### テンプレートからのツールチェーンの作成   
{: #creating_a_toolchain_from_a_template_dedicated}

特定のツール統合のセットを含むツールチェーンを作成するための開始点として、テンプレートを使用できます。

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードの**「DEVOPS」**タブで、ツールチェーンを作成するための追加ボタン (+) をクリックします。
1. **「ツールチェーンの作成 (Create a Toolchain)」**ページで、ツールチェーン・テンプレートをクリックします。 
1. 作成しようとしているツールチェーンの図を確認します。この図は、ツールチェーン内の各ツール統合とそのライフサイクル・フェーズを示しています。次のイメージの図はその例です。ツールチェーンを作成すると、ツールチェーンを構成する各ツール統合がこの図に表示されます。
![Dedicated ツールチェーンの図](images/toolchain_dedicated_diagram.png)

1. ツールチェーン設定のデフォルト情報を確認します。ツールチェーンの名前は、そのツールチェーンを {{site.data.keyword.Bluemix_notm}} 内で識別するためのものです。同じ名前のツールチェーンが既に存在する場合や、別の名前を使用する場合は、ツールチェーンの名前を変更します。  
1. 「構成可能な統合 (Configurable Integrations)」セクションで、ツールチェーンに構成する各ツール統合を選択します。いくつかのツール統合は、構成を必要としません。ツール統合の構成については、[ツール統合の構成](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}を参照してください。
1. **「作成」**をクリックします。以下のようにいくつかのステップが自動的に実行されて、ツールチェーンがセットアップされます。

 * ツールチェーンが作成されます。
 * Delivery Pipeline ツール統合を構成した場合は、パイプラインが作成されて起動します。
 * PagerDuty ツール統合を構成した場合は、指定したサービスにアラート通知を送信するように PagerDuty がセットアップされます。
 * Slack ツール統合を構成した場合は、指定したチャネルにデプロイメント状況に関する通知を送信するように Slack がセットアップされます。
 * GitHub Enterprise ツール統合を構成した場合は、サンプルの GitHub Enterprise リポジトリーが GitHub Enterprise アカウントに複製されます。


### アプリからのツールチェーンの作成
{: #creating_a_toolchain_from_an_app_dedicated}

アプリからツールチェーンを作成することができます。ツールチェーンは、継続的な開発、デプロイメント、モニターなどをサポートすることができ、アプリと関連付けられます。各アプリをツールチェーンと関連付けることができます。ツールチェーンの GitHub Enterprise リポジトリーに変更をプッシュすると、パイプラインが自動的にアプリをビルドしてデプロイします。  

1. アプリの「概要」ページの右上隅にある**「ツールチェーンの追加」**をクリックします。アプリは、アプリ・スターター・コードが取り込まれた新規 GitHub Enterprise リポジトリーからの継続的なデリバリー用に構成されます。
1. ツールチェーン作成ページで、作成しようとしているツールチェーンの図を確認します。この図は、ツールチェーン内の各ツール統合とそのライフサイクル・フェーズを示しています。
1. ツールチェーン設定のデフォルト情報を確認します。ツールチェーンの名前は、そのツールチェーンを {{site.data.keyword.Bluemix_notm}} 内で識別するためのものです。同じ名前のツールチェーンが既に存在する場合や、別の名前を使用する場合は、ツールチェーンの名前を変更します。
1. 「構成可能な統合 (Configurable Integrations)」セクションで、ツールチェーンに構成する各ツール統合を選択します。いくつかのツール統合は、構成を必要としません。ツール統合の構成については、[ツール統合の構成](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}を参照してください。
1. **「作成」**をクリックします。以下のようにいくつかのステップが自動的に実行されて、ツールチェーンがセットアップされます。

 * ツールチェーンが作成されます。
 * Delivery Pipeline ツール統合を構成した場合は、パイプラインが作成されて起動します。
 * PagerDuty ツール統合を構成した場合は、指定したサービスにアラート通知を送信するように PagerDuty がセットアップされます。
 * Slack ツール統合を構成した場合は、指定したチャネルにデプロイメント状況に関する通知を送信するように Slack がセットアップされます。
 * GitHub Enterprise ツール統合を構成した場合は、サンプルの GitHub Enterprise リポジトリーが GitHub Enterprise アカウントに複製されます。


## ツールチェーンの表示
{: #viewing_a_toolchain}

ツールチェーンとそのツール統合を構成した後、ツールチェーンのビジュアル表示を確認することができます。

* {{site.data.keyword.Bluemix_notm}} Public を使用している場合、DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックして、その「概要」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー」タイルで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。 
   
* {{site.data.keyword.Bluemix_notm}} Dedicated を使用している場合、ダッシュボードの**「DEVOPS」**タブでツールチェーンをクリックして、その「ツール統合 (Tool Integrations)」ページを開きます。あるいは、アプリの「概要」ページの右上隅の**「ツールチェーンの表示」**をクリックします。

* ツールチェーン内のツール統合にアクセスするには、そのツールのタイルをクリックします。 
 
 **ヒント**: GitHub または GitHub Enterprise のリポジトリーが複数ある場合は、それぞれのリポジトリーに対応するタイルが表示されるので、同じツール統合に対して複数のタイルが存在することがあります。


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
