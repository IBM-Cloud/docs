---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Swift REST API를 사용하는 {{site.data.keyword.objectstorageshort}} URL 생성

명령행 클라이언트 인터페이스(예: cURL)에서 Swift REST API를 사용하거나 애플리케이션에서 API를 호출할 수 있습니다.
{: shortdesc}


전체 {{site.data.keyword.objectstorageshort}} REST API 옵션과 예제 목록은 [OpenStack Swift API 전체 참조](http://developer.openstack.org/api-ref-objectstorage-v1.html)를 확인하십시오. 

Keystone으로 서비스 인스턴스를 인증한 경우, 카탈로그 응답을 기록하십시오. 이 응답은 다음 예제와 유사합니다. 

```
{
  "id" : "4207049680fa4effbecd044c7448a8cb",
  "region" : "dallas",
  "region_id" : "dallas",
  "url" : "https://dal.objectstorage.open.softlayer.com/v1/AUTH_4abf7d7bac2c4eda89c03dd3afa7a0a3",
  "interface" : "public"
},
```
{: codeblock}


다음 이미지와 같이 컨테이너와 오브젝트의 네임스페이스를 {{site.data.keyword.objectstorageshort}} URL의 끝에 추가하십시오. 

  ![{{site.data.keyword.objectstorageshort}}예제 이미지에 표시된 URL 조각](images/swift_URL.png)
  그림 1: {{site.data.keyword.objectstorageshort}} URL 예제
