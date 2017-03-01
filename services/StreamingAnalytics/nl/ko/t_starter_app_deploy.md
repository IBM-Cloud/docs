---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.Bluemix_short}}에 스타터 애플리케이션 배치
{: #starterapps_deploy}

{{site.data.keyword.streaminganalyticsshort}} 스타터 애플리케이션 중 하나를 {{site.data.keyword.Bluemix_short}} 클라우드에 푸시하고 배치할 수 있습니다.
{:shortdesc}

시작하기 전에 {{site.data.keyword.Bluemix_short}}가 {{site.data.keyword.streaminganalyticsshort}} 스타터 애플리케이션을 배치할 준비가 되게 하십시오. 

* [cf 명령행 도구를 설치](https://github.com/cloudfoundry/cli/releases)하십시오.
* {{site.data.keyword.Bluemix_short}}에 애플리케이션을 작성하고 {{site.data.keyword.streaminganalyticsshort}} 서비스를 애플리케이션에 추가한 다음 애플리케이션을 다시 스테이징하십시오. 
	* Event Detection 스타터 앱을 배치하려면 {{site.data.keyword.sdk4node}} 런타임을 사용하여 애플리케이션을 작성하십시오. 
	* NYC Traffic 스타터 앱을 배치하려면 Liberty for Java™ 런타임으로 애플리케이션을 작성하십시오. 

애플리케이션에 제공한 이름을 기억해 두십시오. 나중에 필요합니다.

{{site.data.keyword.streaminganalyticsshort}}는 서비스를 시작할 수 있게 하는 두 개의 샘플 애플리케이션을 제공합니다.  

Event Detection 스타터 애플리케이션은 실시간 스트림에서 날씨 관련 데이터를 분석하고 분석의 상태 및 결과를 표시합니다. 애플리케이션은 {{site.data.keyword.sdk4node}}로 작성됩니다. Event Detection 스타터 앱을 사용하는 방법에 대한 세부사항은 [Detect complex events in a real-time data stream](https://www.ibm.com/developerworks/library/ba-bluemix-detect-complex-events-from-data-stream-trs/index.html)을 참조하십시오. 

NYC Traffic 스타터 애플리케이션은 공용 웹 사이트에서 트래픽 데이터를 읽고 분석합니다. 애플리케이션은 Liberty for Java™로 작성됩니다. NYC Traffic 스타터 앱을 사용하는 방법에 대한 세부사항은 [{{site.data.keyword.streaminganalyticsfull}} Starter Application](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/)을 참조하십시오. 

스타터 애플리케이션을 다운로드하여 {{site.data.keyword.Bluemix_short}}에 배치하려면 다음을 수행하십시오.

1. [Event Detection](https://hub.jazz.net/project/streamscloud/EventDetection/overview) 또는 [NYC Traffic](https://hub.jazz.net/project/streamscloud/NYCTraffic/overview) 스타터 애플리케이션을 다운로드하십시오.
2. 명령행에서 프로젝트 디렉토리로 이동하십시오. 
  <pre><code>cd myapp</code></pre>
 
3. {{site.data.keyword.Bluemix_short}}의 애플리케이션에 지정한 이름과 일치하도록 프로젝트 디렉토리의 이름을 바꾸십시오. 
4. {{site.data.keyword.Bluemix_short}}에 연결하십시오. 
  <pre><code>cf api https://api.DomainName</code></pre>
   
5. {{site.data.keyword.Bluemix_short}}에 로그인하고 프롬프트가 표시되면 대상 조직을 설정하십시오. 
   <pre><code>cf login</code></pre>
    
6. 애플리케이션을 배치하십시오. 
  <pre><code>cf push myapp</code></pre>
   
7. {{site.data.keyword.Bluemix_short}} 대시보드에서 액세스할 수 있는 애플리케이션 개요 페이지로 이동하여 애플리케이션이 제대로 시작되었는지 확인하십시오. 
8. 애플리케이션을 시작하여 브라우저에서 보십시오. 애플리케이션 개요 페이지에서 애플리케이션의 URL(또는 "라우트")을 찾을 수 있습니다. 

이제 앱이 실행되고 있으며 서비스 대시보드로 이동하여 사용자의 {{site.data.keyword.streaminganalyticsshort}} 인스턴스의 상태를 보고 문제점 해결을 위한 정보를 얻을 수 있습니다. 서비스 대시보드에 액세스하려면 {{site.data.keyword.Bluemix_short}} 대시보드로 이동하여 애플리케이션 개요 페이지에서 {{site.data.keyword.streaminganalyticsshort}} 타일을 클릭하십시오. 
