---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 記載 IBM Bluemix Container Service
{: #logging_containers_ov}

在 {{site.data.keyword.Bluemix}} 中，您可以透過 {{site.data.keyword.Bluemix_notm}} 儀表板、Kibana 和指令行介面來檢視、過濾及分析容器日誌。{:shortdesc}

您可以使用搜索器，從容器外部監視及轉遞容器日誌。搜索器會將資料傳送至 {{site.data.keyword.Bluemix_notm}} 中的多方承租戶 Elasticsearch。

下圖顯示 {{site.data.keyword.containershort}} 記載的高階視圖：

![容器的高階元件概觀](images/logging_containers_ov.jpg "容器的高階元件概觀")

當您在 {{site.data.keyword.Bluemix_notm}} 中部署該容器時，會自動啟用容器的記載功能。

## 為容器收集的日誌
{: #logging_containers_ov_logs_collected}

依預設，會收集下列日誌：

<table>
  <tbody>
    <tr>
      <th align="center">日誌</th>
      <th align="center">說明</th>
    </tr>
    <tr>
      <td align="left" width="30%">/var/log/messages</td>
      <td align="left" width="70%"> 依預設，Docker 訊息儲存在容器的 /var/log/messages 資料夾中。此日誌包括系統訊息。
      </td>
    </tr>
    <tr>
      <td align="left">./docker.log</td>
      <td align="left">此日誌是 Docker 日誌。<br> Docker 日誌檔未儲存為容器內部的檔案，但仍然會予以收集。預設會收集此日誌檔，因為它是標準 Docker 使用慣例，用來公開容器的 stdout（標準輸出）及 stderr（標準錯誤）資訊。如果有任何容器處理程序列印至 stdout 或 stderr，即會收集該資訊。</td>
     </tr>
  </tbody>
</table>

若要收集其他日誌，請在建立容器時，新增 **LOG_LOCATIONS** 環境變數，並包含日誌檔的路徑。您可以新增多個日誌檔，以逗點將其隔開。如需相關資訊，請參閱[收集容器中的非預設日誌資料](logging_containers_other_logs.html#logging_containers_collect_data)。


## 分析容器日誌的方法
{: #logging_containers_ov_methods}
 
您可以選擇下列任何方法來分析容器的日誌：

* 在 {{site.data.keyword.Bluemix_notm}} 中分析日誌，以檢視容器的最新活動。
    
    您可以透過每一個容器都有的**監視及日誌**標籤來檢視、過濾及分析日誌。如需相關資訊，請參閱[從 Bluemix 儀表板分析日誌](../logging_view_dashboard.html#analyzing_logs_bmx_ui)。
    
* 在 Kibana 中分析日誌，以執行進階分析作業。
    
    您可以使用 Kibana（一種開放程式碼分析與視覺化平台），以各種圖形（例如圖表和表格）來監視、搜尋、分析及視覺化您的資料。如需相關資訊，請參閱[在 Kibana 中分析日誌](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana)。

* 透過 CLI 來分析日誌，以程式設計方式使用指令來管理日誌。
    
    您可以透過指令行介面，使用 **cf ic logs** 指令來檢視、過濾及分析日誌。如需相關資訊，請參閱[從指令行介面分析日誌](../logging_view_cli.html#analyzing_logs_cli)。


## 日誌保留
{: #logging_containers_ov_log_retention}

請考量下列關於日誌保留的資訊：

* 每個空間每天最多可儲存 1 GB 資料。超過 1 GB 上限的任何日誌都會被捨棄。上限配額會在每天凌晨 12:30（世界標準時間）重設。 

    您可以聯絡支援中心來增加上限。請在支援問題單中，附上增加上限要求的空間 ID、新的大小上限，以及要求的理由。

* 最多 7 天可搜尋最多 7 GB 的資料。達到 7 GB 資料或在 7 天之後，日誌資料就會輪替（先進先出）。

