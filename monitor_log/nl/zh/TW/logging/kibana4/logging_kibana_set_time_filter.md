---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 設定時間過濾器
{: #set_time_filter}

配置*時間選取器*，以檢視及過濾某個時段內的 {{site.data.keyword.Bluemix}} 日誌。
{:shortdesc}

您可以在「探索」頁面中配置*時間選取器*。依預設，其設定為前 15 分鐘。 

請完成下列步驟，以搜尋包括特定時間的項目：

1. 在「探索」頁面功能表列中，按一下「時間選取器」![時間選取器](images/k4_time_picker_icon.jpg "時間選取器")。

2. 設定時間間隔。 

    您可以定義下列任何類型的時間間隔：
    
    * 快速：這些是預先定義的時間間隔，包括最常使用的「相對」及「絕對」時間間隔，例如，*今天* 及*這個月*。 
    
        ![時間選取器快速選項](images/k4_time_picker_quick.jpg "時間選取器快速選項")
    
    * 相對：在這些時間間隔中，您可以指定開始日期和時間，以及結束日期和時間。您可以取小時的整數。
    
        ![時間選取器相對選項](images/k4_time_picker_relative.jpg "時間選取器相對選項")
    
    * 絕對：這些是介於開始日期與結束日期之間的時間間隔。
    
        ![時間選取器絕對選項](images/k4_time_picker_absolute.jpg "時間選取器絕對選項")
      

配置時間間隔之後，Kibana 中顯示的資料會對應於該時間範圍內的項目。



