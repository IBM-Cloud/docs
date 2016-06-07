---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:new_window: target="_blank"}

#앱 개발 
{: #develop-apps-IDS}

*마지막 업데이트 날짜: 2015년 12월 07일*  

IDE(Integrated Development Environment) 또는 문서 편집기를 사용하여
애플리케이션을 개발하거나 {{site.data.keyword.jazzhub}}를
사용할 수 있습니다. 
{: shortdesc}

##Bluemix DevOps Services로 애플리케이션 개발
{: #dev_ops}

{{site.data.keyword.jazzhub_short}}를 사용하여
클라우드에서 애플리케이션을 개발, 추적 및 계획한 다음
{{site.data.keyword.Bluemix_notm}}에 배치할 수 있습니다. 몇 분 안에 소스 코드에서 실행 중인 애플리케이션으로 이동할 수 있습니다.  

{{site.data.keyword.jazzhub_short}}는
{{site.data.keyword.trackplan}} 및 {{site.data.keyword.deliverypipeline}}이라는 두 개의 서비스를 제공합니다. {{site.data.keyword.trackplan}} 서비스는
Agile 플랜에 사용되고, {{site.data.keyword.deliverypipeline}} 서비스는 빌드 및 배치를 자동으로 수행합니다. 이러한 서비스는
{{site.data.keyword.Bluemix_notm}} 카탈로그에서 찾을 수 있습니다. 이러한 서비스를 사용하는 방법에 대한 자세한 정보는
[Track & Plan 시작하기](../services/TrackPlan/index.html#gettingstartedtemplate) 및
[Delivery Pipeline 시작하기](../services/DeliveryPipeline/index.html#getstartwithCD)를 참조하십시오. 

{{site.data.keyword.jazzhub_short}}는 소스 제어용 Git 호스팅 및 코드를 편집, 관리 및 배치할 수 있는 Web IDE도
제공합니다. 앱에서 앱 개요 페이지의 오른쪽 상단에 있는 **Git 추가** 링크를 클릭하여
Git 호스팅을 설정할 수 있습니다. 그런 다음, **코드 편집**을 클릭하여 Web IDE에서 앱 코드를
편집할 수 있습니다. Web IDE 쉘에서 컨텐츠 지원을 제공하는 cf 명령을 실행할 수 있습니다. 예를 들어 다음 명령을 입력하여 모든 Cloud Foundry 명령 목록을 가져올 수 있습니다.  
```
help cfo
```
{:pre}
