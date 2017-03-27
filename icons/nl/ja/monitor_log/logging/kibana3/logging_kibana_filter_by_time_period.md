---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Kibana での時間による Cloud Foundry アプリ・ログのフィルタリング
<!-- for example, Uploading your data -->
{: #logging_kibana_time_filter}


Kibana ダッシュボードで {{site.data.keyword.Bluemix_notm}} アプリケーション・ログを表示して、時間でフィルタリングします。Kibana ダッシュボードには、Cloud Foundry アプリの**「ログ」**タブからアクセスできます。
{:shortdesc}

Kibana ダッシュボードで Cloud Foundry アプリ・ログを表示して、時間でフィルタリングするには、以下のタスクを行います。

1. Cloud Foundry アプリの**「ログ」**タブにアクセスします。 

    1. {{site.data.keyword.Bluemix_notm}} **「アプリ」**ダッシュボードでアプリ名をクリックします。
    2. **「ログ」**タブをクリックします。 
    
    アプリのログが表示されます。

2. アプリの Kibana ダッシュボードにアクセスします。**「詳細ビュー」** ![「詳細ビュー」リンク](images/logging_advanced_view.jpg) をクリックします。Kibana ダッシュボードが表示されます。


3. Kibana ダッシュボードで、**「Time Filter」** ![Kibana 時間フィルター](images/logging_kibana_time_filter.jpg) をクリックして、ドロップダウン・メニューから**「Custom」**を選択します。次のウィンドウが表示されます。

    ![Kibana ダッシュボードのカスタム時間フィルター](images/logging_custom_time_filter.jpg)

4. **「From」**フィールドと**「To」**フィールドをクリックし、フィルターの開始時刻と終了時刻を編集します。 
    
    現時点までのログを含めるには、**「now」**リンクをクリックします。
    時刻範囲の設定が完了したら、**「Apply」**をクリックします。 

Kibana ダッシュボードに、カスタマイズした時間フィルターに対応するログ・イベントが表示されます。
