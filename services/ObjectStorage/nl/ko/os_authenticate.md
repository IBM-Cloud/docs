---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Keystone으로 {{site.data.keyword.objectstorageshort}} 인스턴스 인증

서비스와 상호작용하려면 Keystone으로 {{site.data.keyword.objectstorageshort}} 인스턴스를 인증하여 URL과 소유자 토큰을 가져와야 합니다.
{: shortdesc}


새 {{site.data.keyword.objectstorageshort}} 인스턴스를 프로비저닝하면 IBM 퍼블릭 클라우드에 격리된 Keystone 프로젝트가 작성됩니다. Keystone 신임 정보 구조에는 사용자 앱에 가장 적합한 OpenStack 토큰 요청 메소드 또는 OpenStack SDK를 선택할 수 있도록 전체 속성 세트가 포함되어 있습니다. 새 앱을 인스턴스에 바인딩하면 프로젝트에 대한 액세스 권한이 있는 새 Keystone 사용자가 작성됩니다. 인스턴스를 프로비저닝 해제하면 프로젝트 및 사용자가 삭제됩니다. 

OpenStack Swift 및 Keystone 사용에 대한 자세한 정보는 [OpenStack 문서 사이트](http://docs.openstack.org)를 참조하십시오. 

1. 다음 cURL 명령에 표시된 대로 `https://identity.open.softlayer.com/v3/auth/tokens`에 대한 POST 요청을 작성하십시오. 
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

2. 카탈로그 응답에서 `object-store` 엔드포인트를 선택하고 이를 기록하십시오. 이는 전체 URL을 구성할 때 필요합니다. 다음 응답 예제는 {{site.data.keyword.objectstorageshort}} 관련 정보만 표시하도록 편집되었습니다. 

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
  	            "url" : "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "admin"
  	          },
  	          {
  	            "id" : "38b8c081b11a452bb951698c334a406d",
  	            "region" : "london",
  	            "region_id" : "london",
  	            "url" : "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "internal"
  	          },
  	          {
  	            "id" : "4207049680fa4effbecd044c7448a8cb",
                "region" : "dallas",
                "region_id" : "dallas",
                "url" : "https://dal.objectstorage.open.softlayer.com/v1/AUTH_4abf7d7bac2c4eda89c03dd3afa7a0a3",
                "interface" : "public"
  	          },
  	          {
  	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
  	            "region" : "london",
  	            "region_id" : "london",
  	            "url" : "https://lon.objectstorage.open.softlayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "public"
  	          },
  	          {
  	            "id" : "a60cf32be624491d89170ef8264de5e8",
  	            "region" : "dallas",
  	            "region_id" : "dallas",
  	            "url" : "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "admin"
  	          },
  	          {
  	            "id" : "c769862200124a308d6748e418c971ba",
  	            "region" : "dallas",
  	            "region_id" : "dallas",
  	            "url" : "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "internal"
  	          }
  	        ],
  	        "id" : "896e4064cbe742afbf9a543c15f27ac0",
  	        "type" : "object-store",
  	        "name" : "swift"
  	      },
  	    ],
  	    "extras" : {

  	    },
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

  <table>
  <caption> 표 1. Post 요청 응답 설명 </caption>
    <tr>
      <th> 응답 엔드포인트 </th>
      <th> 설명 </th>
    </tr>
    <tr>
      <td> <code> X-Subject-Token </code> </td>
      <td> 사용자의 인증 토큰입니다. </td>
    </tr>
    <tr>
      <td> <code> id </code> </td>
      <td> 사용자의 {{site.data.keyword.objectstorageshort}} 인스턴스 ID입니다. </td>
    </tr>
    <tr>
      <td> <code> region </code> </td>
      <td> 스토리지 지역입니다. 반드시 신임 정보에 있는 필드와 일치하는 지역을 선택하십시오. </td>
    </tr>
    <tr>
      <td> <code> url </code> </td>
      <td> {{site.data.keyword.objectstorageshort}} URL입니다. </td>
    </tr>
    <tr>
      <td> <code> interface </code> </td>
      <td> 내부 인터페이스는 {{site.data.keyword.Bluemix_notm}}에서 액세스할 수 없습니다. 공용 인터페이스(<code>publicURL</code>)를 사용하십시오. </td>
    </tr>
  </table>
