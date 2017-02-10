---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 啟用行動裝置的通知
{: #c_enable_push-notifications}
前次更新：2017 年 1 月 18 日
{: .last-updated}

請確定您已通過[配置通知提供者的認證](t__main_push_config_provider.html)。

本節說明如何啟用用戶端應用程式（行動裝置、Web 瀏覽器應用程式以及 Chrome Apps and Extensions）來接收推送通知、如何建立基本通知、取得及起始設定 SDK 或外掛程式，以及如何登錄裝置或瀏覽器來接收推送通知。您也可以使用 [REST API](t_restapi.html)，讓行動及 Web 瀏覽器應用程式接收推送通知。

**附註**：對於裝置、瀏覽器及 Chrome Apps and Extensions 登錄，{{site.data.keyword.mobilepushshort}} Service 會對從通知提供者（APNs for Apple 或 FCM for Google）發出的記號保持唯一參照。
{{site.data.keyword.mobilepushshort}} Service 通知提供者可基於數個原因，而讓這些記號失效。 

例如，解除安裝裝置上的應用程式期間。在這種情境中，當嘗試根據裝置失效的提供者回應遞送通知時，{{site.data.keyword.mobilepushshort}} Service 將移除裝置或 Web 瀏覽器登錄。接著，這將限制隨後不得將通知傳送至失效裝置。
