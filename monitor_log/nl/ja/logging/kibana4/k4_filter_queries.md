---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# カスタム検索照会の定義によるログのフィルタリング
{:#k4_filter_queries}

「Discover」ページの検索バーで、Lucene 照会言語を使用して検索照会を定義および保存できます。検索ごとに、フィルターを適用して、分析で使用可能な項目を詳細化できます。
{:shortdesc}

以下のタスクを実行して、カスタム検索によってログをフィルタリングします。

1. Cloud Foundry (CF) アプリまたはコンテナーの**「ログ」**タブにアクセスします。 

    1. {{site.data.keyword.Bluemix}} ダッシュボードでアプリ名またはコンテナーをクリックします。
    2. CF アプリケーションの場合、**「ログ」**タブをクリックします。コンテナーの場合、**「モニターおよびログ (Monitoring and logs)」**をクリックしてから、**「ロギング (Logging)」**タブを選択します。
    
    ログが表示されます。

2. Kibana にアクセスします。**「詳細ビュー」** ![「詳細ビュー」リンク](images/logging_advanced_view.jpg) をクリックします。Kibana ダッシュボードが表示されます。

    Kibana にアクセスすると、デフォルト検索が適用されます。Kibana を起動した対象リソースのインスタンスのリストに関するログを確認できます。そのスペース内の {{site.data.keyword.Bluemix_notm}} リソースのすべてまたは任意のものについて、ログをフィルタリングできます。

Lucene では、「keyword」ではなく、正しい用語は「term」です。

3. 「Discover」ページを見て、表示されているデータのサブセットを確認します。詳しくは、『[「Discover」ページで表示されているデータの識別](logging_kibana_analize_logs_interactively.html#k4_identify_data)』を参照してください。次に、項目をフィルタリングするためのデフォルト照会を変更します。

    **注:** カスタム照会の定義には、Lucene 照会言語を使用します。詳しくは、『[Apache Lucene - Query Parser Syntax  ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://lucene.apache.org/core/2_9_4/queryparsersyntax.html){: new_window}』を参照してください。
    
    Kibana が {{site.data.keyword.Bluemix_notm}} から起動された場合、照会の変更および複数の検索基準の定義のために、論理項 **AND** および **OR** を使用できます。これらの演算子は、大文字でなければなりません。    
    
    * キーワードまたはその一部を検索するには、語の後にワイルドカード記号 \* を付けて入力します。例えば、`Java*` などです。 
    * 特定の句を検索するには、二重引用符の中にその句を入れます。例えば、`"Java/1.8.0"` などです。
    * さらに複雑な検索を作成するには、論理条件の AND および OR を使用できます。例えば、`"Java/1.8.0" OR "Java/1.7.0"` などです。
    * 特定フィールド内の値を検索するには、*log_field_name:search_term* の形式 (例えば、`instance_id:"1"` など) で検索を入力します。
    * 特定ログ・フィールドで一定範囲の値を検索するには、*log_field_name:[start_of_range TO end_of_range]* の形式 (例えば、`instance_id:["1" TO "2"]` など) で検索を入力します。

     例えば、CF アプリの場合、照会 `application_id:9d222152-8834-4bab-8685-3036cd25931a AND instance_id:["0" TO "1"]` を作成できます。これにより、インスタンス *0* および *1* の項目のみがリストされます。 

4. 照会を保存して、後から再使用できるようにします。詳しくは、『[検索の保存](logging_kibana_filtering_logs.html#k4_save_search)』を参照してください。 

**注:** 照会を削除する必要がある場合は、『[検索の削除](logging_kibana_filtering_logs.html#k4_delete_search)』を参照してください。



