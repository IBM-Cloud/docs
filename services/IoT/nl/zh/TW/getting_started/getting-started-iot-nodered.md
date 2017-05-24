---

copyright:
  years: 2017
lastupdated: "2017-04-24"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 開始使用 {{site.data.keyword.iot_short_notm}} 入門範本
{: #gettingstartedtemplate}
<!-- Provide an appropriate ID above -->

使用「{{site.data.keyword.iot_short_notm}} 入門範本」GitHub 專案，以開始使用 {{site.data.keyword.iot_full}}。您可以使用「入門範本」，快速模擬裝置、建立卡片、產生資料，以及開始在 {{site.data.keyword.iot_short_notm}} 儀表板中分析及顯示資料。  
{:shortdesc}

## 概觀
{: #overview}  

入門範本會自動部署及連接這些服務：
<dl>
<dt>**{{site.data.keyword.iot_short_notm}}**</dt>
<dd>IoT Web 服務，包括閘道管理、裝置管理及應用程式存取。您可以使用 {{site.data.keyword.iot_short_notm}}，收集連接裝置的資料以及分析組織產生的即時資料。</dd>
<dt>**{{site.data.keyword.sdk4nodefull}}**</dt>
<dd>Node-RED 執行所在的運行環境。</br>如需相關資訊，請參閱 [{{site.data.keyword.sdk4nodefull}} 入門範本文件](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html)。</dd>
<dd>Node-RED 是一種工具，以全新且有趣的方式，將硬體裝置、API 和線上服務連接在一起。您可以使用 Node-RED 來建立模擬的恆溫器，將模擬資料傳送至 {{site.data.keyword.iot_short_notm}} 服務。您可以在 {{site.data.keyword.iot_short_notm}} 儀表板中建立卡片來顯示即時資料。</br>如需相關資訊，請參閱 [Node-RED 文件](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered)。</dd>
<dt>**{{site.data.keyword.cloudantfull}}**</dt><dd>Node-RED 在其中儲存 meta 資料的資料庫。</dd>
</dl>

## 開始之前
{: #byb}  

- 必要帳戶  
在開始之前，您需要 [IBM Bluemix 帳戶](https://bluemix.net/registration)。

- 隨意瀏覽  
若要更輕鬆地在下列程序的作業之間移動，請在瀏覽器的不同標籤中開啟 {{site.data.keyword.Bluemix_notm}} 儀表板、{{site.data.keyword.iot_short_notm}} 儀表板及 Node-RED 應用程式。
<dl>
<dt>*{{site.data.keyword.Bluemix_notm}} 儀表板*</dt>
<dd>查看部署的狀態、閱讀文件，以及啟動儀表板。</dd>
<dt>*{{site.data.keyword.iot_short_notm}} 儀表板*</dt>
<dd>定義裝置類型、登錄裝置、監視送入的感應器資料、建立資料視覺化卡，以及查看即時資料視覺化。</dd>
<dt>*Node-RED*</dt>
<dd>配置及執行裝置模擬器流程，以及使用其他流程來處理來自 {{site.data.keyword.iot_short_notm}} 的資料。</dd>
</dl>

## 步驟 1：部署 {{site.data.keyword.iot_short_notm}} 入門範本
{: #deployStarter}

請執行下列步驟來部署「入門範本」範例應用程式：

1. 部署入門範本應用程式。
 1. 按一下 <a href="https://bluemix.net/devops/setup/deploy?repository=https://github.com/ibm-watson-iot/iot-platform-bluemix-starter"><img src="https://bluemix.net/devops/graphics/create_toolchain_button.png" height=25></a>，以在 Bluemix 中建立新的「Continuous Delivery 工具鏈」：（透過 Continuous Delivery）  
 **提示：**如果您要從指令行進行部署，則可以在 GitHub 的 IBM Watson IoT 組織中[尋找 {{site.data.keyword.iot_short_notm}} 入門範本](https://github.com/ibm-watson-iot/iot-platform-bluemix-starter)。
 2. 系統提示時，登入 IBM Bluemix。
 3. 必要的話，請選取您要部署入門範本應用程式的「Bluemix 組織」。
 4. 保留「工具鏈」名稱，或視需要進行更新。它是用來作為預設應用程式名稱以及應用程式 URL 的根：`<app-name>.mybluemix.net`
 5. 按一下**建立**。  
**提示：**按一下 **Delivery Pipeline** 磚，以監視第一個部署的進度。
 6. 部署完成後，請按一下**檢視應用程式**，以在新的標籤中開啟新的 Node-RED 應用程式。
2. 尋找入門範本應用程式服務。
 1. 從 Bluemix 功能表中，選取**儀表板**。
 2. 在*所有服務* 下方，尋找下列服務：
    - iot-starter
    - iotp-starter-cloudantNoSQLDB
 3. 在*所有應用程式* 下方，尋找工具鏈：
    - default-toolchain-{id}}


## 步驟 2：在 {{site.data.keyword.iot_short_notm}} 中定義模擬裝置
{: #definingsimdev}

請完成下列步驟，來模擬使用恆溫器來監視客廳溫度、濕度及位置的情境。

1.	啟動 {{site.data.keyword.iot_short_notm}} 儀表板。
  1. 在 Bluemix 儀表板的*所有服務* 下方，按一下 {{site.data.keyword.iot_short_notm}} 實例的名稱。
**提示：**實例名稱通常包括 `iotp-starter`。
  2. 按一下**啟動**，以在新的瀏覽器標籤中開啟 {{site.data.keyword.iot_short_notm}} 儀表板。   
預設會顯示`所有板` 頁面。
2. 建立裝置類型。
  1.	從主功能表中，選取**裝置**，然後按一下**新增裝置**。
  2.	在「新增裝置」頁面中，按一下**建立裝置類型**。
  3.	在「建立裝置類型」頁面中，按一下**建立裝置類型**。
  4. 輸入裝置類型的唯一名稱（例如 `Thermostat`)，然後按**下一步**。
  5. 選用項目：在接下來的兩個頁面上定義範本及 meta 資料是選用作業，而且按一下每一個頁面上的**下一步**即可放心地略過。
  6.	按一下**建立**，以新增裝置類型。
3.	新增可使用新建裝置類型的裝置。
  1. 在「新增裝置」頁面上，您剛建立的裝置類型會顯示在裝置類型清單中。按**下一步**，以新增可使用該裝置類型的裝置。
  2. 輸入唯一裝置 ID（例如 `LivingRoomThermo1`）。
  3. 選用項目：在「新增裝置」頁面上提供敘述性資料或在下一頁上輸入裝置 meta 資料是選用作業，而且您可以按一下每一個頁面上的**下一步**放心地略過那些頁面。
  4. 在「安全」頁面上，按**下一步**，以產生裝置的鑑別記號。
  5. 在「摘要」頁面上，驗證資訊正確無誤，然後按一下**新增**，以新增裝置。按**上一步**，以回到上一頁。
4.	記下「您的裝置認證」頁面中所顯示的資訊。   
您需要下列資訊，才能配置模擬器以及顯示資料：
 - 組織 ID
  
 - 裝置類型
 - 裝置 ID
 - 鑑別方法
  
 - 鑑別記號
  

## 步驟 3：配置及執行 Node-RED 裝置模擬器。  
{: #confignodered}  
配置 Node-RED 裝置模擬器，以將包含溫度及濕度資訊的 MQTT 裝置訊息傳送至 {{site.data.keyword.iot_short_notm}}。

1. 啟動 Node-RED 流程編輯器。
  1. 在 Bluemix 儀表板的*所有應用程式* 下方，按一下工具鏈的名稱。  
**提示：**工具鏈名稱通常包括 `default-toolchain...`。
  2. 從工具鏈儀表板中，按一下**路徑**並選取路徑鏈結，以開啟 Node-RED 實例。  
  2. 按一下 **Go to your Node-RED flow editor**，以開啟編輯器。
2. 部署裝置。
  1. 在「裝置模擬器」流程中，按兩下藍色**傳送至 IBM IoT Platform** 節點。
  2. 驗證「鑑別」設為 **Bluemix 服務**。
  3. 輸入裝置的**裝置類型**及**裝置 ID**，然後按一下**完成**。
  4. 按一下**部署**，以部署裝置。
3. 配置「Node-RED 溫度監視器」流程。
  1. 在「裝置模擬器」流程中，按兩下藍色 **IBM IoT App In** 節點。
  2. 在「鑑別」中，選取 **Bluemix 服務**。
  3.	針對「裝置類型」、「裝置 ID」、「事件」及「格式」，選取**全部**。
  4.	按一下**完成**。
  5.  按一下**部署**，以部署監視器。
4. 驗證裝置連線。
  1.	開啟 {{site.data.keyword.iot_short_notm}} 儀表板。  
**提示：**如果尚未在另一個標籤中開啟 {{site.data.keyword.iot_short_notm}} 儀表板，請回到 {{site.data.keyword.Bluemix_notm}} 儀表板，並按一下 {{site.data.keyword.iot_short_notm}} 實例的名稱，然後按一下**啟動儀表板**。
  2. 從主功能表中，選取**裝置**。
  3. 按一下您新增的裝置名稱。   
裝置資訊會顯示裝置的連線狀態。
  4.	在 Node-RED 流程編輯器中，按兩下**傳送資料**節點，並將「重複值」設為**間隔**，然後將頻率設為每 `3` 秒。
  5. 按一下**完成**。
  6. 按一下**部署**，以部署變更。  
有效負載包含資料點（例如下列範例中所顯示的資料點）：
```
{"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
```
  7. 選用項目：開啟「除錯」標籤，以驗證正在建立訊息。
    1. 從標題區段中的功能表，選取**檢視**。
    2. 選取**顯示資訊看板**。
    3. 按一下「除錯」標籤，以查看訊息。
  8. 在「{{site.data.keyword.iot_short_notm}} 裝置資訊」頁面中，驗證於「感應器資訊」區段中看到來自裝置的資料點。


## 步驟 4：在 {{site.data.keyword.iot_short_notm}} 中建立卡片以顯示現用資料  
{: #createcards}  
建立板及卡片，以在 {{site.data.keyword.iot_short_notm}} 儀表板中顯示裝置資料。如需板及卡片的相關資訊，請參閱[使用板及卡片視覺化即時資料](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html)。

1. 建立板
  1. 開啟 {{site.data.keyword.iot_short_notm}} 儀表板。  
  **提示：**如果尚未在另一個標籤中開啟 {{site.data.keyword.iot_short_notm}} 儀表板，請回到 {{site.data.keyword.Bluemix_notm}} 儀表板，並按一下 {{site.data.keyword.iot_short_notm}} 實例的名稱，然後按一下**啟動儀表板**。  
  2. 建立板，以包含模擬裝置的卡片。
    1. 如果尚未顯示「所有板」頁面，請從 {{site.data.keyword.iot_short_notm}} 儀表板主功能表中選取**板**，然後按一下**建立新板**。
    2. 輸入板的名稱（例如 `Home Environment`），然後按**下一步**。
    3. 在下一頁上，按一下**提交**。  
  3. 按一下您剛建立的板，以進行開啟。
2. 建立卡片以顯示溫度
  1. 按一下**新增卡片**，然後從「裝置」區段中選取**折線圖**卡片類型。
  2. 從裝置清單中選取裝置，然後按**下一步**。
  3. 按一下**連接新資料集**。
  4. 在「建立儲值卡」頁面中，選取或輸入下列值，然後按**下一步**。
    - 事件：update
    - 內容：temp
    - 名稱：Temperature
    - 類型：Float
    - 單位：°C
    - 精準度：2
    - 最小值：0
    - 最大值：50
  5. 在「卡片預覽」頁面中，選取 **L** 表示折線圖大小，然後按**下一步**。
  6. 在「卡片資訊」頁面中，將卡片的名稱變更為 **Temperature**，然後按一下**提交**。   
溫度卡片會出現在儀表板上，並包括即時溫度資料的折線圖。
3. 建立卡片以顯示濕度
  1. 按一下**新增卡片**，然後從「裝置」區段中選取**量規**卡片類型。
  2. 從清單中選取裝置，然後按**下一步**。
  3. 按一下**連接新資料集**。
  4. 在「建立儲值卡」頁面中，選取或輸入下列值，然後按**下一步**。
  事件：update
     - 內容：humidity
     - 名稱：Humidity
     - 類型：Float
     - 單位：%
     - 精準度：1
     - 最小值：10
     - 最大值：95
  5. 在「卡片預覽」頁面中，選取 **M** 表示量規大小，然後按**下一步**。
  6. 在「卡片資訊」頁面中，將卡片的名稱變更為 **Humidity**，然後按一下**提交**。   
濕度卡片會出現在儀表板上，並包括顯示即時濕度資料的量規。  

<!-- 4. Create a card to display location
  1. Click **Add New Card**, and then select the **Value** card type, which is located in the Devices section.
  2. Select your device from the list, then click **Next**.
  3. Click **Connect new data set**.
  4. In the Create Value Card page, select or enter the following values.
     - Event: update
     - Property: location.latitude
     - Name: Latitude
     - Type: Float
     - Unit: "°N"
     - Precision: 2
     - Min: -180
     - Max: 180
  5. Click **Connect new data set**.
  6. In the Create Value Card page, select or enter the following values and click **Next**.
     - Event: update
     - Property: location.longitude
     - Name: Longitude
     - Type: Float
     - Unit: "°E"
     - Precision: 2
     - Min: -180
     - Max: 180
  7. In the Card Preview page, select **M** as the text size, and click **Next**.
  8. In the Card Information page, change the name of the card to **Location** and click **Submit**.   
The location card appears on the dashboard and shows the live latitude and longitude of the device.-->

## 下一步為何？  
{: #whats-next}  
現在您的模擬裝置正在傳送資料至 {{site.data.keyword.iot_short_notm}}，您可以繼續反覆運算 IoT 專案。
 - 「觀看卡片」會顯示 node-RED 流程所產生的資料。  
Node-Red 會繼續傳送資料，直到您停止它為止。若要停止模擬資料，請執行下列步驟：
    1.	在 Node-RED 流程編輯器中，按兩下灰色**傳送資料**節點，並將「重複值」設為**間隔**，然後將頻率設為每 **3** 秒。
    2. 按一下**完成**。
    3. 按一下**部署**，以部署變更。

 - 連接實體裝置。  
[搜尋 IoT Recipes](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot) 以連接實體裝置（例如 Raspberry Pi），然後將資料傳送至 {{site.data.keyword.iot_short_notm}}。

 - 探索視覺化選項。  
[部署範例 node.js 應用程式，以視覺化裝置資料](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html)。

 -	以密碼保護 Node-RED 流程編輯器。   
依預設，任何人都能開啟編輯器來存取及修改流程。若要以密碼保護編輯器，請執行下列作業：
    1.	在 {{site.data.keyword.Bluemix_notm}} 儀表板中，按一下「入門範本」應用程式的名稱，以開啟應用程式頁面。
    2. 按一下**運行環境**，以顯示「運行環境」頁面。
    3. 按一下**環境變數**，以顯示「環境變數」頁面。
    4. 在**使用者定義**區段中，按一下**新增**，然後輸入下列使用者定義變數：
         -	NODE_RED_USERNAME - 用來保護編輯器的使用者名稱
         -	NODE_RED_PASSWORD - 用來保護編輯器的密碼
    3.	按一下**儲存**。
