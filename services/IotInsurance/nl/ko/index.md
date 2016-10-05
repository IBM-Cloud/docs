---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# {{site.data.keyword.iotinsurance_short}}(베타) 시작하기
{: #iotins_gettingstarted}
마지막 업데이트 날짜: 2016년 9월 12일
{: .last-updated}

{{site.data.keyword.iotinsurance_full}}는 연결된 보험 계약자의 데이터를 수집하고 관리하며 분석하는 데 사용할 수 있는 {{site.data.keyword.Bluemix_notm}} 서비스입니다. {{site.data.keyword.iotinsurance_short}}에는 개인별 맞춤 위험성 평가, 실시간 보호, 정책 비용 감소를 제공하는 기능이 있습니다.
{:shortdesc}

이 서비스를 시작하고 실행하려면 필수 서비스와 앱을 배치하고 서비스를 구성해야 합니다. 

**전제조건** 시작하기 전에 다음 전제조건에 부합하는지 확인하십시오. 
- [{{site.data.keyword.iotinsurance_short}} 서비스](https://new-console.ng.bluemix.net/catalog/services/iot-for-insurance/)의 인스턴스가 {{site.data.keyword.Bluemix_notm}} 영역에 있어야 합니다. 
- 컴퓨터에서 10GB 이상의 스토리지를 사용할 수 있어야 합니다. 

## 필수 서비스 및 애플리케이션 배치
{: #deploying_services}

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 모든 필수 서비스와 애플리케이션을 배치하려면 {{site.data.keyword.iotinsurance_short}} 서비스 타일을 클릭하고 **배치**를 클릭하십시오. 

  {{site.data.keyword.iotinsurance_short}}에서는 모든 서비스 및 필요한 Node.js 애플리케이션을 배치합니다. 또한, 자동으로 애플리케이션을 서비스에 바인드합니다.

  각 서비스 인스턴스는 기본 서비스 플러그인을 사용합니다. 서비스의 콘솔로 이동하여 나중에 서비스 플랜을 업그레이드할 수 있습니다. 새 인스턴스를 삭제하고 기존 인스턴스를 수동으로 {{site.data.keyword.iotinsurance_short}} 서비스에 바인드하여 서비스의 기존 인스턴스를 사용할 수도 있습니다. 애플리케이션에 대한 자세한 정보는 [{{site.data.keyword.iotinsurance_short}} 정보](iotinsurance_overview.html)의 내용을 참조하십시오. 

2. 모든 서비스 및 앱이 작성되었으며 올바로 작동하는지 확인하십시오. {{site.data.keyword.Bluemix_notm}} 대시보드에서 모든 앱의 상태가 `실행 중`인지 확인하십시오. 

3. {{site.data.keyword.iotinsurance_short}} 대시보드가 정상 작동하고 사용자가 API에 액세스할 수 있는지 확인하십시오. 
  1. {{site.data.keyword.iotinsurance_short}} 서비스 타일을 클릭한 후 **서비스 신임 정보** 탭을 선택하십시오. 
  2. **서비스 신임 정보 보기**를 클릭하고 사용자 ID와 비밀번호를 기록해두십시오. 다음 단계에서 이러한 신임 정보를 사용합니다.
  3. **관리** 탭을 선택하고 **열기**를 클릭하여 {{site.data.keyword.iotinsurance_short}} 대시보드를 여십시오. 
  4. **API**를 클릭하여 API를 보십시오. 

## 서비스 구성
{: #iot4i_configservices}
서비스를 구성하려면 다음 태스크를 수행하십시오. 

### {{site.data.keyword.amashort}} 구성
{: #config_ama}
1. {{site.data.keyword.iotinsurance_short}} API 애플리케이션의 기본 URL을 식별하십시오. 이 URL은 애플리케이션 타일에 표시되며 *appName*-api.mybluemix.net 형식입니다. 

2. {{site.data.keyword.amashort}} 서비스를 여십시오. 

3. **사용자 정의** 섹션에서 **구성**을 클릭한 후 다음 인증 신임 정보를 입력하십시오. 

  - **영역 이름**: `IoT4I`

  - **사용자 정의 ID 제공자 URL**: API 애플리케이션의 URL이며 형식은 다음과 같습니다.
      
  ```
  https://appName-api.mybluemix.net
  ```

  - **웹 애플리케이션 경로 재지정 URI**: 이 필드는 공백으로 두십시오. 

### {{site.data.keyword.mobilepushshort}} 구성
{: #config_push}
기존 모바일 앱의 푸시 알림을 사용하려면 {{site.data.keyword.mobilepushshort}} 서비스를 구성하고 공개 키 암호 표준(PKCS) 12 파일을 추가해야 합니다. 모바일 앱에 대한 정보는 [샘플 모바일 앱 설치 및 연결](iotinsurance_mobile_app.html)의 내용을 참조하십시오. {{site.data.keyword.mobilepushshort}}에 대한 정보는 [푸시 알림 시작하기](https://new-console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html)를 참조하십시오. 

  1. {{site.data.keyword.mobilepushshort}} 서비스를 여십시오. 
  2. **푸시 설정**을 클릭하십시오. 
  3. Apple 푸시 알림 인증서 섹션에 모바일 앱에 해당하는 PKCS 12 파일을 업로드한 후 비밀번호를 입력하십시오. 

다음 항목
{: #whats_next}
{{site.data.keyword.iotinsurance_short}}에서 수행할 수 있는 작업을 알아보십시오. 

- [사용자 및 실드 연관](iotinsurance_create_users.html)을 작성하십시오. 
- [샘플 모바일 앱](iotinsurance_mobile_app.html)을 설치하고 연결하십시오.
- [고급 서비스](iotinsurance_advancedservices.html)를 사용하여 성능 개선
- [API](https://iot4i-docs-api.mybluemix.net/dist/)를 보십시오.

# 관련 링크
{: #rellinks}

## 튜토리얼 및 샘플
{: #samples}
* [Github에 있는 샘플 모바일 앱 코드](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## API 참조
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API 예](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## 관련 링크
{: #general}
* [{{site.data.keyword.iot_full}} 문서](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
* [개발자 지원 포럼](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [스택 오버플로우 지원 포럼](http://stackoverflow.com/questions/tagged/ibm-bluemix)
