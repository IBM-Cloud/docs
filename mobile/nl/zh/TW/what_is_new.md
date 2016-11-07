---

copyright:
  years: 2016
lastupdated: "2016-10-18"

---
{:new_window: target="_blank"}

# Mobile 儀表板的新增功能
{: #what_is_new}

前次更新：2016 年 10 月 18 日
{: .last-updated}

{{site.data.keyword.Bluemix}} Mobile 儀表板的十月更新引進了下列變更：

   * 您現在可以直接從儀表板中將 Push Notifications 及 Analytics 功能新增至專案。
   * 現在已提供[程式碼入門範本](starters.html#Code_Starter)。
   * 現在支援 Swift。


### Analytics
{: #analytics}

   * 當您新增 Analytics 功能時，預設會啟用展示模式。在您執行應用程式之後，即可關閉展示模式來檢視分析。


### 使用者介面建置器
{: #ui_builder}

   * 現在可以從專案存取 **Push Notifications** 功能。
   * **專案設定**標籤已重新命名為**設定**標籤。
   * **鑑別**標籤已重新命名為**使用者存取**標籤。


### 程式碼
{: #code}

   * 針對 iOS 產生的 Objective-C 及 Swift 程式碼現在使用 CocoaPods 來管理相依關係。這表示您需要安裝 CocoaPods。若要安裝它，請執行 `sudo gem install cocoapods`。安裝 CocoaPods 之後，請執行 `pod setup` 來進行配置（如果尚未配置）。最後，執行 `pod install` 來下載及安裝必要的專案相依關係，之後再於 Xcode 中開啟 `.xcworkspace` 檔案。在所下載程式碼保存檔的 `README.md` 檔案中提供其他詳細資料。如需相關資訊，請閱讀[必備開發人員工具](get_code.html#prereq-dev-tools)。

請經常檢查，以保有最新的更新項目。


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
* [部落格文章：Introducing the next generation of the Bluemix Mobile dashboard](https://ibm.com/blogs/bluemix/2016/10/introducing-the-next-generation-of-the-bluemix-mobile-dashboard/){: new_window}
* [部落格文章：Introducing Bluemix Mobile Code Starters](https://www.ibm.com/blogs/bluemix/2016/10/rapid-dev-with-mobile-code-starters/){: new_window}
* [部落格文章：Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [部落格文章：Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}

## 指導教學與範例
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}
