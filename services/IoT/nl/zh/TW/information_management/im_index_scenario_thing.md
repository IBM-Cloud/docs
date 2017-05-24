---

copyright:
years: 2016, 2017
lastupdated: "2017-04-11"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 應用程式介面情境 2（測試版）
{: #scenario}

應用程式介面是用來移除應用程式的需求，以瞭解如何配置裝置或事物。例如，您可以使用單一裝置來測量會議室的溫度，也可以取得多個裝置的平均讀數來計算會議室的溫度。應用程式需要一個以上會議室狀態的資訊，而會議室的其中一個元件是 temperature 內容。計算應用程式所收到溫度值的方式無關。

在此情境下，溫度感應器及濕度感應器會發佈在兩間會議室收集到的環境資料。溫度及濕度感應器資料分別對映至兩個裝置類型應用程式介面，一個是用於溫度計裝置類型，一個則是用於濕度計裝置類型。接著會建立稱為 *RoomType* 的事物類型，以及兩個會議室事物實例：*meetingroom1* 及 *meetingroom2*。

此情境會設定包括溫度計及濕度計應用程式介面的組合，然後將正確的環境感應器對映至每一個會議室實例（例如，*temperatureSensor1* 及 *humiditySensor1* 對映至 *meetingroom1*）。

## 必要條件
{: #pre_req}

此情境會以前一個[應用程式介面情境 1](im_index_scenario) 為建置基礎。

繼續之前，請確定您已：
- 使用相同的 {{site.data.keyword.iot_short_notm}} 組織實例，以及該組織的 API 金鑰或記號。如需 API 金鑰及記號的相關資訊，請參閱[應用程式的 HTTP REST API](../applications/api.html#authentication)。
- 建立兩個應用程式介面，一個是適用於溫度感應器，一個則是適用於濕度感應器。如需配置溫度感應器之應用程式介面的相關資訊，請參閱[裝置類型應用程式介面情境](../information_management/im_index_scenario)。

## 關於此作業
{: #about}

在 {{site.data.keyword.iot_short_notm}} 中，事物可以包含數個裝置及事物。事物類型定義事物實例的組合方式。應用程式介面可以與事物類型相關聯。此關聯定義針對事物類型實例所產生之狀態的結構。對映是用來定義如何將所聚集裝置及事物的內容對映至事物狀態的內容。

在此情境下，兩個溫度感應器及兩個濕度感應器會將事件發佈至 {{site.data.keyword.iot_short_notm}}。一個溫度感應器及一個濕度感應器是在辦公室區塊的會議室 1 中。另一個溫度及濕度感應器則是在會議室 2 中。

![{{site.data.keyword.iot_short_notm}} 上溫度及濕度事物與應用程式之間的對映。](images/Information "{{site.data.keyword.iot_short_notm}} 上某會議室的多個環境感應器與應用程式之間的對映")

稱為 *RoomType* 的事物類型是用來定義會議室實例的組合方式。應用程式介面是與 *RoomType* 相關聯，並定義入埠事件對映至同時顯示溫度及濕度的單一讀數。這個單一讀數是事物狀態。對映是用來定義如何將溫度及濕度感應器的內容對映至此事物狀態。這些感應器發佈新的讀數時，與事物狀態相關聯之內容的值就會變更。

包括下列四個裝置：

裝置/類型 | 事件 | 事件有效負載/內容
------------- |  ------------- | -------------
*temperatureSensor1*/溫度計 (meetingroom1) | `iot-2/evt/`*`tevt`*`/fmt/json` | `{ “t” : 34.5 }`/ **temperature1**
*temperatureSensor2*/溫度計 (meetingroom2) | `iot-2/evt/`*`tempevt`*`/fmt/json` | `{ “temp” : 34.5 }`/ **temperature2**  
*humiditySensor1*/濕度計 (meetingroom1) | `iot-2/evt/`*`hevt`*`/fmt/json` | `{  “h” : "75%" }`/ **humidity1**
*humiditySensor2*/濕度計 (meetingroom2) |`iot-2/evt/`*`humevt`*`/fmt/json` | `{  “hum” : "75%"}`/ **humidity2**

事物類型應用程式介面會以下列結構呈現事物狀態：
```
{
  “temperature” : <current temperature value in Celsius>
  "humidity" : <current humidity value>
  }
```

<!--
The code that is used in this example is available in the updated {{site.data.keyword.iot_short_notm}} [[Python library ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-python){: new_window} in GitHub, in the **thingDataTransform** sample.
-->  

使用下列範例情境，以設定您自己的介面環境。  

## 必要的話，新增裝置類型及裝置  
{: #add_device}  
在此情境下，會使用兩個裝置類型及四個裝置實例。裝置實例 *temperatureSensor1* 及 *temperatureSensor2* 是與裝置類型 *Thermometer* 相關聯。裝置實例 *humiditySensor1* 及 *humiditySensor2* 是與裝置類型 *Hygrometer* 相關聯。

如需使用 REST API 來新增裝置類型的相關資訊，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofThings.ibmcloud.com/swagger/v0002.html#!/Device_Types) 文件。  

## 步驟 1：建立組合綱目檔。  
{: #crt_composition_file}  
建立組合綱目檔，以參照每一個溫度及濕度裝置類型的裝置應用程式介面 ID。  

下列範例顯示如何建立稱為 *Room Type Schema* 的組合綱目檔。  
```
{
   "$schema": "http://json-schema.org/draft-04/schema#",
   "type" : "object",
   "title" : "Room Type Schema",
   "description" : "JSON Schema that defines the structure of the Room Thing Type.",
   "properties" : {
       "temperatureSensor": {
           "description": "The temperature sensor device",
           "$applicationInterfaceRef": "58c135e352faff0001198a89"
       },
       "humiditySensor": {
           "description": "The humidity sensor device",
           "$applicationInterfaceRef": "58c135ea52faff0001678f06"
       }
   },
   "required" : [
       "temperatureSensor",
       "humiditySensor"
   ]
}
```
**提示：**使用 "required" 參數，以將一個以上的內容標示為必要。required 內容必須包含在 Watson IoT Platform 的裝置訊息中，才能使用裝置資料來更新裝置狀態。不會處理未包括 required 內容的訊息。   
**附註：**當您建立事物類型時，必須指定在建立事物類型綱目檔時所產生的綱目 ID。  

## 步驟 2：建立組合綱目資源。  
{: #crt_composition_resource}  

上傳前一個步驟中所產生的事物類型綱目檔，即可建立綱目資源。  
使用下列 API，以上傳事物類型綱目檔：  
```
POST /schemas
```  
以下是必要參數：  
<table>
<tr>
<th>	參數</th><th>	說明</th>
</tr>
<tr>
<td>	name	</td><td>	提供所建立組合綱目的名稱。</td>
</tr>
<tr>
<td>	schemaFile	</td><td>	本端組合綱目 JSON 檔案的路徑。</td>
</tr>
</table>

如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas) 文件。

  

<!-- The following example shows how to use Python to create the thing type schema resource:  
```python
roomTypeSchemaFile = open(schemasDir + "roomType.json", "r");
roomTypeSchema = roomTypeSchemaFile.read();
roomTypeSchemaFile.close();
"roomTypeSchemaId", result = api.createSchema("Room Type Schema", "roomType.json", roomTypeSchema)
```  -->

## 步驟 3：建立事物類型  
{: #crt_thing_type}  

事物類型是用來建立事物實例的模型。必須先在組織中建立事物類型，才能建立事物實例。在此情境中，建立一個事物類型。  
與事物類型相關聯的綱目定義聚集在一起以建立事物實例的物件類型。事物類型必須參照您在前一個步驟中所建立的事物類型綱目資源。  
使用下列 API，以建立事物類型：
```
POST /thing/types
```
以下是必要參數：  
<table>
<tr><th>參數</th><th>說明</th></tr>
<tr><td>Id</td><td>提供所建立事物類型的 ID。</td></tr>
<tr><td>name</td><td>提供所建立事物類型的名稱。</td></tr>
<tr><td>schemaId</td><td>針對組合綱目資源所建立的 ID。</td></tr>
</table>

如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) 文件。

  

<!-- The following example shows how to use Python to create a thing type that is called *RoomType*.
```python
result = api.createThingType(thingType, "RoomType", "roomTypeSchemaId", "The Room Thing type")

```  -->

## 步驟 4：建立應用程式介面綱目檔  
{: #crt_ai_schema_file}
在應用程式介面中，您可以定義儲存為事物狀態之資料的結構。在此情境中，建立可定義溫度及濕度內容的應用程式介面。參照建立應用程式介面資源時所產生的應用程式介面 ID，以將應用程式介面與事物類型 *RoomType* 相關聯。  
下列範例顯示如何建立稱為 *RoomType Schema* 的應用程式介面綱目檔。
```
{
   "$schema": "http://json-schema.org/draft-04/schema#",
   "type" : "object",
   "title" : "RoomType Schema",
   "description" : "JSON Schema that defines the canonical room state structure",
   "properties" : {
       "temperature" : {
            "description" : "Temperature in degrees celsius",
           "type" : "number",
           "minimum" : -273.15,
           "default" : 0.0
       },
       "humidity" : {
           "description" : "Percentage humidity",
           "type" : "number",
           "minimum" : 0,
           "maximum" : 100,
           "default" : 0.0
       }
   },
   "required" : [
       "temperature",
       "humidity"
   ]
}
```  
## 步驟 5：建立應用程式介面綱目資源。  
{: #crt_ai_schema_resource}  
使用下列 API，以上傳前一個步驟中所建立的應用程式介面綱目檔，來建立事物類型的應用程式介面綱目資源：  
```
POST /schemas
```  
以下是必要參數：  
<table>
<tr>
<th>參數</th><th>說明</th>
</tr>
<tr>
<td>name</td><td>提供所建立應用程式介面綱目的名稱。</td>
</tr>
<tr>
<td>schemaFile</td><td>本端應用程式介面綱目 JSON 檔案的路徑。</td>
</tr>
</table>  

如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas) 文件。

  

<!-- The following example shows how to use Python to create the thing type application interface schema resource:  
```python
roomSchemaFile = open(schemasDir + "room.json", "r");
roomSchema = roomSchemaFile.read();
roomSchemaFile.close();
"roomSchemaId", result = api.createSchema("Room Schema", "room.json", roomSchema)
```  -->

使用綱目 ID，以將應用程式介面綱目資源新增至事物類型的應用程式介面。  

## 步驟 6：建立事物類型的應用程式介面。  
{: #crt_thing_ai}  
應用程式介面必須參照您在前一個步驟中所建立的應用程式介面綱目資源。  
若要建立應用程式介面，請使用下列 API：  
```
POST /applicationinterfaces
```  
以下是必要參數：  
<table>
<tr>
<th>	參數</th><th>	說明</th>
</tr>
<tr>
<td>	name	</td><td>	提供所建立應用程式介面的名稱。</td>
</tr>
<tr>
<td>	description	</td><td>	提供應用程式介面的說明。</td>
</tr>
<tr>
<td>	schemaId	</td><td>	本端應用程式介面綱目 JSON 檔案的路徑。</td>
</tr>
</table>  

如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Application_Interfaces) 文件。

  
使用前一個回應中所傳回的綱目 ID，以將應用程式介面綱目新增至應用程式介面。  

<!-- The following example shows how to use Python to create an application interface:  
```python
"applicationInterfaceId", result = api.createApplicationInterface("IRoom", "roomSchemaId")
```  -->

使用應用程式介面 ID，以將應用程式介面新增至裝置類型。您也可以使用此 ID，以將入埠裝置事件對映至應用程式介面所定義的內容。

  

## 步驟 7：將應用程式介面新增至事物類型。  
{: #add_thing_ai}  
若要將應用程式介面新增至事物類型，請使用下列 API：  
```
POST /thing/types/{thingtypeId}/applicationinterfaces
```  
以下是必要參數：  
<table>
<tr>
<th>	參數</th><th>	說明</th>
</tr>
<tr>
<td>	id	</td><td>	針對事物類型所建立的 ID。</td>
</tr>
<tr>
<td>	name	</td><td>	提供所建立應用程式介面的名稱。</td>
</tr>
<tr>
<td>	schemaId	</td><td>	針對應用程式介面資源所建立的 ID。</td>
</tr>
<tr>
<td>	refs/schema	</td><td>	應用程式介面資源的路徑。一般是：/schemas/*schemaId*	</td>
</tr>
</table>  

如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) 文件。

  
在此情境下，應用程式介面會與事物類型 *RoomType* 相關聯。

<!-- The following example shows how to use Python to add the thing application interface to the thing type *RoomType*:  
```python
result = api.addApplicationInterfaceToThingType(RoomType, "applicationInterfaceId", "roomSchemaId")
``` -->

## 步驟 8：定義對映
{: #define_Thing_type_mappings}

定義事物類型的對映，以說明如何將所聚集裝置或事物之狀態的內容對映至事物類型應用程式介面上所定義的內容。

若要對映事件，請使用下列 API：  
```
POST /thing/types/{thingtypeId}/mappings
```  

以下是必要參數：  
<table>
<tr>
<th>	參數</th><th>	說明</th>
</tr>
<tr>
<td>	applicationInterfaceId	</td><td>	針對應用程式介面所建立的 ID。</td>
</tr>
<tr>
<td>	propertyMappings	</td><td>	有效的 JSON 結構，可對映針對應用程式介面所定義的內容與裝置事件有效負載的內容。</td>
</tr>
</table>  

如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) 文件。



<!--  The following example shows how to use Python to add a mapping to thing type *RoomType*:

```python
mappings = {
     "humiditySensor": {
       "humidity": "$event.humidity"
     },
     "temperatureSensor": {
       "temperature": "$event.temperatureC"
     }
 }

 result = api.addMappingsToThingType(thingType, "applicationInterfaceId", mappings)
``` -->

下列範例顯示範例 propertyMappings 參數項目：

```
{
  "applicationInterfaceId": "58dd849752faff0001638851",
  "propertyMappings": {
       "humiditySensor": {
         "humidity": "$event.humidity"
       },
       "temperatureSensor": {
         "temperature": "$event.temperatureC"
       }
   }
}
```

*humiditySensor* 定義於事物綱目中。"$event.humidity" 定義於 ID 為 "58c135ea52faff0001678f06" 的應用程式介面綱目中。
*temperatureSensor* 定義於事物綱目中。"$event.temperatureC" 定義於 ID 為 "58c135e352faff0001198a89" 的應用程式介面綱目中。

## 步驟 9：部署與事物類型相關聯的配置  
{: #deploy_Thing_config}   
部署與每一種事物類型的事物狀態更新相關的配置。此配置包括綱目、應用程式介面及對映。

您必須先部署事物類型配置，才能建立事物類型的任何實例。

若要部署事物類型配置，請使用下列 API：

```
PATCH /thing/types/{thingtypeId}
```
如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types) 文件。

<!-- The following example shows how to use Python to deploy your configuration for thing type *Room*:

```python
result = api.deployThingTypeConfiguration(thingType)
``` -->

## 步驟 10：建立事物類型的實例
{: #create_Thing_instances}

事物是事物類型的實例。事物可讓您將裝置或事物的一個以上實例聚集至單一物件。

若要建立事物，請使用下列 API：

```
POST /thing/types/{thingTypeId}/things
```

以下是必要參數：  
<table>
<tr>
<th>	參數</th><th>	說明</th>
</tr>
<tr>
<td>	typeId	</td><td>		先前所建立事物類型的 ID。</td>
</tr>
<tr>
<td>	thingId	</td><td>	提供所建立事物實例的名稱。</td>
</tr>
</table>

如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Things) 文件。



在此情境下，我們需要建立事物類型為 *RoomType* 的兩個事物實例。其中一個事物實例稱為 *meetingroom1*，另一個事物實例則稱為 *meetingroom2*。

<!-- The following example shows how to use Python to create a thing instance that is called *meetingroom1*. *meetingroom1* is associated with the *temperatureSensor1* and *humiditySensor1* device instances.

```python
thingId = "meetingroom1"
 meetingroom1AggregatedObjects = {
   "temperatureSensor": {
     "type": "device",
     "typeId": "TemperatureSensor",
     "id": "temperatureSensor1"
   },
   "humiditySensor": {
     "type": "device",
     "typeId": "HumiditySensor",
     "id": "humiditySensor1"
   }
 }
 result = api.createThing(thingType, thingId, "Meeting Room 1", "The big meeting room!!!", aggregatedObjects = meetingroom1AggregatedObjects)
``` -->

所建立的事物 ID 是用於呼叫以將溫度事件新增至事物應用程式介面的 POST 方法的 URL 中。

<!-- The following example shows how to use Python to create a thing instance that is called *meetingroom2*. *meetingroom2* is associated with the *temperatureSensor2* and *humiditySensor2* device instances.

```python
thingId = "meetingroom2"
   meetingroom2AggregatedObjects = {
    "temperatureSensor": {
      "type": "device",
      "typeId": "TemperatureSensor",
      "id": "temperatureSensor2"
    },
    "humiditySensor": {
      "type": "device",
      "typeId": "HumiditySensor",
      "id": "humiditySensor2"
    }
  }
result = api.createThing(thingType, thingId, "Meeting Room 2", "The little meeting room!!!", aggregatedObjects = meetingroom2AggregatedObjects)  
``` -->

## 步驟 11：驗證對映的裝置事件已發佈至應用程式介面  
{: #publish_event}  
針對聚集至事物 *meetingroom1* 的裝置，發佈下列事件：  
 - 將來自 *temperatureSensor1* 的溫度事件發佈於主題 `iot-2/evt/tevt/fmt/json`  
 - 將來自 *humiditySensor1* 的濕度事件發佈於主題 `iot-2/evt/hevt/fmt/json`  
針對聚集至事物 *meetingroom2* 的裝置，發佈下列事件：  
 - 將來自 *temperatureSensor2* 的溫度事件發佈於主題 `iot-2/evt/tempevt/fmt/json`  
 - 將來自 *humiditySensor2* 的濕度事件發佈於主題 `iot-2/evt/humevt/fmt/json`  
如需發佈來自裝置的入埠事件的相關資訊，請參閱[應用程式的 MQTT 連線功能](../applications/mqtt.html#publishing_device_events)。  

## 步驟 12：確認事物的狀態已變更。  
{: #verify_Thing_state}  
若要檢查事物狀態，請使用下列 API：  
```
GET /thing/types/{thingTypeId}/things/{thingId}/state/{applicationInterfaceId}
```  

以下是必要參數：  
<table>
<tr>
<th>參數</th><th>	說明</th>
</tr>
<tr>
<td>thingtypeId	</td><td>事物類型 ID</td>
</tr>
<tr>
<td>thingId	</td><td>	事物 ID。</td>
</tr>
<tr>
<td>applicationInterfaceId</td><td>針對應用程式介面所建立的 ID。</td>
</tr>
</table>  

如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) 文件。

  

<!-- The following example shows how to use Python to retrieve the current state of *meetingroom1* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom1", applicationInterfaceId)
```  
The following example shows how to use Python to retrieve the current state of *meetingroom2* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom2", applicationInterfaceId)
``` -->
