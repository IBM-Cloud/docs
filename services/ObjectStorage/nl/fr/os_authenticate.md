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


# Authentification de votre instance {{site.data.keyword.objectstorageshort}} avec Keystone

Pour interagir avec le service, vous devez authentifier votre instance {{site.data.keyword.objectstorageshort}} avec Keystone pour obtenir votre URL et le jeton bearer.
{: shortdesc}


La mise à disposition d'une nouvelle instance {{site.data.keyword.objectstorageshort}} crée un projet Keystone isolé dans le cloud public IBM. La
structure des données d'identification Keystone inclut un jeu complet d'attributs de sorte que vous pouvez choisir la méthode de demande de jeton
OpenStack ou bien le SDK OpenStack qui convient le mieux à votre application. Lorsque vous liez une nouvelle application à
l'instance, un nouvel utilisateur Keystone avec accès au projet est créé. Quand vous annulez la mise à disposition de l'instance, le projet et l'utilisateur sont supprimés.

Pour plus d'informations sur l'utilisation d'OpenStack Swift et de Keystone, voir le [site de documentation d'OpenStack](http://docs.openstack.org).

1. Soumettez une requête POST à `https://identity.open.softlayer.com/v3/auth/tokens` comme illustré dans la commande
cURL suivante.
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

2. Sélectionnez un noeud final `object-store` dans la réponse du catalogue et prenez-en note. Vous en aurez besoin pour construire votre URL complète. L'exemple
de réponse suivant a été élagué afin d'afficher uniquement les informations pertinentes sur {{site.data.keyword.objectstorageshort}}.

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
  	        "endpoints": [
			{
  	            "id" : "20cbfa6ff22b4a67a1484d30235bfc80",
  	            "region" : "londres",
  	            "region_id" : "londres",
  	            "url" : "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "admin"
  	          },
  	          {
  	            "id" : "38b8c081b11a452bb951698c334a406d",
  	            "region" : "londres",
  	            "region_id" : "londres",
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
  	            "region" : "londres",
  	            "region_id" : "londres",
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
  <caption> Tableau 1. Explication de la réponse à la requête Post</caption>
    <tr>
      <th> Noeud final de réponse </th>
      <th> Explication </th>
    </tr>
    <tr>
      <td> <code> X-Subject-Token </code> </td>
      <td> Votre jeton d'authentification. </td>
    </tr>
    <tr>
      <td> <code> id </code> </td>
      <td> ID de votre instance {{site.data.keyword.objectstorageshort}}. </td>
    </tr>
    <tr>
      <td> <code> region </code> </td>
      <td> Votre région de stockage. Prenez soin de sélectionner la région correspondant à la zone qui est répertoriée dans vos données d'identification. </td>
    </tr>
    <tr>
      <td> <code> url </code> </td>
      <td> Votre URL {{site.data.keyword.objectstorageshort}}. </td>
    </tr>
    <tr>
      <td> <code> interface </code> </td>
      <td> L'interface interne n'est pas accessible depuis {{site.data.keyword.Bluemix_notm}}. Utilisez l'interface publique (<code>publicURL</code>). </td>
    </tr>
  </table>
