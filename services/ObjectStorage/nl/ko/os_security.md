---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 파일 보호 {: #understanding-authentication}
*마지막 업데이트 날짜: 2016년 10월 19일*
{: .last-updated}

## OpenStack Identity(Keystone) v3 {: #keystone-authentication}

새 {{site.data.keyword.objectstorageshort}} 인스턴스를 프로비저닝하면 IBM 퍼블릭 클라우드에 격리된 Keystone 프로젝트가 작성됩니다.
{: shortdesc}

신임 정보 구조는 사용자 앱에 최적으로 맞는 OpenStack 토큰 요청 메소드 또는 OpenStack SDK를 선택할 수 있는 전체 속성 세트를 포함합니다. 새 앱을 인스턴스에 바인딩하면 프로젝트에 대한 액세스 권한이 있는 새 Keystone 사용자가 작성됩니다. 인스턴스를 디프로비저닝하면 프로젝트 및 사용자가 삭제됩니다. 

OpenStack Swift 및 Keystone 사용에 대한 자세한 정보는 [OpenStack 문서 사이트](http://docs.openstack.org)를 참조하십시오. 

권장되는 v3 토큰 요청은 아래 curl 명령에 표시된 것처럼 다음 사이트에 대한 POST 요청입니다. https://identity.open.softlayer.com/v3/auth/tokens

```
	curl -i \
	  -H "Content-Type: application/json" \
	  -d '
	{
		"auth": {
			"identity": {
				"methods": [
					"password"
				],
				"password": {
					"user": {
						"id": "ad78b2a3f843466988afd077731c61fc",
						"password": "XXXXXXXXXX"
					}
				}
			},
			"scope": {
				"project": {
					"id": "0f47b41b06d047f9aae3b33f1db061ed"
				}
			}
		}
	}' \
	  https://identity.open.softlayer.com/v3/auth/tokens ; echo
```
{: codeblock}

{{site.data.keyword.objectstorageshort}} 서비스에 요청을 작성하는 경우 응답 헤더의 `X-Subject-Token` 필드 값을 `X-Auth-Token` 필드로 사용하십시오. 

예제 응답은 다음과 같습니다. {{site.data.keyword.objectstorageshort}} 관련 정보만 표시하도록 응답이 조정됩니다. 

```
	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json

	{
	  "token" : {
	    "roles" : [
	      {
	        "id" : "f61f06a84f6443e880210fa986bd8691",
	        "name" : "ObjectStorageOperator"
	      }
	    ],
	    "catalog" : [
	      {
	        "endpoints" : [
	          {
	            "id" : "20cbfa6ff22b4a67a1484d30235bfc80",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "38b8c081b11a452bb951698c334a406d",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          },
	          {
	            "id" : "4207049680fa4effbecd044c7448a8cb",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "a60cf32be624491d89170ef8264de5e8",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "c769862200124a308d6748e418c971ba",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          }
	        ],
	        "id" : "896e4064cbe742afbf9a543c15f27ac0",
	        "type" : "object-store",
	        "name" : "swift"
	      },
	    ],
	    "extras" : {},
	    "user" : {
	      "id" : "0b8aebd924ef4cc7aa9232f07e47e874",
	      "name" : "user_87c094ce47a9feae3a137ffcbbfa098a888c12a8",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "expires_at" : "2016-02-29T22:03:42.061343Z",
	    "audit_ids" : [
	      "cbA-iL2dSheyB72PHd7q8Q"
	    ],
	    "issued_at" : "2016-02-29T21:03:42.000000Z",
	    "project" : {
	      "id" : "3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	      "name" : "object_storage_c1d8b3a1",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "methods" : [
	      "password"
	    ]
	  }
	}
```
{: screen}

{{site.data.keyword.objectstorageshort}} URL은 서비스 카탈로그에 있습니다. 서비스 카탈로그는 토큰 요청의 응답 본문에 포함되어 있습니다. 응답은 사용 가능한 OpenStack 서비스의 전체 카탈로그입니다. `object-store` 유형의 서비스 카탈로그에서 엔드포인트를 선택하고 신임 정보의 지역 필드와 일치하는 지역을 선택하십시오. 

**참고:** 공용 인터페이스(`publicURL`)를 사용하십시오. 내부 인터페이스(`internalURL`)는 {{site.data.keyword.Bluemix_notm}}에서 액세스할 수 없습니다. 


## 서비스 신임 정보 이해 {: #understanding-credentials}

서비스 신임 정보는 서비스에 필요한 인증과 보안을 제공하는 데 사용됩니다. 신임 정보 세트는 인스턴스가 프로비저닝될 때 자동으로 생성됩니다. Swift 클라이언트는 다음 표에 있는 환경 변수에서 인증 정보를 가져옵니다. 

<table>
  <tr>
    <th> 환경 변수 </th>
    <th> 설명 </th>
  </tr>
  <tr>
    <td> `OS_USER_ID` </td>
    <td> {{site.data.keyword.objectstorageshort}} 사용자 ID입니다. </td>
  </tr>
  <tr>
    <td> `OS_PASSWORD` </td>
    <td> {{site.data.keyword.objectstorageshort}} 인스턴스의 비밀번호입니다. </td>
  </tr>
  <tr>
    <td> `OS_PROJECT_ID` </td>
    <td> 프로젝트 ID입니다. </td>
  </tr>
  <tr>
    <td> `OS_REGION_NAME` </td>
    <td> 오브젝트가 저장되는 지역입니다. 댈러스 지역과 런던 지역에서 {{site.data.keyword.objectstorageshort}}를 사용할 수 있습니다. </td>
  </tr>
  <tr>
    <td> `OS_AUTH_URL` </td>
    <td> 엔드포인트 URL입니다. `/v3`가 URL의 끝에 추가되었는지 확인하십시오. </td>
  </tr>
</table>

*표 1: 인증 변수와 설명*

####  UI에 서비스 신임 정보 추가
1. 서비스 인스턴스 대시보드의 **서비스 신임 정보** 탭에서 **새 신임 정보**를 클릭하고 이름을 지정하십시오. 
2. (*선택사항*) **인라인 구성 매개변수 추가** 텍스트 필드에 작성할 역할에 대한 신임 정보를 입력하십시오. 이 정보는 JSON 페이로드로 형식화되어야 합니다. {{site.data.keyword.objectstorageshort}} 사용자 역할에 대한 자세한 정보는 [액세스 유형](../os_security.html#access-types)을 참조하십시오. 
    - 관리 사용자 작성: `{"role":"admin"}`
    - 비관리 사용자 작성: `{"role":"member"}`
3. **추가**를 클릭하십시오.


## 액세스 유형 {: #access-types}

서비스에 대한 액세스는 사용자 역할 및 컨테이너 액세스 제어 목록에 의해 제어됩니다. {{site.data.keyword.objectstorageshort}} 사용자는 관리자 또는 비관리자일 수 있습니다. 액세스 제어 목록은 컨테이너 레벨에서 관리자에 의해 사용될 수 있으며 서비스 인스턴스, 스토리지 계정 또는 프로젝트 레벨에 대해 사용할 수 없습니다.

<table>
  <tr>
    <th> 관리 사용자(admin) </th>
    <th> 비관리 사용자(member) </th>
  </tr>
  <tr>
    <td> 액세스 제어 관리 </td>
    <td> 기본적으로 서비스 또는 해당 컨테이너에 대한 액세스가 없음 </td>
  </tr>
  <tr>
    <td> 컨테이너를 작성하고 삭제할 수 있음 </td>
    <td> 컨테이너 읽기/쓰기 ACL을 기반으로 하여 조치를 수행할 수 있음 </td>
  </tr>
  <tr>
    <td> 컨테이너에 대해 읽고 쓸 수 있음 </td>
    <td> admin에 의해 결정된 대로 조치를 수행할 수 있음 </td>
  </tr>
</table>

*표 2: 정의된 사용자 역할*

{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스, Cloud Foundry API 또는 Cloud Foundry CLI를 통해 {{site.data.keyword.objectstorageshort}} 사용자를 관리할 수 있습니다.




## 읽기 액세스 권한 부여 {: #read-access}

admin 역할을 가진 {{site.data.keyword.objectstorageshort}} 사용자는 다른 사용자의 컨테이너에 대한 읽기 액세스 권한을 부여하고 읽기 ACL 조합을 조작할 수 있습니다. 

<table>
  <tr>
    <th> 권한 </th>
    <th> 읽기 ACL 옵션 </th>
  </tr>
  <tr>
    <td> 계정 소속에 상관없이 모든 참조자 읽기 </td>
    <td> `.r,*` </td>
  </tr>
  <tr>
    <td> 모든 참조자 및 목록에 대한 읽기 및 나열 </td>
    <td> `.r:*,.rlistings` </td>
  </tr>
  <tr>
    <td> 특정 프로젝트의 지정된 사용자에 대한 읽기 및 나열 </td>
    <td> `< project_id>:< user_id>` </td>
  </tr>
  <tr>
    <td> 모든 프로젝트의 지정된 사용자에 대한 읽기 및 나열 </td>
    <td> `<*>:< user_id>` </td>
  </tr>
  <tr>
    <td> 지정된 프로젝트의 모든 사용자에 대한 읽기 및 나열 </td>
    <td> `< project_id>:<*>` </td>
  </tr>
  <tr>
    <td> 모든 프로젝트의 모든 사용자에 대한 읽기 및 나열 </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*표 3: 옵션별 읽기 액세스 권한*



1. 신임 정보를 인증하십시오. UI의 서비스 신임 정보 탭에 있는 신임 정보를 사용하거나 새 신임 정보를 생성할 수 있습니다. 새 신임 정보 생성에 대한 자세한 정보는 [서비스 신임 정보 생성](insert link here)을 참조하십시오. 출력으로 {{site.data.keyword.objectstorageshort}} URL과 인증 토큰을 수신합니다. Swift 명령:
    
    ```
  export OS_USER_ID=<user_id>
  export OS_PASSWORD=<password>
  export OS_TENANT_ID=<project_id>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
    ```
    {: codeblock}
    
    cURL 명령:
    
    ```
    curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
    ```
    {: pre}
    
2. 다음 명령을 실행하여 읽기 액세스 권한을 부여하십시오.
    Swift 명령:
    
    ```
    swift post <container_name> --read-acl "<user_id>:<project_id>"
    ```
    {: pre}
    
    cURL 명령:
    
    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
    {: pre}
    **참고**: 액세스 제어 목록을 구분하려면 쉼표(,)를 사용하십시오.


3. 읽기 ACL 값을 확인하십시오.Swift 명령:
    
    ```
  swift stat <container_name>
  ```
    {: pre}
    cURL 명령:
    
    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}
    
    다음 예제 출력에서 읽기 액세스 권한이 부여된 것을 확인할 수 있습니다. 
    
    ```
    HTTP/1.1 204 No Content
    Content-Length: 0
    X-Container-Object-Count: 1
    Accept-Ranges: bytes
    X-Storage-Policy: standard
    X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
    X-Container-Bytes-Used: 31512
    X-Timestamp: 1462818314.11220
    Content-Type: text/plain; charset=utf-8
    X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
    Date: Tue, 28 Jun 2016 20:57:58 GMT
    ```
    {: screen}



## 쓰기 액세스 권한 부여 {: #write-access}

admin 역할을 가진 {{site.data.keyword.objectstorageshort}} 사용자는 다른 사용자의 컨테이너에 대한 쓰기 액세스 권한을 부여하고 쓰기 ACL 조합을 조작할 수 있습니다. 

<table>
  <tr>
    <th> 권한 </th>
    <th> 쓰기 ACL 옵션 </th>
  </tr>
  <tr>
    <td> 특정 프로젝트의 지정된 사용자에 대한 쓰기 </td>
    <td> `<project_id>:<user_id>` </td>
  </tr>
  <tr>
    <td> 모든 프로젝트의 지정된 사용자에 대한 쓰기 </td>
    <td> `*:<user_id>` </td>
  </tr>
  <tr>
    <td> 지정된 프로젝트의 모든 사용자에 대한 쓰기 </td>
    <td> `<project_id>:<*>` </td>
  </tr>
  <tr>
    <td> 모든 프로젝트의 모든 사용자에 대한 쓰기 </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*표 4: 옵션별 쓰기 액세스 권한*




1. 사용자가 작성한 서비스 신임 정보 내에 있는 정보를 사용하여 신임 정보를 인증하십시오. 출력으로 {{site.data.keyword.objectstorageshort}} URL과 인증 토큰을 수신합니다.
    Swift 명령:
    
    ```
    export OS_USER_ID="<user_id>"
    export OS_PASSWORD="<password>"
    export OS_TENANT_ID=<project_id>
    export OS_AUTH_URL=https://identity.open.softlayer.com/v3
    export OS_REGION_NAME=<region>
    export OS_IDENTITY_API_VERSION=3
    export OS_AUTH_VERSION=3

    swift auth
    ```
    {: codeblock}
    
    cURL 명령:
    
    ```
    curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
    ```
    {: pre}
    
2. 다음 명령을 실행하여 쓰기 액세스 권한을 부여하십시오.
    Swift 명령:
    
    ```
    swift post <container_name> --write-acl "<user_id>:<project_id>"
    ```
    {: pre}
    
    cURL 명령:
    
    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"

  ```
    {: pre}
    
    **참고**: 액세스 제어 목록을 구분하려면 쉼표(,)를 사용하십시오. 

3. 쓰기 ACL 값을 확인하십시오.Swift 명령:
    
    ```
  swift stat <container_name>
  ```
    {: pre}
    
    cURL 명령:
    
    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}



## 액세스 제거 {: #removing-access}

컨테이너에서 읽기 ACL 제거:
* Swift 명령:

    ```
  swift post <container_name> --read-acl “”
  ```
    {: pre}
    
*  cURL 명령:

    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
    {: pre}

컨테이너에서 쓰기 ACL 제거:

* Swift 명령:

    ```
  swift post <container_name> --write-acl “”
  ```
    {: pre}
    
*    cURL 명령: 

    ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
    {: pre}

ACL을 제거했는지 여부 확인:

* Swift 명령:

    ```
  swift stat <container_name>
  ```
    {: pre}

  다음 예제 출력에서는 읽기 ACL과 쓰기 ACL을 공백으로 표시하며 이는 액세스 권한이 제거되었음을 의미합니다. 
  
  ```
         Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8

  ```
  {: screen}

*   cURL 명령: 
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
  {: pre}
