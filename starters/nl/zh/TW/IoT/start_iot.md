---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 開始使用 {{site.data.keyword.iot_short_notm}} 入門範本
{: #gettingstartedtemplate}
<!-- Provide and appropriate ID above -->
*前次更新：2016 年 6 月 27 日*
{: .last-updated}

利用「{{site.data.keyword.iot_short_notm}} 入門範本」樣板，開始使用 {{site.data.keyword.iot_full}}。透過「入門範本」，您可以快速模擬裝置、建立卡片、產生資料，並開始在 {{site.data.keyword.iot_short_notm}} 儀表板中分析及顯示資料。
{: shortdesc}

「入門範本」會自動部署及連接下列服務：

{{site.data.keyword.iot_short_notm}} - 此平台提供多用途的 IoT 工具箱，其中包含閘道裝置、裝置管理功能，以及功能強大的應用程式存取。透過 {{site.data.keyword.iot_short_notm}}，您可以收集連接裝置的資料，並針對組織產生的即時資料執行分析。

{{site.data.keyword.sdk4nodefull}} - 建立供 Node-RED 在其中執行的運行環境。

{{site.data.keyword.cloudantfull}} - 供 Node-RED 在其中儲存 meta 資料的資料庫。

## 關於 {{site.data.keyword.iot_short_notm}}
{: #about_iotplatform}
{{site.data.keyword.iot_short_notm}} 提供功能強大的應用程式存取，可讓您存取 IoT 裝置和資料，以協助您快速組合分析應用程式、視覺化儀表板和行動 IoT 應用程式。
{{site.data.keyword.iot_short_notm}} 可讓您執行功能強大的裝置管理作業、儲存和存取裝置資料，以及連接各式各樣的裝置和閘道裝置。{{site.data.keyword.iot_short_notm}} 採用 MQTT 和 TLS，可讓您與裝置之進行安全通訊。

## 關於 Node-RED
{: #about_nodered}
Node-RED 是一種可讓您以新鮮有趣的方法，將硬體裝置、API 和線上服務連接在一起的工具。您可以使用 Node-RED 來建立模擬的恆溫器，將模擬資料傳送至 {{site.data.keyword.iot_short_notm}} 服務。您可以在 {{site.data.keyword.iot_short_notm}} 儀表板中建立卡片來顯示即時資料。如需相關資訊，請參閱 [Node-RED 文件](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered)。

## 隨意瀏覽
{: #gettingaround}
您在執行下列步驟時，將會使用瀏覽器中三個不同的標籤：
  1. *{{site.data.keyword.Bluemix_notm}} 儀表板* - {{site.data.keyword.Bluemix_notm}} 儀表板可用來查看您的部署狀態、閱讀文件，以及啟動儀表板。
  2. *{{site.data.keyword.iot_short_notm}} 儀表板* - 此儀表板可用來處理此服務。您可以使用此儀表板來定義裝置類型、登錄裝置、監視送入的感應器資料、建立資料視覺化卡片，以及查看即時資料視覺化。
  3. *Node-RED* - 作為 node.js Web 應用程式來執行，您可以配置及執行裝置模擬器流程，以及搭配其他流程來處理 {{site.data.keyword.iot_short_notm}} 產生的資料。

## 定義 {{site.data.keyword.iot_short_notm}} 中的模擬裝置
{: #definingsimdev}
向 {{site.data.keyword.iot_short_notm}} 登錄您的裝置：
  1.	在 {{site.data.keyword.Bluemix_notm}} 中，移至您部署之應用程式的概觀標籤。
  2.	按一下「連線」區段或標籤中的 {{site.data.keyword.iot_short_notm}} 方框。
  3.	按一下「啟動儀表板」，以在新的瀏覽器視窗中開啟 {{site.data.keyword.iot_short_notm}} 儀表板。
  4.	選取「裝置」。
  5.	按一下「新增裝置」。
  6.	在「新增裝置」對話框中按一下「建立裝置類型」。
  7.	在「建立裝置類型」對話框中按一下「建立裝置類型」。
  8. 輸入裝置類型的敘述性名稱和說明，例如「恆溫器」。
  9.	跳過：「定義範本」。
  10.	跳過「meta 資料」。
  11.	按一下「建立」，以新增裝置類型。
  12.	按「下一步」以新增您的裝置（已預先選取「選擇裝置類型」）。
  13.	輸入裝置 ID，例如 LivingRoomThermo1。
  14.	跳過：輸入裝置 meta 資料。
  15.	按「下一步」，以新增具有自動產生之鑑別記號的裝置連線。
  16.	驗證摘要資訊是否正確，然後按一下「新增」以新增連線。
  17.	在開啟的裝置資訊頁面中，複製並儲存裝置資訊：
      -	組織 ID
      -	裝置類型
      -	裝置 ID 
      - 鑑別方法
      - 鑑別記號

**提示**：在後續幾個步驟中，您將會需要「組織 ID」、「裝置類型」和「裝置 ID」，才能完成 Node-RED 應用程式的配置，以完成連線。

## 配置及執行 Node-RED 裝置模擬器。
{: #confignodered}
配置 Node-RED 裝置模擬器。使用裝置模擬器將 MQTT 裝置訊息傳送至 {{site.data.keyword.iot_short_notm}}。裝置模擬器會將溫度和濕度資訊傳送至 {{site.data.keyword.iot_short_notm}}。

1. 在 Bluemix 儀表板中，選取**檢視應用程式**或按一下鏈結（例如，http://myIoTApp.mybluemix.net），以開啟 Node-RED。
2.	按一下 **Go to your Node-RED flow editor**，以開啟編輯器。
3.	在 Device Simulator 流程中，按兩下藍色的 **Send** to {{site.data.keyword.iot_short_notm}} 節點。
  1.	驗證 Authentication = Bluemix Service。
  2.	貼上來自您登錄裝置的 Device Type。
  3.	貼上來自您登錄裝置的 Device ID。
  4.	按一下 Done。
4.	按一下 Node-RED 流程編輯器右上角的 **Deploy**。
5.	配置 Node-RED Temperature Monitor 流程
  1.	在 Device Simulator 流程中，按兩下藍色的 IBM IoT App In 節點。
  2.	將 Authentication 變更為 Bluemix Service。
  3.	Device Type、Device Id、Event 及 Format 皆選取 All。
  4.	按一下 Done。
6.	按一下 Node-RED 流程編輯器右上角的 **Deploy**。
7.	驗證裝置連線
  1.	在其他瀏覽器分頁或視窗中，回到 {{site.data.keyword.iot_short_notm}} 儀表板。
  2.	選取「裝置」，然後按一下 LivingRoomThermo1 或您新增的裝置名稱（如果不同的話）。裝置資訊頁面隨即開啟。此視圖可讓您查看裝置的連線狀態。裝置狀態為中斷連線。
  3.	回到 Node-RED 流程編輯器，按一下灰色 Send Data 節點上的按鈕，以產生資產有效負載。有效負載包含下列資料點：
  ```
  {"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
  ```
  4.	在右窗格的除錯標籤中，驗證已建立訊息。
  5.	在 {{site.data.keyword.iot_short_notm}} 裝置資訊頁面中，驗證您在「感應器資訊」區段中看到的資料點與從裝置接收到的相同。

8.	將您的範例 IoT 裝置連接至 {{site.data.keyword.iot_short_notm}}，以檢視裝置資料。

## 在 {{site.data.keyword.iot_short_notm}} 中建立卡片以顯示即時資料
{: #createcards}
若要建立卡片，請執行下列作業。

### 每 3 秒自動產生資料
1. 在 Node-RED 標籤中，按兩下 Send Data 節點
2.	將 Repeat 設為 Interval Every 3 seconds
3.	部署

### 在儀表板中建立新的卡片
1. 移至 {{site.data.keyword.iot_short_notm}} 儀表板瀏覽器分頁。
2. 選取「板」。
3. 按一下「建立新的板」。
4. 為其命名，例如「住家環境」。
5. 建立。
6. 按一下「新增卡片」（用於溫度）。
   1.	在「裝置」之下，選取「即時」圖表。
   2.	卡片來源資料，勾選您的裝置 "LivingRoomThermo1"，然後按「下一步」。
   3. 連接新的資料集。
       - 名稱：溫度
       - 事件：更新
       - 內容：temp
       - 類型：浮動
       - 單位：°C
       - 精準度：2
       - 最小值：0
       - 最大值：50
       - 下一步
  4. 卡片預覽。
       - 選取 L
       - 下一步
  5. 卡片資訊。
       - 標題：溫度
  6.	提交。
  7.	溫度卡片會出現在儀表板上，其中包含即時溫度資料的圖形。
7.	按一下「新增卡片」（用於濕度）。
  1.	在「裝置」之下，選取「顯示更多」。
  2.	選取「量規」。
  3.	卡片來源資料，勾選您的「裝置」，然後按「下一步」。
  4.	連接新的資料集。
       -	名稱：濕度
       -	事件：更新
       -	內容：humidity
       -	類型：浮動
       -	單位：「% 相對濕度」
       -	精準度：1
       -	最小值：10
       -	最大值：95
       -	下一步
  5.	卡片預覽。
       -	設定
          -	低臨界值：40% 和普通
          -	中間：良好
          -	高臨界值：50% 和普通
       -	選取 M
       -	下一步
  6.	卡片資訊。
       -	標題：濕度
  7.	提交。
  8.	濕度卡片會出現在儀表板上，其中包含即時濕度資料的量規。
8.	按一下「新增卡片」（用於位置）。
  1.	在「裝置」之下，選取「顯示更多」。
  2.	選取「值」。
  3.	卡片來源資料，勾選您的裝置 "LivingRoomThermo1"，然後按「下一步」。
  4.	連接新的資料集。
       -	名稱：緯度
       -	事件：更新
       -	內容：location.latitude
       -	類型：浮動
       -	單位："°N"
       -	精準度：2
       -	最小值：-180
       -	最大值：180
  5. 連接新的資料集。
       -	名稱：經度
       -	事件：更新
       -	內容：location.longitude
       -	類型：浮動
       -	單位："°E"
       -	精準度：2
       -	最小值：-180
       -	最大值：180
       -  下一步
  6.	卡片預覽。
       -	選取 L
       -	下一步
  7.	卡片資訊。
       -	標題：位置
  8.	提交。
9.	使用 Node-RED 流程產生的模擬器資料，即時監看新的卡片更新。
**附註**：Node-RED 會持續傳送資料，直到您將它停止。
10.	在 Node-RED 流程編輯器中，將 Send Data 節點更新為 Repeat: none。
11.	部署。

## 下一步為何？
{: #whatsnext}
現在您的模擬裝置正在傳送資料至 {{site.data.keyword.iot_short_notm}}，您可以繼續反覆運算 IoT 專案。

1. [搜尋我們的 IoT 秘訣](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot)，以連接 Raspberry Pi 之類的實體裝置，並將資料傳送至 {{site.data.keyword.iot_short_notm}}。
2. [部署範例 node.js 應用程式，以將裝置資料視覺化。](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html)
3.	以密碼保護 Node-RED 流程編輯器。依預設，任何人都能使用編輯器來存取及修改流程。若要以密碼保護編輯器，請執行下列作業：
  1.	在 Bluemix 儀表板中，選取應用程式的「環境變數」頁面。
  2.	新增下列使用者定義變數：
       -	NODE_RED_USERNAME - 用來保護編輯器的使用者名稱
       -	NODE_RED_PASSWORD - 用來保護編輯器的密碼
  3.	按一下「儲存」。


# 相關鏈結
{: #rellinks}

## 指導教學及範例
{: #samples}
* [用來連接裝置的秘訣](https://developer.ibm.com/recipes/?post_type=tutorials&s=iot){:new_window}
* [{{site.data.keyword.iot_short}} Play 組織](https://play.internetofthings.ibmcloud.com/){:new_window}
* [將 Intel Galileo 連接至 {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/connect-an-intel-galileo-to-the-internet-of-things-foundation-connect/){:new_window}
* [連接 ARM&reg; mbed&trade; IoT 入門範本套件](https://developer.ibm.com/recipes/tutorials/arm-mbed-iot-starter-kit-part-1/){:new_window}
* [將 Raspberry Pi 連接至 {{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/tutorials/raspberry-pi-4/){:new_window}

## API 參考資料
{: #api}
* [{{site.data.keyword.iot_short}}API 文件](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#/){:new_window}


## 相關鏈結
{: #general}
* [{{site.data.keyword.iot_short_notm}} 文件](https://www.bluemix.net/docs/services/IoT/iotplatform_overview.html){:new_window}
* [{{site.data.keyword.sdk4nodefull}} 入門範本文件](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html){:new_window}
