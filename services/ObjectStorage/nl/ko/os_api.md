---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Swift REST API를 사용하여 {{site.data.keyword.objectstorageshort}}에 액세스 {: #using-swift-restapi}


명령행 클라이언트 인터페이스(예: cURL)에서 Swift REST API를 사용하거나 애플리케이션에서 API를 호출할 수 있습니다.
{: shortdesc}



## OpenStack Identity(Keystone) v3 {: #keystone-authentication}

새 {{site.data.keyword.objectstorageshort}} 인스턴스를 프로비저닝하면 IBM 퍼블릭 클라우드에 격리된 Keystone 프로젝트가 작성됩니다. 

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






## {{site.data.keyword.objectstorageshort}} URL 생성 {: #access-points}

{{site.data.keyword.objectstorageshort}} API와 상호작용하려면 다음과 같이 {{site.data.keyword.objectstorageshort}} URL을 생성하십시오.
  ```
https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>
  ```
  {: pre}

<table>
  <tr>
    <th> URL 조각 </th>
    <th> 정의 </th>
  </tr>
  <tr>
    <td> API 버전 </td>
    <td> 버전 1: v1 </td>
  </tr>
  <tr>
    <td> 계정 정보 </td>
    <td> 프로젝트 ID이며 접두부가 결합되어 있습니다. UI에서 찾을 수 있습니다. </td>
  </tr>
  <tr>
    <td> 컨테이너 네임스페이스 </td>
    <td> 컨테이너의 이름입니다. UI에서 찾을 수 있습니다. </td>
  </tr>
  <tr>
    <td> 오브젝트 네임스페이스 </td>
    <td> 파일 또는 오브젝트의 이름입니다. UI에서 찾을 수 있습니다. </td>
  </tr>
  <tr>
    <td> 액세스 지점</td>
    <td> 런던: https://lon.objectstorage.open.softlayer.com/
    <br> 댈러스: https://dal.objectstorage.open.softlayer.com/ </br> </td>
  </tr>
</table>

표 1. {{site.data.keyword.objectstorageshort}} URL 조각 설명

예:

![예제 이미지에 표시된 {{site.data.keyword.objectstorageshort}} URL 조각](images/Swift_URL.png)





## {{site.data.keyword.objectstorageshort}} API {: #openstack-reference}

{{site.data.keyword.objectstorageshort}} REST API 옵션과 예제의 전체 목록은 [OpenStack Swift API 전체 참조](http://developer.openstack.org/api-ref-objectstorage-v1.html)를 참조하십시오. 
