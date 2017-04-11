---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# 디바이스 모델
{: #device_model}

디바이스 모델은 디바이스의 관리 특성 및 메타데이터에 대해 설명합니다. {{site.data.keyword.iot_full}}의 디바이스 데이터베이스는
디바이스 정보의 마스터 소스입니다. 애플리케이션과 관리 디바이스는 위치 변경 등의 업데이트 또는 펌웨어 업데이트 진행상태를 디바이스 데이터베이스로 보낼 수 있습니다. {{site.data.keyword.iot_short_notm}}에서 이러한 업데이트를 받는 즉시 데이터베이스가 업데이트되고 애플리케이션에서 정보를 사용할 수 있게 됩니다.

**참고:** [디바이스 관리 확장기능](#devicemanagementextension)을 제외하고 전체 디바이스 모델은 관리 디바이스와 비관리 디바이스 모두에 사용 가능합니다. 그러나 비관리 디바이스는 데이터베이스에서 디바이스 모델을 직접 업데이트할 수 없습니다.

## 디바이스 ID
{: #device_id}

모든 디바이스에 `typeId` 및 `deviceId` 속성이 있습니다. 일반적으로 `typeId`는 디바이스의 모델을 나타내는 반면 `deviceId`는 일련 번호를 나타낼 수 있습니다. {{site.data.keyword.iot_short_notm}}
조직에서 `typeId`와 `deviceId` 조합은 디바이스마다 고유해야 합니다.

이러한 속성 외에 {{site.data.keyword.iot_short_notm}}은 각 디바이스에 다른 ID를 생성합니다. 이 ID를 `clientId`라고 합니다. `clientId`는 `organizationId` 및 디바이스의 `typeId`와 `deviceId` 값을 기반으로 합니다. `clientId`는 개별 디바이스를 고유하게 식별하는 방법을 제공합니다. 통신 프로토콜 및 REST API와 호환 가능하도록 이 ID에서 사용할 수 있는 문자는 제한됩니다. 

다음 선택적 디바이스 ID도 사용할 수 있습니다.

- deviceInfo.manufacturer
- deviceInfo.serialNumber
- deviceInfo.model
- deviceInfo.deviceClass
- deviceInfo.description

ID에 대한 자세한 정보와 다른 디바이스 관리 표준에 정의된 상대 ID에 대한 설명은 [속성](#attributes)을 참조하십시오.


## ID 및 디바이스 유형
{: #id_and_device_types}

{{site.data.keyword.iot_short_notm}}에 연결된 모든 디바이스는 디바이스 유형과 연관되어 있습니다. 디바이스 유형은 특성 또는 동작을 공유하는 디바이스 그룹입니다.

디바이스 유형에는 속성 세트가 있습니다. {{site.data.keyword.iot_short_notm}}에 디바이스가 추가되면 해당 디바이스 유형의 속성을 템플리트로 사용합니다. 디바이스에 값이 있으면 이 값이 사용됩니다. 디바이스에 값이 없으면 디바이스 유형 값이 사용됩니다. 예를 들어, 디바이스 유형에 `deviceInfo.fwVersion` 속성 값이 있으며 이 값은 제조 시 펌웨어 버전을 반영합니다. 디바이스가 추가되면 이 값이 디바이스 유형에서 디바이스로 복사됩니다. 디바이스가 추가될 때 `deviceInfo.fwVersion` 값이 이미 있으면 값을 겹쳐쓰지 않습니다.

디바이스 유형의 속성을 업데이트할 때 등록된 새 디바이스만 디바이스 유형 템플리트의 수정사항을 상속합니다.

## 속성
{: #attributes}

다음 표에서는 {{site.data.keyword.iot_short_notm}}의 디바이스에 적용할 수 있는 속성 목록을 표시합니다. 이탤릭체 속성은 디바이스 유형에도 적용될 수 있습니다.

키:
  - API : API를 사용하여 업데이트할 수 있음
  - DMA : 디바이스 관리 에이전트를 사용하여 업데이트할 수 있음
  - R: 읽기 전용
  - W: 쓰기 및 읽기
  - A: 추가

속성                         | 유형       | 설명                                        | API | DMA   
------------- | ------------- | ------------- | ------------- | -------------  |
 clientId                         | 문자열     | MQTT 연결에 사용되는 클라이언트 ID          |  R  |   -  
 *typeId*                         | 문자열     | 디바이스 유형                                       |  R  |   -  
 deviceId                         | 문자열     | 디바이스 ID                                         |  R  |    -
 classId                          | 문자열     | 디바이스 클래스("디바이스" 또는 "게이트웨이")           |  R  |   -  
 gatewayTypeId                    | 문자열     | 이 디바이스가 사용 중인 게이트웨이의 유형 ID       |  R  |    -
 gatewayId                        | 문자열     | 이 디바이스가 사용 중인 게이트웨이의 디바이스 ID     |  R  |   -  
 status.alert                     | 부울       | 디바이스에 경보가 있는지 여부 표시                   |  W  |  -   
 *deviceInfo.serialNumber*        | 문자열     | 디바이스의 일련 번호                   |  W  |  W    
 *deviceInfo.manufacturer*        | 문자열     | 디바이스의 제조업체                    |  W  |  W   
 *deviceInfo.model*               | 문자열     | 디바이스의 모델                           |  W  |  W  
 *deviceInfo.deviceClass*         | 문자열     | 디바이스의 클래스                           |  W  |  W  
 *deviceInfo.description*         | 문자열     | 디바이스의 설명 이름                |  W  |  W  
 *deviceInfo.fwVersion*           | 문자열     | 디바이스에 있는 것으로 현재 알려진 펌웨어 버전    |  W  |  W  
 *deviceInfo.hwVersion*           | 문자열     | 디바이스의 하드웨어 버전                |  W  |  W  
 *deviceInfo.descriptiveLocation* | 문자열     | 방, 빌딩 번호 또는 지역 등의 설명적 위치      |  W  |  W  
 *metadata*                       | 복합    | 자유 양식 메타데이터                                |  W  |  W  
 added.auth.id                    | 문자열     | 디바이스를 추가한 ID                          |  R  |   -  
 added.dateTime                   | 문자열     | ISO8601 date-time: 디바이스가 추가된 날짜 및 시간 |  R  |    -
 refs.diag.errorCodes             | 문자열     | 표시된 경우 오류 코드에 대한 진단 확장기능의 URI |  R  |   -  
 refs.diag.logs                   | 문자열     | 표시된 경우 로그에 대한 진단 확장기능의 URI        |  R  |   -  
 refs.location                    | 문자열     | 표시된 경우 위치 확장기능의 URI             |  R  |   -  
 refs.mgmt                        | 문자열     | 표시된 경우 디바이스 관리 확장기능의 URI                 |  R  |    -



## 확장 속성
{: #extended_attributes}

위의 속성 섹션에 나열된 코어 속성 외에도 코어 디바이스 모델의 확장기능으로
처리되는 추가 속성이 있습니다. 디바이스에 대한 단순 조회에서는 코어 디바이스
모델에서 정보를 리턴하지만 확장기능은 아닙니다. 확장기능의
정보는 특별히 요청해야 합니다.


확장기능 이름    | 속성의 접두부 | 용도      
------------- | ------------- | -------------                                         
 진단       | diag                 | 오류 로그 및 진단 정보                 
 위치          | location             | 잠재적으로 정기 업데이트될 디바이스의 위치
 디바이스 관리 | mgmt                 | 디바이스 관리 조치(예: 펌웨어 업데이트)       


### 진단 확장기능


진단 속성이 선택적이고 오류 로그 정보가 포함된 디바이스에 대해서만 표시됩니다. 이러한 속성은 {{site.data.keyword.iot_short_notm}}에 대한 연결 문제점을 해결하지 않고 디바이스 문제점을 진단하는 데 사용합니다. 진단 속성에 저장된 정보의 양이 매우 많을 수 있으므로 특별히 조회해야 합니다.

진단 로그 정보는 항목의 배열로 저장됩니다. 각 항목은 메시지, 심각도의 표시, 시간소인 및 데이터의 선택적 바이트-배열로 구성됩니다. API를 사용하여 항목을 추가할 수 있습니다. 하지만 항목을 추가하면 진단 로그의 크기를 관리 가능하도록 유지하기 위해 이전 항목이 유실될 수 있습니다.


속성             | 유형       | 설명                                                  | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 diag.errorCodes[]    | 정수 </br> 배열  | 오류 코드의 배열                                        |  A  |  A  
 diag.log[]           | 배열      | 진단 데이터의 배열                                    |  A  |  A  
 diag.log[].message   | 문자열     | 진단 메시지                                          |  -   |    -
 diag.log[].timestamp | 문자열     | ISO8601 date-time: 로그 항목의 날짜 및 시간               |  -   |    -
 diag.log[].logData   | 문자열     | 바이트: 진단 데이터, base-64 인코딩됨                      |  -   |    -
 diag.log[].severity  | 수     | 메시지의 심각도, 0: 정보용, 1: 경고, 2: 오류 |  -   |    -


### 위치 확장기능

위치 속성은 선택적이고 위치 정보가 포함된 디바이스에 대해서만 표시됩니다. 위치 정보는 동적 정보에 더 잘 맞는 스토리지 메커니즘을 사용할 수 있도록 별도로 저장됩니다. 이는 정보가 자주 업데이트되는 경우에(예: 모바일 디바이스의 경우) 중요합니다.

빈번한 위치 업데이트가 매우 중요한 솔루션의 경우 위치를 디바이스 이벤트 페이로드의 일부로 처리하여 업데이트 비율을 높이고 간단한 히스토리 스토리지와 쉬운 데이터 분석이 가능하게 해야 합니다.


속성                  | 유형   | 설명                                              | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 location.longitude        | 수 | WGS84를 사용한 DD(Decimal degrees) 방식의 경도                |  W  |  W  
 location.latitude         | 수 | WGS84를 사용한 DD(Decimal degrees) 방식의 위도                 |  W  |  W  
 location.elevation        | 수 | WGS84를 사용한 미터로 된 고도                         |  W  |  W  
 location.measuredDateTime | 문자열 |ISO8601 date-time: 위치 측정의 날짜 및 시간 |  W  |  W  
 location.updatedDateTime  | 문자열 | ISO8601 date-time: 날짜 및 시간                        |  R  |   
 location.accuracy         | 수 | 미터로 된 위치의 정확도                      |  W  |  W  


### 디바이스 관리 확장기능
{: #devicemanagementextension}

관리 속성은 관리 디바이스에만 있습니다. 관리 디바이스가 휴면 상태가 되면 비관리 디바이스가 되고 `mgmt.` 속성이 삭제됩니다. `mgmt.` 속성은 디바이스 관리 요청을 처리한 결과 {{site.data.keyword.iot_short_notm}}에서 설정합니다. 이러한 속성은 API를 사용하여 직접 작성할 수 없습니다.

디바이스에는 해당 상태가 관리 디바이스로 정의된 관리 라이프사이클이 있습니다. 디바이스의 디바이스 관리 에이전트는 디바이스 관리 프로토콜을 통해 디바이스 관리 요청 전송을 담당합니다. 대규모 디바이스 모집단에서 존재하지 않는 디바이스를 처리하려면 정기적으로 디바이스 관리 요청을 보내도록 관리 디바이스를 설정할 수 있습니다. 지정된 시간 동안 {{site.data.keyword.iot_short_notm}}에 이 요청을 보내지 않으면 관리 디바이스는 휴면 상태가 됩니다. 이 기능을 쉽게 사용하도록 디바이스 관리 요청에 선택적 lifetime 매개변수가 있습니다. {{site.data.keyword.iot_short_notm}}이 lifetime 매개변수 세트가 있는 디바이스 관리 요청을 받으면 다른 디바이스 관리 요청이 필요하기 전까지의 시간을 계산하여 `mgmt.dormantDateTime` 속성에 저장합니다.


속성                      | 유형    | 설명                              | API | DMA
------------- | ------------- | ------------- | ------------- | -------------
 mgmt.dormant                   | 부울    | 디바이스가 휴면 상태가 되었는지 여부 표시                  |  R  |  -
 mgmt.dormantDateTime           | 문자열  | ISO8601 date-time: 관리 디바이스가 휴면 상태가 되는 날짜 및 시간   |  R  |  -   
 mgmt.lastActivityDateTime      | 문자열  | ISO8601 date-time: 마지막 활동의 날짜 및 시간으로 정기적으로 업데이트됨    |  R  |    -
 mgmt.supports.deviceActions    | 부울    | 디바이스가 재부팅 및 팩토리 재설정 조치를 지원하는지 여부 표시  |  R  |   -  
 mgmt.supports.firmwareActions  | 부울    | 디바이스가 펌웨어 다운로드 및 펌웨어 업데이트 조치를 지원하는지 여부 표시    |  R  |     -
 mgmt.firmware.version          | 문자열  | 디바이스의 펌웨어 버전              |  R  |  W  
 mgmt.firmware.name             | 문자열  | 디바이스에서 사용되는 펌웨어의 이름      |  R  |  W  
 mgmt.firmware.uri              | 문자열  | 펌웨어 이미지를 다운로드할 수 있는 URI |  R  |  W  
 mgmt.firmware.verifier         | 문자열  | 무결성을 유효성 검증하는 데 사용되는 펌웨어 이미지에 대한 체크섬 등의 검사기 |  R  |  W  
 mgmt.firmware.state            | 수  | 펌웨어 다운로드의 상태를 표시함               |  R  |  W  
 mgmt.firmware.updateStatus     | 수  | 업데이트의 상태를 표시함                     |  R  |  W  
 mgmt.firmware.updatedDateTime  | 문자열  | ISO8601 date-time: 마지막 업데이트의 날짜                 |  R  |    -
