---

copyright:
 years: 2015, 2016

---

# 啟用通知
{: #c_enable_push-notifications}
*前次更新：2016 年 6 月 14 日*
{: .last-updated}

您可讓應用程式接收推送通知，並將其傳送至您的裝置。

本節說明如何讓行動應用程式可接收推送通知、如何建立基本通知、取得及起始設定 SDK 或外掛程式，以及如何登錄裝置來接收推送通知。您也可以使用 [REST API](t_restapi.html)，讓行動應用程式可以接收推送通知。

附註：若為具有推送的裝置登錄，Push Notification Service 會對從通知提供者（APNS for Apple 或 GCM for Google）發出的記號保持唯一參照。Push Notification Service 推送提供者可基於數個原因，讓這些記號失效。 

例如，在解除安裝裝置上的應用程式期間。在這類實務範例中，當嘗試根據裝置失效的提供者回應遞送通知時，Push Notification Service 將移除裝置登錄。接著，這將限制隨後不得將通知傳送至失效裝置。
