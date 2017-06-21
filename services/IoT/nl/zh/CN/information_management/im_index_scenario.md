---

copyright:
years: 2016, 2017
lastupdated: "2017-04-10"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 应用程序接口场景 1 (Beta)
{: #scenario}

使用以下信息创建一个场景：两个温度传感器将事件发布到 {{site.data.keyword.iot_short_notm}}。一个传感器以摄氏度为单位测量温度。另一个传感器以华氏度为单位测量温度。这两个读数都会映射到以摄氏度为单位的单个温度读数。这两个设备发布新的温度读数时，与设备状态关联的属性的值会更改。

## 先决条件

您必须具有 {{site.data.keyword.iot_short_notm}} 组织实例以及该组织的 API 密钥或令牌。有关 API 密钥和令牌的更多信息，请参阅[针对应用程序的 HTTP REST API](../applications/api.html#authentication)。

## 关于此任务

在此场景中，配置了两个设备。

一个设备名为 *TemperatureSensor1*。此设备将发布以摄氏度为单位测量的温度事件。温度事件会在主题 `iot-2/evt/tevt/fmt/json` 上发布，并具有以下示例有效内容：
```
{
  “t” : 34.5
}
```

**注：**事件标识为 *tevt*。向物理接口添加此类型的温度事件时，以及定义映射以用于将与此类型的入站事件关联的属性映射到应用程序接口中的属性时，此标识是必需的。在此场景中，应用程序接口中定义的属性名为 **temperature**。

另一个设备名为 *TemperatureSensor2*。此设备将发布以华氏度为单位测量的温度事件。温度事件会在主题 `iot-2/evt/tempevt/fmt/json` 上发布，并具有以下示例有效内容：
```
{
  “temp” : 72.55
}
```

**注：**事件标识为 *tempevt*。向物理接口添加此类型的温度事件时，以及定义映射以用于将与此类型的入站事件关联的属性映射到应用程序接口中的属性时，此标识是必需的。在此场景中，应用程序接口中定义的属性名为 **temperature**。

此外，还会配置应用程序接口。此应用程序接口表示此类型的设备的状态，结构如下：
```
{
  “temperature” : <current temperature value in Celsius>
  }
```
此配置表示您可以将应用程序配置为处理与 **temperature** 关联的值，而不是将应用程序配置为处理与 **t** 关联的值以及与 **temp** 关联的值（在该值转换为摄氏度后）。
![在 {{site.data.keyword.iot_short_notm}} 上温度传感器设备与应用程序之间的映射。](images/Information "在 {{site.data.keyword.iot_short_notm}} 上温度传感器设备与应用程序之间的映射")  

使用以下示例场景来设置您自己的接口环境。

## 根据需要添加设备类型和设备
{: #step14}

在此场景中，假定有两种设备类型和两个设备实例。设备实例 *TemperatureSensor1* 与设备类型 *EnvSensor1* 相关联。设备实例 *TemperatureSensor2* 与设备类型 *EnvSensor2* 相关联。

有关使用 REST API 来添加设备类型的信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types) 文档。

## 步骤 1：创建事件模式文件
{: #step1}

对于此场景，创建两个事件模式文件以定义每个入站温度事件的结构。

**重要信息：**对于已结构化的 [JSON ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://json-schema.org/){:new_window} 事件有效内容，请确保将每个嵌套级别正确地合并在 `"properties"` 条目中。例如，如果有效内容为 `{"d":{"t":<temp>}}`，那么可能会使用：
```
 "properties" : {
    "d" : {
      "properties" : {
        "t" : {
      "description" : "Temperature in degrees Celsius",
          "type" : "number",
          "minimum" : -273.15,
          "default" : 0.0
        }
      },
      "required" : ["t"]
    }
  },
  "required" : ["d"]
```

以下示例显示了如何创建名为 *tEventSchema.json* 的模式文件。此文件定义来自以摄氏度为单位测量温度的温度传感器的入站事件的结构：

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor1 tEvent Schema",
  "description" : “defines the structure of a temperature event in degrees Celsius",
  "properties" : {
    "t" : {
      "description" : "temperature in degrees Celsius",
      "type" : "number",
      "minimum" : -273.15,
      "default" : 0.0
    }
  },
  "required" : ["t"]
}
  ```
**提示：**使用“required”参数将一个或多个属性设为必需属性。设备消息中必须包含必需属性，Watson IoT Platform 才能使用设备数据更新设备状态。不会对不包含必需属性的消息进行处理。   

为事件类型创建事件模式资源时，将使用模式文件名 *tEventSchema*。

以下示例显示了如何创建名为 *tempEventSchema.json* 的模式文件。此文件定义来自以华氏度为单位测量温度的温度传感器的入站事件的结构：

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor2 tempEvent Schema",
  "description" : “defines the structure of a temperature event in degrees Fahrenheit",
  "properties" : {
    "temp" : {
      "description" : "temperature in degrees Fahrenheit",
      "type" : "number",
      "minimum" : −459.67,
      "default" : 0.0
    }
  },
  "required" : ["temp"]
}
  ```
为事件类型创建事件模式资源时，将使用模式文件名 *tempEventSchema*。   

## 步骤 2：为事件类型创建事件模式资源
{: #step2}

要创建事件模式资源，请使用以下 API：

```
POST /schemas
```

以下参数是必需的：  

参数	|	描述  
------	|	-----  
name	|	为您要创建的事件模式提供名称。  
schemaFile	|	到本地事件模式 JSON 文件的路径。  



有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas) 文档。



以下示例显示了如何使用 cURL 创建事件模式资源 *tEventSchema.json*：

```curl
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=tEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tEventSchema.json'
```

以下示例显示了对 POST 方法的响应：

```
{
  "name" : “tEventSchema",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "contentType" : "application/octet-stream",
  "updated" : "2016-12-06T14:38:52Z",
  "schemaFileName" : "tEventSchema.json",
  "created" : "2016-12-06T14:38:52Z",
  "id" : "5846cd7c6522050001db0e0d",
  "refs" : {
      "content" : "/schemas/5846cd7c6522050001db0e0d/content"
  },
  "schemaType" : "json-schema",
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
向事件类型添加事件模式时，需要在对 POST 方法的响应中返回的模式标识 *5846cd7c6522050001db0e0d*。

以下示例显示了如何使用 cURL 创建事件模式资源 *tempEventSchema.json*：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: multipart/form-data’ \
  --form name=tempEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tempEventSchema.json"'
```

以下示例显示了对 POST 方法的响应：

```
{
  "schemaType" : "json-schema",
  "schemaFileName" : "tempEventSchema.json",
  "updated" : "2016-12-06T14:44:51Z",
  "name" : "tempEventSchema",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "created" : "2016-12-06T14:44:51Z",
  "id" : "5846cee36522050001db0e0e",
  "refs" : {
      "content" : "/schemas/5846cee36522050001db0e0e/content"
  },
  "contentType" : "application/octet-stream",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```
向事件类型添加事件模式时，需要在对 POST 方法的响应中返回的模式标识 *5846cee36522050001db0e0e*。

## 步骤 3：创建引用事件模式的事件类型
{: #step3}

每种事件类型都会引用在先前示例中，使用在对用于创建事件模式资源的 POST 方法的响应中返回的模式标识创建的相关事件模式。

要创建事件类型，请使用以下 API：

```
POST /event/types
```

以下参数是必需的：  

参数	|	描述
------	|	-----
name	|	为您要创建的事件类型提供名称。
schemaId	|	为事件模式资源创建的标识。
有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types) 文档。



以下示例显示了如何使用 cURL 为以摄氏度为单位测量的温度事件创建事件类型：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d”}'
```

模式标识 *5846cd7c6522050001db0e0d* 用于向事件类型添加事件模式。此标识在对用于创建事件模式资源 *tEventSchema.json* 的 POST 方法的响应中返回。

以下示例显示了对 POST 方法的响应：

```
{
  "updated" : "2016-12-06T14:53:49Z",
  "schemaId" : "5846cd7c6522050001db0e0d",
  "refs" : {
    "schema" : "/schemas/5846cd7c6522050001db0e0d"
  },
  "name" : "tEvent",
  "created" : "2016-12-06T14:53:49Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846d0fd6522050001db0e0f",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

事件类型标识 *5846d0fd6522050001db0e0f* 在对用于向物理接口添加事件类型的 POST 方法的响应中返回。

以下示例显示了如何使用 cURL 为以华氏度为单位测量的温度事件创建事件类型：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tempEvent", "schemaId" : "5846cee36522050001db0e0e"}'
```
模式标识 *5846cee36522050001db0e0e* 用于向事件类型添加事件模式。此标识在对用于创建事件模式资源 *tempEventSchema.json* 的 POST 方法的响应中返回。以下示例显示了对 POST 方法的响应：

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "schemaId" : "5846cee36522050001db0e0e",
  "created" : "2016-12-06T15:00:20Z",
  "id" : "5846d2846522050001db0e10",
  "updated" : "2016-12-06T15:00:20Z",
  "name" : “tempEvent”,
  "refs" : {
    "schema" : "/schemas/5846cee36522050001db0e0e"
  },
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
事件类型标识 *5846d2846522050001db0e10* 在对用于向物理接口添加事件类型的 POST 方法的响应中返回。

## 步骤 4：创建物理接口
{: #step7}

要创建物理接口，请使用以下 API：

```
POST /physicalinterfaces
```

以下参数是必需的：  

参数	|	描述
------	|	-----
name	|	为您要创建的物理接口提供名称。
有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces) 文档。


在此场景中，需要两个物理接口，分别用于每种事件类型。

以下示例显示了如何使用 cURL 创建第一个物理接口：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 1"}'
```

以下示例显示了对 POST 方法的响应：

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1a/events"
  },
  "id" : "5847d1df6522050001db0e1a",
  "name" : "Env sensor physical interface 1",
  "created" : "2016-12-07T09:09:51Z",
  "updated" : "2016-12-07T09:09:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

在响应中返回的物理接口标识 *5847d1df6522050001db0e1a* 将在为了向物理接口添加以摄氏度为单位测量的温度事件而调用的 POST 方法的 URL 中使用。

以下示例显示了如何使用 cURL 创建第二个物理接口：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 2"}'
```

以下示例显示了对 POST 方法的响应：

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1b/events"
  },
  "id" : "5847d1df6522050001db0e1b",
  "name" : "Env sensor physical interface 2",
  "created" : "2016-12-07T09:19:51Z",
  "updated" : "2016-12-07T09:19:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

在响应中返回的物理接口标识 *5847d1df6522050001db0e1b* 将在为了向物理接口添加以华氏度为单位测量的温度事件而调用的 POST 方法的 URL 中使用。   

## 步骤 5：向物理接口添加事件类型
{: #step8}

要向物理接口添加事件类型，请使用以下 API：

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```

以下参数是必需的：  

参数	|	描述
------	|	-----
eventId	|	输入来自设备事件有效内容的事件名称。
eventTypeId	|	为事件类型创建的标识。
有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces) 文档。


在此场景中，将向指定的物理接口添加以下事件类型：
- 摄氏温度事件 *tevt* 将使用来自主题的 *eventId* 以及通过创建事件模式资源而生成的 *eventTypeId*，添加到标识为 *5847d1df6522050001db0e1a* 的物理接口。
- 华氏温度事件 *tempevt* 将使用来自主题的 *eventId* 以及通过创建事件模式资源而生成的 *eventTypeId*，添加到标识为 *5847d1df6522050001db0e1b* 的物理接口。


以下示例显示了如何使用 cURL 向标识为 *5847d1df6522050001db0e1a* 的物理接口添加温度事件 *tevt*：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : “tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
```

以下示例显示了对 POST 方法的响应：

```
{
  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
}
```

以下示例显示了如何使用 cURL 向标识为 *5847d1df6522050001db0e1b* 的物理接口添加温度事件 *tempevt*：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1b/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tempevt", "eventTypeId" : "5846d2846522050001db0e10"}'
```

以下示例显示了对 POST 方法的响应：

```
{
  "eventTypeId" : "5846d2846522050001db0e10",
  "eventId" : “tempevt"
}
```

## 步骤 6：更新设备类型以连接物理接口
{: #step9}

要更新设备类型，请使用以下 API：

```
PUT /device/types/{typeId}
```

以下参数是必需的：  

参数	|	描述
------	|	-----
physicalInterfaceId	|	为物理接口创建的标识。
有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文档。


在此场景中，设备类型 *EnvSensor1* 更新为连接到物理接口 *5847d1df6522050001db0e1a*，并且设备类型 *EnvSensor2* 更新为连接到物理接口 *5847d1df6522050001db0e1b*。

以下示例显示了如何使用 cURL 更新设备类型 *EnvSensor1*：

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a”}’
```

以下示例显示了对 POST 方法的响应：

```
{
  "deviceInfo" : {},
  "physicalInterfaceId" : "5847d1df6522050001db0e1a",
  "updatedDateTime" : "2016-12-07T09:49:52+00:00",
  "refs" : {
    "mappings" : "/device/types/EnvSensor1/mappings",
    "applicationInterfaces" : "/device/types/EnvSensor1/applicationinterfaces",
    "physicalInterface" : "/physicalinterfaces/5847d1df6522050001db0e1a"
   },
  "id" : "EnvironmentSensor",
  "description" : "an environment sensor",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
添加物理接口和应用程序接口时，设备标识 *EnvSensor1* 是必需的。

以下示例显示了如何使用 cURL 更新设备类型 *EnvSensor2*：

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b”}’
```

以下示例显示了对 POST 方法的响应：

```
{
  "deviceInfo" : {},
  "physicalInterfaceId" : "5847d1df6522050001db0e1b",
  "updatedDateTime" : "2016-12-07T09:59:52+00:00",
  "refs" : {
    "mappings" : "/device/types/EnvSensor2/mappings",
    "applicationInterfaces" : "/device/types/EnvSensor2/applicationinterfaces",
    "physicalInterface" : "/physicalinterfaces/5847d1df6522050001db0e1b"
   },
  "id" : "EnvironmentSensor",
  "description" : "an environment sensor",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
添加物理接口和应用程序接口时，设备标识 *EnvSensor2* 是必需的。



## 步骤 7：创建应用程序接口模式文件
{: #step4}

以下示例显示了如何创建名为 *envSensor.json* 的应用程序接口模式文件。

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
    "type" : "object",
    "title" : "Environment Sensor Schema",
    "description" : "Schema to represent a canonical environment sensor device",
    "properties" : {
        "temperature" : {
            "description" : "temperature in degrees Celsius",
            "type" : "number",
            "minimum" : -273.15,
            "default" : 0.0
        }
    },
    "required" : ["temperature"]
}
```

## 步骤 8：创建应用程序接口模式资源
{: #step5}

要创建应用程序接口模式资源，请使用以下 API：

```
POST /schemas
```

以下参数是必需的：  

参数	|	描述
------	|	-----
name	|	为您要创建的应用程序接口模式提供名称。
schemaFile	|	到本地应用程序接口模式 JSON 文件的路径。
有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas) 文档。



以下示例显示了如何使用 cURL 创建应用程序接口模式：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=temperatureEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/envSensor.json"'
```

以下示例显示了对 POST 方法的响应：

```
{
  "created" : "2016-12-06T16:51:14Z",
  "name" : "temperatureEventSchema",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "updated" : "2016-12-06T16:51:14Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "schemaType" : "json-schema",
  "contentType" : "application/octet-stream",
  "schemaFileName" : "envSensor.json",
  "refs" : {
    "content" : "/schemas/5846ec826522050001db0e11/content"
  },
  "id" : "5846ec826522050001db0e11"
}
```
使用在对 POST 方法的响应中返回的模式标识 *5846ec826522050001db0e11*，向应用程序接口添加应用程序接口模式。

## 步骤 9：创建引用应用程序接口模式的应用程序接口
{: #step6}

要创建应用程序接口，请使用以下 API：

```
POST /applicationinterfaces
```

以下参数是必需的：  

参数	|	描述
------	|	-----
name	|	为您要创建的应用程序接口提供名称。
schemaId	|	为应用程序接口模式资源创建的标识。
有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Application_Interfaces) 文档。



在此场景中，使用在先前响应中返回的模式标识 *5846ec826522050001db0e11*，向应用程序接口添加应用程序接口模式。

以下示例显示了如何使用 cURL 创建应用程序接口：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "environment sensor interface", "schemaId" : "5846ec826522050001db0e11"}'
```

以下示例显示了对 POST 方法的响应：

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "schemaId" : "5846ec826522050001db0e11",
  "created" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846ed076522050001db0e12",
  "updated" : "2016-12-06T16:53:27Z",
  "name" : "environment sensor interface"
}
```
在此场景中，使用在对 POST 方法的响应中返回的应用程序接口标识 *5846ed076522050001db0e12*，向设备类型添加应用程序接口。此外，还将使用此标识将入站设备事件映射到由应用程序接口定义的属性。

## 步骤 10：向设备类型添加应用程序接口
{: #step10}

要向设备类型添加应用程序接口，请使用以下 API：

```
POST /device/types/{typeId}/applicationinterfaces
```

以下参数是必需的：  

参数	|	描述
------	|	-----
id	|	为应用程序接口创建的标识。
name	|	设备类型的名称。
schemaId	|	为应用程序接口资源创建的标识。
refs/schema	|	到应用程序接口资源的路径。通常是：/schemas/*schemaId*


有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文档。


在此场景中，应用程序接口与设备类型 *EnvSensor1* 和设备类型 *EnvSensor2* 相关联。

以下示例显示了如何使用 cURL 向设备类型 *EnvSensor1* 添加引用应用程序模式标识 *5846ec826522050001db0e11* 的应用程序接口 *5846ed076522050001db0e12*：

```
curl --request POST \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/applicationinterfaces \
--header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
--header 'content-type: application/json' \
--data '{"createdBy" : "a-8x7nmj-9iqt56kfil", \
          "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11", "created" : "2016-12-06T16:53:27Z", \
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface”
        }'
```

以下示例显示了对 POST 方法的响应：

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "environment sensor interface",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

以下示例显示了如何使用 cURL 向设备类型 *EnvSensor2* 添加与应用程序模式标识 *5846ec826522050001db0e11* 关联的应用程序接口 *5846ed076522050001db0e12*：

```
curl --request POST \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/applicationinterfaces \
--header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
--header 'content-type: application/json' \
--data '{"createdBy" : "a-8x7nmj-9iqt56kfil", \
          "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11", "created" : "2016-12-06T16:53:27Z", \
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface”
        }'
```


以下示例显示了对 POST 方法的响应：

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "environment sensor interface",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

## 步骤 11：定义映射以用于将入站事件中的属性映射到应用程序接口中的属性
{: #step11}

要映射事件，请使用以下 API：

```
POST /device/types/{typeId}/mappings
```

以下参数是必需的：  

参数	|	描述
------	|	-----
applicationInterfaceId	|	为应用程序接口创建的标识。
propertyMappings	|	有效的 JSON 结构，将为应用程序接口定义的属性映射到设备事件有效内容的属性。请参阅以下示例。有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文档。


在此场景中，将针对设备类型 *EnvSensor1* 定义映射以用于将入站事件 *tevt* 中的 **t** 属性映射到应用程序接口上的 **temperature** 属性。此外，还将针对设备类型 *EnvSensor1* 定义映射以用于将入站事件 *tempevt* 中的 **temp** 属性映射到应用程序接口上的 **temperature** 属性。

以下示例显示了如何使用 cURL 向设备类型 *EnvSensor1* 添加映射：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/mappings \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"applicationInterfaceId" : "5846ed076522050001db0e12","propertyMappings" : {
              "tevt" : {
                  "temperature" : "$event.t"
              }
            }
          }'
```

**重要信息：**对于已结构化的 [JSON ![外部链接图标](../../../icons/launch-glyph.svg "外部链接图标")](http://json-schema.org/){:new_window} 事件有效内容，请确保 $event.*property* 条目正确匹配您属性的 JSON 结构。例如，如果有效内容为 `{"d":{"t":<temp>}}`，请使用 `$event.d.t`

指定在对用于创建应用程序接口和设备类型 *EnvSensor1* 的 POST 方法的响应中返回的应用程序接口标识 *5846ed076522050001db0e12*。

以下示例显示了对 POST 方法的响应：

```
{
  "propertyMappings" : {
      "tevt" : {
       "temperature" : "$event.t"
    }
  },
  "applicationInterfaceId" : "5846ed076522050001db0e12"
}
```
以下示例显示了如何使用 cURL 向设备类型 *EnvSensor2* 添加映射：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/mappings \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"applicationInterfaceId" : "5846ed076522050001db0e12","propertyMappings" : {
              "tempevt" : {
                  "temperature" : "($event.temp - 32) / 1.8"
              }
            }
          }'
```

指定在对用于创建应用程序接口和设备类型 *EnvSensor2* 的 POST 方法的响应中返回的应用程序接口标识 *5846ed076522050001db0e12*。将应用转换，使值从华氏测量单位转换为摄氏测量单位。


以下示例显示了对 POST 方法的响应：

```
{
  "propertyMappings" : {
    "tempevt" : {
      "temperature" : "($event.temp - 32) / 1.8"
    }
  },
  "applicationInterfaceId" : "5846ed076522050001db0e12"
}
```

## 步骤 12：部署配置
{: #step15}

部署与每种设备类型的设备状态更新相关的配置。此配置包括模式、事件类型、物理接口、应用程序接口和映射。

要部署设备类型配置，请使用以下 API：

```
PATCH /device/types/{typeId}
```

以下参数是必需的：  

参数	|	描述
------	|	-----
typeId	|	设备类型标识

有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文档。


在此场景中，需要部署两种设备类型的配置。

以下示例显示了如何使用 cURL 部署设备类型 *EnvSensor1* 的配置：

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy-configuration"
          }'
```

以下示例显示了对 PATCH 方法的响应：

```
{
 "message": "CUDRS0520I: State update configuration for device type 'EnvSensor1' has been successfully submitted for deployment",
  "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor1"]
  },
 "failures": []
}
```

以下示例显示了如何使用 cURL 部署设备类型 *EnvSensor2* 的配置：

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
          }'
```

以下示例显示了对 PATCH 方法的响应：

```
{
 "message": "CUDRS0520I: State update configuration for device type 'EnvSensor2' has been successfully submitted for deployment",
  "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor2"]
  },
 "failures": []
}
```

## 步骤 13：发布入站设备事件
{: #step12}

在主题 `iot-2/evt/tevt/fmt/json` 上发布来自 *TemperatureSensor1* 的温度事件，以及在主题 `iot-2/evt/tempevt/fmt/json` 上发布来自 *TemperatureSensor2* 的温度事件。

有关从设备发布入站事件的信息，请参阅[应用程序的 MQTT 连接](../applications/mqtt.html#publishing_device_events)。


## 步骤 14：检查设备状态是否已更改
{: #step13}

要检查设备状态，请使用以下 API：
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```

以下参数是必需的：  

参数	|	描述
------	|	-----
typeId	|	设备类型标识
deviceId	|	设备的标识。
applicationInterfaceId	|	为应用程序接口创建的标识。
有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文档。


以下示例显示了如何使用 cURL 通过引用所创建应用程序接口的标识来检索 *TemperatureSensor1* 的当前状态：
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/devices/TemperatureSensor1/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

应用程序接口标识 *5846ed076522050001db0e12* 会在 GET 方法中使用。此标识在对用于创建应用程序接口的 POST 方法的响应中返回。以下示例显示了对 GET 方法的响应：
```
{
  "temperature":34.5
}
```
以下示例显示了如何使用 cURL 通过引用所创建应用程序接口的标识来检索 *TemperatureSensor2* 的当前状态：
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/devices/TemperatureSensor2/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

应用程序接口标识 *5846ed076522050001db0e12* 会在 GET 方法中使用。此标识在对用于创建应用程序接口的 POST 方法的响应中返回。以下示例显示了对 GET 方法的响应：
```
{
  "temperature":22.5
}
```
请注意，返回的温度读数以摄氏度而不是华氏度为单位。

您的应用程序可以处理此规范化数据，而无需用于识别或转换不同温标的配置。


**注：**要检索最新的已部署配置，请使用以下 API：

```
GET /device/types/<typeId>/deployedconfiguration
```
使用此 API 可检索 PATCH 部署操作上次成功完成的已部署配置。要检索已更改但未部署的资源的配置，请使用与您要查询的资源关联的常规 GET 方法。
有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文档。


以下示例显示了如何使用 cURL 检索最新部署的配置：
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/deployedconfiguration \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```
以下示例显示了对 GET 方法的响应：

```
{
    "schemas": [
        {
          "name" : “tEventSchema",
          "createdBy" : "a-8x7nmj-9iqt56kfil",
          "contentType" : "application/octet-stream",
          "updated" : "2016-12-06T14:38:52Z",
          "schemaFileName" : "tEventSchema.json",
          "created" : "2016-12-06T14:38:52Z",
          "id" : "5846cd7c6522050001db0e0d",
          "refs" : {
              "content" : "/schemas/5846cd7c6522050001db0e0d/content"
  },
          "schemaType" : "json-schema",
          "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "content": "ew0KICAiJHNjaGVtYSI6ICJodHRwOi8vanNvbi1zY2hlbWEub3JnL2RyYWZ0LTA0L3NjaGVtYSMiLA0KICAidHlwZSIgOiAib2JqZWN0IiwNCiAgInRpdGxlIiA6ICJFbnZTZW5zb3IxIHRFdmVudCBTY2hlbWEiLA0KICAiZGVzY3JpcHRpb24iIDog4oCcZGVmaW5lcyB0aGUgc3RydWN0dXJlIG9mIGEgdGVtcGVyYXR1cmUgZXZlbnQgaW4gZGVncmVlcyBDZWxzaXVzIiwNCiAgInByb3BlcnRpZXMiIDogew0KICAgICJ0IiA6IHsNCiAgICAgICJkZXNjcmlwdGlvbiIgOiAidGVtcGVyYXR1cmUgaW4gZGVncmVlcyBDZWxzaXVzIiwNCiAgICAgICJ0eXBlIiA6ICJudW1iZXIiLA0KICAgICAgIm1pbmltdW0iIDogLTI3My4xNSwNCiAgICAgICJkZWZhdWx0IiA6IDAuMA0KICAgIH0NCiAgfSwNCiAgInJlcXVpcmVkIiA6IFsidCJdDQp9"
        }
    ],
    "eventTypes": [
        {
          "updated" : "2016-12-06T14:53:49Z",
  "schemaId" : "5846cd7c6522050001db0e0d",
  "refs" : {
    "schema" : "/schemas/5846cd7c6522050001db0e0d"
  },
  "name" : "tEvent",
  "created" : "2016-12-06T14:53:49Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846d0fd6522050001db0e0f",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
},
        {
          "createdBy" : "a-8x7nmj-9iqt56kfil",
          "schemaId" : "5846cee36522050001db0e0e",
          "created" : "2016-12-06T15:00:20Z",
          "id" : "5846d2846522050001db0e10",
          "updated" : "2016-12-06T15:00:20Z",
          "name" : “tempEvent”,
          "refs" : {
            "schema" : "/schemas/5846cee36522050001db0e0e"
  },
          "updatedBy" : "a-8x7nmj-9iqt56kfil"
        }
    ],
    "physicalInterface": {
          "events":[
            {
                  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
},
            {
                "eventTypeId" : "5846d2846522050001db0e10",
                "eventId" : “tempevt"
            }
          ],
        "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "refs" : {
            "events" : "/physicalinterfaces/5847d1df6522050001db0e1a/events"
  },
  "id" : "5847d1df6522050001db0e1a",
  "name" : "Env sensor physical interface 1",
  "created" : "2016-12-07T09:09:51Z",
  "updated" : "2016-12-07T09:09:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
},
    "applicationInterfaces": [
        {
          "createdBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11",
          "created" : "2016-12-06T16:53:27Z",
          "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "id" : "5846ed076522050001db0e12",
          "updated" : "2016-12-06T16:53:27Z",
          "name" : "environment sensor interface"
        }
    ],
    "mappings": [
        {
          "propertyMappings" : {
      "tevt" : {
                  "temperature" : "$event.t"
            },
            "tempevt" : {
                  "temperature" : "($event.temp - 32) / 1.8"
    }
  },
          "applicationInterfaceId" : "5846ed076522050001db0e12"
        }
    ]
}
```
