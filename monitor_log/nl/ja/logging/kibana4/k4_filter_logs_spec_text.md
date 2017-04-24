---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# フィールド値に特定のテキストが含まれたログのフィルタリング
{:#k4_filter_logs_spec_text}

フィールドの値に特定のテキストが含まれている項目を表示および検索します。
{:shortdesc}

**注意:** Elasticsearch アナライザーによって分析されるストリング・フィールドのフリー・テキスト検索のみを実行できます。 
    
Elasticsearch では、ストリング・フィールドの値を分析する際、Unicode Consortium での定義に従ってワード境界でテキストを分割し、句読点を削除し、すべての単語を小文字化します。
    
フィールド値に特定のテキストが含まれた項目を検索するには、以下のステップを実行します。

1. Kibana の「Discover」ページを見て、表示されているデータのサブセットを確認します。詳しくは、『[「Discover」ページで表示されているデータの識別]((logging_kibana_analize_logs_interactively.html#k4_identify_data)』を参照してください。

2. デフォルトで ElasticSearch で分析されるフィールドを指定します。

    ログ・データの検索およびフィルタリングで使用可能な分析されるフィールドの完全なリストを表示するには、[フィールドのリストを再ロードします](logging_kibana_analize_logs_interactively.html#kibana_discover_view_reload_fields)。その後、「Discover」ページで使用可能な*フィールド・リスト* で、以下のステップを実行します。
    
    1. 構成アイコン ![構成アイコン](images/k4_configure_icon.jpg "構成アイコン") をクリックします。フィールドをフィルタリングできる**「Selected fields」**セクションが表示されます。

        ![特定の属性が含まれたフィールドを表示する構成セクション](images/k4_reset_filters.jpg "特定の属性が含まれたフィールドを表示する構成セクション")
    
    2. 分析されるフィールドを指定するには、検索フィールド**「Analyzed」**で**「Yes」**を選択します。

        ![分析される属性](images/k4_reset_filters_analyze_options.jpg "分析される属性")
    
        分析されるフィールドのリストが表示されます。
    
        ![分析されるフィールドのリスト](images/k4_list_analyzed_fields.jpg "分析されるフィールドのリスト")
        
         
    3. フリー・テキスト検索を行うフィールドが、デフォルトで ElasticSearch によって分析されるフィールドかどうかを確認します。
    
3. フィールドが分析される場合は、フィールドの値の一部としてそのフリー・テキストを含む項目をログで検索するように照会を変更します。

    
**例**

{{site.data.keyword.Bluemix}} UI から Cloud Foundry (CF) アプリケーション用に Kibana を起動し、メッセージ ID *CWWKT0016I:* が含まれている特定のメッセージを検索する場合は、そのフリー・テキストが含まれるように検索を変更します。
    
1. ロードされた検索照会、および「Discover」ページに表示されたデータを確認します。
       
    ![デフォルト検索照会](images/k4_filter_by_text_default_query.jpg "デフォルト検索照会")
        
2. メッセージ ID *CWWKT0016I* を検索するには、以下のように検索照会を変更し、**Enter** キーを押します。
    
    ```
	application_id:f52f6016-3aab-4b5c-aa2e-5493747cb978 AND message:"CWWKT0016I:" 
	```
        
    ![照会の変更](images/k4_filter_by_text_modify_query.jpg "照会の変更")
      
    
テキスト *CWWKT0016I* が *message* フィールドの値に含まれている CF アプリの項目が表で表示されます。
    
![新規検索ビュー](images/k4_filter_by_text_result_query.jpg "新規検索ビュー")     	
        
 
 
