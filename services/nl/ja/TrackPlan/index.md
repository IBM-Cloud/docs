{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#{{site.data.keyword.trackplan}} サービスの概要
{: #track-plan}  

*最終更新日: 2016 年 1 月 21 日*

タスクを表示、編集、および計画するために、{{site.data.keyword.trackplanlong}} ({{site.data.keyword.trackplan}} サービス) を使用します。自分の作業とチームの作業の追跡、障害報告の作成、次の課題の確認、バックログの保守、および今後のスプリントの作業計画を行うことができます。
{: shortdesc}

{{site.data.keyword.trackplan}} サービスが計画とコードを結び付けるため、計画と開発チームの進行状況の同期状態が保たれます。このサービスにより、プロジェクトの作業を説明および追跡するためのストーリー、タスク、および障害報告を作成できます。また、製品のバックログ、リリース、スプリントを計画および管理できます。

1. {{site.data.keyword.Bluemix_notm}} にログインして、アプリの組織とスペースを選択します。
1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで、**「アプリの作成」**をクリックします。
1. Web またはモバイルのアプリ・テンプレートを選択し、スターターを選択して、**「続行」**をクリックします。アプリに名前を付け、**「終了 (FINISH)」**をクリックします。
1. 「コーディングの開始」ページでスクロールダウンして、**「アプリの概要の表示」**をクリックします。
1. {{site.data.keyword.Bluemix_notm}} アプリ・ダッシュボードで**「Git の追加」**をクリックして、アプリ用に Git でホストされたプロジェクトを作成します。**「リポジトリーにスターター・アプリ・パッケージを取り込み、Delivery Pipeline (Build & Deploy) を使用可能にする (Populate the repository with the starter app package and enable Delivery Pipeline (Build & Deploy))」**チェック・ボックスが選択されていることを確認し、次に**「続行」**をクリックします。Git リポジトリーが作成された後、**「閉じる」**をクリックします。「Git の追加」リンクが「コードの編集」リンクと GIt URL に置き換えられます。
1. {{site.data.keyword.trackplan}} サービスをスペースに追加して、チームの作業を管理できるようにします。
    1. {{site.data.keyword.Bluemix_notm}} アプリ・ダッシュボードで、**「サービスまたは API の追加」**をクリックします。カテゴリーで**「DevOps」**を選択し、カタログで**「Track & Plan」**をクリックします。
    2. {{site.data.keyword.trackplan}} ページで、プランを選択して**「作成」**をクリックします。    
1. アプリのリストの「状態」列で、現在の状態 (この場合は**「オフ」**) をクリックして、{{site.data.keyword.trackplan}} サービスの状態を変更します。{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} に「プロジェクト設定 (Project Settings)」ページが開きます。
    1. {{site.data.keyword.trackplan}} サービスを使用可能にするオプションを選択します。必要に応じて、地域、組織、またはスペースを更新します。
    2. **「保存」**をクリックします。  
1. {{site.data.keyword.Bluemix_notm}} ダッシュボードに戻り、{{site.data.keyword.trackplan}} サービスのタイルをクリックします。アプリに対する {{site.data.keyword.trackplan}} サービスの状態が**「オン」**に変わります。
1. アプリのリストの「作業項目 (Work Item)」列で**「作成」**をクリックし、{{site.data.keyword.trackplan}} サービスの使用を開始します。  

{{site.data.keyword.Bluemix_notm}} ダッシュボードで、{{site.data.keyword.jazzhub_short}} プロジェクトとそのプロジェクトのメンバー数、可視性、およびそのプロジェクトで {{site.data.keyword.trackplan}} サービスが使用可能になっているかどうかが確認できます。任意の {{site.data.keyword.jazzhub_short}} プロジェクトの作業項目を作成したり、計画ツールに移動したりできます。  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks">
<h2 class="topictitle2" id="d68e338">関連リンク</h2>
<aside>
<div class="linklist" id="general"><h3 class="linklistlabel">関連リンク</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(新しいタブまたはウィンドウで開きま)">{{site.data.keyword.Bluemix_notm}} 前提条件</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">チュートリアルおよびサンプル</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(新しいタブまたはウィンドウで開きます)">アプリを複製、編集およびデプロイする</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(新しいタブまたはウィンドウで開きます)">Node.js アプリを開発およびデプロイする</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(新しいタブまたはウィンドウで開きます)">Java アプリを開発およびデプロイする</a></li>
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/track%20and%20plan%20service" rel="external" title="(新しいタブまたはウィンドウで開きます)">developerWorks: {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.trackplan}} service</a></li>
</ul>
</div>
</aside>
</article>
