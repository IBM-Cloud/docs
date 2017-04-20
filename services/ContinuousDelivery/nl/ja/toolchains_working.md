---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-7"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# ツールチェーンの作成
{: #toolchains_getting_started}

*ツールチェーン*は、開発、デプロイメント、運用の作業をサポートするツール統合のセットです。ツールチェーンの集合的な機能は、個々のツール統合を合わせたものより優れています。
{: shortdesc}

{{site.data.keyword.Bluemix}} の Public 環境と Dedicated 環境で、オープンなツールチェーンが使用可能です。ツールチェーンの作成方法には、テンプレートを使用する方法と、アプリから作成する方法の 2 とおりがあります。{{site.data.keyword.Bluemix_notm}} Public の場合、ツールチェーンは米国南部地域でのみ利用可能です。

各ツールチェーンは特定の組織と関連付けられており、その組織のメンバーであるユーザーであればどのユーザーでも、組織に関連付けられたツールチェーンのうちの任意のツールチェーンのアクセス制御リストに追加できます。ツールチェーンのアクセス制御について詳しくは、[アクセスの管理](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){: new_window}を参照してください。ツールチェーンを作成する前に、そのツールチェーンを作成したい組織で作業していることを確認してください。作業している組織は、メニュー・バーに表示されています。別の組織に切り替えるには、メニュー・バーの組織をクリックしてから、切り替え先の組織を選択します。


##テンプレートからのツールチェーンの作成   
{: #creating_a_toolchain_from_a_template}

特定のツール統合のセットを含む[ツールチェーンを作成する ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/devops/create){: new_window} ための開始点としてテンプレートを使用できます。テンプレートの使用方法について詳しくは、[IBM Cloud Garage Method ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/devops/method/category/tools){:new_window} を参照してください。

1. {{site.data.keyword.Bluemix_notm}} Public を使用する場合、[{{site.data.keyword.Bluemix_notm}} ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://console.ng.bluemix.net){:new_window} にログインします。
1. {{site.data.keyword.Bluemix_notm}} Dedicated を使用する場合、{{site.data.keyword.Bluemix_notm}} の Dedicated 環境にログインします。
1. ハンバーガー・メニュー (三本線のアイコン) から、**「サービス」**をクリックし、**「DevOps」**をクリックします。
1. DevOps ダッシュボードの**「ツールチェーン」**ページで、**「ツールチェーンの作成 (Create a Toolchain)」**をクリックします。
1. **「ツールチェーンの作成 (Create a Toolchain)」**ページで、ツールチェーン・テンプレートをクリックします。
1. 作成しようとしているツールチェーンの図を確認します。この図は、ツールチェーン内の各ツール統合とそのライフサイクル・フェーズを示しています。

 **ヒント**: 一部のツールチェーン・テンプレートには、同じツール統合の複数のインスタンスが含まれています。例えば、{{site.data.keyword.Bluemix_notm}} Public の Microservices ツールチェーン・テンプレートには、GitHub の 3 つのインスタンスと Delivery Pipeline の 3 つのインスタンス (3 つのマイクロサービスのそれぞれに対して 1 つずつ) が含まれています。

 次のイメージの図はその例です。ツールチェーンを作成すると、ツールチェーンを構成する各ツール統合がこの図に表示されます。
![ツールチェーンの図](images/toolchain_diagram.png)

1. ツールチェーン設定のデフォルト情報を確認します。ツールチェーンの名前は、そのツールチェーンを {{site.data.keyword.Bluemix_notm}} 内で識別するためのものです。別の名前を使用する場合は、ツールチェーンの名前を変更します。  
1. 「ツール統合 (Tool Integrations)」セクションで、ツールチェーンに構成する各ツール統合を選択します。いくつかのツール統合は、構成を必要としません。ツール統合の構成については、[ツール統合の構成](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}を参照してください。
1. **「作成」**をクリックします。以下のようにいくつかのステップが自動的に実行されて、ツールチェーンがセットアップされます。セットアップされるツール統合は、どのツールチェーン・テンプレートを選択したのか、また、{{site.data.keyword.Bluemix_notm}} Public と {{site.data.keyword.Bluemix_notm}} Dedicated のどちらを使用しているのかによって異なります。例えば、Microservices ツールチェーンを {{site.data.keyword.Bluemix_notm}} Public で作成する場合、以下のステップが実行されます。

 * ツールチェーンが作成されます。
 * Delivery Pipeline を構成した場合は、パイプラインが作成されて起動します。
 * Sauce Labs を構成した場合は、パイプラインに Sauce Labs テスト・ジョブを追加するようにツールチェーンがセットアップされます。
 * PagerDuty を構成した場合は、指定した PagerDuty サービスにアラート通知を送信するようにツールチェーンがセットアップされます。
 * Slack を構成した場合は、指定した Slack チャネルにデプロイメント状況に関する通知を送信するようにツールチェーンがセットアップされます。
 * GitHub などのソース・コード・ツール統合を構成した場合、サンプル GitHub リポジトリーが GitHub アカウントに複製されます。


##アプリからのツールチェーンの作成
{: #creating_a_toolchain_from_an_app}

アプリからツールチェーンを作成することができます。ツールチェーンは、継続的な開発、デプロイメント、モニターなどをサポートすることができ、アプリと関連付けられます。各アプリをツールチェーンと関連付けることができます。ツールチェーンの GitHub リポジトリーまたは {{site.data.keyword.ghe_short}} リポジトリーに変更をプッシュすると、パイプラインは自動的にアプリをビルドしてデプロイします。  

1. アプリの「概要」ページの「継続的デリバリー」カードで、**「有効化」**をクリックします。{{site.data.keyword.Bluemix_notm}} Public を使用する場合、アプリは、アプリ・スターター・コードが取り込まれた新規 GitHub リポジトリーからの継続的デリバリー用に構成されます。{{site.data.keyword.Bluemix_notm}} Dedicated を使用する場合、アプリは、アプリ・スターター・コードが取り込まれた新規 GitHub リポジトリーまたは {{site.data.keyword.ghe_short}} リポジトリーからの継続的デリバリー用に構成されます。
1. ツールチェーン作成ページで、作成しようとしているツールチェーンの図を確認します。この図は、ツールチェーン内の各ツール統合とそのライフサイクル・フェーズを示しています。
1. ツールチェーン設定のデフォルト情報を確認します。ツールチェーンの名前は、そのツールチェーンを {{site.data.keyword.Bluemix_notm}} 内で識別するためのものです。別の名前を使用する場合は、ツールチェーンの名前を変更します。
1. 「ツール統合 (Tool Integrations)」セクションで、ツールチェーンに構成する各ツール統合を選択します。いくつかのツール統合は、構成を必要としません。ツール統合の構成については、[ツール統合の構成](/docs/services/ContinuousDelivery/toolchains_integrations.html){: new_window}を参照してください。
1. **「作成」**をクリックします。以下のようにいくつかのステップが自動的に実行されて、ツールチェーンがセットアップされます。セットアップされるツール統合は、{{site.data.keyword.Bluemix_notm}} Public と {{site.data.keyword.Bluemix_notm}} Dedicated のどちらでツールチェーンを使用するのかによって異なります。例えば、{{site.data.keyword.Bluemix_notm}} Public でアプリからツールチェーンを作成する場合、以下のステップが実行されます。

 * ツールチェーンが作成されます。
 * Delivery Pipeline を構成した場合は、パイプラインが作成されて起動します。
 * GitHub を構成した場合は、GitHub アカウントにサンプル GitHub リポジトリーが複製されます。


##ツールチェーンの表示
{: #viewing_a_toolchain}

ツールチェーンとそのツール統合を構成した後、ツールチェーンのビジュアル表示を確認することができます。

1. DevOps ダッシュボードの**「ツールチェーン」**ページで、ツールチェーンをクリックしてその「概要」ページを開きます。あるいは、アプリの「概要」ページの「継続的デリバリー」カードで、**「ツールチェーンの表示」**をクリックします。次に、**「概要」**をクリックします。
2. ツールチェーン内にあるツール統合にアクセスするには、ツールをクリックします。

 **ヒント**: GitHub リポジトリー、{{site.data.keyword.ghe_short}} リポジトリー、または Git リポジトリーが複数ある場合、各リポジトリーはそれぞれ固有のカードで表されるため、同じツール統合に対して複数のカードが存在することがあります。複数のパイプラインがある場合、各パイプラインはそれぞれ固有のカードで表されるため、同じツール統合に対して複数のカードが存在することがあります。例えば、Microservices ツールチェーンを作成する場合、3 つのマイクロサービスのそれぞれが固有の GitHub リポジトリー、{{site.data.keyword.ghe_short}} リポジトリー、または Git リポジトリーと、固有のパイプラインを持ちます。
