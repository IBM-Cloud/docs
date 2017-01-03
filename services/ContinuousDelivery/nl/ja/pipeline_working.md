---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# {{site.data.keyword.deliverypipeline}} での作業{: #pipeline-working}  

最終更新日: 2016 年 11 月 18 日
{: .last-updated}

ビルドと {{site.data.keyword.Bluemix}} へのデプロイメントを自動化するには、{{site.data.keyword.Bluemix_notm}} 用の {{site.data.keyword.deliverypipeline}} を使用します。{: shortdesc}

{{site.data.keyword.deliverypipeline}} では、いくつかのビルド・タイプから選択できます。ビルド・スクリプトを指定すれば、
{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} が実行します。ビルド・システムをセットアップする必要はありません。1 回クリックするだけで、1 つ以上の {{site.data.keyword.Bluemix_notm}} スペース、Cloud Foundry のパブリック・サーバー、{{site.data.keyword.Bluemix_notm}} 用の IBM コンテナーの Docker コンテナーに自動的にアプリをデプロイできます。  

ビルド・ジョブが、アプリのソース・コードを Git リポジトリーからコンパイルしてパッケージします。ビルド・ジョブは、WAR ファイルや IBM コンテナーの Docker コンテナーなど、デプロイ可能な成果物を作成します。また、ビルド内で単体テストを自動的に実行することができます。コミットがプッシュされるたびにビルドがトリガーされるように、ビルド・ジョブを設定することができます。

デプロイメント・ジョブは、出力をビルド・ジョブから取得して、IBM コンテナーや Cloud Foundry サーバー ({{site.data.keyword.Bluemix_notm}} など) にデプロイします。  

1 つ以上の地域やサービスにデプロイできます。例えば、1 つ以上のサービスを使用して、1 つの地域でテストし、複数の地域で実動にデプロイするよう {{site.data.keyword.deliverypipeline}} をセットアップできます。詳しくは、『[地域](/docs/overview/whatisbluemix.html#ov_intro_reg)』を参照してください。

パイプラインの作成にはいくつか方法があり、例えば、パイプラインを既存のアプリケーションに追加する方法や、既存のアプリケーションなしでパイプラインを作成する方法があります。組織に {{site.data.keyword.deliverypipeline}} サービスがまだない場合は、カタログにアクセスして、{{site.data.keyword.deliverypipeline}} をクリックし、「作成」をクリックします。

既存のアプリケーションのために {{site.data.keyword.deliverypipeline}} をセットアップするには、次の手順を実行します。    

1. {{site.data.keyword.Bluemix_notm}} のアプリのダッシュボードで、アプリをクリックします。
1. {{site.data.keyword.Bluemix_notm}} メニュー・バーのハンバーガー・メニューから、**「サービス」**をクリックして、**「DevOps」**をクリックします。
1. **「パイプライン」**をクリックして、 **「パイプラインの作成 (Create a Pipeline)」**をクリックします。

Cloud Foundry アプリケーションをデプロイするように構成された[パイプラインを作成する (新しいウィンドウでリンクが開きます)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} には、以下のステップを実行します。    

1. **「Cloud Foundry」**をクリックします。  
1. パイプラインに別の名前を使用する場合は、デフォルトの名前を変更します。
 
1. アプリケーションに別の名前を使用する場合は、デフォルトの名前を変更します。この名前は、パイプラインのデプロイ先のアプリケーションです。 
1. ツールチェーンがない場合は、デフォルトの名前が付いたツールチェーンが作成されます。ツールチェーンに別の名前を使用する場合は、名前を変更します。
ツールチェーンを使用して、他のツールやサービスと統合することで、パイプラインの機能を拡張できます。

 **ヒント**: パイプラインとツールチェーンは、組織に属します。ツールチェーンを持つ組織に属していれば、これらのツールチェーンの作成者でなくても使用することができます。
 
1. 使用するツールチェーンを選択するか、作成する新しいツールチェーンの名前を入力します。
1. GitHub リポジトリーの場所を指定します。

 **ヒント**: {{site.data.keyword.Bluemix_notm}} に GitHub へのアクセスをまだ認可していない場合は、**「認可 (Authorize)」** をクリックして GitHub の Web サイトにアクセスするよう求められます。アクティブな GitHub セッションがない場合は、ログインするよう求められます。**「アプリケーションを許可 (Authorize Application)」** をクリックして、{{site.data.keyword.Bluemix_notm}} が GitHub アカウントにアクセスできるようにします。アクティブな GitHub セッションはあるものの、最近パスワードを入力していない場合は、確認のために GitHub パスワードの入力を求められることがあります。

   * 既存の GitHub リポジトリーを使用する場合は、リポジトリーのタイプとして**「リンク (Link)」**を選択します。リポジトリーの場所を検索するか、選択可能なリポジトリーのリストからリポジトリーを選択します。
   
   * 空の GitHub リポジトリーを作成する場合は、リポジトリー・タイプとして**「新規」**を選択します。リポジトリーの名前を入力します。
   
   * GitHub リポジトリーのクローンを作成する場合は、リポジトリーのタイプに**「コピー」**を選択します。リポジトリーの場所を検索するか、選択可能なリポジトリーのリストからリポジトリーを選択します。
   
   * GitHub リポジトリーをフォークし、プル・リクエストで変更内容を提供できるようにする場合は、**「フォーク (Fork)」**を選択します。リポジトリーの場所を検索するか、選択可能なリポジトリーのリストからリポジトリーを選択します。
 
1. **「作成」**をクリックします。 パイプラインが作成され、構成されて、ツールチェーンの「概要」ページに表示されます。
![パイプラインのタイル](images/cd_pipeline.png)

事前構成されたステージのない[空のパイプライン (新しいウィンドウでリンクが開きます)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} を作成するには、以下のようにします。

1. **「カスタム」**をクリックします。
1. パイプラインに別の名前を使用する場合は、デフォルトの名前を変更します。
 
1. ツールチェーンがない場合は、デフォルトの名前が付いたツールチェーンが作成されます。ツールチェーンに別の名前を使用する場合は、名前を変更します。
ツールチェーンを使用して、他のツールやサービスと統合することで、パイプラインの機能を拡張できます。
1. 使用するツールチェーンを選択するか、作成する新しいツールチェーンの名前を入力します。
1. **「作成」**をクリックします。 空のパイプラインが作成され、ツールチェーンの「概要」ページにタイルとして表示されます。

{{site.data.keyword.deliverypipeline}} タイルから、構成を変更したり、ビルドのステータス、デプロイされたアプリ、最近のデプロイメントを確認したり、最新のログとデプロイメントの詳細を参照したり、パイプラインを削除したりすることができます。  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks" role="article">
<h2 class="topictitle2" id="d68e338">関連リンク
</h2>
<aside role="complementary" aria-labelledby="related_links">
<div class="linklist" id="general"><h3 class="linklistlabel" id="related_links">関連リンク
</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(新しいウィンドウまたはタブで開きます)">{{site.data.keyword.Bluemix_notm}}前提条件</a></li>
<li><img src="./sout.gif" alt=""><a href="https://www.ibm.com/devops/method/content/deliver/practice_delivery_pipeline/" rel="external" title="(新しいウィンドウまたはタブで開きます)">IBM Bluemix Garage Method: Delivery pipeline</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">チュートリアルとサンプル</h3>
<ul>

<!--
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Opens in a new tab or window)">Clone, edit, and deploy an app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Node.js app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Java app</a></li>
-->

<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(新しいタブまたはウィンドウで開きます)">developerWorks: {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}} service</a></li>
</ul>
</div>
</aside>
</article>
