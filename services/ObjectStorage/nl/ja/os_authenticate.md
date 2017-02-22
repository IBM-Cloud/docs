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


# Keystone を使用した {{site.data.keyword.objectstorageshort}} インスタンスの認証

サービスと対話するには、Keystone を使用して {{site.data.keyword.objectstorageshort}} インスタンスを認証し、URL とベアラー・トークンを取得する必要があります。
{: shortdesc}


新しい {{site.data.keyword.objectstorageshort}} インスタンスをプロビジョンすると、IBM Public Cloud に独立した Keystone プロジェクトが作成されます。アプリに最適な OpenStack トークン要求メソッドまたは OpenStack SDK を選択できるように、Keystone の資格情報構造体には完全な属性セットが含まれています。インスタンスに新しいアプリをバインドすると、プロジェクトへのアクセス権限を持つ新しい Keystone ユーザーが作成されます。インスタンスをプロビジョン解除すると、プロジェクトとユーザーは削除されます。

OpenStack Swift および Keystone について詳しくは、[OpenStack 資料サイト](http://docs.openstack.org)を参照してください。

1. 以下の cURL コマンドに示されているように、`https://identity.open.softlayer.com/v3/auth/tokens` への POST 要求を実行します。
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

2. カタログ応答から `object-store` エンドポイントを選択し、メモします。完全な URL を作成するために必要になります。以下の応答例は、{{site.data.keyword.objectstorageshort}} に関連した情報のみを示すように切り取られています。

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
  <caption> 表 1. POST 要求の応答の説明</caption>
    <tr>
      <th> 応答エンドポイント </th>
      <th> 説明 </th>
    </tr>
    <tr>
      <td> <code> X-Subject-Token </code> </td>
      <td> ご使用の認証トークン。</td>
    </tr>
    <tr>
      <td> <code> id </code> </td>
      <td> ご使用の {{site.data.keyword.objectstorageshort}} インスタンス ID。</td>
    </tr>
    <tr>
      <td> <code> region </code> </td>
      <td> ご使用のストレージ地域。資格情報にリストされているフィールドに一致する地域を必ず選択するようにしてください。</td>
    </tr>
    <tr>
      <td> <code> url </code> </td>
      <td> ご使用の {{site.data.keyword.objectstorageshort}} URL。</td>
    </tr>
    <tr>
      <td> <code> interface </code> </td>
      <td> 内部インターフェースには、{{site.data.keyword.Bluemix_notm}} からアクセスできません。パブリック・インターフェース (<code>publicURL</code>) を使用してください。</td>
    </tr>
  </table>
