---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 監視 Push Notifications 
{: #monitor-notifications}
前次更新：2017 年 4 月 12 日
{: .last-updated}


IBM {{site.data.keyword.mobilepushshort}} 服務現在已擴充功能，可藉由從您的使用者資料產生圖形，來監視推送效能。您可以使用此公用程式來列出所有已傳送的推送通知，或是列出所有已登錄裝置，並以每日、每週或每月為基礎分析資訊。

若要產生所有已傳送通知的報告，請使用 [REST API](https://mobile.{DomainName}/imfpush/){: new_window} 中的 Push Messages GET report 方法。 

![已傳送通知報告](images/monitoring_messages.jpg)


若要產生所有已登錄裝置的報告，請使用 [REST API](https://mobile.{DomainName}/imfpush/){: new_window} 中的 Push Device Registrations GET report 方法。

![已登錄裝置報告](images/monitoring_devices.jpg)

如需如何更新 Android SDK 以監視通知資訊的相關資訊，請參閱[啟用行動裝置的通知](c_enable_push.html)中的「在 Android 裝置上監視推送通知」主題。


 
