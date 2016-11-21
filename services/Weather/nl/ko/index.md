---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.weather_short}} 시작하기
{: #insights_weather_overview}

{{site.data.keyword.weatherfull}}를 사용하여 TWC(The Weather Company)의 기상 데이터를
{{site.data.keyword.Bluemix}} 애플리케이션에 통합할 수 있습니다.
{:shortdesc}

**주의:** 현재 {{site.data.keyword.weather_short}} 서비스는 다음 국가 또는 지역에서 구매하거나 사용되지 **않을 수 있습니다**.
아프가니스탄, 아르메니아, 아제르바이잔,
바레인, 방글라데시, 부탄, 브루나이, 캄보디아, 중국, 키프로스, 조지아,
인도네시아, 이란, 이라크, 일본, 요르단, 카자흐스탄, 쿠웨이트, 키르기스스탄, 라오스,
레바논, 말레이시아, 몰디브, 몽골, 미얀마, 네팔, 오만, 파키스탄, 필리핀,
카타르, 러시아, 사우디아라비아, 싱가폴, 한국, 스리랑카, 시리아,
타지키스탄, 동티모르, 터키, 투르크메니스탄, 아랍 에미리트,
우즈베키스탄, 베트남, 예멘. 추가 정보가 사용 가능하면 이 목록이 업데이트됩니다.


[Insights for Weather 서비스](https://console.{DomainName}/docs/services/InsightsWeather/index.html){: new_window}를 사용하는
기존 애플리케이션이 있는 경우,
{{site.data.keyword.weather_short}}의 도입 이후 90일 동안 수정 없이 앱이 계속해서 작업합니다. 새로 추가된 API
및 개선된 가격 책정 모델을 이용하기 위해 새 서비스에 애플리케이션을 마이그레이션할 수 있습니다.

시작하기 전에, Liberty for Java 등의 런타임으로 대시보드에서 {{site.data.keyword.Bluemix_notm}} 웹 앱을 작성하십시오. 앱이 프로비저닝될 때까지 기다린 후
{{site.data.keyword.weather_short}} 서비스를 앱에 추가하십시오.

{{site.data.keyword.weather_short}}에 앱을 바인드할 때
고유 신임 정보를 사용하여 서비스 인스턴스를 프로비저닝하는 중입니다. 
앱은 [REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}에서 이 신임 정보를 사용하여 기상 데이터를 검색합니다. 

다음 단계를 수행하여 `VCAP_SERVICES`에서 서비스 신임 정보를 검색하고
서비스 인스턴스를 앱과 통합하십시오.

1. 애플리케이션 개요 페이지로 이동하십시오.
2. **환경 변수** 섹션으로 이동하십시오. 각 서비스에 대한 `VCAP_SERVICES` 정보가 표시됩니다.
3. {{site.data.keyword.weather_short}} 서비스에서 사용자 이름 및 비밀번호 값을 참고하십시오.
[REST API](https://twcservice.{APPDomain}/rest-api/){:new_window}를
시도하려면 로그인하는 프롬프트가 나타날 때 이 신임 정보를 입력해야 합니다.
`VCAP_SERVICES`는 다음 예와 유사합니다. 

```
{
{
   "weatherinsights": [
      {
         "name": "Weather Company Data for IBM Bluemix",
         "label": "weatherinsights",
         "plan": "Free",
         "credentials": {
            "username": "d40845df-8125-441f-8e7c-e650726ce721",
            "password": "tDV0HGZz3O",
            "host": "twcservice.mybluemix.net",
            "port": 443,
            "url": "https://d40845df-8125-441f-8e7c-e650726ce721:tDV0HGZz3O@twcservice.mybluemix.net"
         }
      }
   ]
}
```

**참고:** 각 지역은 독립적입니다. 한 지역에서 사용자에게
프로비저닝된 서비스 신임 정보를 사용하여 다른 지역의 서비스에 대해 인증할 수 없습니다.
적절한 신임 정보를 입력하지 않으면 응답 본문에 *Unauthorized* 메시지가 포함됩니다.

# 관련 링크
{: #rellinks}
## 샘플
{: #samples}
* [{{site.data.keyword.weather_short}} 데모 앱](http://weather-company-data-demo.{APPDomain}){: new_window}
* [{{site.data.keyword.weather_short}} Deep Dive 동영상](https://youtu.be/pZHXIibziUo){: new_window}
* [Places Insights hands-on lab](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [{{site.data.keyword.Bluemix_notm}} + Weather 샘플 앱](https://github.com/IBM-Bluemix/insights-weather){: new_window}
* [IBM Cloud - Bare Metal, NYC Taxi Data 및 Insights for Weather(YouTube 튜토리얼)](https://www.youtube.com/watch?v=Uwmzpx9DZ5c){: new_window}

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
* [애플리케이션에 서비스 추가](/docs/services/reqnsi.html){: new_window}
* [엔드-투-엔드 개발](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 가격 책정 시트](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}} 전제조건](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
