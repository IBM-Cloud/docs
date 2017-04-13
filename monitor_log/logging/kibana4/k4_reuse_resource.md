---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Reusing Kibana resources to analyze Bluemix logs
{:#k4_reuse_resource}

To copy a search, a visualization, or a dashboard from one {{site.data.keyword.Bluemix}} space to a different one, use the export and import capabilities that are available in Kibana. You can copy resources individually or export all resources in Kibana.
{:shortdesc}

| Task | Description |
|------|-------------|
| [Copy a search](k4_reuse_resource.html#k4_reuse_search) | Copy a search between spaces. |
| [Copy a visualization](k4_reuse_resource.html#k4_reuse_visualization) | Copy a visualization between spaces |

Consider the following scenarios in {{site.data.keyword.Bluemix_notm}} for reusing searches, visualizations, or dashboards: 

* Copy a resource between spaces in the same organization.

    For example, you might want to copy your visualizations from your development space in {{site.data.keyword.Bluemix_notm}} to your stage space.
    
* Copy a resource between spaces in different organizations in the same account.

    For example, you might want to copy your visualizations from a space in your development organization in {{site.data.keyword.Bluemix_notm}} to a space in your staging organization.

* Copy a resource between spaces that are in the same organization but located different public regions.

    For example, you might want to copy your visualizations from a space in organization A in {{site.data.keyword.Bluemix_notm}} that is located in the public region US South to a space in your organization A in the public region United Kingdom.



## Copying a search
{:#k4_reuse_search}

Complete the following steps to copy a search between spaces in {{site.data.keyword.Bluemix_notm}}:

1. Launch Kibana where the search that you want to copy is available. 

    * Launch Kibana from {{site.data.keyword.Bluemix_notm}} UI: The JSON search file that you can export includes the following fields: *space ID*, and *application ID* for Cloud Foundry (CF) applications or the *instance ID* for containers. For more information, see [Getting to the Kibana dashboard from the {{site.data.keyword.Bluemix_notm}} dashboard](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).
    
    * Launch Kibana from a browser: The JSON search file that you can export includes the field *space ID*. For more information, see [Getting to the Kibana dashboard from a browser](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser).

2. In the *Settings* page, select **Objects**, and the **Searches** tab. Then select a search and copy the following information:

    <table>
      <tbody>
        <tr>
          <th align="center">Search field</th>
          <th align="center">Description</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> Space ID where the search is applied to filter data.</td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">Name of the search.</td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">Version of the search.</td>
        </tr>
      </tbody>
    </table>
   
3. Export the search.

    1. In the Settings page, select the **Objects** tab.
    2. In the **Searches** tab, select the search that you want to export.
    3. Click **Export**.
    4. Save the JSON file.

4. In the {{site.data.keyword.Bluemix_notm}} UI, change to the space where you want to copy the search, and check the CF application or container is available and running.
    
5. Launch Kibana for the {{site.data.keyword.Bluemix_notm}} space where you want to import the search and then, get the following information:

    From the [Bluemix UI](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix):
    
    <table>
      <tbody>
        <tr>
          <th align="center">Search field</th>
          <th align="center">Description</th>
        </tr>
        <tr>
          <td align="left">space ID</td>
          <td align="left"> <ol><li> In the *Settings* page, select the *Indices* tab.</li> <br> <li>The space ID is embedded in the index pattern. The format of the index pattern is the following: `[logstash-3d8d2eae-SpaceID-]YYYY.MM.DD` where *SpaceID* is the ID of the space. Copy the space ID.</li></ol></td>
        </tr>
        <tr>
          <td align="left">application ID or instance ID</td>
          <td align="left"><ul><li>When you launch Kibana from the {{site.data.keyword.Bluemix_notm}} UI, the *Discover* page is opened by default. Get the application ID or the instance ID from the search bar in the *Discover* page, for example, `application_id:d88d1f16-e9d9-4623-bce7-0348c88f5133`.</li> <br> <li>When you launch Kibana from a browser, select the field application_id or instance_id from the Fields List in the Discover page.</li></ul></td>
        </tr>
      </tbody>
    </table>

6. Modify the search JSON search file that you exported in a previous step. Replace the application ID value. 

    For example, the following JSON is an example of a search JSON file. 
 
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
    
    In this sample JSON file, you can modify the following variables with the information of the new space: 
    
    * SPACEID: Replace this variable with the space ID of the new space.
    * NAME: Replace this variable if you want to change the name of the search in the new space. To maintain the same name, do not change this value.
    * APPID: Replace this variable with the application_id value of the CF app in the new space or the instance ID of the container in the new space.
    
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

6. Import the search JSON file into Kibana for the new space.

    1. In the Settings page, select the **Objects** tab.
    2. In the **Searches** tab, select the search JSON file that you want to import.
    3. Click **Import**.

You can use the search in Kibana to monitor the data that is available for your application in the new space.


    
## Copying a visualization
{:#k4_reuse_visualization}

Complete the following steps to copy a visualization that you use to analyze data of an application in a space to a different space:

1. Launch Kibana for the space where the visualization that you want to copy is available. 

    * Launch Kibana from {{site.data.keyword.Bluemix_notm}} UI: The JSON search file that you can export includes the following fields: *space ID*, and *application ID* for Cloud Foundry (CF) applications or the *instance ID* for containers. For more information, see [Getting to the Kibana dashboard from the {{site.data.keyword.Bluemix_notm}} dashboard](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).
    
    * Launch Kibana from a browser: The JSON search file that you can export includes the field *space ID*. For more information, see [Getting to the Kibana dashboard from a browser](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser).
    
2. Copy the search that is associated with the visualization between spaces. For more information, see [Copying a search between Bluemix spaces](k4_reuse_resource.html#k4_reuse_search).

    A visualization uses a search to filter the data that it displays. A visualization might be linked to a search so all the updates that you make to the search are updated automatically, or not linked to a search so the only data that is available for analysis is the data displayed at the time that you created the visualization.

    When you copy a visualization, regardles of its linked status to a search, you must also copy the search that is associated to it. **Note:** When you import a visualization into the new space, the new visualization is linked to the search in the new space.
    
3. In the *Settings* page, select **Objects** and the **Visualizations** tab. Then, select a visualization and obtain the following information: 

    <table>
      <tbody>
        <tr>
          <th align="center">Visualization field</th>
          <th align="center">Description</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> Space ID value where the visualization is used to analyze data.</td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">Name of the visualization.</td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">Version of the visualization.</td>
        </tr>
        <tr>
          <td align="left">savedSearchID</td>
          <td align="left">ID of the search that is used to filter the data that is displayed through the visualization. <br> The value has the following format: `SpaceID_SearchTitle` where SearchTitle is the value of the *title* field of the search. </td>
        </tr>
      </tbody>
    </table>
   

4. Export the Visualization.

    1. In the Settings page, select the **Objects** tab.
    2. In the **Visualizations** tab, select the visualization that you want to export.
    3. Click **Export**.
    4. Save the JSON file.
    
5. In the {{site.data.keyword.Bluemix_notm}} UI, change to the space where you want to copy the visualization, and check the CF application or container is available and running.
    
6.  Modify the search JSON visualization file that you exported in a previous step. Replace the space ID and the search ID values. 

    For example, the following JSON is an example of a visualization JSON file. 

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
    
    In this sample JSON file, you can modify the following variables: 
    
    * SPACEID: Replace this variable with the space ID of the new space.
    * NAME: Replace this variable if you want to change the name of the visualization in the new space.
    * SEARCHID: Replace this variable with the search ID in the new space. This is the ID of the query that is used to filter the data that is displayed through the visualization.
    
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

8. Import the visualization.

    1. In the Settings page, select the **Objects** tab.
    2. In the **Visualizations** tab, select the visualization JSON file that you want to import.
    3. Click **Import**.


You can use the visualization in Kibana to monitor the data that is available for your application in the new space.
    
