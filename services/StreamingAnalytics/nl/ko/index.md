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


#{{site.data.keyword.streaminganalyticsshort}} 시작하기
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}}는 실시간으로 다양한 유형의 데이터 소스에서 도착하는 정보를 삽입, 분석, 상관시키기 위해 사용할 수 있는 고급 분석 플랫폼인 {{site.data.keyword.streamsshort}}에서 제공합니다. {{site.data.keyword.streaminganalyticsshort}} 서비스의 인스턴스를 작성하면 {{site.data.keyword.streamsshort}} 애플리케이션을 실행할 준비가 된 {{site.data.keyword.Bluemix_short}} 클라우드에서 자체 {{site.data.keyword.streamsshort}} 인스턴스를 실행할 수 있습니다.
{:shortdesc}

{{site.data.keyword.Bluemix_short}} 클라우드에서 실행 중인 {{site.data.keyword.streaminganalyticsshort}} 인스턴스에 애플리케이션을 배치할 수 있습니다. 

[스타터 애플리케이션](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}을 실행하여 즉시 {{site.data.keyword.streaminganalyticsshort}}를 시작할 수 있습니다. 자체 애플리케이션으로 작업을 더 수행하려면 {{site.data.keyword.streamsshort}} 개발 환경이 있어야 하고 SPL 클라우드 가능이어야 합니다.

{{site.data.keyword.streaminganalyticsshort}}를 시작하려면 SPL 또는 Java™ 애플리케이션과 연관된 애플리케이션 번들(.sab 파일)을 제출하기 위해 다음 방법 중 하나를 사용하십시오.
* {{site.data.keyword.streaminganalyticsshort}} 콘솔을 사용하십시오. 
* {{site.data.keyword.Bluemix_short}} 애플리케이션을 개발하고 {{site.data.keyword.streamsshort}} 애플리케이션을 여기에 추가하십시오.
[{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220)를 사용하여 이를 제어하십시오. SPL 또는 Java 애플리케이션이 개발 환경에서 적절히 실행되는지 확인하십시오.

이제, {{site.data.keyword.cloudant}} 및 {{site.data.keyword.messagehub}} 등의 기타 {{site.data.keyword.Bluemix_short}} 서비스와 함께 {{site.data.keyword.streaminganalyticsshort}}를 사용할 수 있습니다. 시작하고 실행할 수 있게 하는 예제에 대해서는 [다른 {{site.data.keyword.Bluemix_short}} 서비스와 통합하기 위한 튜토리얼](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window}을 참조하십시오. 

{{site.data.keyword.streamsshort}} 애플리케이션을 개발하려면 {{site.data.keyword.streamsshort}} 개발 환경이 반드시 있어야 합니다. {{site.data.keyword.streamsshort}} 환경이 없으면 [{{site.data.keyword.streamsshort}} 제품 페이지](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)에서 {{site.data.keyword.streamsshort}} Quick Start Edition을 무료로 다운로드할 수 있습니다.

{{site.data.keyword.streamsshort}} 애플리케이션 개발이 익숙하지 않는 경우 학습을 도와줄 리소스가 있습니다. 자세한 정보는 [{{site.data.keyword.streamsshort}} Knowledge Center](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}를 참조하십시오.

온프레미스에서 실행하는 SPL 애플리케이션이 이미 있는 경우 [애플리케이션을 클라우드에 대해 준비해야 합니다.](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}

# 관련 링크
{: #rellinks}

## 튜토리얼 및 샘플
{: #samples}
* [Introduction to {{site.data.keyword.streaminganalyticsshort}}](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} SDK for Node.js™ Starter Application](http://bit.ly/1iR1bzu){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} Liberty for Java™ Starter Application](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-starter-application/){:new_window}
* [Getting your SPL application ready for the cloud](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud){:new_window}
* [Bluemix {{site.data.keyword.streaminganalyticsshort}} Development Guide](https://developer.ibm.com/streamsdev/docs/bluemix-streaming-analytics-development-guide/){:new_window}
* [더 많은 튜토리얼](StreamingAnalytics.html#r_integrating_cloudant_rest){:new_window}


## API 참조
{: #api}
* [{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220){:new_window}
* [{{site.data.keyword.streaminganalyticsshort}} metrics using the {{site.data.keyword.streamsshort}} REST API](https://developer.ibm.com/bluemix/2016/07/25/streaming-analytics-metrics-using-rest-api/){:new_window}

## 호환 가능 런타임
{: #buildpacks}
* [Liberty for Java](/docs/runtimes/liberty/index.html#liberty)
* [Node.js](/docs/runtimes/nodejs/index.html#nodejs)

## 관련 링크
{: #general}
* [{{site.data.keyword.streamsshort}} documentation](http://www.ibm.com/support/knowledgecenter/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}
* [{{site.data.keyword.streamsshort}}Quick
Start Edition](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}
