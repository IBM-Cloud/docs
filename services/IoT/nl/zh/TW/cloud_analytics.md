---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 雲端分析
{: #cloud_analytics}

您可以使用 {{site.data.keyword.iot_short}} 雲端分析，指定以即時裝置資料為依據的規則條件，用來在符合時觸發警示及選用性動作。    
{: shortdesc}

例如，您可以建立一個規則，以確保當裝置掉落時，或裝置溫度驟升時，將警示傳送至使用者裝置上的儀表板，並將電子郵件傳送給管理者。

## 開始之前
{: #byb}
請確定您要在規則中用來作為條件的裝置內容，已對映至綱目。如需相關資訊，請參閱[連接裝置](iotplatform_task.html)及[建立綱目](im_schemas.html)。

也請檢閱[使用 {{site.data.keyword.iot_short}} 雲端分析來使用規則及動作![外部鏈結圖示](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){: new_window} 秘訣，來瞭解「雲端分析」中所使用的規則及動作。

## 管理規則及動作  
{: #managing_rules}

使用**規則**儀表板，以建立及管理您組織的規則和動作。

若要取得已針對您裝置所觸發之規則及警示的概觀，請使用下列板：

 |板名稱 | 說明 |  
 |:---|:---|  
  |以規則為主的分析 | 顯示您組織的規則。其他卡片會列出已觸發的警示、關聯的裝置、裝置內容及警示資訊。 |  
 |以裝置為主的分析 | 顯示連接至您組織的裝置。其他卡片會顯示所選取裝置的警示、所選取裝置的資訊、裝置內容及警示資訊。 |

 如需預設分析板的相關資訊，請參閱[使用板及卡片視覺化即時資料](data_visualization.html#default_boards)。


## 建立規則
{: #rules}

規則是條件型決策點，用來比對即時裝置資料與預先定義的臨界值或其他內容資料，以在符合條件時觸發警示。除了 {{site.data.keyword.iot_short}} 儀表板中顯示的警示之外，您還可以新增一個以上的動作，以在觸發規則時執行商業邏輯。

**重要事項：**您必須先建立裝置類型的綱目，才能建立裝置類型的規則。如需相關資訊，請參閱[建立裝置類型綱目](im_schemas.html)。

若要建立規則，請執行下列動作：
1. 在 {{site.data.keyword.iot_short}} 儀表板中，移至**規則**。
2. 按一下**建立規則**、指定規則名稱、提供說明、選取規則適用的裝置類型，然後按**下一步**。  
3. 若要設定規則邏輯，請新增一個以上的 IF 條件，用來作為規則的觸發程式。  
您可以在平行列中新增條件，將它們套用為 OR 條件，或者在循序欄中新增條件，將它們套用為 AND 條件。
  
**重要事項：**若要觸發一個條件，而該條件會比較兩個內容，或觸發兩個以上使用 AND 循序結合的內容條件，則觸發資料點必須包含在相同的裝置訊息中。如果在多則訊息中收到資料，則不會觸發條件或循序條件。  
  
**範例：**   
如果參數值大於指定的值，則簡單的規則可能會觸發警示：
Condition = `temp_cpu>80`  
符合臨界值組合時，可能會觸發較複雜的規則：
Condition = `temp_cpu>60 AND cpu_load>90`   

4. 配置規則的條件式觸發需求。  
若要控制一段時間針對規則所觸發的警示數目，您可以配置規則的條件式觸發需求。  
**重要事項：**條件式觸發會對規則中的任何條件採取動作。例如，如果規則有五個使用 OR 設定的不同平行條件，則每一個符合的條件都會列入條件式觸發計數的計算中。若要設定規則的條件式觸發，請執行下列動作：
 1. 在規則編輯器中，按一下預設的**每次符合條件時觸發**鏈結，以開啟「設定頻率需求」對話框。
 2. 選取並配置您要在規則中使用的條件式觸發程式。
 <ul>
 <li>每次符合條件時觸發</li>
 <li>在 M 個*時間單位*內符合條件 N 次時觸發</li>
 </ul>  
 如需條件式觸發程式的其他詳細說明，請參閱[條件式規則觸發](#conditional "條件式觸發概觀")。
5. 建立或選取在符合規則條件時發生的一個以上動作。  
如需動作的相關資訊，請參閱[搭配使用動作與規則](#shared "建立動作")。   
例如：動作可以是傳送電子郵件或張貼 Webhook。
3. **選用項目：**選取規則的警示優先順序。  
優先順序是用來分類**規則型分析**板中所顯示的警示。預設優先順序是「低」。
6. 規則符合您的要求之後，請按一下**儲存**進行儲存而不啟動，或按一下**啟動**進行儲存並啟動規則。

即會建立您的規則。如果您啟動這個規則，則會在符合規則的條件時，將警示新增至**板 > 規則型分析**板，並執行任何規則動作。

## 條件式規則觸發
{: #conditional}

若要控制一段時間針對規則所觸發的警示數目，您可以配置規則的條件式觸發需求。

根據訊息頻率及規則條件，在符合觸發條件之後，規則可能會觸發許多次。例如，如果條件是 `temp >= 90`，而且溫度增加並穩定於 91，則每一則送入訊息都會觸發規則。根據裝置訊息的頻率，以及設定規則要執行的動作，這個警示數量可能會快速填滿電子郵件收件匣，或使訊息充斥在 Twitter 資訊來源而未提供任何額外值。

**重要事項：**條件式觸發會對規則中的任何條件採取動作。例如，如果規則有五個使用 OR 設定的不同平行條件，則每一個符合的條件都會列入條件式觸發計數的計算中。

條件 | 說明
------------- | -------------
每次符合條件時觸發 | 每次符合規則條件時，即觸發規則。
在 *M* *天/小時/分鐘/自訂*內符合條件 *N* 次時觸發 | 在選取的時間間隔內符合條件 *N* 次時會觸發規則，而且在配置的時段過去之前都不會再次觸發。</br>範例：條件式觸發需求 =`Trigger only once if conditions are met 4 times in 30 minutes`。裝置每隔五分鐘會傳送一則新訊息。在中午，溫度一開始超過 90 度（這符合條件）。條件式觸發計數器即會啟動，但尚未觸發規則。經過 15 分鐘，而且收到另外三則訊息指出 `temp > 90`，就會觸發規則。然後，不論溫度為何，另一個 15 分鐘內都不會觸發規則。
只在第一次符合條件時觸發，並於不再符合條件時重設。 | 在符合條件時觸發規則，但針對也符合條件的連續訊息則不會觸發規則。第一個不符合規則條件的訊息會重設觸發準則。
在條件持續 *M* *天/小時/分鐘/自訂* 時觸發。 | 如果在時間間隔期間收到的所有資料點都符合條件，或未收到任何其他資料點，則會在選取的時間間隔之後觸發規則。一開始符合條件時，時間間隔即開始。



## 在規則中使用動作
{: #shared}

除了在「警示」儀表板中顯示警示之外，{{site.data.keyword.iot_short}} 還支援數種類型的規則觸發動作，例如傳送電子郵件及張貼 Webhook。

您可以直接在規則編輯器中建立動作，或在「動作」標籤中建立動作，然後在建立規則時選取動作。

若要在「動作」標籤上建立動作，請執行下列動作：
1. 在 {{site.data.keyword.iot_short}} 儀表板中，移至**規則**。
2. 在「規則」儀表板中，選取**動作**標籤。
2. 按一下**建立動作**、指定動作名稱及說明，並選取動作類型，然後按**下一步**。
3. 為您所建立的動作類型提供必要的參數。
  
動作類型：  
 - [傳送電子郵件](#email "傳送電子郵件")
 - [IFTTT](#ifttt "IFTTT")
 - [Node-RED](#nodered "Node-RED")
 - [Webhook](#webhook "Webhook")
4. 按一下**確定**，以建立新的動作。

此動作現在會出現在規則編輯器中。

**附註：**後面的範例都使用下列規則條件來代表在溫度（以裝置的 `temp_cpu` 內容表示）超過 80 度時通知服務工程師的動作：`temp_cpu >= 80`

### 傳送電子郵件  
{: #email}
使用傳送電子郵件動作，在觸發規則時，將電子郵件傳送給一位以上的收件者。

範例：[傳送電子郵件](#emailex)。

下列參數用來配置傳送電子郵件動作：

參數 | 說明
---|---
名稱 | 動作的名稱（用於「警示」儀表板中）。
說明 | 動作的簡要說明。
主旨 | 電子郵件的主旨行。預設主旨行是 "IBM Watson IoT Alert: Mail action"。
收件者 | 選取以只將警示傳送給您自己，或傳送至以逗點區隔的電子郵件位址清單。如果您選擇傳送給您自己，則會將電子郵件傳送至您用來登入 {{site.data.keyword.iot_short}} 的電子郵件位址。
副本 | 無，或以逗點區隔的電子郵件位址清單。
電子郵件內文是透過觸發規則時的裝置訊息自動建立的。  
**重要事項：**電子郵件預設不包括可能包括機密性資訊的裝置資料。變更**包括資料**設定，以包括裝置資料。

#### 範例：使用傳送電子郵件
{: #emailex}

在此範例中，將動作配置成使用傳送電子郵件特性，以將電子郵件傳送給主要服務工程師，同時將備份電子郵件傳送給其主管。

若要建立「電子郵件」動作，請執行下列動作：
1. 在 {{site.data.keyword.iot_short}} 儀表板中，移至**規則**。
2. 按一下**建立動作**。
4. 輸入動作名稱 `Send service request email`。
5. 輸入說明 `Send an email to the service engineer and his manager`。
3. 選取**電子郵件**類型。
6. 在「收件者」欄位中，選取**特定人員**，然後輸入 `service.engineer@company.com`。
7. 在「副本」欄位中，選取**特定人員**，然後輸入：`service.manager@company.com`。
8. 在主旨行中，輸入：`Service required`。
10. 選取**包括資料**，以在電子郵件中包括裝置資料。
11. 按一下**完成**，以儲存動作。  


### IFTTT  
{: #ifttt}

使用 IFTTT 動作，以在觸發規則時觸發 IFTTT 秘訣。如需將動作觸發為 IFTTT 秘訣的相關資訊，請參閱 IFTTT 網站上的 [Maker 通道 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://ifttt.com/maker){: new_window}。

範例：[使用 IFTTT 張貼 Trello 卡片](#iftttex)。

下列參數用來配置 IFTTT 動作：

參數 | 說明
---|---
名稱 | 動作的名稱（用於「警示」儀表板中）。
說明 | 動作的簡要說明。
金鑰 | 用來觸發事件的「Maker 通道」金鑰。
事件 | 配置為「Maker 事件」的觸發程式的事件名稱。您可以使用不同的觸發程式來建立多個秘訣，這些觸發程式各有不同的事件名稱。
值 1-3 | 您可以在這些參數中傳遞任何內容，而這些參數會傳遞給 IFTTT 秘訣中的動作。**提示：**您可以使用[變數替代](#variable_substitution)，以在標頭中動態包括其他資料。

#### 範例：使用 IFTTT 張貼 Trello 卡片{: #iftttex}

在此範例中，將動作配置成使用 IFTTT，以將卡片張貼到 Trello 上的服務要求清單。

若要建立「在 Trello 上張貼卡片」動作，請執行下列動作：
1.	在 IFTTT 中，連接至 Trello 通道。
2.	在 IFTTT 中，連接至 Maker 通道。記下 IFTTT 金鑰。您需要此金鑰，才能從 {{site.data.keyword.iot_short_notm}} 連接至 IFTTT。
5.	在 IFTTT 中，建立秘訣：
 1. 按一下 **THIS**。
 2. 選取 **Maker** 通道。  
 2. 按一下**接收 Web 要求**。
 3. 輸入事件名稱 `post-Trello-card`。
 4. 按一下 **THAT**。
 5. 選取 **Trello** 通道。
 6. 選取要在其中建立卡片的 Trello 板。
 7. 輸入要在其中新增卡片的清單名稱。
 8. 編輯標題及說明。
 9. 指派 @service.engineer 及 @service.manager 成員。
 8. 按一下**建立動作**。   
3. 在 {{site.data.keyword.iot_short}} 儀表板中，移至**規則 > 動作**，然後建立具有下列參數的新動作：
<ul>
<li>類型 - **IFTTT**</li>
<li>名稱 - `Post service request card`</li>
<li>說明 - `Use IFTTT to post a card in the service requests list in Trello.`</li>
<li>金鑰 - 您的 IFTTT 金鑰</li>
<li>事件 - `post-Trello-card`</li>
<li>選擇性地新增「值 1-3」的值。**提示：**您可以使用[變數替代](#variable_substitution)，以動態包括裝置資料。</li>
</ul>
4. 按一下**確定**，以儲存動作。


### Node-RED
{: #nodered}

使用 Node-RED 動作，以在觸發規則時連接至 Node-RED 應用程式。如需使用 Node-RED 的相關資訊，請參閱[使用 Internet of Things 入門範本應用程式建立應用程式](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html)。

範例：[使用 Node-RED 傳送文字訊息](#noderedex)。

下列參數用來配置 Node-RED 動作：

參數 | 說明
---|---
名稱 | 動作的名稱（用於「警示」儀表板中）。
說明 | 動作的簡要說明。
URL | 目標 Node-RED HTTP 輸入節點的 URL。
使用者名稱 | 在 Node-RED 服務需要時包括。
密碼 | 在 Node-RED 服務需要時包含。**重要事項：**密碼是以明碼形式傳送。
內文 | 依預設，內文欄位會預先填入[變數替代](#variable_substitution)中所列的所有變數。

#### 範例：使用 Node-RED 傳送文字訊息
{: #noderedex}

在此範例中，將動作配置成搭配使用 Node-RED 與 Twilio 節點，以將文字訊息傳送給服務工程師。

若要建立「傳送文字訊息」動作，請執行下列動作：
1. 在 Twilio 中，找出或建立新的「傳訊服務」，以用來傳送 Twilio 帳戶的文字訊息。如需相關資訊，請參閱 [Twilio 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://www.twilio.com/help){: new_window}。
2. 在 Bluemix 中，使用 Node-RED URL `http://mynodered.mybluemix.net/red/` 來設定並存取 Node-RED 帳戶。如需相關資訊，請參閱 Bluemix 文件中的[使用 Node-RED 入門範本建立應用程式](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html)主題。
3. 在 Node-RED 中，建立簡式兩節點流程（例如 [RTI-alert]->[SMS]）。
  
其中，第一個節點是 http 節點，第二個節點則是 twilio 節點。
 1. 新增 "http" 輸入節點，並使用下列屬性進行配置：
  <ul>
  <li>方法 - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>名稱 - RTI Action</li>
  </ul>
  2. 新增 "http response" 輸出節點，並將它與 "http" 輸入節點連接在一起，方法是將某個節點的輸出埠拖曳至另一個節點的輸入埠。
  3. 新增 "twilio" 輸出節點，並使用下列屬性進行配置：
  <ul>
  <li>服務 - **External service**</li>
  <li>Twilio - Add new twilio-api</li>
  <li>SMS 至 - `Phone number for the service engineer`</li>
  <li>名稱 - **SMS**</li>
  </ul>
  4. 將節點連接在一起  
  將 http 與 twilio 節點連接在一起，方法是將某個節點的輸出埠拖曳至另一個節點的輸入埠。
  5. 按一下**部署**按鈕，以將流程部署至伺服器
4. 在 {{site.data.keyword.iot_short}} 儀表板中，移至**規則 > 動作**，然後建立具有下列參數的新動作：
 - 類型 - **Node-RED**
 - 名稱 - `Send text using Node-RED and Twilio`
 - 說明 - `Send a text message alert to the service engineer.`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - BODY   
 ```json
 {"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
5. 按一下**完成**，以儲存動作。



### Webhook
{: #webhook}

使用 Webhook 動作，以在觸發警示時對已啟用 Webhook 的 Web 服務提出 HTTP 要求。例如，如果裝置中的感應器報告異常讀數，則會使用 Webhook 來開啟資產的服務要求。

範例：[使用 Webhook 在 Slack 上張貼](#webhookex)。

下列參數用來配置 Webhook 動作：

參數 | 說明
---|---
名稱 | 動作的名稱（用於「警示」儀表板中）。
說明 | 動作的簡要說明。
URL | 目標已啟用 Webhook 之伺服器的 URL。**提示：**您可以使用[變數替代](#variable_substitution)，以在 URL 中動態包括其他資料。
方法 | 要執行的 Webhook 呼叫類型。請選取下列其中一種類型：GET、HEAD、OPTIONS、PATCH、PUT、POST 或 DELETE。
使用者名稱 | 在 Web 服務需要時包括。
密碼 | 在 Web 服務需要時包含。**重要事項：**密碼是以明碼形式傳送。
標頭 | 標頭是由索引鍵及值配對所構成。**提示：**您可以使用[變數替代](#variable_substitution)，以在標頭中動態包括其他資料。
內容類型 | 內文的內容類型：JSON、XML、WWW 形式 URL 編碼或純文字。可用於 OPTIONS、PATCH、PUT、POST 及 DELETE 方法。
內文 | Webhook 呼叫的內文。可用於 OPTIONS、PATCH、PUT、POST 及 DELETE 方法。依預設，內文欄位會預先填入[變數替代](#variable_substitution)中所列的所有變數。**重要事項：**Webhook 伺服器可能需要在內文中包括某些特定欄位。例如，Slack Webhook 必須包含 "text" 欄位。   

#### 範例：使用 Webhook 在 Slack 上張貼
{: #webhookex}

在此範例中，將動作配置成使用 Webhook，以將訊息張貼到 #service-requests Slack 通道。

若要建立「張貼到 Slack」動作，請執行下列動作：
1. 在 Slack 中，設定通道 #service-requests 的「送入 Webhook」整合。記下 Webhook URL。如需相關資訊，請參閱 [Slack 文件 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://api.slack.com/incoming-webhooks){: new_window}。
2. 在 {{site.data.keyword.iot_short}} 儀表板中，移至**規則 > 動作**，然後建立具有下列參數的新動作：
 - 名稱 - `Post service request on Slack`
 - 類型 - **Webhook**
 - URL - `Your Slack webhooks URL`
 - 方法 - **POST**
 - 內容類型 - `application/json`
 - 內文   
 ```json
 {"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
  **重要事項：**Slack Webhook 最少必須包含 "text" 欄位。如需相關資訊，請參閱 Slack 文件中的[送入 Webhook ![外部鏈結圖示](../icons/launch-glyph.svg)](https://api.slack.com/incoming-webhooks){: new_window}。
11. 按一下**完成**，以儲存動作。


### 變數替代  
{: #variable_substitution}

包括下列變數替代，以動態包括裝置資料。變數必須用雙大括弧括住。

變數 | 說明
---|---
**URL、Head 及 Body** |
`{{timestamp}}` | 訊息中的時間戳記。
`{{orgId}}` | {{site.data.keyword.iot_short_notm}} 服務的組織 ID。
`{{tenantId}}` | 已淘汰：{{site.data.keyword.iotrtinsights_full}} 服務的 ID。
`{{deviceId}}` | 裝置的 ID。
`{{ruleName}}` | 包括動作之規則的名稱。
`{{ruleID}}` | 包括動作之規則的 ID。
**僅內文** |
`{{ruleDescription}}`| 包括動作之規則的說明。
`{{ruleCondition}}` | 已觸發動作的規則條件。
`{{message}}` | 包括已觸發規則之資料點值的原始裝置訊息。
## 雲端分析的秘訣

下列秘訣說明如何將「雲端分析」特性用於不同的使用案例：

- [使用 IBM Watson™ IoT Platform 分析的即時資料分析 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/real-time-data-analysis-using-ibm-watson-iot-platform-analytics/){: new_window}

- [IOT 取樣資料的預測分析 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/predictive-analytics-on-iot-sample-data/){: new_window}

- [WIoTP 儀表板上的裝置清單卡 SIMPLIFIES 即時裝置監視 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/device-list-card-simplifies-real-time-device-monitoring-on-wiotp-dashboard/){: new_window}

- [在 IBM Watson IoT Platform 雲端分析中執行動作 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/perform-actions-in-ibm-watson-iot-platform-cloud-analytics/){: new_window}

- [使用 IBM Data Science Experience 偵測時間序列異常 ![外部鏈結圖示](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/use-ibm-data-science-experience-to-detect-time-series-anomalies/){: new_window}
