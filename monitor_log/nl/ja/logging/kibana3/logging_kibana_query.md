---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Kibana での照会による Cloud Foundry アプリ・ログのフィルタリング
{: #logging_kibana_query}

Kibana を使用して、ログでキーの条件について検索する照会を作成し、それらの条件でフィルタリングします。Kibana を使用すると、ダッシュボードで照会を視覚的に比較することができます。Kibana ダッシュボードには、Cloud Foundry アプリの**「ログ」**タブからアクセスできます。
{:shortdesc}

Kibana ダッシュボードで Cloud Foundry アプリ・ログの照会を作成するには、以下のタスクを行います。

1. Cloud Foundry アプリの**「ログ」**タブにアクセスします。 

    1. {{site.data.keyword.Bluemix_notm}} **「アプリ」**ダッシュボードでアプリ名をクリックします。
    2. **「ログ」**タブをクリックします。 
    
    アプリのログが表示されます。

2. アプリの Kibana ダッシュボードにアクセスします。**「詳細ビュー」** ![「詳細ビュー」リンク](images/logging_advanced_view.jpg "「詳細ビュー」リンク") をクリックします。Kibana ダッシュボードが表示されます。

3. Kibana ダッシュボードで**「QUERY」** ![「QUERY」アイコン](images/logging_query.jpg "「QUERY」アイコン") をクリックすると、フィールドが表示されます。Kibana にアクセスしてアプリの**「ログ」**タブからアプリのログを表示すると、アプリの該当 application_id のログをすべて表示するための照会が作成されます。
	
    照会を編集するには、**「QUERY」**フィールドをクリックして検索条件を入力します。

    * キーワードまたはその一部を検索するには、語の後にワイルドカード記号 \* を付けて入力します。例えば、`Java*` などです。 
	* 特定の句を検索するには、二重引用符の中にその句を入れます。例えば、`"Java/1.8.0"` などです。
	* さらに複雑な検索を作成するには、論理条件の AND および OR を使用できます。例えば、`"Java/1.8.0" OR "Java/1.7.0"` などです。
	* 特定フィールド内の値を検索するには、*log_field_name:search_term* の形式 (例えば、`instance_id:1` など) で検索を入力します。
	* 特定ログ・フィールドで一定範囲の値を検索するには、*log_field_name:[start_of_range TO end_of_range]* の形式 (例えば、`instance_id:[1 TO 2]` など) で検索を入力します。

4. 異なる 2 つの照会の結果を比較する場合は、別の照会条件をダッシュボードに追加することができます。別の照会を追加するには、**「QUERY」**フィールドの終わりにある **「+」** アイコンをクリックします。

    ![「QUERY」フィールド](images/logging_query_field.jpg "「QUERY」フィールド")
	
    新しい**「QUERY」**フィールドが表示され、ワイルドカード \* が含まれています。この照会では、すべての項目を含めるように Kibana に指示しています。
	
    ![追加の「QUERY」フィールド](images/logging_additional_query_field.jpg "追加の「QUERY」フィールド")
	
    新しい照会の結果でダッシュボードが更新されます。**「EVENTS BY TIME」**ペインに、両方の照会のグラフィカル表現が表示され、各照会の条件ヒットの数が括弧内に示されます。 
	
    ![両方の照会のグラフが表示されたダッシュボード](images/logging_dashboard_queries.jpg "両方の照会のグラフが表示されたダッシュボード")
	
5. この新しい**「QUERY」**フィールドをクリックしてその内容を編集し、照会条件 (例えば、`instance_id:1` など) を追加します。**「EVENTS BY TIME」**ペインを使用して、照会の結果を比較します。

    ![両方の照会のグラフが表示されたダッシュボード](images/logging_dashboard_queries2.jpg "両方の照会のグラフが表示されたダッシュボード")

6. 照会を削除するには、削除対象の**「QUERY」**フィールドの上にマウスを移動して**「delete」**アイコンを表示します。**「delete」**アイコンをクリックします。

    ![delete アイコンを含む「QUERY」フィールド](images/logging_delete_query.jpg "delete アイコンを含む「QUERY」フィールド")

7. このダッシュボードを分かりやすい名前で保存し、**「Save」**アイコン ![「Save」アイコン](images/logging_save.jpg "「Save」アイコン") をクリックし、ダッシュボードの名前を入力します。 

    **注:** スペースを含む名前でダッシュボードを保存しようとすると、保存されません。スペースを含まない名前を入力し、**「Save」**アイコンをクリックしてください。

    ![ダッシュボード名の保存](images/logging_save_dashboard.jpg "ダッシュボード名の保存")


