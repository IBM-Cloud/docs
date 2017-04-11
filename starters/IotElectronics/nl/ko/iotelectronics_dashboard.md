---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-10"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 데이터 및 디바이스 관리
{: #iot4e_dashboard}
{{site.data.keyword.iotelectronics}} 대시보드를 사용하여 등록된 디바이스의 데이터를 보고
{{site.data.keyword.iot_full}}의 디바이스 및 사용자를 관리하십시오.
{:shortdesc}

{{site.data.keyword.iotelectronics}} 대시보드를 사용하여 다음을 수행하십시오.
- 조직에 등록된 어플라이언스 보기
- 어플라이언스에 사용자 맵핑
- 많은 수의 어플라이언스 추가 및 삭제와 같은 대량 조치 수행
- 어플라이언스 데이터 추출

## 대시보드 열기
{: #iot4e_opendashboard}

**중요:** 처음으로 대시보드를 사용하기 전에 먼저 [이를 사용하도록 설정](#iot4e_enabledashboard)해야 합니다.

대시보드를 열려면
1. {{site.data.keyword.Bluemix_notm}} 대시보드를 열고 {{site.data.keyword.iot_short_notm}} 서비스의 이름을 클릭하십시오.  

    **팁:** 서비스 이름은 `iotf-service`로 끝나며 서비스 오퍼링 열에서 *Internet of Things Platform*으로 설명되어 있습니다.
2. 시작 페이지에서 **실행**을 클릭하십시오.
3. 메뉴에서 **가전제품**을 선택하십시오.

## 대시보드 사용 설정
{: #iot4e_enabledashboard}

다음 단계를 수행하여 {{site.data.keyword.iot_full}} 내에서 {{site.data.keyword.iotelectronics}} 대시보드를 사용으로 설정하십시오.

  **참고:** 시작하기 전에 {{site.data.keyword.Bluemix_notm}} 조직에 {{site.data.keyword.iotelectronics}} Starter의 인스턴스를 배치해야 합니다. 스타터의 인스턴스를 배치하면 {{site.data.keyword.iot_short_notm}}를 포함하여 해당 컴포넌트 애플리케이션 및 서비스가 자동으로 배치됩니다. 

1. {{site.data.keyword.iot_short_notm}} API 키에 새 역할을 추가하십시오.
  1. {{site.data.keyword.Bluemix_notm}} 대시보드를 열고 {{site.data.keyword.iot_short_notm}} 서비스의 이름을 클릭하십시오.  

    **팁:** 서비스 이름은 `iotf-service`로 끝나며 서비스 오퍼링 열에서 *Internet of Things Platform*으로 설명되어 있습니다.
  2. 시작 페이지에서 **실행**을 클릭하십시오.
  3. 메뉴에서 **앱** ![앱 아이콘](images/IOT_Icons_apps2.svg "앱 아이콘")을 선택한 다음 API 키 옆의 편집 아이콘 ![편집 아이콘](images/IOT_Icons_Edit_Active_50.svg "편집 아이콘")을 클릭하십시오.
  4. **다른 역할 추가**를 클릭하고 **오퍼레이션 애플리케이션**을 선택하십시오.
  5. **저장**을 클릭하십시오.

    ![API 역할](images/IoT4E_API_roles.svg "API 역할")

2. {{site.data.keyword.iot_short_notm}} 조직 ID, API 키 및 인증 코드를 찾으십시오.
  1. {{site.data.keyword.Bluemix_notm}} 대시보드로 돌아가십시오.
  2. {{site.data.keyword.iotelectronics}} 애플리케이션을 여십시오.

    **팁:** 애플리케이션은 {{site.data.keyword.Bluemix_notm}} 대시보드의 애플리케이션 섹션에 있습니다. 라우트가 아닌 이름을 클릭하십시오.
  3. **런타임**을 클릭한 다음 **환경 변수**를 선택하여 환경 변수를 표시하십시오.
  4. `iotf-service`로 레이블 지정된 섹션까지 스크롤하십시오. 다음 값을 복사하십시오. 다음 단계에 필요합니다.

    - `org` - {{site.data.keyword.iot_short_notm}} 조직 ID
    - `apiKey` - {{site.data.keyword.iot_short_notm}} API 키
    - `apiToken` - {{site.data.keyword.iot_short_notm}} 인증 토큰  

    ![API 인증 신임 정보](images/IoT4E_IoTFcred.svg "API 인증 신임 정보")

3. {{site.data.keyword.iotelectronics}} 서비스에서 {{site.data.keyword.iot_short_notm}} 신임 정보를 입력하십시오.

  1. {{site.data.keyword.Bluemix_notm}} 대시보드로 돌아가십시오.
  2. 서비스 이름을 클릭하여 {{site.data.keyword.iotelectronics}} 서비스를 여십시오.

    **팁:** 서비스 이름은 `ibmiotforelectronics`로 끝나며 서비스 오퍼링 열에서 *IoT for Electronics*로 설명되어 있습니다.
  3. 시작 페이지에 이전 단계에서 찾은 API 키, 인증 토큰 및 조직 ID를 입력하십시오.
  4. **업데이트**를 클릭하여 항목을 저장하십시오.

    ![플랫폼 구성](images/IoT4E_Platform_config.svg "플랫폼 구성")

4. 이제 {{site.data.keyword.iot_short_notm}}에서 [{{site.data.keyword.iotelectronics}} 대시보드 열기](#iot4e_opendashboard)를 수행할 수 있습니다.
