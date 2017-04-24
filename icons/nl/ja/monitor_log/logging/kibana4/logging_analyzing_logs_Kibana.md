---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Kibana での高度なログ分析
{:#analyzing_logs_Kibana}

{{site.data.keyword.Bluemix}} では、分析および視覚化のためのオープン・ソース・プラットフォームである Kibana を使用して、さまざまなグラフ (図表や表など) でデータのモニター、検索、分析、および視覚化を行うことができます。高機能な分析タスクを実行するには、Kibana を使用してください。
{:shortdesc}

Kibana は以下のどの方法でも起動できます。

* {{site.data.keyword.Bluemix_notm}} から

    Kibana では特定の CF アプリのログをその特定のアプリに応じて起動できます。
    
    Kibana では特定の Docker コンテナーのログをその特定のコンテナーに応じて起動できます。 
    
    CF アプリでは、Kibana で分析に使用できるデータをフィルタリングするために使用される照会により、Cloud Foundry アプリケーションのログ項目を取得します。Kibana にデフォルトで表示されるログ情報は、単一の Cloud Foundry アプリケーションとそのすべてのインスタンスに関連するすべてです。 
    
    コンテナーでは、Kibana で分析に使用できるデータをフィルタリングするために使用される照会により、コンテナーのすべてのインスタンスのログ項目を取得します。Kibana にデフォルトで表示されるログ情報は、単一コンテナーまたはコンテナー・グループおよびそのすべてのインスタンスに関連するすべてです。 
    
    詳しくは、『[Bluemix ダッシュボードから Kibana ダッシュボードへの移動](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix)』を参照してください。

* ブラウザーの直接リンクから

    Kibana を起動し、表示されるデータで、提供されている {{site.data.keyword.Bluemix_notm}} スペース内のサービスからのログを集約するようにすることができます。
    
    ダッシュボードに表示されるデータをフィルター操作するために使用される照会によって、{{site.data.keyword.Bluemix_notm}} 組織内のスペースのログ項目が取り出されます。Kibana に表示されるログ情報には、ログインしている {{site.data.keyword.Bluemix_notm}} 組織のスペース内にデプロイされているすべてのリソースに関するレコードが含まれます。 
    
    詳しくは、『[Web ブラウザーから Kibana ダッシュボードへの移動](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser)』を参照してください。
    
    ブラウザーから Kibana を起動するときに、Kibana 4 または Kibana 3 のいずれかで作業することを選択できます。**注:** Kibana 3 は非推奨です。Kibana 3 を使用したログの分析については、[Kibana 3 でのログの分析 (非推奨)](../logging_view_kibana3.html#analyzing_logs_Kibana3) に関する個所を参照してください。

<br>    

Kibana はブラウザー・ベースのインターフェースであり、データを対話式に分析したり、ダッシュボードをカスタマイズしてから使用することで、ログ・データを分析し、高機能な管理タスクを実行したりすることができます。 

Kibana ページで表示されるデータは、検索によって制限されます。デフォルトのデータ・セットは、事前構成の索引パターンによって定義されています。情報をフィルタリングするために、新しい検索照会を追加し、フィルターをデフォルトのデータ・セットに適用できます。その後、その検索を将来の再使用のために保存できます。 

Kibana には、ログの分析に使用できる、以下のような各種ページが含まれています。

| Kibana ページ | 説明 |
|-------------|-------------|
| Discover | このページは、検索を定義し、表およびヒストグラムでログを対話式に分析する場合に使用します。 |
| Visualize | このページは、ログ・データの分析および結果の比較に使用できるグラフや表などの視覚化を作成する場合に使用します。  |
| ダッシュボード | このページは、保存済みの視覚化および検索のコレクションを介してログを分析する場合に使用します。  |

**注:** 「Visualize」ページまたは「Dashboard」ページで一度に分析できる期間は丸 1 日だけです。ただし、7 日遡ることができます。ログ・データはデフォルトで 7 日間保管されます。 

| Kibana ページ | 期間の情報 |
|-------------|-------------------------|
| Discover | 最大 7 日分のデータを分析します。 |
| Visualize | 24 時間の期間のデータを分析します。<br> 24 時間のカスタム期間のログ・データをフィルタリングできます。  |
| ダッシュボード | 24 時間の期間のデータを分析します。<br> 24 時間のカスタム期間のログ・データをフィルタリングできます。<br> 設定した時間ピッカーは、ダッシュボードに含まれているすべての視覚化に適用されます。 |


例えば、以下のように、Kibana を使用して、各ページでスペース内の CF アプリまたはコンテナーに関する情報を表示できます。

* 「Discover」ページで、新規検索照会を定義し、照会ごとにフィルターを適用します。ログ・データは、表およびヒストグラムで表示されます。これらの視覚化を使用して、データを対話式に分析できます。詳しくは、『[Kibana でのログの対話式分析](logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively)』を参照してください。

    ログ・フィールド (例: message_type や instance_ID) からフィルターを構成したり、期間を設定したりすることができます。これらのフィルターを動的に有効または無効にすることができます。有効にした照会およびフィルターの基準に一致するログ項目が表やヒストグラムに表示されます。詳しくは、『[Kibana でのログのフィルタリング](logging_kibana_filtering_logs.html#kibana_filtering_logs)』を参照してください。
    
* 「Visualize」ページで、新規検索照会および視覚化を定義します。

    データを分析するために、既存の検索または新規検索に基づいて、視覚化を作成できます。Kibana には、さまざまなタイプの視覚化 (表、トレンド、ヒストグラムなど) が組み込まれているので、情報を分析するためにそれらを利用できます。各視覚化の目標は異なります。一部の視覚化は、1 つ以上の照会の結果を表す行に編成されています。文書またはカスタム情報を表示する視覚化もあります。視覚化のデータは、検索照会を更新して、修正または変更できます。視覚化を Web ページに埋め込んだり、共有したりすることができます。詳しくは、『[視覚化を使用したログの分析](logging_kibana_visualizations.html#logging_kibana_visualizations)』を参照してください。

* 「Dashboard」ページでは、複数の視覚化および検索を同時にカスタマイズ、保存、および共有できます。 

    ダッシュボード内の視覚化の追加、削除、並べ替えを行うことができます。詳しくは、『[ダッシュボードを使用した Kibana でのログの分析](logging_kibana_analize_logs_dashboard.html#kibana_analize_logs_dashboard)』を参照してください。
    
    Kibana ダッシュボードをカスタマイズした後、その視覚化を使用してデータを分析し、将来再使用するために保存できます。詳しくは、『[Kibana ダッシュボードの保存](logging_kibana_analize_logs_dashboard.html#save_Kibana_dashboard)』を参照してください。

Kibana には「*Settings*」ページもあり、このページを使用して、Kibana を構成したり、検索、視覚化、およびダッシュボードの保存、削除、エクスポート、およびインポートを行ったりすることができます。

詳しくは、「[Kibana User Guide ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}」を参照してください。

**注:** Kibana 4 および Kibana 3 がサポートされています。Kibana 3 は推奨されません。


##  Bluemix ダッシュボードから Kibana ダッシュボードへの移動
{: #launch_Kibana_from_bluemix}

Kibana で表示されるデータをフィルタリングするために使用される照会によって、Kibana を起動した {{site.data.keyword.Bluemix_notm}} CF アプリまたはコンテナーのログ項目を取得します。 

Cloud Foundry アプリケーションまたは Docker コンテナーのログを Kibana で表示するには、以下のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} にログインし、{{site.data.keyword.Bluemix_notm}} ダッシュボードでアプリ名またはコンテナーをクリックします。 
    
2. {{site.data.keyword.Bluemix_notm}} UI でログ・タブを開きます。

    * CF アプリの場合、ナビゲーション・バーの**「ログ」**をクリックします。 
    * コンテナーの場合、ナビゲーション・バーの**「モニターおよびログ (Monitoring and logs)」**を選択してから、**「ロギング (Logging)」**タブをクリックします。 
    
    「ログ」タブが開きます。 
    
3. **「拡張ビュー」**をクリックします。**「Kibana 4」**ダッシュボードが開きます。

    デフォルトでは、**「Discover」**ページは、デフォルトの索引パターンが選択され、時間フィルターが過去 30 秒に設定された状態でロードされます。検索照会は、CF アプリまたは Docker コンテナーのすべての項目に突き合わせるように設定されます。

    「Discover」ページでログ項目が表示されない場合は、時間ピッカーを調整します。詳しくは、『[時間フィルターの設定](logging_kibana_set_time_filter.html#set_time_filter)』を参照してください。

Kibana について詳しくは、「[Kibana User Guide](https://www.elastic.co/guide/en/kibana/current/index.html)」を参照してください。

##  Web ブラウザーから Kibana ダッシュボードへの移動
{: #launch_Kibana_from_browser}

Kibana に表示されるデータをフィルター操作するために使用される照会によって、{{site.data.keyword.Bluemix_notm}} 組織内のスペースのログ項目が取り出されます。Kibana に表示されるログ情報には、ログインしている {{site.data.keyword.Bluemix_notm}} 組織のスペース内にデプロイされているすべてのリソースに関するレコードが含まれます。

以下のステップを実行して、ブラウザーから Kibana を起動します。

1. Kibana ユーザー・インターフェースにログインするため、[https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) を開きます。

2. ログの分析に使用する Kibana のバージョンを選択します。
    * Kibana 4 で作業する場合は、**「Kibana 4」**タブを選択します。「Discovery」ページが開きます。詳しくは、[logging_kibana_analize_logs_interactively.html#kibana_analize_logs_interactively) を参照してください。
    * Kibana 3 を使用して作業する場合は**「Kibana 3」**タブを選択します。 デフォルト Kibana ダッシュボードが開きます。Kibana 3 ダッシュボードのカスタマイズについて詳しくは、[このブログ投稿](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/)を参照してください。
     
        **注:** Kibana 3 は非推奨です。

    「Discover」ページでログ項目が表示されない場合は、時間ピッカーを調整します。詳しくは、『[時間フィルターの設定](logging_kibana_set_time_filter.html#set_time_filter)』を参照してください。

Kibana について詳しくは、「[Kibana User Guide ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}」を参照してください。

