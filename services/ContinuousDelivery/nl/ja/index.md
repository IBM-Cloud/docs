---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.contdelivery_short}} 概説
{: #cd_getting_started}

最終更新日: 2016 年 11 月 18 日
{: .last-updated}  

アプリケーションのビルドとデプロイメントを自動化するツールチェーンが含まれる {{site.data.keyword.contdelivery_full}} を使用することによって、DevOps アプローチを取り入れることができます。開発、デプロイメント、運用の作業をサポートする単純なデプロイメント・ツールチェーンを作成することから始めることができます。
{: shortdesc}

{{site.data.keyword.Bluemix_notm}} カタログからサービス・タイルを選択して {{site.data.keyword.contdelivery_short}} のインスタンスを作成した後、サービスにどのように取り掛かるかを選択できます。
![Continuous Delivery ウェルカム・ページ](images/cd_landing_page.png)

 * 自動化パイプラインを使用して迅速に始めてアプリケーションをデプロイするには、「パイプラインで開始 (Starting with a pipeline)」セクションで、**[「ここから開始 (Start here)](#starting_with_a_pipeline)**をクリックします。後でさらにツールを追加できます。 
 * テンプレートから継続的デリバリー・ツールチェーンを作成して構成するには、「ツールチェーン・テンプレートから開始 (Starting from a toolchain template)」セクションで、**[「ここから開始 (Start here)」](#starting_from_a_toolchain_template)**をクリックします。ツールチェーンは、パイプラインのプランニング、開発、デプロイと、アプリケーションの管理のためのツールを統合したものです。ツールチェーンに対していつでもツールを追加したり削除したりできます。
 * ツールチェーンが既にある場合は、「ツールチェーン・テンプレートから開始 (Starting from a toolchain template)」セクションで、**「ツールチェーンを表示 (View your toolchains)」**をクリックします。ツールチェーンの扱いについて詳しくは、[Bluemix Public でのツールチェーンの使用](/docs/services/ContinuousDelivery/toolchains_using.html){: new_window}を参照してください。

## パイプラインで開始 (Starting with a pipeline)
{: #starting_with_a_pipeline}

パイプラインは、ビルドやデプロイメントなどを自動化します。自動化パイプラインを開始するには、テンプレートを選択し、GitHub リポジトリーの場所を指定します。

Cloud Foundry アプリケーションをデプロイするように構成された[パイプラインを作成する (新しいウィンドウでリンクが開きます)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} には、以下のステップを実行します。

1. **「Cloud Foundry」**をクリックします。
1. パイプラインに別の名前を使用する場合は、デフォルトの名前を変更します。{{site.data.keyword.Bluemix_notm}} では、パイプラインはその名前で識別されます。 
1. アプリケーションに別の名前を使用する場合は、デフォルトの名前を変更します。{{site.data.keyword.Bluemix_notm}} では、アプリケーションはその名前で識別されます。この名前は、パイプラインのデプロイ先のアプリケーションです。 
1. ツールチェーンがない場合は、デフォルトの名前が付いたツールチェーンが作成されます。ツールチェーンに別の名前を使用する場合は、名前を変更します。パイプラインはツールチェーンによって管理されます。ツールチェーンを使用して、他のツールやサービスと統合することで、パイプラインの機能を拡張できます。 

 **ヒント**: パイプラインとツールチェーンは組織に属します。ツールチェーンを持つ組織に属していれば、これらのツールチェーンの作成者でなくても使用することができます。
 
1. 使用するツールチェーンを選択するか、作成する新しいツールチェーンの名前を入力します。
1. GitHub リポジトリーの場所を指定します。

 **ヒント**: {{site.data.keyword.Bluemix_notm}} に GitHub へのアクセスをまだ認可していない場合は、**「認可 (Authorize)」** をクリックして GitHub の Web サイトにアクセスするよう求められます。アクティブな GitHub セッションがない場合は、ログインするよう求められます。**「アプリケーションを許可 (Authorize Application)」** をクリックして、{{site.data.keyword.Bluemix_notm}} が GitHub アカウントにアクセスできるようにします。アクティブな GitHub セッションはあるものの、最近パスワードを入力していない場合は、確認のために GitHub パスワードの入力を求められることがあります。

   * 既存の GitHub リポジトリーを使用する場合は、リポジトリーのタイプとして**「リンク (Link)」**を選択します。リポジトリーの場所を検索するか、選択可能なリポジトリーのリストからリポジトリーを選択します。
   
   * 空の GitHub リポジトリーを作成する場合は、リポジトリー・タイプとして**「新規」**を選択します。リポジトリーの名前を入力します。
   
   * GitHub リポジトリーのクローンを作成する場合は、リポジトリーのタイプに**「コピー」**を選択します。リポジトリーの場所を検索するか、選択可能なリポジトリーのリストからリポジトリーを選択します。
   
   * GitHub リポジトリーをフォークし、プル・リクエストで変更内容を提供できるようにする場合は、**「フォーク (Fork)」**を選択します。リポジトリーの場所を検索するか、選択可能なリポジトリーのリストからリポジトリーを選択します。
 
1. **「作成」**をクリックします。パイプラインが作成され、構成されて、ツールチェーンの「概要」ページに表示されます。
![パイプラインのタイル](images/cd_pipeline.png)
 
事前構成されたステージのない[空のパイプライン (新しいウィンドウでリンクが開きます)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} を作成するには、以下のようにします。

1. **「カスタム」**をクリックします。
1. パイプラインに別の名前を使用する場合は、デフォルトの名前を変更します。{{site.data.keyword.Bluemix_notm}} では、パイプラインはその名前で識別されます。 
1. ツールチェーンがない場合は、デフォルトの名前が付いたツールチェーンが作成されます。ツールチェーンに別の名前を使用する場合は、名前を変更します。パイプラインはツールチェーンによって管理されます。ツールチェーンを使用して、他のツールやサービスと統合することで、パイプラインの機能を拡張できます。
1. 使用するツールチェーンを選択するか、作成する新しいツールチェーンの名前を入力します。
1. **「作成」**をクリックします。空のパイプラインが作成され、ツールチェーンの「概要」ページにタイルとして表示されます。

## ツールチェーン・テンプレートから開始 (Starting from a toolchain template)
{: #starting_from_a_toolchain_template}

[テンプレート (新しいウィンドウでリンクが開きます)](https://console.ng.bluemix.net/devops/create){: new_window} から継続的デリバリー・ツールチェーンを作成して構成するには、以下のようにします。

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

# 関連リンク
{: #rellinks}

## チュートリアルとサンプル
{: #samples}

* [最初のツールチェーンの作成と使用 (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_flow){:new_window}
* [カスタム・ツールチェーンの作成 (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_custom){:new_window}
* [3 つのマイクロサービスを使用したアプリケーションの作成 (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices){:new_window}

## 関連リンク
{: #general}

* [マイクロサービスのツールチェーン (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [シンプルなツールチェーン (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM Bluemix Garage のメソッド (新しいウィンドウでリンクが開きます)](https://www.ibm.com/devops/method){:new_window}
