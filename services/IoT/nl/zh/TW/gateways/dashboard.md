---

copyright:

years: 2015, 2017

lastupdated: "2017-03-16"


---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 連接閘道
{: #IoT_connectGateway}

您必須先將閘道連接至 {{site.data.keyword.iot_full}}，才能開始接收來自連接至閘道之裝置的資料。若要將閘道連接至 {{site.data.keyword.iot_short_notm}}，需要建立閘道裝置類型，並且向 {{site.data.keyword.iot_short_notm}} 登錄閘道。然後，您就可以使用登錄資訊，將閘道連接至 {{site.data.keyword.iot_short_notm}}。
{:shortdesc}

閘道是 {{site.data.keyword.iot_short_notm}} 中的特殊化類別裝置。閘道可作為其他裝置的 {{site.data.keyword.iot_short_notm}} 存取點。


## 開始之前
{: #Prerequisites}

相較於一般裝置，閘道裝置具有額外的許可權，並且可以執行下列功能：
- 向 {{site.data.keyword.iot_short_notm}} 登錄新裝置
- 傳送及接收其專屬的感應器資料，例如直接連接的裝置，
- 代表與其連接的裝置來傳送及接收資料
- 執行裝置管理代理程式，以讓它受管理，以及管理與其連接的裝置。  
如需閘道開發人員資訊，請參閱[閘道的 MQTT 連線功能](mqtt.html)。

您也可以使用閘道來對閘道裝置所傳送的資料執行邊緣分析。如需相關資訊，請參閱[邊緣分析](../edge_analytics.html)及[安裝邊緣分析代理程式](#edge)。

## 步驟 1：向 {{site.data.keyword.iot_short_notm}} 登錄您的閘道  
{: #register_gateway}

若要登錄閘道，需要將裝置分類成閘道類型、為閘道命名，並提供閘道資訊。然後，您可以提供連線記號，或是接受 {{site.data.keyword.iot_short_notm}} 產生的記號。


**提示：**您可以從 {{site.data.keyword.iot_short_notm}} 儀表板一次新增一個閘道，或是使用[組織管理 API ![外部鏈結圖示](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Bulk_Configuration/post_bulk_devices_add){: new_window}，一次新增一個以上閘道。

若要從 {{site.data.keyword.iot_short_notm}} 儀表板新增閘道，請執行下列動作：

1. 在 {{site.data.keyword.iot_short_notm}} 儀表板中，選取**裝置**。
2. 按一下**新增裝置**。
3. 選取或建立您要新增之裝置的裝置類型。  
連接至 {{site.data.keyword.iot_short_notm}} 的每一個裝置都必須與裝置類型相關聯。裝置類型是一群共用相同性質的裝置。  
 1. 按一下**建立裝置類型**，然後按一下**建立閘道類型**。
 2. 輸入裝置類型名稱（例如 `my_gateway_type`）和閘道類型的說明。   
 **重要事項：**裝置類型名稱不得超過 36 個字元，且只能包含：
 <ul>
  <li>英數字元（a-z 、A-Z、0-9）</li>
  <li>連字號 (-)</li>
  <li>底線 (&lowbar;)</li>
  <li>句點 (.) </li>
  </ul>3. 選用項目：輸入閘道類型屬性和 meta 資料。    
 **提示：**您可以稍後再新增及編輯屬性和 meta 資料。
 4. 按一下**建立**，以新增閘道類型。
10. 按**下一步**，開始新增所選取閘道類型的閘道裝置。
11. 輸入裝置 ID，例如 `my_gateway_device`。  
裝置 ID 可用來識別 {{site.data.keyword.iot_short_notm}} 儀表板中的閘道裝置，它也是將閘道裝置連接至 {{site.data.keyword.iot_short_notm}} 的必要參數。  
**重要事項：**裝置 ID 不得超過 36 個字元，且只能包含：
 <ul>
 <li>英數字元（a-z 、A-Z、0-9）</li>
 <li>連字號 (-)</li>
 <li>底線 (&lowbar;)</li>
 <li>句點 (.) </li>  
 </ul>
 **提示：**若為連接網路的裝置，裝置 ID 可以是（例如）不含任何分隔冒號的裝置 MAC 位址。  
12. 選用項目：按一下**其他欄位**，以新增閘道裝置資訊，例如序號、製造商、機型等等。  
   
 **提示：**您可以稍後再新增及編輯此資訊。
12. 選用項目：輸入裝置 JSON meta 資料。  
   
 **提示：**您可以稍後再新增及編輯裝置 meta 資料。
13. 按**下一步**，以完成新增閘道裝置。
14. 驗證摘要資訊正確無誤，然後按一下**新增**，以新增閘道裝置。  
  
**提示：**您可以選擇接受自動產生的鑑別記號，或是自行提供鑑別記號。如果您選擇自行建立記號，請確定其長度介於 8 到 36 個字元之間、包含大小寫混合的字母、數字，以及連字號、底線或句點。記號不得包含重複的字元順序、字典單字、使用者名稱或其他預先定義的順序。
15. 在裝置資訊頁面中，複製並儲存下列裝置資訊：  
 - 組織 ID，例如 `tubo8x`
 - 裝置類型，例如 `my_gateway_type`
 - 裝置 ID。**提示：**若為連接網路的裝置，這個值可以是（例如）沒有任何分隔冒號的 MAC 位址。
 - 鑑別方法，例如 `token`
 - 鑑別記號，例如 `PtBVriRqIg4uh)_-Kl`  
  **提示：**您需要有「組織 ID」、「鑑別記號」、「裝置類型」及「裝置 ID」，才能配置您的裝置來連接至 {{site.data.keyword.iot_short_notm}}。  

恭喜，您已登錄閘道裝置。現在您可以配置閘道裝置來連接至 {{site.data.keyword.iot_short_notm}}

如需示範登錄閘道所需流程的逐步指示，請參閱[如何在 IBM Watson IoT Platform 中登錄閘道 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/how-to-register-gateways-in-ibm-watson-iot-platform/){:new_window} 秘訣。

## 步驟 2：將您的閘道連接至 {{site.data.keyword.iot_short_notm}}
{: #connect_gateway}

向 {{site.data.keyword.iot_short_notm}} 登錄閘道之後，請使用登錄資訊來將閘道連接至 {{site.data.keyword.iot_short_notm}}，並開始接收來自連接至閘道之裝置的資料。

如需有關將閘道連接至 {{site.data.keyword.iot_short_notm}} 的詳細資訊，請參閱[閘道的 MQTT 連線功能](mqtt.html)。

**提示：**有一系列的秘訣可用來將裝置連接到 {{site.data.keyword.iot_short_notm}}。若要取得秘訣清單，請參閱 IBM.com 上的[裝置連線秘訣![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window}。


## 步驟 3：透過閘道來連接裝置
{: #gateway_devices}

已連接至閘道的裝置，會在閘道從裝置發佈訊息時，自動新增至 {{site.data.keyword.iot_short_notm}}。當閘道針對尚未存在的裝置類型與裝置 ID 組合發佈訊息時，就會自動建立裝置類型與裝置本身。

如需裝置自動登錄，以及為已連接裝置發佈和接收資料的相關資訊，請參閱[閘道的 MQTT 連線功能](mqtt.html)。


當裝置順利連接至閘道時，它會顯示在 {{site.data.keyword.iot_short_notm}} 組織的儀表板上。

如需詳細流程及說明，請參閱[將 Raspberry Pi 當作閘道連接至 Watson IoT ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-as-a-gateway-to-watson-iot-using-node-red/){:new_window} 秘訣。

**附註：**在 {{site.data.keyword.iot_short_notm}} 儀表板中，直接連接到 {{site.data.keyword.iot_short_notm}} 的裝置和閘道會顯示狀態圖示，指出其已連接。儀表板會將透過閘道間接連接的裝置顯示為中斷連線，因為它無法得知裝置對閘道的連線情形。


## 安裝邊緣分析代理程式
{: #edge}

「邊緣分析代理程式」(Edge Analytics Agent, EAA) 是一種軟體元件，建置在針對邊緣處理最佳化的串流引擎之上，它會從 {{site.data.keyword.iot_short_notm}} 儀表板上傳及管理邊緣分析規則，以在閘道上執行邊緣分析作業。如需邊緣分析的相關資訊，請參閱[邊緣分析](../edge_analytics.html)。

### 安裝 EAA
{: #eaa_install}

若要將 EAA 安裝在您的閘道上，請執行下列動作：
1. 在 {{site.data.keyword.iot_short}} 儀表板中，移至**規則**。
2. 按一下**下載邊緣代理程式**，以移至 [IBM 邊緣分析社群 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true){:new_window}。
3. 導覽至**檔案**區段，並針對您的閘道類型，下載適當的壓縮目錄。  
針對支援 Java 的裝置，「邊緣分析」解決方案可用來當作 SDK，針對 Cisco 閘道裝置，則可用來當作 DSLink。
4. 如需如何在閘道上安裝及配置 EAA 軟體元件的相關資訊，請參閱下列資訊：
 - SDK  
請參閱 PDF 和 Readme 檔，以及社群中可用的視訊鏈結。  
 [Edge Recipe for SDK - 開始使用 (SDK) ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/tutorials/getting-started-with-the-ibm-edge-analytics-sdk-in-watson-iot-platform/){:new_window} 秘訣。
 - DSLink  
 [開始在 Watson IoT Platform 中使用邊緣分析 ![外部鏈結圖示](../../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/recipes/?post_type=pnext_tutorial&p=19472){:new_window} 秘訣。

### EAA 配置設定
{: #eaa_configuration}

您可以使用 EAA config.properties 檔案來設定基本軟體配置參數。

若要更新 EAA 配置，請執行下列動作：
1. 在 EAA 執行的閘道系統上，找出 EAA config.properties 檔案。  
例如：
`../dglux-server/dslinks/ibm-watson-iot-edge-analytics-dslink-java-0.0.1/config.properties`
2. 在開始編輯設定之前，請先備份檔案。
3. 開啟 config.properties 檔案以進行編輯。
4. 針對您的環境來編輯配置參數：
 <dl>
 <dt>DataDirectSendEnable</dt>
 <dd>布林值 (true|false)</br>
 TRUE（預設值）- 將所有資料傳送至 {{site.data.keyword.iot_short_notm}}。</br>
 FALSE - 唯有在引擎上設定規則時，才能將資料傳送至 {{site.data.keyword.iot_short_notm}}。</dd>
 <dt>MonitorInterval</dt>
 <dd>整數（毫秒）</br>
 將新的監視訊息傳送至 {{site.data.keyword.iot_short_notm}} 之前的時間（毫秒）。</br>
 設定的值愈小，報告監視度量值的頻率就愈高。設定的值愈大，{{site.data.keyword.iot_short_notm}} 的監視資訊就愈詳細。</br>
 預設值：60000    </br>
 建議範圍：[1000, 360000]</dd>
 <dt>MonitorLogDesample</dt>
 <dd>整數  </br>
 將傳送至 {{site.data.keyword.iot_short_notm}} 的監視訊息數，與在本端日誌中輸入的訊息數相互比較的反取樣比例。例如，如果 `MonitorLogDesample` 設為 10，則每傳送 10 則訊息至 {{site.data.keyword.iot_short_notm}}，只會寫入一個本端日誌項目。</br>數值較大，可讓本端日誌維持較小的狀態。數值較小，則會提供較詳細的本端日誌。</br>
 預設值：10</br>
 建議範圍：[1, 100]</dd>
 <dt>MemoryAlertThreshold</dt>
 <dd>整數 (MB)</br>
 達到這個可用 JVM 資料堆記憶體臨界值時，就會傳送記憶體警告日誌訊息至 {{site.data.keyword.iot_short_notm}} 診斷日誌。此警示是由監視作業驅動。</br>數值較小，可減少傳送至 {{site.data.keyword.iot_short_notm}} 的警示訊息數。數值較大，可在 EAA 伺服器快要發生記憶體問題時，盡早警告您。</br>**提示：**您可以使用[雲端分析](../cloud_analytics.html)規則來配置警示動作，例如傳送電子郵件通知，以警示您有記憶體問題。如需可用來建置規則之內容的相關資訊，請參閱[邊緣分析代理程式診斷度量](../edge_analytics.html#eaa_metrics)。</br>
 預設值：10</br>
 建議範圍：[10 或總記憶體的 5% , 200]</dd>
 </dl>
5. 儲存已編輯的檔案，然後重新啟動 EAA。

EAA config.properties 檔案範例
```
#######################################################################
# Engine Parameters
#######################################################################
# DataDirectSendEnable
#                    - BOOLEAN(true|false) Set to true to forward all
#                      the data; Set to false to disable data direct
#                      send to IOTP when there is no rule set in the
#                      engine.
#                      DEFAULT: true
#######################################################################
DataDirectSendEnable=true

#######################################################################
# Monitoring Parameters
#######################################################################
# MonitorInterval    - INTEGER Time interval in milliseconds before a  
#                      new monitoring message is generated. Set it to a
#                      small value to report the monitor metrics more
#                      frequently. Set it to a big value to have more
#                      detailed monitoring information on IoTP.
#                      DEFAULT: 60000    RECOMMEND: [1000, 360000]
# MonitorLogDesample - INTEGER The de-sampling ratio of the number of
#                      monitoring messages sent to IOTP vs. local log,
#                      i.e. number of monitoring messages N where
#                      EAA would output only one to the Info log for
#                      every N messages. Set it big to keep the size
#                      of the log small. Set it small to have detailed
#                      monitoring information in local log.
#                      DEFAULT: 10       RECOMMEND: [1, 100]
# MemoryAlertThreshold
#                    - INTEGER the free JVM heap memory in megabyte under
#                      which a log message would be generated and send to
#                      IOTP diagnosis log. The alert is driven by the
#                      monitoring. Set it small to eliminate unnecessary
#                      alert message on IoTP. Set it big to receive early
#                      alert when the system is likely to crash. Set to
#                      Min(Max(10MB, 5% of the total memory), 200MB) is
#                      recommended.
#                      DEFAULT: 10       RECOMMEND: [10, 200]
#######################################################################

MonitorInterval=60000
MonitorLogDesample=10
MemoryAlertThreshold=10
```
