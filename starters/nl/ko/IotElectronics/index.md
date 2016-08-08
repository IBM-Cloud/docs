---

copyright:
  years: 2016

---

{:new_window: target="_blank"}

{:shortdesc: .shortdesc}


# {{site.data.keyword.iotelectronics}} 스타터로 앱 작성
*마지막 업데이트 날짜: 2016년 6월 14일*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}}는 사용자의 앱이 연결된 어플라이언스와 통신하고 이를 제어하며 분석하고 업데이트할 수 있도록 하는 통합된 엔드-투-엔드 솔루션입니다. 스타터에는 시뮬레이션된 어플라이언스를 작성하고 제어하도록 하는 스타터 앱 및 모바일 디바이스에서 해당 어플라이언스를 제어하도록 하는 샘플 모바일 앱이 포함됩니다.
{:shortdesc}

**전제조건**:  
Bluemix 카탈로그의 표준 유형 섹션에서 {{site.data.keyword.iotelectronics}} 스타터를 배치했는지 확인하십시오. 그러면 {{site.data.keyword.amafull}}를 포함하여 스타터의 서비스와 컴포넌트 애플리케이션이 자동으로 배치됩니다.

{{site.data.keyword.iotelectronics}}를 시작하려면, 뒤따르는 섹션에 설명된 대로 다음 태스크를 완료하십시오.

1. {{site.data.keyword.amashort}}를 구성하여 샘플 모바일 앱과의 통신을 가능하게 하십시오.
2. {{site.data.keyword.iotelectronics}} 스타터 웹 애플리케이션을 통해 시뮬레이션된 어플라이언스를 작성하십시오.
3. 샘플 모바일 앱을 설치하여 연결하십시오.

## {{site.data.keyword.amashort}} 구성
{: #configureMCA}
모바일 앱을 사용하려면 다음과 같이 {{site.data.keyword.amashort}}를 구성해야 합니다.
1. {{site.data.keyword.Bluemix_notm}} 대시보드에서, [{{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)를 여십시오.
2. **사용자 정의** 섹션에서 **구성**을 선택하십시오.
3. 다음 인증 신임 정보를 입력하십시오.
  - **영역 이름**: myRealm
  - **URL**: https://<*myIoT4eStarterApp*>.mybluemix.net  

    **팁:** URL에 안전한 `https://` 접두부를 사용해야 합니다. **모바일 옵션**을 클릭하여 스타터 앱의 URL을 찾을 수 있습니다.
4. 저장하십시오.

  자세한 지시사항은 [{{site.data.keyword.amashort}} 구성](iotelectronics_config_mobile.html#iot4e_configureMCA)을 참조하십시오.

##시뮬레이션된 어플라이언스 작성
시뮬레이션된 어플라이언스를 작성하려면 다음 단계를 수행하십시오.
1. {{site.data.keyword.Bluemix_notm}} 대시보드에서, {{site.data.keyword.iotelectronics}} 애플리케이션을 시작하십시오.
2. *앱이 실행 중* 상태 메시지를 기다린 후 **앱 보기**를 클릭하여 스타터 앱을 표시하십시오.  
3. **연결된 어플라이언스를 원격으로 제어**를 선택하십시오.
4. **다음, 시뮬레이션된 새 세탁기 선택 또는 추가**로 레이블이 지정된 섹션으로 화면 이동하고 추가(+) 단추를 클릭하십시오. 새 세탁기가 작성됩니다.

## 샘플 모바일 앱 설치 및 연결
샘플 모바일 앱을 설치하고 연결하려면 다음 단계를 수행하십시오.

*참고*: iOS 디바이스가 있어야 샘플 모바일 앱을 사용할 수 있습니다.

1. 전화기에서, 앱 스토어를 열고 `ibm iot`를 검색하십시오. **IBM IoT for Electronics**를 선택하고 설치하십시오.
2. 스타터 앱에 있는 연결 QR 코드를 스캔하여 조직에 전화기를 연결하십시오.
3. 스타터 앱에 있는 어플라이언스 QR 코드를 스캔하여 시뮬레이션된 어플라이언스를 연결하십시오.

  자세한 지시사항은 [{{site.data.keyword.iotelectronics}} 환경에 모바일 앱 연결](iotelectronics_config_mobile.html#iot4e_connecting_mobile)을 참조하십시오.

##다음 항목
{{site.data.keyword.iotelectronics}}에서 수행할 수 있는 항목을 확인하십시오.

- 스타터 앱을 탐색하여 엔터프라이즈 제조업체가 {{site.data.keyword.iot_short_notm}}에 연결되는 어플라이언스를 모니터할 수 있는 방식을 체험하십시오.
- 샘플 모바일 앱을 탐색하여 어플라이언스 소유자가 해당 어플라이언스를 등록하고 이와 상호작용할 수 있는 방식을 체험하십시오.
- 수동으로 디바이스 실패를 유발하여 제조업체 및 어플라이언스 소유자 둘 다에 대해 경보, 알림 및 조치를 트리거합니다.
- 운영 데이터를 사용자 데이터와 연관시켜서 제품 및 디바이스가 운영되는 방식과 해당 운영자를 파악하십시오.


# 관련 링크
{: #rellinks}
## API 문서
{: #api}
* [{{site.data.keyword.iotelectronics}} API](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iot_short}} API](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## 컴포넌트
{: #general}

* [{{site.data.keyword.iotelectronics}} 문서](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}} 문서](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
*  [{{site.data.keyword.amashort}} 문서](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}} 문서](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## 샘플
{: #samples}
* [샘플 모바일 앱](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
