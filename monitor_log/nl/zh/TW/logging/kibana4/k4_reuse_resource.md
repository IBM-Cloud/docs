---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 重複使用 Kibana 資源以分析 Bluemix 日誌
{:#k4_reuse_resource}

若要將搜尋、視覺化或儀表板從某個 {{site.data.keyword.Bluemix}} 空間複製到不同的空間，請使用 Kibana 中提供的匯出及匯入功能。您可以個別地複製資源，或匯出 Kibana 中的所有資源。
{:shortdesc}

| 作業 | 說明 |
|------|-------------|
| [複製搜尋](k4_reuse_resource.html#k4_reuse_search) | 在空間之間複製搜尋。 |
| [複製視覺化](k4_reuse_resource.html#k4_reuse_visualization) | 在空間之間複製視覺化 |

請在 {{site.data.keyword.Bluemix_notm}} 中考量下列重複使用搜尋、視覺化或儀表板的情境： 

* 複製相同組織中空間之間的資源。

    例如，您可能要將視覺化從 {{site.data.keyword.Bluemix_notm}} 中的開發空間複製到編譯打包空間。
    
* 複製相同帳戶中不同組織內空間之間的資源。

    例如，您可能要將視覺化從 {{site.data.keyword.Bluemix_notm}} 中開發組織內的空間複製到編譯打包組織中的空間。

* 在位於相同組織但位在不同公用地區的空間之間複製資源。

    例如，您可能要將視覺化從 {{site.data.keyword.Bluemix_notm}} 中位在「美國南部」公用地區的組織 A 中的空間，複製到位在「英國」公用地區的組織 A 中的空間。



## 副本搜尋
{:#k4_reuse_search}

請完成下列步驟，以在 {{site.data.keyword.Bluemix_notm}} 中的空間之間複製搜尋：

1. 啟動您要複製的搜尋所在的 Kibana。 

    * 從 {{site.data.keyword.Bluemix_notm}} 使用者介面啟動 Kibana：您可匯出的 JSON 搜尋檔案包括下列欄位：*空間 ID*，以及 Cloud Foundry (CF) 應用程式的*應用程式 ID* 或容器的*實例 ID*。如需相關資訊，請參閱[從 {{site.data.keyword.Bluemix_notm}} 儀表板進入 Kibana 儀表板](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix)。
    
    * 從瀏覽器啟動 Kibana：您可匯出的 JSON 搜尋檔案包括*空間 ID* 欄位。如需相關資訊，請參閱[從瀏覽器進入 Kibana 儀表板](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser)。

2. 在*設定* 頁面中，選取**物件**及**搜尋**標籤。然後選取搜尋，並複製下列資訊：

    <table>
      <tbody>
        <tr>
          <th align="center">搜尋欄位</th>
          <th align="center">說明</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> 套用搜尋以過濾資料的空間 ID。</td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">搜尋的名稱。</td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">搜尋的版本。</td>
        </tr>
      </tbody>
    </table>
   
3. 匯出搜尋。

    1. 在「設定」頁面中，選取**物件**標籤。
    2. 在**搜尋**標籤中，選取您要匯出的搜尋。
    3. 按一下**匯出**。
    4. 儲存 JSON 檔案。

4. 在 {{site.data.keyword.Bluemix_notm}} 使用者介面中，切換到您要複製搜尋的空間，然後檢查 CF 應用程式或容器是否可供使用且正在執行中。
    
5. 針對您要匯入搜尋的 {{site.data.keyword.Bluemix_notm}} 空間啟動 Kibana，然後取得下列資訊：

    從 [Bluemix 使用者介面](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix)：
    
    <table>
      <tbody>
        <tr>
          <th align="center">搜尋欄位</th>
          <th align="center">說明</th>
        </tr>
        <tr>
          <td align="left">空間 ID</td>
          <td align="left"> <ol><li> 在*設定* 頁面中，選取*索引* 標籤。</li> <br> <li>空間 ID 內嵌在索引型樣中。索引型樣的格式如下：`[logstash-3d8d2eae-SpaceID-]YYYY.MM.DD`，其中 *SpaceID* 是空間的 ID。請複製空間 ID。</li></ol></td>
        </tr>
        <tr>
          <td align="left">應用程式 ID 或實例 ID</td>
          <td align="left"><ul><li>當您從 {{site.data.keyword.Bluemix_notm}} 使用者介面啟動 Kibana 時，依預設會開啟*探索* 頁面。從*探索* 頁面的搜尋列中，取得應用程式 ID 或實例 ID（例如，`application_id:d88d1f16-e9d9-4623-bce7-0348c88f5133`）。</li> <br> <li>當您從瀏覽器啟動 Kibana 時，請從「探索」頁面的「欄位清單」中選取 application_id 或 instance_id 欄位。</li></ul></td>
        </tr>
      </tbody>
    </table>

6. 修改在前一個步驟中匯出的搜尋 JSON 搜尋檔案。取代應用程式 ID 值。 

    例如，下列 JSON 是搜尋 JSON 檔案的範例。 
 
    <pre class="pre">
    [
  {
    "_id": "52edf6e6-5386-4235-8fb8-598de3b80f41_Dev",
    "_type": "search",
    "_source": {
      "columns": [
        "application_id",
        "source_id",
        "instance_id"
      ],
      "description": "",
      "group": "52edf6e6-5386-4235-8fb8-598de3b80f41",
      "hits": 0,
      "kibanaSavedObjectMeta": {
        "searchSourceJSON": "{\"index\":\"[logstash-52edf6e6-5386-4235-8fb8-598de3b80f41-]YYYY.MM.DD\",\"query\":{\"query_string\":{\"analyze_wildcard\":true,\"query\":\"application_id:4ae73dcd-1fc4-48f0-9dc7-425839040436\"}},\"highlight\":{\"pre_tags\":[\"@kibana-highlighted-field@\"],\"post_tags\":[\"@/kibana-highlighted-field@\"],\"fields\":{\"*\":{}},\"fragment_size\":2147483647},\"filter\":[{\"meta\":{\"negate\":false,\"index\":\"[logstash-52edf6e6-5386-4235-8fb8-598de3b80f41-]YYYY.MM.DD\",\"key\":\"application_id\",\"value\":\"4ae73dcd-1fc4-48f0-9dc7-425839040436\",\"disabled\":false},\"query\":{\"match\":{\"application_id\":{\"query\":\"4ae73dcd-1fc4-48f0-9dc7-425839040436\",\"type\":\"phrase\"}}}}]}"
      },
      "sort": [
        "@timestamp",
        "desc"
      ],
      "title": "Dev",
      "version": 1
    }
  }
]
    </pre>
    
    在此範例 JSON 檔案中，您可以使用新空間的資訊來修改下列變數： 
    
    * SPACEID：將此變數取代為新空間的空間 ID。
    * NAME：如果您要變更新空間中的搜尋名稱，請取代此變數。若要維護相同的名稱，請不要變更此值。
    * APPID：將此變數取代為新空間中 CF 應用程式的 application_id 值或新空間中容器的實例 ID。
    
   <pre class="pre">
   [
  {
    "_id": "SPACEID_NAME",
    "_type": "search",
    "_source": {
      "columns": [
        "application_id",
        "source_id",
        "instance_id"
      ],
      "description": "",
      "group": "SPACEID",
      "hits": 0,
      "kibanaSavedObjectMeta": {
        "searchSourceJSON": "{\"index\":\"[logstash-SPACEID-]YYYY.MM.DD\",\"query\":{\"query_string\":{\"analyze_wildcard\":true,\"query\":\"application_id:APPID\"}},\"highlight\":{\"pre_tags\":[\"@kibana-highlighted-field@\"],\"post_tags\":[\"@/kibana-highlighted-field@\"],\"fields\":{\"*\":{}},\"fragment_size\":2147483647},\"filter\":[{\"meta\":{\"negate\":false,\"index\":\"[logstash-SPACEID-]YYYY.MM.DD\",\"key\":\"application_id\",\"value\":\"APPID\",\"disabled\":false},\"query\":{\"match\":{\"application_id\":{\"query\":\"APPID\",\"type\":\"phrase\"}}}}]}"
      },
      "sort": [
        "@timestamp",
        "desc"
      ],
      "title": "Dev",
      "version": 1
    }
  }
]
    </pre>

6. 將搜尋 JSON 檔案匯入至新空間的 Kibana。

    1. 在「設定」頁面中，選取**物件**標籤。
    2. 在**搜尋**標籤中，選取您要匯入的搜尋 JSON 檔案。
    3. 按一下**匯入**。

您可以在 Kibana 中使用搜尋，以監視新空間中應用程式可用的資料。


    
## 複製視覺化
{:#k4_reuse_visualization}

請完成下列步驟，以將用來分析空間中應用程式資料的視覺化複製到不同空間：

1. 針對您要複製之視覺化所在的空間啟動 Kibana。 

    * 從 {{site.data.keyword.Bluemix_notm}} 使用者介面啟動 Kibana：您可匯出的 JSON 搜尋檔案包括下列欄位：*空間 ID*，以及 Cloud Foundry (CF) 應用程式的*應用程式 ID* 或容器的*實例 ID*。如需相關資訊，請參閱[從 {{site.data.keyword.Bluemix_notm}} 儀表板進入 Kibana 儀表板](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix)。
    
    * 從瀏覽器啟動 Kibana：您可匯出的 JSON 搜尋檔案包括*空間 ID* 欄位。如需相關資訊，請參閱[從瀏覽器進入 Kibana 儀表板](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser)。
    
2. 複製空間之間與視覺化相關聯的搜尋。如需相關資訊，請參閱[在 Bluemix 空間之間複製搜尋](k4_reuse_resource.html#k4_reuse_search)。

    視覺化使用搜尋來過濾所顯示的資料。視覺化可能鏈結至搜尋，以自動更新您對搜尋進行的所有更新，也可能不鏈結至搜尋，如此則只有在您建立視覺化時顯示的資料可用於分析。

    當您複製視覺化時，不論其對搜尋的鏈結狀態為何，您必須同時複製與其相關聯的搜尋。**附註：**當您將視覺化匯入至新空間時，新的視覺化會鏈結至新空間中的搜尋。
    
3. 在*設定* 頁面中，選取**物件**及**視覺化**標籤。然後，選取視覺化，並取得下列資訊： 

    <table>
      <tbody>
        <tr>
          <th align="center">視覺化欄位</th>
          <th align="center">說明</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> 空間 ID 值，其中使用視覺化來分析資料。</td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">視覺化的名稱。</td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">視覺化的版本。</td>
        </tr>
        <tr>
          <td align="left">savedSearchID</td>
          <td align="left">用來過濾透過視覺化顯示的資料的搜尋 ID。<br> 值的格式如下：`SpaceID_SearchTitle`，其中 SearchTitle 是搜尋的 *title* 欄位值。</td>
        </tr>
      </tbody>
    </table>
   

4. 匯出視覺化。

    1. 在「設定」頁面中，選取**物件**標籤。
    2. 在**視覺化**標籤中，選取您要匯出的視覺化。
    3. 按一下**匯出**。
    4. 儲存 JSON 檔案。
    
5. 在 {{site.data.keyword.Bluemix_notm}} 使用者介面中，切換到您要複製視覺化的空間，然後檢查 CF 應用程式或容器是否可供使用且正在執行中。
    
6.  修改在前一個步驟中匯出的搜尋 JSON 視覺化檔案。請取代空間 ID 及搜尋 ID 值。 

    例如，下列 JSON 是視覺化 JSON 檔案的範例。 

    <pre class="pre">
    [
  {
    "_id": "3d8d2eae-f3f0-44f6-9717-126113a00b51_test",
    "_type": "visualization",
    "_source": {
      "description": "",
      "group": "3d8d2eae-f3f0-44f6-9717-126113a00b51",
      "kibanaSavedObjectMeta": {
        "searchSourceJSON": "{\"filter\":[]}"
      },
      "savedSearchId": "3d8d2eae-f3f0-44f6-9717-126113a00b51_Default_9d222152-8834-4bab-8685-3036cd25931a",
      "title": "test",
      "version": 1,
      "visState": "{\"type\":\"line\",\"params\":{\"shareYAxis\":true,\"addTooltip\":true,\"addLegend\":true,\"showCircles\":true,\"smoothLines\":false,\"interpolate\":\"linear\",\"scale\":\"linear\",\"drawLinesBetweenPoints\":true,\"radiusRatio\":9,\"times\":[],\"addTimeMarker\":false,\"defaultYExtents\":false,\"setYExtents\":false,\"yAxis\":{}},\"aggs\":[{\"id\":\"1\",\"type\":\"count\",\"schema\":\"metric\",\"params\":{}}],\"listeners\":{}}"
    }
    }
    ]
    </pre>
    
    在此範例 JSON 檔案中，您可以修改下列變數： 
    
    * SPACEID：將此變數取代為新空間的空間 ID。
    * NAME：如果您要變更新空間中的視覺化名稱，請取代此變數。
    * SEARCHID：將此變數取代為新空間中的搜尋 ID。這是用來過濾透過視覺化顯示的資料的查詢 ID。
    
       <pre class="pre">
    [
  {
    "_id": "SPACEID_NAME",
    "_type": "visualization",
    "_source": {
      "description": "",
      "group": "SPACEID",
      "kibanaSavedObjectMeta": {
        "searchSourceJSON": "{\"filter\":[]}"
      },
      "savedSearchId": "SPACEID_SEARCHID",
      "title": "NAME",
      "version": 1,
      "visState": "{\"type\":\"line\",\"params\":{\"shareYAxis\":true,\"addTooltip\":true,\"addLegend\":true,\"showCircles\":true,\"smoothLines\":false,\"interpolate\":\"linear\",\"scale\":\"linear\",\"drawLinesBetweenPoints\":true,\"radiusRatio\":9,\"times\":[],\"addTimeMarker\":false,\"defaultYExtents\":false,\"setYExtents\":false,\"yAxis\":{}},\"aggs\":[{\"id\":\"1\",\"type\":\"count\",\"schema\":\"metric\",\"params\":{}}],\"listeners\":{}}"
    }
    }
    ]
    </pre>

8. 匯入視覺化。

    1. 在「設定」頁面中，選取**物件**標籤。
    2. 在**視覺化**標籤中，選取您要匯入的視覺化 JSON 檔案。
    3. 按一下**匯入**。


您可以在 Kibana 中使用視覺化，以監視新空間中應用程式可用的資料。
    
