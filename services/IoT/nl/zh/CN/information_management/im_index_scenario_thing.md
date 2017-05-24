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

# 应用程序接口场景 2 (Beta)
{: #scenario}

通过使用应用程序接口，应用程序就无需了解设备和事物是如何配置的。例如，您可能会使用单个设备测量房间的温度，或者，可能会通过将多个设备的读数取平均值来计算房间的温度。应用程序需要了解一个或多个房间的状态，其中之一就是温度属性。至于如何计算应用程序接收到的温度值则无关紧要。

在此场景中，温度传感器和湿度传感器发布在两个会议室中收集到的环境数据。温度和湿度传感器数据分别映射到两个设备类型应用程序接口，一个针对温度计设备类型，一个针对湿度计设备类型。然后会创建一个名为 *RoomType* 的事物类型，以及两个房间事物实例：*meetingroom1* 和 *meetingroom2*。

此场景设置一个组合，其中包含温度计和湿度计应用程序接口，然后将正确的环境传感器映射到每个房间实例，例如 *temperatureSensor1* 和 *humiditySensor1* 映射到 *meetingroom1*。

## 先决条件
{: #pre_req}

此场景构建在先前的[应用程序接口场景 1](im_index_scenario) 上。

继续操作之前，请先确保：
- 使用相同的 {{site.data.keyword.iot_short_notm}} 组织实例以及该组织的 API 密钥或令牌。有关 API 密钥和令牌的更多信息，请参阅[针对应用程序的 HTTP REST API](../applications/api.html#authentication)。
- 已创建两个应用程序接口，一个用于温度传感器，一个用于湿度传感器。有关为温度传感器配置应用程序接口的信息，请参阅[设备类型应用程序接口场景](../information_management/im_index_scenario)。

## 关于此任务
{: #about}

在 {{site.data.keyword.iot_short_notm}} 中，事物可以由多个设备和事物组成。事物类型定义如何编写事物的实例。应用程序接口可以与事物类型相关联。此关联定义为事物类型实例生成的状态的结构。映射用于定义如何将来自聚合设备和事物的属性映射到事物状态上的属性。

在此场景中，两个温度传感器和两个湿度传感器将事件发布到 {{site.data.keyword.iot_short_notm}}。一个温度传感器和一个湿度传感器位于办公区块的会议室 1 中。另一个温度和湿度传感器位于会议室 2 中。

![一个房间中的多个环境传感器与 {{site.data.keyword.iot_short_notm}} 上应用程序之间的映射。](images/Information "一个房间中的多个环境传感器与 {{site.data.keyword.iot_short_notm}} 上应用程序之间的映射")

名为 *RoomType* 的事物类型用于定义如何编写各房间的实例。一个应用程序接口与 *RoomType* 相关联，并定义将入站事件映射到同时显示温度和湿度的单个读数。此单个读数即是事物状态。映射用于定义如何将来自温度和湿度传感器的属性映射到此事物状态。在这些传感器发布新的读数时，与事物状态关联的属性的值会更改。

包含下列四个设备：

设备/类型 | 事件 | 事件有效内容/属性
------------- |  ------------- | -------------
*temperatureSensor1*/Thermometer (meetingroom1) | `iot-2/evt/`*`tevt`*`/fmt/json` | `{ “t” : 34.5 }`/ **temperature1**
*temperatureSensor2*/Thermometer (meetingroom2) | `iot-2/evt/`*`tempevt`*`/fmt/json` | `{ “temp” : 34.5 }`/ **temperature2**  
*humiditySensor1*/Hygrometer (meetingroom1) | `iot-2/evt/`*`hevt`*`/fmt/json` | `{  “h” : "75%" }`/ **humidity1**
*humiditySensor2*/Hygrometer (meetingroom2) |`iot-2/evt/`*`humevt`*`/fmt/json` | `{  “hum” : "75%"}`/ **humidity2**

该事物类型应用程序接口表示事物状态的结构如下：
```
{
  “temperature” : <current temperature value in Celsius>
  "humidity" : <current humidity value>
  }
```

<!--
The code that is used in this example is available in the updated {{site.data.keyword.iot_short_notm}} [[Python library ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-python){: new_window} in GitHub, in the **thingDataTransform** sample.
-->  

使用以下示例场景来设置您自己的接口环境。  

## 根据需要添加设备类型和设备  
{: #add_device}  
在此场景中，会使用两种设备类型和四个设备实例。设备实例 *temperatureSensor1* 和 *temperatureSensor2* 与设备类型 *Thermometer* 相关联。设备实例 *humiditySensor1* 和 *humiditySensor2* 与设备类型 *Hygrometer* 相关联。

有关使用 REST API 来添加设备类型的信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofThings.ibmcloud.com/swagger/v0002.html#!/Device_Types) 文档。  

## 步骤 1：创建组合模式文件。  
{: #crt_composition_file}  
创建组合模式文件，该文件引用每个温度和湿度设备类型的设备应用程序接口标识。  

以下示例显示了如何创建名为 *Room Type Schema* 的组合模式文件。  
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
**提示：**使用“required”参数将一个或多个属性设为必需属性。设备消息中必须包含必需属性，Watson IoT Platform 才能使用设备数据更新设备状态。不会对不包含必需属性的消息进行处理。   
**注：**在创建事物类型模式文件时生成的模式标识必须在创建事物类型时指定。  

## 步骤 2：创建组合模式资源。  
{: #crt_composition_resource}  

创建模式资源，方法是上传在先前步骤中生成的事物类型模式文件。  
使用以下 API 上传事物类型模式文件：  
```
POST /schemas
```  
以下参数是必需的：  
<table>
<tr>
<th>	参数</th><th>	描述</th>
</tr>
<tr>
<td>	name	</td><td>	为您要创建的组合模式提供名称。</td>
</tr>
<tr>
<td>	schemaFile	</td><td>	到本地组合模式 JSON 文件的路径。</td>
</tr>
</table>

有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas) 文档。

  

<!-- The following example shows how to use Python to create the thing type schema resource:  
```python
roomTypeSchemaFile = open(schemasDir + "roomType.json", "r");
roomTypeSchema = roomTypeSchemaFile.read();
roomTypeSchemaFile.close();
"roomTypeSchemaId", result = api.createSchema("Room Type Schema", "roomType.json", roomTypeSchema)
```  -->

## 步骤 3：创建事物类型  
{: #crt_thing_type}  

事物类型用于为事物实例建模。必须先在组织中创建事物类型，然后才能创建事物实例。对于此场景，请创建一个事物类型。  
与事物类型关联的模式可定义那些聚合在一起以形成事物实例的对象的类型。事物类型必须引用您在先前步骤中创建的事物类型模式资源。  
使用以下 API 创建事物类型：
```
POST /thing/types
```
以下参数是必需的：  
<table>
<tr><th>参数</th><th>描述</th></tr>
<tr><td>Id</td><td>为您要创建的事物类型提供标识。</td></tr>
<tr><td>name</td><td>为您要创建的事物类型提供名称。</td></tr>
<tr><td>schemaId</td><td>为组合模式资源创建的标识。</td></tr>
</table>

有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) 文档。

  

<!-- The following example shows how to use Python to create a thing type that is called *RoomType*.
```python
result = api.createThingType(thingType, "RoomType", "roomTypeSchemaId", "The Room Thing type")

```  -->

## 步骤 4：创建应用程序接口模式文件  
{: #crt_ai_schema_file}
在应用程序接口中，可以定义存储为事物状态的数据的结构。对于此场景，请创建用于定义温度和湿度属性的应用程序接口。将应用程序接口与事物类型 *RoomType* 相关联，方法是引用在创建应用程序接口资源时生成的该应用程序接口标识。  
以下示例显示了如何创建名为 *RoomType Schema* 的应用程序接口模式文件。
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
## 步骤 5：创建应用程序接口模式资源。  
{: #crt_ai_schema_resource}  
使用以下 API 上传您在先前步骤中为创建事物类型的应用程序接口模式资源而创建的应用程序接口模式文件：  
```
POST /schemas
```  
以下参数是必需的：  
<table>
<tr>
<th>参数</th><th>描述</th>
</tr>
<tr>
<td>name</td><td>为您要创建的应用程序接口模式提供名称。</td>
</tr>
<tr>
<td>schemaFile</td><td>到本地应用程序接口模式 JSON 文件的路径。</td>
</tr>
</table>  

有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas) 文档。

  

<!-- The following example shows how to use Python to create the thing type application interface schema resource:  
```python
roomSchemaFile = open(schemasDir + "room.json", "r");
roomSchema = roomSchemaFile.read();
roomSchemaFile.close();
"roomSchemaId", result = api.createSchema("Room Schema", "room.json", roomSchema)
```  -->

使用模式标识将应用程序接口模式资源添加到事物类型的应用程序接口。  

## 步骤 6：创建事物类型的应用程序接口。  
{: #crt_thing_ai}  
应用程序接口必须引用您在先前步骤中创建的应用程序接口模式资源。  
要创建应用程序接口，请使用以下 API：  
```
POST /applicationinterfaces
```  
以下参数是必需的：  
<table>
<tr>
<th>	参数</th><th>	描述</th>
</tr>
<tr>
<td>	name	</td><td>	为您要创建的应用程序接口提供名称。</td>
</tr>
<tr>
<td>	description	</td><td>	提供应用程序接口的描述。</td>
</tr>
<tr>
<td>	schemaId	</td><td>	到本地应用程序接口模式 JSON 文件的路径。</td>
</tr>
</table>  

有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Application_Interfaces) 文档。

  
使用在先前响应中返回的模式标识，向应用程序接口添加应用程序接口模式。  

<!-- The following example shows how to use Python to create an application interface:  
```python
"applicationInterfaceId", result = api.createApplicationInterface("IRoom", "roomSchemaId")
```  -->

使用应用程序接口标识向设备类型添加应用程序接口。此外，还将使用此标识将入站设备事件映射到由应用程序接口定义的属性。

  

## 步骤 7：向事物类型添加应用程序接口。  
{: #add_thing_ai}  
要向事物类型添加应用程序接口，请使用以下 API：  
```
POST /thing/types/{thingtypeId}/applicationinterfaces
```  
以下参数是必需的：  
<table>
<tr>
<th>	参数</th><th>	描述</th>
</tr>
<tr>
<td>	id	</td><td>	为事物类型创建的标识。</td>
</tr>
<tr>
<td>	name	</td><td>	为您要创建的应用程序接口提供名称。</td>
</tr>
<tr>
<td>	schemaId	</td><td>	为应用程序接口资源创建的标识。</td>
</tr>
<tr>
<td>	refs/schema	</td><td>	到应用程序接口资源的路径。通常是：/schemas/*schemaId*</td>
</tr>
</table>  

有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) 文档。

  
在此场景中，应用程序接口与事物类型 *RoomType* 相关联。

<!-- The following example shows how to use Python to add the thing application interface to the thing type *RoomType*:  
```python
result = api.addApplicationInterfaceToThingType(RoomType, "applicationInterfaceId", "roomSchemaId")
``` -->

## 步骤 8：定义映射
{: #define_Thing_type_mappings}

定义事物类型的映射，用于描述如何将来自聚合设备或事物的状态的属性映射到在事物类型应用程序接口上定义的属性。

要映射事件，请使用以下 API：  
```
POST /thing/types/{thingtypeId}/mappings
```  

以下参数是必需的：  
<table>
<tr>
<th>	参数</th><th>	描述</th>
</tr>
<tr>
<td>	applicationInterfaceId	</td><td>	为应用程序接口创建的标识。</td>
</tr>
<tr>
<td>	propertyMappings	</td><td>	有效的 JSON 结构，将为应用程序接口定义的属性映射到设备事件有效内容的属性。</td>
</tr>
</table>  

有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) 文档。



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

以下示例显示了样本 propertyMappings 参数条目：

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

*humiditySensor* 是在事物模式中定义的。“$event.humidity”是在应用程序接口模式中使用标识“58c135ea52faff0001678f06”定义的。*temperatureSensor* 是在事物模式中定义的。“$event.temperatureC”是在应用程序接口模式中使用标识“58c135e352faff0001198a89”定义的。

## 步骤 9：部署与事物类型关联的配置  
{: #deploy_Thing_config}   
部署与每种事物类型的事物状态更新相关的配置。此配置包括模式、应用程序接口和映射。

必须先部署事物类型配置，然后才能创建事物类型的实例。

要部署事物类型配置，请使用以下 API：

```
PATCH /thing/types/{thingtypeId}
```
有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types) 文档。

<!-- The following example shows how to use Python to deploy your configuration for thing type *Room*:

```python
result = api.deployThingTypeConfiguration(thingType)
``` -->

## 步骤 10：创建事物类型的实例
{: #create_Thing_instances}

事物是事物类型的实例。通过事物，您可以将某个设备或事物的一个或多个实例聚合成一个对象。

要创建事物，请使用以下 API：

```
POST /thing/types/{thingTypeId}/things
```

以下参数是必需的：  
<table>
<tr>
<th>	参数</th><th>	描述</th>
</tr>
<tr>
<td>	typeId	</td><td>		您早先创建的事物类型的标识。</td>
</tr>
<tr>
<td>	thingId	</td><td>	为您要创建的事物实例提供名称。</td>
</tr>
</table>

有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Things) 文档。



在此场景中，我们需要创建两个事物类型为 *RoomType* 的事物实例。其中一个事物实例名为 *meetingroom1*，另一个事物实例名为 *meetingroom2*。

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

创建的事物标识在 POST 方法的 URL 中使用，调用该方法时，可将温度事件添加到事物应用程序接口。

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

## 步骤 11：验证映射的设备事件是否已发布到应用程序接口  
{: #publish_event}  
发布已聚合到事物 *meetingroom1* 中的各个设备的下列事件：  
 - 在主题 `iot-2/evt/tevt/fmt/json` 上发布来自 *temperatureSensor1* 的温度事件  
 - 在主题 `iot-2/evt/hevt/fmt/json` 上发布来自 *humiditySensor1* 的湿度事件  
发布已聚合到事物 *meetingroom2* 中的各个设备的下列事件：  
 - 在主题 `iot-2/evt/tevt/fmt/json` 上发布来自 *temperatureSensor2* 的温度事件  
 - 在主题 `iot-2/evt/hevt/fmt/json` 上发布来自 *humiditySensor2* 的湿度事件  
有关从设备发布入站事件的信息，请参阅[应用程序的 MQTT 连接](../applications/mqtt.html#publishing_device_events)。  

## 步骤 12：检查事物状态是否已更改。  
{: #verify_Thing_state}  
要检查事物状态，请使用以下 API：  
```
GET /thing/types/{thingTypeId}/things/{thingId}/state/{applicationInterfaceId}
```  

以下参数是必需的：  
<table>
<tr>
<th>参数</th><th>	描述</th>
</tr>
<tr>
<td>thingtypeId	</td><td>事物类型标识</td>
</tr>
<tr>
<td>thingId	</td><td>	事物标识。</td>
</tr>
<tr>
<td>applicationInterfaceId</td><td>为应用程序接口创建的标识。</td>
</tr>
</table>  

有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) 文档。

  

<!-- The following example shows how to use Python to retrieve the current state of *meetingroom1* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom1", applicationInterfaceId)
```  
The following example shows how to use Python to retrieve the current state of *meetingroom2* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom2", applicationInterfaceId)
``` -->
