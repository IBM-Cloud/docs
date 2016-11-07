---

copyright:
  years: 2016
lastupdated: "2016-10-13"

---
{:new_window: target="_blank"}

# 指導教學 - Watson Language 程式碼入門範本
{: #tutorial_watson_language}

前次更新：2016 年 10 月 13 日
{: .last-updated}

「{{site.data.keyword.Bluemix}} Mobile for Watson Language 程式碼入門範本」展示 Watson 的 Text To Speech 及 Language Translation 服務，並提供每一個 {{site.data.keyword.Bluemix_notm}} Mobile 服務的整合點。


## 需求
{: #tutorial_requirements}

* [Bluemix](http://bluemix.net) 帳戶
* 取自 [Bluemix Catalog](https://console.{DomainName}/catalog/) 的 [Language Translator](https://console.{DomainName}/catalog/services/language-translator/) 及 [Text to Speech](https://console.{DomainName}/catalog/services/text-to-speech/) 服務實例


## 開始使用
{: #tutorial_gs}

若要快速開始進行「Watson Language 程式碼入門範本」，請遵循下列步驟：

1. 在 {{site.data.keyword.Bluemix_notm}} 中建立 Mobile 儀表板專案。

   1. 從 Mobile 儀表板的**開始使用**頁面中，按一下**建立專案**。

      您也可以按一下**專案**頁面中的**建立專案**。

   2. 按一下**程式碼入門範本**。

   3. 選取 **Watson Language**，然後按一下**建立專案**。

   4. 輸入專案名稱，然後按一下**建立**。

2. 選用項目：新增 Push Notifications。

   1. 在**專案概觀**頁面中，針對 **Push Notifications** 按一下**新增**。

      您也可以按一下 **Push Notifications** 頁面中的**建立**。

   2. 輸入服務名稱，然後按一下**建立**。

   3. 若為 iOS，[配置 Apple Push Notification Service](../services/mobilepush/t_push_provider_ios.html){: new_window}。

   4. 若為 Android，[配置 Google Cloud Messaging](../services/mobilepush/t_push_provider_android.html){: new_window}。

3. 選用項目：新增其他服務。

   1. 在**專案概觀**頁面上，針對服務按一下**新增**。

   2. 輸入服務名稱，然後按一下**建立**。

   3. 遵循服務的指示來進行設定。

4. 下載專案。

   1. 按一下**程式碼**，然後選取偏好的語言。

   2. 按一下**下載程式碼**。

5. 解壓縮保存檔，並且使用 Markdown 檢視器檢視 `README.md` 檔案，以完成設定。


## 下一步
{: #tutorial_next}

[試用看看吧！](http://new-console.{DomainName}/mobile/create-project?starter=512568a1-72db-35c7-b9c4-4f3e3bc89375){: new_window}


# 相關鏈結
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Beta)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## 部落格文章
{: #general}
* [部落格文章：Introducing the Bluemix Mobile dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [部落格文章：Introducing the next generation of the Bluemix Mobile dashboard](https://ibm.event.ibm.com/blogs/bluemix/2016/10/introducing-the-next-generation-of-the-bluemix-mobile-dashboard/){: new_window}
* [部落格文章：Introducing Bluemix Mobile Code Starters](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [部落格文章：Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [部落格文章：Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## 指導教學與範例
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
