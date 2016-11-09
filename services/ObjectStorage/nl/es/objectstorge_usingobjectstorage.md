---

copyright:
  years: 2014, 2016

---

{:new_window: target="_blank"}

# Empiece a utilizar {{site.data.keyword.objectstorageshort}}  {: #using-object-storage}

*Última actualización: 13 de agosto de 2016*
{: .last-updated}


## Utilización de la interfaz de usuario de {{site.data.keyword.objectstorageshort}} {: #using-object-storage-ui}

### Navegación y elementos de IU
Cuando se suministra {{site.data.keyword.objectstorageshort}}, puede ver la información de instancia en el panel de control de instancia de servicio de {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}}. Desde el panel de control, seleccione la instancia de {{site.data.keyword.objectstorageshort}} para visualizar el panel con información más detallada.  
#### Datos de uso
En la página principal de la aplicación, visualizará la información de uso de almacenamiento para su instancia. También muestra el número actual de **Contenedores de almacenamiento** y el número total de **Objetos** en todos los contenedores. Lista el uso de memoria en megabytes. **Almacenamiento consumido** se refiere a la cantidad actual de espacio que se utiliza.
#### Acciones
Para recuperar los datos de uso más recientes, pulse el botón **Renovar**.   
####Navegador de objetos
Utilice este navegador para gestionar los objetos y contenedores de almacenamiento de objetos. Puede crear contenedores, cargar archivos, suprimir contenedores y suprimir archivos, entre otras acciones.


## Utilización de {{site.data.keyword.objectstorageshort}} desde una app de {{site.data.keyword.Bluemix_notm}} {: #using-object-storage-from-bluemix-app}

### Cómo enlazar el servicio de {{site.data.keyword.objectstorageshort}} a una aplicación después de la creación {: #bind-object-storage-to-application}
1.	En el panel de control de {{site.data.keyword.Bluemix_notm}}, seleccione la app que desee enlazar.
2.	En la visión general de la app, pulse **Enlazar un servicio o API**.
3.	Seleccione la instancia de {{site.data.keyword.objectstorageshort}} desde la lista de servicios y pulse **Añadir**.
4.	Haga clic en **Volver a transferir** cuando se le solicite. Es necesario volver a transferir su app para utilizar el nuevo servicio.

### Contexto enlazado

Si desea utilizar {{site.data.keyword.objectstorageshort}} en un contexto enlazado, las credenciales de la nube se proporcionan de forma indirecta a través del proceso de enlace de la aplicación. Después de enlazar correctamente una instancia de servicio a la aplicación, se añade una configuración similar al ejemplo siguiente en la variable de entorno `VCAP_SERVICES`.

```
{
"Object-Storage": [
{
  "name": "Object-Storage - YP",
      "label": "Object-Storage",
      "plan": "Free",
      "credentials": {
     "auth_url": "https://identity.open.softlayer.com",
         "project": "object_storage_d049255b",
         "projectId": "0f47b41b06d047f9aae3b33f1db061ed",
         "region": "dallas",
         "userId": "ad78b2a3f843466988afd077731c61fc",
         "username": "user_202db1f8a7aa3f3ac51ec68f10dbe7dc29070bc7",
         "password": "K/jyIi2jR=1?D.TP",
         "domainId": "2df6373c549e49f8973fb6d22ab18c1a",
         "domainName": "639347"
        }
   }
  ]
}
```

## Utilización de Swift CLI para acceder a {{site.data.keyword.objectstorageshort}} {: #using-swift-cli}

Puede acceder al servicio de {{site.data.keyword.objectstorageshort}} mediante Internet y desde las aplicaciones y los servidores virtuales del IBM {{site.data.keyword.Bluemix_notm}}. Los casos de uso comunes para el servicio de {{site.data.keyword.objectstorageshort}} son los siguientes:

* Copia de seguridad de datos de volumen desde las instancias
* Utilización de una ubicación intermediaria al transferir grandes cantidades de datos
* Transferencia de datos entre entornos que no están conectados directamente
* Función de repositorio central

El servicio de {{site.data.keyword.objectstorageshort}} se basa en OpenStack Swift y se puede acceder a él mediante cualquier aplicación cliente compatible. Esta sección describe cómo utilizar el cliente de Python Swift, que es la interfaz de línea de mandatos (CLI) para la API de {{site.data.keyword.objectstorageshort}} y sus extensiones, para que funcione con los contenedores y los archivos.

### Instalación del cliente Swift {: #install-swift-client}

Instale el software de requisito previo siguiente si aún no está instalado. Para obtener más información, consulte la [Documentación de OpenStack](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}.
* Python 2.7 o posterior
* Paquete setuptools
* Paquete pip

Instale el cliente de Python Swift utilizando Python pip:

```
	sudo pip install python-swiftclient
```

Instale el cliente Python Keystone ejecutando el siguiente mandato:

```
	sudo pip install python-keystoneclient
```

### Configuración del cliente {: #setup-swift-client}

El cliente de Swift toma la información de autenticación de las siguientes variables de entorno:
* `OS_AUTH_URL` es el URL de punto final
* `OS_USER_ID` es el nombre de usuario
* `OS_PASSWORD` es la contraseña

Establezca la información de autenticación como se indica a continuación:

```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
export OS_PASSWORD=aaa55AAAaaaaa]?,
export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
export OS_AUTH_URL=https://identity.open.softlayer.com/v3
export OS_REGION_NAME=dallas
export OS_IDENTITY_API_VERSION=3
export OS_AUTH_VERSION=3
```

Puede encontrar los valores de credenciales para el servicio de {{site.data.keyword.objectstorageshort}} en la página **Credenciales de servicio** de la interfaz de usuario de {{site.data.keyword.objectstorageshort}}.

**Nota:** Asegúrese de añadir un `/v3` al `auth_url` desde las credenciales de la interfaz de usuario de {{site.data.keyword.objectstorageshort}} al configurar las variables de entorno `OS_AUTH_URL` para el cliente de Swift.


### Trabajar con contenedores {: #work-with-containers}

Lista de contenedores:
```
	swift list
```
Creación de un contenedor:
```
	swift post <nombre_contenedor>
```
Listar el contenido de un contenedor:
```
	swift list <nombre_contenedor>
```
### Trabajo con objetos {: #work-with-objects}

#### Cómo añadir un archivo a un contenedor
```
	swift upload <nombre_contenedor> <nombre_archivo>
```
#### Cómo añadir archivos mayores de 5 GB en un contenedor

Si está cargando un archivo mayor de 5 GB, debe dividirlo en fragmentos más pequeños. Puede dar instrucciones al cliente de Swift para que maneje tal subida facilitando el parámetro `-segment-size`:
```
	swift upload <nombre_contenedor> <nombre_archivo> --segment-size <tamaño_en_bytes>
```
Cada segmento se carga en paralelo en un contenedor separado llamado `<nombre_contenedor>_segmentos`. Una vez que se hayan cargado todos los segmentos, Swift creará un archivo manifest para que los segmentos se puedan descargar en un único archivo desde el contenedor original `<nombre_contenedor>` con el nombre de archivo original `<nombre_archivo>`.

Por ejemplo, el mandato siguiente carga un archivo denominado `archivo_grande` de un contenedor llamado `contenedor_prueba` con un tamaño de archivo de `1073741824`.
```
	swift upload test_container -S 1073741824 large_file
```
Puede ejecutar el siguiente mandato para descargar el archivo:
```
	swift download test_container large_file
```
#### Descarga de un archivo
```
	swift download <nombre_contenedor> <nombre_contenedor>
```
#### Cómo añadir un directorio a un contenedor

Swift no tiene una auténtica estructura de directorios, sino que utiliza la denominación para representar un diseño de directorios. Para añadir un directorio a un contenedor, ejecute el mandato siguiente:
```
	swift upload <nombre_contenedor> <nombre_directorio>
```
Este mandato cargará la estructura de directorios completa como una vía de acceso relativa. Por ejemplo, si especifica `/mnt/volume1`, la estructura de directorios mnt/volume1 se añadirá a todos los nombres de archivos para indicar la estructura de directorios.


#### Descarga de un directorio

Para descargar una estructura de directorios, utilice el parámetro `-prefix` para indicar el directorio o la estructura de directorios que desea descargar.
```
	swift download <nombre_contenedor> --prefix <directorio>
```
#### Supresión de un archivo
```
	swift delete <nombre_contenedor> <nombre_archivo>
```
### Trabajo con mantenimiento de versiones de objetos {: #work-with-object-versioning}

Puede configurar versiones de cada objeto del contenedor mediante el distintivo `X-Versions-Location`. Para ello, cree un contenedor adicional para conservar versiones más antiguas de los objetos como se indica a continuación.

Si está utilizando el cliente swift, puede configurarlo de la forma siguiente:
```
	swift post container_one -H "X-Versions-Location:container_two"
```
Si está utilizando curl, puede configurarlo de la forma siguiente:
```
	curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:container_two" https://<object-storage_url>/container_one
```
En el ejemplo, `container_two` se ha configurado para incluir las versiones anteriores de los objetos almacenados en `container_one`. Por lo tanto, `container_one` tendrá la versión más actualizada de los objetos, y `container_two` tendrá las versiones más antiguas de los objetos. Asegúrese de que exista `container_two` para que el control de versiones funcione.

Con el control de versiones configurado, al cargar un objeto en `container_one`, si ya existe una versión del objeto, la versión existente se mueve a `container_two` mientras la nueva versión se crea en `container_one`. Si suprime un objeto de `container_one`, la versión anterior del objeto se vuelve a mover de `container_two` a `container_one`.

Los objetos de `container_two` se nombrarán automáticamente con el siguiente formato: `<Length><Object_name>/<Timestamp>`.

`Length` hace referencia a la longitud del nombre del objeto; hay un número hexadecimal de 3 caracteres del teclado numeral. `Object_name` es el nombre del objeto. `Timestamp` es la indicación de fecha y hora de cuándo se cargó originalmente esta versión concreta del objeto.

Para inhabilitar el control de versiones, utilice el distintivo `X-Remove-Versions-Location`:
```
	swift post container_one -H "X-Remove-Versions-Location:"
```
o
```
	cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/container_one
```
A continuación hay un ejemplo completo del uso del control de versiones:

1. Crear un contenedor:
```
		$ swift post container_one
		$
```
2. Configurar el control de versiones para container_one:
```
		$ swift post container_one -H "X-Versions-Location:container_two"
		$
```
3. Crear container_two:
```
		$ swift post container_two
		$
```
4. Cargar un objeto por primera vez en container_one:
```
		$ swift upload container_one object
		object
		$
```
5. Listar objetos en container_one:
```
		$ swift list container_one
		object
		$
```
6. Listar objetos en container_two:
```
		$ swift list container_two
		$
```
7. Cargar una versión nueva del objeto en container_one:
```
		$ swift upload container_one object
		object
		$
```
8. Listar objetos en container_one:
```
		$ swift list container_one
		object
		$
```
9. Listar objetos en container_two:
```
		$ swift list container_two
		006object/1457456909.27383
		$
```
10. Suprimir objetos en container_one:
```
		$ swift delete container_one object
		object
		$
```
11. Listar ambos contenedores:
```
		$ swift list container_one
		object
		$ swift list container_two
		$
```

### Planificación de la supresión de objetos {: #schedule-object-deletion}

Puede configurar los objetos para que caduquen en una determinada cantidad de tiempo. En otras palabras, puede planificar la supresión de los objetos. Puede hacer esto haciendo uso de las cabeceras `X-Delete-At` o `X-Delete-After`. La cabecera `X-Delete-At` toma un número entero que representa el tiempo Epoch en el que se suprime el objeto. La cabecera `X-Delete_After` toma un número entero que representa el número de segundos tras los que se suprimirá el objeto.

Si está utilizando el cliente swift para realizar una publicación en el objeto del contenedor, consulte los ejemplos siguientes.

* Para establecer el objeto que se suprimirá en "2016/04/01 08:00:00", utilice el mandato siguiente:
```
		swift post -H "X-Delete-At:1459515600" container object
```
* Para establecer el objeto que se suprimirá en una hora desde este momento, utilice el mandato siguiente:
```
		swift post -H "X-Delete-After:3600" container object
```
  Tras hacer esto, el mandato `swift stat container object` mostrará la cabecera `X-Delete-At` con la caducidad adecuada en el tiempo Epoch.

* Para eliminar la hora de caducidad del objeto, utilice el mandato siguiente:
```
		swift post -H "X-Remove-Delete-After:" container object
```
Si está utilizando cURL, los mandatos serán los siguientes.

* Para establecer el objeto que se suprimirá en "2016/04/01 08:00:00", utilice el mandato siguiente:
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:1459515600" https://<object-storage_url>/container/object
```
* Para establecer el objeto que se suprimirá en una hora desde este momento, utilice el mandato siguiente:
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:3600" https://<object-storage_url>/container/object
```
* Para comprobar si el objeto tiene la cabecera, utilice el mandato siguiente:
```
		cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/container/object
```
* Para eliminar la hora de caducidad, utilice el mandato siguiente:
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:" https://<object-storage_url>/container/object
```
**Nota:** La supresión real de un objeto puede que no se produzca a la hora exacta indicada. Sin embargo, el objeto caducará de hecho a la hora especificada, lo que significa que ya no se podrá acceder a él. La supresión real tendrá lugar la próxima vez que se ejecute el daemon swift-object-expirer configurado en el clúster swift.





### Creación de un URL temporal {: #create-temporary-url}

Un URL temporal es un URL largo y difícil de adivinar que se puede utilizar para un periodo específico para descargar objetos sin que requieran una mayor autenticación. Genere un URL temporal con los pasos siguientes:

1. Identifique la cuenta de autenticación.
2. Establezca una clave secreta.
3. Cree el URL temporal.

#### Identificación de la cuenta de autenticación

El mandato `stat` de Swift imprime información sobre la cuenta:
```
	swift stat
```
Localice el campo Account y anote toda la cadena de texto que aparece tras *Account*: incluido `AUTH_`.

#### Configuración de una clave secreta

Esta clave puede ser cualquiera que seleccione, pero la práctica recomendada es que seleccione una serie larga, aleatoria y difícil de adivinar.
```
	swift post -m "Temp-URL-Key:<key>"
```
Ejecute el mandato `stat` de Swift para verificar que la `Temp-URL-Key` se haya configurado correctamente.
```
	swift stat
```

#### Creación de un URL temporal

El mandato `tempurl` de Swift toma estos argumentos de posición:

* [method] GET para permitir la descarga. PUT para permitir la carga.
* [seconds] Tiempo en segundos durante los que el URL estará disponible.
* [path] Vía de acceso completa del objeto expresada como `/v1/<cuenta_autorización>/<nombre_contenedor>/<nombre_objeto>`. Para obtener más información, consulte el [URL de {{site.data.keyword.objectstorageshort}}](#access-points).
* [key] Clave que se establece en el paso 2.

```
swift tempurl GET <segundos> <vía_acceso> <clave>
```

Este mandato devolverá un URL que se puede adjuntar al nombre de clúster para obtener un URL completo. Utilice el URL completo para descargar el objeto con cualquier cliente de HTTP compatible como por ejemplo curl, wget o Firefox.

## Utilización de la API REST de Swift para acceder a {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}

Puede utilizar la API REST de Swift con una interfaz de clientes de línea de mandatos, como por ejemplo cURL, o invocar la API desde la aplicación.  

### URL de {{site.data.keyword.objectstorageshort}} {: #access-points}

Para interactuar con la API de {{site.data.keyword.objectstorageshort}}, genere el URL de {{site.data.keyword.objectstorageshort}} tal como se indica a continuación:
```
	https://<punto de acceso>/<versión de la API>/AUTH_<ID de proyecto>/<espacio de nombres del contenedor>/<object namespace>
```


El URL consta de cinco partes. La `<versión de la API>` es la v1. Puede encontrar el `<ID de proyecto>`, el `<espacio de nombres del contenedor>` y el `<object namespace>` de {{site.data.keyword.objectstorageshort}} en la interfaz de usuario de {{site.data.keyword.objectstorageshort}}.  Para el `<punto de acceso>`, consulte la tabla siguiente:


| **Región**  |   **Punto de acceso público**                     |
|-------------|-----------------------------------------------|
| Dallas      | https://dal.objectstorage.open.softlayer.com/ |
| Londres      | https://lon.objectstorage.open.softlayer.com/ |


*Tabla 1. Punto de acceso de {{site.data.keyword.objectstorageshort}}*


### API de {{site.data.keyword.objectstorageshort}}

Consulte la [Referencia completa de la API de OpenStack Swift](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window} para obtener una lista completa de las opciones y los ejemplos de la API REST de {{site.data.keyword.objectstorageshort}}.

## Utilización de {{site.data.keyword.objectstorageshort}} entre varias regiones {: #multi-regions}  

El servicio de IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} da soporte a las regiones de almacenamiento Dallas y Londres. Estas regiones de almacenamiento son independientes de la región {{site.data.keyword.Bluemix_notm}}, como por ejemplo EE.UU.-Sur y Reino Unido, en la que se crea la instancia de servicio de {{site.data.keyword.objectstorageshort}}.  Por ejemplo, si crea una instancia de {{site.data.keyword.objectstorageshort}} en la región {{site.data.keyword.Bluemix_notm}} EE.UU.-Sur, puede leer y grabar datos a cualquier región de almacenamiento Dallas o Londres.  

Para la región {{site.data.keyword.Bluemix_notm}} EE.UU.-Sur, la región de almacenamiento Dallas es el valor predeterminado. Para la región {{site.data.keyword.Bluemix_notm}} Reino Unido, la región de almacenamiento Londres es el valor predeterminado.  La interfaz de usuario de {{site.data.keyword.objectstorageshort}} siempre se lanza en la región de almacenamiento predeterminada de la región {{site.data.keyword.Bluemix_notm}}. Para conmutar regiones, pulse la lista desplegable de Región de {{site.data.keyword.objectstorageshort}} y seleccione otra región.

**Nota:** El servicio de {{site.data.keyword.objectstorageshort}} NO da soporte a la réplica de la región de almacenamiento cruzada.

### Acceso de varias regiones

Para utilizar el servicio de {{site.data.keyword.objectstorageshort}}, debe [autenticarse con OpenStack Keystone](#keystone-authentication). Una vez que se haya autenticado correctamente, estarán disponibles en la respuesta `X-Subject-Token` y los puntos finales de {{site.data.keyword.objectstorageshort}}.

Por ejemplo, para crear un contenedor denominado `my_container` en la región de almacenamiento Dallas, especifique un punto de acceso Dallas en el mandato curl como se indica a continuación:
```
	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```

Para crear un contenedor denominado `my_container` en la región de almacenamiento Londres, especifique un punto de acceso Londres en el mandato curl como se indica a continuación:
```
	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```
**Nota:** `X-Subject-Token` que ha adquirido desde Keystone funciona en regiones de almacenamiento.

Para obtener más información sobre los puntos de acceso para distintas regiones, consulte la tabla [Punto de acceso de Object Storage](#access-points).


## Descripción de la autenticación y las credenciales {: #understanding-authentication-credentials}

### Generación de credenciales de {{site.data.keyword.objectstorageshort}} sin enlazar una aplicación

Para generar credenciales de nube de {{site.data.keyword.objectstorageshort}} para utilizarlas fuera de una aplicación de {{site.data.keyword.Bluemix_notm}}, debe generar una clave de servicio para la instancia de {{site.data.keyword.objectstorageshort}}. Puede generar una clave nueva mediante la selección de las **Credenciales de servicio** desde la barra lateral de la interfaz de usuario o utilizando la CLI de Cloud Foundry (versión 6.11.3 o posterior). Después de generar y recuperar una clave de servicio para la instancia de {{site.data.keyword.objectstorageshort}}, puede utilizar la información de integración de nube para solicitar una señal de Keystone utilizando un SDK de OpenStack o la API de OpenStack Identity y empezar a utilizar la cuenta de Swift para gestionar objetos.

Para crear la clave utilizando la CLI de Cloud Foundry, inicie sesión y ejecute el mandato siguiente:
 ```
    cf create-service-key <nombre_instancia_almacenamiento_objetos> <nombre_exclusivo_para_esta_clave>
```
Para recuperar las credenciales de servicio desde la CLI de Cloud Foundry, ejecute el mandato siguiente:
```
	cf service-key <nombre_instancia_almacenamiento_objeto> <nombre_exclusivo_para_esta_clave>
```

### Usuarios y proyectos de nube
El suministro de una nueva instancia de {{site.data.keyword.objectstorageshort}} crea un proyecto Keystone aislado en la nube pública de IBM. Cuando enlace una aplicación nueva en la instancia de {{site.data.keyword.objectstorageshort}}, se creará un nuevo usuario de Keystone con acceso al proyecto. Cuando desaprovisione la instancia, se suprimen el proyecto y el usuario.

### OpenStack Identity (Keystone) v3 {: #keystone-authentication}
La estructura de credenciales contiene un conjunto completo de atributos para permitirle seleccionar el método de solicitud de señales OpenStack o el SDK de OpenStack que se ajuste mejor a la aplicación.

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
						"password": "K/jyIi2jR=1?D.TP"
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
Utilice el valor del campo `X-Subject-Token` desde la cabecera de respuestas como el campo `X-Auth-Token` al realizar solicitudes en el servicio de {{site.data.keyword.objectstorageshort}}.

Una respuesta de ejemplo es como la siguiente. La respuesta se recorta para mostrar solo la información relevante de {{site.data.keyword.objectstorageshort}}.

	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json
```
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

El URL de {{site.data.keyword.objectstorageshort}} se encuentra en el Catálogo de servicios. El Catálogo de servicios está contenido en el cuerpo de respuesta de la solicitud de señal. La respuesta es un catálogo completo de servicios de OpenStack que están disponibles. Seleccione el punto final desde el Catálogo de servicios con el tipo de `object-store` y la región que coincide con el campo región de las credenciales.

**Nota:** Utilice la interfaz pública (`publicURL`). No se puede acceder a la interfaz interna (`internalURL`) desde {{site.data.keyword.Bluemix_notm}}.



## Protección de archivos con control de acceso preciso {: #fine-grained-access-control}

Las listas de control de acceso preciso ayudan a proteger los archivos cuando más de un usuario almacena archivos en el mismo contenedor.

Nota: los procedimientos destacados en este documento requieren la CLI de Swift. Para obtener más información, consulte [uso de {{site.data.keyword.objectstorageshort}} con la CLI de Swift](https://console.ng.bluemix.net/docs/services/ObjectStorage/objectstorge_usingobjectstorage.html#using-swift-cli).


### Tipos de acceso {: #access-types}

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

*Tabla 1: Roles de usuario definidos*

Puede gestionar usuarios de {{site.data.keyword.objectstorageshort}} a través de la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, la API de Cloud Foundry o la CLI de Cloud Foundry.



### Generación de credenciales de servicio de {{site.data.keyword.objectstorageshort}} {: #generating}

Desde la nueva consola de {{site.data.keyword.Bluemix_notm}}, puede generar nuevas credenciales de servicio para los usuarios de {{site.data.keyword.objectstorageshort}}.  Para ver la nueva consola, haga clic en **Try the new {{site.data.keyword.Bluemix_notm}}**.

1.  Inicie sesión en {{site.data.keyword.Bluemix_notm}} como usuario con rol de desarrollador. Debe encontrarse en el espacio de la instancia de servicio que desee gestionar.
2. Pulse el separador **Credenciales de servicio**.
3. Pulse **Nueva credencial**.
4. Asigne un nombre a la credencial.
5. En el campo de texto **Añadir parámetros de configuración en línea**, introduzca la información de credencial del rol que desee crear. La información debe seguir el formato de las cargas útiles de JSON.
  - Para crear un usuario administrativo: `{"role":"admin"}`
  - Para crear un usuario no administrativo: `{"role":"member"}`
5. Pulse **Añadir**.

Para generar credenciales de servicio utilizando mandatos cURL o la CLI de Swift, siga estos pasos.

1. Inicie sesión en {{site.data.keyword.Bluemix_notm}} como usuario con rol de desarrollador. Debe encontrarse en el espacio de la instancia de servicio que desee gestionar.

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```

2. Generar credenciales de servicio. `service-key-name` será el nombre de su credencial. Puede utilizar el mandato Cloud Foundry o el mandato cURL.

  Mandato Cloud Foundry:
  ```
  cf create-service-key "<nombre_instancia_servicio_almacenamiento_objetos>" <service-key-name> -c '{"role":"<rol_almacenamiento_objetos>"}'
  ```

  Ejemplo:

  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'

  ```
  Mandato cURL:
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "guid_instancia_servicio": "<guid_instancia_servicio>",   "name": "<nombre_usuario>", "role": "member"}' -X POST -H "Authorization: <señal_portador>" -H "Content-Type: " -H "Cookie: "
  ```

3. Valide las credenciales de la clave de servicio creada.

  Mandato Cloud Foundry:
  ```
  cf service-key <nombre_clave_servicio> <nombre_miembro>
  ```
  Ejemplo:
  Creación de una clave de servicio de miembro para una instancia de servicio llamada Object-Storage-Acl-Test.
  ```
  {
    "auth_url": "https://identity.open.softlayer.com",
    "domainId": "8753ff40ac1a4f4a9f162ad8026b6ce0",
    "domainName": "757955",
    "password": "xxxxxxxx",
    "project": "object_storage_6046b6e2_ee53_4884_916f_89c65e4d408e",
    "projectId": "c727d7e248b448f6b268f31a1bd8691e",
    "region": "dallas",
    "role": "member",
    "userId": "3c5b516655e4479881d3d216895faedb",
    "username": "member_2afbeea1d58b1867f46c699553d1e4513e7df83a"
  }
  ```
  Mandato cURL:
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <señal_bearer>" -H "Cookie: "
  ```



### Asignación de acceso {: #assigning-access}  

Solo un usuario de {{site.data.keyword.objectstorageshort}} con rol de administrador puede conceder acceso de lectura o escritura a un contenedor para otro uso.

Para conceder acceso de lectura en la CLI utilice la opción `--read-acl` o `-r`.

1. Autentique sus credenciales utilizando la información de las credenciales de servicio creadas.  Recibirá el URL de almacenamiento de objetos y la señal de autenticación como salida.

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
  Mandato cURL:
  ```
  curl -i -H "X-Auth-User: <ID_usuario>" -H "X-Auth-Key: <contraseña>" <url_autorización>
  ```
3. Conceda acceso de lectura ejecutando el siguiente mandato:

  Mandato Swift:
  ```
  swift post <nombre_contenedor> --read-acl "<ID_usuario>:<ID_proyecto>"
  ```
  Mandato cURL:
  ```
  curl -i <URL_ALMACENAMIENTO_SO> -X POST -H "Content-Length: 0" -H "X-Container-Read: <ID_inquilino>:<ID_poyecto>" -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"
  ```
4. Verifique el valor de ACL de lectura.

  Mandato Swift:
  ```
  swift stat <nombre_contenedor>
  ```
  Mandato cURL:
  ```
  curl -i <URL_ALMACENAMIENTO_SO> -I -H "X-Auth-Token:<SEÑAL_AUTENTICACIÓN_SO>"
  ```
  Resultado de ejemplo:
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

Es posible manipular las combinaciones de ACL de lectura.

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

*Tabla 2: Permisos de acceso de lectura por opción*

Nota: utilice una coma (,) para separar las listas de control de acceso. Por ejemplo, `-read-acl project id:usuario_id1, project_id2:usuario_id2`.


Para conceder acceso de escritura, utilice la opción `--write-acl` o `-w` a través de la CLI de Swift.

1. Autentique sus credenciales utilizando la información de las credenciales de servicio creadas.  Recibirá el URL de almacenamiento de objetos y la señal de autenticación como salida.

  Mandato Swift:
  ```
  export OS_USER_ID="<ID_usuario>"
  export OS_PASSWORD="<contraseña>"
  export OS_TENANT_ID=<ID_inquilino>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<región>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
  Mandato cURL:
  ```
  curl -i -H "X-Auth-User:< ID_usuario>" -H "X-Auth-Key:< contraseña>" https://identity.open.softlayer.com/v3
  ```
2. Conceda acceso de escritura ejecutando el siguiente mandato:

  Mandato Swift:
  ```
  swift post <nombre_contenedor> --write-acl "<ID_usuario>:<ID_proyecto>"
  ```
  Mandato cURL:
  ```
  curl -i <URL_ALMACENAMIENTO_SO> -X POST -H "Content-Length: 0" -H "X-Container-Write: <ID_usuario>:<ID_poyecto>" -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"

  ```
3. Verifique el valor de ACL de escritura.

  Mandato Swift:
  ```
  swift stat <nombre_contenedor>
  ```
  Mandato cURL:
  ```
  curl -i <URL_ALMACENAMIENTO_SO> -I -H "X-Auth-Token:<SEÑAL_AUTENTICACIÓN_SO>"
  ```


Es posible manipular las combinaciones de ACL de escritura.

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

*Tabla 3: Permisos de acceso de escritura por opción*

Nota: utilice una coma (,) para separar las listas de control de acceso. Por ejemplo, `-write-acl project id:usuario_id1, project_id2:usuario_id2`.




### Eliminación de acceso {: #removing-access}

Para eliminar los ACL de lectura de un contenedor:

  Mandato Swift:
  ```
  swift post <nombre_contenedor> --read-acl “”
  ```
  Mandato cURL:
  ```
  curl -i <URL_ALMACENAMIENTO_SO> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"
  ```

Para eliminar los ACL de escritura de un contenedor:

  Mandato Swift:
  ```
  swift post <nombre_contenedor> --write-acl “”
  ```
  Mandato cURL:
  ```
  curl -i <URL_ALMACENAMIENTO_SO> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"
  ```

Para comprobar que se ha eliminado un ACL:

  Mandato Swift:
  ```
  swift stat <nombre_contenedor>
  ```

  Resultado de ejemplo:
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
  Mandato cURL:
  ```
  curl -i <URL_ALMACENAMIENTO_SO> -I -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"
  ```




## Desenlazar y desaprovisionar {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

### Cómo desaprovisionar su servicio de {{site.data.keyword.objectstorageshort}}
1.	Seleccione el servicio del panel de control de {{site.data.keyword.Bluemix_notm}}.  
2.	Pulse el icono de engranaje y seleccione **Suprimir servicio**.

**Atención:** si desaprovisiona un IBM {{site.data.keyword.objectstorageshort}} para la instancia de servicio de {{site.data.keyword.Bluemix_notm}}, se suprimirán el proyecto de nube y la cuenta de Swift. Todos los contenedores y objetos de la instancia desaprovisionada se suprimirán de Swift y no se podrán restaurar.

### Desenlace de una aplicación o supresión de una clave de servicio

Si desenlaza una aplicación de la instancia de {{site.data.keyword.objectstorageshort}} o si suprime la clave de servicio, se suprimirán las credenciales. La cuenta de {{site.data.keyword.objectstorageshort}} no se suprime hasta que desaprovisiona la instancia de {{site.data.keyword.objectstorageshort}}. Puede generar credenciales de nube nuevas [volviendo a enlazar o creando una nueva clave de servicio](#bind-object-storage-to-application).
