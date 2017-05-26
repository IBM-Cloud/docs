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

# 애플리케이션 인터페이스 시나리오 2(베타)
{: #scenario}

애플리케이션 인터페이스를 사용하면 애플리케이션이 디바이스 또는 사물이 구성된 방법을 알아야 할 필요가 없습니다. 예를 들어, 하나의 디바이스를 사용하여 룸의 온도를 측정하거나 여러 디바이스의 평균 측정값을 취합하여 룸 온도를 계산할 수 있습니다. 애플리케이션은 룸의 상태에 대한 정보를 요구하며, 이 가운데 하나의 컴포넌트는 온도 특성입니다. 애플리케이션이 수신한 온도 값을 계산하는 방법은 중요하지 않습니다. 

이 시나리오에서 온도 센서와 습도 센서는 두 미팅 룸에서 수집된 환경 데이터를 공개합니다. 온도 및 습도 센서 데이터는 두 디바이스 유형 애플리케이션 인터페이스에 개별적으로 맵핑됩니다(온도계 디바이스 유형에 대해 하나와 습도계 디바이스 유형에 대해 하나). 그리고 두 개의 룸 사물 인스턴스 *meetingroom1* 및 *meetingroom2*와 함께 *RoomType*이라고 하는 사물 유형이 작성됩니다. 

이 시나리오에서는 온도계 및 습도계 애플리케이션 인터페이스가 포함된 구성을 설정한 후에 적합한 환경 센서를 각각의 룸 인스턴스에 맵핑합니다(예: *temperatureSensor1* 및 *humiditySensor1*이 *meetingroom1*에 맵핑됨). 

## 전제조건
{: #pre_req}

이 시나리오는 앞의 [애플리케이션 인터페이스 시나리오 1](im_index_scenario) 위에서 빌드됩니다. 

계속하기 전에 다음을 확인하십시오. 
- 해당 조직에 대해 동일한 {{site.data.keyword.iot_short_notm}} 조직 인스턴스 및  API 키 또는 토큰을 사용합니다. API 키와 토큰에 대한 자세한 정보는 [애플리케이션용 HTTP REST API](../applications/api.html#authentication)를 참조하십시오. 
- 두 개의 애플리케이션 인터페이스(온도 센서에 대해 하나와 습도 센서에 대해 하나)를 작성했습니다. 온도 센서의 애플리케이션 인터페이스 구성에 대한 정보는 [디바이스 유형 애플리케이션 인터페이스 시나리오](../information_management/im_index_scenario)를 참조하십시오. 

## 이 태스크에 관한 정보
{: #about}

{{site.data.keyword.iot_short_notm}}에서 하나의 사물은 여러 디바이스와 사물로 구성될 수 있습니다. 사물 유형은 사물의 인스턴스가 작성되는 방법을 정의합니다. 애플리케이션 인터페이스는 사물 유형과
연관될 수 있습니다. 이 연관은 사물 유형 인스턴스에 대해 생성된 상태의 구조를 정의합니다. 맵핑을 사용하면 집계된 디바이스와 사물의 특성이 사물 상태의 특성에
맵핑되는 방법을 정의할 수 있습니다. 

이 시나리오에서는 두 개의 온도 센서와 두 개의 습도 센서가 이벤트를 {{site.data.keyword.iot_short_notm}}에 공개합니다. 하나의 온도 센서와 하나의 습도 센서는 사무실 블록의 미팅 룸 1에 있습니다. 다른 온도 및 습도 센서는 미팅 룸 2에 있습니다. 

![온도 및 습도 사물과 {{site.data.keyword.iot_short_notm}}의 애플리케이션 간의 맵핑](images/Information "한 룸의 여러 환경 센서 및 {{site.data.keyword.iot_short_notm}}의 애플리케이션 간의 맵핑")

*RoomType*이라고 하는 사물 유형은 룸의 인스턴스가 작성되는 방법을 정의하는 데 사용됩니다. 애플리케이션 인터페이스는 *RoomType*과 연관되며 온도와 습도를 모두 보여주는 단일 측정값으로 인바운드 이벤트가 맵핑됨을 정의합니다. 이 단일 측정값은 사물 상태입니다. 맵핑을 사용하면 온도 및 습도 센서의 특성이 이 사물 상태에 맵핑되는 방법을 정의할 수 있습니다. 새 측정값이 이러한 센서에 의해 공개되면 사물 상태와 연관된 특성의 값이 변경됩니다. 

다음과 같은 네 개의 디바이스가 포함됩니다. 

디바이스/유형 | 이벤트 | 이벤트 페이로드/특성
------------- |  ------------- | -------------
*temperatureSensor1*/온도계(meetingroom1) | `iot-2/evt/`*`tevt`*`/fmt/json` | `{ “t” : 34.5 }`/ **temperature1**
*temperatureSensor2*/온도계(meetingroom2) | `iot-2/evt/`*`tempevt`*`/fmt/json` | `{ “temp” : 34.5 }`/ **temperature2**  
*humiditySensor1*/습도계(meetingroom1) | `iot-2/evt/`*`hevt`*`/fmt/json` | `{  “h” : "75%" }`/ **humidity1**
*humiditySensor2*/습도계(meetingroom2) |`iot-2/evt/`*`humevt`*`/fmt/json` | `{  “hum” : "75%"}`/ **humidity2**

사물 유형 애플리케이션 인터페이스는 다음과 같은 구조로 사물 상태를 표시합니다. 
```
{
  “temperature” : <current temperature value in Celsius>
  "humidity" : <current humidity value>
  }
```

<!--
The code that is used in this example is available in the updated {{site.data.keyword.iot_short_notm}} [[Python library ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-python){: new_window} in GitHub, in the **thingDataTransform** sample.
-->  

다음 예제 시나리오를 사용하여 자체 인터페이스 환경을 설정할 수 있습니다.   

## 필요하면 디바이스 유형 및 디바이스 추가  
{: #add_device}  
이 시나리오에서는 두 개의 디바이스 유형과 네 개의 디바이스 인스턴스가 사용됩니다. 디바이스 인스턴스 *temperatureSensor1* 및 *temperatureSensor2*는 디바이스 유형 *온도계*와 연관되어 있습니다. 디바이스 인스턴스 *humiditySensor1* 및 *humiditySensor2*는 디바이스 유형 *습도계*와 연관되어 있습니다. 

REST API를 사용한 디바이스 유형 추가에 대한 정보는 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofThings.ibmcloud.com/swagger/v0002.html#!/Device_Types) 문서를 참조하십시오.   

## 1단계: 구성 스키마 파일 작성.   
{: #crt_composition_file}  
각 온도 및 습도 디바이스 유형에 대해 디바이스 애플리케이션 인터페이스 ID를 참조하는 구성 스키마 파일을 작성하십시오.   

다음 예제는 *룸 유형 스키마*라고 하는 구성 스키마 파일을 작성하는 방법을 보여줍니다.   
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
**팁:** “필수” 매개변수를 사용하여 하나 이상의 특성을 필수로 표시할 수 있습니다. Watson IoT Platform이 디바이스 데이터로 디바이스 상태를 업데이트할 수 있도록 필수 특성은 디바이스 메시지에 포함되어야 합니다. 필수 특성이 포함되지 않은 메시지는 처리되지 않습니다.    
**참고:** 사물 유형 스키마 파일을 작성할 때 생성된 스키마 ID는 사물 유형을 작성할 때 지정되어야 합니다.   

## 2단계: 구성 스키마 리소스 작성.   
{: #crt_composition_resource}  

이전 단계에서 생성된 사물 유형 스키마 파일을 업로드하여 스키마 리소스를 작성하십시오.   
다음 API를 사용하여 사물 유형 스키마 파일을 업로드하십시오.   
```
POST /schemas
```  
필수 매개변수는 다음과 같습니다.   
<table>
<tr>
<th>	매개변수 </th><th>	설명 </th>
</tr>
<tr>
<td>	name	</td><td>	작성 중인 구성 스키마의 이름을 제공합니다. </td>
</tr>
<tr>
<td>	schemaFile	</td><td>	로컬 구성 스키마 JSON 파일의 경로입니다. </td>
</tr>
</table>

세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas) 문서를 참조하십시오.   

<!-- The following example shows how to use Python to create the thing type schema resource:  
```python
roomTypeSchemaFile = open(schemasDir + "roomType.json", "r");
roomTypeSchema = roomTypeSchemaFile.read();
roomTypeSchemaFile.close();
"roomTypeSchemaId", result = api.createSchema("Room Type Schema", "roomType.json", roomTypeSchema)
```  -->

## 3단계: 사물 유형 작성   
{: #crt_thing_type}  

사물 유형은 사물 인스턴스를 모델링하는 데 사용됩니다. 사물 인스턴스를 작성하려면 우선 사물 유형이 조직에서 작성되어야 합니다. 이 시나리오의 경우에는 하나의 사물 유형을 작성합니다.   
사물 유형과 연관된 스키마는 사물의 인스턴스를 작성하기 위해 공동 집계되는 오브젝트의 유형을 정의합니다. 사물 유형은 이전 단계에서 작성된 사물 유형 스키마 리소스를 참조해야 합니다.   
다음 API를 사용하여 사물 유형을 작성하십시오. 
```
POST /thing/types
```
필수 매개변수는 다음과 같습니다.   
<table>
<tr><th>매개변수</th><th>설명 </th></tr>
<tr><td>Id</td><td>작성 중인 사물 유형의 ID를 제공합니다. </td></tr>
<tr><td>name</td><td>작성 중인 사물 유형의 이름을 제공합니다. </td></tr>
<tr><td>schemaId</td><td>구성 스키마 리소스에 대해 작성된 id입니다. </td></tr>
</table>

세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) 문서를 참조하십시오.   

<!-- The following example shows how to use Python to create a thing type that is called *RoomType*.
```python
result = api.createThingType(thingType, "RoomType", "roomTypeSchemaId", "The Room Thing type")

```  -->

## 4단계: 애플리케이션 인터페이스 스키마 파일 작성  
{: #crt_ai_schema_file}
애플리케이션 인터페이스에서 사용자는 사물 상태로서 저장된 데이터의 구조를 정의할 수 있습니다. 이 시나리오의 경우에는 온도 및 습도 특성을 정의하는 애플리케이션 인터페이스를 작성합니다. 애플리케이션 인터페이스 리소스를 작성할 때 생성된 애플리케이션 인터페이스 ID를 참조하여 애플리케이션 인터페이스를 사물 유형 *RoomType*과 연관시키십시오.   
다음 예제는 *RoomType 스키마*라고 하는 애플리케이션 인터페이스 스키마 파일을 작성하는 방법을 보여줍니다. 
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
## 5단계: 애플리케이션 인터페이스 스키마 리소스 작성.   
{: #crt_ai_schema_resource}  
다음 API를 사용하여 사물 유형의 애플리케이션 인터페이스 스키마 리소스를 작성하려면 이전 단계에서 작성된 애플리케이션 인터페이스 스키마 파일을 업로드하십시오.   
```
POST /schemas
```  
필수 매개변수는 다음과 같습니다.   
<table>
<tr>
<th>매개변수</th><th>설명 </th>
</tr>
<tr>
<td>name</td><td>작성 중인 애플리케이션 인터페이스 스키마의 이름을 제공합니다. </td>
</tr>
<tr>
<td>schemaFile</td><td>로컬 애플리케이션 인터페이스 스키마 JSON 파일의 경로입니다. </td>
</tr>
</table>  

세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas) 문서를 참조하십시오.   

<!-- The following example shows how to use Python to create the thing type application interface schema resource:  
```python
roomSchemaFile = open(schemasDir + "room.json", "r");
roomSchema = roomSchemaFile.read();
roomSchemaFile.close();
"roomSchemaId", result = api.createSchema("Room Schema", "room.json", roomSchema)
```  -->

스키마 ID를 사용하여 애플리케이션 인터페이스 스키마 리소스를 사물 유형의 애플리케이션 인터페이스에 추가하십시오.   

## 6단계: 사물 유형의 애플리케이션 인터페이스 작성.   
{: #crt_thing_ai}  
애플리케이션 인터페이스는 이전 단계에서 작성된 애플리케이션 인터페이스 스키마 리소스를 참조해야 합니다.   
애플리케이션 인터페이스를 작성하려면 다음 API를 사용하십시오.   
```
POST /applicationinterfaces
```  
필수 매개변수는 다음과 같습니다.   
<table>
<tr>
<th>	매개변수 </th><th>	설명 </th>
</tr>
<tr>
<td>	name	</td><td>	작성 중인 애플리케이션 인터페이스의 이름을 제공합니다. </td>
</tr>
<tr>
<td>	description	</td><td>	애플리케이션 인터페이스의 설명을 제공합니다. </td>
</tr>
<tr>
<td>	schemaId	</td><td>	로컬 애플리케이션 인터페이스 스키마 JSON 파일의 경로입니다. </td>
</tr>
</table>  

세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Application_Interfaces) 문서를 참조하십시오.   
이전 응답에서 리턴된 스키마 ID를 사용하여 애플리케이션 인터페이스 스키마를 애플리케이션 인터페이스에 추가하십시오.   

<!-- The following example shows how to use Python to create an application interface:  
```python
"applicationInterfaceId", result = api.createApplicationInterface("IRoom", "roomSchemaId")
```  -->

애플리케이션 인터페이스 ID를 사용하여 애플리케이션 인터페이스를 디바이스 유형에 추가하십시오. 이 ID를 사용하여 애플리케이션 인터페이스에 의해 정의된 특성에 인바운드 디바이스 이벤트를 맵핑할 수도 있습니다.  

## 7단계: 애플리케이션 인터페이스를 사물 유형에 추가.   
{: #add_thing_ai}  
애플리케이션 인터페이스를 사물 유형에 추가하려면 다음 API를 사용하십시오.   
```
POST /thing/types/{thingtypeId}/applicationinterfaces
```  
필수 매개변수는 다음과 같습니다.   
<table>
<tr>
<th>	매개변수 </th><th>	설명 </th>
</tr>
<tr>
<td>	id	</td><td>	사물 유형에 대해 작성된 id입니다. </td>
</tr>
<tr>
<td>	name	</td><td>	작성 중인 애플리케이션 인터페이스의 이름을 제공합니다. </td>
</tr>
<tr>
<td>	schemaId	</td><td>	애플리케이션 인터페이스 리소스에 대해 작성된 id입니다. </td>
</tr>
<tr>
<td>	refs/schema	</td><td>	애플리케이션 인터페이스 리소스의 경로입니다. 일반적인 값: /schemas/*schemaId*	</td>
</tr>
</table>  

세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) 문서를 참조하십시오.   
이 시나리오에서는 애플리케이션 인터페이스가 사물 유형 *RoomType*과 연관되어 있습니다. 

<!-- The following example shows how to use Python to add the thing application interface to the thing type *RoomType*:  
```python
result = api.addApplicationInterfaceToThingType(RoomType, "applicationInterfaceId", "roomSchemaId")
``` -->

## 8단계: 맵핑 정의 
{: #define_Thing_type_mappings}

집계된 디바이스 또는 사물의 상태에서의 특성을 사물 유형 애플리케이션 인터페이스에 정의된 특성에 맵핑하는 방법을 기술하는 사물 유형에 대한 맵핑을 정의하십시오. 

이벤트를 맵핑하려면 다음 API를 사용하십시오.   
```
POST /thing/types/{thingtypeId}/mappings
```  

필수 매개변수는 다음과 같습니다.   
<table>
<tr>
<th>	매개변수 </th><th>	설명 </th>
</tr>
<tr>
<td>	applicationInterfaceId	</td><td>	애플리케이션 인터페이스에 대해 작성된 id입니다. </td>
</tr>
<tr>
<td>	propertyMappings	</td><td>	디바이스 이벤트 페이로드의 특성으로 애플리케이션 인터페이스에 대해 정의된 특성을 맵핑하는 유효한 JSON 구조입니다. </td>
</tr>
</table>  

세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) 문서를 참조하십시오. 

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

다음 예제는 샘플 propertyMappings 매개변수 항목을 보여줍니다. 

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

*humiditySensor*는 사물 스키마에 정의되어 있습니다. "$event.humidity"는 ID "58c135ea52faff0001678f06"으로 애플리케이션 인터페이스 스키마에 정의되어 있습니다.
*temperatureSensor*는 사물 스키마에 정의되어 있습니다. "$event.temperatureC"는 ID "58c135e352faff0001198a89"로 애플리케이션 인터페이스 스키마에 정의되어 있습니다. 

## 9단계: 사물 유형과 연관된 구성의 배치   
{: #deploy_Thing_config}   
각 사물 유형에 대한 사물 상태 업데이트와 관련된 구성을 배치하십시오. 이 구성에는 스키마, 애플리케이션 인터페이스 및 맵핑이 포함됩니다. 

사물 유형의 인스턴스를 작성하려면 우선 사물 유형 구성을 배치해야 합니다. 

사물 유형 구성을 배치하려면 다음 API를 사용하십시오. 

```
PATCH /thing/types/{thingtypeId}
```
세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types) 문서를 참조하십시오.

<!-- The following example shows how to use Python to deploy your configuration for thing type *Room*:

```python
result = api.deployThingTypeConfiguration(thingType)
``` -->

## 10단계: 사물 유형의 인스턴스 작성 
{: #create_Thing_instances}

사물은 사물 유형의 인스턴스입니다. 사물을 사용하면 디바이스 또는 사물의 하나 이상의 인스턴스를 단일 오브젝트에 함께 집계할 수 있습니다. 

사물을 작성하려면 다음 API를 사용하십시오. 

```
POST /thing/types/{thingTypeId}/things
```

필수 매개변수는 다음과 같습니다.   
<table>
<tr>
<th>	매개변수 </th><th>	설명 </th>
</tr>
<tr>
<td>	typeId	</td><td>		이전에 작성된 사물 유형의 ID입니다. </td>
</tr>
<tr>
<td>	thingId	</td><td>	작성 중인 사물 인스턴스의 이름을 제공합니다. </td>
</tr>
</table>

세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Things) 문서를 참조하십시오. 

이 시나리오에서는 사물 유형 *RoomType*의 사물 인스턴스를 두 개 작성해야 합니다. 하나의 사물 인스턴스를 *meetingroom1*이라고 하며 또 하나의 사물 인스턴스를 *meetingroom2*라고 합니다. 

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

작성된 사물 ID는 온도 이벤트를 사물 애플리케이션 인터페이스에 추가하기 위해 호출된 POST 메소드의 URL에서 사용됩니다. 

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

## 11단계: 맵핑된 디바이스 이벤트가 애플리케이션 인터페이스에 공개되었는지 확인  
{: #publish_event}  
사물 *meetingroom1*에 집계된 디바이스에 대해 다음 이벤트를 공개하십시오.   
 - `iot-2/evt/tevt/fmt/json` 주제에서 *temperatureSensor1*의 온도 이벤트  
 - `iot-2/evt/hevt/fmt/json` 주제에서 *humiditySensor1*의 습도 이벤트  
사물 *meetingroom2*에 집계된 디바이스에 대해 다음 이벤트를 공개하십시오.   
 - `iot-2/evt/tempevt/fmt/json` 주제에서 *temperatureSensor2*의 온도 이벤트  
 - `iot-2/evt/humevt/fmt/json` 주제에서 *humiditySensor2*의 습도 이벤트  
디바이스에서 인바운드 이벤트의 공개에 대한 정보는 [애플리케이션용 MQTT 연결](../applications/mqtt.html#publishing_device_events)을 참조하십시오.   

## 12단계: 사물의 상태가 변경되었는지 확인.   
{: #verify_Thing_state}  
사물 상태를 확인하려면 다음 API를 사용하십시오.   
```
GET /thing/types/{thingTypeId}/things/{thingId}/state/{applicationInterfaceId}
```  

필수 매개변수는 다음과 같습니다.   
<table>
<tr>
<th>매개변수 </th><th>	설명 </th>
</tr>
<tr>
<td>thingtypeId	</td><td>사물 유형 ID입니다. </td>
</tr>
<tr>
<td>thingId	</td><td>	사물 ID입니다. </td>
</tr>
<tr>
<td>applicationInterfaceId	</td><td>애플리케이션 인터페이스에 대해 작성된 id입니다. </td>
</tr>
</table>  

세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) 문서를 참조하십시오.   

<!-- The following example shows how to use Python to retrieve the current state of *meetingroom1* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom1", applicationInterfaceId)
```  
The following example shows how to use Python to retrieve the current state of *meetingroom2* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom2", applicationInterfaceId)
``` -->
