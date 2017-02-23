---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-23"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Authenticating your {{site.data.keyword.objectstorageshort}} instance with Keystone

To interact with the service, you must authenticate your {{site.data.keyword.objectstorageshort}} instance with Keystone to obtain your URL and bearer token.
{: shortdesc}


Provisioning a new {{site.data.keyword.objectstorageshort}} instance creates an isolated Keystone project in the IBM Public Cloud. The Keystone credentials structure contains a complete set of attributes so that you can choose the OpenStack token request method or OpenStack SDK that best fits your app. When you bind a new app to the instance, a new Keystone user with access to the project is created. When you deprovision the instance, the project and user are deleted.

For more information about using OpenStack Swift and Keystone, view the <a href="http://docs.openstack.org" target="_blank">OpenStack documentation site. <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>



1. Make a POST request to `https://identity.open.softlayer.com/v3/auth/tokens` as shown in the following cURL command.
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

2. Select an `object-store` endpoint from the catalog response and take note. You need it to construct your full URL. The following response example is trimmed to show only information relevant to {{site.data.keyword.objectstorageshort}}.

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
  <caption> Table 1. Post request response explained </caption>
    <tr>
      <th> Response endpoint </th>
      <th> Explanation </th>
    </tr>
    <tr>
      <td> <code> X-Subject-Token </code> </td>
      <td> Your authentication token. </td>
    </tr>
    <tr>
      <td> <code> id </code> </td>
      <td> Your {{site.data.keyword.objectstorageshort}} instance ID. </td>
    </tr>
    <tr>
      <td> <code> region </code> </td>
      <td> Your storage region. Be sure to select the region that matches the field that is listed in your credentials. </td>
    </tr>
    <tr>
      <td> <code> url </code> </td>
      <td> Your {{site.data.keyword.objectstorageshort}} URL. </td>
    </tr>
    <tr>
      <td> <code> interface </code> </td>
      <td> The internal interface  is not accessible from {{site.data.keyword.Bluemix_notm}}. Use the public interface (<code>publicURL</code>). </td>
    </tr>
  </table>
