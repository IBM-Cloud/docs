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

# {{site.data.keyword.streaminganalyticsshort}}용 Python 애플리케이션 개발
{: #t_develop_apps_python}

이제 IBM Data Science Experience(DSX) 또는 로컬 Python 개발 환경에서 Python 애플리케이션을 개발하고 {{site.data.keyword.streaminganalyticsshort}}에서 이러한 애플리케이션을 배치할 수 있습니다.
{:shortdesc}

다음 방법 중 하나로 {{site.data.keyword.streaminganalyticsshort}} 서비스를 사용하여 Python 애플리케이션을 개발하고 이를 {{site.data.keyword.Bluemix_short}} 클라우드에 배치하십시오. 


## DSX에서 Streams Python 애플리케이션 개발
{: #t_develop_python_dsx}

아직 Python 개발 환경이 마련되지 않은 경우, 가장 손쉬운 시작 방법은 DSX에서 노트북을 사용하여 {{site.data.keyword.streaminganalyticsshort}} 서비스의 샘플 Python 애플리케이션을 작성하는 것입니다. 이러한 노트북은 DSX Python 환경 내에서 {{site.data.keyword.streaminganalyticsshort}} 서비스의 단순 Python 애플리케이션을 작성하고 배치하기 위한 단계와 코드 샘플을 제공합니다. 

* [Hello World!](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca9c6e8): 단순 Hello World! 애플리케이션을 작성하여 시작한 후에 이 애플리케이션을 {{site.data.keyword.streaminganalyticsshort}} 서비스의 인스턴스에 배치하십시오. 

* [의료 데모](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039cad29a6): 피드의 스트리밍 데이터를 수집하고 분석하는 애플리케이션을 작성한 후에 노트북에서 데이터를 시각화하십시오. 최종적으로는 이 애플리케이션을 {{site.data.keyword.streaminganalyticsshort}} 서비스 인스턴스에 제출하십시오. 

* [신경망 데모](https://apsportal.ibm.com/exchange/public/entry/view/9fc33ce7301f10e21a9f92039ca60bb7): 샘플 데이터 세트를 작성하고 샘플 데이터의 모델을 작성한 후에 스트리밍 애플리케이션에서 해당 모델을 사용하여 스트리밍 데이터를 시각화하고, 최종적으로는 스트리밍 애플리케이션을 {{site.data.keyword.streaminganalyticsshort}} 서비스에 제출하십시오. 

## 로컬 Python 환경에서 애플리케이션 개발
 {: #t_develop_python_api}

 streamsx 패키지에 포함되어 있는 [{{site.data.keyword.streamsshort}} Python 애플리케이션 API](http://ibmstreams.github.io/streamsx.documentation/docs/python/python-appapi-devguide/#50-api-features)를 활용하면 Python 호출 가능 클래스나 함수를 사용하여 스트림 처리 애플리케이션을 작성할 수 있습니다. Python 애플리케이션 API를 사용하여 애플리케이션을 정의하고 이를 서비스에 제출할 수 있습니다. 

로컬 Python 환경에서 샘플 애플리케이션을 작성하고 이를 {{site.data.keyword.streaminganalyticsshort}} 서비스에 배치하려면 [Developing for the {{site.data.keyword.streaminganalyticsshort}} service](http://ibmstreams.github.io/streamsx.documentation/docs/python/1.6/python-appapi-devguide-2a/index.html) 튜토리얼의 단계에 따라 시작하십시오. 
