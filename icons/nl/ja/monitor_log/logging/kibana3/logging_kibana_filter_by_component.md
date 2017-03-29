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

# Kibana でのログ・タイプによる Cloud Foundry アプリ・ログのフィルタリング
<!-- for example, Uploading your data -->
{: #logging_kibana_component_filter}
<!-- Provide an appropriate ID above -->

Kibana ダッシュボードで {{site.data.keyword.Bluemix_notm}} アプリケーション・ログを表示して、コンポーネント (ログ・タイプ) でフィルタリングします。Kibana ダッシュボードには、Cloud Foundry アプリの**「ログ」**タブからアクセスできます。
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->
Kibana ダッシュボードで Cloud Foundry アプリ・ログを表示して、ログ・タイプでフィルタリングするには、以下のタスクを行います。

1. Cloud Foundry アプリの**「ログ」**タブにアクセスします。 

    1. {{site.data.keyword.Bluemix_notm}} **「アプリ」**ダッシュボードでアプリ名をクリックします。
    2. **「ログ」**タブをクリックします。 
    
    アプリのログが表示されます。

2. アプリの Kibana ダッシュボードにアクセスします。**「詳細ビュー」** ![「詳細ビュー」リンク](images/logging_advanced_view.jpg) をクリックします。Kibana ダッシュボードが表示されます。

3. **「ALL EVENTS」**ウィンドウで、右矢印アイコンをクリックしてすべてのフィールドを表示します。 

    ![「ALL EVENTS」ウィンドウに右矢印アイコンが含まれています](images/logging_all_events_no_fields.jpg)

4. **「Fields」**ペインで **source_id** を選択し、各ログ項目を生成したコンポーネントを**「ALL EVENTS」**ウィンドウに表示します。

    ![「ALL EVENTS」ウィンドウで source_id フィールドが選択されています](images/logging_component.png)

5. **「ALL EVENTS」**ウィンドウで、ログ・イベント行をクリックすると、そのイベントの詳細が表示されます。フィルタリングする source_id を示しているイベントを選択します。

    ![「ALL EVENTS」ウィンドウに、選択されたログ・イベントの詳細が表示されています](images/logging_component_add_filter.png)

6. 特定のコンポーネント (ログ・タイプ) に関する情報を含める、または除外するためのフィルターを追加します。 

    * 特定のコンポーネント値を含めるフィルターを追加するには、表の source_id 行で**「Magnifying Glass」**アイコン ![「Magnifying glass」アイコン](images/logging_magnifying_glass.jpg) をクリックします。 

        ![source_id フィールドのフィルター条件](images/logging_component_filter.png) 

    * 特定のコンポーネント値を除外するフィルターを追加するには、表の source_id 行で**「Exclusion」**アイコン ![「Exclusion」アイコン](images/logging_exclusion_icon.png) をクリックします。 
    
         ![source_id フィールドを除外するフィルター条件](images/logging_component_add_exclusion_filter.png) 
     
     Kibana ダッシュボードに新しいフィルター条件が追加されました。

7. オプションで、前のステップを繰り返して、各コンポーネントに関するフィルターを追加できます。コンポーネントの全リストを表示するには、『[ログのフォーマット (Log format)](../logging_view_kibana3.html#kibana_log_format_cf)』を参照してください。

    以下の図は、さまざまなコンポーネントに関する複数のフィルターを指定したダッシュボードを示しています。
    
    ![source_id フィールドに関する複数のフィルター条件](images/logging_component_multiple_filters.png)

8. ダッシュボードを保存します。 

    フィルターの追加とダッシュボードのカスタマイズが終了したら、**「Save」**アイコン ![「Save」アイコン](images/logging_save.jpg) をクリックして、ダッシュボードの名前を入力します。 
      
    **注:** スペースを含む名前でダッシュボードを保存しようとすると、保存されません。スペースを含まない名前を入力し、**「Save」**アイコンをクリックしてください。
    
    ![ダッシュボード名の保存](images/logging_save_dashboard.jpg)

ログ項目をコンポーネント (ログ・タイプ) でフィルタリングするダッシュボードを作成しました。**「Folder」**アイコン ![「Folder」アイコン](images/logging_folder.jpg) をクリックし、ダッシュボードを名前で選択することで、保存したダッシュボードをいつでもロードできます。


