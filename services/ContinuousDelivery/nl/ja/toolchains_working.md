---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-28"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# ツルチェンの作成
{: #toolchains_getting_started}

*ツルチェン*は、開発、デプロイメント、運用の作業をサポトするツル統合のセットです。ツルチェンの集合的な機能は、個々のツル統合を合わせたものより優れています。
{: shortdesc}

{{site.data.keyword.Bluemix}} の Public 環境と Dedicated 環境で、オプンなツルチェンが使用可能です。ツルチェンの作成方法には、テンプレトを使用する方法と、アプリから作成する方法の 2 とおりがあります。

各ツルチェンは特定の組織と関連付けられており、その組織のメンバであるユザであればどのユザでも、組織に関連付けられたツルチェンのうちの任意のツルチェンのアクセス制御リストに追加できます。ツルチェンのアクセス制御について詳しくは、[アクセスの管理](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}を参照してください。ツルチェンを作成する前に、そのツルチェンを作成したい組織で作業していることを確認してください。作業している組織は、メニュ・バに表示されています。別の組織に切り替えるには、メニュ・バの組織をクリックしてから、切り替え先の組織を選択します。


##テンプレトからのツルチェンの作成   
{: #creating_a_toolchain_from_a_template}

特定のツル統合のセットを含む[ツルチェンを作成する ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/create){: new_window} ための開始点としてテンプレトを使用できます。テンプレトの使用方法について詳しくは、[IBM Cloud Garage Method ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/category/tools){:new_window} を参照してください。

1. {{site.data.keyword.Bluemix_notm}} Public を使用する場合、[{{site.data.keyword.Bluemix_notm}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://console.ng.bluemix.net){:new_window} にログインします。
1. {{site.data.keyword.Bluemix_notm}} Dedicated を使用する場合、{{site.data.keyword.Bluemix_notm}} の Dedicated 環境にログインします。
1. {{site.data.keyword.Bluemix_notm}} メニュ・バのメニュから、**「サビス」**をクリックして、**「DevOps」**をクリックします。
1. DevOps ダッシュボドの**「ツルチェン」**ペジで、**「ツルチェンの作成 (Create a Toolchain)」**をクリックします。
1. **「ツルチェンの作成 (Create a Toolchain)」**ペジで、ツルチェン・テンプレトをクリックします。
1. 作成しようとしているツルチェンの図を確認します。この図は、ツルチェン内の各ツル統合とそのライフサイクル・フェズを示しています。

 **ヒント**: 一部のツルチェン・テンプレトには、同じツル統合の複数のインスタンスが含まれています。例えば、{{site.data.keyword.Bluemix_notm}} Public の Microservices ツルチェン・テンプレトには、GitHub の 3 つのインスタンスと Delivery Pipeline の 3 つのインスタンス (3 つのマイクロサビスのそれぞれに対して 1 つずつ) が含まれています。

 次のイメジの図はその例です。ツルチェンを作成すると、ツルチェンを構成する各ツル統合がこの図に表示されます。
![ツルチェンの図](images/toolchain_diagram.png)

1. ツルチェン設定のデフォルト情報を確認します。ツルチェンの名前は、そのツルチェンを {{site.data.keyword.Bluemix_notm}} 内で識別するためのものです。別の名前を使用する場合は、ツルチェンの名前を変更します。  
1. 「ツル統合 (Tool Integrations)」セクションで、ツルチェンに構成する各ツル統合を選択します。いくつかのツル統合は、構成を必要としません。ツル統合の構成については、[ツル統合の構成](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}を参照してください。
1. **「作成」**をクリックします。以下のようにいくつかのステップが自動的に実行されて、ツルチェンがセットアップされます。セットアップされるツル統合は、どのツルチェン・テンプレトを選択したのか、また、{{site.data.keyword.Bluemix_notm}} Public と {{site.data.keyword.Bluemix_notm}} Dedicated のどちらを使用しているのかによって異なります。例えば、Microservices ツルチェンを {{site.data.keyword.Bluemix_notm}} Public で作成する場合、以下のステップが実行されます。

 * ツルチェンが作成されます。
 * Delivery Pipeline を構成した場合は、パイプラインが作成されて起動します。
 * Sauce Labs を構成した場合は、パイプラインに Sauce Labs テスト・ジョブを追加するようにツルチェンがセットアップされます。
 * PagerDuty を構成した場合は、指定した PagerDuty サビスにアラト通知を送信するようにツルチェンがセットアップされます。
 * Slack を構成した場合は、指定した Slack チャネルにデプロイメント状況に関する通知を送信するようにツルチェンがセットアップされます。
 * GitHub などのソス・コド・ツル統合を構成した場合、サンプル GitHub リポジトリが GitHub アカウントに複製されます。


##アプリからのツルチェンの作成
{: #creating_a_toolchain_from_an_app}

アプリからツルチェンを作成することができます。ツルチェンは、継続的な開発、デプロイメント、モニタなどをサポトすることができ、アプリと関連付けられます。各アプリをツルチェンと関連付けることができます。ツルチェンの GitHub リポジトリまたは {{site.data.keyword.ghe_short}} リポジトリに変更をプッシュすると、パイプラインは自動的にアプリをビルドしてデプロイします。  

1. アプリの「概要」ペジの「継続的デリバリ」カドで、**「有効化」**をクリックします。{{site.data.keyword.Bluemix_notm}} Public を使用する場合、アプリは、アプリ・スタタ・コドが取り込まれた新規 GitHub リポジトリからの継続的デリバリ用に構成されます。{{site.data.keyword.Bluemix_notm}} Dedicated を使用する場合、アプリは、アプリ・スタタ・コドが取り込まれた新規 GitHub リポジトリまたは {{site.data.keyword.ghe_short}} リポジトリからの継続的デリバリ用に構成されます。
1. ツルチェン作成ペジで、作成しようとしているツルチェンの図を確認します。この図は、ツルチェン内の各ツル統合とそのライフサイクル・フェズを示しています。
1. ツルチェン設定のデフォルト情報を確認します。ツルチェンの名前は、そのツルチェンを {{site.data.keyword.Bluemix_notm}} 内で識別するためのものです。別の名前を使用する場合は、ツルチェンの名前を変更します。
1. 「ツル統合 (Tool Integrations)」セクションで、ツルチェンに構成する各ツル統合を選択します。いくつかのツル統合は、構成を必要としません。ツル統合の構成については、[ツル統合の構成](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}を参照してください。
1. **「作成」**をクリックします。以下のようにいくつかのステップが自動的に実行されて、ツルチェンがセットアップされます。セットアップされるツル統合は、{{site.data.keyword.Bluemix_notm}} Public と {{site.data.keyword.Bluemix_notm}} Dedicated のどちらでツルチェンを使用するのかによって異なります。例えば、{{site.data.keyword.Bluemix_notm}} Public でアプリからツルチェンを作成する場合、以下のステップが実行されます。

 * ツルチェンが作成されます。
 * Delivery Pipeline を構成した場合は、パイプラインが作成されて起動します。
 * GitHub を構成した場合は、GitHub アカウントにサンプル GitHub リポジトリが複製されます。


##ツルチェンの表示
{: #viewing_a_toolchain}

ツルチェンとそのツル統合を構成した後、ツルチェンのビジュアル表示を確認することができます。

1. DevOps ダッシュボドの**「ツルチェン」**ペジで、ツルチェンをクリックしてその「概要」ペジを開きます。あるいは、アプリの「概要」ペジの「継続的デリバリ」カドで、**「ツルチェンの表示」**をクリックします。次に、**「概要」**をクリックします。
2. ツルチェン内にあるツル統合にアクセスするには、ツルをクリックします。

 **ヒント**: GitHub リポジトリ、{{site.data.keyword.ghe_short}} リポジトリ、または Git リポジトリが複数ある場合、各リポジトリはそれぞれ固有のカドで表されるため、同じツル統合に対して複数のカドが存在することがあります。複数のパイプラインがある場合、各パイプラインはそれぞれ固有のカドで表されるため、同じツル統合に対して複数のカドが存在することがあります。例えば、Microservices ツルチェンを作成する場合、3 つのマイクロサビスのそれぞれが固有の GitHub リポジトリ、{{site.data.keyword.ghe_short}} リポジトリ、または Git リポジトリと、固有のパイプラインを持ちます。
