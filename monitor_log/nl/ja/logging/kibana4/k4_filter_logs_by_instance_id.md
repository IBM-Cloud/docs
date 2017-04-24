---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# インスタンス ID によるログのフィルタリング
{:#k4_filter_logs_by_instance_id}

インスタンス ID によって {{site.data.keyword.Bluemix}} ログを表示およびフィルタリングします。
{:shortdesc}

Kibana ダッシュボードでインスタンス ID によってログを表示およびフィルタリングするには、以下のステップを実行します。

1. Kibana の「Discover」ページを見て、表示されているデータのサブセットを確認します。詳しくは、『[「Discover」ページで表示されているデータの識別](logging_kibana_analize_logs_interactively.html#k4_identify_data)』を参照してください。

2. *フィールド・リスト* で、特定のインスタンス ID を検索する以下のいずれかのフィールドを選択します。

    * **instance_ID**: このフィールドは、Cloud Foundry アプリケーションのログで使用可能な各種インスタンス ID をリストします。 
    * **instance**: このフィールドは、コンテナー・グループのすべてのインスタンスの各種 GUID をリストします。 

    例えば、以下の図では、CF アプリのインスタンスの各値を示しています。
    
    ![instance_id フィールドを示すフィルター・リスト](images/k4_filter_instanceid_f1.jpg "instance_id フィールドを示すフィルター・リスト")
   
3. 特定のログ・タイプを検索するフィルターを追加するには、分析するログ・タイプの拡大ボタン ![拡大鏡ボタン (包含モード)](images/k4_include_field_icon.jpg "拡大鏡ボタン (包含)") を選択します。

   例えば、CF アプリ・インスタンス *2* の項目を含めるフィルターを追加するには、フィールド・リスト・セクションの値「*2*」に対して使用可能な拡大鏡ボタン ![拡大鏡ボタン (包含モード)](images/k4_include_field_icon.jpg "拡大鏡ボタン (包含)") を選択します。以下の図では、インスタンス *2* の項目を含めるフィルターを示しています。
    
    ![インスタンス 2 の instance_id 項目を含めるフィルター](images/k4_filter_instanceid_f2.jpg "インスタンス 2 の instance_id 項目を含めるフィルター")

    特定のインスタンス ID が含まれていない項目を検索するフィルターを追加するには、その値の拡大ボタン ![拡大鏡ボタン (除外モード)](images/k4_exclude_field_icon.jpg "拡大鏡ボタン (除外)") を選択します。

     例えば、CF アプリ・インスタンス *2* の項目を除外するフィルターを追加するには、フィールド・リスト・セクションの値「*2*」に対して使用可能な拡大鏡ボタン ![拡大鏡ボタン (除外モード)](images/k4_exclude_field_icon.jpg "拡大鏡ボタン (除外)") を選択します。以下の図では、インスタンス *2* の項目を除外するフィルターを示しています。
     
      ![インスタンス 2 の instance_id 項目を除外するフィルター](images/k4_filter_instanceid_f3.jpg "インスタンス 2 の instance_id 項目を除外するフィルター")

