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

# Swift REST API を使用した {{site.data.keyword.objectstorageshort}} へのアクセス {: #using-swift-restapi}


コマンド・ライン・クライアント・インターフェース (cURL など) で Swift REST API を使用することも、アプリケーションから API を呼び出すこともできます。
{: shortdesc}



## OpenStack Identity (Keystone) v3 {: #keystone-authentication}

新しい {{site.data.keyword.objectstorageshort}} インスタンスをプロビジョンすると、IBM Public Cloud に独立した Keystone プロジェクトが作成されます。

アプリに最適な OpenStack トークン要求メソッドまたは OpenStack SDK を選択できるように、資格情報構成には全セットの属性が含まれています。インスタンスに新しいアプリをバインドすると、プロジェクトへのアクセス権限を持つ新しい Keystone ユーザーが作成されます。インスタンスをプロビジョン解除すると、プロジェクトとユーザーは削除されます。

OpenStack Swift および Keystone について詳しくは、[OpenStack 資料サイト](http://docs.openstack.org)を参照してください。

推奨される v3 トークン要求は、以下の curl コマンドに示されているように、https://identity.open.softlayer.com/v3/auth/tokens への POST 要求です。
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

応答ヘッダーの `X-Subject-Token` フィールドの値を、{{site.data.keyword.objectstorageshort}} サービスへの要求を行うときに `X-Auth-Token` フィールドとして使用します。


応答の例を以下に示します。この応答は、{{site.data.keyword.objectstorageshort}} 関連の情報のみを示すために切り取られています。
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

{{site.data.keyword.objectstorageshort}} URL は、サービス・カタログ内にあります。サービス・カタログは、トークン要求の応答本体に含まれています。応答は、使用可能な OpenStack サービスの完全なカタログです。サービス・カタログから、タイプが `object-store` で、地域が、資格情報の地域フィールドに一致しているエンドポイントを選択します。

**注:** パブリック・インターフェース (`publicURL`) を使用してください。内部インターフェース (`internalURL`) は、{{site.data.keyword.Bluemix_notm}} からアクセスできません。






## {{site.data.keyword.objectstorageshort}} URL の構成 {: #access-points}

{{site.data.keyword.objectstorageshort}} API と相互作用するには、 {{site.data.keyword.objectstorageshort}} URL を次のように構成します。
  ```
https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>
  ```
  {: pre}

<table>
  <tr>
    <th> URL の構成要素  </th>
    <th> 定義 </th>
  </tr>
  <tr>
    <td> API のバージョン  </td>
    <td> バージョン 1: v1 </td>
  </tr>
  <tr>
    <td> アカウント情報  </td>
    <td> これは、お客様の ProjectID と接頭部の組み合わせです。これは、UI で確認できます。</td>
  </tr>
  <tr>
    <td> コンテナー名前空間  </td>
    <td> コンテナーの名前。これは、UI で確認できます。</td>
  </tr>
  <tr>
    <td> オブジェクト名前空間  </td>
    <td> ファイルまたはオブジェクトの名前。これは、UI で確認できます。</td>
  </tr>
  <tr>
    <td> アクセス・ポイント</td>
    <td> ロンドン: https://lon.objectstorage.open.softlayer.com/
    <br> ダラス: https://dal.objectstorage.open.softlayer.com/ </br> </td>
  </tr>
</table>

表 1. {{site.data.keyword.objectstorageshort}} URL 構成要素の説明

例:

![{{site.data.keyword.objectstorageshort}} URL の構成要素が例のイメージで示されています](images/Swift_URL.png)





## {{site.data.keyword.objectstorageshort}} API {: #openstack-reference}

{{site.data.keyword.objectstorageshort}} REST API のオプションと例の包括的な一覧については、[OpenStack Swift API の詳細リファレンス](http://developer.openstack.org/api-ref-objectstorage-v1.html)を参照してください。
