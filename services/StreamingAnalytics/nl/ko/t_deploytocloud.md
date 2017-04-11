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

#클라우드에 {{site.data.keyword.streamsshort}} 애플리케이션 배치
{: #t_deploytocloud}

{{site.data.keyword.Bluemix_short}} 클라우드에서 실행 중인 {{site.data.keyword.streaminganalyticsshort}} 인스턴스에 {{site.data.keyword.streamsshort}} 애플리케이션을 배치할 수 있습니다.
{:shortdesc}

{{site.data.keyword.streamsshort}} 애플리케이션은 {{site.data.keyword.streamsshort}} 환경에 SPL({{site.data.keyword.streamsshort}} Processing Language)로 작성됩니다. {{site.data.keyword.streamsshort}}는 또한 사용자의 애플리케이션을 개발하기 위해 사용할 수 있는 여러 가지 Java™ 개발 킷을 지원합니다. {{site.data.keyword.streamsshort}}에서 Java 지원에 대한 자세한 정보는 [Supported Java development kits for application development](https://www.ibm.com/support/knowledgecenter/en/SSCRJU_4.2.0/com.ibm.streams.install.doc/doc/ibminfospherestreams-install-prerequisites-java-supported-sdks.html){:new_window}를 참조하십시오.
{{site.data.keyword.streaminganalyticsshort}}는 클라우드에 {{site.data.keyword.streamsshort}} 개발 환경을 포함하지 않지만 로컬로 개발한 애플리케이션을 클라우드에 배치할 수 있습니다. 

시작하기 전에 브라우저의 팝업 차단기를 사용 안함으로 설정하여 Streaming Analytics 콘솔을 표시하십시오.

{{site.data.keyword.streamsshort}} 애플리케이션을 클라우드에 배치하려면 다음을 수행하십시오. 

1. 애플리케이션을 개발하고 테스트할 {{site.data.keyword.streamsshort}} 환경을 설정하십시오.  

	{{site.data.keyword.streamsshort}} 환경이 없으면
{{site.data.keyword.streamsshort}} Quick Start Edition을 무료로 다운로드할 수 있습니다. [IBM Streams 제품 페이지](http://www.ibm.com/analytics/us/en/technology/stream-computing/){:new_window}로 이동하고 **기본 소프트웨어 설치 다운로드**를 클릭하십시오.

2. Streams Studio 또는 명령행 도구를 사용하여 {{site.data.keyword.streamsshort}} 환경에서 SPL 또는 Java 애플리케이션을 개발하십시오.
3. SPL 또는 Java 애플리케이션이 개발 환경에서 적절히 실행되는지 확인하십시오.
4. 다음 방법 중 하나를 사용하여 SPL 또는 Java 애플리케이션에 연관된 애플리케이션 번들(.sab 파일)을 클라우드의 서비스 인스턴스에 제출하십시오.
	* {{site.data.keyword.streaminganalyticsshort}} 콘솔을 사용하여 애플리케이션 번들을 제출하십시오.
    * {{site.data.keyword.Bluemix_short}} 애플리케이션을 개발하고 {{site.data.keyword.streamsshort}} 애플리케이션을 여기에 추가하십시오.
{{site.data.keyword.streaminganalyticsshort}} REST API를 사용하여 이를 제어하십시오. 

애플리케이션이 이제 클라우드에 배치됩니다. {{site.data.keyword.streaminganalyticsshort}} 서비스를 사용하여 애플리케이션을 모니터할 수 있습니다. 또한 둘 이상의 SPL 또는 Java 애플리케이션(.sab 파일)을 서비스 인스턴스에 제출할 수 있습니다. 원하는 수만큼 제출할 수 있습니다. 
