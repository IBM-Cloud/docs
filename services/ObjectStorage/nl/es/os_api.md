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

# Utilización de la API REST de Swift para acceder a {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}


Puede utilizar la API REST de Swift con una interfaz de clientes de línea de mandatos, como por ejemplo cURL, o invocar la API desde la aplicación.
{: shortdesc}



## OpenStack Identity (Keystone) v3 {: #keystone-authentication}

El suministro de una nueva instancia de {{site.data.keyword.objectstorageshort}} crea un proyecto Keystone aislado en la nube pública de IBM.

La estructura de credenciales contiene un conjunto completo de atributos para permitirle seleccionar el método de solicitud de señales OpenStack o el SDK de OpenStack que se ajuste mejor a la app. Cuando enlace una app nueva en la instancia, se creará un nuevo usuario de Keystone con acceso al proyecto. Cuando desaprovisione la instancia, se suprimen el proyecto y el usuario.

Para obtener más información sobre el uso de OpenStack Swift y Keystone, vea el [sitio de documentación de OpenStack](http://docs.openstack.org).

La solicitud de señal v3 recomendada es una solicitud POST a https://identity.open.softlayer.com/v3/auth/tokens, tal como se muestra en el siguiente mandato curl:
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

Utilice el valor del campo `X-Subject-Token` desde la cabecera de respuestas como el campo `X-Auth-Token` al realizar solicitudes en el servicio de {{site.data.keyword.objectstorageshort}}.

Una respuesta de ejemplo es como la siguiente. La respuesta se recorta para mostrar solo la información relevante de {{site.data.keyword.objectstorageshort}}.
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

El URL de {{site.data.keyword.objectstorageshort}} se encuentra en el catálogo de servicios. El catálogo de servicios está contenido en el cuerpo de respuesta de la solicitud de señal. La respuesta es un catálogo completo de servicios de OpenStack que están disponibles. Seleccione el punto final desde el catálogo de servicios con el tipo de `object-store` y la región que coincide con el campo región de las credenciales.

**Nota:** Utilice la interfaz pública (`publicURL`). No se puede acceder a la interfaz interna (`internalURL`) desde {{site.data.keyword.Bluemix_notm}}.






## Construcción del URL de {{site.data.keyword.objectstorageshort}} {: #access-points}

Para interactuar con la API de {{site.data.keyword.objectstorageshort}}, genere el URL de {{site.data.keyword.objectstorageshort}} tal como se indica a continuación:
  ```
  https://<punto de acceso>/<versión de la API>/AUTH_<ID de proyecto>/<espacio de nombres del contenedor>/<object namespace>
  ```
  {: pre}

<table>
  <tr>
    <th> Partes del URL  </th>
    <th> Definición </th>
  </tr>
  <tr>
    <td> Versión de API  </td>
    <td> Versión 1: v1 </td>
  </tr>
  <tr>
    <td> Información sobre la cuenta  </td>
    <td> Este es el ProjectID y el prefijo combinados. Se puede encontrar en la IU. </td>
  </tr>
  <tr>
    <td> Espacio de nombres del contenedor  </td>
    <td> El nombre del contenedor. Se puede encontrar en la IU. </td>
  </tr>
  <tr>
    <td> Espacio de nombres de objeto  </td>
    <td> El nombre de su archivo u objeto. Se puede encontrar en la IU. </td>
  </tr>
  <tr>
    <td> Punto de acceso</td>
    <td> Londres: https://lon.objectstorage.open.softlayer.com/
    <br> Dallas: https://dal.objectstorage.open.softlayer.com/ </br> </td>
  </tr>
</table>

Tabla 1. Partes del URL de {{site.data.keyword.objectstorageshort}} explicadas

Por ejemplo:

Partes del URL de ![{{site.data.keyword.objectstorageshort}} mostradas en una imagen de ejemplo](images/Swift_URL.png)





## API de {{site.data.keyword.objectstorageshort}} {: #openstack-reference}

Consulte la [Referencia completa de la API de OpenStack Swift](http://developer.openstack.org/api-ref-objectstorage-v1.html) para obtener una lista completa de las opciones y los ejemplos de la API REST de {{site.data.keyword.objectstorageshort}}.
