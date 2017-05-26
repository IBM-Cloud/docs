---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Kibana での照会からの表とグラフの作成
{: #logging_kibana_tables_graphs}


Kibana を使用して、照会のグラフと表を作成し、ログ・データを視覚化して結果を比較します。Kibana ダッシュボードには、Cloud Foundry アプリの**「ログ」**タブからアクセスできます。
{:shortdesc}

Kibana ダッシュボードは、一連の行でレイアウトされ、各行には 1 つ以上のパネルが含まれます。データのグラフィカル表現を表示するためのパネルを構成できます。照会を使用して、表示するデータを決定します。グラフまたは表を作成するには、まずブランク行を作成し、その後、パネルを作成する必要があります。CF アプリの**「ログ」**タブから Kibana ダッシュボードにアクセスすると、ヒストグラムと表の 2 つのパネルがダッシュボードに自動的に表示されます。

Kibana ダッシュボードにグラフまたは表を追加するには、以下のタスクを行います。

1. Cloud Foundry アプリの**「ログ」**タブにアクセスするには、{{site.data.keyword.Bluemix_notm}} **「アプリ」**ダッシュボードの**「Cloud Foundry アプリ」**表でアプリ名をクリックし、**「ログ」**タブをクリックします。アプリのログが表示されます。

2. アプリの Kibana ダッシュボード表示にアクセスするには、**「詳細ビュー」** ![「詳細ビュー」リンク](images/logging_advanced_view.jpg "「詳細ビュー」リンク") をクリックします。Kibana ダッシュボードが表示されます。

3. Kibana ダッシュボードで、ダッシュボードの下部にスクロールし、**「ADD A ROW」** ![「ADD A ROW」アイコン](images/logging_add_row.jpg "「ADD A ROW」アイコン") をクリックし、追加するパネルの行を作成します。「Dashboard Settings」ペインが表示されます。 
	
	![「Dashboard Settings」ペイン](images/logging_dashboard_settings.jpg "「Dashboard Settings」ペイン")
	
	「Add Row」ペインで、**「Title」**フィールドに行の名前を入力し、**「Create Row」**をクリックします。新しい行が追加されます。行の順序は、行タイトルの横にある**上矢印**または**下矢印**のアイコンをクリックして調整できます。行の順序を設定したら、**「Save」**をクリックします。Kibana ダッシュボードに空の行が作成されます。

4. **「Add panel to empty row」**をクリックしてパネルを追加します。「Row Settings」ペインが表示されます。

    ![「Row Settings」ペイン](images/logging_row_settings.jpg "「Row Settings」ペイン")
	
	**「Select Panel Type」**ドロップダウン・リストから**「table」**、**「histogram」**、**「terms」**などのさまざまなパネル・タイプを選択できます。**「terms」**を選択し、照会を基に棒グラフ、円グラフ、または表を作成します。「Row Settings」ペインにさまざまな構成オプションが表示されます。
	
	![「Row Settings」ペインにおけるパネルの追加](images/logging_add_panel.jpg "「Row Settings」ペインにおけるパネルの追加")
	
	パネルを構成します。グラフィカル表示の**「Title (タイトル)」**を入力します。ドロップダウン・リストからパネルの**「Span」**を選択します。**「Span」**は、ダッシュボードにおけるパネルの幅を決定します。「Parameters」セクションで、**「Field」**の内容を削除し、有効なログ・フィールド (例えば、`instance_id` など) を入力します。 

5. 「View Options」セクションで、**「Style」**ドロップダウン・リストから**「bar」**、**「pie」**、または**「table」**を選択することで、棒グラフ、円グラフ、または表を選びます。「Queries」セクションで、**「Queries」**ドロップダウン・リストから**「selected」**を選択し、ダッシュボードの照会によるログ・データを使用します。最後に**「Save」**をクリックします。ダッシュボードに新しいパネルが表示されます。

	![棒グラフを含むパネルが表示されたダッシュボード](images/logging_bar_chart_panel.jpg "棒グラフを含むパネルが表示されたダッシュボード")
	
6. このパネルに表が表示されるように変更するには、**「Configure」**アイコン ![「Configure」アイコン](images/logging_dashboard_config_panel.jpg "「Configure」アイコン") をクリックします。「Terms Settings」ペインが表示されます。 

	![「Terms Settings」ペイン](images/logging_terms_settings.jpg "「Terms Settings」ペイン")
	
	**「Panel」**タブをクリックし、**「Style」**ドロップダウン・リストから**「table」**を選択します。**「Save」**をクリックしてパネルを更新し、ダッシュボードに戻ります。

7. 行とパネルをダッシュボードにさらに追加します。完了したら、**「Save」**アイコンをクリックしてこのダッシュボードへの変更を保存します。

    **注:** スペースを含む名前でダッシュボードを保存しようとすると、保存されません。スペースを含まない名前を入力し、**「Save」**アイコンをクリックしてください。

    ![ダッシュボード名の保存](images/logging_save_dashboard.jpg "ダッシュボード名の保存") 


