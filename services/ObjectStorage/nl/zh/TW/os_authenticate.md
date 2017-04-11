---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 使用 Keystone 鑑別您的 {{site.data.keyword.objectstorageshort}} 實例

如果要與服務互動，您必須使用 Keystone 鑑別 {{site.data.keyword.objectstorageshort}} 實例，以取得您的 URL 和載送記號。
{: shortdesc}


佈建新的 {{site.data.keyword.objectstorageshort}} 實例會在 IBM Public Cloud 中建立隔離的 Keystone 專案。Keystone 認證結構包含一組完整的屬性，以便您可以選擇最符合您應用程式的 OpenStack 記號要求方法或 OpenStack SDK。當您將新的應用程式連結至實例時，會建立具有專案存取權的新 Keystone 使用者。當您取消佈建實例時，會刪除專案及使用者。

如需使用 OpenStack Swift 和 Keystone 的相關資訊，請檢視 <a href="http://docs.openstack.org" target="_blank">OpenStack 文件網站 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。



1. 對 `https://identity.open.softlayer.com/v3/auth/tokens` 提出 POST 要求，如下列 cURL 指令中所示。
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

2. 從型錄回應中選取 `object-store` 端點並記錄。您需要它才能建構完整 URL。下列回應範例已經過修整，只顯示與 {{site.data.keyword.objectstorageshort}} 相關的資訊。

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

  <table>
  <caption> 表 1. 說明的 POST 要求回應</caption>
    <tr>
      <th> 回應端點</th>
      <th> 說明</th>
    </tr>
    <tr>
      <td> <code> X-Subject-Token </code> </td>
      <td> 您的鑑別記號。</td>
    </tr>
    <tr>
      <td> <code> id </code> </td>
      <td> 您的 {{site.data.keyword.objectstorageshort}} 實例 ID。</td>
    </tr>
    <tr>
      <td> <code> region </code> </td>
      <td> 您的儲存空間地區。請務必選取符合認證中所列欄位的地區。</td>
    </tr>
    <tr>
      <td> <code> url </code> </td>
      <td> 您的 {{site.data.keyword.objectstorageshort}} URL。</td>
    </tr>
    <tr>
      <td> <code> interface </code> </td>
      <td> 無法從 {{site.data.keyword.Bluemix_notm}} 存取內部介面。請使用公用介面 (<code>publicURL</code>)。</td>
    </tr>
  </table>
