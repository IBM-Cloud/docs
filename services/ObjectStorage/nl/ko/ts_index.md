---

copyright:
  years: 2014, 2016

---

{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} 문제점 해결
{: #troubleshooting}

*마지막 업데이트 날짜: 2016년 8월 17일*
{: .last-updated}

다음은 {{site.data.keyword.objectstoragefull}} 사용에 대한 일반적인 문제점 해결 질문에 대한 응답입니다.

## Liberty Profile이 포함된 openstack4J를 사용하는 경우 인식되지 않은 토큰 컨텐츠팩이 리턴됨
{: #unrecognized_token}

### 증상

Liberty Profile이 포함된 openstack4J를 사용하는 경우 다음 스택 추적이 발생할 수 있습니다. 

    Exception thrown by application class 'org.openstack4j.connectors.okhttp.HttpResponseImpl.readEntity:124'
    org.openstack4j.api.exceptions.ClientResponseException: Unrecognized token 'contentpack': was expecting ('true', 'false' or 'null') at [Source: contentpack ; line: 1, column: 12]
    at org.openstack4j.connectors.okhttp.HttpResponseImpl.readEntity(HttpResponseImpl.java:124)
    at org.openstack4j.core.transport.HttpEntityHandler.handle(HttpEntityHandler.java:56)
    at org.openstack4j.connectors.okhttp.HttpResponseImpl.getEntity(HttpResponseImpl.java:68)
    at org.openstack4j.openstack.internal.BaseOpenStackService$Invocation.execute(BaseOpenStackService.java:169)
    at org.openstack4j.openstack.internal.BaseOpenStackService$Invocation.execute(BaseOpenStackService.java:163)
    at org.openstack4j.openstack.storage.object.internal.ObjectStorageContainerServiceImpl.list(ObjectStorageContainerServiceImpl.java:41)
    at com.mimotic.SecureMessageApp.HelloResource.getInformation(HelloResource.java:47)
    at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
    at sun.reflect.NativeMethodAccessorImpl.invoke(Unknown Source)
    at sun.reflect.DelegatingMethodAccessorImpl.invoke(Unknown Source)
    at java.lang.reflect.Method.invoke(Unknown Source)

### 솔루션

이 문제점은 Liberty Profile에 제공되는 동일한 패키지의 일부가 openstack4j 라이브러리에 포함되는 클래스 로드 문제가 원인입니다. 예를 들어, OpenStack4j는 JERSEY를 사용하며 이는 Wink 라이브러리와 충돌할 수 있습니다. 

문제점을 해결하려면 다음 단계를 따르십시오. 

1. 역방향 클래스로딩을 사용합니다(parentLast).
2. 사용하도록 설정된 기능에서 jaxrs를 제외합니다. 

## {{site.data.keyword.objectstorageshort}}에 대한 도움말 가져오기 및 지원
{: #gettinghelp}

{{site.data.keyword.objectstoragefull}} 사용에 대한 문제점 또는 질문이 있는 경우, 정보를 검색하거나 포럼을 통해 질문하여 도움말을 가져올 수 있습니다. 또한 지원 티켓을 열 수도 있습니다.

포럼을 통해 질문하는 경우, {{site.data.keyword.Bluemix_notm}} 개발 팀이 볼 수 있도록 질문에 태그를 지정하십시오.

* {{site.data.keyword.objectstorageshort}}에 대한 기술적인 질문이 있는 경우, [스택 오버플로우](http://stackoverflow.com/search?q=object-storage+ibm-bluemix){:new_window}에 질문을 게시하고 "ibm-bluemix" 및 "object-storage"를 사용하여 질문을 태그하십시오.
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* 서비스 및 시작하기 지시사항에 대한 질문은 [IBM developerWorks dW 응답](https://developer.ibm.com/answers/topics/object-storage/?smartspace=bluemix){:new_window} 포럼을 사용하십시오. "object-storage" 및 "bluemix" 태그를 포함하십시오.

포럼 사용에 대한 자세한 정보는 [도움말 가져오기](https://console.ng.bluemix.net/docs/support/index.html#getting-help)를 참조하십시오.

IBM 지원 티켓 열기 또는 지원 레벨 및 티켓 심각도에 대한 정보는 [지원 문의](https://console.ng.bluemix.net/docs/support/index.html#contacting-support)를 참조하십시오.
