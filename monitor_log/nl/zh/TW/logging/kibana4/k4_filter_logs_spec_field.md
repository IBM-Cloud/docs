---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 針對特定欄位值過濾日誌
{:#k4_filter_logs_spec_field}

您可以搜尋包括特定欄位值的項目。
{:shortdesc}

請完成下列步驟，以搜尋包括特定欄位值的項目：

1. 在 Kibana 的「探索」頁面中，查看其顯示哪些資料子集。如需相關資訊，請參閱[識別 Kibana 探索頁面中顯示的資料](logging_kibana_analize_logs_interactively.html#k4_identify_data)。

2. 在*欄位清單* 中，識別您要為其定義過濾器的欄位，然後按一下該欄位。

    針對該欄位，最多可顯示 5 個值。每一個值都有兩個放大鏡按鈕。 
    
    如果您看不到該值，請參閱[針對未列示在「欄位清單」中的值新增過濾器](k4_add_filter_out_value.html#k4_add_filter_out_value)。

3. 若要新增過濾器，以搜尋包含欄位值的項目，請選擇該值的放大鏡按鈕 ![內含模式的放大鏡按鈕](images/k4_include_field_icon.jpg "內含模式的放大鏡按鈕")。

    ![包括欄位值的過濾器](images/k4_add_filter_for_field.jpg "包括欄位值的過濾器")

    若要新增過濾器，以搜尋不包括該欄位值的項目，請選擇該值的放大鏡按鈕 ![排除模式的放大鏡按鈕](images/k4_exclude_field_icon.jpg "排除模式的放大鏡按鈕")。

    ![排除欄位值的過濾器](images/k4_add_filter_to_exclude_field.jpg "排除欄位值的過濾器")

4. 選擇下列任何選項，以用於 Kibana 中的過濾器：

    <table>
      <tbody>
        <tr>
          <th align="center">選項</th>
          <th align="center">說明</th>
          <th align="center">其他資訊</th>
        </tr>
        <tr>
          <td align="left">啟用</td>
          <td align="left">選取此選項可啟用過濾器。</td>
          <td align="left">當您新增過濾器時，會自動予以啟用。<br> 如果過濾器停用，按一下該過濾器即可啟用。</td>
        </tr>
        <tr>
          <td align="left">停用</td>
          <td align="left">選取此選項可停用過濾器。</td>
          <td align="left">新增過濾器之後，如果您想要隱藏欄位值的項目，請按一下**停用**。</td>
        </tr>
        <tr>
          <td align="left">固定</td>
          <td align="left">選取此選項可將過濾器持續保存在所有 Kibana 頁面上。</td>
          <td align="left">您可以將過濾器固定在*探索*頁面、*視覺化*頁面或*儀表板*頁面。</td>
        </tr>
        <tr>
          <td align="left">切換</td>
          <td align="left">選取此選項可切換過濾器。</td>
          <td align="left">依預設，會顯示符合過濾器的項目。若要顯示不相符的項目，請切換過濾器。</td>
        </tr>
        <tr>
          <td align="left">移除</td>
          <td align="left">選取此選項可移除過濾器。</td>
          <td align="left"></td>
        </tr>
      </tbody>
    </table>

 

 
 

