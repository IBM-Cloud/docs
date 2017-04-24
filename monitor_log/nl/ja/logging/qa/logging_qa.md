---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-07"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# よくある質問と回答
{: #logging_qa}

ここでは、{{site.data.keyword.Bluemix}} ロギング機能の使用に関するよくある質問に対する回答を示します。{:shortdesc}

* [Kibana の「Discover」ページでデータを表示できない場合、どうすればよいですか?](logging_qa.html#logging_qa_no_data_discover_kibana)

* [認証例外を受け取った場合、どうすればよいですか?](logging_qa.html#logging_qa_no_data_dashboard_kibana)





## Kibana の「Discover」ページでデータを表示できない場合、どうすればよいですか?
{: #logging_qa_no_data_discover_kibana}

Kibana でデータを表示できない場合、以下の異なるシナリオが考えられます。

1. Kibana を起動したときに、「Discover」ページでデータが表示されない場合があります。**「No results found.」**というメッセージを受け取ります。 
2. Kibana の「Discover」ページで作業している場合があります。しかし、ある程度の期間の経過後に、Kibana でタスクを実行しようとすると、**「No results found.」**というメッセージを受け取ります。

この問題を解決するには、以下のステップを実行します。

1. 「Discover」ページで設定されている*時間ピッカー* を確認し、期間を長くします。 

    **注**: デフォルトでは、{{site.data.keyword.Bluemix_notm}} において*時間ピッカー* は、過去 15 分間のデータを表示するように設定されています。

    *時間ピッカー* の設定方法について詳しくは、『[時間フィルターの設定](../kibana4/logging_kibana_set_time_filter.html#set_time_filter)』を参照してください。
       
2. 「*Discover*」ページの検索バーにある拡大鏡をクリックします。ページ・データが、デフォルトの検索照会に基づいて最新表示されます。

    あるいは、*自動最新表示* の期間を設定できます。

    **注**: デフォルトでは、{{site.data.keyword.Bluemix_notm}} において*自動最新表示* の期間は、**OFF** に設定されています。
    
    これを有効にする方法について詳しくは、『[データの自動最新表示](../kibana4/logging_kibana_analize_logs_interactively.html#kibana_discover_view_refresh_interval)』を参照してください。



## 認証例外を受け取った場合、どうすればよいですか?
{: #logging_qa_no_data_dashboard_kibana}

「Dashboard」ページの視覚化にデータが表示されず、**「Error: Authorization Exception.」**というエラー・メッセージを受け取った場合、各視覚化のデータを表示する権限を確認します。

以下の情報を考慮します。
「Dashboard」ページで 1 つ以上の視覚化を構成できます。「Dashboard」ページが視覚化で表示されるデータを収集する要求を行う際には、すべての視覚化に対して 1 つの要求のみが発行されます。いずれかの視覚化のデータを表示する権限がない場合、要求全体が失敗します。

この問題を解決するには、以下のステップを実行します。

1. 権限がない視覚化を識別します。

    1. 「*Dashboard*」ページ内の視覚化の*鉛筆* アイコンをクリックします。「*Visualize*」ページで視覚化が開きます。あるいは、「*Visualize*」ページで 1 つの視覚化をロードします。 
    2. データを表示できるかを確認します。
    
    視覚化ごとに上記ステップを繰り返します。

2. クラウド管理者に対して、視覚化のデータを表示する権限を要求します。

3. 問題の原因となっている視覚化のデータを表示する権限を付与してもらっている間、権限のない視覚化を除外した新規「Dashboard」ページを作成します。 

    そのダッシュボードを共有している場合、同じダッシュボードを使用している他のチーム・メンバーが影響を受けるため、視覚化を削除しないでください。


