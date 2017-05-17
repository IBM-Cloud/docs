---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# {{site.data.keyword.iotinsurance_short}} 시작하기
{: #gettingstarted}

{{site.data.keyword.iotinsurance_full}}는 연결된 보험 계약자의 데이터를 수집하고 관리하며 분석하는 데 사용할 수 있는 {{site.data.keyword.Bluemix_notm}} 서비스입니다. {{site.data.keyword.iotinsurance_short}}에는 개인별 맞춤 위험성 평가, 실시간 보호, 정책 비용 감소를 제공하는 기능이 있습니다.
{:shortdesc}

이 서비스를 시작하고 실행하려면 필수 서비스와 앱을 배치하고 서비스를 구성해야 합니다. [{{site.data.keyword.iotinsurance_short}} 정보](iotinsurance_overview.html)에서 아키텍처 다이어그램과 앱 및 서비스 개요를 찾으십시오. 

**전제조건:** 시작하기 전에 다음 전제조건에 부합하는지 확인하십시오. 
- [{{site.data.keyword.iotinsurance_short}} 서비스](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/)의 인스턴스가 {{site.data.keyword.Bluemix_notm}} 영역에 있어야 합니다. 
- 배치 기능을 사용하기 위해서는 최소 2GB의 여유 메모리가 {{site.data.keyword.Bluemix_notm}} 조직에 있어야 합니다. 이전 버전에서 업그레이드하는 경우 최소 2.5GB가 있어야 합니다. 

## 필수 서비스 및 애플리케이션 배치
{: #deploying_services}

1. [{{site.data.keyword.Bluemix_notm}} 콘솔](https://console.ng.bluemix.net/#all-items)에서 모든 필수 서비스와 애플리케이션을 배치하려면 {{site.data.keyword.iotinsurance_short}} 서비스를 클릭하고 **배치**를 클릭하십시오. 

  {{site.data.keyword.iotinsurance_short}}에서는 모든 서비스 및 필요한 Node.js 애플리케이션을 배치합니다. 또한, 자동으로 애플리케이션을 서비스에 바인드합니다.

  각 서비스 인스턴스는 기본 서비스 플러그인을 사용합니다. 서비스의 콘솔로 이동하여 나중에 서비스 플랜을 업그레이드할 수 있습니다. 새 인스턴스를 삭제하고 기존 인스턴스를 수동으로 {{site.data.keyword.iotinsurance_short}} 서비스에 바인드하여 서비스의 기존 인스턴스를 사용할 수도 있습니다. 애플리케이션에 대한 자세한 정보는 [{{site.data.keyword.iotinsurance_short}} 정보](iotinsurance_overview.html)의 내용을 참조하십시오. 

  **중요:** {{site.data.keyword.iotinsurance_short}}의 평가판 버전을 배치하는 경우에는 함께 배치되는 기타 서비스와 애플리케이션의 무료 버전에 기능상 제한이 있음을 유념하십시오. {{site.data.keyword.iot_short_notm}}은 최대 500개 디바이스로 제한되고, {{site.data.keyword.cloudant_short_notm}}는 1GB 데이터로 제한되며 읽기-쓰기 스레딩 기능이 제한됩니다. 

  **참고**: {{site.data.keyword.iotinsurance_short}}는 {{site.data.keyword.amafull}} 또는 {{site.data.keyword.mobilepushfull}}를 더 이상 배치하지 않습니다. {{site.data.keyword.iotinsurance_short}}의 이전 버전에서는 모바일 앱에서 응답을 처리하기 위해 {{site.data.keyword.amashort}} 서비스를 사용했습니다. 이 프로세스는 {{site.data.keyword.iotinsurance_short}}의 모든 기존 인스턴스에 대해 계속 작동합니다. 그러나 {{site.data.keyword.iotinsurance_short}}의 새 인스턴스로 모바일 앱을 사용하려면 사용자 정의 인증 프로세스를
  작성해야 합니다. 선택적으로 [{{site.data.keyword.mobilepushshort}}의 인스턴스를 작성](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)하여 구성하고 {{site.data.keyword.iotinsurance_short}} API에 바인드할 수도 있습니다.

2. {{site.data.keyword.iotinsurance_short}} 대시보드가 정상 작동하고 사용자가 API에 액세스할 수 있는지 확인하십시오. 
  1. **열기**를 클릭하여 {{site.data.keyword.iotinsurance_short}} 대시보드를 엽니다. **로그인**을 클릭하여 사전 작성된 신임 정보를 승인하십시오. 
  2. {{site.data.keyword.iotinsurance_short}} 서비스 콘솔로 돌아가서 **API**를 클릭하여 API를 확인합니다. 

  **참고:** 배치 후에 브라우저에 개별 URL을 입력하여 대시보드나 API에 직접 액세스할 수 있습니다. 이 메소드를 사용하는 경우 {{site.data.keyword.iotinsurance_short}} 서비스 신임 정보를 입력해야 합니다. 신임 정보를 찾으려면 {{site.data.keyword.iotinsurance_short}} 서비스 콘솔로 돌아가십시오. **서비스 신임 정보** 탭을 클릭한 다음 **신임 정보 보기**를 클릭하십시오. 사용자 ID와 비밀번호를 기록하십시오. 


<!--
## Configuring
{: #iot4i_configservices}



### Configuring {{site.data.keyword.amashort}}
{: #config_ama}
1. Return to your Bluemix console. All apps and services that were deployed by {{site.data.keyword.iotinsurance_short}} are displayed.

2. Copy the URL of the {{site.data.keyword.iotinsurance_short}} API application. Right-click the API application and select **Copy Link Location**.

3. Open the {{site.data.keyword.amashort}} service. The service is available in the Services section of your {{site.data.keyword.Bluemix_notm}} console.

4. Enable authentication by clicking **On**.

5. In the **Custom** section, enter the following authentication credentials:

  - **Realm name**: `IoT4I`

  - **Custom Identity Provider Url**: Paste the URL of the API application that you copied in a previous step.

  - **Your Web Application Redirect URIs**: Leave this field blank.

6. Save your settings. You can now return to the {{site.data.keyword.iotinsurance_short}} service console or your {{site.data.keyword.Bluemix_notm}} console.
-->


## {{site.data.keyword.mobilepushshort}} 작성 및 구성
{: #config_push}

(선택사항) 기존 모바일 앱에서 푸시 알림을 사용하려면 {{site.data.keyword.mobilepushshort}} 서비스의 인스턴스를 선택적으로 작성하고, 이를 {{site.data.keyword.iotinsurance_short}} API에 바인드한 뒤, 공개 키 암호 표준(PKCS) 12 파일을 추가할 수 있습니다. 모바일 앱에 대한 정보는 [샘플 모바일 앱 설치 및 연결](iotinsurance_mobile_app.html)을 참조하십시오. {{site.data.keyword.mobilepushshort}}에 대한 정보는 [Push Notifications 시작하기](https://console.ng.bluemix.net/docs/services/mobilepush/index.html)를 참조하십시오. 

작성 후에 서비스를 구성하려면 다음 단계를 수행하십시오. 

  1. {{site.data.keyword.mobilepushshort}} 서비스를 여십시오. 
  2. **구성**을 클릭하십시오. 
  3. Apple 푸시 알림 인증서 섹션에 모바일 앱에 해당하는 PKCS 12 파일을 업로드한 후 비밀번호를 입력하십시오. 

## Weather Company 데이터 사용
{: #weather_company}

(선택사항) {{site.data.keyword.iotinsurance_short}}는 사용자가 데모 용도로 볼 수 있는 Weather Company의 정적 데이터 세트를 제공합니다. [{{site.data.keyword.weatherfull}} 서비스](../Weather/index.html)의 인스턴스를 작성하고 이를 {{site.data.keyword.iotinsurance_short}} 날씨 앱에 바인딩하여 Weather Company의 라이브 데이터에 선택적으로 액세스할 수도 있습니다. 

**중요:** {{site.data.keyword.weather_short}} 서비스의 무료 버전은 10,000개 요청으로 제한됩니다. 추가 요청이 필요하면 유료 버전으로 업그레이드할 수 있습니다. 

다음에 수행할 작업
{: #whats_next}
{{site.data.keyword.iotinsurance_short}}에서 수행할 수 있는 작업을 알아보십시오. 

- 실드 툴킷의 API와 지시사항을 사용하여 [사용자 및 실드 연관](iotinsurance_shield_toolkit.html)을 작성하십시오. 
<!-- - Install and connect the [sample mobile app](iotinsurance_mobile_app.html). -->
- [GitHub 사이트의 API 예제 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}를 모두 다운로드하거나 보십시오. 
