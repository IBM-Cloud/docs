---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Kibana での既知のアプリケーション ID による Cloud Foundry アプリ・ログのフィルタリング
<!-- for example, Uploading your data -->
{: #logging_kibana_known_application_id}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Cloud Foundry アプリのアプリケーション ID が分かっている場合、Kibana ダッシュボードでログを表示して、アプリのアプリケーション ID (application_id) ですぐにフィルタリングすることができます。Kibana ダッシュボードには、Cloud Foundry アプリの**「ログ」**タブからアクセスできます。
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Kibana ダッシュボードで Cloud Foundry アプリ・ログを表示して、既知のアプリケーション ID でフィルタリングするには、以下のタスクを行います。

1. Cloud Foundry アプリの**「ログ」**タブにアクセスします。 

    1. {{site.data.keyword.Bluemix_notm}} **「アプリ」**ダッシュボードでアプリ名をクリックします。
    2. **「ログ」**タブをクリックします。 
    
    アプリのログが表示されます。

2. アプリの Kibana ダッシュボードにアクセスします。**「詳細ビュー」** ![「詳細ビュー」リンク](images/logging_advanced_view.jpg) をクリックします。Kibana ダッシュボードが表示されます。

3. Kibana ダッシュボードで、**「Folder」**アイコン ![「Folder」アイコン](images/logging_folder.jpg) をクリックして、最近のダッシュボードをすべてリストするメニューを表示します。 

    **注:** このメニューには、名前で保存したダッシュボードのほかに、名前を付けていないダッシュボードが *ALCH_TENANT_ID_application_id* の形式でリストされます。 

    ![ダッシュボードのリスト](images/logging_list_of_dashboards.jpg)

4. 既知の application_id を含む名前のダッシュボードを選択します。 

    該当の application_id でフィルタリングされた情報がダッシュボードにロードされ、表示されます。

5. オプションで、フィルター・セクションにさらにフィールドを追加することができます。例えば、**instance_id** を追加して、インスタンス ID によるレコードのフィルタリングを有効または無効にします。 
  
    1. **「ALL EVENTS」**ウィンドウで、ログ・イベント行をクリックすると、そのイベントの詳細が表示されます。 
	
        ![「ALL EVENTS」ウィンドウに、選択されたログ・イベントの詳細が表示されています](images/logging_selected_log_event.jpg)
	
    2. フィルタリングするフィールド値を示しているイベントを選択します。
	
    3. フィルターを追加します。
    
        特定のフィールド値に関する情報を含めるフィルターを追加するには、表内のフィルタリング対象フィールドを含む行で**「Magnifying Glass」**アイコン ![「Magnifying glass」アイコン](images/logging_magnifying_glass.jpg) をクリックします。 
	
        特定のフィールド値に関する情報を除外するフィルターを追加するには、表内のフィルタリング対象フィールドを含む行で**「Exclusion」**アイコン ![「Exclusion」アイコン](images/logging_exclusion_icon.png) をクリックします。  

        Kibana ダッシュボードに新しいフィルター条件が追加されました。
	
	    ![instance_id フィールドのフィルター条件](images/logging_instance_id_filter.jpg)
	
6. 分かりやすい名前でこのダッシュボードを保存します。 

    **「Save」**アイコン ![「Save」アイコン](images/logging_save.jpg) をクリックし、ダッシュボードの名前を入力します。 

    **注:** スペースを含む名前でダッシュボードを保存しようとすると、保存されません。スペースを含まない名前を入力し、**「Save」**アイコンをクリックしてください。

    ![ダッシュボード名の保存](images/logging_save_dashboard.jpg)。


ログ項目をアプリケーション ID とインスタンス ID でフィルタリングするダッシュボードを作成しました。**「Folder」**アイコン ![「Folder」アイコン](images/logging_folder.jpg) をクリックし、ダッシュボードを名前で選択することで、保存したダッシュボードをいつでもロードできます。
