---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Weather 시작하기
{: #insights_weather_overview}

*마지막 업데이트 날짜: 2016년 4월 6일*

{{site.data.keyword.weatherfull}}를 사용하여 TWC(The Weather Company)의 기상 데이터를
{{site.data.keyword.Bluemix}} 애플리케이션에 통합할 수 있습니다.
{:shortdesc}

다음 지시사항에서는 애플리케이션 작성, Insights for Weather 서비스에 애플리케이션 바인딩,
그리고 [REST API](https://twcservice.{APPDomain}/rest-api/)와의 상호작용을 위한
서비스 신임 정보 검색 프로세스를 전체적으로 안내합니다. 

### 애플리케이션 작성
{: #create_an_app}

데모 용도로 사용자는 Liberty for Java 런타임을 사용하여 애플리케이션을
작성하지만, 다음 일반 프로세스가 기타 런타임에 적용될 수 있습니다. 

1. 기존 애플리케이션이 없으면 대시보드에서 **앱 작성**을 클릭하십시오.
2. 앱 템플리트를 선택하라는 요청을 받으면 **웹**을 클릭하십시오.
3. 시작 프로그램을 선택하라는 요청을 받으면 **Liberty for Java**를 클릭하십시오.
4. **계속**을 클릭하십시오.
5. **앱 이름** 필드에 앱의 이름을 입력하십시오.
6. **완료**를 클릭하십시오.애플리케이션이 프로비저닝될 때까지 기다리십시오.

### Insights for Weather 서비스 추가
{: #add_insights_for_weather_service}

Insights for Weather 서비스를 앱에 추가하려면 다음 단계를 따르십시오.
1. **카탈로그** 메뉴를 여십시오.
2. **데이터 & 분석** 섹션에서 **Insights for Weather** 타일을 클릭하십시오. 
3. **앱** 드롭 다운 목록에서 앱을 선택하십시오.
4. **사용**을 클릭하십시오.
5. 프롬프트가 표시되면 **다시 스테이징**을 클릭하여 애플리케이션을 다시 시작하십시오.

### Insights for Weather 신임 정보 검색
{: #retrieve_weather_credentials}

애플리케이션을 Insights for Weather에 바인드할 때 사용자는
고유 신임 정보로 서비스 인스턴스를 프로비저닝합니다. 이 신임 정보는 애플리케이션의
`VCAP_SERVICES`에 저장되며 서비스 간의 상호작용을 지원하는 데 필수적입니다. 

1. 애플리케이션 개요 페이지로 이동하십시오.
2. **환경 변수** 섹션으로 이동하십시오. 각 서비스에 대한 `VCAP_SERVICES` 정보가 표시됩니다.
3. Insights for Weather 서비스의 사용자 이름 및 비밀번호 값을 기록하십시오.
[REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}를
시도하려면 로그인하는 프롬프트가 나타날 때 이 신임 정보를 입력해야 합니다.
`VCAP_SERVICES`는 다음 예와 유사합니다. 

```
{
   "weatherinsights": [
     {
      "name": "Insights for Weather",
      "label": "weatherinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "twcservice.mybluemix.net",
         "password": "7abcxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }
   ]
}
```

# 관련 링크
## 샘플
* [Insights for Weather 데모](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [What's the weather like in Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## api
* [REST API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## 호환 가능 런타임 {:id="buildpacks"}
* [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## 일반
* [Insights for Weather 정보](https://console.{DomainName}/docs/services/Weather/weather_overview.html){: new_window}
* [애플리케이션에 서비스 추가](https://console.{DomainName}/docs/services/reqnsi.html#add_service){: new_window}
* [엔드-투-엔드 개발](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 가격 책정 시트](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 전제조건](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
