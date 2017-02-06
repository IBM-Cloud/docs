---



copyright:

  years: 2015，2017

lastupdated: "2016-03-15"


---

{:shortdesc: .shortdesc}

# VCAP 서비스


VCAP_SERVICES 환경 변수는 {{site.data.keyword.Bluemix_notm}}의 서비스 인스턴스와 상호작용하는 데 사용할 수 있는 정보가 포함된 JSON 오브젝트입니다.
{:shortdesc}


## VCAP_SERVICES 환경 변수의 값 검색
{:retrieving}

VCAP_SERVICES 환경 변수는 {{site.data.keyword.Bluemix_notm}}의 서비스 인스턴스와 상호작용하는 데 사용할 수 있는 정보가 포함된 JSON 오브젝트입니다. 이러한 정보로는 서비스 인스턴스 이름, 신임 정보 및 서비스 인스턴스의 연결 URL 등이 있습니다. 애플리케이션이 {{site.data.keyword.Bluemix_notm}}의 서비스 인스턴스에 바인딩된 경우 이러한 값이 VCAP_SERVICES 환경 변수에 채워집니다.

VCAP_SERVICES 환경 변수의 값은 서비스 인스턴스를 애플리케이션에 바인딩한 경우에만 사용할 수 있습니다. 다음 명령을 사용하여 애플리케이션 환경 변수를 볼 수 있습니다. 
```
cf env APP_NAME
```
