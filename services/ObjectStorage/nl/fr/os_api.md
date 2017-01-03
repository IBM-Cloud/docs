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

# Utilisation de l'API Swift REST pour accéder à {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}


Vous pouvez vous servir de l'API Swift REST avec une interface client de ligne de commande, comme cURL, ou appeler l'API depuis votre application.
{: shortdesc}



## OpenStack Identity (Keystone) v3 {: #keystone-authentication}

La mise à disposition d'une nouvelle instance {{site.data.keyword.objectstorageshort}} crée un projet Keystone isolé dans le cloud public IBM.

La structure des données d'identification contient un ensemble complet d'attributs pour vous permettre de choisir la méthode de demande de jeton OpenStack ou le kit SDK OpenStack qui convient le mieux pour votre application. Quand vous liez une nouvelle application à l'instance, un nouvel utilisateur Keystone avec un accès au projet est créé. Quand vous annulez la mise à disposition de l'instance, le projet et l'utilisateur sont supprimés.

Pour plus d'informations sur l'utilisation d'OpenStack Swift et de Keystone, voir le [site de documentation d'OpenStack](http://docs.openstack.org).

La demande de jeton v3 recommandée est une demande POST vers https://identity.open.softlayer.com/v3/auth/tokens, comme illustré dans la commande curl suivante :
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

Utilisez la valeur de la zone `X-Subject-Token` depuis l'en-tête de réponse comme zone `X-Auth-Token` quand vous effectuez des demandes vers le service {{site.data.keyword.objectstorageshort}}.

Voici un exemple de réponse. La réponse est tronquée afin de n'afficher que les informations pertinentes pour
{{site.data.keyword.objectstorageshort}}.
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
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "38b8c081b11a452bb951698c334a406d",
	            "region" : "londres",
	            "region_id" : "londres",
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
	            "region" : "londres",
	            "region_id" : "londres",
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

L'adresse URL {{site.data.keyword.objectstorageshort}} se trouve dans le catalogue de service. Ce dernier est contenu dans le corps de réponse de la demande de jeton. La réponse est un catalogue complet des services OpenStack qui sont disponibles. Sélectionnez le noeud final depuis le catalogue de service avec le type `object-store` et la région qui correspond à la zone région des données d'identification.

**Remarque :** utilisez l'interface publique (`publicURL`). L'interface interne (`internalURL`)
n'est pas accessible depuis {{site.data.keyword.Bluemix_notm}}.






## Construction de votre URL {{site.data.keyword.objectstorageshort}} {: #access-points}

Pour interagir avec l'API {{site.data.keyword.objectstorageshort}}, construisez l'URL {{site.data.keyword.objectstorageshort}} comme suit :
  ```
  https://<point d'accès>/<version d'API>/AUTH_<ID projet>/<espace de nom de conteneur>/<object namespace>
  ```
  {: pre}

<table>
  <tr>
    <th> Eléments de l'URL  </th>
    <th> Définition </th>
  </tr>
  <tr>
    <td> Version de l'API  </td>
    <td> Version 1 : v1 </td>
  </tr>
  <tr>
    <td> Informations de compte  </td>
    <td> Il s'agit de l'ID du projet associé au préfixe. Vous le trouverez dans l'interface utilisateur. </td>
  </tr>
  <tr>
    <td> Espace de nom du conteneur  </td>
    <td> Nom de votre conteneur. Vous le trouverez dans l'interface utilisateur. </td>
  </tr>
  <tr>
    <td> Espace de nom d'objet  </td>
    <td> Nom de votre fichier ou objet. Vous le trouverez dans l'interface utilisateur. </td>
  </tr>
  <tr>
    <td> Point d'accès</td>
    <td> Londres : https://lon.objectstorage.open.softlayer.com/
    <br> Dallas : https://dal.objectstorage.open.softlayer.com/ </br> </td>
  </tr>
</table>

Tableau 1. Présentation des éléments composant l'URL {{site.data.keyword.objectstorageshort}}

Exemple :

![{{site.data.keyword.objectstorageshort}} Eléments de l'URL montrés dans une image exemple](images/Swift_URL.png)





## API {{site.data.keyword.objectstorageshort}} {: #openstack-reference}

Voir [Swift/API - OpenStack, dans le site openstack](http://developer.openstack.org/api-ref-objectstorage-v1.html) pour une liste complète des options d'API REST d'{{site.data.keyword.objectstorageshort}}.
