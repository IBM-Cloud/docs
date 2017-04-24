---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 特定のフィールド値が含まれたログのフィルタリング
{:#k4_filter_logs_spec_field}

特定のフィールド値が含まれた項目を検索できます。
{:shortdesc}

特定のフィールド値が含まれた項目を検索するには、以下のステップを実行します。

1. Kibana の「Discover」ページを見て、表示されているデータのサブセットを確認します。詳しくは、『[「Discover」ページで表示されているデータの識別](logging_kibana_analize_logs_interactively.html#k4_identify_data)』を参照してください。

2. *フィールド・リスト* で、フィルターを定義するフィールドを識別してクリックします。

    フィールドに対して最大で 5 つの値が表示されます。各値には、2 つの拡大鏡ボタンがあります。 
    
    値を表示できない場合は、『[フィールド・リストでリストされない値のフィルターの追加](k4_add_filter_out_value.html#k4_add_filter_out_value)』を参照してください。

3. あるフィールド値が含まれている項目を検索するフィルターを追加するには、その値の拡大ボタン ![拡大鏡ボタン (包含モード)](images/k4_include_field_icon.jpg "拡大鏡ボタン (包含)") を選択します。

    ![フィールド値を含むフィルター](images/k4_add_filter_for_field.jpg "フィールド値を含むフィルター")

    当該フィールド値が含まれていない項目を検索するフィルターを追加するには、その値の拡大ボタン ![拡大鏡ボタン (包含モード)](images/k4_exclude_field_icon.jpg "拡大鏡ボタン (包含)") を選択します。

    ![フィールド値を除外するフィルター](images/k4_add_filter_to_exclude_field.jpg "フィールド値を除外するフィルター")

4. Kibana のフィルターを操作するには、以下のいずれかのオプションを選択します。

    <table>
      <tbody>
        <tr>
          <th align="center">オプション</th>
          <th align="center">説明</th>
          <th align="center">その他の情報</th>
        </tr>
        <tr>
          <td align="left">有効化</td>
          <td align="left">このオプションは、フィルターを有効にする場合に選択します。</td>
          <td align="left">フィルターを追加すると、そのフィルターは自動的に有効になります。<br> フィルターが無効になっている場合、有効にするにはそのフィルターをクリックします。</td>
        </tr>
        <tr>
          <td align="left">無効化</td>
          <td align="left">このオプションは、フィルターを無効にする場合に選択します。</td>
          <td align="left">フィルターの追加後に、あるフィールド値の項目を非表示にする場合、**「disable」**をクリックします。</td>
        </tr>
        <tr>
          <td align="left">Pin</td>
          <td align="left">このオプションは、すべての Kibana ページでフィルターを保持する場合に選択します。</td>
          <td align="left">「*Discover*」ページ、「*Visualize*」ページ、または「*Dashboard*」ページでフィルターをピン留めできます。</td>
        </tr>
        <tr>
          <td align="left">Toggle</td>
          <td align="left">このオプションは、フィルターを切り替える場合に選択します。</td>
          <td align="left">デフォルトでは、フィルターに一致する項目が表示されます。一致しない項目を表示するには、フィルターを切り替えます。</td>
        </tr>
        <tr>
          <td align="left">削除</td>
          <td align="left">このオプションは、フィルターを削除する場合に選択します。</td>
          <td align="left"></td>
        </tr>
      </tbody>
    </table>

 

 
 

