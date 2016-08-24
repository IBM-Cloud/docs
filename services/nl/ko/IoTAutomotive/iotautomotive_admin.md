---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.iot4auto_short}} 관리
{: #1stanchor}
마지막 업데이트 날짜: 2016년 7월 29일
{: .last-updated}

{{site.data.keyword.Bluemix_notm}} 대시보드의 관리 콘솔을 사용하여 {{site.data.keyword.iot4auto_full}} 서비스 인스턴스를 관리하십시오. 관리 콘솔에서 {{site.data.keyword.iot4auto_short}}의 매개변수를 구성하고 서비스에 저장된 데이터를 관리할 수 있습니다. 또한 테넌트 정보를 보고 테넌트 비밀번호를 재설정할 수 있습니다.

{:shortdesc}

## 관리 콘솔 시작
{: #start_admin_console}

{{site.data.keyword.iot4auto_short}} 서비스의 관리 콘솔에 액세스하려면 다음을 수행하십시오.

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.iot4auto_short}} 서비스 타일을 클릭하십시오.
2. 서비스 인스턴스의 **관리** 보기를 선택하십시오.
나중에 필요하므로 사용자 이름 및 비밀번호 신임 정보를 기록해 두십시오. 관리 콘솔에 액세스하려면 IBM ID가 필요하며, 이는 {{site.data.keyword.Bluemix_notm}} 신임 정보와 동일하지 않을 수 있습니다.
3. **실행**을 클릭하고 프롬프트가 표시되면 IBM ID 신임 정보를 입력하십시오.
4. **로그인**을 클릭하십시오. **관리 콘솔** 창이 열립니다.

## 테넌트 정보 관리
{: #view_tenant_info}

테넌트 정보를 보려면 **Tenant Information**을 클릭하십시오.

### 테넌트 비밀번호 재설정
{: #reset_tenant_password}

테넌트 비밀번호를 재설정하려면 다음을 수행하십시오.

1. **Tenant Information** 창에서 **RESET**을 클릭하십시오.
2. 대화 상자에서 **OK**를 클릭하십시오.
새 비밀번호가 생성되어 **Tenant Information** 보기에 표시됩니다.
**중요:** {{site.data.keyword.iot4auto_short}} API에 액세스하는 모든 애플리케이션에서 비밀번호를 업데이트하십시오.

## 서비스 매개변수 구성
{: #configure_parameters}

서비스 매개변수는 운행 데이터가 분석되는 방식을 제어합니다. 서비스 매개변수를 수정하려면 다음을 수행하십시오.

1. **Parameters** 보기를 열고 다음 서비스 매개변수를 조정하십시오.
  - **Behavior** 탭을 클릭하고 요구사항에 맞게 [운전 행동 매개변수](#behavior_parameters)를 업데이트하십시오.
  - **Context** 탭을 클릭하고 요구사항에 맞게 [컨텍스트 맵핑 매개변수](#context_parameters)를 업데이트하십시오.
2. **SAVE**를 클릭하십시오.
3. **OK**를 클릭하십시오.

업데이트된 매개변수 값은 다음으로 제출되는 작업에 적용됩니다.

### 운전 행동 매개변수
{: #behavior_parameters}


다음 표에서는 **Behavior** 탭에서 구성할 수 있는 카테고리의 운전 행동 매개변수를 설명합니다.

#### 제한 속도 설정

각 도로 유형의 제한 속도를 km/h 단위로 지정할 수 있습니다. 속도가 도로 유형에 지정된 제한 속도 값을 초과하면 과속이 발견됩니다.

|매개변수 이름|설명|기본값(km/h)|
|:--------|:--------|:-------|
|Motorway|Motorway 도로 유형의 제한 속도|120|
|Urban Highway|Urban Highway 도로 유형의 제한 속도|90|
|Urban Primary|Urban Primary 도로 유형의 제한 속도|60|
|Urban Road|Urban Road 도로 유형의 제한 속도|40|
|Others|'Others'로 분류된 도로 유형의 제한 속도|30|
|Unknown|Unknown 도로 유형의 제한 속도|120|
*표 1. 제한 속도 구성 매개변수*

#### 회전 설정

|매개변수 이름|설명|기본값|
|:--------|:--------|:-------|
|Angular Velocity (Min \- Max, deg/s)|회전의 일반 각속도 값입니다. 최소값은 회전 세그먼트를 식별하는 임계값으로 사용됩니다. 최대값은 급회전 행동을 발견하는 데 사용됩니다.|10 \- 25|
|Average Speed (km/h)|회전 중의 일반 속도입니다. 이 값은 각속도 값이 있는 회전 세그먼트의 행동을 식별하는 데 사용됩니다.|60|
*표 2. 차량 회전 구성 매개변수*

#### 피로운전 설정

|매개변수 이름|설명|기본값|
|:--------|:--------|:-------|
|Time of Continuous Driving (s)|허용된 최대 연속 운전 시간입니다.|10800|
*표 3. 피로운전 발견 구성 매개변수*

### 컨텍스트 맵핑 매개변수
{: #context_parameters}

다음 표에서는 **Context** 탭에서 구성할 수 있는 카테고리의 컨텍스트 맵핑 매개변수를 설명합니다.

#### 시간대 및 시간 범위 설정

시간대 및 각 기간의 시간을 지정하십시오.

|매개변수 이름|설명|기본값|
|:--------|:--------|:-------|
|Analysis time zone|분석에 적용된 시간대입니다. |+00:00|
|Day Time|낮의 시간 범위입니다.|1030 \- 1730|
|Night Time|밤의 시간 범위입니다.|2030 \- 0700|
|Morning Peak|아침 피크 시간의 시간 범위입니다.|0700 \- 1030|
|Evening Peak|저녁 피크 시간의 시간 범위입니다.|1730 \- 2030|
*표 4. 시간대 및 범위 구성 매개변수*

#### 도로 유형

도로 유형 매개변수는 입력 데이터의 도로 유형 값을 {{site.data.keyword.iot4auto_short}} 도로 유형 분류에 맵핑하는 데 사용됩니다. 도로 유형 값이 없으면 {{site.data.keyword.iotmapinsights_short}} 서비스에서 제공하는 `getLinkInformation` REST API 명령을 사용하여 도로 유형 값을 검색할 수 있습니다.

[`getLinkInformation`의 샘플 JSON 응답](#sampleJson)에서 개략적으로 설명한 것처럼, 도로 유형 값이 리턴되어 `getLinkInformation` JSON 응답의 특성 섹션에 저장되며 `type`으로 정의됩니다.


|매개변수 이름|설명|기본값|
|:--------|:--------|:-------|
|Motorway|Motorway에 맵핑된 도로 유형 값입니다.|1|
|Urban Highway|Urban Highway에 맵핑된 도로 유형 값입니다.|2|
|Urban Primary|Urban Primary에 맵핑된 도로 유형 값입니다.|3|
|Urban Road|Urban Road에 맵핑된 도로 유형 값입니다.|4|
|Others|Others에 맵핑된 도로 유형 값입니다.|5|
*표 5. 도로 유형 구성 매개변수*

#### 속도 임계값

속도 임계값 매개변수가 각 도로 유형의 중간 속도 범위를 km/h로 정의합니다. 중간 속도 범위는 지정된 가장 낮은 값과 가장 높은 값 사이의 범위입니다.

|매개변수 이름|설명|기본값|
|:--------|:--------|:-------|
|Motorway|Motorway 도로 유형의 중간 속도 범위입니다.|55 \- 85|
|Urban Highway|Urban Highway 도로 유형의 중간 속도 범위입니다.|35 \- 65|
|Urban Primary|Urban Primary 도로 유형의 중간 속도 범위입니다.|20 \- 40|
|Urban Road|Urban Road 도로 유형의 중간 속도 범위입니다.|15 \- 35|
|Others|Others 도로 유형의 중간 속도 범위입니다.|10 \- 20|
|Unknown|Unknown 도로 유형의 중간 속도 범위입니다.|20 \- 60|
*표 6. 속도 임계값 구성 매개변수*


### `getLinkInformation`의 샘플 JSON 응답
{: #sampleJson}

다음 코드 샘플에서는 `getLinkInformation` REST API 명령에 대한 JSON 응답의 예를 제공합니다.

```
{
	"links": [{
		"internal_link_id": "32088220365736308",
		"external_link_id": "3846419005",
		...
		"properties": {
			"type": "5",
			...
		},
		...
	}]
}
```
{: screen}

## 서비스에 저장된 데이터 삭제
{: #managedata}

자동차 프로브 데이터, 컨텍스트 데이터 및 분석 결과는 삭제될 때까지 서비스에 저장됩니다.

서비스에 저장된 데이터를 삭제하려면 다음을 수행하십시오.

1. 자동차 프로브 및 분석 결과 데이터를 보려면 **Data Management**를 클릭하십시오.
2. 레코드를 선택한 다음 **DELETE**를 클릭하십시오.
