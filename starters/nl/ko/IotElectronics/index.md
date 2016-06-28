---

copyright:
  years: 2016

---

{:new_window: target="_blank"}

{:shortdesc: .shortdesc}


# {{site.data.keyword.iotelectronics}} 스타터를 사용하여 앱 작성
*마지막 업데이트 날짜: 2016년 6월 14일*

{{site.data.keyword.iotelectronics_full}}는 사용자 앱이 연결된 어플라이언스와 통신, 제어, 분석 및 업데이트할 수 있는 통합 엔트-투-엔드 솔루션입니다. 스타터에는 시뮬레이션된 어플라이언스를 작성하고 제어할 수 있는 스타터 앱과 모바일 디바이스에서 이러한 어플라이언스를 제어할 수 있는 샘플 모바일 앱이 포함되어 있습니다.
{:shortdesc}

**전제조건**:  
Bluemix 카탈로그의 표준 유형 섹션에서 {{site.data.keyword.iotelectronics}} 스타터를 배치했는지 확인하십시오. 그렇게 하면 {{site.data.keyword.amafull}}를 포함하여 컴포넌트 애플리케이션 및 스타터의 서비스가 자동으로 배치됩니다. 

{{site.data.keyword.iotelectronics}}를 시작하려면, 뒤에 나오는 섹션에 설명된 대로 다음 태스크를 완료하십시오. 

1. {{site.data.keyword.amashort}}를 구성하여 샘플 모바일 앱과의 통신을 사용으로 설정하십시오. 
2. {{site.data.keyword.iotelectronics}} 스타터 웹 애플리케이션을 사용하여 시뮬레이션된 어플라이언스를 작성하십시오. 
3. 샘플 모바일 앱을 설치하고 연결하십시오. 

## {{site.data.keyword.amashort}} 구성 
{: #configureMCA}
모바일 앱을 사용하려면, 다음과 같이 {{site.data.keyword.amashort}}를 구성해야 합니다. 
1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 [{{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)를 여십시오. 
2. **사용자 정의** 섹션에서 **구성**을 선택하십시오. 
3. 다음 인증 신임 정보를 입력하십시오. 
  - **영역 이름**: myRealm
  - **URL**: https://<*myIoT4eStarterApp*>.mybluemix.net  

    **팁:** URL에 보안 `https://` 접두부를 사용해야 합니다. **모바일 옵션**을 클릭하면 스타터의 URL을 확인할 수 있습니다.
4. 저장하십시오. 

  자세한 지시사항은 [{{site.data.keyword.amashort}} 구성](iotelectronics_config_mobile.html#iot4e_configureMCA)을 참조하십시오. 

##시뮬레이션된 어플라이언스 작성
시뮬레이션된 어플라이언스를 작성하려면, 다음 단계를 수행하십시오. 
1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.iotelectronics}} 애플리케이션을 시작하십시오. 
2. `앱 실행 중` 상태 메시지가 표시될 때까지 대기한 후, **앱 보기**를 클릭하여 스타터 앱을 표시하십시오.   
3. **연결된 어플라이언스를 원격으로 제어**를 선택하십시오. 
4. **다음으로, 시뮬레이션된 새 와셔 선택 또는 추가**라는 레이블이 지정된 섹션까지 스크롤하고 추가(+) 단추를 클릭하십시오. 새 와셔가 작성됩니다. 

## 샘플 모바일 앱 설치 및 연결
샘플 모바일 앱을 설치하고 연결하려면, 다음 담계를 수행하십시오. 

*참고*: 샘플 모바일 앱을 사용하려면 iOS 디바이스가 있어야 합니다. 

1. 휴대전화에서 App Store를 열고 `ibm iot`를 검색하십시오. **IBM IoT for Electronics**를 선택하고 앱을 설치하십시오. 
2. 스타터 앱에서 찾은 연결 QR 코드를 스캔하여 휴대전화를 조직과 연결하십시오. 
3. 스타터 앱에서 찾은 어플라이언스 QR 코드를 스캔하여 시뮬레이션된 어플라이언스를 연결하십시오. 

  자세한 지시사항은 [{{site.data.keyword.iotelectronics}} 환경에 모바일 앱 연결](iotelectronics_config_mobile.html#iot4e_connecting_mobile)을 참조하십시오. 

##다음에 수행할 작업
{{site.data.keyword.iotelectronics}}를 사용하여 수행할 수 있는 작업을 알아봅니다. 

- 스타터 앱을 탐색하여 엔터프라이즈 제조업체에서 {{site.data.keyword.iot_short_notm}}에 연결된 어플라이언스를 어떻게 모니터할 수 있는지 경험할 수 있습니다. 
- 샘플 모바일 앱을 탐색하여 어플라이언스 소유자가 어떻게 해당 어플라이언스를 등록하고 상호작용하는지 경험할 수 있습니다. 
- 제조업체 및 어플라이언스 소유자 모두에게 경보, 알림 및 조치가 트리거되도록 디바이스를 수동으로 실패하게 할 수 있습니다. 
- 운영 데이터와 사용자 데이터를 연관시켜 제품 및 디바이스가 어떻게 운영되는지 및 운영자는 누구인지 파악할 수 있습니다. 


# 관련 링크
{: #rellinks}
## API 문서
{: #api}
* [{{site.data.keyword.iotelectronics}}](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iotrtinsights_short}}](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)  
* [{{site.data.keyword.iot_short}}](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## 컴포넌트
{: #general}

* [{{site.data.keyword.iotelectronics_full}} 문서](iotelectronics_overview.html)
* [{{site.data.keyword.iot_full}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
* [{{site.data.keyword.iotrtinsights_full}}](https://new-console.ng.bluemix.net/docs/services/iotrtinsights/iotrtinsights_overview.html)
* [{{site.data.keyword.amafull}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [{{site.data.keyword.sdk4nodefull}}](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## 샘플
{: #samples}
* [샘플 모바일 앱](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
