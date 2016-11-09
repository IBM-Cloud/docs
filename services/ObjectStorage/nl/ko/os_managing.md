---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 지역에서 {{site.data.keyword.objectstorageshort}} 관리 {: #multi-regions}
*마지막 업데이트 날짜: 2016년 10월 19일*
{: .last-updated}

{{site.data.keyword.objectstorageshort}} 서비스에서는 댈러스 스토리지 지역과 런던 스토리지 지역을 지원합니다. 해당 스토리지 지역은 {{site.data.keyword.objectstorageshort}} 서비스 인스턴스가 작성되는 {{site.data.keyword.Bluemix_notm}} 지역(예: 미국 남부와 영국)에 독립적입니다. 미국 남부 {{site.data.keyword.Bluemix_notm}} 지역에서 인스턴스를 작성하는 경우 댈러스 또는 런던 스토리지 지역에서 데이터를 읽고 쓸 수 있습니다.
{: shortdesc}

미국 남부 {{site.data.keyword.Bluemix_notm}} 지역의 경우 댈러스 스토리지 지역이 기본입니다. 영국 {{site.data.keyword.Bluemix_notm}} 지역의 경우에는 런던 스토리지 지역이 기본입니다. {{site.data.keyword.objectstorageshort}} 사용자 인터페이스는 항상 {{site.data.keyword.Bluemix_notm}} 지역의 기본 스토리지 지역으로 시작합니다. 지역을 전환하려면 {{site.data.keyword.objectstorageshort}} 지역 드롭 다운 목록을 클릭한 후 다른 지역을 선택하십시오.

**참고:** {{site.data.keyword.objectstorageshort}} 서비스는 스토리지 지역 간 복제를 지원하지 않습니다.

### 다중 지역 액세스

{{site.data.keyword.objectstorageshort}} 서비스를 사용하려면 [OpenStack Keystone에 인증](../ObjectStorage/os_security.html#keystone-authentication){: new_window}해야 합니다. 인증이 완료되면 응답에서 `X-Subject-Token` 엔드포인트와 {{site.data.keyword.objectstorageshort}} 엔드포인트를 사용할 수 있습니다. 각 스토리지 지역의 [액세스 지점](../ObjectStorage/os_api.html#access-points)은 서로 다릅니다. 


예를 들어, 댈러스 스토리지 지역에 `my_container` 컨테이너를 작성하려면 다음과 같이 curl 명령에 댈러스 액세스 지점을 지정하십시오. 

  ```
  curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
다음과 같은 출력이 수신됩니다.

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

런던 스토리지 지역에서 `my_container` 컨테이너를 작성하려면, 다음과 같이 curl 명령에 런던 액세스 지점을 지정하십시오. 

  ```
  curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
다음과 같은 출력이 수신됩니다.

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

**참고:** Keyston에서 획득한, 예제에서 `X-Trans-ID`로 레이블이 지정된 `X-Subject-Token`은 여러 스토리지 지역에서 작동합니다. 
