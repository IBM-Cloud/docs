{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

#{{site.data.keyword.deliverypipeline}} の概要
{: #delivery-pipeline}  

*最終更新日: 2016 年 1 月 21 日*

ビルドおよび {{site.data.keyword.Bluemix}} へのデプロイメントを自動化するには、IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}} ({{site.data.keyword.deliverypipeline}} サービス) を使用します。
{: shortdesc} 

クラウドでアプリを開発するとき、いくつかの選択肢の中からビルド・タイプを選択できます。ビルド・スクリプトを指定すると、{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} がそれを実行するため、ビルド・システムをセットアップする必要はありません。その後、1 回のクリックで、1 つ以上の {{site.data.keyword.Bluemix_notm}} スペース、パブリックの Cloud Foundry サーバー、または IBM Containers for {{site.data.keyword.Bluemix_notm}} 上の Docker コンテナーに、アプリを自動的にデプロイできます。  

ビルド・ジョブは、Git のリポジトリーまたは Jazz ソース・コントロール管理 (SCM) のリポジトリーから取得したアプリのソース・コードをコンパイルしてパッケージ化します。このビルド・ジョブによって、WAR ファイルや IBM Containers 用の Docker コンテナーなど、デプロイ可能な成果物が生成されます。さらに、ビルド内で単体テストを自動的に実行できます。ソース・コードが変更されるたびに、ビルドがトリガーされます。  

デプロイメント・ジョブは、ビルド・ジョブの出力を取り込み、それを IBM Containers または {{site.data.keyword.Bluemix_notm}} などの Cloud Foundry サーバーにデプロイします。  

1 つ以上の地域およびサービスにデプロイできます。例えば、開発成果物が IBM Containers を使用し、1 つの地域でテストされ、複数の地域の実働環境にデプロイされるように {{site.data.keyword.deliverypipeline}} サービスをセットアップすることができます。詳細については、『[Regions](../../overview/index.html#ov_intro__reg)』を参照してください。

1. {{site.data.keyword.Bluemix_notm}} にログインして、アプリの組織とスペースを選択します。
1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、**「アプリの作成」**をクリックします。
1. Web またはモバイルのアプリ・テンプレートを選択し、スターターを選択して、**「続行」**をクリックします。アプリに名前を付け、**「終了 (FINISH)」**をクリックします。  
1. 「コーディングの開始」ページでスクロールダウンして、**「アプリの概要の表示」**をクリックします。  
1. {{site.data.keyword.Bluemix_notm}} アプリ・ダッシュボードで**「Git の追加」**をクリックして、アプリ用に Git でホストされたプロジェクトを作成します。**「リポジトリーにスターター・アプリ・パッケージを取り込み、{{site.data.keyword.deliverypipeline}} (Build & Deploy) を使用可能にする (Populate the repository with the starter app package and enable Delivery Pipeline (Build & Deploy))」**チェック・ボックスが選択されていることを確認し、次に **「続行」**をクリックします。   
1. Git リポジトリーが作成された後、**「閉じる」**をクリックします。「Git の追加」リンクが「コードの編集」リンクと GIt URL に置き換えられます。  
1. {{site.data.keyword.deliverypipeline}} サービスを、関連スペース (複数可) に追加します。このサービスを追加した後、ビルド、テスト、およびデプロイメントの各ジョブが含まれているステージを構成して実行することで、{{site.data.keyword.Bluemix_notm}} スペース内にマルチステージ・デプロイメント・パイプラインを作成できます。
    1. {{site.data.keyword.Bluemix_notm}} アプリ・ダッシュボードで、**「サービスまたは API の追加」**をクリックします。カテゴリーで **「DevOps」**チェック・ボックスを選択し、カタログで**「Delivery Pipeline」**をクリックします。
    2. プランを選択して、**「作成」**をクリックします。{{site.data.keyword.deliverypipeline}} ダッシュボードが開き、先に作成したアプリが表示されます。     
  
{{site.data.keyword.deliverypipeline}} ダッシュボードで、{{site.data.keyword.jazzhub_short}} プロジェクトとそのプロジェクトの状態が確認できます。ビルド、デプロイ済みのアプリ、および最新のデプロイメントの状況を確認したり、最新のログやデプロイメントの詳細を表示したりできます。  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks">
<h2 class="topictitle2" id="d68e338">関連リンク</h2>
<aside>
<div class="linklist" id="general"><h3 class="linklistlabel">関連リンク</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(新しいタブまたはウィンドウで開きます)">{{site.data.keyword.Bluemix_notm}} 前提条件</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">チュートリアルおよびサンプル</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(新しいタブまたはウィンドウで開きます)">アプリを複製、編集およびデプロイする</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(新しいタブまたはウィンドウで開きます)">Node.js アプリを開発およびデプロイする</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(新しいタブまたはウィンドウで開きます)">Java アプリを開発およびデプロイする</a></li>
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(新しいタブまたはウィンドウで開きます)">developerWorks: {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.deliverypipeline}} service</a></li>
</ul>
</div>
</aside>
</article>
