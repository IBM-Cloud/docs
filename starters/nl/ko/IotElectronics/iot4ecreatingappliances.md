---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}

{:shortdesc: .shortdesc}


# 스타터 앱 사용
*마지막 업데이트 날짜: 2016년 9월 15일*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}} 스타터 앱에서 시뮬레이션된 어플라이언스를 작성합니다. 엔터프라이즈 제조업체가 {{site.data.keyword.iot_short_notm}}에 연결된 어플라이언스를 모니터하는 방법을 경험합니다. 시뮬레이션된 어플라이언스와 수동으로 상호작용하여 경보, 알림 및 조치를 트리거합니다.
{:shortdesc}


## 스타터 앱 열기
{: #iot4e_openAppMain}

스타터 앱을 여는 방법은 사용하는 {{site.data.keyword.Bluemix_notm}} 콘솔 버전에 따라 조금씩 다르므로 해당 버전에 대한 지시사항을 읽어야 합니다. 

다음 옵션을 찾아 사용 중인 버전을 판별할 수 있습니다. 
  - [새 {{site.data.keyword.Bluemix_notm}}](#iot4e_openApp). 새 {{site.data.keyword.Bluemix_notm}} 인터페이스를 사용 중인 경우, 헤더 섹션에 **새 Bluemix 시도**가 표시되지 *않습니다*. 
  - [기존 {{site.data.keyword.Bluemix_notm}}](#iot4e_openApp_c). 기존 {{site.data.keyword.Bluemix_notm}} 인터페이스를 사용 중인 경우, 헤더 섹션에 **새 Bluemix 시도**가 표시됩니다.   

**팁:** 기존 {{site.data.keyword.Bluemix_notm}} 인터페이스로 전환하려면 헤더 섹션에서 사용자 이름을 클릭한 후 아래로 화면 이동하여 **기존으로 전환**을 클릭하십시오. 새 {{site.data.keyword.Bluemix_notm}} 인터페이스로 전환하려면 헤더 섹션에서 **새 Bluemix 시도**를 클릭하십시오. 

### 새 {{site.data.keyword.Bluemix_notm}} 인터페이스에서 스타터 앱 열기
{: #iot4e_openApp}
1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 스타터 애플리케이션 타일을 클릭하여 {{site.data.keyword.iotelectronics}} 스타터 애플리케이션을 시작하십시오. 

    ![대시보드의 {{site.data.keyword.iotelectronics}}, 새 인터페이스](images/IoT4E_bm_dashboard.png "대시보드의 {{site.data.keyword.iotelectronics}}, 새 인터페이스")

2. 헤더에 *앱이 실행 중임* 상태 메시지가 표시될 때까지 기다린 후 **앱 보기**를 클릭하여 스타터 앱을 표시하십시오.  

    ![대시보드의 {{site.data.keyword.iotelectronics}}, 새 인터페이스](images/IoT4E_view_app.png "대시보드의 {{site.data.keyword.iotelectronics}}, 새 인터페이스")

### 기존 {{site.data.keyword.Bluemix_notm}} 인터페이스에서 스타터 앱 열기
{: #iot4e_openApp_c}

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 스타터 애플리케이션 타일을 클릭하여 {{site.data.keyword.iotelectronics}} 스타터 애플리케이션을 시작하십시오. 

    ![대시보드의 {{site.data.keyword.iotelectronics}}, 기존](images/IoT4E_bm_dashboard_c.png "대시보드의 {{site.data.keyword.iotelectronics}}, 기존")

2. 앱 상태 섹션에 *앱이 실행 중임* 상태 메시지가 표시될 때까지 기다린 후 기본 창의 애플리케이션 이름 옆에 있는 **라우트** URL을 클릭하여 스타터 앱을 표시하십시오.  

    ![대시보드의 {{site.data.keyword.iotelectronics}}, 기존](images/IoT4E_view_app_c.png "대시보드의 {{site.data.keyword.iotelectronics}}")

## 시뮬레이션된 어플라이언스 작성
{: #iot4eCreateAppliances}

스타터 앱에서, 어플라이언스 제조업체 또는 이용자로 시뮬레이션된 어플라이언스를 작성하고 제어할 수 있습니다. 이러한 시뮬레이션된 어플라이언스의 상태 및 이벤트 데이터가 저장되며, {{site.data.keyword.iot_full}}에서 이러한 데이터를 볼 수 있습니다. 

1. 다음 옵션 중 하나를 선택하십시오.
    - 어플라이언스 제조업체로서 시뮬레이션된 어플라이언스를 작성하려면 **시뮬레이션된 어플라이언스 연결 및 관리**를 선택하십시오.
    - 어플라이언스 소유자로 시뮬레이션된 어플라이언스를 작성하고 [샘플 모바일 앱](iotelectronics_config_mobile.html)과 연결하려면 **연결된 어플라이언스 원격 제어**를 선택하십시오.

    ![{{site.data.keyword.iotelectronics}} 스타터 인터페이스](images/IoT4E_remotely_option.png "{{site.data.keyword.iotelectronics}} 스타터 인터페이스")

2. **다음, 시뮬레이션된 새 세탁기 선택 또는 추가**로 레이블 지정된 섹션으로 화면 이동하여 추가(+) 아이콘을 클릭하십시오. 새 세탁기가 작성됩니다.

    ![세탁기 추가](images/IoT4E_add_washer.png "세탁기 추가")

3. 세탁기 세부사항을 보고 명령을 실행하며 고장을 일으키려면 세탁기를 클릭하십시오. 

  ![세탁기 상태 세부사항](images/IoT4E_washer_control.png "세탁기 상태 세부사항")


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
