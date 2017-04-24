---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-07"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 常見問題與解答
{: #logging_qa}

以下是關於使用 {{site.data.keyword.Bluemix}} 記載功能的常見問題與解答。{:shortdesc}

* [如果在 Kibana 的「探索」頁面中看不到資料，我該怎麼辦](logging_qa.html#logging_qa_no_data_discover_kibana)

* [如果發生鑑別異常狀況，我該怎麼辦](logging_qa.html#logging_qa_no_data_dashboard_kibana)





## 如果在 Kibana 的「探索」頁面中看不到資料，我該怎麼辦
{: #logging_qa_no_data_discover_kibana}

您在 Kibana 中看不到資料，可能會有以下幾種不同情境：

1. 啟動 Kibana 時，您在「探索」頁面中可能未看到任何資料，並且收到下列訊息：**找不到任何結果**。 
2. 您可能正在 Kibana 的「探索」頁面中工作。不過，一段時間之後，當您嘗試在 Kibana 中執行作業時，收到下列訊息：**找不到任何結果**。

若要解決這個問題，請完成下列步驟：

1. 檢查「探索」頁面中設定的*時間選取器*，並增長時段。 

    **附註**：依預設，在 {{site.data.keyword.Bluemix_notm}} 中，*時間選取器* 設定為顯示前 15 分鐘的資料。

    如需如何設定*時間選取器* 的相關資訊，請參閱[設定時間過濾器](../kibana4/logging_kibana_set_time_filter.html#set_time_filter)。
       
2. 按一下位於*探索* 頁面搜尋列中的放大鏡。頁面資料會根據預設搜尋查詢來重新整理。

    或者，您也可以設定*自動重新整理* 週期。

    **附註**：依預設，在 {{site.data.keyword.Bluemix_notm}} 中，*自動重新整理* 週期設定為**關閉**。
    
    如需如何啟用此功能的相關資訊，請參閱[自動重新整理資料](../kibana4/logging_kibana_analize_logs_interactively.html#kibana_discover_view_refresh_interval)。



## 如果發生鑑別異常狀況，我該怎麼辦
{: #logging_qa_no_data_dashboard_kibana}

如果您在「儀表板」頁面中，看不到以視覺化顯示的資料，並收到錯誤訊息：**錯誤：授權異常狀況。**，請檢查您查看各視覺化資料的許可權。

請考量下列資訊：您可以在「儀表板」頁面中配置一個以上的視覺化。當「儀表板」頁面要求收集透過那些視覺化顯示的資料時，針對所有視覺化，僅發出一個要求。如果您沒有查看其中一項視覺化資料的許可權，整個要求都會失敗。

若要解決這個問題，請完成下列步驟：

1. 識別您沒有許可權的視覺化。

    1. 在*儀表板* 頁面中按一下視覺化的*鉛筆* 圖示。該視覺化會在*視覺化* 中開啟。或者，您也可以在*視覺化* 頁面中，載入一個視覺化。 
    2. 驗證您可以看到資料。
    
    重複這些步驟來處理每一個視覺化。

2. 向您的雲端管理者要求查看那些視覺化中之資料的存取權。

3. 建立新的「儀表板」頁面，排除您沒有許可權的視覺化，但您有權查看造成問題之視覺化中的資料。 

    如果您共用該「儀表板」，請勿刪除視覺化，因為那樣會影響其他使用相同儀表板的團隊成員。


