---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# 建立裝置類型綱目
{: #iotrtinsights_task}

若要使用規則和動作之類的 {{site.data.keyword.iot_short}} 特性，您必須建立綱目，以將裝置內容對映至對使用者友善的內容名稱、設定內容的資料單位，以及指定要用於綱目的訊息類型。
{: shortdesc}

**重要事項：**綱目必須利用規則和動作。如需相關資訊，請參閱[雲端分析](cloud_analytics.html#rules)。

**重要事項：**合併的分析特性來自 {{site.data.keyword.iotrtinsights_full}} 服務。如果您的 {{site.data.keyword.iot_short_notm}} 組織用來作為現有 {{site.data.keyword.iotrtinsights_short}} 實例的資料來源，則除非移轉現有 {{site.data.keyword.iotrtinsights_short}} 實例，否則不會啟用「雲端和邊緣分析」。在移轉完成之前，請繼續使用 {{site.data.keyword.iotrtinsights_short}} 儀表板來因應分析的需求。如需相關資訊，請參閱 IBM developerWorks 上的 [IBM Watson IoT Platform 部落格 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/iotplatform/2016/04/28/iot-real-time-insights-and-watson-iot-platform-a-match-made-in-heaven/){: new_window}，以及您的現有 {{site.data.keyword.iotrtinsights_short}} 實例儀表板。  

## 新增裝置綱目
{: #add_schema}

若要新增綱目，請執行下列動作：  
1. 移至**裝置 > 管理綱目**，然後按一下**新增綱目**。  
2. 選取要與此訊息綱目建立關聯的裝置類型。**重要事項：**一種裝置類型只能定義一個綱目。

3. 新增一個以上內容。  
您可以從連接的裝置選取內容、建立用來修改或結合現有內容的虛擬內容，或是手動新增內容。  

    **提示：**可用的內容定義在裝置所傳送的訊息有效負載中。如需 {{site.data.keyword.iot_short}} 有效負載格式的相關資訊，請參閱[訊息有效負載](reference/mqtt/index.html#message-payloadl "訊息有效負載。")主題。   
  <dl>
  <dt>手動新增內容</dt>
  <p><b>提示：</b>若要建立巢狀內容結構，請先新增資料類型為 Parent 的內容。然後您可以在內容表中，按一下 ![「新增子項」圖示](images/add_child.png "新增子項")，以新增一個以上子項內容。</p>
  <dd>
  <ol>
    <li>選取**手動**標籤。</li>
    <li>定義下列內容詳細資料：
    <ul>  
      <li>名稱 - 在 {{site.data.keyword.iot_short}} 儀表板、功能表和精靈中使用之內容的敘述性名稱。</li>
      <li>資料類型 - 內容的資料類型：  
   `String`、`Integer`、`Float` 或 `Parent`。</li>
   <!--<li>Event - A specific event to collect data for. Leave blank to collect for all events.</li>-->
   <li>內容 - 內容 ID，例如：  
 `temp` 或 `speed`  </br> 如需有關如何識別裝置訊息內容的詳細資訊，請參閱[識別裝置的內容](#identify-datapoints "識別內容")。</li>
  <li>內容單位 - 選用項目：內容的資料單位。例如：  
     `C` 或 `Mph`  </li>
     <li> 小數位數 - 選用項目，僅限 Float：裝置資料中所包含的小數位數。</li>
    </ul>
    </li>
    <li>按一下**完成**，以建立內容。</li>
  </ol>
  </dd>
  <dt>建立虛擬內容</dt>
  <dd> 例如，如果裝置內容 temp（溫度）傳回華氏的溫度值，但您想要使用攝氏，則可以建立具有下列函數 *temp_c=(temp-32)/1.8* 的虛擬內容 *temp_c*。然後，您可以使用虛擬的 *temp_c* 內容來取代規則條件中的即時 *temp* 內容。  
若要建立虛擬內容，請執行下列動作：
  <ol>
    <li>選取**虛擬內容**標籤。</li>  
    <li>定義下列內容詳細資料：
    <ul>
    <li>名稱 - 在 {{site.data.keyword.iot_short}} 儀表板、功能表和精靈中使用之內容的敘述性名稱。</li>
    <li>資料類型 - 內容的資料類型：  
 `Float` 或 `Integer`。</li>
 <li>內容 - 虛擬內容的內容 ID。例如：  
`temp_virt`</li>
    <li>運算式 - 新增一個以上元件，以定義有效的函數。您可以使用內容、數值和數學運算子（例如 +、-、\*、/、( 及 )）。  
    按一下一組公式的**進階**，以與邊緣裝置上的一系列資料點搭配使用。如需進階公式的相關資訊，請參閱[邊緣虛擬內容的進階計算](im_vir_calculations.html)。  
    **重要事項：**不支援根據進階公式來比較虛擬內容的規則條件。</li>
    <li>內容單位 - 選用項目：內容的資料單位。例如：`C` 或 `Mph`</li>
    <li> 小數位數 - 選用項目，僅限 Float：裝置資料中所包含的小數位數。</li>
   </ul>
   </li>
   <li>按一下**完成**，以建立內容。</li>
  </ol>
  </dd>
  <dt>從已連接的裝置中選取內容</dt>
  <dd>
  <ol>
    <li>選取**從已連接的**標籤。</li>  
    <li>選取一個以上要新增至綱目的內容。稍後可以編輯這些內容，來設定名稱和資料單位之類的屬性。  
<!--**Important:** Each property must be unique for a schema. If you select multiple occurrences of the same property for different events, only one of the selected properties is added to the schema.</li>-->
  <li>按一下**確定**，以建立內容。</li>
  </ol>
  </dd>
    <dd>即會新增所選取的內容，且說明會設定成內容的名稱。按一下清單中的內容並予以編輯，然後新增其他屬性，例如感應器類型、資料類型及小數位數。</dd>
  </dl>
8. 按一下**完成**，以建立訊息綱目。

## 識別裝置的內容。
{: #identify-datapoints}
您可以在 {{site.data.keyword.iot_short}} 儀表板中找到裝置的內容。

1. 在 {{site.data.keyword.iot_short}} 儀表板中，移至**裝置**。
2. 按一下裝置，以開啟顯示裝置詳細資料的頁面。
3. 向下捲動至**感應器資訊**區段，以查看已連接裝置的可用內容清單。
