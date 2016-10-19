---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 邊緣分析
{: #edge_analytics}
前次更新：2016 年 8 月 1 日
{: .last-updated}

使用邊緣分析，您可以將雲端中的分析規則觸發程序移至啟用邊緣分析功能的閘道，如此即可透過在接近裝置之處進行分析處理，顯著減少傳送至雲端的裝置資料流量。
{:shortdesk}

裝置可將其資料傳送至啟用邊緣分析功能的閘道，在這裡邊緣分析規則會剖析資料。根據您的規則及其動作，重要資料及警示可能會傳送至 {{site.data.keyword.iot_full}}、在閘道上觸發警示，或寫入至閘道本端的文字檔。

下圖說明 {{site.data.keyword.iot_full}} 邊緣分析環境的一般架構。
![具有邊緣分析架構的 IBM Watson IoT Platform](images/architecture_platform_edge.svg "具有邊緣分析架構的 IBM Watson IoT Platform")

**重要事項：**合併的分析特性來自 {{site.data.keyword.iotrtinsights_full}} 服務。如果您的 {{site.data.keyword.iot_short_notm}} 組織被用作現有 {{site.data.keyword.iotrtinsights_short}} 實例的資料來源，則除非移轉現有 {{site.data.keyword.iotrtinsights_short}} 實例，否則不會啟用「雲端和邊緣分析」。在移轉完成之前，請繼續使用 {{site.data.keyword.iotrtinsights_short}} 儀表板來因應分析的需求。如需相關資訊，請參閱 IBM developerWorks 上的 [IBM Watson IoT Platform 部落格](https://developer.ibm.com/iotplatform/2016/04/28/iot-real-time-insights-and-watson-iot-platform-a-match-made-in-heaven/){: new_window}，以及您的現有 {{site.data.keyword.iotrtinsights_short}} 實例儀表板。  

## 開始之前
{: #byb}

在開始建立邊緣規則及動作之前，請：
- 確定您的閘道已連接至 {{site.data.keyword.iot_short}}，而且裝置資料正在傳送中。如需相關資訊，請參閱[連接閘道](gateways/dashboard.html)。
- 在您的閘道上安裝「邊緣分析代理程式 (EAA)」。如需相關資訊，請參閱[安裝邊緣分析代理程式](gateways/dashboard.html#edge)。</br> **提示：**啟用 EAA 功能的閘道會以閘道裝置訊息的形式提供 EAA 診斷資料。如需相關資訊，請參閱[邊緣分析代理程式診斷度量](#eaa_metrics)。
- 確定要在規則中用作條件的裝置內容已對映至綱目。如需相關資訊，請參閱[連接裝置](iotplatform_task.html)及[建立綱目](im_schemas.html)。

## 管理邊緣規則及動作  
{: #managing_rules}

邊緣規則是使用下列項目進行管理：
- **規則**儀表板用來為您的裝置與閘道建立及編輯雲端與邊緣規則和動作。
- **邊緣規則閘道**板用來啟動、取消啟動、更新及移除閘道上的邊緣規則。若要存取「邊緣規則閘道」板，請從「規則」儀表板中，對您要管理的邊緣規則按一下**管理規則**。如需相關資訊，請參閱[啟動、取消啟動及管理閘道的邊緣規則](#manage)。

若要針對閘道連接的裝置取得邊緣規則及警示的概觀，請使用下列板：

 |板名稱 | 說明 |  
 |:---|:---|  
  |以規則為主的分析 | 顯示您組織的規則，包括邊緣規則。其他卡片會列出轉遞的邊緣警示、關聯的裝置、裝置內容及轉遞的邊緣警示資訊。 |  
 |以裝置為主的分析 | 顯示連接至您組織的裝置。其他卡片會顯示所選取邊緣裝置轉遞的警示、所選取裝置的資訊、裝置內容及轉遞的警示資訊。 |

 如需預設分析板的相關資訊，請參閱[使用板及卡片視覺化即時資料](data_visualization.html#default_boards)。


## 建立邊緣規則
{: #rules}

邊緣規則是條件型決策點，用來比對即時裝置資料與預先定義的臨界值或其他內容資料，以在符合條件時觸發邊緣動作。

**重要事項：**您必須先建立裝置類型的綱目，才能建立裝置類型的規則。如需相關資訊，請參閱[建立裝置類型綱目](im_schemas.html)。

若要建立規則，請執行下列動作：
1. 在 {{site.data.keyword.iot_short}} 儀表板中，移至**規則**。
2. 按一下**建立邊緣規則**、指定規則名稱、提供說明、選取要套用規則的邊緣裝置類型，然後按**下一步**。  
3. 設定規則邏輯。
新增一個以上的 IF 條件，用作規則的觸發程式。
您可以在平行列中新增條件，將它們套用為 OR 條件，或您可以在循序欄中新增條件，將它們套用為 AND 條件。
**附註：**若要能夠選取一個裝置內容作為規則的輸入，內容必須對映至綱目。如需相關資訊，請參閱[建立綱目](im_schemas.html)。
**重要事項：**若要觸發一個條件，其會觸發兩個以上使用 AND 循序結合的內容條件，觸發資料點必須併入相同的裝置訊息中。如果在多則訊息中收到資料，則不會觸發循序條件。
**範例：**
如果參數值大於指定的值，則簡式規則可能觸發警示：
`temp>80`
符合臨界值組合時，可能會觸發較複雜的規則：
`temp>60 AND capacity>50`   

4. 配置規則的條件式觸發程式需求。
若要控制一段時間針對規則所觸發的警示及動作數目，您可以配置規則的條件式觸發程式需求。
**重要事項：**條件式觸發會對規則中的任何條件採取動作。例如，如果規則有五個使用 OR 設定的不同平行條件，則每一個符合的條件都會列入條件式觸發程式計數的計算中。
若要設定規則的條件式觸發，請執行下列動作：
 1. 在規則編輯器中，按一下預設**每次符合條件時觸發**鏈結，以開啟「設定頻率需求」對話框。
 2. 選取並配置您要在規則中使用的條件式觸發程式。
 <ul>
 <li>每次符合條件時觸發</li>
 <li>在 M 個*時間單位*內符合條件 N 次時觸發</li>
 </ul>  
如需條件式觸發程式的其他詳細說明，請參閱雲端分析一節中的[條件式規則觸發](cloud_analytics.html#conditional "條件式觸發概觀")。
5. 建立或選取在符合規則條件時發生的一個以上動作。
如需邊緣動作的相關資訊，請參閱[建立邊緣動作](#edge_actions "建立邊緣動作")。範例：動作可以是將裝置資料傳送至雲端，或將警示寫入至本端檔案。
3. **選用項目：**選取規則的警示優先順序。
 優先順序是用來分類**規則型分析**板中所顯示的警示。預設優先順序是「低」。
6. 當規則符合您的要求時，請按一下**儲存**。

即會建立您的規則，並新增至瀏覽儀表板。您現在可以從開啟的**邊緣規則閘道**板[啟動](#manage)規則。


## 建立邊緣動作
{: #edge_actions}

您可以直接在規則編輯器中建立動作，或在「動作」標籤中建立動作，然後在建立規則時選取動作。

若要在「動作」標籤上建立動作，請執行下列動作：
1. 在 {{site.data.keyword.iot_short}} 儀表板中，移至**規則**。
2. 在「規則」儀表板中，選取**動作**標籤。
2. 按一下**建立動作**、指定動作名稱及說明，並選取動作類型，然後按**下一步**。邊緣分析支援兩個動作類型：
<dl>
<dt>將事件轉遞至雲端</dt>  
<dd>裝置事件會傳送至 {{site.data.keyword.iot_short}}，在這裡它可以用於板及卡片中，以及符合雲端分析規則。如需相關資訊，請參閱[與雲端分析整合](#integrate_with_cloud_analytics)。    
**提示：**使用將事件轉遞至雲端動作，可以減少傳送至雲端的裝置資料數量，方法為直接在閘道裝置過濾掉較不重要的資料。</dd>
<dt>警示</dt>  
<dd>警示是在閘道裝置上建立的。</dd>
</dl>
3. 為您所選取的動作類型提供必要的參數。  
<dl>
<dt>將事件轉遞至雲端</dt>  
<dd>選取要轉遞至雲端的事件資料，並提供要在訊息中使用的事件名稱。</br>
**提示：**當設定板及卡片時，以及當建立雲端分析規則時，您可以使用事件及內容。</br>
您可以：
 <ul>
 <li>併入所有裝置內容及虛擬內容
 <li>僅併入綱目定義的內容及虛擬內容  
 </ul>
 </dd>
<dt>警示</dt>  
<dd>指定一則警示訊息，並為警示至少選取一個目的地。
 <ul>
 <li>轉遞至雲端  
 警示會轉遞至 {{site.data.keyword.iot_short}}，在這裡它會顯示在「以規則為主的分析」及「以裝置為主的分析」板中。
 <li>發佈至閘道分配管理系統
 警示會發佈至閘道分配管理系統。分配管理系統配置決定如何向使用者顯示警示。
 <li>儲存至本端文字檔
 警示會附加至閘道伺服器上的本端 *IBMEdgeAnalyticsAlerts.csv* 文字檔。
 </ul>
 </dd>
</dl>
4. 按一下**確定**，以建立新的動作。

此動作現在會出現在規則編輯器中。


## 啟動、取消啟動及管理閘道的邊緣規則
{: #manage}

對於要觸發動作的規則，您必須先在一個以上的閘道上啟動它。您可以使用**邊緣規則閘道**板，來啟動、取消啟動、更新及移除閘道上的邊緣規則。

若要啟動邊緣規則，請執行下列動作：
1. 從「規則」儀表板中，對您要管理的邊緣規則按一下**管理規則**按鈕。
在開啟的**邊緣規則閘道**板中，您會看到一個清單，列出所有已連接之啟用 EAA 功能的閘道。未上傳及啟動規則之閘道的規則狀態為*無*。
2. 尋找您要在其上啟動規則的閘道，然後在「選取作業」直欄中，選取功能表中的**啟動**。
邊緣規則即會上傳至閘道。當上傳完成且規則作用中時，「規則」狀態會變更為**作用中**。  

現在規則作用在閘道上，因此當符合規則條件時，配置的動作即會觸發。

**提示：**若要管理多個閘道上的規則，您可以選取「閘道」直欄標頭旁的「全選」方框。清除您不想要併入的所有閘道，然後從**選取作業**功能表（位於具有相同名稱之直欄的頂端）挑選作業。

除了啟動規則之外，您還可以在閘道上執行下列規則管理作業：

作業 | 說明--- | ---
啟動 | 在選取的閘道上，上傳及啟動規則。規則狀態會設為*作用中*。
取消啟動 | 在選取的閘道上，取消啟動規則。規則仍會留在閘道上，必要的話，可以重新啟動規則。規則狀態會設為*非作用中*。
更新 | 將更新的規則版本上傳至選取的閘道。如果閘道的規則狀態為*作用中（較舊）*，請使用此作業帶來最新的閘道。規則狀態會設為*作用中*。
移除 | 從選取的閘道中移除規則。閘道的規則狀態會回復為*無*。


## 與雲端分析整合
{: #integrate_with_cloud_analytics}

使用在啟用 EAA 功能的閘道上執行的邊緣規則觸發動作，可以過濾流至雲端的資料，並將閘道產生的警示轉遞至雲端，以與 {{site.data.keyword.iot_short}} 板及卡片搭配使用。  

您也可以使用 {{site.data.keyword.iot_short}}，對從閘道傳送至雲端的裝置資料執行雲端分析。如果您在邊緣規則中使用 `Forward event to cloud` 動作，則建立的訊息可以用作雲端分析規則的輸入，就好像是提供已觸發邊緣規則之資料的裝置已直接連接至 {{site.data.keyword.iot_short}} 一般。

如需如何建立雲端分析規則及動作的相關資訊，請參閱[雲端分析](cloud_analytics.html)。

## 邊緣分析代理程式診斷度量
{: #eaa_metrics}

已連接之啟用 EAA 功能的閘道會傳送診斷資訊，作為事件類型 `gateway_xv-monitor-event` 的裝置訊息。</br> **提示：**您可以使用[雲端分析](cloud_analytics.html)規則，根據啟用 EAA 功能的閘道所傳回的診斷值來配置警示動作，例如傳送電子郵件通知。例如，您可以建立一個規則，在 `SystemLoad` 超出特定臨界值時警示您。

若要查看閘道狀態的相關資訊，請執行下列動作：
1. 在 {{site.data.keyword.iot_short}} 儀表板中，選取功能表資訊看板中的**裝置**。
2. 按一下您的閘道裝置，以開啟裝置詳細資料頁面。
3. 存取閘道診斷資訊：  
 - 參閱**最近事件**一節，以取得閘道所傳送的最近訊息清單。
 - 參閱**診斷日誌**一節，以取得任何閘道警告及其他診斷訊息。
 - 參閱**感應器資訊**一節，從閘道取得詳細診斷資訊。下表說明可能併入閘道裝置訊息中的不同內容。


內容 | 說明
--- | ---
`MsgInCount` |已傳送至「邊緣分析代理程式 (EAA)」的訊息數目。
`MsgInRate`、`MsgInRate1Min`、`MessageInRate5Min`、`MsgInRate15Min`、`MsgInMeanRate` | 最後時段傳送至 EAA 之訊息的每秒預估數。</br>**附註：** `MsgInRate` 是 `MsgInRate1Min` 的別名。`MsgInMeanRate` 是自從啟動以來的平均訊息速率。
`LastHeartBeat` | 產生最後一則活動訊號訊息的毫秒時間戳記。最少每 10 秒會產生一則活動訊號訊息。
`CurrentTimestamp` | 產生現行監視訊息的毫秒時間戳記。
`IsAlive` | 如果 `LastHeartBeat` 與 `CurrentTimestamp` 之間的差異大於 20 秒，則此內容為 0。
`BytesOutCount` | EAA 傳送至 {{site.data.keyword.iot_short}} 的訊息位元組數。
`BytesOutRate`、`BytesOutRate1Min`、`BytesOutRate15Min`、`BytesOutRate5Min`、`BytesOutMeanRate` | 最後時段 EAA 傳送至 {{site.data.keyword.iot_short}} 之訊息位元組的每秒預估數。</br>**附註：**`BytesOutRate` 是 `BytesOutRate1Min` 的別名。`BytesOutMeanRate` 是自從啟動以來的平均速率。
`BytesInCount` | {{site.data.keyword.iot_short}} 傳送至 EAA 的訊息位元組數。
`BytesInMeanRate`、`BytesInRate1Min`、`BytesInRate`、`BytesInRate15Min`、`BytesInRate5Min` | 最後時段 {{site.data.keyword.iot_short}} 傳送至 EAA 之訊息位元組的每秒預估數。</br>**附註：**BytesOutRate 是 BytesOutRate1Min 的別名。BytesOutMeanRate 計算自從啟動以來的平均速率。
`RuleBytesInCount` |傳送至 EAA 規則引擎核心的訊息位元組數。</br> **附註：**如果未對裝置類型設定規則，則該裝置類型的訊息不會傳送至規則引擎核心。
`RuleBytesInRate5Min`、`RuleBytesInRate`、`RuleBytesInMeanRate`、`RuleBytesInRate1Min`、`RuleBytesInRate15Min` | 最後時段傳送至 EAA 規則引擎核心之訊息位元組的每秒預估數。</br> **附註：**`RuleBytesInMeanRate` 是自從啟動以來的平均速率。
`MsgOutCount` | EAA 傳送至 {{site.data.keyword.iot_short}} 的訊息數目。
`MsgOutRate`、`MsgOutMeanRate`、`MsgOutRate1Min`、`MessageOutRate5Min`、`MsgOutRate15Min` | 最後時段 EAA 傳送至 {{site.data.keyword.iot_short}} 之訊息位元組的每秒預估數。</br> **附註：**`MsgOutRate` 是 `MsgOutRate1Min` 的別名。`MsgOutMeanRate` 是自從啟動以來的平均速率。
`MsgReducePercent` | 送入訊息與送出訊息之間的百分比差異。</br>下列公式用於計算：`(msgIn - msgOut) / msgIn`
`BytesReducePercent` | 送入位元組與送出位元組之間的百分比差異。</br>下列公式用於計算：`(bytesIn - bytesOut) / bytesIn`
`MsgRateReduce` | 送入訊息速率與送出訊息速率之間的百分比差異。</br>下列公式用於計算：`(msgInRate - msgOutRate) / msgInRate`
`BytesRateReduce` | 送入訊息位元組與送出訊息位元組之間的百分比差異。</br>下列公式用於計算：`(bytesInRate - bytesOutRate) / bytesInRate`
`SystemLoad` | EAA 執行所在之系統的現行系統負載。**附註：**只在 EAA 執行所在之系統上可以使用 `mpstat` 指令時，才能傳送 CPU 速率。否則，傳送前 1 分鐘的系統負載平均值。</br>「系統負載平均值是下列兩個數目的總和：為了可用處理器而置入佇列之可執行實體的數目，以及平均時間內在可用處理器上執行之可執行實體的數目。計算負載平均值的方式是作業系統特有的，但通常是衰减的時間相依平均值。如果沒有可用的負載平均值，則會傳回負值。」  
來自 ManagementFactory.getOperatingSystemMXBean 的 javadoc
`FreeMemory` | EAA 執行所在之「Java 虛擬機器 (JVM)」的可用記憶體的位元組數。
`MemoryUsed` | EAA 所使用之 JVM 記憶體的位元組數。
`InQueueSize` | 置入佇列以供 EAA 處理之訊息的數目。
`RuleNumber` | 規則引擎核心中已定義的規則數目。
`ProcessorNumber` | 用於除錯。規則引擎核心中已定義的處理器數目。</br>**附註：**處理器是規則引擎核心中的最小執行單位。
`DataPointsInWindow` | 時間範圍內緩衝的資料點總數。資料點的位元組大小視其資料類型而有所不同。例如，浮點/整數資料點大小為 8 個位元組，而字串資料點大小視其長度而有所不同。在大部分情況下，您可以使用下列公式，預估時間範圍的記憶體用量：`DataPointsInWindow * 8`。
