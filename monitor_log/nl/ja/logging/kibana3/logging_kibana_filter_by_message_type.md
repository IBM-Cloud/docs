---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-16"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Kibana でのメッセージ・タイプによる Cloud Foundry アプリ・ログのフィルタリング
{: #logging_kibana_message_type_filter}

Kibana ダッシュボードで {{site.data.keyword.Bluemix_notm}} アプリケーション・ログを表示して、メッセージ・タイプでフィルタリングします。Kibana ダッシュボードには、Cloud Foundry アプリの**「ログ」**タブからアクセスできます。
{:shortdesc}

Kibana ダッシュボードで Cloud Foundry アプリ・ログを表示して、メッセージ・タイプでフィルタリングするには、以下のタスクを行います。

1. Cloud Foundry アプリの**「ログ」**タブにアクセスします。 

    1. {{site.data.keyword.Bluemix_notm}} **「アプリ」**ダッシュボードでアプリ名をクリックします。
    2. **「ログ」**タブをクリックします。 
    
    アプリのログが表示されます。

2. アプリの Kibana ダッシュボードにアクセスします。**「詳細ビュー」** ![「詳細ビュー」リンク](images/logging_advanced_view.jpg "「詳細ビュー」リンク") をクリックします。Kibana ダッシュボードが表示されます。

3. **「ALL EVENTS」**ウィンドウで、右矢印アイコンをクリックしてすべてのフィールドを表示します。 

    ![「ALL EVENTS」ウィンドウに右矢印アイコンが含まれています](images/logging_all_events_no_fields.jpg "「ALL EVENTS」ウィンドウに右矢印アイコンが含まれています")

4. **「Fields」**ペインで **message_type** を選択し、各ログ項目を生成したコンポーネントを**「ALL EVENTS」**ウィンドウに表示します。

    ![「ALL EVENTS」ウィンドウで message_type フィールドが選択されています](images/logging_message_type.png "「ALL EVENTS」ウィンドウで message_type フィールドが選択されています")

5. **「ALL EVENTS」**ウィンドウで、ログ・イベント行をクリックすると、そのイベントの詳細が表示されます。フィルタリングする **message_type** を示しているイベントを選択します。

    ![「ALL EVENTS」ウィンドウに、選択されたログ・イベントの詳細が表示されています](images/logging_message_type_add_filter.png "「ALL EVENTS」ウィンドウに、選択されたログ・イベントの詳細が表示されています")

6. 特定のメッセージ・タイプに関する情報を含める、または除外するためのフィルターを追加します。 

    * 特定のメッセージ・タイプに関する情報を含めるフィルターを追加するには、表の message_type 行で**「Magnifying Glass」**アイコン ![「Magnifying glass」アイコン](images/logging_magnifying_glass.jpg "「Magnifying glass」アイコン") をクリックします。 
    
           ![message_type フィールドのフィルター条件](images/logging_message_type_filter.png "message_type フィールドのフィルター条件")
    
    * 特定のメッセージ・タイプに関する情報を除外するフィルターを追加するには、表の message_type 行で**「Exclusion」**アイコン ![「Exclusion」アイコン](images/logging_exclusion_icon.png "「Exclusion」アイコン") をクリックします。 
    
    Kibana ダッシュボードに新しいフィルター条件が追加されました。

7. オプションで、前のステップを繰り返して他のメッセージ・タイプに関するフィルターを追加します。メッセージ・タイプの全リストを表示するには、『[ログのフォーマット (Log format)](../logging_view_kibana3.html#kibana_log_format_cf)』を参照してください。

9. ダッシュボードを保存します。    
        
    フィルターの作成が終了したら、**「Save」**アイコン ![「Save」アイコン](images/logging_save.jpg "「Save」アイコン") をクリックして、ダッシュボードの名前を入力します。 
      
    **注:** スペースを含む名前でダッシュボードを保存しようとすると、保存されません。スペースを含まない名前を入力し、**「Save」**アイコンをクリックしてください。
    
    ![ダッシュボード名の保存](images/logging_save_dashboard.jpg "ダッシュボード名の保存") 

ログ項目をメッセージ・タイプでフィルタリングするダッシュボードを作成しました。**「Folder」**アイコン ![「Folder」アイコン](images/logging_folder.jpg "「Folder」アイコン") をクリックし、ダッシュボードを名前で選択することで、保存したダッシュボードをいつでもロードできます。
