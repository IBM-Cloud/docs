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
{:tip: .tip}

# SMS 및 음성 메시징 사용
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}}는 SMS 및 음성 메시징을 사용할 수 있도록 Twilio와의 통합을 지원합니다. Twilio는 사용자가 {{site.data.keyword.Bluemix_notm}} 대시보드에서 설치할 수 있는 써드파티 애플리케이션입니다.
{: shortdesc}

## 전제조건
음성 메시징을 사용하려면 권한 부여된 Twilio 계정과 Twilio 발신(call-from) 전화번호가 있어야 합니다. Twilio 무료 계정을 사용하는 경우에는 호출이나 메시지의 수신을 위한 전화번호의 권한 부여도 필요합니다. 자세한 정보는 [Twilio 문서 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://support.twilio.com/hc/en-us/articles/223136107-How-does-Twilio-s-Free-Trial-work-){:new_window}를 참조하십시오. 

## Twilio 인스턴스 작성 및 구성
1. {{site.data.keyword.iotinsurance_short}}를 설치한 동일한 {{site.data.keyword.Bluemix_notm}} 조직과 영역에서 Twilio 인스턴스를 작성하십시오. 
    1. [{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net)에 로그인하십시오. 
    2. **카탈로그** 탭을 선택하십시오. 
    3. 서비스 카탈로그의 모바일 섹션을 찾아서 **Twilio**를 클릭하십시오. 

    **팁:** Twilio 페이지로 직접 이동하려면 [여기 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://console.ng.bluemix.net/catalog/services/twilio/){: new_window}를 클릭하십시오.
    {: tip}

    4. Twilio 페이지에서 다음과 같이 신임 정보를 제공하고 애플리케이션을 바인드하십시오. 

      1. 서비스 이름으로 `Twilio-00`을 입력하십시오. **중요:** {{site.data.keyword.iotinsurance_short}} 연결에 성공하려면 `Twilio-00`을 사용해야 합니다. 

      2. Twilio 신임 정보를 입력하십시오. 

      3. **연결 대상** 메뉴에서 iot4i-action-engine 애플리케이션을 선택하여 Twilio 인스턴스를 {{site.data.keyword.iotinsurance_short}}에 바인드하십시오. 

      4. **작성**을 클릭하십시오.   

    Twilio 애플리케이션이 사용자 환경에 설치됩니다. 바인딩을 적용하려면 iot4i-action-engine 애플리케이션을 다시 스테이징하거나 다시 시작하라는 메시지가 프롬프트됩니다. 지금 다시 시작하거나, 다음 단계에서 새 환경 변수를 추가할 때까지 다시 시작을 대기할 수 있습니다. 

2. iot4i-action-egine 컴포넌트에 대해 TWILIO_FROM_NUMBER라고 하는 환경 변수를 작성하십시오. 
    1. Bluemix 대시보드에서 iot4i-action-engine 애플리케이션을 여십시오. 
    2. **런타임**을 선택한 후에 **환경 변수**를 클릭하십시오. 
    3. **사용자 정의** 섹션에서 **추가**를 클릭하십시오. 
    4. 이름 열에서 `TWILIO_FROM_NUMBER`를 입력한 후에 값 열에서 Twilio 음성 및 SMS 가능 번호를 입력하십시오. 
    5. **저장**을 클릭하십시오. 

3. 라우트 단추 옆에 있는 다시 시작 아이콘을 클릭하여 Iot4i-action-engine 애플리케이션을 다시 시작하십시오. 

## SMS 및 음성 조치를 실드에 추가

SMS 및 음성 기능을 실드에 추가하려면 실드 정의에 다음 조치를 추가해야 합니다. 
  - `send-sms`
  - `phone-call`

조치 목록이 포함된 실드의 예제는 [샘플 실드 작성 예제 ![외부 링크 아이콘](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/blob/master/bl/shield.js){:new_window}를 참조하십시오. 예제에서 SMS 및 음성 조치는 `email` 및 `pushios` 조치가 포함된 조치 목록에 추가될 수 있습니다. 

실드 작성에 대한 자세한 정보는 [실드 툴킷 사용](iotinsurance_shield_toolkit.html)을 참조하십시오. 
