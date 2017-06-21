---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-22"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Kibana 3 でのログの分析 (非推奨)
{: #analyzing_logs_Kibana3}

{{site.data.keyword.Bluemix}} では、分析および視覚化のためのオープン・ソース・プラットフォームである Kibana を使用して、さまざまなグラフ (図表や表など) でデータのモニター、検索、分析、および視覚化を行うことができます。高機能な分析タスクを実行するには、Kibana を使用してください。
{:shortdesc}

Kibana は以下のどの方法でも起動できます。

* Cloud Foundary アプリ・ダッシュボードから

    Kibana では特定の CF アプリのログをその特定のアプリに応じて起動できます。
    
    ダッシュボードに表示されるデータをフィルター操作するために使用される照会によって、Cloud Foundry アプリケーションのログ項目が取り出されます。Kibana ダッシュボードにデフォルトで表示されるログ情報は、単一の Cloud Foundry アプリケーションとそのすべてのインスタンスに関連するすべてです。詳しくは、『[Bluemix ダッシュボードから Kibana ダッシュボードへの移動](logging_view_kibana3.html#launch_Kibana_from_bluemix)』を参照してください。

* ブラウザーの直接リンクから

    提供された {{site.data.keyword.Bluemix}} スペース内のサービスからのデータを集約するカスタム Kibana ダッシュボードを起動したい場合があります。
    
    ダッシュボードに表示されるデータをフィルター操作するために使用される照会によって、{{site.data.keyword.Bluemix}} 組織内のスペースのログ項目が取り出されます。Kibana ダッシュボードに表示されるログ情報には、ログインしている {{site.data.keyword.Bluemix}} 組織のスペース内にデプロイされているすべてのリソースに関するレコードが含まれます。詳しくは、『[Web ブラウザーから Kibana ダッシュボードへの移動](logging_view_kibana3.html#launch_Kibana_from_browser)』を参照してください。
    
    初期の照会を変更または削除したり、他の照会を追加したりできます。詳しくは、『[Kibana での照会を使用した Cloud Foundry アプリ・ログのフィルタリング](kibana3/logging_kibana_query.html#logging_kibana_query)』を参照してください。


Kibana はブラウザー・ベースのインターフェースであり、ダッシュボードをカスタマイズしてから使用することで、ログ・データを分析し、高機能な管理タスクを実行することができます。 

{{site.data.keyword.Bluemix}} では、Cloud Foundry アプリごと、および組織のスペースごとに使用可能なデフォルト Kibana ダッシュボードを使用して、データを分析できます。デフォルトでは、これらのダッシュボードには、最近 24 時間についてのすべての使用可能なデータが、「ヒストグラム」行と「イベント表」行が含まれるパネルを使用して表示されます。 

デフォルト・ダッシュボードを使用して表示される情報を制限するために、デフォルト・ダッシュボードに照会およびフィルターを追加できます。その後、そのダッシュボードを将来の再使用のために保存できます。 

Kibana ダッシュボードで表示されるデータは、照会によって制御されます。ダッシュボードに表示される情報を変更するために、照会を変更したり、複数の照会を追加したりでき、その後、ダッシュボードを保存できます。複数のダッシュボードを同時にカスタマイズ、保存、および共有できます。このようにして、例えば、ご使用のスペース内の単一のアプリについての情報を Kibana で表示できます。

ログ・フィールドからフィルターを構成することもできます (例: message_type および instance_ID)。詳しくは、『[Kibana ログのフォーマット](logging_view_kibana3.html#kibana_log_format_cf)』を参照してください。 フィルターは動的に有効または無効にすることができます。有効にした照会およびフィルターの基準に一致するログ項目がダッシュボードに表示されます。詳しくは、『[Kibana ダッシュボードでのデータのフィルタリング](logging_view_kibana3.html#filter_data_kibana_dashboard)』を参照してください。

データを視覚化するために、パネルを構成できます。Kibana には、さまざまなパネル (表、トレンド、ヒストグラムなど) が組み込まれているので、情報を分析するためにそれらを利用できます。ダッシュボード内のパネルの追加、削除、並べ替えを行うことができます。各パネルの目標は異なります。一部のパネルは、1 つ以上の照会の結果を表す行に編成されています。その他のパネルは、文書またはカスタム情報を表示します。詳しくは、『[Kibana ダッシュボードのカスタマイズ](logging_view_kibana3.html#customize_kibana_dashboard)』を参照してください。

ダッシュボードをカスタマイズした後、以下から選択した操作を実行できます。

* 将来の再使用のためにダッシュボードを保存できます。詳しくは、『[Kibana ダッシュボードの保存](logging_view_kibana3.html#save_Kibana_dashboard)』を参照してください。

* Kibana ダッシュボードへの直接リンクを、エクスポートしたり、別のユーザーと共有したりできます。詳しくは、『[Kibana ダッシュボードのエクスポートおよび共有](kibana3/logging_kibana_export_share_dashboard.html#sexporting_sharing_kibana_dash)』を参照してください。

* ダッシュボードを Web ページに埋め込むことができます。埋め込まれたダッシュボードを表示するユーザーは、Kibana にアクセスする許可を持っている必要があります。

詳しくは、[Kibana ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window} の資料を参照してください。

**注:** Kibana 4 および Kibana 3 がサポートされています。Kibana 3 は推奨されません。


##  Bluemix ダッシュボードから Kibana ダッシュボードへの移動
{: #launch_Kibana_from_bluemix}

ダッシュボードに表示されるデータをフィルター操作するために使用される照会によって、Cloud Foundry アプリケーションのログ項目が取り出されます。Kibana ダッシュボードにデフォルトで表示されるログ情報は、単一の Cloud Foundry アプリケーションとそのすべてのインスタンスに関連するすべてです。

Cloud Foundry アプリケーションのログを Kibana で表示するには、以下の手順を実行します。

1. {{site.data.keyword.Bluemix_notm}} にログインし、{{site.data.keyword.Bluemix_notm}} **「アプリ」**ダッシュボードでアプリ名をクリックします。アプリ詳細ページが開きます。
    
2. ナビゲーション・バーで、**「ログ」**をクリックします。「ログ」タブが開きます。 
    
3. **「拡張ビュー」**をクリックします。**「Kibana 3」**ダッシュボードが開きます。

ログが何も表示されない場合は、ヘッダーにあるタイム・ピッカーを調整してください。

Kibana ダッシュボードのカスタマイズについて詳しくは、[このブログ投稿![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/){: new_window} または [Kibana ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window} の資料を参照してください。

##  Web ブラウザーから Kibana ダッシュボードへの移動
{: #launch_Kibana_from_browser}

ダッシュボードに表示されるデータをフィルター操作するために使用される照会によって、{{site.data.keyword.Bluemix}} 組織内のスペースのログ項目が取り出されます。Kibana ダッシュボードに表示されるログ情報には、ログインしている {{site.data.keyword.Bluemix}} 組織のスペース内にデプロイされているすべてのリソースに関するレコードが含まれます。

ブラウザーから Kibana ダッシュボードを開くには、以下の手順を実行します。

1. Kibana ユーザー・インターフェースにログインするため、[https://logmet.<span class="keyword" data-hd-keyref="DomainName">DomainName</span>](https://logmet.{DomainName}) を開きます。

2. Kibana 3 を使用して作業する場合は**「Kibana 3」**タブを、Kibana 4 を使用して作業する場合は**「Kibana 4」**タブを選択します。 デフォルト Kibana ダッシュボードが開きます。 

ログが何も表示されない場合は、ヘッダーにあるタイム・ピッカーを調整してください。

Kibana ダッシュボードのカスタマイズについて詳しくは、[このブログ投稿![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/blogs/bluemix/2015/09/creating-custom-kibana-dashboard-in-bluemix/){: new_window} または [Kibana ![外部リンク・アイコン](../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/kibana/current/index.html){: new_window} の資料を参照してください。



## Kibana ダッシュボードでのデータのフィルタリング
{: #filter_data_kibana_dashboard}

{{site.data.keyword.Bluemix}} では、リソースごと、または {{site.data.keyword.Bluemix}} スペースごとに提供されるデフォルト Kibana ダッシュボードを使用して、データを分析できます。デフォルトでは、これらのダッシュボードには、最近 24 時間についての使用可能なすべてのデータが表示されます。ただし、ダッシュボードで表示される情報を制限することができます。デフォルト・ダッシュボードに照会およびフィルターを追加することができ、その後で、そのダッシュボードを将来の再使用のために保存できます。

1 つのダッシュボードで、複数の照会およびフィルターを追加できます。照会は、ログ項目のサブセットを定義します。フィルターは、情報の包含または除外によって、データ選択を詳細化します。 

以下のリストに、Cloud Foundry アプリについてのデータをフィルタリングする方法を示す例の概要を示します。
* 重要用語を含む情報をログから探す場合、それらの用語でフィルター操作するような照会を作成できます。Kibana を使用すると、ダッシュボードで照会を視覚的に比較することができます。詳しくは、『[Kibana での照会を使用した Cloud Foundry アプリ・ログのフィルタリング](kibana3/logging_kibana_query.html#logging_kibana_query)』を参照してください。

* 特定の期間内の情報を探す場合、時刻範囲内のデータをフィルター操作できます。詳しくは、『[Kibana での時刻による Cloud Foundry アプリ・ログのフィルタリング](kibana3/logging_kibana_filter_by_time_period.html#logging_kibana_time_filter)』を参照してください。

* 特定のインスタンス ID の情報を探す場合、インスタンス ID でデータをフィルター操作できます。詳しくは、『[Kibana でのインスタンス ID による Cloud Foundry アプリ・ログのフィルタリング](kibana3/logging_kibana_filter_by_instance_id.html#logging_kibana_instance_id)』および『[Kibana での既知のアプリケーション ID による Cloud Foundry アプリ・ログのフィルタリング](kibana3/logging_kibana_filter_by_known_application_id.html#logging_kibana_known_application_id)』を参照してください。

* 特定のコンポーネントの情報を探す場合、コンポーネント (ログ・タイプ) でデータをフィルター操作できます。詳しくは、『[Kibana でのログ・タイプによる Cloud Foundry アプリ・ログのフィルタリング](kibana3/logging_kibana_filter_by_component.html#logging_kibana_component_filter)』を参照してください。

* 例えばエラー・メッセージの情報を探す場合、メッセージ・タイプでデータをフィルター操作できます。詳しくは、『[Kibana でのメッセージ・タイプによる Cloud Foundry アプリ・ログのフィルタリング](kibana3/logging_kibana_filter_by_message_type.html#logging_kibana_message_type_filter)』を参照してください。

## Kibana ダッシュボードのカスタマイズ
{: #customize_kibana_dashboard}

異なるタイプのダッシュボードがあり、それらをカスタマイズしてデータを視覚化および分析できます。以下に例を示します。
* single-cf-app ダッシュボード: これは、単一の Cloud Foundry アプリケーションの情報を表示するダッシュボードです。  
* multi-cf-app ダッシュボード: これは、同じ {{site.data.keyword.Bluemix}} スペースにデプロイされているすべての Cloud Foundry アプリケーションの情報を表示するダッシュボードです。 

ダッシュボードをカスタマイズする際、照会およびフィルターを構成して、そのダッシュボードで表示するログ・データのサブセットを選択することができます。

データを視覚化するために、パネルを構成できます。Kibana には、さまざまなパネル (表、トレンド、ヒストグラムなど) が組み込まれているので、情報を分析するためにそれらを利用できます。ダッシュボード内のパネルの追加、削除、並べ替えを行うことができます。各パネルの目標は異なります。一部のパネルは、1 つ以上の照会の結果を表す行に編成されています。その他のパネルは、文書またはカスタム情報を表示します。データを視覚化し、分析するために、例えば、棒グラフ、円グラフ、または表を構成することができます。  


## Kibana ダッシュボードの保存
{: #save_Kibana_dashboard}

カスタマイズした Kibana ダッシュボードを保存するには、以下の手順を実行します。

1. ツールバーで、**「保存」**アイコンをクリックします。

2. ダッシュボードの名前を入力します。

    **注:** スペースを含む名前でダッシュボードを保存しようとすると、保存されません。

3. 名前フィールドの横の**「保存」**アイコンをクリックします。



## Kibana ダッシュボードを使用したログの分析
{: #analyze_kibana_logs}

Kibana ダッシュボードをカスタマイズした後、そのダッシュボードのパネルを使用してデータの視覚化および分析を行うことができます。 

情報を検索するために、照会をピン留めしたり、ピン留めを解除したりできます。 

* ダッシュボードに照会をピン留めすることができ、その検索は自動的にアクティブになります。
* 照会を非アクティブにすると、ダッシュボードから内容を削除できます。

情報をフィルター操作するために、フィルターを有効にしたり、無効にしたりできます。 

* フィルターの**「トグル」**チェック・ボックス ![フィルターを組み込むためのトグル・ボックス](images/logging_toggle_include_filter.jpg) を選択して、そのフィルターを有効にすることができます。   
* フィルターの**「トグル」**チェック・ボックス ![フィルターを組み込むためのトグル・ボックス](images/logging_toggle_exclude_filter.jpg) を選択解除して、そのフィルターを無効にすることができます。 

ダッシュボードのグラフおよび図表でデータが表示されます。ダッシュボードのグラフおよび図表を使用して、データをモニターできます。 

例えば、single-cf-app ダッシュボードには、1 つの Cloud Foundry アプリケーションについての情報が含まれます。視覚化および分析できるデータは、そのアプリケーションに限定されます。そのアプリケーションのすべてのインスタンスについてのデータをこのダッシュボードを使用して分析できます。インスタンス同士を比較することができます。インスタンス ID で情報をフィルター操作することができます。 

インスタンス ID ごとに照会を定義し、ダッシュボードにピン留めすることができます。 

![照会がピン留めされたダッシュボード](images/logging_kibana_dash_activate_query.jpg)

次に、ダッシュボードに表示したいインスタンス情報に基づいて、個々の照会をアクティブ化または非アクティブ化できます。 

以下の図では、1 つの照会がアクティブであり、他の照会は非アクティブになっています。

![照会がピン留めされたダッシュボード](images/logging_kibana_dash_deactivate_query.jpg)

1 つのヒストグラムを使用して 2 つのインスタンスを比較したい場合、同じダッシュボードに 2 つの照会 (インスタンス ID ごとに 1 つ) を定義できます。それらを簡単に識別できるように、別名を付け、固有の色にすることができます。Kibana は、複数の照会を論理 OR で結合して処理します。 

以下の図に示すパネルでは、照会の別名と色を構成し、その照会をダッシュボードにピン留めし、非アクティブにすることができます。

![照会を構成するためのダッシュボード・ウィザード](images/logging_kibana_query_def.jpg)



## Cloud Foundry アプリケーションの Kibana ログ・フォーマット
{: #kibana_log_format_cf}

各ログ項目に以下のフィールドを表示するように Kibana ダッシュボードを構成できます。

<dl>
<dt><strong>@timestamp</strong></dt>
<dd>
<pre class="pre screen"><code>yyyy-MM-ddTHH:mm:ss:SS-0500</code></pre>
<p>ログに記録されたイベントの時刻。タイム・スタンプは、ミリ秒単位まで定義されます。</p>
</dd>

<dt><strong>@version</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>ALCH_TENANT_ID</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} リソースの ID。</p>
</dd>

<dt><strong>_id</strong></dt>
<dd>
<p>ログ文書の固有 ID。</p>
</dd>

<dt><strong>_index</strong></dt>
<dd>
<p>ログ項目のインデックス。</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>ログのタイプ (例: <samp>syslog</samp>)。</p>
</dd>

<dt><strong>app_name</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} アプリケーションの名前。</p>
</dd>

<dt><strong>application_id</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} アプリケーションの固有 ID。</p>
</dd>

<dt><strong>host</strong></dt>
<dd>
<p>ログ・データを生成したアプリケーションの名前。</p>
</dd>

<dt><strong>instance_id</strong></dt>
<dd>
<p>ログ・データを生成したアプリケーション・インスタンスのインスタンス ID。</p>
</dd>

<dt><strong>module</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>loglevel</strong></dt>
<dd>
<p>ログに記録されたイベントの重大度。</p>
</dd>

<dt><strong>message</strong></dt>
<dd>
<pre class="pre screen"><code>&lt;<var class="keyword varname">Message</var>&gt;</code></pre>
<p>コンポーネントによって発行されたメッセージ。メッセージは、コンテキストによって異なります。</p>
</dd>

<dt><strong>message_type</strong></dt>
<dd>
<pre class="pre screen"><code>OUT</code></pre>
<p>ログ・メッセージが書き込まれたストリーム。<samp class="ph codeph">OUT</samp> は <samp class="ph codeph">stdout</samp> ストリームを示し、<samp class="ph codeph">ERR</samp> は <samp class="ph codeph">stderr</samp> ストリームを示します。</p>
</dd>

<dt><strong>org_id</strong></dt>
<dd>
<p>{{site.data.keyword.Bluemix_notm}} 組織の固有 ID。</p>
</dd>

<dt><strong>org_name</strong></dt>
<dd>
<p>アプリがステージ化されている {{site.data.keyword.Bluemix_notm}} 組織の名前。</p>
</dd>

<dt><strong>origin</strong></dt>
<dd>
<p></p>
</dd>

<dt><strong>source_id</strong></dt>
<dd>
<pre class="pre screen"><code>[App/0]</code></pre>
<p>ログを生成したコンポーネント。各コンポーネントからのログは、以下のリストのとおりです。</p>

<dl>
<dt><strong>API</strong></dt>
<dd>アプリ状況の変更を要求する API 呼び出しへの応答がログに記録されます。</dd>

<dt><strong>APP</strong></dt>
<dd>アプリからの応答がログに記録されます。</dd>

<dt><strong>CELL</strong></dt>
<dd>アプリの開始、停止、またはクラッシュがいつ起こったのかを示す Diego セルからの応答がログに記録されます。</dd>

<dt><strong>LGR</strong></dt>
<dd>ロギング処理での問題を示す Loggregator からの応答がログに記録されます。</dd>

<dt><strong>RTR</strong></dt>
<dd>ルーターが HTTP 要求をアプリに転送したときのルーターからの応答がログに記録されます。</dd>

<dt><strong>SSH</strong></dt>
<dd>**cf ssh** コマンドを使用してユーザーがアプリ・コンテナーにアクセスしたときの Diego セルからの応答がログに記録されます。</dd>

<dt><strong>STG</strong></dt>
<dd>アプリがステージ化または再ステージ化されたときの Diego セルまたは Droplet Execution Agent からの応答がログに記録されます。</dd>
</dl>
</dd>

<dt><strong>space_name</strong></dt>
<dd>
<p>アプリがステージ化されている {{site.data.keyword.Bluemix_notm}} スペースの名前。</p>
</dd>

<dt><strong>timestamp</strong></dt>
<dd>
<p>ログに記録されたイベントの時刻。タイム・スタンプは、ミリ秒単位まで定義されます。</p>
</dd>

<dt><strong>_type</strong></dt>
<dd>
<p>ログのタイプ (例: <samp>syslog</samp>)。</p>
</dd>
</dl>




