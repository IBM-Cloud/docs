---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 啟用使用者型通知
{: #user_based_notifications}
前次更新：2017 年 1 月 16 日
{: .last-updated}

使用者 ID 型 {{site.data.keyword.mobilepushshort}} 是以具有自訂訊息的行動應用程式使用者為目標。運用使用者型通知，您可以選擇根據其喜好設定來通知特定個體。

## 向使用者 ID 登錄裝置
若要啟用「使用者 ID」設為目標的推送通知，請確定您已設定「使用者 ID」欄位來登錄裝置。     

「使用者 ID」可以是應用程式提供給裝置登錄 API 的任何字串。一般而言，行動應用程式會先執行鑑別週期，在此鑑別週期，會對鑑別服務（例如 [{{site.data.keyword.amafull}} ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html "外部鏈結圖示"){: new_window}）鑑別行動應用程式使用者。鑑別成功時，接著會將已鑑別使用者 ID 傳遞至「推送裝置登錄 API」。 

## 同步化使用者登入及登出 

只有在使用者已登入時，您才能選擇傳送通知。 

例如，請考慮使用家族成員或工作團隊成員共用的裝置，而且需要定址特定使用者。在這類使用案例中，將會有使用者登入及登出序列。此鑑別機制容許應用程式追蹤現行應用程式使用者的身分。這確保一律只有該使用者才會接收到以特定使用者為目標的通知。在成功登入之後，請呼叫傳遞已登入使用者之「使用者 ID」的裝置登錄 API。同樣地，登出之前，請呼叫裝置取消登錄 API。排序這些具有登入及登出的 Push API，可確保只將要送往特定使用者的通知傳送給該使用者。
