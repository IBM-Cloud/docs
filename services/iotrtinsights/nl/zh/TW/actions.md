---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# 動作類型 {: #actions}

除了在警示儀表板中顯示警示之外，{{site.data.keyword.iotrtinsights_short}} 還支援數種類型的規則觸發動作，例如傳送電子郵件及傳送 Webhook。
{: shortdesc}

## 建立動作 {: #shared}
您可以[直接從規則編輯器建立動作](rules.html "建立規則")，或在「動作」畫面中建立動作，然後在建立規則時選取動作。

若要從「動作」畫面中建立動作，請執行下列動作：
1. 在 {{site.data.keyword.iotrtinsights_short}} 主控台中，移至**分析 > 動作**。
2. 按一下**新增動作**、選取動作類型、提供動作的名稱，以及提供說明。
3. 提供所建立動作類型的必要參數。
動作類型：  
 - [傳送電子郵件](#email "傳送電子郵件")
 - [Webhook](#webhook "Webhook")
 - [Node-RED](#nodered "Node-RED")
 - [IFTTT](#ifttt "IFTTT")
4. 按一下**確定**，以建立新動作。

動作現在會出現在[規則編輯器](rules.html#rules "規則編輯器")中。



## 傳送電子郵件 {: #email}
使用傳送電子郵件動作，在觸發規則時，將電子郵件傳送給一位以上的收件者。

範例：[傳送電子郵件](action_examples.html#emailex)。

下列參數用來配置傳送電子郵件動作：

參數 | 說明
---|---
名稱 | 動作的名稱（用於「警示」儀表板中）。
說明 | 動作的簡要說明。
收件者 | 一個以上的電子郵件位址（以逗點區隔）。
副本 | 一個以上的電子郵件位址（以逗點區隔）。
主旨 | 電子郵件的主旨行。您可以選擇性地讓主旨自動以 "IoT Real-Time Insight alert" 為開頭。

電子郵件內文是在觸發規則時，自動從裝置訊息建立。  
**重要事項：**如果裝置資料包含機密性資訊，則可以選擇不要在電子郵件訊息中包括裝置資料，以及僅在警示畫面中顯示機密性資料。


## Webhook {: #webhook}
使用 Webhook 動作，以在觸發警示時，對啟用 Webhook 功能的 Web 服務提出 HTTP 要求。例如，如果裝置中的感應器報告異常讀數，則可以使用 Webhook 來開啟資產的服務要求。

範例：[使用 Webhook 在 Slack 上進行張貼](action_examples.html#webhookex)。

下列參數用來配置 Webhook 動作：

參數 | 說明
---|---
名稱 | 動作的名稱（用於「警示」儀表板中）。
說明 | 動作的簡要說明。
URL | 目標啟用 Webhook 功能伺服器的 URL。**提示：**您可以使用[變數替代](#variable_substitution)，以在 URL 中動態包括其他資料。
方法 | 要執行的 Webhook 呼叫類型。請選取下列其中一種類型：GET、HEAD、OPTIONS、PATCH、PUT、POST 或 DELETE。
使用者名稱 | 在 Web 服務需要時包括。
密碼 | 在 Web 服務需要時包括。**重要事項：**密碼是以明碼形式傳送。
標頭 | 標頭是由索引鍵及值配對所構成。**提示：**您可以使用[變數替代](#variable_substitution)，以在標頭中動態包括其他資料。
內容類型 | 內文的內容類型：JSON、XML、WWW 形式 URL 編碼或純文字。可用於 OPTIONS、PATCH、PUT、POST 及 DELETE 方法。
內文 | Webhook 呼叫的內文。可用於 OPTIONS、PATCH、PUT、POST 及 DELETE 方法。依預設，內文欄位會預先填入[變數替代](#variable_substitution)中所列的所有變數。選取**使用自訂的訊息內文**，以編輯內文欄位的內容。**重要事項：**Webhook 伺服器可能需要在內文中包括某些特定欄位。例如，Slack Webhook 必須包含 "text" 欄位。   



## Node-RED {: #nodered}
使用 Node-RED 動作，以在觸發規則時連接至 Node-RED 應用程式。如需使用 Node-RED 的相關資訊，請參閱[使用 Internet of Things 入門範本應用程式建立應用程式](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500)。

範例：[使用 Node-RED 傳送文字訊息](action_examples.html#noderedex)。

下列參數用來配置 Node-RED 動作：

參數 | 說明
---|---
名稱 | 動作的名稱（用於「警示」儀表板中）。
說明 | 動作的簡要說明。
URL | 目標 Node-RED HTTP 輸入節點的 URL。
使用者名稱 | 在 Node-RED 服務需要時包括。
密碼 | 在 Node-RED 服務需要時包括。**重要事項：**密碼是以明碼形式傳送。
內文 | 依預設，內文欄位會預先填入[變數替代](#variable_substitution)中所列的所有變數。選取**使用自訂的訊息內文**，以編輯內文欄位的內容。

## IFTTT {: #ifttt}
使用 IFTTT 動作，以在觸發規則時觸發 IFTTT 秘訣。如需觸發 Real-Time Insights 動作作為 IFTTT 秘訣的相關資訊，請參閱 IFTTT 網站上的 [Maker 通道](https://ifttt.com/maker)。

範例：[使用 IFTTT 來張貼 Trello 卡片](action_examples.html#iftttex)。

下列參數用來配置 IFTTT 動作：

參數 | 說明
---|---
名稱 | 動作的名稱（用於「警示」儀表板中）。
說明 | 動作的簡要說明。
金鑰 | 用來觸發事件的「Maker 通道」金鑰。
事件 | 配置為「Maker 事件」之觸發程式的事件名稱。您可以建立具有不同觸發程式的多個秘訣，每一個都有不同的事件名稱。
值 1-3 | 您可以在這些參數中傳遞任何內容，而這些參數會傳遞至 IFTTT 秘訣中的動作。**提示：**您可以使用[變數替代](#variable_substitution)，以在標頭中動態包括其他資料。

## 變數替代 {: #variable_substitution}
包括下列變數替代來動態包括裝置資料。變數必須用雙大括弧括住。

變數 | 說明
---|---
**URL、標頭及內文** |
`{{timestamp}}` | 訊息中的時間戳記
`{{tenantId}}` | Real-Time Insights 服務的 ID
`{{deviceId}}` | 裝置的 ID
`{{ruleName}}` | 包含動作的規則名稱
**僅內文** |
`{{ruleDescription}}`| 包含動作的規則說明
`{{ruleCondition}}` | 觸發動作的規則條件
`{{message}}` | 包含已觸發規則之資料點值的原始裝置訊息
