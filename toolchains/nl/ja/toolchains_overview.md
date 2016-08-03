---

copyright:
  years: 2016

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# ツールチェーン (試験用) の概要
{: #toolchains_getting_started}

*最終更新日: 2016 年 6 月 8 日*
{: .last-updated}  

ツールチェーンは、開発、デプロイメント、運用の作業をサポートするツール統合のセットです。ツールチェーンの集合的な機能は、個々のツール統合の機能を合わせたものより優れています。
{: shortdesc}

ツールチェーンを作成する方法は、2 つあります。テンプレートを使用してツールチェーンを作成する方法と、アプリからツールチェーンを作成する方法です。使用するテンプレートまたはツールチェーンによっては、
アプリのスターター・コードが設定された GitHub リポジトリーと、事前構成済みのデリバリー・パイプラインがツールチェーンに含まれているものがあります。ツールチェーンの GitHub リポジトリーに変更内容をプッシュすると、デリバリー・パイプラインによってアプリが自動的に作成され、{{site.data.keyword.Bluemix}} にデプロイされます。

開始点として、ツールチェーン・テンプレートを使用して、特定のツール統合のセットが含まれたツールチェーンを作成するか、または、空のツールチェーンを作成してそこにツール統合を追加していくことができます。

**重要**: この機能は試験段階です。ツールチェーンは安定していない可能性があり、前のバージョンとは互換性のない変更が加えられる場合があります。実稼働環境での使用は推奨されません。ツールチェーンを使用するには、一回限りの[アクセスの要求](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}を行う必要があります。ツールチェーンは米国南部地域でのみ利用可能です。


##テンプレートからのツールチェーンの作成   
{: #creating_a_toolchain_from_a_template}

ツールチェーンへのアクセスの要求が承認された後、テンプレートを開始点として使用して、特定のツール統合のセットが含まれたツールチェーンを作成できます。

1. DevOps ダッシュボードの**「ツールチェーン (Toolchains)」**タブで、**「ツールチェーンの作成 (Create a Toolchain)」**をクリックして最初のツールチェーンを作成します。ツールチェーンが既に存在する場合、他のツールチェーンを作成するには、追加ボタン (+) をクリックします。
1. ツールチェーン・テンプレートをクリックします。例えば、オンライン・ストアのサンプルを使用してツールチェーンを作成する場合は、**「マイクロサービス・ツールチェーン (Microservices Toolchain)」**をクリックします。 
1. ツールチェーン作成ページで、作成しようとしているツールチェーンの図を確認します。この図は、各ツール統合のツールチェーンにおけるライフサイクル・フェーズを表しています。次のイメージの図はその例です。ツールチェーンを作成するときは、この図に、ツールチェーンを構成する各ツール統合が表示されます。
![ツールチェーンの図](images/toolchain_diagram.png)

1. ツールチェーンの設定値のデフォルトの情報を確認します。{{site.data.keyword.Bluemix}} にツールチェーンの名前が示されます。同じ名前のツールチェーンが既に存在する場合や、別の名前を使用したい場合は、ツールチェーンの名前を変更してください。  
1. 「構成可能な統合 (Configurable Integrations)」セクションで、ツールチェーンに構成する各ツール統合を選択します。ツール統合の構成については、[ツール統合の構成](../toolchains/toolchains_integrations.html){: new_window}を参照してください。
1. **「作成」**をクリックします。以下のようないくつかのステップが自動で実行されて、ツールチェーンがセットアップされます。

 * ツールチェーンが作成されます。
 * Delivery Pipeline ツール統合を構成した場合は、それらのパイプラインが起動されます。
 * Sauce Labs ツール統合を構成した場合は、ジョブをパイプラインに追加してテストを実行するように Sauce Labs 統合が構成されます。
 * PagerDuty ツール統合を構成した場合は、Slack で構成したチャネルに通知を送信するように PagerDuty 統合が構成されます。これらの通知は、いつ問題が発生したかを示します。
 * Slack ツール統合を構成した場合は、Slack で構成したチャネルに通知を送信するように Slack 統合が構成されます。これらの通知は、デプロイメントの進捗 (例えば、「`プロジェクト XYZ に接続しました (Connected with Project XYZ)`」、「`パイプラインが構成されました (Pipeline Configured)`」、「 `'build' ステージを開始しました (Stage 'build' started)`」など) を示します。
 * GitHub ツール統合を構成した場合は、サンプルの GitHub リポジトリーが GitHub アカウント内に複製されます。


##アプリからのツールチェーンの作成
{: #creating_a_toolchain_from_an_app}

ツールチェーンへのアクセスの要求が承認された後、アプリからツールチェーンを作成することができます。ツールチェーンは、継続的な開発、デプロイメント、モニタリングなどをサポートでき、使用するアプリに関連付けられます。それぞれのアプリをツールチェーンに関連付けることができます。ツールチェーンの GitHub リポジトリーに変更内容をプッシュすると、パイプラインによってアプリが自動的に作成されてデプロイされます。  

1. 使用するアプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの追加 (Add Toolchain)」**をクリックします。または、Bluemix Classic Experience で**「Git の追加」**をクリックします。使用するアプリに、アプリのスターター・コードが設定された新しい GitHub リポジトリーからの継続的デリバリーのための構成が行われます。
1. ツールチェーン作成ページで、作成しようとしているツールチェーンの図を確認します。この図は、各ツール統合のツールチェーンにおけるライフサイクル・フェーズを表しています。
1. ツールチェーンの設定値のデフォルトの情報を確認します。{{site.data.keyword.Bluemix}} にツールチェーンの名前が示されます。同じ名前のツールチェーンが既に存在する場合や、別の名前を使用したい場合は、ツールチェーンの名前を変更してください。
1. 「構成可能な統合 (Configurable Integrations)」セクションで、ツールチェーンに構成する各ツール統合を選択します。ツール統合の構成については、[ツール統合の構成](../toolchains/toolchains_integrations.html){: new_window}を参照してください。
1. **「作成」**をクリックします。以下のようないくつかのステップが自動で実行されて、ツールチェーンがセットアップされます。

 * ツールチェーンが作成されます。
 * Delivery Pipeline ツール統合を構成した場合は、それらのパイプラインが起動されます。
 * Sauce Labs ツール統合を構成した場合は、ジョブをパイプラインに追加してテストを実行するように Sauce Labs 統合が構成されます。
 * PagerDuty ツール統合を構成した場合は、Slack で構成したチャネルに通知を送信するように PagerDuty 統合が構成されます。これらの通知は、いつ問題が発生したかを示します。
 * Slack ツール統合を構成した場合は、Slack で構成したチャネルに通知を送信するように Slack 統合が構成されます。これらの通知は、デプロイメントの進捗 (例えば、「`プロジェクト XYZ に接続しました (Connected with Project XYZ)`」、「`パイプラインが構成されました (Pipeline Configured)`」、「 `'build' ステージを開始しました (Stage 'build' started)`」など) を示します。
 * GitHub ツール統合を構成した場合は、サンプルの GitHub リポジトリーが GitHub アカウント内に複製されます。

 
##ツールチェーンの表示
{: #viewing_a_toolchain}

ツールチェーンとすべてのツール統合を構成した後、「ツール統合 (Tool Integrations)」ページでそのツールチェーンをビジュアル表示することができます。

1. DevOps ダッシュボードの**「ツールチェーン (Toolchains)」**タブで、ツールチェーンをクリックしてその「ツール統合 (Tool Integrations)」ページを開きます。または、アプリの「概要」ページの「継続的デリバリー (Continuous Delivery)」タイルで、**「ツールチェーンの表示」**をクリックしてから、**「ツール統合 (Tool Integrations)」**をクリックします。
1. ページでツールチェーンのビジュアル表示を確認します。
1. ツールチェーン内のツール統合にアクセスするには、そのツール・タイルをクリックします。 
 
 **ヒント**: 複数の GitHub リポジトリーがある場合は、リポジトリーごとに別のパイプラインが必要であるため、同一のツール統合に対して複数のタイルが表示されることがあります。


 <!-- The toolchain in the following image is an example. When you create your own toolchain, the visual representation of the toolchain shows the tool integrations that you configure.
![Sample toolchain](images/toolchain.png) -->


# 関連リンク
{: #rellinks}

## チュートリアルとサンプル
{: #samples}

* [3 つのマイクロサービスを使用するアプリケーションの作成](https://www.ibm.com/devops/method/tutorials/tutorial_microservices_part1){:new_window}

## 関連リンク
{: #general}

* [マイクロサービス・ツールチェーン (試験用)](https://www.ibm.com/devops/method/toolchains/microservices_toolchain){:new_window}
* [シンプルなツールチェーン (試験用)](https://www.ibm.com/devops/method/toolchains/simple_toolchain){:new_window}
* [IBM&reg; Bluemix&reg; Garage Method](https://www.ibm.com/devops/method){:new_window}
