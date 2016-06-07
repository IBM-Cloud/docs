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

*마지막 업데이트 날짜: 2016년 5월 19일*

{{site.data.keyword.weatherfull}}를 사용하여 TWC(The Weather Company)의 기상 데이터를
{{site.data.keyword.Bluemix}} 애플리케이션에 통합할 수 있습니다.
{:shortdesc}

**참고:** Insights for Weather 서비스는 현재 일본에서는 사용할 수 없습니다. 

시작하기 전에, Liberty for Java 등의 런타임으로 대시보드에서 {{site.data.keyword.Bluemix_notm}} 웹 앱을 작성하십시오. 
앱이 프로비저닝될 때까지 기다린 후에 Insights for Weather 서비스를 앱에 추가하십시오. 

앱을 Insights for Weather에 바인드할 때 사용자는 고유 신임 정보로 서비스 인스턴스를 프로비저닝합니다. 
앱은 [REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}에서 이 신임 정보를 사용하여 기상 데이터를 검색합니다. 

`VCAP_SERVICES`에서 신임 정보를 검색하고 서비스 인스턴스를 앱과 통합하려면 다음 단계를 수행하십시오. 

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

**참고:** 각 지역은 독립적입니다. 한 지역에서 사용자에게
프로비저닝된 서비스 신임 정보를 사용하여 다른 지역의 서비스에 대해 인증할 수 없습니다.
적절한 신임 정보를 입력하지 않으면 응답 본문에 "권한 없음" 메시지가 포함됩니다.  

# 관련 링크
{: #rellinks}
## 샘플
{: #samples}
* [Insights for Weather 데모](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [What's the weather like in Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## api
{: #api}
* [REST API](https://twcservice.{APPDomain}/rest-api/){: new_window}

## 호환 가능 런타임 
{: #buildpacks}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## 일반
{: #general}
* [애플리케이션에 서비스 추가](../reqnsi.html){: new_window}
* [엔드-투-엔드 개발](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 가격 책정 시트](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 전제조건](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
