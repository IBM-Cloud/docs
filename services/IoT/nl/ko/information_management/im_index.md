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

# 인터페이스를 사용하여 디바이스 데이터 맵핑(베타)
{: #im_index}

{{site.data.keyword.iot_full}}의 인터페이스 맵핑 기능을 사용하여 입출력 디바이스 데이터를 구성하고 통합할 수 있습니다.
{:shortdesc}

**중요:** 인터페이스 맵핑 기능은 현재 베타 기능으로만 사용 가능합니다. 최종 릴리스 이전에는 베타 업데이트에 현재 버전과 호환되지 않는 변경사항이 포함될 수 있습니다. 최종 릴리스 전에는 베타 기능을 프로덕션 애플리케이션에서 사용하지 않도록 적극 권장합니다. 추가 정보를 받고 이 베타에 대한 피드백을 제공하려면 [IM 베타 프로그램에 등록](https://www.ibm.com/software/support/trial/cst/forms/nomination.wss?id=7050)하고 귀하의 의견을 알려 주십시오. 

## 개요
{: #overview}

인터페이스 맵핑 기능을 사용하여 애플리케이션에 대한 인터페이스를 개발할 수 있습니다. {{site.data.keyword.iot_short_notm}}에 연결하고자 하는 다양한 유형, 제품 또는 모델의 디바이스 또는 센서가 있을 수 있으며, 이러한 디바이스는 다양한 형식의 데이터를 공개할 수 있습니다. 인터페이스 맵핑 기능을 사용하면 입력 데이터를 정규화할 수 있으며 특정 디바이스가 연결된 방법의 복잡성에서 애플리케이션을 분리함으로써 이를 단순화할 수 있습니다. 

예를 들어, 두 개의 온도 센서가 있을 수 있습니다. 하나의 센서는 섭씨로 온도를 측정하며 다른 하나의 센서는 화씨로 온도를 측정합니다. 

![{{site.data.keyword.iot_short_notm}}에서 온도 센서 디바이스 및 애플리케이션 간의 맵핑.](images/Information "{{site.data.keyword.iot_short_notm}}에서 온도 센서 디바이스 및 애플리케이션 간의 맵핑")

온도 센서 1은 `{ "t" : 34.5 }`의 온도 측정값을 {{site.data.keyword.iot_short_notm}}에 공개합니다. 이는 섭씨 값의 온도 측정값입니다. 온도 센서 2는 `{ "temp" : 72.55 }`의 온도 측정값을 {{site.data.keyword.iot_short_notm}}에 공개합니다. 이는 화씨 값의 측정값을 갖는 다른 유형의 온도 센서입니다. 이 온도 측정값은 별도의 이벤트로서 {{site.data.keyword.iot_short_notm}}에 공개됩니다. 

인터페이스 맵핑 기능을 사용하면 이러한 측정값을 처리를 위해 일관된 양식으로 정규화할 수 있습니다. 서로 다른 온도 스케일을 파악하거나 변환하기 위한 애플리케이션을 작성할 필요가 없습니다. 애플리케이션은 하나의 정규화된 보기를 수신하며, **t** 및 **temp**에 연결하는 대신 **temperature**에 연결할 수 있습니다. 

## 디바이스 및 애플리케이션 간의 데이터 플로우
{: #mapping}

다음의 플로우 다이어그램은 인터페이스 맵핑 기능에서 서로 다른 자원이 사용되는 방법을 표시합니다. 

![{{site.data.keyword.iot_short_notm}}에서 디바이스 및 애플리케이션 간의 플로우.](images/Information "{{site.data.keyword.iot_short_notm}}에서 디바이스 및 애플리케이션 간의 플로우")

다음 다이어그램은 이 플로우에서 스키마가 사용되는 방법을 예시합니다. 

![{{site.data.keyword.iot_short_notm}}에서 디바이스 및 애플리케이션 간의 플로우.](images/Information "{{site.data.keyword.iot_short_notm}}에서 디바이스 및 애플리케이션 간의 플로우")

JSON 스키마는 [디바이스 상태](#key_concepts) 및 입력 이벤트의 형식을 정의하고 유효성 검증하는 데 사용됩니다. 이러한 스키마에 대한 자세한 정보는 [스키마](#resources)를 참조하십시오. 

## 핵심 개념
{: #key_concepts}

인터페이스 맵핑 기능은 {{site.data.keyword.iot_short_notm}}을 통해 이동되는 데이터를 보다 잘 제어할 수 있도록 실제 인터페이스 자원과 애플리케이션 인터페이스 자원을 추가함으로써 [디바이스 유형](#resources)의 현재 개념을 확장합니다. 

다음 다이어그램은 [자원](#resources)을 사용한 {{site.data.keyword.iot_short_notm}}의 디바이스와 애플리케이션 간의 논리 맵핑을 예시합니다. 

![{{site.data.keyword.iot_short_notm}}에서 디바이스 및 애플리케이션 간의 논리 맵핑.](images/im_mapping.svg "{{site.data.keyword.iot_short_notm}}에서 디바이스 및 애플리케이션 간의 논리 맵핑")

인터페이스 맵핑은 디바이스 상태의 개념을 참조합니다. 디바이스 상태는 애플리케이션 인터페이스가 정의하는 특성의 세트로 구성됩니다. 이러한 특성의 가장 최신 값은 {{site.data.keyword.iot_short_notm}}에 저장되며, HTTP API를 사용하여 요청 시에 애플리케이션이 이를 사용할 수 있습니다. 

인바운드 이벤트의 데이터를 처리하고 인바운드 이벤트의 특성을 애플리케이션 인터페이스의 특성으로 맵핑하려면 다음 정보를 구성해야 합니다. 

- 하나 이상의 인바운드 이벤트의 구조. 이벤트 스키마는 이 정보를 정의합니다. 각 이벤트 스키마는 하나의 인바운드 이벤트의 구조를 정의하고 하나의 이벤트 유형과 연관됩니다. 실제 인터페이스는 하나 이상의 이벤트 유형을 그룹화합니다. 

    인바운드 디바이스 이벤트 내에 포함된 데이터의 구조와 형식은 JSON 스키마 형식인 이벤트 스키마 파일로 정의됩니다. 이름 지정된 스키마 자원을 작성하는 POST 메소드를 사용하여 이벤트 스키마 파일을 {{site.data.keyword.iot_short_notm}}에 업로드할 수 있습니다. 베타인 경우에는 모든 인바운드 이벤트가 JSON 형식이어야 합니다. 

- 원하는 디바이스 상태의 구조. 애플리케이션 인터페이스 스키마에서 이 정보를 정의합니다. 

    디바이스 상태는 애플리케이션이 디바이스에서 데이터로서 수신하도록 구성된 데이터 구조 및 데이터의 표시입니다. 디바이스 상태에 저장된 특성 값은 인바운드 디바이스 이벤트에 대한 응답으로 업데이트됩니다. 최신 디바이스 상태 값은 HTTP API를 사용하여 요청 시에 애플리케이션에 제공됩니다. 

- 인바운드 이벤트를 원하는 디바이스 상태로 맵핑하는 방법에 대한 정보. 맵핑에서 이 정보를 정의합니다. 

    인바운드 이벤트의 특성에 포함된 데이터를 애플리케이션 인터페이스의 해당되는 특성으로 맵핑하려면 맵핑을 작성해야 합니다. 맵핑은 디바이스의 인바운드 이벤트에 대한 응답으로 특정 애플리케이션 인터페이스가 정의한 특성을 업데이트하는 방법을 기술합니다. 


## 자원
{: #resources}

REST API를 사용하여 이전 다이어그램에 예시된 자원을 관리할 수 있습니다. REST API에 대한 정보는 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html) 문서를 참조하십시오. 

자원                        | 설명        
------------- | ------------- | -------------  
스키마                         | JSON 스키마는 원하는 디바이스 상태 및 디바이스에서 {{site.data.keyword.iot_short_notm}}에 공개된 인바운드 이벤트의 구조를 정의하는 데 사용됩니다. JSON 스키마에 대한 자세한 정보는 [JSON 스키마](http://json-schema.org/)를 참조하십시오. 인터페이스 맵핑에서는 두 개의 JSON 스키마(이벤트 스키마 및 애플리케이션 인터페이스 스키마)가 참조됩니다. 이벤트 스키마는 디바이스에 의해 {{site.data.keyword.iot_short_notm}}에 공개된 이벤트의 구조를 정의하는 데 사용됩니다. 애플리케이션 인터페이스 스키마는 애플리케이션 인터페이스에 의해 참조되며, {{site.data.keyword.iot_short_notm}}에 저장된 [디바이스 상태](#key_concepts)의 정의를 정의하는 데 사용됩니다.
이벤트 유형                         | {{site.data.keyword.iot_short_notm}}이 특정 이벤트 내에 포함된 데이터를 처리할 수 있도록 사용자는 조직 내의 이벤트 유형을 작성해야 합니다. 모든 이벤트 유형은 이벤트 스키마를 참조해야 합니다. 베타인 경우에는 모든 인바운드 이벤트가 JSON 형식이어야 합니다.    
실제 인터페이스                         | 실제 인터페이스는 하나 이상의 이벤트 유형과 연관될 수 있으며, 디바이스 유형와 연관된 이벤트 유형을 정의합니다.   
디바이스 유형                         | Watson IoT Platform에 연결된 모든 디바이스는 디바이스 유형과 연관됩니다. 디바이스 유형은 특성 또는 동작을 공유하는 디바이스 그룹입니다. 인터페이스 맵핑에서는 디바이스 상태를 검색하는 데 사용될 수 있는 애플리케이션 인터페이스 및 디바이스의 실제 인터페이스를 포함하도록 디바이스 유형이 확장됩니다. 디바이스 유형은 다수의 애플리케이션 인터페이스에서 구성될 수 있습니다. 디바이스 유형에 대한 자세한 정보는 [디바이스 모델](../reference/device_model.html#id_and_device_types)의 "ID 및 디바이스 유형" 절을 참조하십시오.
애플리케이션 인터페이스                         | 애플리케이션 인터페이스는 애플리케이션 인터페이스 스키마를 참조해야 합니다. 애플리케이션 인터페이스 내에서는 디바이스 상태로서 저장된 데이터의 구조를 정의할 수 있습니다. 디바이스 상태는 애플리케이션이 디바이스에서 데이터로서 수신하도록 구성된 데이터 구조 및 데이터의 표시입니다. 맵핑을 정의하려면 우선 최소한 하나의 애플리케이션이 디바이스 유형과 연관되어야 합니다.
맵핑                         | 맵핑은 인바운드 이벤트와 연관된 특성이 특정 애플리케이션 인터페이스에서 정의된 특정으로 맵핑되는 방법을 정의합니다. 맵핑은 적용되는 대상인 애플리케이션 인터페이스 ID를 지정해야 하며, 해당 애플리케이션 인터페이스는 맵핑이 추가되는 대상 디바이스 유형과 연관되어야 합니다.


## 상위 레벨 워크플로우
{: #workflow}



### 이 태스크에 관한 정보

다음 단계를 사용하면 인터페이스를 사용하여 디바이스 데이터의 맵핑을 시작해야 하는 자원을 구성하는 데 도움이 됩니다. 

API에 대한 세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html) 문서를 참조하십시오.
각 단계에 대한 자세한 정보는 [예제 시나리오](#scenario)를 참조하십시오. 또는 링크를 사용하여 예제 시나리오 내의 특정 단계로 직접 이동하십시오. 

### 인터페이스를 사용한 디바이스 데이터 맵핑을 시작하도록 환경 구성

1.  필요하면 디바이스 유형 및 디바이스를 추가하십시오. 

  1. 다음 URI로 REST API POST 메소드를 사용하여 디바이스 유형을 작성하십시오. 
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types
      ```
  2.  필요하면 디바이스를 추가하십시오.   
디바이스 유형 및 디바이스 추가에 대한 자세한 정보는 [디바이스 연결](../iotplatform_task.html#devices)을 참조하십시오. 

2. 실제 인터페이스 작성

  1. [이벤트 스키마 파일을 작성](#step1)하십시오. 이벤트 스키마 파일은 인바운드 이벤트의 구조와 형식을 정의하는 로컬 .JSON 파일입니다. 

  2. 다음 URI로 REST API POST 메소드를 사용하여 [이벤트 유형에 대한 이벤트 스키마 자원을 작성](#step2)하십시오. 
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
      ```  

  3. 다음 URI로 REST API POST 메소드를 사용하여 [이벤트 스키마를 참조하는 이벤트 유형을 작성](#step3)하십시오. 
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/event/types
      ```
      이벤트 스키마 자원의 작성에 사용되는 POST 메소드에 대한 응답으로 리턴된 스키마 ID를 사용하여 이벤트 스키마에 이벤트 유형을 추가하십시오.

  4. 다음 URI로 REST API POST 메소드를 사용하여 [실제 인터페이스를 작성](#step7)하십시오. 
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces
        ```

   5. 다음 URI로 REST API POST 메소드를 사용하여 [실제 인터페이스에 이벤트 유형을 추가](#step8)하십시오. 
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/{physicalInterfaceId}/events
        ```

       이벤트 유형의 작성에 사용되는 POST 메소드에 대한 응답으로 리턴된 이벤트 유형 ID *eventTypeId* 및 주제의 *eventId*를 사용하여 실제 인터페이스에 이벤트 유형을 추가하십시오.        

3. 디바이스 유형에 실제 인터페이스 추가       

      다음 URI로 REST API PUT 메소드를 사용하여 [실제 인터페이스에 연결하도록 디바이스 유형을 업데이트](#step9)하십시오. 
     ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
     ```

4. 애플리케이션 인터페이스 작성

  1. [애플리케이션 인터페이스 스키마 파일을 작성](#step4)하십시오. 애플리케이션 인터페이스 스키마 파일은 디바이스 상태를 정의하는 로컬 .JSON 파일입니다. 

  2. 다음 URI로 REST API POST 메소드를 사용하여 [애플리케이션 인터페이스 스키마 자원을 작성](#step5)하십시오. 
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
        ```     

  3. 다음 URI로 REST API POST 메소드를 사용하여 [애플리케이션 인터페이스 스키마를 참조하는 애플리케이션 인터페이스를 작성](#step6)하십시오. 
         ```
         https://**orgId**.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces
         ```  

        애플리케이션 인터페이스는 애플리케이션 인터페이스 스키마 자원의 작성에 사용되는 POST 메소드에 대한 응답으로 리턴된 스키마 ID를 사용하여 애플리케이션 인터페이스 스키마를 참조합니다. 

  4. 다음 URI로 REST API POST 메소드를 사용하여 [디바이스 유형에 애플리케이션 인터페이스를 추가](#step10)하십시오. 
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/types/{typeId}/applicationinterfaces
        ```

        애플리케이션 인터페이스의 작성에 사용된 POST 메소드에 대한 응답을 사용하여 디바이스 유형에 애플리케이션 인터페이스를 추가하십시오. 

5. 디바이스 유형에 대한 맵핑 정의

  다음 URI로 REST API POST 메소드를 사용하여 [인바운드 이벤트의 특성을 애플리케이션 인터페이스의 특성에 맵핑하는 맵핑을 정의](#step11)하십시오.        
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/mappings/{applicationInterfaceId}
      ```

6. 디바이스 유형과 연관된 구성 배치

  다음 URI로 REST API PATCH 메소드를 사용하여 {{site.data.keyword.iot_short_notm}}에 [구성을 배치](#step15)하십시오. 
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
     ```

7. 맵핑된 디바이스 이벤트가 애플리케이션 인터페이스에 공개되었는지 확인

  1. [인바운드 디바이스 이벤트를 공개](#step12)하십시오. 

  2. 다음 URI로 REST API GET 메소드를 사용하여 [디바이스의 상태가 변경되었는지 확인](#step13)하십시오. 
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
        ```

## 예제 시나리오
{: #scenario}

다음 정보를 사용하여 두 개의 온도 센서가 {{site.data.keyword.iot_short_notm}}에 이벤트를 공개하는 시나리오를 작성할 수 있습니다. 하나의 센서는 섭씨로 온도를 측정합니다. 또 하나의 센서는 화씨로 온도를 측정합니다. 이러한 측정값은 섭씨인 하나의 온도 측정값으로 맵핑됩니다. 새 온도 측정값이 이러한 디바이스에 의해 공개되는 경우, 디바이스 상태와 연관된 특성의 값이 변경됩니다. 

### 전제조건

해당 조직에 대한 API 키 또는 토큰과 {{site.data.keyword.iot_short_notm}} 조직 인스턴스가 있어야 합니다. API 키와 토큰에 대한 자세한 정보는 [애플리케이션용 HTTP REST API](../applications/api.html#authentication)를 참조하십시오. 

### 이 시나리오에 대한 정보

이 시나리오에서는 두 개의 디바이스가 구성됩니다. 

하나의 디바이스를 *TemperatureSensor1*이라고 합니다. 이 디바이스는 섭씨로 측정되는 온도 이벤트를 공개합니다. 
온도 이벤트는 주제 `iot-2/evt/tevt/fmt/json`에서 공개되며 다음 예제 페이로드를 갖습니다. 
```
{
  "t" : 34.5
}
```

**참고:** 이벤트 ID는 *tevt*입니다. 이 ID는 이 유형의 온도 이벤트를 실제 인터페이스에 추가할 때와 이 유형의 인바운드 이벤트와 연관된 특성을 애플리케이션 인터페이스의 특성에 맵핑하는 맵핑을 정의할 때 필요합니다. 이 시나리오에서는 애플리케이션 인터페이스에 정의된 특성을 **temperature**라고 합니다. 

다른 디바이스를 *TemperatureSensor2*라고 합니다. 이 디바이스는 화씨로 측정되는 온도 이벤트를 공개합니다. 온도 이벤트는 주제 `iot-2/evt/tempevt/fmt/json`에서 공개되며 다음 예제 페이로드를 갖습니다. 
```
{
  "temp" : 72.55
}
```

**참고:** 이벤트 ID는 *tempevt*입니다. 이 ID는 이 유형의 온도 이벤트를 실제 인터페이스에 추가할 때와 이 유형의 인바운드 이벤트와 연관된 특성을 애플리케이션 인터페이스의 특성에 맵핑하는 맵핑을 정의할 때 필요합니다. 이 시나리오에서는 애플리케이션 인터페이스에 정의된 특성을 **temperature**라고 합니다. 

애플리케이션 인터페이스도 구성됩니다. 이 애플리케이션 인터페이스는 다음 구조로 이 유형의 디바이스에 대한 상태를 표시합니다. 
```
{
  "temperature" : <current temperature value in Celsius>
  }
```
이 구성은 해당 값을 섭씨로 변환한 후에 **t**와 연관된 값을 처리하고 **temp**와 연관된 값을 처리하는 애플리케이션을 구성하는 대신에 **temperature**와 연관된 값을 처리하는 애플리케이션을 구성할 수 있음을 의미합니다.

## 단계

다음 정보를 사용하면 인터페이스를 사용하여 예제 시나리오를 구성할 수 있습니다. 

### 필요하면 디바이스 유형 및 디바이스를 추가하십시오. 
{: #step14}

이 시나리오에서는 두 개의 디바이스 유형과 두 개의 디바이스 인스턴스를 가정합니다. 디바이스 인스턴스 *TemperatureSensor1*은 디바이스 유형 *EnvSensor1*과 연관되어 있습니다. 디바이스 인스턴스 *TemperatureSensor2*는 디바이스 유형 *EnvSensor2*와 연관되어 있습니다. 

REST API를 사용한 디바이스 유형 추가에 대한 정보는 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types) 문서를 참조하십시오. 

### 이벤트 스키마 파일 작성
{: #step1}

이 시나리오의 경우에는 각각의 인바운드 온도 이벤트의 구조를 정의하는 두 개의 이벤트 스키마 파일을 작성하십시오. 

다음 예제는 *tEventSchema.json*이라고 하는 스키마 파일을 작성하는 방법을 표시합니다. 이 파일은 섭씨로 온도를 측정하는 온도 센서의 인바운드 이벤트에 대한 구조를 정의합니다. 

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

스키마 파일 이름 *tEventSchema*는 이벤트 유형에 대한 이벤트 스키마 자원을 작성할 때 사용됩니다. 

다음 예제는 *tempEventSchema.json*이라고 하는 스키마 파일을 작성하는 방법을 표시합니다. 이 파일은 화씨로 온도를 측정하는 온도 센서의 인바운드 이벤트에 대한 구조를 정의합니다. 

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
스키마 파일 이름 *tempEventSchema*는 이벤트 유형에 대한 이벤트 스키마 자원을 작성할 때 사용됩니다.    

### 이벤트 유형에 대한 이벤트 스키마 자원 작성
{: #step2}

이벤트 스키마 자원을 작성하려면 다음 API를 사용하십시오. 

```
POST /schemas
```
세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas) 문서를 참조하십시오.

다음 예제는 cURL을 사용하여 이벤트 스키마 자원 *tEventSchema.json*을 작성하는 방법을 표시합니다. 

```
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
POST 메소드에 대한 응답으로 리턴된 스키마 ID *5846cd7c6522050001db0e0d*는 이벤트 유형에 이벤트 스키마를 추가할 때 필요합니다.

다음 예제는 cURL을 사용하여 이벤트 스키마 자원 *tempEventSchema.json*을 작성하는 방법을 표시합니다. 

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

### 이벤트 스키마를 참조하는 이벤트 유형 작성
{: #step3}

각각의 이벤트 유형은 이벤트 스키마 자원의 작성에 사용된 POST 메소드에 대한 응답으로 리턴된 스키마 ID를 사용하여 이전 예제에서 작성된 관련 이벤트 스키마를 참조합니다. 

이벤트 유형을 작성하려면 다음 API를 사용하십시오. 

```
POST /event/types
```

세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types) 문서를 참조하십시오.



다음 예제는 cURL을 사용하여 섭씨로 측정되는 온도 이벤트에 대한 이벤트 유형을 작성합니다. 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d"}'
```

스키마 ID *5846cd7c6522050001db0e0d*는 이벤트 유형에 이벤트 스키마를 추가하는 데 사용됩니다. 이 ID는 이벤트 스키마 자원 *tEventSchema.json*을 작성하는 데 사용된 POST 메소드에 대한 응답으로 리턴되었습니다. 

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
스키마 ID *5846cee36522050001db0e0e*는 이벤트 유형에 이벤트 스키마를 추가하는 데 사용됩니다. 이 ID는 이벤트 스키마 자원 *tempEventSchema.json*을 작성하는 데 사용된 POST 메소드에 대한 응답으로 리턴되었습니다.

다음 예제는 POST 메소드에 대한 응답을 표시합니다. 

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
POST 메소드에 대한 응답으로 리턴된 이벤트 유형 ID *5846d2846522050001db0e10*는 실제 인터페이스에 이벤트 유형을 추가하는 데 사용됩니다.

### 실제 인터페이스 작성
{: #step7}

실제 인터페이스를 작성하려면 다음 API를 사용하십시오. 

```
POST /physicalinterfaces
```
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

### 실제 인터페이스에 이벤트 유형 추가
{: #step8}

실제 인터페이스에 이벤트 유형을 추가하려면 다음 API를 사용하십시오. 

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```
세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces) 문서를 참조하십시오.

이 시나리오에서는 다음 이벤트 유형이 지정된 실제 인터페이스에 추가됩니다. 
- 섭씨 온도 이벤트 *tevt*가 주제의 *eventId* 및 이벤트 스키마 자원 작성의 *eventTypeId*를 사용하여 ID *5847d1df6522050001db0e1a*의 실제 인터페이스에 추가됩니다. 
- 화씨 온도 이벤트 *tempevt*가 주제의 *eventId* 및 이벤트 스키마 자원 작성의 *eventTypeId*를 사용하여 ID *5847d1df6522050001db0e1b*의 실제 인터페이스에 추가됩니다. 


다음 예제는 cURL을 사용하여 온도 이벤트 *tevt*를 ID *5847d1df6522050001db0e1a*의 실제 인터페이스에 추가하는 방법을 표시합니다. 

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
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
  "eventId" : "tempevt"
}
```

### 실제 인터페이스에 연결하도록 디바이스 유형 업데이트
{: #step9}

디바이스 유형를 업데이트하려면 다음 API를 사용하십시오. 

```
PUT /device/types/{typeId}
```

세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 문서를 참조하십시오. 

이 시나리오에서는 실제 인터페이스 *5847d1df6522050001db0e1a*에 연결하도록 디바이스 유형 *EnvSensor1*이 업데이트되며 실제 인터페이스 *5847d1df6522050001db0e1b*에 연결하도록 디바이스 유형 *EnvSensor2*이 업데이트됩니다. 

다음 예제는 cURL을 사용하여 디바이스 유형 *EnvSensor1*을 업데이트하는 방법을 표시합니다. 

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a"}’
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
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b"}’
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



### 애플리케이션 인터페이스 스키마 파일 작성
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

### 애플리케이션 인터페이스 스키마 자원 작성
{: #step5}

애플리케이션 인터페이스 스키마 자원을 작성하려면 다음 API를 사용하십시오. 

```
POST /schemas
```
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

### 애플리케이션 인터페이스 스키마를 참조하는 애플리케이션 인터페이스 작성
{: #step6}

애플리케이션 인터페이스를 작성하려면 다음 API를 사용하십시오. 

```
POST /applicationinterfaces
```
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

### 디바이스 유형에 애플리케이션 인터페이스 추가
{: #step10}

디바이스 유형에 애플리케이션 인터페이스를 추가하려면 다음 API를 사용하십시오. 

```
POST /device/types/{typeId}/applicationinterfaces
```
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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
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

### 인바운드 이벤트의 특성을 애플리케이션 인터페이스의 특성에 맵핑하는 맵핑 정의
{: #step11}

이벤트를 맵핑하려면 다음 API를 사용하십시오. 

```
POST /device/types/{typeId}/mappings
```
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

### 구성 배치
{: #step15}

각 디바이스 유형에 대한 디바이스 상태 업데이트와 관련된 구성을 배치하십시오. 이 구성에는 스키마, 이벤트 유형, 실제 인터페이스, 애플리케이션 인터페이스 및 맵핑이 포함됩니다. 

디바이스 유형 구성을 배치하려면 다음 API를 사용하십시오. 

```
PATCH /device/types/{typeId}
```
세부사항은 [{{site.data.keyword.iot_short_notm}} HTTP REST API](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) 문서를 참조하십시오.

이 시나리오에서는 두 개의 디바이스 유형에 대한 구성을 배치해야 합니다. 

다음 예제는 cURL을 사용하여 디바이스 유형 *EnvSensor1*에 대한 구성을 배치하는 방법을 표시합니다. 

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
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

### 인바운드 디바이스 이벤트 공개
{: #step12}

주제 `iot-2/evt/tevt/fmt/json`에서 *TemperatureSensor1*의 온도 이벤트와 주제 `iot-2/evt/tempevt/fmt/json`에서 *TemperatureSensor2*의 온도 이벤트를 공개하십시오. 

디바이스에서 인바운드 이벤트의 공개에 대한 정보는 [애플리케이션용 MQTT 연결](../applications/mqtt.html#publishing_device_events)을 참조하십시오. 


### 디바이스 상태 변경 확인
{: #step13}

디바이스 상태를 확인하려면 다음 API를 사용하십시오. 
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```
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
