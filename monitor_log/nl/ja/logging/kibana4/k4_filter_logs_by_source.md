---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# ソースによる CF アプリ・ログのフィルタリング
{:#k4_filter_logs_by_source}

Kibana ダッシュボードで、ソース・タイプによって Cloud Foundry アプリケーション・ログを表示およびフィルタリングします。
{:shortdesc}

特定のログ・ソースが含まれた項目を検索するには、以下のステップを実行します。

1. Kibana の「Discover」ページを見て、表示されているデータのサブセットを確認します。詳しくは、『[「Discover」ページで表示されているデータの識別](logging_kibana_analize_logs_interactively.html#k4_identify_data)』を参照してください。

2. *フィールド・リスト* で、**source_id** フィールドを選択します。

    ![source_id フィールドを表示するフィルター・リスト](images/k4_filter_sourceid_F1.jpg "source_id フィールドを表示するフィルター・リスト")     

3. 特定の source_id が含まれている項目を検索するフィルターを追加するには、その値の拡大ボタン ![拡大鏡ボタン (包含モード)](images/k4_include_field_icon.jpg "拡大鏡ボタン (包含)") を選択します。

    CF アプリで使用可能なログ・ソースのリストについては、『[CF アプリのログ・ソース](../logging_cf_apps.html#logging_bluemix_cf_apps_log_sources)』を参照してください。

    例えば、CF アプリケーションの開始、停止、または異常終了に関するログ項目を含めるフィルターを追加するには、*フィールド・リスト*・セクションの値「*CELL*」に対して使用可能な拡大鏡ボタン ![拡大鏡ボタン (包含モード)](images/k4_include_field_icon.jpg "拡大鏡ボタン (包含)") を選択します。以下の図では、source_id 値が *CELL* のフィルターが有効になっているのを示しています。
    
    ![フィールド値を含むフィルター](images/k4_filter_sourceid_F2.jpg "フィールド値を含むフィルター")

    特定の source_id が含まれていない項目を検索するフィルターを追加するには、その値の拡大ボタン ![拡大鏡ボタン (除外モード)](images/k4_exclude_field_icon.jpg "拡大鏡ボタン (除外モード)") を選択します。
    
    例えば、CF アプリケーションの開始、停止、または異常終了に関するログ項目を除外するフィルターを追加するには、*フィールド・リスト*・セクションの値「*CELL*」に対して使用可能な拡大鏡ボタン ![拡大鏡ボタン (包含モード)](images/k4_exclude_field_icon.jpg "拡大鏡ボタン (包含)") を選択します。以下の図では、source_id 値が *CELL* の項目を除外するフィルターを示しています。

    ![フィールド値を除外するフィルター](images/k4_filter_sourceid_F3.jpg "フィールド値を除外するフィルター")




