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


# 애플리케이션 인터페이스 시나리오 1(베타)
{: #scenario}

다음 정보를 사용하여 두 개의 온도 센서가 {{site.data.keyword.iot_short_notm}}에 이벤트를 공개하는 시나리오를 작성할 수 있습니다. 하나의 센서는 섭씨로 온도를 측정합니다. 또 하나의 센서는 화씨로 온도를 측정합니다. 이러한 측정값은 섭씨인 하나의 온도 측정값으로 맵핑됩니다. 새 온도 측정값이 이러한 디바이스에 의해 공개되는 경우, 디바이스 상태와 연관된 특성의 값이 변경됩니다. 

## 전제조건

해당 조직에 대한 API 키 또는 토큰과 {{site.data.keyword.iot_short_notm}} 조직 인스턴스가 있어야 합니다. API 키와 토큰에 대한 자세한 정보는 [애플리케이션용 HTTP REST API](../applications/api.html#authentication)를 참조하십시오. 

## 이 태스크에 관한 정보

이 시나리오에서는 두 개의 디바이스가 구성됩니다. 

하나의 디바이스를 *TemperatureSensor1*이라고 합니다. 이 디바이스는 섭씨로 측정되는 온도 이벤트를 공개합니다. 온도 이벤트는 주제 `iot-2/evt/tevt/fmt/json`에서 공개되며 다음 예제 페이로드를 갖습니다. 
```
{
  “t” : 34.5
}
```

**참고:** 이벤트 ID는 *tevt*입니다. 이 ID는 이 유형의 온도 이벤트를 실제 인터페이스에 추가할 때와 이 유형의 인바운드 이벤트와 연관된 특성을 애플리케이션 인터페이스의 특성에 맵핑하는 맵핑을 정의할 때 필요합니다. 이 시나리오에서는 애플리케이션 인터페이스에 정의된 특성을 **temperature**라고 합니다. 

다른 디바이스를 *TemperatureSensor2*라고 합니다. 이 디바이스는 화씨로 측정되는 온도 이벤트를 공개합니다. 온도 이벤트는 주제 `iot-2/evt/tempevt/fmt/json`에서 공개되며 다음 예제 페이로드를 갖습니다. 
```
{
  “temp” : 72.55
}
```

**참고:** 이벤트 ID는 *tempevt*입니다. 이 ID는 이 유형의 온도 이벤트를 실제 인터페이스에 추가할 때와 이 유형의 인바운드 이벤트와 연관된 특성을 애플리케이션 인터페이스의 특성에 맵핑하는 맵핑을 정의할 때 필요합니다. 이 시나리오에서는 애플리케이션 인터페이스에 정의된 특성을 **temperature**라고 합니다. 

애플리케이션 인터페이스도 구성됩니다. 이 애플리케이션 인터페이스는 다음 구조로 이 유형의 디바이스에 대한 상태를 표시합니다. 
```
{
  “temperature” : <current temperature value in Celsius>
  }
```
이 구성은 해당 값을 섭씨로 변환한 후에 **t**와 연관된 값을 처리하고 **temp**와 연관된 값을 처리하는 애플리케이션을 구성하는 대신에 **temperature**와 연관된 값을 처리하는 애플리케이션을 구성할 수 있음을 의미합니다.

![{{site.data.keyword.iot_short_notm}}에서 온도 센서 디바이스 및 애플리케이션 간의 맵핑.](images/Information "{{site.data.keyword.iot_short_notm}}에서 온도 센서 디바이스 및 애플리케이션 간의 맵핑")  

다음 예제 시나리오를 사용하여 자체 인터페이스 환경을 설정할 수 있습니다. 

## 필요하면 디바이스 유형 및 디바이스를 추가하십시오. 
{: #step14}

이 시나리오에서는 두 개의 디바이스 유형과 두 개의 디바이스 인스턴스를 가정합니다. 디바이스 인스턴스 *TemperatureSensor1*은 디바이스 유형 *EnvSensor1*과 연관되어 있습니다. 디바이스 인스턴스 *TemperatureSensor2*는 디바이스 유형 *EnvSensor2*와 연관되어 있습니다. 

REST API를 사용한 디바이스 유형 추가에 대한 정보는 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types) 문서를 참조하십시오. 

## 1단계: 이벤트 스키마 파일 작성. 
{: #step1}

이 시나리오의 경우에는 각각의 인바운드 온도 이벤트의 구조를 정의하는 두 개의 이벤트 스키마 파일을 작성하십시오. 

**중요:** 구조화된 [JSON ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://json-schema.org/){:new_window} 이벤트 페이로드에 대해 각각의 중첩 레벨이 `"properties"` 항목에서 올바르게 랩핑되었는지 확인하십시오. 예를 들어, 페이로드가 `{"d":{"t":<temp>}}`인 경우에는 다음을 사용할 수 있습니다. 
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

다음 예제는 *tEventSchema.json*이라고 하는 스키마 파일을 작성하는 방법을 표시합니다. 이 파일은 섭씨로 온도를 측정하는 온도 센서의 인바운드 이벤트에 대한 구조를 정의합니다. 

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
**팁:** “필수” 매개변수를 사용하여 하나 이상의 특성을 필수로 표시할 수 있습니다. Watson IoT Platform이 디바이스 데이터로 디바이스 상태를 업데이트할 수 있도록 필수 특성은 디바이스 메시지에 포함되어야 합니다. 필수 특성이 포함되지 않은 메시지는 처리되지 않습니다.    

스키마 파일 이름 *tEventSchema*는 이벤트 유형에 대한 이벤트 스키마 리소스를 작성할 때 사용됩니다. 

다음 예제는 *tempEventSchema.json*이라고 하는 스키마 파일을 작성하는 방법을 표시합니다. 이 파일은 화씨로 온도를 측정하는 온도 센서의 인바운드 이벤트에 대한 구조를 정의합니다. 

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
스키마 파일 이름 *tempEventSchema*는 이벤트 유형에 대한 이벤트 스키마 리소스를 작성할 때 사용됩니다.    

## 2단계: 이벤트 유형에 대한 이벤트 스키마 리소스 작성
{: #step2}

이벤트 스키마 리소스를 작성하려면 다음 API를 사용하십시오. 

```
POST /schemas
```

필수 매개변수는 다음과 같습니다.   

매개변수	|	설명   
------	|	-----  
name	|	작성 중인 이벤트 스키마의 이름을 제공합니다.   
schemaFile	|	로컬 이벤트 스키마 JSON 파일의 경로입니다.   



세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas) 문서를 참조하십시오. 

다음 예제는 cURL을 사용하여 이벤트 스키마 리소스 *tEventSchema.json*을 작성하는 방법을 표시합니다. 

```curl
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=tEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tEventSchema.json'
```

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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
POST 메소드에 대한 응답으로 리턴된 스키마 ID *5846cd7c6522050001db0e0d*는 이벤트 유형에 이벤트 스키마를 추가할 때 필요합니다.

다음 예제는 cURL을 사용하여 이벤트 스키마 리소스 *tempEventSchema.json*을 작성하는 방법을 표시합니다. 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: multipart/form-data’ \
  --form name=tempEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tempEventSchema.json"'
```

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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
POST 메소드에 대한 응답으로 리턴된 스키마 ID *5846cee36522050001db0e0e*는 이벤트 유형에 이벤트 스키마를 추가할 때 필요합니다.

## 3단계: 이벤트 스키마를 참조하는 이벤트 유형 작성
{: #step3}

각각의 이벤트 유형은 이벤트 스키마 리소스의 작성에 사용된 POST 메소드에 대한 응답으로 리턴된 스키마 ID를 사용하여 이전 예제에서 작성된 관련 이벤트 스키마를 참조합니다. 

이벤트 유형을 작성하려면 다음 API를 사용하십시오. 

```
POST /event/types
```

필수 매개변수는 다음과 같습니다.   

매개변수	|	설명
------	|	-----
name	|	작성 중인 이벤트 유형의 이름을 제공합니다.
schemaId	|	이벤트 스키마 리소스에 대해 작성된 id입니다.


세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types) 문서를 참조하십시오. 


다음 예제는 cURL을 사용하여 섭씨로 측정되는 온도 이벤트에 대한 이벤트 유형을 작성합니다. 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d”}'
```

스키마 ID *5846cd7c6522050001db0e0d*는 이벤트 유형에 이벤트 스키마를 추가하는 데 사용됩니다. 이 ID는 이벤트 스키마 리소스 *tEventSchema.json*을 작성하는 데 사용된 POST 메소드에 대한 응답으로 리턴되었습니다. 

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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

POST 메소드에 대한 응답으로 리턴된 이벤트 유형 ID *5846d0fd6522050001db0e0f*는 실제 인터페이스에 이벤트 유형을 추가하는 데 사용됩니다. 

다음 예제는 cURL을 사용하여 화씨로 측정되는 온도 이벤트에 대한 이벤트 유형을 작성합니다. 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tempEvent", "schemaId" : "5846cee36522050001db0e0e"}'
```
스키마 ID *5846cee36522050001db0e0e*는 이벤트 유형에 이벤트 스키마를 추가하는 데 사용됩니다. 이 ID는 이벤트 스키마 리소스 *tempEventSchema.json*을 작성하는 데 사용된 POST 메소드에 대한 응답으로 리턴되었습니다.

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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
POST 메소드에 대한 응답으로 리턴된 이벤트 유형 ID *5846d2846522050001db0e10*는 실제 인터페이스에 이벤트 유형을 추가하는 데 사용됩니다.

## 4단계: 실제 인터페이스 작성
{: #step7}

실제 인터페이스를 작성하려면 다음 API를 사용하십시오. 

```
POST /physicalinterfaces
```

필수 매개변수는 다음과 같습니다.   

매개변수	|	설명
------	|	-----
name	|	작성 중인 실제 인터페이스의 이름을 제공합니다.


세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces) 문서를 참조하십시오. 

이 시나리오에서는 각 이벤트 유형마다 하나씩 두 개의 실제 인터페이스가 필요합니다. 

다음 예제는 cURL을 사용하여 첫 번째 실제 인터페이스를 작성하는 방법을 표시합니다. 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 1"}'
```

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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

응답으로 리턴된 실제 인터페이스 ID *5847d1df6522050001db0e1a*는 섭씨로 측정되는 온도 이벤트를 실제 인터페이스에 추가하기 위해 호출된 POST 메소드의 URL에서 사용됩니다. 

다음 예제는 cURL을 사용하여 두 번째 실제 인터페이스를 작성하는 방법을 표시합니다. 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 2"}'
```

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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

응답으로 리턴된 실제 인터페이스 ID *5847d1df6522050001db0e1b*는 화씨로 측정되는 온도 이벤트를 실제 인터페이스에 추가하기 위해 호출된 POST 메소드의 URL에서 사용됩니다.    

## 5단계: 실제 인터페이스에 이벤트 유형 추가
{: #step8}

실제 인터페이스에 이벤트 유형을 추가하려면 다음 API를 사용하십시오. 

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```

필수 매개변수는 다음과 같습니다.   

매개변수	|	설명
------	|	-----
eventId	|	디바이스 이벤트 페이로드에서 이벤트 이름을 입력합니다.
eventTypeId	|	이벤트 유형에 대해 작성된 id입니다.


세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces) 문서를 참조하십시오. 

이 시나리오에서는 다음 이벤트 유형이 지정된 실제 인터페이스에 추가됩니다. 
- 섭씨 온도 이벤트 *tevt*가 주제의 *eventId* 및 이벤트 스키마 리소스 작성의 *eventTypeId*를 사용하여 ID *5847d1df6522050001db0e1a*의 실제 인터페이스에 추가됩니다. 
- 화씨 온도 이벤트 *tempevt*가 주제의 *eventId* 및 이벤트 스키마 리소스 작성의 *eventTypeId*를 사용하여 ID *5847d1df6522050001db0e1b*의 실제 인터페이스에 추가됩니다. 


다음 예제는 cURL을 사용하여 온도 이벤트 *tevt*를 ID *5847d1df6522050001db0e1a*의 실제 인터페이스에 추가하는 방법을 표시합니다. 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : “tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
```

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

```
{
  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
}
```

다음 예제는 cURL을 사용하여 온도 이벤트 *tempevt*를 ID *5847d1df6522050001db0e1b*의 실제 인터페이스에 추가하는 방법을 표시합니다. 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1b/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tempevt", "eventTypeId" : "5846d2846522050001db0e10"}'
```

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

```
{
  "eventTypeId" : "5846d2846522050001db0e10",
  "eventId" : “tempevt"
}
```

## 6단계: 실제 인터페이스에 연결하도록 디바이스 유형 업데이트
{: #step9}

디바이스 유형를 업데이트하려면 다음 API를 사용하십시오. 

```
PUT /device/types/{typeId}
```

필수 매개변수는 다음과 같습니다.   

매개변수	|	설명
------	|	-----
physicalInterfaceId	|	실제 인터페이스에 대해 작성된 id입니다.


세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 문서를 참조하십시오. 

이 시나리오에서는 실제 인터페이스 *5847d1df6522050001db0e1a*에 연결하도록 디바이스 유형 *EnvSensor1*이 업데이트되며 실제 인터페이스 *5847d1df6522050001db0e1b*에 연결하도록 디바이스 유형 *EnvSensor2*이 업데이트됩니다. 

다음 예제는 cURL을 사용하여 디바이스 유형 *EnvSensor1*을 업데이트하는 방법을 표시합니다. 

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a”}’
```

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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
디바이스 ID *EnvSensor1*는 실제 인터페이스와 애플리케이션 인터페이스를 추가할 때 필요합니다.

다음 예제는 cURL을 사용하여 디바이스 유형 *EnvSensor2*를 업데이트하는 방법을 표시합니다. 

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b”}’
```

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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
디바이스 ID *EnvSensor2*는 실제 인터페이스와 애플리케이션 인터페이스를 추가할 때 필요합니다.



## 7단계: 애플리케이션 인터페이스 스키마 파일 작성
{: #step4}

다음 예제는 *envSensor.json*이라고 하는 애플리케이션 인터페이스 스키마 파일을 작성하는 방법을 표시합니다. 

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

## 8단계: 애플리케이션 인터페이스 스키마 리소스 작성 
{: #step5}

애플리케이션 인터페이스 스키마 리소스를 작성하려면 다음 API를 사용하십시오. 

```
POST /schemas
```

필수 매개변수는 다음과 같습니다.   

매개변수	|	설명
------	|	-----
name	|	작성 중인 애플리케이션 인터페이스 스키마의 이름을 제공합니다.
schemaFile	|	로컬 애플리케이션 인터페이스 스키마 JSON 파일의 경로입니다.


세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas) 문서를 참조하십시오. 

다음 예제는 cURL을 사용하여 애플리케이션 인터페이스 스키마를 작성하는 방법을 표시합니다. 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=temperatureEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/envSensor.json"'
```

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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
POST 메소드에 대한 응답으로 리턴된 스키마 ID *5846ec826522050001db0e11*를 사용하면 애플리케이션 인터페이스 스키마를 애플리케이션 인터페이스에 추가할 수 있습니다.

## 9단계: 애플리케이션 인터페이스 스키마를 참조하는 애플리케이션 인터페이스 작성
{: #step6}

애플리케이션 인터페이스를 작성하려면 다음 API를 사용하십시오. 

```
POST /applicationinterfaces
```

필수 매개변수는 다음과 같습니다.   

매개변수	|	설명
------	|	-----
name	|	작성 중인 애플리케이션 인터페이스의 이름을 제공합니다.
schemaId	|	애플리케이션 인터페이스 스키마 리소스에 대해 작성된 id입니다.


세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Application_Interfaces) 문서를 참조하십시오. 

이 시나리오에서는 이전 응답에서 리턴된 스키마 ID *5846ec826522050001db0e11*을 사용하여 애플리케이션 인터페이스 스키마를 애플리케이션 인터페이스에 추가합니다. 

다음 예제는 cURL을 사용하여 애플리케이션 인터페이스를 작성하는 방법을 표시합니다. 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "environment sensor interface", "schemaId" : "5846ec826522050001db0e11"}'
```

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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
이 시나리오에서는 POST 메소드에 대한 응답으로 리턴된 애플리케이션 인터페이스 ID *5846ed076522050001db0e12*를 사용하여 애플리케이션 인터페이스를 디바이스 유형에 추가합니다. 이 ID를 사용하여 애플리케이션 인터페이스에 의해 정의된 특성에 인바운드 디바이스 이벤트를 맵핑할 수도 있습니다.

## 10단계: 디바이스 유형에 애플리케이션 인터페이스 추가
{: #step10}

디바이스 유형에 애플리케이션 인터페이스를 추가하려면 다음 API를 사용하십시오. 

```
POST /device/types/{typeId}/applicationinterfaces
```

필수 매개변수는 다음과 같습니다.   

매개변수	|	설명
------	|	-----
id	|	애플리케이션 인터페이스에 대해 작성된 id입니다.
name	|	디바이스 유형의 이름입니다.
schemaId	|	애플리케이션 인터페이스 리소스에 대해 작성된 id입니다.
refs/schema	|	애플리케이션 인터페이스 리소스의 경로입니다. 일반적인 값: /schemas/*schemaId*


	세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 문서를 참조하십시오. 

이 시나리오에서는 애플리케이션 인터페이스가 디바이스 유형 *EnvSensor1* 및 디바이스 유형 *EnvSensor2*와 연관됩니다. 

다음 예제는 cURL을 사용하여 애플리케이션 스키마 ID *5846ec826522050001db0e11*을 참조하는 애플리케이션 인터페이스 *5846ed076522050001db0e12*를 디바이스 유형 *EnvSensor1*에 추가하는 방법을 표시합니다. 

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

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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

다음 예제는 cURL을 사용하여 애플리케이션 스키마 ID *5846ec826522050001db0e11*과 연관된 애플리케이션 인터페이스 *5846ed076522050001db0e12*를 디바이스 유형 *EnvSensor2*에 추가하는 방법을 표시합니다. 

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


다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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

## 11단계: 인바운드 이벤트의 특성을 애플리케이션 인터페이스의 특성에 맵핑하기 위한 맵핑 정의
{: #step11}

이벤트를 맵핑하려면 다음 API를 사용하십시오. 

```
POST /device/types/{typeId}/mappings
```

필수 매개변수는 다음과 같습니다.   

매개변수	|	설명
------	|	-----
applicationInterfaceId		|	애플리케이션 인터페이스에 대해 작성된 id입니다.
propertyMappings	|	디바이스 이벤트 페이로드의 특성으로 애플리케이션 인터페이스에 대해 정의된 특성을 맵핑하는 유효한 JSON 구조입니다. 다음 예제를 참조하십시오.


세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 문서를 참조하십시오. 

이 시나리오에서는 인바운드 이벤트 *tevt*의 **t** 특성을 애플리케이션 인터페이스의 **temperature** 특성에 맵핑하기 위한 디바이스 유형 *EnvSensor1*의 맵핑을 정의합니다. 또한 인바운드 이벤트 *tempevt*의 **temp** 특성을 애플리케이션 인터페이스의 **temperature** 특성에 맵핑하기 위한 디바이스 유형 *EnvSensor2*의 맵핑도 정의합니다. 

다음 예제는 cURL을 사용하여 디바이스 유형 *EnvSensor1*에 대한 맵핑을 추가하는 방법을 표시합니다. 

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

**중요:** 구조화된 [JSON ![외부 링크 아이콘](../../../icons/launch-glyph.svg "외부 링크 아이콘")](http://json-schema.org/){:new_window} 이벤트 페이로드에 대해 $event.*property* 항목이 사용자 특성의 JSON 구조와 올바르게 일치하는지 확인하십시오. 예를 들어, 페이로드가 `{"d":{"t":<temp>}}`인 경우에는 `$event.d.t`를 사용하십시오. 

애플리케이션 인터페이스 및 디바이스 유형 *EnvSensor1*의 작성에 사용되는 POST 메소드에 대한 응답으로 리턴된 애플리케이션 인터페이스 ID *5846ed076522050001db0e12*를 지정하십시오. 

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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
다음 예제는 cURL을 사용하여 디바이스 유형 *EnvSensor2*에 대한 맵핑을 추가하는 방법을 표시합니다.

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

애플리케이션 인터페이스 및 디바이스 유형 *EnvSensor2*의 작성에 사용되는 POST 메소드에 대한 응답으로 리턴된 애플리케이션 인터페이스 ID *5846ed076522050001db0e12*를 지정하십시오.
변환을 적용하여 값을 화씨의 측정값에서 섭씨의 측정값으로 변경할 수 있습니다. 


다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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

## 12단계: 구성 배치
{: #step15}

각 디바이스 유형의 디바이스 상태 업데이트와 관련된 구성을 배치하십시오. 이 구성에는 스키마, 이벤트 유형, 실제 인터페이스, 애플리케이션 인터페이스 및 맵핑이 포함됩니다. 

디바이스 유형 구성을 배치하려면 다음 API를 사용하십시오. 

```
PATCH /device/types/{typeId}
```

필수 매개변수는 다음과 같습니다.   

매개변수	|	설명
------	|	-----
typeId	|	디바이스 유형 ID입니다.

세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 문서를 참조하십시오. 

이 시나리오에서는 두 개의 디바이스 유형에 대한 구성을 배치해야 합니다. 

다음 예제는 cURL을 사용하여 디바이스 유형 *EnvSensor1*에 대한 구성을 배치하는 방법을 표시합니다. 

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy-configuration"
          }'
```

다음 예제는 PATCH 메소드에 대한 응답을 표시합니다. 

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

다음 예제는 cURL을 사용하여 디바이스 유형 *EnvSensor2*에 대한 구성을 배치하는 방법을 표시합니다. 

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
          }'
```

다음 예제는 PATCH 메소드에 대한 응답을 표시합니다. 

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

## 13단계: 인바운드 디바이스 이벤트 공개
{: #step12}

주제 `iot-2/evt/tevt/fmt/json`에서 *TemperatureSensor1*의 온도 이벤트와 주제 `iot-2/evt/tempevt/fmt/json`에서 *TemperatureSensor2*의 온도 이벤트를 공개하십시오. 

디바이스에서 인바운드 이벤트의 공개에 대한 정보는 [애플리케이션용 MQTT 연결](../applications/mqtt.html#publishing_device_events)을 참조하십시오. 


## 14단계: 디바이스의 상태가 변경되었는지 확인
{: #step13}

디바이스 상태를 확인하려면 다음 API를 사용하십시오. 
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```

필수 매개변수는 다음과 같습니다.   

매개변수	|	설명
------	|	-----
typeId	|	디바이스 유형 ID
deviceId	|	디바이스 ID입니다.
applicationInterfaceId		|	애플리케이션 인터페이스에 대해 작성된 id입니다.

세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 문서를 참조하십시오. 

다음 예제는 cURL을 사용하여 작성된 애플리케이션 인터페이스의 ID를 참조함으로써 *TemperatureSensor1*의 현재 상태를 검색하는 방법을 표시합니다. 
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/devices/TemperatureSensor1/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

애플리케이션 인터페이스 ID *5846ed076522050001db0e12*는 GET 메소드에서 사용됩니다. 이 ID는 애플리케이션 인터페이스의 작성에 사용된 POST 메소드에 대한 응답으로 리턴됩니다.
다음 예제는 GET 메소드에 대한 응답을 표시합니다. 
```
{
  "temperature":34.5
}
```
다음 예제는 cURL을 사용하여 작성된 애플리케이션 인터페이스의 ID를 참조함으로써 *TemperatureSensor2*의 현재 상태를 검색하는 방법을 표시합니다.
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/devices/TemperatureSensor2/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

애플리케이션 인터페이스 ID *5846ed076522050001db0e12*는 GET 메소드에서 사용됩니다. 이 ID는 애플리케이션 인터페이스의 작성에 사용된 POST 메소드에 대한 응답으로 리턴됩니다.
다음 예제는 GET 메소드에 대한 응답을 표시합니다. 
```
{
  "temperature":22.5
}
```
참고로, 리턴되는 온도 측정값은 화씨가 아닌 섭씨입니다.

애플리케이션은 서로 다른 온도 스케일을 파악하거나 변환하기 위한 구성을 요구하지 않고도 이 정규화된 데이터를 처리할 수 있습니다. 


**참고:** 최근에 배치된 구성을 검색하려면 다음 API를 사용하십시오. 

```
GET /device/types/<typeId>/deployedconfiguration
```
이 API를 사용하면 PATCH 배치 조작이 정상적으로 완료된 최근 시간에 배치된 구성을 검색할 수 있습니다. 변경되었지만 배치되지 않은 리소스의 구성을 검색하려면 조회할 리소스와 연관된 일반 GET 메소드를 사용하십시오.

세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 문서를 참조하십시오. 

다음 예제는 cURL을 사용하여 최근에 배치된 구성을 검색하는 방법을 보여줍니다. 
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/deployedconfiguration \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```
다음 예제는 GET 메소드에 대한 응답을 표시합니다.

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
