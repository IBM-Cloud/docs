---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-05"

---
{:new_window: target="blank"}
{:shortdesc: .shortdesc}



# {{site.data.keyword.objectstorageshort}} 시작하기 {: #getting-started-with-object-storage}


{{site.data.keyword.objectstoragefull}}에서는 구조화되지 않은 클라우드 데이터 스토리지를 제공합니다. 대화식으로 앱과 서비스를 작성하고 앱과 서비스에 연결할 수 있을 뿐만 아니라 컨텐츠를 저장하고 컨텐츠에 액세스할 수 있습니다.
{: shortdesc}

{{site.data.keyword.objectstorageshort}} 서비스의 몇몇 일반적인 유스 케이스는 다음과 같습니다. 

* 인스턴스에서 볼륨 데이터 백업
* 대량의 데이터를 전송하는 경우 중개 위치로 사용
* 직접 연결되지 않은 환경 간 데이터 전송
* 중앙 저장소 역할 수행


{{site.data.keyword.Bluemix_notm}} 퍼블릭 {{site.data.keyword.objectstorageshort}}에서는 데이터를 관리할 전체 프로비저닝된 Swift {{site.data.keyword.objectstorageshort}} 계정에 대한 액세스를 제공합니다. 제공자 측 암호화는 제공되지 않습니다. 


1.	{{site.data.keyword.Bluemix_notm}} 카탈로그에서 서비스 인스턴스를 프로비저닝하십시오. 인스턴스를 구성하고 **작성**을 클릭하십시오. 초기에 **앱** 필드에 대해 **바인딩되지 않은 상태로 두기** 옵션을 선택하는 경우 나중에 서비스 인스턴스를 {{site.data.keyword.Bluemix_notm}} 앱에 바인딩할 수 있습니다. 
2. 서비스 인스턴스 대시보드에서 컨테이너를 작성하여 오브젝트 저장을 시작하십시오. 
3. **조치** 드롭 다운 메뉴에서 컨테이너에 파일을 추가하십시오. 
4. 오브젝트에 대한 액세스를 테스트하려면 **다운로드**를 클릭하고 파일을 검토하십시오. 
5. 인스턴스를 애플리케이션에 연결할 준비가 되면 서비스 신임 정보를 설정하고 [서비스 바인드](/docs/services/reqnsi.html#add_service)를 수행하십시오. 



# 관련 링크 
{: #rellinks}

## API 참조 
{: #api}
* [OpenStack {{site.data.keyword.objectstorageshort}}(Swift) API v1](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}
* [OpenStack Identity(Keystone) API v3.0](http://developer.openstack.org/api-ref-identity-v3.html){: new_window}

## SDK 
{: #sdk}
* [OpenStack 소프트웨어 개발 킷(SDK)](https://wiki.openstack.org/wiki/SDKs){: new_window}

## 튜토리얼 및 샘플 
{: #samples}
* [Java를 사용하여 IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}에 연결](https://developer.ibm.com/recipes/tutorials/connecting-to-ibm-object-storage-for-bluemix-with-java/){: new_window}
* [Python을 사용하여 {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.objectstorageshort}}에 액세스](https://developer.ibm.com/recipes/tutorials/use-python-to-access-your-bluemix-object-storage/){: new_window}
* [PHP를 사용하여 {{site.data.keyword.objectstorageshort}} 활용](https://developer.ibm.com/recipes/tutorials/use-php-to-leverage-object-storage-for-bluemix/){: new_window}

## 호환 가능 런타임 
{: #buildpacks}
* [Liberty for Java](https://www.ng.bluemix.net/docs/runtimes/liberty/index.html){: new_window}
* [SDK for Node.js](https://www.ng.bluemix.net/docs/runtimes/nodejs/index.html){: new_window}
* [Go](https://www.ng.bluemix.net/docs/runtimes/go/index.html){: new_window}
* [PHP](https://www.ng.bluemix.net/docs/runtimes/php/index.html){: new_window}
* [Python](https://www.ng.bluemix.net/docs/runtimes/python/index.html){: new_window}
* [Ruby](https://www.ng.bluemix.net/docs/runtimes/ruby/index.html){: new_window}
* [커뮤니티 빌드팩](https://www.ng.bluemix.net/docs/starters/byob.html){: new_window}


## 관련 링크 
{: #general}
* [IBM {{site.data.keyword.Bluemix_notm}} 가격 책정 시트](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM {{site.data.keyword.Bluemix_notm}} 전제조건](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
