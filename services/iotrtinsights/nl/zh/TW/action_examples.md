---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# 動作範例

「傳送電子郵件」、IFTTT、Node-RED 及 Webhook 動作類型會開啟用於執行作業的整個選項範圍，而此範圍僅受限您的想像以及其他工具所使用的連接器。例如，在 Slack 上張貼裝置狀態訊息、將文字訊息傳送給服務人員、建立裝置服務要求等等動作。
{: shortdesc}

下列範例都使用下列規則條件來代表溫度（以裝置的 temp 資料點代表）超過 100 度時用來通知服務工程師的動作：
`temp >= 100`

發生規則條件時，您可以觸發下列一個以上的動作類型：  
 - [傳送電子郵件](#emailex "傳送電子郵件")
 - [Webhook](#webhookex "Webhook")
 - [Node-RED](#noderedex "Node-RED")
 - [IFTTT](#iftttex "IFTTT")

## 使用傳送電子郵件{: #emailex}
在此範例中，動作配置成使用 Real-Time Insights「傳送電子郵件」特性，將電子郵件傳送至主要服務工程師，同時將備份電子郵件傳送給他的經理。

若要建立電子郵件動作，請執行下列動作：
1. 在 Real-Time Insights 中，移至**分析 > 動作**。
2. 按一下**新增動作**。
3. 選取**傳送電子郵件**類型。
4. 輸入動作名稱 `Send service request email`。
5. 輸入說明 `Send an email to the service engineer and his manager`。
6. 在「收件者」欄位中，輸入 `service.engineer@company.com`。
7. 在「副本」欄位中，輸入：`service.manager@company.com`。
8. 在主旨行中，輸入：`Service required`。
9. 選取以在前面附加 "{{site.data.keyword.iotrtinsights_short}} alert"，來釐清電子郵件的來源位置。
10. 若要在電子郵件中包括裝置資料，請清除**不要在電子郵件訊息中包括裝置資料**勾選框。
11. 按一下**確定**，以儲存動作。  




## 使用 Webhook 在 Slack 上進行張貼{: #webhookex}

在此範例中，動作配置成使用 Webhook 將訊息張貼至 #service-requests Slack 通道。

若要建立張貼至 Slack 動作，請執行下列動作：
1. 在 Slack 中，設定 #service-requests 通道的「送入 Webhook」整合。請記下 Webhook URL。如需相關資訊，請參閱 [Slack 文件](https://api.slack.com/incoming-webhooks)。
2. 在 Real-Time Insights 中，移至**分析 > 動作**，然後建立具有下列參數的新動作：
 - 類型 - **Webhook**
 - 名稱 - `Post service request on Slack`
 - URL - `Your Slack webhooks URL`
 - 方法 - **POST**
 - 內容類型 - application/json
 - 選取**使用自訂的訊息內文**
 - 內文
 ```{"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iotrtinsights_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}```  
 {: codeblock}  
 **重要事項：**Slack Webhook 必須至少包含 "text" 欄位。如需相關資訊，請參閱 Slack 文件中的[送入 Webhook](https://api.slack.com/incoming-webhooks "Slack 文件")。
11. 按一下**確定**，以儲存動作。

## 使用 Node-RED 傳送文字訊息 {: #noderedex}

在此範例中，動作配置成搭配使用 Node-RED 與 Twilio 節點，以將文字訊息傳送給服務工程師。

若要建立傳送文字訊息動作，請執行下列動作：
1. 在 Twilio 中，找到或建立新的「傳訊服務」，以用來從 Twilio 帳戶傳送文字訊息。如需相關資訊，請參閱 [Twilio 文件](https://www.twilio.com/help)。
1. 在 Bluemix 中，使用 Node-RED URL `http://mynodered.mybluemix.net/red/` 來設定及存取 Node-RED 帳戶。如需相關資訊，請參閱 Bluemix 文件中的[使用 Node-RED 入門範本建立應用程式](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html)主題。
2. 在 Node-RED 中，建立一個簡單的兩節點流程（例如 [RTI-alert]->[SMS]）。
其中，第一個節點是 http 節點，而第二個是 twilio 節點。
 1. 新增 "http" 輸入節點，並且使用下列屬性進行配置：
  <ul>
  <li>方法 - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>名稱 - RTI Action</li>
  </ul>
  2. 新增 "http response" 輸出節點，並將它與 "http" 輸入節點連接在一起，方法是將其中一個節點的輸出埠拖曳到另一個節點的輸入埠。
  3. 新增 "twilio" 輸出節點，並且使用下列屬性進行配置：
  <ul>
  <li>服務 - **外部服務**</li>
  <li>Twilio - 新增 twilio-api</li>
  <li>SMS 至 - `Phone number for the service engineer`</li>
  <li>名稱 - **SMS**</li>
  </ul>
  4. 將節點連接在一起
  將 http 與 twilio 節點連接在一起，方法是將其中一個節點的輸出埠拖曳到另一個節點的輸入埠。
  5. 按一下**部署**按鈕，以將流程部署至伺服器
3. 在 {{site.data.keyword.iotrtinsights_short}} 中，移至**分析 > 動作**，然後建立具有下列參數的動作：
 - 類型 - **Node-RED**
 - 名稱 - `Send text using Node-RED and Twilio`
 - 說明 - `Send a text message alert to the service engineer.`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - 內文
 ```{"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iotrtinsights_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}```  
 {: codeblock}
4. 按一下**確定**，以儲存動作。

## 使用 IFTTT 來張貼 Trello 卡片 {: #iftttex}

在此範例中，我們配置動作以在 Trello 上使用 IFTTT 將卡片張貼至服務要求清單。

若要建立在 Trello 上張貼卡片動作，請執行下列動作：
1.	在 IFTTT 中，連接至 Trello 通道。
2.	在 IFTTT 中，連接至 Maker 通道。請記下 IFTTT 金鑰。您需要有此項目，才能從 Real-Time Insights 連接至 IFTTT。
5.	在 IFTTT 中，建立秘訣：
 1. 按一下 **THIS**。
 2. 選取 **Maker** 通道。  
 2. 按一下**接收 Web 要求**。
 3. 輸入事件名稱 `post-Trello-card`。
 4. 按一下 **THAT**。
 5. 選取 **Trello** 通道。
 6. 選取在其中建立卡片的 Trello 主機板。
 7. 輸入在其中新增卡片的清單名稱。
 8. 編輯標題及說明。
 9. 指派 @service.engineer 及 @service.manager 成員。
 8. 按一下**建立動作**。   
3. 在 {{site.data.keyword.iotrtinsights_short}} 中，移至**分析 > 動作**，然後建立具有下列參數的動作：
<ul>
<li>類型 - **IFTTT**</li>
<li>名稱 - `Post service request card`</li>
<li>說明 - `Use IFTTT to post a card in the service requests list in Trello.`</li>
<li>金鑰 - 您的 IFTTT 金鑰</li>
<li>事件 - `post-Trello-card`</li>
<li>選擇性地新增「值 1」到「值 3」的值。**提示：**您可以使用[變數替代](actions.html#variable_substitution)來動態包括裝置資料。</li>
</ul>
4. 按一下**確定**，以儲存動作。
