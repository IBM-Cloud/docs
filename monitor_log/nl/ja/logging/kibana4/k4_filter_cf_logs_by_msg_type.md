---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# メッセージ・タイプによる CF アプリ・ログのフィルタリング
{:#k4_filter_cf_logs_by_msg_type}

Kibana でメッセージ・タイプ別に Cloud Foundry ログを表示およびフィルタリングできます。
{:shortdesc}


特定のメッセージ・タイプが含まれた項目を検索するには、以下のステップを実行します。

1. Kibana の「Discover」ページを見て、表示されているデータのサブセットを確認します。詳しくは、『[「Discover」ページで表示されているデータの識別](logging_kibana_analize_logs_interactively.html#k4_identify_data)』を参照してください。

2. *フィールド・リスト* で、**message_type** フィールドを選択します。

    以下の図では、CF アプリのログ内の *message_type* フィールドで見つかった値を示しています。
    
    ![message_type フィールドを示すフィルター・リスト](images/k4_filter_by_msg_type_f1.jpg "message_type フィールドを示すフィルター・リスト")     

3. 特定の *message_type* が含まれている項目を検索するフィルターを追加するには、その値の拡大ボタン ![拡大鏡ボタン (包含モード)](images/k4_include_field_icon.jpg "拡大鏡ボタン (包含)") を選択します。

    例えば、message_type 値が *OUT* のログ項目が含まれるフィルターを追加するには、*フィールド・リスト*・セクションの値「*OUT*」に対して使用可能な拡大鏡ボタン ![拡大鏡ボタン (包含モード)](images/k4_include_field_icon.jpg "拡大鏡ボタン (包含)") を選択します。以下の図では、message_type 値が *OUT* のフィルターが有効になっているのを示しています。
    
    ![フィールド値を含むフィルター](images/k4_filter_by_msg_type_f2.jpg "フィールド値を含むフィルター")

    特定の *message_type* が含まれていない項目を検索するフィルターを追加するには、その値の拡大ボタン ![拡大鏡ボタン (除外モード)](images/k4_exclude_field_icon.jpg "拡大鏡ボタン (除外モード)") を選択します。
    
    例えば、message_type が *OUT* のログ項目を除外するフィルターを追加するには、*フィールド・リスト*・セクションの値「*CELL*」に対して使用可能な拡大鏡ボタン ![拡大鏡ボタン (包含モード)](images/k4_exclude_field_icon.jpg "拡大鏡ボタン (包含)") を選択します。以下の図では、message_type 値が *OUT* の項目を除外するフィルターを示しています。

    ![フィールド値を除外するフィルター](images/k4_filter_by_msg_type_f3.jpg "フィールド値を除外するフィルター")

