---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Protección de archivos {: #understanding-authentication}
*Última actualización: 19 de octubre de 2016*
{: .last-updated}

## OpenStack Identity (Keystone) v3 {: #keystone-authentication}

El suministro de una nueva instancia de {{site.data.keyword.objectstorageshort}} crea un proyecto Keystone aislado en la nube pública de IBM.
{: shortdesc}

La estructura de credenciales contiene un conjunto completo de atributos para permitirle seleccionar el método de solicitud de señales OpenStack o el SDK de OpenStack que se ajuste mejor a la aplicación. Cuando enlace una aplicación nueva en la instancia, se creará un nuevo usuario de Keystone con acceso al proyecto. Cuando desaprovisione la instancia, se suprimen el proyecto y el usuario.

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


## Descripción de las credenciales de servicio {: #understanding-credentials}

Las credenciales de servicio se utilizan para proporcionar autenticación y seguridad para el servicio. Se genera automáticamente un conjunto de credenciales cuando se proporciona una instancia. El cliente de Swift toma la información de autenticación de las variables de entorno de la tabla siguiente.

<table>
  <tr>
    <th> Variable de entorno</th>
    <th> Descripción</th>
  </tr>
  <tr>
    <td> `OS_USER_ID` </td>
    <td> El ID de usuario de {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> `OS_PASSWORD` </td>
    <td> La contraseña de la instancia de {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> `OS_PROJECT_ID` </td>
    <td> El ID del proyecto. </td>
  </tr>
  <tr>
    <td> `OS_REGION_NAME` </td>
    <td> La región en la que se almacenan los objetos. {{site.data.keyword.objectstorageshort}} está disponible en las regiones de Dallas y Londres.</td>
  </tr>
  <tr>
    <td> `OS_AUTH_URL` </td>
    <td> URL del punto final. Asegúrese de que `/v3` esté añadido al final del URL. </td>
  </tr>
</table>

*Tabla 1: Variables y descripciones de autenticación*

####  Adición de credenciales de servicio en la IU
1. En el separador **Credenciales de servicio** del panel de control de instancias del servicio, pulse **Nueva credencial** y dele un nombre.
2. (*Opcional*) En el campo de texto **Añadir parámetros de configuración en línea**, introduzca la información de credenciales del rol que desee crear. La información debe seguir el formato de las cargas útiles de JSON. Para obtener más información sobre los roles de usuario de {{site.data.keyword.objectstorageshort}}, consulte [Tipos de acceso](../os_security.html#access-types).
    - Para crear un usuario administrativo: `{"role":"admin"}`
    - Para crear un usuario no administrativo: `{"role":"member"}`
3. Pulse **Añadir**.


## Tipos de acceso {: #access-types}

El acceso al servicio se control mediante roles de usuario y listas de control de acceso al contenedor. Los usuarios de {{site.data.keyword.objectstorageshort}} pueden ser administrativos o no administrativos. Las listas de control de acceso son habilitadas por los usuarios administrativos a nivel de contenedor y no están disponibles para la instancia de servicio, cuenta de almacenamiento o nivel de proyecto.

<table>
  <tr>
    <th> Usuarios administrativos (admin) </th>
    <th> Usuarios no administrativos (miembro) </th>
  </tr>
  <tr>
    <td> Gestión del control de acceso </td>
    <td> De forma predeterminada, no tiene acceso al servicio o a sus contenedores </td>
  </tr>
  <tr>
    <td> Puede crear y suprimir contenedores </td>
    <td> Puede realizar acciones basándose en los ACL de lectura/escritura de los contenedores </td>
  </tr>
  <tr>
    <td> Puede leer y escribir en los contenedores </td>
    <td> Puede realizar acciones tal como las determina el administrador </td>
  </tr>
</table>

*Tabla 2: Roles de usuario definidos*

Puede gestionar usuarios de {{site.data.keyword.objectstorageshort}} a través de la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, la API de Cloud Foundry o la CLI de Cloud Foundry.




## Concesión de acceso de lectura{: #read-access}

Un usuario de {{site.data.keyword.objectstorageshort}} con rol de administrador puede conceder acceso de lectura a un contenedor para otro usuario y manipular las combinaciones de ACL de lectura.

<table>
  <tr>
    <th> Permiso </th>
    <th> Opciones de ACL de lectura </th>
  </tr>
  <tr>
    <td> Lectura para todos los usuarios a los que se hace referencia para la afiliación de cuentas </td>
    <td> `.r,*` </td>
  </tr>
  <tr>
    <td> Lectura y lista para todos los usuarios a los que se hace referencia y se incluyen en la lista </td>
    <td> `.r:*,.rlistings` </td>
  </tr>
  <tr>
    <td> Lectura y lista para un usuario especificado en un proyecto específico </td>
    <td> `< ID_proyecto>:< ID_usuario>` </td>
  </tr>
  <tr>
    <td> Lectura y lista para un usuario especificado en cada proyecto </td>
    <td> `<*>:< ID_usuario>` </td>
  </tr>
  <tr>
    <td> Lectura y lista para cada usuario de un proyecto especificado </td>
    <td> `< ID_proyecto>:<*>` </td>
  </tr>
  <tr>
    <td> Lectura y lista para cada usuario del proyecto  </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*Tabla 3: Permisos de acceso de lectura por opción*



1. Autenticar las credenciales. Puede utilizar las credenciales que se encuentran en el separador de credenciales de servicio de la IU o bien puede generar credenciales nuevas. Para obtener más información sobre la generación de nuevas credenciales, consulte [Generación de credenciales de servicio](insert link here). Recibirá el URL de {{site.data.keyword.objectstorageshort}} y la señal de autenticación como salida.
    Mandato Swift:
    
    ```
    export OS_USER_ID=<ID_usuario>
  export OS_PASSWORD=<contraseña>
  export OS_TENANT_ID=<ID_proyecto>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<región>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

    swift auth
    ```
    {: codeblock}
    
    Mandato cURL:
    
    ```
    curl -i -H "X-Auth-User: <ID_usuario>" -H "X-Auth-Key: <contraseña>" <url_autorización>
    ```
    {: pre}
    
2. Conceda acceso de lectura ejecutando el siguiente mandato:
    Mandato Swift:
    
    ```
    swift post <nombre_contenedor> --read-acl "<ID_usuario>:<ID_proyecto>"
    ```
    {: pre}
    
    Mandato cURL:
    
    ```
    curl -i <URL_ALMACENAMIENTO_SO> -X POST -H "Content-Length: 0" -H "X-Container-Read: <ID_inquilino>:<ID_poyecto>" -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"
    ```
    {: pre}
    **Nota**: Utilice una coma (,) para separar las listas de control de acceso.


3. Verifique el valor de ACL de lectura.
    Mandato Swift:
    
    ```
    swift stat <nombre_contenedor>
    ```
    {: pre}
    Mandato cURL:
    
    ```
    curl -i <URL_ALMACENAMIENTO_SO> -I -H "X-Auth-Token:<SEÑAL_AUTENTICACIÓN_SO>"
    ```
    {: pre}
    
    Puede ver en la siguiente salida de ejemplo que se ha concedido el acceso de lectura:
    
    ```
    HTTP/1.1 204 No Content
  Content-Length: 0
  X-Container-Object-Count: 1
  Accept-Ranges: bytes
  X-Storage-Policy: standard
  X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
  X-Container-Bytes-Used: 31512
  X-Timestamp: 1462818314.11220
  Content-Type: text/plain; charset=utf-8
  X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
  Date: Tue, 28 Jun 2016 20:57:58 GMT
    ```
    {: screen}



## Concesión de acceso de escritura{: #write-access}

Un usuario de {{site.data.keyword.objectstorageshort}} con un rol de administrador puede conceder acceso de escritura a un contenedor para otro usuario y manipular las combinaciones de ACL de escritura.

<table>
  <tr>
    <th> Permiso </th>
    <th> Opciones de ACL de escritura </th>
  </tr>
  <tr>
    <td> Escritura para un usuario especificado en un proyecto específico </td>
    <td> `<ID_proyecto>:< ID_usuario>` </td>
  </tr>
  <tr>
    <td> Escritura para un usuario especificado en cada proyecto </td>
    <td> `*:<ID_usuario>` </td>
  </tr>
  <tr>
    <td> Escritura para cada usuario de un proyecto específico </td>
    <td> `<ID_proyecto>:<*>` </td>
  </tr>
  <tr>
    <td> Escritura para cada usuario de cada proyecto </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*Tabla 4: Permisos de acceso de escritura por opción*




1. Autentique sus credenciales utilizando la información de las credenciales de servicio creadas. Recibirá el URL de {{site.data.keyword.objectstorageshort}} y la señal de autenticación como salida.
    Mandato Swift:
    
    ```
    export OS_USER_ID="<user_id>"
    export OS_PASSWORD="<password>"
    export OS_TENANT_ID=<project_id>
    export OS_AUTH_URL=https://identity.open.softlayer.com/v3
    export OS_REGION_NAME=<region>
    export OS_IDENTITY_API_VERSION=3
    export OS_AUTH_VERSION=3

    swift auth
    ```
    {: codeblock}
    
    Mandato cURL:
    
    ```
    curl -i -H "X-Auth-User:< ID_usuario>" -H "X-Auth-Key:< contraseña>" https://identity.open.softlayer.com/v3
    ```
    {: pre}
    
2. Conceda acceso de escritura ejecutando el siguiente mandato:
    Mandato Swift:
    
    ```
    swift post <nombre_contenedor> --write-acl "<ID_usuario>:<ID_proyecto>"
    ```
    {: pre}
    
    Mandato cURL:
    
    ```
    curl -i <URL_ALMACENAMIENTO_SO> -X POST -H "Content-Length: 0" -H "X-Container-Write: <ID_usuario>:<ID_poyecto>" -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"
    ```
    {: pre}
    
    **Nota**: Utilice una coma (,) para separar las listas de control de acceso.

3. Verifique el valor de ACL de escritura.
    Mandato Swift:
    
    ```
    swift stat <nombre_contenedor>
    ```
    {: pre}
    
    Mandato cURL:
    
    ```
    curl -i <URL_ALMACENAMIENTO_SO> -I -H "X-Auth-Token:<SEÑAL_AUTENTICACIÓN_SO>"
    ```
    {: pre}



## Eliminación de acceso {: #removing-access}

Para eliminar los ACL de lectura de un contenedor:
* Mandato Swift:

    ```
    swift post <nombre_contenedor> --read-acl “”
    ```
    {: pre}
    
*  Mandato cURL:

    ```
    curl -i <URL_ALMACENAMIENTO_SO> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"
    ```
    {: pre}

Para eliminar los ACL de escritura de un contenedor:

* Mandato Swift:

    ```
    swift post <nombre_contenedor> --write-acl “”
    ```
    {: pre}
    
*  Mandato cURL:

    ```
    curl -i <URL_ALMACENAMIENTO_SO> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"
    ```
    {: pre}

Para comprobar que se ha eliminado un ACL:

* Mandato Swift:

    ```
    swift stat <nombre_contenedor>
    ```
    {: pre}

  La siguiente salida de ejemplo muestra tanto el ACL de lectura como el ACL de escritura en blanco, lo que significa que se ha eliminado el acceso.
  
  ```
           Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8
  ```
  {: screen}

* Mandato cURL:
  ```
  curl -i <URL_ALMACENAMIENTO_SO> -I -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"
  ```
  {: pre}
