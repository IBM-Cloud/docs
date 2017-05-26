---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-06"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 在 Kibana 中依時間過濾 Cloud Foundry 應用程式日誌
{: #logging_kibana_time_filter}


在 Kibana 儀表板上，依時間檢視及過濾 {{site.data.keyword.Bluemix_notm}} 應用程式日誌。您可以從 Cloud Foundry 應用程式的**日誌**標籤存取 Kibana 儀表板。
{:shortdesc}

完成下列作業，以在 Kibana 儀表板上，依時間檢視及過濾 Cloud Foundry 應用程式日誌：

1. 存取 Cloud Foundry 應用程式的**日誌**標籤。 

    1. 在 {{site.data.keyword.Bluemix_notm}} **應用程式**儀表板上按一下應用程式名稱。
    2. 按一下**日誌**標籤。 
    
    即會顯示應用程式的日誌。

2. 存取應用程式的 Kibana 儀表板。按一下**進階視圖** ![「進階視圖」鏈結](images/logging_advanced_view.jpg "「進階視圖」鏈結")。即會顯示 Kibana 儀表板。


3. 在 Kibana 儀表板上，按一下**時間過濾器** ![Kibana 時間過濾器](images/logging_kibana_time_filter.jpg "Kibana 時間過濾器")，然後從下拉功能表中選取**自訂**。即會顯示下列視窗：

    ![Kibana 儀表板上的自訂時間過濾器](images/logging_custom_time_filter.jpg "Kibana 儀表板上的自訂時間過濾器")

4. 按一下**開始時間**和**結束時間**欄位，以編輯過濾器的開始和結束時間。 
    
    若要包含到目前時間為止的日誌，請按一下**現在**鏈結。確定時間範圍後，按一下**套用**。 

Kibana 儀表板現在會針對您自訂的時間過濾器來顯示所記載的事件。
