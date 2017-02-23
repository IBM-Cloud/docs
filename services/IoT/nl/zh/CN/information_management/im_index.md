---

copyright:
years: 2016, 2017
lastupdated: "2017-01-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 使用接口映射设备数据 (Beta)
{: #im_index}

使用 {{site.data.keyword.iot_full}} 的接口映射功能可组织和集成入局和出局设备数据。
{:shortdesc}

**重要信息：**目前，接口映射功能只作为 Beta 功能提供。在推出最终发行版之前，Beta 更新可能会包含与当前版本不兼容的更改。因此强烈建议在推出最终发行版之前，不要将 Beta 功能用于生产应用程序。要接收其他信息并提供对此 Beta 的反馈，请[注册 IM Beta 程序](https://www.ibm.com/software/support/trial/cst/forms/nomination.wss?id=7050)，并告诉我们您的想法。

## 概述
{: #overview}

您可以使用接口映射功能来为应用程序开发接口。您可能有不同类型、品牌或型号的设备或传感器要连接到 {{site.data.keyword.iot_short_notm}}，并且这些设备可能会发布不同格式的数据。使用接口映射功能可规范化入局数据，并通过去除应用程序中特定设备连接方式的复杂性来简化应用程序。

例如，您可能有两个温度传感器。一个传感器以摄氏度为单位测量温度，另一个传感器以华氏度为单位测量温度。

![在 {{site.data.keyword.iot_short_notm}} 上温度传感器设备与应用程序之间的映射。](images/Information "在 {{site.data.keyword.iot_short_notm}} 上温度传感器设备与应用程序之间的映射")

温度传感器 1 将温度读数 `{ "t" : 34.5 }` 发布到 {{site.data.keyword.iot_short_notm}}。此温度读数值的单位为摄氏度。温度传感器 2 将温度读数 `{ "temp" : 72.55 }` 发布到 {{site.data.keyword.iot_short_notm}}。这是另一种类型的温度传感器，读数值的单位为华氏度。温度读数会作为单独的事件发布到 {{site.data.keyword.iot_short_notm}}。

通过使用接口映射功能，可以将这些读数规范化为统一格式进行处理。您无需将应用程序编写为能够识别或转换不同的温标。应用程序会收到单一的规范化视图，并可以连接到 **temperature**，而不是连接到 **t** 或 **temp**。

## 设备与应用程序之间的数据流
{: #mapping}

以下流程图显示了如何使用接口映射功能中的不同资源：

![在 {{site.data.keyword.iot_short_notm}} 上设备与应用程序之间的流程。](images/Information "在 {{site.data.keyword.iot_short_notm}} 上设备与应用程序之间的流程")

下图说明了在此流程中如何使用模式：

![在 {{site.data.keyword.iot_short_notm}} 上设备与应用程序之间的流程。](images/Information "在 {{site.data.keyword.iot_short_notm}} 上设备与应用程序之间的流程")

JSON 模式用于定义和验证入局事件以及[设备状态](#key_concepts)的格式。有关这些模式的更多信息，请参阅[模式](#resources)。

## 关键概念
{: #key_concepts}

接口映射功能通过添加物理接口资源和应用程序接口资源来更好地控制流经 {{site.data.keyword.iot_short_notm}} 的数据，从而扩展了[设备类型](#resources)的当前概念。

下图使用[资源](#resources)说明了在 {{site.data.keyword.iot_short_notm}} 上设备与应用程序之间的逻辑映射：

![在 {{site.data.keyword.iot_short_notm}} 上设备与应用程序之间的逻辑映射。](images/im_mapping.svg "在 {{site.data.keyword.iot_short_notm}} 上设备与应用程序之间的逻辑映射")

接口映射是指设备状态的概念。设备状态由应用程序接口所定义的一组属性组成。这些属性最近的值会存储在 {{site.data.keyword.iot_short_notm}} 中，并在请求时使用 HTTP API 提供给应用程序。

要处理来自入站事件的数据，并将入站事件中的属性映射到应用程序接口上的属性，必须配置以下信息：

- 一个或多个入站事件的结构。事件模式会定义此信息。每个事件模式会定义一个入站事件的结构，并与一种事件类型相关联。物理接口会对一种或多种事件类型分组。

    入站设备事件内包含的数据的结构和格式由 JSON 模式格式的事件模式文件进行定义。可以通过使用 POST 方法创建指定的模式资源，从而将事件模式文件上传到 {{site.data.keyword.iot_short_notm}}。对于 Beta，所有入站事件必须为 JSON 格式。

- 所需设备状态的结构。应用程序接口模式会定义此信息。

    设备状态是应用程序配置为要从设备接收作为数据的数据结构和数据的表示。设备状态中存储的属性值会根据入站设备事件进行更新。最新的设备状态值会在请求时使用 HTTP API 提供给应用程序。

- 有关如何将入站事件映射到首选设备状态的信息。映射会定义此信息。

    要将入站事件的属性中包含的数据映射到应用程序接口上的相应属性，您需要创建映射。映射描述如何根据来自设备的入站事件，更新特定应用程序接口所定义的属性。


## 资源
{: #resources}

您可以使用 REST API 来管理上面各图中所示的资源。有关 REST API 的信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html) 文档。

资源                        | 描述       
------------- | ------------- | -------------  
模式                         | JSON 模式用于定义从设备发布到 {{site.data.keyword.iot_short_notm}} 的入站事件的结构以及所需的设备状态。有关 JSON 模式的更多信息，请参阅 [JSON 模式](http://json-schema.org/)。在接口映射中，引用了两种 JSON 模式 - 事件模式和应用程序接口模式。事件模式用于定义由设备发布到 {{site.data.keyword.iot_short_notm}} 的事件的结构。应用程序接口模式由应用程序接口引用，并用于定义 {{site.data.keyword.iot_short_notm}} 上存储的[设备状态](#key_concepts)的结构。
事件类型                         | 必须在组织内创建某种事件类型，以使 {{site.data.keyword.iot_short_notm}} 能够处理特定事件内包含的数据。所有事件类型都必须引用一种事件模式。对于 Beta，所有入站事件必须为 JSON 格式。   
物理接口                         | 物理接口可以与一种或多种事件类型相关联，并定义哪些事件类型与某种设备类型相关联。  
设备类型                         | 每个连接到 Watson IoT Platform 的设备都必须与一种设备类型相关联。设备类型为共享特征或行为的设备组。在接口映射中，设备类型扩展为包含设备的物理接口以及可用于检索设备状态的应用程序接口。一种设备类型可以配置有多个应用程序接口。有关设备类型的更多信息，请参阅[设备模型](../reference/device_model.html#id_and_device_types)中的“标识和设备类型”部分。
应用程序接口                         | 应用程序接口必须引用应用程序接口模式。在应用程序接口内，可以定义存储为设备状态的数据的结构。设备状态是应用程序配置为要从设备接收作为数据的数据结构和数据的表示。必须至少将一个应用程序接口与一种设备类型相关联后，才能定义任何映射。
映射                         | 映射会定义与入站事件关联的属性如何映射到在特定应用程序接口上定义的属性。映射必须指定其应用于的应用程序接口标识，并且该应用程序接口必须与该映射所添加到的设备类型相关联。


## 高级别工作流
{: #workflow}



### 关于此任务

使用以下步骤可帮助您配置开始使用接口来映射设备数据所需的资源。

有关 API 的详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html) 文档。
有关每个步骤的更详细信息，请参阅[示例场景](#scenario)或使用链接直接转至示例场景内的特定步骤。

### 配置环境以开始使用接口来映射设备数据

1.  根据需要添加设备类型和设备

  1. 使用 REST API POST 方法及以下 URI 创建设备类型：
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types
      ```
  2.  根据需要添加设备。  
有关添加设备类型和设备的更多信息，请参阅[连接设备](../iotplatform_task.html#devices)

2. 创建物理接口

  1. [创建事件模式文件](#step1)。事件模式文件是本地 .JSON 文件，用于定义入站事件的结构和格式。

  2. 使用 REST API POST 方法及以下 URI [为事件类型创建事件模式资源](#step2)：
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
      ```  

  3. 使用 REST API POST 方法及以下 URI [创建引用事件模式的事件类型](#step3)：
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/event/types
      ```
      使用在对用于创建事件模式资源的 POST 方法的响应中返回的模式标识，向事件模式添加事件类型。
  4. 使用 REST API POST 方法及以下 URI [创建物理接口](#step7)：
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces
        ```

   5. 使用 REST API POST 方法及以下 URI [向物理接口添加事件类型](#step8)：
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/{physicalInterfaceId}/events
        ```

       使用主题中的 *eventId* 以及在对用于创建事件类型的 POST 方法的响应中返回的事件类型标识 *eventTypeId*，向物理接口添加事件类型。
       

3. 向设备类型添加物理接口       

      使用 REST API PUT 方法及以下 URI [更新用于连接物理接口的设备类型](#step9)：
     ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
     ```

4. 创建应用程序接口

  1. [创建应用程序接口模式文件](#step4)。应用程序接口模式文件是本地 .JSON 文件，用于定义设备状态。

  2. 使用 REST API POST 方法及以下 URI [创建应用程序接口模式资源](#step5)：
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
        ```     

  3. 使用 REST API POST 方法及以下 URI [创建引用应用程序接口模式的应用程序接口](#step6)：
         ```
         https://**orgId**.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces
         ```  

        应用程序接口使用在对用于创建应用程序接口模式资源的 POST 方法的响应中返回的模式标识，引用应用程序接口模式。


  4. 使用 REST API POST 方法及以下 URI [向设备类型添加应用程序接口](#step10)：
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/types/{typeId}/applicationinterfaces
        ```

        使用对用于创建应用程序接口的 POST 方法的响应，向设备类型添加应用程序接口。


5. 定义设备类型的映射

  使用 REST API POST 方法及以下 URI [定义用于将入站事件中的属性映射到应用程序接口中属性的映射](#step11)：       
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/mappings/{applicationInterfaceId}
      ```

6. 部署与设备类型关联的配置

  使用 REST API PATCH 方法及以下 URI 向 {{site.data.keyword.iot_short_notm}} [部署配置](#step15)：
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
      ```

7. 验证映射的设备事件是否已发布到应用程序接口

  1. [发布入站设备事件](#step12)。

  2. 使用 REST API GET 方法及以下 URI [检查设备状态是否已更改](#step13)：
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
        ```

## 示例场景
{: #scenario}

使用以下信息创建一个场景：两个温度传感器将事件发布到 {{site.data.keyword.iot_short_notm}}。一个传感器以摄氏度为单位测量温度。另一个传感器以华氏度为单位测量温度。这两个读数都会映射到以摄氏度为单位的单个温度读数。这两个设备发布新的温度读数时，与设备状态关联的属性的值会更改。

### 先决条件

您必须具有 {{site.data.keyword.iot_short_notm}} 组织实例以及该组织的 API 密钥或令牌。有关 API 密钥和令牌的更多信息，请参阅[针对应用程序的 HTTP REST API](../applications/api.html#authentication)。

### 关于此场景

在此场景中，配置了两个设备。

一个设备名为 *TemperatureSensor1*。此设备将发布以摄氏度为单位测量的温度事件。温度事件会在主题 `iot-2/evt/tevt/fmt/json` 上发布，并具有以下示例有效内容：
```
{
  "t" : 34.5
}
```

**注：**事件标识为 *tevt*。向物理接口添加此类型的温度事件时，以及定义映射以用于将与此类型的入站事件关联的属性映射到应用程序接口中的属性时，此标识是必需的。在此场景中，应用程序接口中定义的属性名为 **temperature**。

另一个设备名为 *TemperatureSensor2*。此设备将发布以华氏度为单位测量的温度事件。温度事件会在主题 `iot-2/evt/tempevt/fmt/json` 上发布，并具有以下示例有效内容：
```
{
  "temp" : 72.55
}
```

**注：**事件标识为 *tempevt*。向物理接口添加此类型的温度事件时，以及定义映射以用于将与此类型的入站事件关联的属性映射到应用程序接口中的属性时，此标识是必需的。在此场景中，应用程序接口中定义的属性名为 **temperature**。

此外，还会配置应用程序接口。此应用程序接口表示此类型的设备的状态，结构如下：
```
{
  "temperature" : <current temperature value in Celsius>
  }
```
此配置表示您可以将应用程序配置为处理与 **temperature** 关联的值，而不是将应用程序配置为处理与 **t** 关联的值以及与 **temp** 关联的值（在该值转换为摄氏度后）。
## 步骤

使用以下信息可通过接口配置示例场景。

### 根据需要添加设备类型和设备
{: #step14}

在此场景中，假定有两种设备类型和两个设备实例。设备实例 *TemperatureSensor1* 与设备类型 *EnvSensor1* 相关联。设备实例 *TemperatureSensor2* 与设备类型 *EnvSensor2* 相关联。

有关使用 REST API 来添加设备类型的信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types) 文档。

### 创建事件模式文件
{: #step1}

对于此场景，创建两个事件模式文件以定义每个入站温度事件的结构。

以下示例显示了如何创建名为 *tEventSchema.json* 的模式文件。此文件定义来自以摄氏度为单位测量温度的温度传感器的入站事件的结构：

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor1 tEvent Schema",
  "description" : "defines the structure of a temperature event in degrees Celsius",
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

为事件类型创建事件模式资源时，将使用模式文件名 *tEventSchema*。

以下示例显示了如何创建名为 *tempEventSchema.json* 的模式文件。此文件定义来自以华氏度为单位测量温度的温度传感器的入站事件的结构：

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor2 tempEvent Schema",
  "description" : "defines the structure of a temperature event in degrees Fahrenheit",
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

### 为事件类型创建事件模式资源
{: #step2}

要创建事件模式资源，请使用以下 API：

```
POST /schemas
```
有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas) 文档。

以下示例显示了如何使用 cURL 创建事件模式资源 *tEventSchema.json*：

```
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
  "name" : "tEventSchema",
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

### 创建引用事件模式的事件类型
{: #step3}

每种事件类型都会引用在先前示例中，使用在对用于创建事件模式资源的 POST 方法的响应中返回的模式标识创建的相关事件模式。

要创建事件类型，请使用以下 API：

```
POST /event/types
```

有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types) 文档。



以下示例显示了如何使用 cURL 为以摄氏度为单位测量的温度事件创建事件类型：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d"}'
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
  "name" : "tempEvent",
  "refs" : {
    "schema" : "/schemas/5846cee36522050001db0e0e"
  },
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
事件类型标识 *5846d2846522050001db0e10* 在对用于向物理接口添加事件类型的 POST 方法的响应中返回。

### 创建物理接口
{: #step7}

要创建物理接口，请使用以下 API：

```
POST /physicalinterfaces
```
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

### 向物理接口添加事件类型
{: #step8}

要向物理接口添加事件类型，请使用以下 API：

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```
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
  --data '{"eventId" : "tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
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
  "eventId" : "tempevt"
}
```

### 更新用于连接物理接口的设备类型
{: #step9}

要更新设备类型，请使用以下 API：

```
PUT /device/types/{typeId}
```

有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文档。


在此场景中，设备类型 *EnvSensor1* 更新为连接到物理接口 *5847d1df6522050001db0e1a*，并且设备类型 *EnvSensor2* 更新为连接到物理接口 *5847d1df6522050001db0e1b*。

以下示例显示了如何使用 cURL 更新设备类型 *EnvSensor1*：

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a"}’
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
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b"}’
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



### 创建应用程序接口模式文件
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

### 创建应用程序接口模式资源
{: #step5}

要创建应用程序接口模式资源，请使用以下 API：

```
POST /schemas
```
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

### 创建引用应用程序接口模式的应用程序接口
{: #step6}

要创建应用程序接口，请使用以下 API：

```
POST /applicationinterfaces
```
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

### 向设备类型添加应用程序接口
{: #step10}

要向设备类型添加应用程序接口，请使用以下 API：

```
POST /device/types/{typeId}/applicationinterfaces
```
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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
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

### 定义映射以用于将入站事件中的属性映射到应用程序接口中的属性
{: #step11}

要映射事件，请使用以下 API：

```
POST /device/types/{typeId}/mappings
```
有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文档。

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

### 部署配置
{: #step15}

部署与每种设备类型的设备状态更新相关的配置。此配置包括模式、事件类型、物理接口、应用程序接口和映射。

要部署设备类型配置，请使用以下 API：

```
PATCH /device/types/{typeId}
```
有关更多详细信息，请参阅 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文档。

在此场景中，需要部署两种设备类型的配置。

以下示例显示了如何使用 cURL 部署设备类型 *EnvSensor1* 的配置：

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
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

### 发布入站设备事件
{: #step12}

在主题 `iot-2/evt/tevt/fmt/json` 上发布来自 *TemperatureSensor1* 的温度事件，以及在主题 `iot-2/evt/tempevt/fmt/json` 上发布来自 *TemperatureSensor2* 的温度事件。

有关从设备发布入站事件的信息，请参阅[应用程序的 MQTT 连接](../applications/mqtt.html#publishing_device_events)。


### 检查设备状态是否已更改
{: #step13}

要检查设备状态，请使用以下 API：
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```
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
