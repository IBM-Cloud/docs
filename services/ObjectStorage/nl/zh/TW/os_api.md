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

# 使用 Swift REST API 來存取 {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}


您可以搭配使用 Swift REST API 與指令行用戶端介面（例如 cURL），或是從應用程式中呼叫 API。
{: shortdesc}



## OpenStack Identity (Keystone) 第 3 版 {: #keystone-authentication}

佈建新的 {{site.data.keyword.objectstorageshort}} 實例會在 IBM Public Cloud 中建立隔離的 Keystone 專案。


認證結構包含一組完整的屬性，可讓您選擇最符合您應用程式的 OpenStack 記號要求方法或 OpenStack SDK。當您將新的應用程式連結至實例時，會建立具有專案存取權的新 Keystone 使用者。當您取消佈建實例時，會刪除專案及使用者。

如需使用 OpenStack Swift 和 Keystone 的相關資訊，請檢視 [OpenStack 文件網站](http://docs.openstack.org)。

建議的第 3 版記號要求是 https://identity.open.softlayer.com/v3/auth/tokens 的 POST 要求，如下列 curl 指令中所示：
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

當您對 {{site.data.keyword.objectstorageshort}} 服務發出要求時，請使用回應標頭中 `X-Subject-Token` 欄位的值作為 `X-Auth-Token` 欄位。

範例回應如下。回應會縮減為只顯示 {{site.data.keyword.objectstorageshort}} 相關資訊。
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

{{site.data.keyword.objectstorageshort}} URL 位在服務型錄中。服務型錄包含在記號要求的回應內文中。回應是可用的 OpenStack 服務的完整型錄。從服務型錄中選取類型為 `object-store` 的端點，以及符合認證中地區欄位的地區。

**附註：**請使用公用介面（`publicURL`)。無法從 {{site.data.keyword.Bluemix_notm}} 存取內部介面 (`internalURL`)。






## 建構 {{site.data.keyword.objectstorageshort}} URL {: #access-points}

若要與 {{site.data.keyword.objectstorageshort}} API 進行互動，請如下所示建構 {{site.data.keyword.objectstorageshort}} URL：
  ```
https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>
  ```
  {: pre}

<table>
  <tr>
    <th> URL 部分  </th>
    <th> 定義</th>
  </tr>
  <tr>
    <td> API 版本  </td>
    <td> 第 1 版：v1</td>
  </tr>
  <tr>
    <td> 帳戶資訊  </td>
    <td> 這合併了 ProjectID 與字首兩者。您可以在使用者介面中找到它。</td>
  </tr>
  <tr>
    <td> 容器名稱空間  </td>
    <td> 容器的名稱。您可在使用者介面中找到它。</td>
  </tr>
  <tr>
    <td> 物件名稱空間  </td>
    <td> 檔案或物件的名稱。您可在使用者介面中找到它。</td>
  </tr>
  <tr>
    <td> 存取點</td>
    <td> 倫敦：https://lon.objectstorage.open.softlayer.com/
    <br> 達拉斯：https://dal.objectstorage.open.softlayer.com/ </br> </td>
  </tr>
</table>

表 1. 說明的 {{site.data.keyword.objectstorageshort}} URL 部分

例如：

![範例影像中所顯示的 {{site.data.keyword.objectstorageshort}} URL 部分](images/Swift_URL.png)





## {{site.data.keyword.objectstorageshort}} API {: #openstack-reference}

如需 {{site.data.keyword.objectstorageshort}} REST API 選項及範例的綜合性清單，請參閱 [OpenStack Swift API Complete Reference](http://developer.openstack.org/api-ref-objectstorage-v1.html)。
