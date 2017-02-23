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

# 使用介面來對映裝置資料（測試版）
{: #im_index}

使用 {{site.data.keyword.iot_full}} 的介面對映特性，來組織和整合送入及送出裝置資料。
{:shortdesc}

**重要事項：**介面對映特性目前只能當作「測試版」特性使用。在最終版本之前，「測試版」更新可能會包含與現行版本不相容的變更。除非是最終發行版本，否則強烈建議不要在正式作業應用程式中使用「測試版」特性。若要接收其他資訊，以及提供對此「測試版」的意見，請[登錄 IM Beta 程式](https://www.ibm.com/software/support/trial/cst/forms/nomination.wss?id=7050)，讓我們知道您的想法。

## 概觀
{: #overview}

您可以使用介面對映特性來開發應用程式的介面。您可能有不同類型、品牌或型號的裝置或感應器要連接至 {{site.data.keyword.iot_short_notm}}，而且這些裝置可能會以不同的格式來發佈資料。使用介面對映特性來正規化送入資料，並將應用程式與特定裝置連接方式的複雜性取消連結，以簡化應用程式。

例如，您有兩個溫度感應器。一個感應器測量攝氏度數的溫度，一個感應器則測量華氏度數的溫度。

![{{site.data.keyword.iot_short_notm}} 上溫度感應器裝置與應用程式之間的對映。](images/Information "{{site.data.keyword.iot_short_notm}} 上溫度感應器裝置與應用程式之間的對映")

溫度感應器 1 會將 `{ "t" : 34.5 }` 的溫度讀數發佈至 {{site.data.keyword.iot_short_notm}}。這是攝氏值的溫度讀數。溫度感應器 2 會將 `{ "temp" : 72.55 }` 的溫度讀數發佈至 {{site.data.keyword.iot_short_notm}}。這是不同類型的溫度感應器，其讀數為華氏值。溫度讀數會以個別事件形式發佈至 {{site.data.keyword.iot_short_notm}}。

使用介面對映特性，即可將這些讀數正規化成一致形式來進行處理。您不需要撰寫應用程式，即可瞭解或轉換不同的溫標。應用程式會接收單一正規化視圖，而且可以連接至 **temperature**，而非連接至 **t** 和 **temp**。

## 裝置與應用程式之間的資料流程
{: #mapping}

下列流程圖顯示如何在介面對映特性中使用不同的資源：

![{{site.data.keyword.iot_short_notm}} 上裝置與應用程式之間的流程。](images/Information "{{site.data.keyword.iot_short_notm}} 上裝置與應用程式之間的流程")

下圖說明如何在此流程中使用綱目：

![{{site.data.keyword.iot_short_notm}} 上裝置與應用程式之間的流程。](images/Information "{{site.data.keyword.iot_short_notm}} 上裝置與應用程式之間的流程")

JSON 綱目是用來定義與驗證送入事件格式及[裝置狀態](#key_concepts)。如需這些綱目的相關資訊，請參閱[綱目](#resources)。

## 主要概念
{: #key_concepts}

介面對映特性藉由新增實體介面資源及應用程式介面資源，更適當地控制流過 {{site.data.keyword.iot_short_notm}} 的資料，來擴充[裝置類型](#resources)的現行概念。

下圖使用[資源](#resources)來說明 {{site.data.keyword.iot_short_notm}} 上裝置與應用程式之間的邏輯對映：

![{{site.data.keyword.iot_short_notm}} 上裝置與應用程式之間的邏輯對映。](images/im_mapping.svg "{{site.data.keyword.iot_short_notm}} 上裝置與應用程式之間的邏輯對映")

介面對映是指裝置狀態的概念。裝置狀態包含應用程式介面所定義的一組內容。這些內容的最新值儲存在 {{site.data.keyword.iot_short_notm}} 中，而且使用 HTTP API 即可在要求時供應用程式使用。

若要處理來自入埠事件的資料，並將入埠事件中的內容對映至應用程式介面上的內容，則必須配置下列資訊：

- 一個以上入埠事件的結構。事件綱目定義此資訊。每一個事件綱目都定義一個入埠事件的結構，並且與一種事件類型相關聯。實體介面可將一種以上的事件類型群組在一起。

    入埠裝置事件內所含資料的結構及格式是透過 JSON 綱目格式的事件綱目檔所定義。您可以使用 POST 方法建立具名綱目資源，以將事件綱目檔上傳至 {{site.data.keyword.iot_short_notm}}。若為測試版，所有入埠事件都必須為 JSON 格式。

- 所需裝置狀態的結構。應用程式介面綱目定義此資訊。

    裝置狀態會呈現資料結構，以及呈現配置應用程式所接收的資料，而資料來自裝置。裝置狀態中所儲存的內容值會進行更新，以回應入埠裝置事件。使用 HTTP API，即可在要求時將最新裝置狀態值提供給應用程式。

- 如何將入埠事件對映至偏好裝置狀態的相關資訊。對映定義此資訊。

    若要將入埠事件內容中所含的資料對映至應用程式介面上的適當內容，則需要建立對映。此對映說明如何更新特定應用程式介面所定義的內容，以回應來自裝置的入埠事件。


## 資源
{: #resources}

您可以使用 REST API 來管理先前圖表中所說明的資源。如需 REST API 的相關資訊，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html) 文件。

資源                        | 說明       
------------- | ------------- | -------------  
綱目                         | JSON 綱目是用來定義從裝置發佈至 {{site.data.keyword.iot_short_notm}} 之入埠事件的結構，以及所需的裝置狀態。如需「JSON 綱目」的相關資訊，請參閱 [JSON 綱目](http://json-schema.org/)。在介面對映中，參照兩個 JSON 綱目：事件綱目及應用程式介面綱目。事件綱目是用來定義裝置發佈至 {{site.data.keyword.iot_short_notm}} 之事件的結構。應用程式介面綱目是供應用程式介面所參照，並且用來定義儲存在 {{site.data.keyword.iot_short_notm}} 之[裝置狀態](#key_concepts)的結構。
事件類型                         | 您必須在組織內建立事件類型，讓 {{site.data.keyword.iot_short_notm}} 可以處理特定事件內所含的資料。所有事件類型都必須參照事件綱目。若為測試版，所有入埠事件都必須為 JSON 格式。   
實體介面                         | 實體介面可以與一種以上的事件類型相關聯，並定義與裝置類型相關聯的事件類型。  
裝置類型                         | 每個連接至 Watson IoT Platform 的裝置都會與一種裝置類型相關聯。裝置類型是共用性質或行為的裝置群組。在介面對映中，裝置類型會擴充成包括裝置的實體介面以及可用來擷取裝置狀態的應用程式介面。一種裝置類型可以配置多個應用程式介面。如需裝置類型的相關資訊，請參閱[裝置機型](../reference/device_model.html#id_and_device_types)中的「ID 及裝置類型」小節。
應用程式介面                         | 應用程式介面必須參照應用程式介面綱目。在應用程式介面內，您可以定義儲存為裝置狀態之資料的結構。裝置狀態會呈現資料結構，以及呈現配置應用程式所接收的資料，而資料來自裝置。至少一個應用程式介面必須先與裝置類型相關聯，才能定義任何對映。
對映                         | 對映可定義如何將與入埠事件相關聯的內容對映至特定應用程式介面上所定義的內容。對映必須指定套用它的應用程式介面 ID，而且該應用程式介面必須與將新增該對映的裝置類型相關聯。


## 高階工作流程
{: #workflow}



### 關於此作業

使用下列步驟，可協助您使用介面來配置開始對映裝置資料所需的資源。

如需 API 的詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html) 文件。
如需每一個步驟的其他詳細資訊，請參閱[範例情境](#scenario)，或使用鏈結直接移至範例情境內的特定步驟。

### 配置環境，開始使用介面來對映裝置資料

1.  必要的話，新增「裝置類型」及「裝置」

  1. 搭配使用 REST API POST 方法與下列 URI，以建立裝置類型：
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types
      ```
  2.  必要的話，新增裝置。  
如需新增裝置類型及裝置的相關資訊，請參閱[連接裝置](../iotplatform_task.html#devices)。

2. 建立實體介面

  1. [建立事件綱目檔](#step1)。事件綱目檔是定義入埠事件結構及格式的本端 .JSON 檔案。

  2. 搭配使用 REST API POST 方法與下列 URI，以[建立事件類型的事件綱目資源](#step2)：
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
      ```  

  3. 搭配使用 REST API POST 方法與下列 URI，以[建立參照事件綱目的事件類型](#step3)：
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/event/types
      ```
      將事件類型新增至事件綱目，方法是使用用來建立事件綱目資源的 POST 方法回應中所傳回的綱目 ID。

  4. 搭配使用 REST API POST 方法與下列 URI，以[建立實體介面](#step7)：
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces
        ```

   5. 搭配使用 REST API POST 方法與下列 URI，以[將事件類型新增至實體介面](#step8)：
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/{physicalInterfaceId}/events
        ```

       將事件類型新增至實體介面，方法是使用主題中的 *eventId* 以及用來建立事件類型的 POST 方法回應中所傳回的事件類型 ID *eventTypeId*。       

3. 將實體介面新增至裝置類型       

      搭配使用 REST API PUT 方法與下列 URI，以[更新裝置類型以連接實體介面](#step9)：
     ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
     ```

4. 建立應用程式介面

  1. [建立應用程式介面綱目檔](#step4)。應用程式介面綱目檔是定義裝置狀態的本端 .JSON 檔案。

  2. 搭配使用 REST API POST 方法與下列 URI，以[建立應用程式介面綱目資源](#step5)：
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
        ```     

  3. 搭配使用 REST API POST 方法與下列 URI，以[建立參照應用程式介面綱目的應用程式介面](#step6)：
         ```
         https://**orgId**.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces
         ```  

        應用程式介面參照應用程式介面綱目，方法是使用用來建立應用程式介面綱目資源的 POST 方法回應中所傳回的綱目 ID。

  4. 搭配使用 REST API POST 方法與下列 URI，以[將應用程式介面新增至裝置類型](#step10)：
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/types/{typeId}/applicationinterfaces
        ```

        將應用程式介面新增至裝置類型，方法是使用用來建立應用程式介面的 POST 方法的回應。

5. 定義裝置類型的對映

  搭配使用 REST API POST 方法與下列 URI，以[定義對映，將入埠事件中的內容對映至應用程式介面中的內容](#step11)：       
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/mappings/{applicationInterfaceId}
      ```

6. 部署與裝置類型相關聯的配置

  搭配使用 REST API PATCH 方法與下列 URI，以[部署配置](#step15)至 {{site.data.keyword.iot_short_notm}}：
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
      ```

7. 驗證對映的裝置事件已發佈至應用程式介面

  1. [發佈入埠裝置事件](#step12)。

  2. 搭配使用 REST API GET 方法與下列 URI，以[確認裝置狀態已變更](#step13)：
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
        ```

## 範例情境
{: #scenario}

使用下列資訊，以建立兩個溫度感應器將事件發佈至 {{site.data.keyword.iot_short_notm}} 的情境。一個感應器測量攝氏度數的溫度。另一個感應器則測量華氏度數的溫度。這些讀數都會對映成攝氏度數的單一溫度讀數。這些裝置發佈新的溫度讀數時，與裝置狀態相關聯之內容的值就會變更。

### 必要條件

您必須有 {{site.data.keyword.iot_short_notm}} 組織實例以及該組織的 API 金鑰或記號。如需 API 金鑰及記號的相關資訊，請參閱[應用程式的 HTTP REST API](../applications/api.html#authentication)。

### 關於此情境

在此情境下，會配置兩個裝置。

一個裝置稱為 *TemperatureSensor1*。此裝置會發佈以攝氏度數測量的溫度事件。溫度事件發佈於主題 `iot-2/evt/tevt/fmt/json`，並且具有下列範例有效負載：
```
{
  "t" : 34.5
}
```

**附註：**事件 ID 是 *tevt*。將這類型的溫度事件新增至實體介面時，以及定義對映以將與這類型入埠事件相關聯的內容對映至應用程式介面中的內容時，需要此 ID。在此情境下，應用程式介面中所定義的內容稱為 **temperature**。

另一個裝置稱為 *TemperatureSensor2*。此裝置會發佈以華氏度數測量的溫度事件。溫度事件發佈於主題 `iot-2/evt/tempevt/fmt/json`，並且具有下列範例有效負載：
```
{
  "temp" : 72.55
}
```

**附註：**事件 ID 是 *tempevt*。將這類型的溫度事件新增至實體介面時，以及定義對映以將與這類型入埠事件相關聯的內容對映至應用程式介面中的內容時，需要此 ID。在此情境下，應用程式介面中所定義的內容稱為 **temperature**。

也會配置應用程式介面。此應用程式介面以下列結構呈現這類型裝置的狀態：
```
{
  "temperature" : <current temperature value in Celsius>
  }
```
此配置表示您可以配置應用程式來處理與 **temperature** 相關聯的值，而不是配置應用程式來處理與 **t** 相關聯的值，以及在將與 **temp** 相關聯的值轉換成攝氏度數之後處理該值。

## 步驟

使用下列資訊，以使用介面來配置範例情境。

### 必要的話，新增「裝置類型」及「裝置」
{: #step14}

在此情境下，假設兩種裝置類型及兩個裝置實例。裝置實例 *TemperatureSensor1* 與裝置類型 *EnvSensor1* 相關聯。裝置實例 *TemperatureSensor2* 與裝置類型 *EnvSensor2* 相關聯。

如需使用 REST API 來新增裝置類型的相關資訊，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types) 文件。

### 建立事件綱目檔
{: #step1}

在此情境中，建立兩個事件綱目檔，以定義每一個入埠溫度事件的結構。

下列範例顯示如何建立稱為 *tEventSchema.json* 的綱目檔。此檔案定義以攝氏度數測量溫度的溫度感應器的入埠事件結構：

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

建立事件類型的事件綱目資源時，會使用綱目檔名稱 *tEventSchema*。

下列範例顯示如何建立稱為 *tempEventSchema.json* 的綱目檔。此檔案定義以華氏度數測量溫度的溫度感應器的入埠事件結構：

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
建立事件類型的事件綱目資源時，會使用綱目檔名稱 *tempEventSchema*。   

### 建立事件類型的事件綱目資源
{: #step2}

若要建立事件綱目資源，請使用下列 API：

```
POST /schemas
```
如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas) 文件。

下列範例顯示如何使用 cURL 來建立事件綱目資源 *tEventSchema.json*：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=tEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tEventSchema.json'
```

下列範例顯示 POST 方法的回應：

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
將事件綱目新增至事件類型時，需要 POST 方法回應中所傳回的綱目 ID *5846cd7c6522050001db0e0d*。

下列範例顯示如何使用 cURL 來建立事件綱目資源 *tempEventSchema.json*：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: multipart/form-data’ \
  --form name=tempEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tempEventSchema.json"'
```

下列範例顯示 POST 方法的回應：

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
將事件綱目新增至事件類型時，需要 POST 方法回應中所傳回的綱目 ID *5846cee36522050001db0e0e*。

### 建立參照事件綱目的事件類型
{: #step3}

每一種事件類型都會參照前一個範例中所建立的相關事件綱目，方法是使用用來建立事件綱目資源的 POST 方法回應中所傳回的綱目 ID。

若要建立事件類型，請使用下列 API：

```
POST /event/types
```

如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types) 文件。


下列範例顯示如何使用 cURL 來建立以攝氏度數測量的溫度事件的事件類型：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d"}'
```

綱目 ID *5846cd7c6522050001db0e0d* 是用來將事件綱目新增至事件類型。此 ID 是在用來建立事件綱目資源 *tEventSchema.json* 的 POST 方法回應中所傳回。

下列範例顯示 POST 方法的回應：

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

POST 方法回應中所傳回的事件類型 ID *5846d0fd6522050001db0e0f* 是用來將事件類型新增至實體介面。

下列範例顯示如何使用 cURL 來建立以華氏度數測量的溫度事件的事件類型：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tempEvent", "schemaId" : "5846cee36522050001db0e0e"}'
```
綱目 ID *5846cee36522050001db0e0e* 是用來將事件綱目新增至事件類型。此 ID 是在用來建立事件綱目資源 *tempEventSchema.json* 的 POST 方法回應中所傳回。

下列範例顯示 POST 方法的回應：

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
POST 方法回應中所傳回的事件類型 ID *5846d2846522050001db0e10* 是用來將事件類型新增至實體介面。

### 建立實體介面
{: #step7}

若要建立實體介面，請使用下列 API：

```
POST /physicalinterfaces
```
如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces) 文件。

在此情境下，我們需要兩個實體介面 - 一種事件類型一個。

下列範例顯示如何使用 cURL 來建立第一個實體介面：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 1"}'
```

下列範例顯示 POST 方法的回應：

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

回應中所傳回的實體介面 ID *5847d1df6522050001db0e1a* 是用於呼叫以將以攝氏度數測量的溫度事件新增至實體介面的 POST 方法的 URL 中。

下列範例顯示如何使用 cURL 來建立第二個實體介面：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 2"}'
```

下列範例顯示 POST 方法的回應：

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

回應中所傳回的實體介面 ID *5847d1df6522050001db0e1b* 是用於呼叫以將以華氏度數測量的溫度事件新增至實體介面的 POST 方法的 URL 中。   

### 將事件類型新增至實體介面
{: #step8}

若要將事件類型新增至實體介面，請使用下列 API：

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```
如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces) 文件。

在此情境下，下列事件類型會新增至指定的實體介面：
- 攝氏溫度事件 *tevt* 會新增至 ID 為 *5847d1df6522050001db0e1a* 的實體介面，方法是使用主題中的 *eventId* 以及建立事件綱目資源的 *eventTypeId*。
- 華氏溫度事件 *tempevt* 會新增至 ID 為 *5847d1df6522050001db0e1b* 的實體介面，方法是使用主題中的 *eventId* 以及建立事件綱目資源的 *eventTypeId*。


下列範例顯示如何使用 cURL 以將溫度事件 *tevt* 新增至 ID 為 *5847d1df6522050001db0e1a* 的實體介面：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
```

下列範例顯示 POST 方法的回應：

```
{
  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
}
```

下列範例顯示如何使用 cURL 以將溫度事件 *tempevt* 新增至 ID 為 *5847d1df6522050001db0e1b* 的實體介面：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1b/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tempevt", "eventTypeId" : "5846d2846522050001db0e10"}'
```

下列範例顯示 POST 方法的回應：

```
{
  "eventTypeId" : "5846d2846522050001db0e10",
  "eventId" : "tempevt"
}
```

### 更新裝置類型以連接實體介面
{: #step9}

若要更新裝置類型，請使用下列 API：

```
PUT /device/types/{typeId}
```

如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文件。

在此情境下，會更新裝置類型 *EnvSensor1* 以連接至實體介面 *5847d1df6522050001db0e1a*，以及更新裝置類型 *EnvSensor2* 以連接至實體介面 *5847d1df6522050001db0e1b*。

下列範例顯示如何使用 cURL 來更新裝置類型 *EnvSensor1*：

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a"}’
```

下列範例顯示 POST 方法的回應：

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
新增實體介面及應用程式介面時，需要裝置 ID *EnvSensor1*。

下列範例顯示如何使用 cURL 來更新裝置類型 *EnvSensor2*：

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b"}’
```

下列範例顯示 POST 方法的回應：

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
新增實體介面及應用程式介面時，需要裝置 ID *EnvSensor2*。



### 建立應用程式介面綱目檔
{: #step4}

下列範例顯示如何建立稱為 *envSensor.json* 的應用程式介面綱目檔。

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

### 建立應用程式介面綱目資源
{: #step5}

若要建立應用程式介面綱目資源，請使用下列 API：

```
POST /schemas
```
如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas) 文件。

下列範例顯示如何使用 cURL 來建立應用程式介面綱目：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=temperatureEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/envSensor.json"'
```

下列範例顯示 POST 方法的回應：

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
使用 POST 方法回應中所傳回的綱目 ID *5846ec826522050001db0e11*，以將應用程式介面綱目新增至應用程式介面。

### 建立參照應用程式介面綱目的應用程式介面
{: #step6}

若要建立應用程式介面，請使用下列 API：

```
POST /applicationinterfaces
```
如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Application_Interfaces) 文件。

在此情境下，使用前一個回應中所傳回的綱目 ID *5846ec826522050001db0e11*，以將應用程式介面綱目新增至應用程式介面。

下列範例顯示如何使用 cURL 來建立應用程式介面：

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "environment sensor interface", "schemaId" : "5846ec826522050001db0e11"}'
```

下列範例顯示 POST 方法的回應：

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
在此情境下，使用 POST 方法回應中所傳回的應用程式介面 ID *5846ed076522050001db0e12*，以將應用程式介面新增至裝置類型。您也可以使用此 ID，以將入埠裝置事件對映至應用程式介面所定義的內容。

### 將應用程式介面新增至裝置類型
{: #step10}

若要將應用程式介面新增至裝置類型，請使用下列 API：

```
POST /device/types/{typeId}/applicationinterfaces
```
如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文件。

在此情境下，應用程式介面會與裝置類型 *EnvSensor1* 和裝置類型 *EnvSensor2* 相關聯。

下列範例顯示如何使用 cURL 以將參照應用程式綱目 ID *5846ec826522050001db0e11* 的應用程式介面 *5846ed076522050001db0e12* 新增至裝置類型 *EnvSensor1*：

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

下列範例顯示 POST 方法的回應：

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

下列範例顯示如何使用 cURL 以將與應用程式綱目 ID *5846ec826522050001db0e11* 相關聯的應用程式介面 *5846ed076522050001db0e12* 新增至裝置類型 *EnvSensor2*：

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


下列範例顯示 POST 方法的回應：

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

### 定義對映，將入埠事件中的內容對映至應用程式介面中的內容
{: #step11}

若要對映事件，請使用下列 API：

```
POST /device/types/{typeId}/mappings
```
如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文件。

在此情境下，我們定義裝置類型 *EnvSensor1* 的對映，以將入埠事件 *tevt* 中的 **t** 內容對映至應用程式介面上的 **temperature** 內容。我們還會定義裝置類型 *EnvSensor2* 的對映，以將入埠事件 *tempevt* 中的 **temp** 內容對映至應用程式介面上的 **temperature** 內容。

下列範例顯示如何使用 cURL 以將對映新增至裝置類型 *EnvSensor1*：

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

指定用來建立應用程式介面及裝置類型 *EnvSensor1* 的 POST 方法回應中所傳回的應用程式介面 ID *5846ed076522050001db0e12*。

下列範例顯示 POST 方法的回應：

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
下列範例顯示如何使用 cURL 以將對映新增至裝置類型 *EnvSensor2*：

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

指定用來建立應用程式介面及裝置類型 *EnvSensor2* 的 POST 方法回應中所傳回的應用程式介面 ID *5846ed076522050001db0e12*。
套用轉換，以將值從華氏度數測量變更為攝氏度數測量。


下列範例顯示 POST 方法的回應：

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

部署與每一種裝置類型的裝置狀態更新相關的配置。此配置包括您的綱目、事件類型、實體介面、應用程式介面及對映。

若要部署裝置類型配置，請使用下列 API：

```
PATCH /device/types/{typeId}
```
如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文件。

在此情境下，我們需要部署兩種裝置類型的配置。

下列範例顯示如何使用 cURL 來部署裝置類型 *EnvSensor1* 的配置：

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
          }'
```

下列範例顯示 PATCH 方法的回應：

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

下列範例顯示如何使用 cURL 來部署裝置類型 *EnvSensor2* 的配置：

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
          }'
```

下列範例顯示 PATCH 方法的回應：

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

### 發佈入埠裝置事件
{: #step12}

將來自 *TemperatureSensor1* 的溫度事件發佈於主題 `iot-2/evt/tevt/fmt/json`，並將來自 *TemperatureSensor2* 的溫度事件發佈於主題 `iot-2/evt/tempevt/fmt/json`。

如需發佈來自裝置的入埠事件的相關資訊，請參閱[應用程式的 MQTT 連線功能](../applications/mqtt.html#publishing_device_events)。


### 確認裝置狀態已變更
{: #step13}

若要檢查裝置狀態，請使用下列 API：
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```
如需詳細資料，請參閱 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 文件。

下列範例顯示如何使用 cURL 以參照所建立應用程式介面的 ID 來擷取 *TemperatureSensor1* 的現行狀態：
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/devices/TemperatureSensor1/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

應用程式介面 ID *5846ed076522050001db0e12* 用於 GET 方法中。此 ID 是在用來建立應用程式介面的 POST 方法回應中所傳回。
下列範例顯示 GET 方法的回應：
```
{
  "temperature":34.5
}
```
下列範例顯示如何使用 cURL 以參照所建立應用程式介面的 ID 來擷取 *TemperatureSensor2* 的現行狀態：
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/devices/TemperatureSensor2/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

應用程式介面 ID *5846ed076522050001db0e12* 用於 GET 方法中。此 ID 是在用來建立應用程式介面的 POST 方法回應中所傳回。
下列範例顯示 GET 方法的回應：
```
{
  "temperature":22.5
}
```
請注意，傳回的溫度讀數是攝氏度數，而非華氏度數。

您的應用程式可以處理此正規化資料，而且不需要配置即可瞭解或轉換不同的溫標。
