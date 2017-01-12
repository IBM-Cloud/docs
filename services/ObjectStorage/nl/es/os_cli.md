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


# Acceso a {{site.data.keyword.objectstorageshort}} utilizando la CLI de Swift {: #using-swift-cli}


El servicio de {{site.data.keyword.objectstorageshort}} se basa en OpenStack Swift y se puede acceder a él mediante cualquier aplicación cliente compatible. Esta sección describe cómo utilizar el cliente de Python Swift, que es la interfaz de línea de mandatos (CLI) para la API de {{site.data.keyword.objectstorageshort}} y sus extensiones, para que funcione con los contenedores y los archivos.
{: shortdesc}




## Instalación del cliente de Swift {: #install-swift-client}

Si no lo ha hecho aún, instale el siguiente [software de requisito previo](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}.
* Python 2.7 o posterior
* Paquete setuptools
* Paquete pip


Para instalar el cliente de Python Swift, ejecute el mandato siguiente:
```
pip install python-swiftclient
```
{: pre}

Para instalar el cliente de Python Keystone, ejecute el mandato siguiente:
```
pip install python-keystoneclient
```
{: pre}




## Configuración del cliente {: #setup-swift-client}

Para configurar el cliente de Swift, debe `exportar` la información de autenticación. Puede generar credenciales [mediante la IU](../ObjectStorage/os_security.html#understanding-credentials) o [mediante la CLI](../ObjectStorage/os_cli.html#generating-cli).

Para exportar la información de autenticación, especifique sus credenciales y ejecute el siguiente mandato:
```
export OS_USER_ID=
export OS_PASSWORD=
export OS_PROJECT_ID=
export OS_AUTH_URL=
export OS_REGION_NAME=
export OS_IDENTITY_API_VERSION=
export OS_AUTH_VERSION=

swift auth
```
{: codeblock}


Ejemplo:
```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
  export OS_PASSWORD=*******
  export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=dallas
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

swift auth
```
{: screen}




## Generación de credenciales de servicio de {{site.data.keyword.objectstorageshort}} {: #generating-cli}

Para generar credenciales de servicio utilizando la CLI de Swift, puede utilizar los pasos siguientes.

1. Si no ha iniciado la sesión en {{site.data.keyword.Bluemix_notm}}, inicie la sesión como usuario con rol de desarrollador. Debe encontrarse en el espacio de la instancia de servicio que desee gestionar.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Generar credenciales de servicio. `service-key-name` es el nombre que le da a su credencial. Puede utilizar el mandato Cloud Foundry o el mandato cURL.
  Mandato Cloud Foundry:
  ```
  cf create-service-key "<nombre_instancia_servicio_almacenamiento_objetos>" <service-key-name> -c '{"role":"<rol_almacenamiento_objetos>"}'
  ```
  {: pre}

  Mandato de ejemplo de Cloud Foundry:
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
  ```
  {: screen}

  Mandato cURL:
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "guid_instancia_servicio": "<guid_instancia_servicio>",   "name": "<nombre_usuario>", "role": "member"}' -X POST -H "Authorization: <señal_portador>" -H "Content-Type: " -H "Cookie: "
  ```
  {: pre}

3. Valide las credenciales de la clave de servicio creada.
  Mandato Cloud Foundry:
  ```
  cf service-keys <instancia_servicio>
  ```
  {: pre}

  Clave de servicio miembro de ejemplo para una instancia denominada Object-Storage-Acl-Test:

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
  {: screen}

  Mandato cURL:
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <señal_bearer>" -H "Cookie: "
  ```
  {: pre}




## Almacenamiento de objetos en contenedores mediante la CLI {: #storing-cli}

1. Si no ha iniciado la sesión en {{site.data.keyword.Bluemix_notm}}, inicie la sesión en la organización y espacio que contiene su instancia de {{site.data.keyword.objectstorageshort}}.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Cree un nuevo contenedor de {{site.data.keyword.objectstorageshort}} ejecutando el siguiente mandato. Usted establecerá la variable *nombre_contenedor* en este momento.
  ```
  swift post <nombre_contenedor>
  ```
  {: pre}

**Nota**: Si aparece un mensaje de error, confirme que ha instalado [el software de requisito previo](../ObjectStorage/os_cli.html##install-swift-client).

3. (Opcional:) Para verificar que se haya creado el contenedor, ejecute el siguiente mandato para listar los contenedores.
  ```
  swift list
  ```
  {: pre}

4. Para evitar la destrucción de datos debido a sobrescrituras accidentales, [configure el mantenimiento de versiones de objetos](../ObjectStorage/os_versioning.html#work-with-object-versioning). Si no desea el mantenimiento de versiones de objetos, genere una lista de los archivos existentes en el almacén y, si es necesario, renombre el directorio o los archivos antes de cargarlos.

4. Cargue un archivo en el contenedor ejecutando el siguiente mandato.
  ```
  swift upload <nombre_contenedor> <nombre_archivo>
  ```
  {: pre}

**Nota**: Para cargar archivos mayores de 5 GB, [son necesarios pasos adicionales](../ObjectStorage/os_large_files.html#large-files). 


5. (Opcional:) Para verificar que la carga ha sido correcta, visualice el contenido del contenedor ejecutando el mandato siguiente:
  ```
  swift list <nombre_contenedor>
  ```
  {: pre}




## Descarga de objetos con la CLI de Swift {: #downloading-cli}


1.  Si no ha iniciado la sesión en {{site.data.keyword.Bluemix_notm}}, inicie la sesión en la organización y espacio que contiene su instancia de {{site.data.keyword.objectstorageshort}}.

```
cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
```
{: pre}

2. Para evitar la destrucción de datos debido a sobrescrituras accidentales, [configure el mantenimiento de versiones de objetos](../ObjectStorage/os_versioning.html#work-with-object-versioning). Si no desea el mantenimiento de versiones de objetos, genere una lista de los archivos existentes en el almacén y, si es necesario, renombre el directorio o los archivos antes de descargarlos.

3. Descargue un archivo ejecutando el siguiente mandato:

```
swift download <nombre_contenedor> <nombre_contenedor>
```
{: pre}




## Supresión de objetos y contenedores mediante la CLI {: #deleting-cli}

**Atención**: Si suprime el contenedor, suprimirá cualquier objeto que esté almacenado en el contenedor.

1.  Si no ha iniciado la sesión en {{site.data.keyword.Bluemix_notm}}, inicie la sesión en la organización y espacio que contiene su instancia de {{site.data.keyword.objectstorageshort}}.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. (Opcional:) Confirme que tiene una copia de seguridad de los objetos antes de suprimir los archivos y contenedores.

3. Ejecute el siguiente mandato para suprimir un archivo:
  ```
  swift delete <nombre_contenedor> <nombre_archivo>
  ```
  {: pre}

3. Para suprimir el contenedor, ejecute el mandato siguiente:
  ```
  swift delete <nombre_contenedor>
  ```
  {: pre}

**Nota**: Puede planificar una [hora específica para que se suprima el objeto](../ObjectStorage/os_deletion.html#schedule-object-deletion).




## Trabajo con directorios {: #directory-cli}

#### Cómo añadir un directorio a un contenedor con la CLI de Swift

Swift no tiene una auténtica estructura de directorios, sino que utiliza la denominación para representar un diseño de directorios. Si especifica un nombre de directorio, se adjuntará a todos los nombres de archivo como parte de la vía de acceso relativa.

1. Localmente, cree un directorio y guarde el archivo en él.
2. Ejecute el siguiente mandato para cargar un directorio al contenedor:
  ```
  swift upload <nombre_contenedor> <nombre_directorio>
  ```
  {: pre}

#### Descarga de un directorio
Para descargar una estructura de directorios, utilice el parámetro `-prefix` para indicar el directorio o la estructura de directorios que desea descargar.

1. Ejecute el siguiente mandato para descargar un directorio:
  ```
  swift download <nombre_contenedor> --prefix <directorio>
  ```
  {: pre}
