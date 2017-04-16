---

copyright:
  years: 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Insights for Twitter 시작하기 {: #insights_twitter_overview}

{{site.data.keyword.twitterfull}}를 사용하여 Twitter [Decahose](http://support.gnip.com/gnip2.0/){: new_window} 또는 [PowerTrack](http://support.gnip.com/apis/powertrack2.0/){: new_window} 스트림의 Twitter 컨텐츠를 {{site.data.keyword.Bluemix}} 애플리케이션에 통합합니다.
{:shortdesc}

{{site.data.keyword.twittershort}} 사용을 시작하려면 먼저 Liberty for Java와 같은 런타임을 사용하여 Bluemix 웹 애플리케이션을 작성한 다음 앱의 {{site.data.keyword.twittershort}} 서비스를 추가하십시오. {{site.data.keyword.twittershort}} 서비스가 앱에 바인드되면 고유 신임 정보를 사용하여 서비스 인스턴스가 프로비저닝됩니다. 사용자의 앱은 이러한 신임 정보를 REST API와 함께 사용하여 Twitter 컨텐츠를 검색하고 이용합니다. 다음 단계에 따라 VCAP_SERVICES에서 신임 정보를 검색하고 서비스 인스턴스를 사용자의 앱과 통합하십시오. 

1. 애플리케이션 개요 페이지로 이동하십시오. 
2. **환경 변수** 섹션으로 이동하십시오. 각 서비스에 대한 `VCAP_SERVICES` 정보가 표시됩니다.
3. {{site.data.keyword.twittershort}} 서비스의 사용자 이름과 비밀번호 값을 기록해두십시오. REST API 참조 문서의 조작을 테스트하려면 이 신임 정보를 입력해야 합니다. 예를 들어, `VCAP_SERVICES`는 다음 스니펫과 유사합니다. 

```
{  
   "twitterinsights": [    
     {      
      "name": "IBM Insights for Twitter-x3",
      "label": "twitterinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "cdeservice.mybluemix.net",
         "password": "7cunxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }  
   ]
}
```

# 관련 링크
{: #rellinks}
## 샘플
{: #samples}
* [대화식 Decahose 검색 데모](https://cdetestapp.mybluemix.net/){: new_window}
* [developerWorks: Decahose 검색 데모에 대한 학습서 및 소스 코드](http://www.ibm.com/developerworks/cloud/library/cl-twitter-search-insights-bluemix-trs/index.html){: new_window}
* ["American Sniper" 박스 오피스 데이터 분석 (유튜브)](https://www.youtube.com/watch?v=Gfk5quglXvI){: new_window}
* [Insights 핸즈온 랩 위치](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}

## API
{: #api}
* [REST API](https://cdeservice.{APPDomain}/rest-api/){: new_window}

## 호환 가능 런타임 
{: #buildpacks}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Swift](https://console.{DomainName}/docs/runtimes/swift/index.html){: new_window}
* [Tomcat](https://console.{DomainName}/docs/runtimes/tomcat/index.html){: new_window}

## 일반
{: #general}
* [{{site.data.keyword.Bluemix_notm}} 서비스의 새로운 기능](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){: new_window}
* [서비스를 애플리케이션에 추가](../reqnsi.html){: new_window}
* [엔드 투 엔드 개발](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [{{site.data.keyword.Bluemix_notm}}가격 책정 시트](https://console.{DomainName}/pricing/){: new_window}
* [{{site.data.keyword.Bluemix_notm}}필수 소프트웨어](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}

