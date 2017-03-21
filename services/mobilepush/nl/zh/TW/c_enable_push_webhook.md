---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 啟用 Webhook 
{: #tag_based_notifications}
前次更新：2017 年 1 月 23 日
{: .last-updated}


使用 {{site.data.keyword.mobilepushshort}} 服務，您可以選擇接收關於已變更資訊的警示。企業資訊的變更會建立事件，您可以將事件登錄為 Webhook 事件，以收到其通知。這些 Webhook 事件會觸發警示。 

Webhook 是使用者定義的回呼，它們是由例如登錄裝置或訂閱標籤等事件所觸發。在 {{site.data.keyword.mobilepushshort}} 服務上，您可以登錄下列 Webhook 事件： 

- **onDeviceRegister**：裝置登錄推送時會觸發 Webhook 事件。
- **onDeviceUpdate**：已登錄裝置的相關資訊更新時會觸發 Webhook 事件。
- **onDeviceUnregister**：取消登錄裝置時會觸發 Webhook 事件。 
- **onSubscribe**：使用者訂閱標籤時會觸發 Webhook 事件。
- **onUnsubscribe**：使用者取消訂閱標籤時會觸發 Webhook 事件。
- **onNotificationSend**分派通知時會觸發 Webhook 事件。
- **onNotificationFailure**通知失敗時會觸發 Webhook 事件。


**附註：**通知分派會以批次處理。訊息分派可以有多個 Webhook 事件，事件可能同時包含失敗和成功。Webhook 事件的 messageID 會與分派訊息的相同。 

如需 Webhook 的相關資訊，請參閱 [IBM Push Notifications REST API ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://mobile.{DomainName}/imfpush/#/webhooks){: new_window}。
