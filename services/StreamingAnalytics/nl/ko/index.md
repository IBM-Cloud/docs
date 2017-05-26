---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# {{site.data.keyword.streaminganalyticsshort}} 시작하기
{: #gettingstarted}

{{site.data.keyword.streaminganalyticsshort}}는 실시간으로 다양한 유형의 데이터 소스에서 도착하는 정보를 수집, 분석, 상관시키기 위해 사용할 수 있는 고급 분석 플랫폼인 {{site.data.keyword.streamsshort}}에서 제공합니다. {{site.data.keyword.streaminganalyticsshort}} 서비스의 인스턴스를 작성하면 {{site.data.keyword.streamsshort}} 애플리케이션을 실행할 준비가 된 {{site.data.keyword.Bluemix_short}} 클라우드에서 자체 {{site.data.keyword.streamsshort}} 인스턴스를 실행할 수 있습니다.
{:shortdesc}

[스타터 애플리케이션](/docs/services/StreamingAnalytics/c_starterapps.html){:new_window}을 실행하여 바로 {{site.data.keyword.streaminganalyticsshort}}를 시작하십시오. 

{{site.data.keyword.streaminganalyticsshort}}를 시작하려면 다음 방법 중 하나를 사용하여 SPL, Java™, Python 또는 Scala Streams 애플리케이션과 연관된 애플리케이션 번들(.sab 파일)을 제출하십시오. 
* {{site.data.keyword.streaminganalyticsshort}} 콘솔에서 **작업 제출** 단추를 사용하십시오. 
* {{site.data.keyword.Bluemix_short}} 애플리케이션을 개발하고 {{site.data.keyword.streamsshort}} 애플리케이션을 여기에 추가하십시오.
[{{site.data.keyword.streaminganalyticsshort}} REST API](https://console.ng.bluemix.net/apidocs/220)를 사용하여 이를 제어하십시오. 


{{site.data.keyword.cloudant}} 및 {{site.data.keyword.messagehub}}를 포함하여 기타 {{site.data.keyword.Bluemix_short}} 서비스와 함께 {{site.data.keyword.streaminganalyticsshort}}를 사용하십시오. 시작하고 실행할 수 있게 하는 예제에 대해서는 [다른 {{site.data.keyword.Bluemix_short}} 서비스와 통합하기 위한 튜토리얼](/docs/services/StreamingAnalytics/r_integrating_cloudant_rest.html){:new_window}을 참조하십시오. 

자체 애플리케이션으로 추가 작업을 진행하려는 경우, {{site.data.keyword.streamsshort}} 개발 환경을 가져올 수 있으며 애플리케이션 클라우드를 준비해야 합니다. {{site.data.keyword.streamsshort}} 환경이 없으면 [{{site.data.keyword.streamsshort}} 제품 페이지](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products)에서 {{site.data.keyword.streamsshort}} Quick Start Edition을 무료로 다운로드할 수 있습니다.

{{site.data.keyword.streamsshort}} 애플리케이션 개발이 익숙하지 않는 경우 학습을 도와줄 리소스가 있습니다. 자세한 정보는 [{{site.data.keyword.streamsshort}} Knowledge Center](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.welcome.doc/doc/kc-homepage.html){:new_window}를 참조하십시오.

온프레미스에서 실행하는 SPL 애플리케이션이 이미 있는 경우 [애플리케이션을 클라우드에 대해 준비해야 합니다.](https://developer.ibm.com/streamsdev/docs/getting-spl-application-ready-cloud/){:new_window}

**참고:** Intel 프로세서를 사용하여 Red Hat Enterprise Linux(RHEL) 6.5 또는 이와 동등한 CentOS 버전에서 애플리케이션을 컴파일해야 합니다. 

## {{site.data.keyword.streaminganalyticsshort}}용 {{site.data.keyword.streamsshort}} Python 앱
{: #gettingstarted_py notoc}

이제 IBM Data Science Experience(DSX) 등의 Python 환경에서 Streams 앱을 작성할 수 있으며, 이러한 앱을 Bluemix 클라우드에 배치되도록 {{site.data.keyword.streaminganalyticsshort}} 인스턴스에 제출할 수 있습니다. Streams Python 앱을 컴파일하고 배치하기 위해 더 이상 로컬로 {{site.data.keyword.streamsshort}}를 설치할 필요가 없습니다. 

DSX에서 Jupyter 노트북을 사용하여 샘플 Streams Python 앱을 작성하여 시작하고, DSX에서 직접 서비스 인스턴스에 이러한 앱을 제출하십시오.
자세한 정보는 [DSX에서 Streams Python 앱 개발](/docs/services/StreamingAnalytics/t_develop_apps_python.html#t_develop_python_dsx)을 참조하십시오. 

{{site.data.keyword.streaminganalyticsshort}}에서는 로컬 Python 환경에서 Streams 앱의 배치도 지원합니다. Streams Python 앱을 로컬로 개발하고 이를 서비스 인스턴스에 제출하려면, streamsx 패키지에 포함되어 있는 [{{site.data.keyword.streamsshort}} Python 애플리케이션 API](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features)를 사용해야 합니다. 시작하려면 [Developing for the {{site.data.keyword.streaminganalyticsshort}} service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) 튜토리얼의 단계를 따르십시오.
