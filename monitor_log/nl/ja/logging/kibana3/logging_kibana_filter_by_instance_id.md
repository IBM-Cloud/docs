---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Kibana でのインスタンス ID による Cloud Foundry アプリ・ログのフィルタリング
{: #logging_kibana_instance_id}

Kibana ダッシュボードで {{site.data.keyword.Bluemix_notm}} インスタンス・ログを表示して、アプリのインスタンス ID (instance_id) でフィルタリングします。Kibana ダッシュボードには、Cloud Foundry アプリの**「ログ」**タブからアクセスできます。
{:shortdesc}

Kibana ダッシュボードで Cloud Foundry アプリ・ログを表示して、instance_id でフィルタリングするには、以下のタスクを行います。

1. Cloud Foundry アプリの**「ログ」**タブにアクセスします。 

    1. {{site.data.keyword.Bluemix_notm}} **「アプリ」**ダッシュボードでアプリ名をクリックします。
    2. **「ログ」**タブをクリックします。 
    
    アプリのログが表示されます。

2. アプリの Kibana ダッシュボードにアクセスします。**「詳細ビュー」** ![「詳細ビュー」リンク](images/logging_advanced_view.jpg "「詳細ビュー」リンク") をクリックします。Kibana ダッシュボードが表示されます。

3. Kibana ダッシュボードで、**「Go to saved default」**アイコン ![「Go to saved default」アイコン](images/logging_default_dash.jpg "「Go to saved default」アイコン") をクリックし、スペースのすべてのログを表示します。**「ALL EVENTS」**ウィンドウで、右矢印アイコンをクリックしてすべてのフィールドを表示します。 

    ![「ALL EVENTS」ウィンドウに右矢印アイコンが含まれています](images/logging_all_events_no_fields.jpg "「ALL EVENTS」ウィンドウに右矢印アイコンが含まれています")

4. **「Fields」**ペインで **application_id** と **instance_id** を選択し、**「ALL EVENTS」**ウィンドウに application_id フィールドと instance_id フィールドを表示します。

    ![「ALL EVENTS」ウィンドウで application_id フィールドと instance_id フィールドが選択されています](images/logging_all_events_app_instance_select.jpg "「ALL EVENTS」ウィンドウで application_id フィールドと instance_id フィールドが選択されています")

5. **「ALL EVENTS」**ウィンドウで、ログ・イベント行をクリックすると、そのイベントの詳細が表示されます。フィルタリングする instance_id を示しているイベントを選択します。

    ![「ALL EVENTS」ウィンドウに、選択されたログ・イベントの詳細が表示されています](images/logging_selected_log_event.jpg "「ALL EVENTS」ウィンドウに、選択されたログ・イベントの詳細が表示されています")

6. 特定のアプリ ID に関する情報を含める、または除外するためのフィルターを追加します。 

    * 特定のアプリケーション ID に関する情報を含めるフィルターを追加するには、表の application_id 行で**「Magnifying Glass」**アイコン ![「Magnifying glass」アイコン](images/logging_magnifying_glass.jpg) をクリックします。 
    
           ![application_id フィールドのフィルター条件](images/logging_application_id_filter.jpg "application_id フィールドのフィルター条件")
    
    * 特定のアプリケーション ID に関する情報を除外するフィルターを追加するには、表の application_id 行で**「Exclusion」**アイコン ![「Exclusion」アイコン](images/logging_exclusion_icon.png) をクリックします。 
    
           ![特定のアプリケーション ID を除外するフィルター条件](images/logging_application_id_exclude_filter.jpg "特定のアプリケーション ID を除外するフィルター条件")
    
    Kibana ダッシュボードに新しいフィルター条件が追加されました。
 

7. 特定のアプリ・インスタンス ID に関する情報を含める、または除外するためのフィルターを追加します。 

    * 特定のインスタンス ID に関する情報を含めるフィルターを追加するには、表の instance_id 行で**「Magnifying Glass」**アイコン ![「Magnifying glass」アイコン](images/logging_magnifying_glass.jpg "「Magnifying glass」アイコン") をクリックします。 

    ![instance_id フィールドのフィルター条件](images/logging_instance_id_filter.jpg "instance_id フィールドのフィルター条件")

     * 特定のインスタンス ID に関する情報を除外するフィルターを追加するには、表の instance_id 行で**「Exclusion」**アイコン ![「Exclusion」アイコン](images/logging_exclusion_icon.png "「Exclusion」アイコン") をクリックします。 
    
           ![特定のインスタンス ID を除外するフィルター条件](images/logging_application_instance_id_exclude_filter.jpg "特定のインスタンス ID を除外するフィルター条件")
    
    Kibana ダッシュボードに新しいフィルター条件が追加されました。

9. ダッシュボードを保存します。フィルターの作成が終了したら、**「Save」**アイコン ![「Save」アイコン](images/logging_save.jpg "「Save」アイコン") をクリックして、ダッシュボードの名前を入力します。 

    **注:** スペースを含む名前でダッシュボードを保存しようとすると、保存されません。スペースを含まない名前を入力し、**「Save」**アイコンをクリックしてください。

    ![ダッシュボード名の保存](images/logging_save_dashboard.jpg "ダッシュボード名の保存") 

ログ項目を instance_id でフィルタリングするダッシュボードを作成しました。**「Folder」**アイコン ![「Folder」アイコン](images/logging_folder.jpg "「Folder」アイコン") をクリックし、ダッシュボードを名前で選択することで、保存したダッシュボードをいつでもロードできます。 
