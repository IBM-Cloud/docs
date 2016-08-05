{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} 문제점 해결
{: #troubleshooting}

*마지막 업데이트 날짜: 2016년 6월 24일*
{: .last-updated}

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
