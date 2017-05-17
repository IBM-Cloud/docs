---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 复用 Kibana 资源来分析 Bluemix 日志
{:#k4_reuse_resource}

要将搜索、可视化项或仪表板从一个 {{site.data.keyword.Bluemix}} 空间复制到其他空间，请使用 Kibana 中提供的导出和导入功能。您可以在 Kibana 中分别复制资源，也可以导出所有资源。
{:shortdesc}

| 任务 | 描述 |
|------|-------------|
| [复制搜索](k4_reuse_resource.html#k4_reuse_search) | 在不同空间之间复制搜索。 |
| [复制可视化项](k4_reuse_resource.html#k4_reuse_visualization) | 在不同空间之间复制可视化项 |

请考虑 {{site.data.keyword.Bluemix_notm}} 中用于复用搜索、可视化项或仪表板的以下场景： 

* 在同一组织的不同空间之间复制资源。

    例如，您可能希望将可视化项从 {{site.data.keyword.Bluemix_notm}} 中的开发空间复制到编译打包空间。
    
* 在同一帐户的不同组织的不同空间之间复制资源。

    例如，您可能希望将可视化项从 {{site.data.keyword.Bluemix_notm}} 的开发组织中的空间复制到编译打包组织中的空间。

* 在同一组织中位于不同公共区域中的不同空间之间复制资源。

    例如，您可能希望将可视化项从 {{site.data.keyword.Bluemix_notm}} 的组织 A 中位于公共区域“美国南部”的空间复制到组织 A 中位于公共区域“英国”的空间。



## 复制搜索
{:#k4_reuse_search}

要在 {{site.data.keyword.Bluemix_notm}} 中的不同空间之间复制搜索，请完成以下步骤：

1. 启动要复制的搜索在其中可用的 Kibana。 

    * 通过 {{site.data.keyword.Bluemix_notm}} UI 启动 Kibana：可以导出的 JSON 搜索文件包含以下字段：*空间标识*和 Cloud Foundry (CF) 应用程序的*应用程序标识*或容器的*实例标识*。有关更多信息，请参阅[通过 {{site.data.keyword.Bluemix_notm}} 仪表板访问 Kibana 仪表板](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix)。
    
    * 通过浏览器启动 Kibana：可以导出的 JSON 搜索文件包含*空间标识*字段。有关更多信息，请参阅[通过浏览器访问 Kibana 仪表板](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser)。

2. 在*设置*页面中，选择**对象**，然后选择**搜索**选项卡。接着选择一个搜索，并复制以下信息：

    <table>
      <tbody>
        <tr>
          <th align="center">搜索字段</th>
          <th align="center">描述</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> 要应用搜索以过滤数据的空间标识。</td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">搜索的名称。</td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">搜索的版本。</td>
        </tr>
      </tbody>
    </table>
   
3. 导出搜索。

    1. 在“设置”页面中，选择**对象**选项卡。
    2. 在**搜索**选项卡中，选择要导出的搜索。
    3. 单击**导出**。
    4. 保存 JSON 文件。

4. 在 {{site.data.keyword.Bluemix_notm}} UI 中，切换到要复制其搜索的空间，并检查 CF 应用程序或容器是否可用并在运行。
    
5. 启动要将搜索导入其中的 {{site.data.keyword.Bluemix_notm}} 空间的 Kibana，然后获取以下信息：

    在 [Bluemix UI](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix) 中：
    
    <table>
      <tbody>
        <tr>
          <th align="center">搜索字段</th>
          <th align="center">描述</th>
        </tr>
        <tr>
          <td align="left">空间标识</td>
          <td align="left"> <ol><li> 在*设置*页面中，选择*索引*选项卡。</li> <br> <li>空间标识嵌入在索引模式中。索引模式的格式如下：`[logstash-3d8d2eae-SpaceID-]YYYY.MM.DD`，其中 *SpaceID* 是空间的标识。复制该空间标识。</li></ol></td>
        </tr>
        <tr>
          <td align="left">应用程序标识或实例标识</td>
          <td align="left"><ul><li>通过 {{site.data.keyword.Bluemix_notm}} UI 启动 Kibana 时，缺省情况下会打开*发现*页面。从*发现*页面的搜索栏中获取应用程序标识或实例标识，例如 `application_id:d88d1f16-e9d9-4623-bce7-0348c88f5133`。</li> <br> <li>通过浏览器启动 Kibana 时，请从“发现”页面的“字段列表”中选择 application_id 或 instance_id 字段。</li></ul></td>
        </tr>
      </tbody>
    </table>

6. 修改在先前步骤中导出的搜索 JSON 搜索文件。替换应用程序标识值。 

    例如，以下 JSON 是搜索 JSON 文件的示例。 
 
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
    
    在此样本 JSON 文件中，可以使用新空间的信息来修改以下变量： 
    
    * SPACEID：将此变量替换为新空间的空间标识。
    * NAME：如果要更改搜索在新空间中的名称，请替换此变量。要保留原有名称不变，请勿更改此值。
    * APPID：将此变量替换为新空间中 CF 应用程序的 application_id 值，或替换为新空间中容器的实例标识。
    
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

6. 将搜索 JSON 文件导入到新空间的 Kibana。

    1. 在“设置”页面中，选择**对象**选项卡。
    2. 在**搜索**选项卡中，选择要导入的搜索 JSON 文件。
    3. 单击**导入**。

可以在 Kibana 中使用搜索来监视可用于新空间中应用程序的数据。


    
## 复制可视化项
{:#k4_reuse_visualization}

要将用于分析一个空间中应用程序的数据的可视化项复制到其他空间，请完成以下步骤：

1. 启动要复制的可视化项在其中可用的空间的 Kibana。 

    * 通过 {{site.data.keyword.Bluemix_notm}} UI 启动 Kibana：可以导出的 JSON 搜索文件包含以下字段：*空间标识*和 Cloud Foundry (CF) 应用程序的*应用程序标识*或容器的*实例标识*。有关更多信息，请参阅[通过 {{site.data.keyword.Bluemix_notm}} 仪表板访问 Kibana 仪表板](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix)。
    
    * 通过浏览器启动 Kibana：可以导出的 JSON 搜索文件包含*空间标识*字段。有关更多信息，请参阅[通过浏览器访问 Kibana 仪表板](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser)。
    
2. 在不同空间之间复制与可视化项关联的搜索。有关更多信息，请参阅[在不同 Bluemix 空间之间复制搜索](k4_reuse_resource.html#k4_reuse_search)。

    可视化项使用搜索来过滤其显示的数据。可视化项可链接到搜索，以便对搜索所做的所有更新都会自动更新，也可不链接到搜索，这样可供分析的数据仅为创建可视化项时显示的数据。

    复制可视化项时，不管它是否链接到搜索，都必须同时复制与其关联的搜索。**注：**将可视化项导入到新空间时，新可视化项会链接到新空间中的搜索。
    
3. 在*设置*页面中，选择**对象**，然后选择**可视化项**选项卡。接着选择一个可视化项，并获取以下信息： 

    <table>
      <tbody>
        <tr>
          <th align="center">可视化项字段</th>
          <th align="center">描述</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> 在其中使用可视化项来分析数据的空间的标识值。</td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">可视化项的名称。</td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">可视化项的版本。</td>
        </tr>
        <tr>
          <td align="left">savedSearchID</td>
          <td align="left">用于过滤通过可视化项显示的数据的搜索标识。<br> 值的格式如下：`SpaceID_SearchTitle`，其中 SearchTitle 是搜索的 *title* 字段的值。</td>
        </tr>
      </tbody>
    </table>
   

4. 导出可视化项。

    1. 在“设置”页面中，选择**对象**选项卡。
    2. 在**可视化项**选项卡中，选择要导出的可视化项。
    3. 单击**导出**。
    4. 保存 JSON 文件。
    
5. 在 {{site.data.keyword.Bluemix_notm}} UI 中，切换到要复制其可视化项的空间，并检查 CF 应用程序或容器是否可用并在运行。
    
6.  修改在先前步骤中导出的搜索 JSON 可视化项文件。替换空间标识和搜索标识值。 

    例如，以下 JSON 是可视化项 JSON 文件的示例。 

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
    
    在此样本 JSON 文件中，可以修改以下变量： 
    
    * SPACEID：将此变量替换为新空间的空间标识。
    * NAME：如果要更改可视化项在新空间中的名称，请替换此变量。
    * SEARCHID：将此变量替换为新空间中的搜索标识。这是用于过滤通过可视化项显示的数据的查询标识。
    
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

8. 导入可视化项。

    1. 在“设置”页面中，选择**对象**选项卡。
    2. 在**可视化项**选项卡中，选择要导入的可视化项 JSON 文件。
    3. 单击**导入**。


可以在 Kibana 中使用可视化项来监视可用于新空间中应用程序的数据。
    
