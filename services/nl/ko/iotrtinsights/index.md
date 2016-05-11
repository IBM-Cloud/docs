---

copyright:
  years: 2015,2016

---

{:new_window: target=_"blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.iotrtinsights_full}} 시작하기
{: #gettingstartedtemplate}
*마지막 업데이트 날짜: 2016년 2월 11일*

{{site.data.keyword.iotrtinsights_full}} on Bluemix({{site.data.keyword.iotrtinsights_short}})를 사용하여 IoT(Internet of Things) 디바이스의 실시간 데이터를 분석하고, 디바이스 상태 및 사용자 오퍼레이션의 전반적 상태를 통찰할 수 있습니다.
{:shortdesc}

{{site.data.keyword.iotrtinsights_short}} 사용을 시작하려면 먼저 분석 엔진을 사용자의 디바이스에 연결하기 위해 {{site.data.keyword.iot_full}} 서비스({{site.data.keyword.iot_short}})를 설정해야 합니다. 기존 {{site.data.keyword.iot_short}} 서비스를 사용하거나 새 서비스를 작성할 수 있습니다. 빠르게 시작하고 실행하기 위해 Internet of Things 전화 애플리케이션 및 이와 연관된 {{site.data.keyword.iot_short}} 서비스를 사용자의 조직에 배치할 수 있습니다. 

이 서비스를 빠르게 시작하고 실행하려면 다음 단계를 따르십시오. 
1. {{site.data.keyword.iotrtinsights_short}} 서비스를 사용자의 Bluemix 조직에 배치하십시오. 
  1. Bluemix 계정 대시보드에서 **서비스 또는 API 사용**을 클릭하십시오. 
  2. 서비스 카탈로그의 Internet of Things 섹션을 찾은 다음 **{{site.data.keyword.iotrtinsights_short}}**를 선택하십시오. 
  3. {{site.data.keyword.iotrtinsights_short}} 페이지에서 서비스 추가 선택을 확인하십시오.   
    - 영역 - {{site.data.keyword.iot_short}} 서비스를 배치한 동일한 영역에 서비스를 배치하고 있는지 확인하십시오. 
    - 앱 - 바인딩되지 않은 상태로 두십시오. 
    - 서비스 이름 - 선택적으로 기억하기 쉬운 이름으로 서비스 이름을 변경하십시오. 이 이름은 Bluemix 대시보드의 IoT {{site.data.keyword.iotrtinsights_short}} 타일에 표시됩니다. 
    - 선택한 플랜 - 무료 또는 사용자의 필요에 적합한 유료 플랜을 선택하십시오.   
    > **중요:** 무료 {{site.data.keyword.iotrtinsights_short}} 플랜의 경우 조직당 하나의 서비스 인스턴스만 배치할 수 있습니다.
  4. **사용**을 클릭하여 {{site.data.keyword.iotrtinsights_short}}를 Bluemix 서비스에 배치하십시오. 
2. 선택사항: IoT {{site.data.keyword.iotrtinsights_short}}를 이용하여 사용자의 전화를 IoT 디바이스로 사용하십시오.
Internet of Things 전화 애플리케이션을 사용하여 사용자의 스마트폰이 {{site.data.keyword.iotrtinsights_short}} 환경 검증에 사용될 수 있는 IoT 디바이스로 작동하도록 빠르게 설정하고, 데이터에 대한 실시간 분석 정의를 시작하십시오. Internet of Things 전화 애플리케이션에 대한 자세한 정보는 [Internet of Things 전화 애플리케이션](https://github.com/ibm-messaging/IoT-html5-phone) 프로젝트를 참조하십시오.

  애플리케이션을 작성하고 전화를 {{site.data.keyword.iot_full}}에 연결하려면 다음을 수행하십시오. 
  1. 배치 프로세스를 시작하려면 아래 버튼을 클릭하십시오.   
  [![Bluemix에 배치 아이콘.](images/deploy_to_bluemix.png "Bluemix에 배치 아이콘")](https://bluemix.net/deploy?repository=https://github.com/ibm-messaging/iot-html5-phone "IoT 전화를 Bluemix에 배치")  
  > **참고:** Internet of Things 전화 애플리케이션을 배치하면 전화 애플리케이션에 자동으로 바인드되는 {{site.data.keyword.iot_short}} 서비스(*iot-phone-iotf-service*)도 배치됩니다. Internet of Things 전화 애플리케이션을 테스트하기 위한 데이터 소스로 이 {{site.data.keyword.iot_short}}을 추가하십시오. 이는 또한 애플리케이션에서 사용하는 Cloudant NoSQL DB 서비스(*iot-phone-cloudant-cloudantNoSQLDB*)를 작성합니다.

  2. IBM Single Sign On Service(OAuth Consent)에 대한 액세스를 자체 승인하도록 프롬프트된 경우 **승인**을 클릭하십시오.  
  >**팁:** Bluemix 계정이 없을 경우 가입을 통해 Bluemix 무료 평가판을 활성화할 수 있습니다.
  2. 앱 이름 필드를 기억하기 쉬운 이름으로 바꾸십시오. 본 지시사항의 나머지 부분에서는 이를 *전화 애플리케이션*으로 지칭하겠습니다. 이 이름은 사용자의 Bluemix 대시보드의 애플리케이션 타일에 표시되며 {{site.data.keyword.iot_short}}에 전화를 연결할 때 사용하는 URL의 일부가 됩니다. 
  2. **배치**를 클릭하십시오. 
  2. 배치 프로세스를 완료한 후 '성공' 메시지가 표시됩니다. Bluemix 대시보드로 돌아가십시오.
  *전화 애플리케이션* 타일과 *iot-phone-iotf-service* 타일이 사용자의 계정에 추가됩니다.
  1. Bluemix 대시보드에서 *전화 애플리케이션* 타일을 클릭하십시오.
  2. 전화에서 브라우저를 열고 애플리케이션 이름 아래 표시되는 라우트 URL로 이동하십시오. 프롬프트가 표시되면 {{site.data.keyword.iot_short}} 및 IoT {{site.data.keyword.iotrtinsights_short}} 대시보드의 디바이스로 사용자의 전화를 식별하기 위해 사용자가 선택한 디바이스 ID를 입력하십시오. 
  3. **연결**을 클릭하여 {{site.data.keyword.iot_short}} *iot-phone-iotf-service*에 전화를 연결하십시오.
  사용자의 전화에서 {{site.data.keyword.iot_short}}으로 전송된 데이터를 표시하도록 보기가 새로 고쳐집니다. 
2. Internet of Things 서비스를 작성하고 구성하십시오.  
> **팁:** Internet of Things 전화 애플리케이션을 배치했으면 *iot-phone-iotf-service*가 이미 작성되어 있으므로 이 단계를 건너뛸 수 있습니다.  

  1. Bluemix 조직에 로그인하고 IoT {{site.data.keyword.iotrtinsights_short}}를 배치할 영역을 선택하십시오.
  2. Bluemix 대시보드에서 **서비스 또는 API 사용**을 클릭하십시오. 
  3. 서비스 카탈로그의 Internet of Things 섹션을 찾은 다음 **Internet of Things**를 선택하십시오. 
  4. {{site.data.keyword.iot_full}} 페이지에서 서비스 추가 선택을 확인하고 **사용**을 클릭하여 {{site.data.keyword.iot_short}}을 Bluemix 서비스에 추가하십시오.
  {{site.data.keyword.iot_short}} 서비스가 배치된 후 서비스 관리 페이지로 연결됩니다. 
3. 연결 API 키를 찾으십시오.
새 {{site.data.keyword.iot_short}} 서비스를 작성했으면 이제 API 키를 작성하여 두 서비스를 연결해야 합니다. 기존 서비스를 사용 중이면 기존 키를 사용할 수 있습니다.   
  1. Bluemix 대시보드에서 Internet of Things 타일을 클릭하십시오.  
  >**참고:** Internet of Things 전화 애플리케이션을 사용 중인 경우 *iot-phone-iotf-service* 타일을 클릭하십시오.  

  1. **대시보드 실행**을 클릭하여 {{site.data.keyword.iot_full}} 대시보드를 여십시오.
  2. **액세스 > API 키**로 이동하십시오.
  3. **API 키 생성**을 클릭하십시오.
  3. {{site.data.keyword.iot_short}} 대시보드의 맨 위에 표시되는 조직 ID, 인증 토큰, API 키를 기록하십시오.
  IoT {{site.data.keyword.iotrtinsights_short}}에서 서비스에 연결할 때 이 정보를 사용합니다. 
4. {{site.data.keyword.iot_short}} 서비스와 IoT {{site.data.keyword.iotrtinsights_short}} 서비스에 연결하십시오. 
  1. Bluemix 대시보드에서 IoT {{site.data.keyword.iotrtinsights_short}} 타일을 클릭하십시오.  
  2. 서비스 페이지에서 **데이터 소스 추가**를 선택하십시오.
  2. {{site.data.keyword.iotrtinsights_short}} 콘솔의 데이터 소스 관리 페이지에서 **새 데이터 소스 추가**를 클릭하십시오. 
  3. 데이터 소스에 설명식 이름을 제공하고 앞에서 수집한 다음 정보를 제공하십시오.
    - 조직 ID
    - API 키
    - 인증 토큰
  4. ![작성 아이콘](images/create.png "작성 아이콘")을 클릭하여 데이터 소스를 작성하고 연결하십시오. 
4. {{site.data.keyword.iotrtinsights_short}} 사용을 시작하십시오.
이제 사용자 추가, 디바이스 연결, 관련 디바이스 데이터를 보기 위한 대시보드 구성, 경보 설정으로 {{site.data.keyword.iotrtinsights_short}}의 사용을 시작할 수 있습니다. 
>**{{site.data.keyword.iotrtinsights_short}} 인스턴스 선택:** 사용자가 운영자 또는 관리자로서 추가 {{site.data.keyword.iotrtinsights_short}} 인스턴스에 대한 액세스를 부여받은 경우 이러한 인스턴스 사이를 빠르게 전환할 수 있습니다.{{site.data.keyword.iotrtinsights_short}} 콘솔에서 사용자 이름을 클릭하고 액세스하려는 인스턴스를 선택하십시오.   

# 관련 링크
## 샘플
* [Internet of Things 전화 애플리케이션](https://github.com/ibm-messaging/IoT-html5-phone)
* [developerWorks Internet of Things 레시피](https://developer.ibm.com/recipes/)
* [Internet of Things 스타터 애플리케이션으로 앱 작성](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500)

## API
* [API 문서](https://iotrti-prod.mam.ibmserviceengage.com/apidoc/)

## 일반
* [정보](iotrtinsights_overview.html)   
* [Bluemix 서비스의 새로운 기능](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category)
* [{{site.data.keyword.iot_full}} 시작하기](https://www.ng.bluemix.net/docs/services/IoT/index.html)
* [IBM developerWorks의 dW Answers](https://developer.ibm.com/answers/topics/iot-real-time/)
