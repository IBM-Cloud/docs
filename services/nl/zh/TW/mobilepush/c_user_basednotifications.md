---

標題：啟用使用者型 Push Notifications

關鍵字：使用者型 Push Notifications，userId
copyright:
 years: 2015, 2016

---

# 啟用使用者型通知
{: #user_based_notifications}
前次更新：2016 年 8 月 16 日
{: .last-updated}

使用者 ID 型 {{site.data.keyword.mobilepushshort}} 是以具有自訂訊息的行動應用程式使用者為目標。使用者型通知可以利用其個人喜好設定及選擇，來協助吸引特定個人。  

## 向使用者 ID 登錄裝置
若要啟用以「使用者 ID」為目標的推送通知，請確定您向「使用者 ID」登錄裝置，同時也傳遞佈建 {{site.data.keyword.mobilepushshort}} Service 時所配置的 'clientSecret'。若沒有有效的 'clientSecret'，裝置登錄會失敗。  

「使用者 ID」可以是應用程式提供給裝置登錄 API 的任何字串。一般而言，行動應用程式會先執行鑑別週期，在此鑑別週期，會對鑑別服務（例如 [{{site.data.keyword.amafull}}](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html)）鑑別行動應用程式使用者。鑑別成功時，已鑑別使用者 ID 接著會與 'clientSecret' 一起傳遞至「推送裝置登錄 API」。'clientSecret' 的存在只會強制執行「使用者 ID」與行動裝置登錄的已授權關聯。

保留 'clientSecret' 機密，而且絕不寫在行動應用程式中。您可以利用各種應用程式起始設定型樣，在應用程式運行環境期間動態地取回 'clientSecret'。序列圖會概述此型樣。

![Enable_Push](images/init_client_secret.jpg) 

您也可以登錄要與 'anonymous' 使用者相關聯的裝置。這需要您使用不需要使用者 ID 及 'clientSecret' 引數的裝置登錄 API 變式。   

## 同步化使用者登入/登出並啟用推送通知 

只有在使用者已登入時，您才能選擇傳送通知。 

例如，如果家人或工作團隊共用裝置，而且您需要定址家人或團隊中的特定使用者。在這類使用案例中，將會有可保護應用程式以追蹤現行應用程式使用者身分的使用者登入及登出序列。若要確保一律只有該使用者才會接收到以特定使用者為目標的通知，請在成功登入之後，呼叫傳遞已登入使用者之「使用者 ID」的裝置登錄 API。同樣地，登出之前，請呼叫裝置取消登錄 API。排序這些具有登入及登出的 Push API，可確保只將要送往特定使用者的推送通知傳送至該使用者。
