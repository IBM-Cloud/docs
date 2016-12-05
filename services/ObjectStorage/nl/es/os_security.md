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


# Protección de archivos {: #understanding-authentication}


## Descripción de las credenciales de servicio {: #understanding-credentials}

Las credenciales de servicio se utilizan para proporcionar autenticación y seguridad para el servicio. Se genera automáticamente un conjunto de credenciales cuando se proporciona una instancia. El cliente de Swift toma la información de autenticación de las variables de entorno de la tabla siguiente.

<table>
  <tr>
    <th> Variable de entorno </th>
    <th> Descripción </th>
  </tr>
  <tr>
    <td> <code>OS_USER_ID</code> </td>
    <td> El ID de usuario de {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> <code>OS_PASSWORD</code> </td>
    <td> La contraseña de la instancia de {{site.data.keyword.objectstorageshort}}. </td>
  </tr>
  <tr>
    <td> <code>OS_PROJECT_ID</code> </td>
    <td> El ID del proyecto. </td>
  </tr>
  <tr>
    <td> <code>OS_REGION_NAME</code> </td>
    <td> La región en la que se almacenan los objetos. {{site.data.keyword.objectstorageshort}} está disponible en las regiones de Dallas y Londres. </td>
  </tr>
  <tr>
    <td> <code>OS_AUTH_URL</code> </td>
    <td> URL del punto final. Asegúrese de que `/v3` esté añadido al final del URL. </td>
  </tr>
</table>

Tabla 1: Variables y descripciones de autenticación

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

Tabla 2: Roles de usuario definidos

Puede gestionar usuarios de {{site.data.keyword.objectstorageshort}} a través de la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, la API de Cloud Foundry o la CLI de Cloud Foundry.




## Concesión de acceso de lectura {: #read-access}

Un usuario de {{site.data.keyword.objectstorageshort}} con rol de administrador puede conceder acceso de lectura a un contenedor para otro usuario y manipular las combinaciones de ACL de lectura.

<table>
  <tr>
    <th> Permiso </th>
    <th> Opciones de ACL de lectura </th>
  </tr>
  <tr>
    <td> Lectura para todos los usuarios a los que se hace referencia para la afiliación de cuentas </td>
    <td> <code> .r,*` </code> </td>
  </tr>
  <tr>
    <td> Lectura y lista para todos los usuarios a los que se hace referencia y se incluyen en la lista </td>
    <td> <code>.r:*,.rlistings</code> </td>
  </tr>
  <tr>
    <td> Lectura y lista para un usuario especificado en un proyecto específico </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Lectura y lista para un usuario especificado en cada proyecto </td>
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> Lectura y lista para cada usuario de un proyecto especificado </td>
    <td> <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> Lectura y lista para cada usuario del proyecto  </td>
    <td> <code> *:* </code> </td>
  </tr>
</table>

Tabla 3: Permisos de acceso de lectura por opción



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



## Concesión de acceso de escritura {: #write-access}

Un usuario de {{site.data.keyword.objectstorageshort}} con un rol de administrador puede conceder acceso de escritura a un contenedor para otro usuario y manipular las combinaciones de ACL de escritura.

<table>
  <tr>
    <th> Permiso </th>
    <th> Opciones de ACL de escritura </th>
  </tr>
  <tr>
    <td> Escritura para un usuario especificado en un proyecto específico </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Escritura para un usuario especificado en cada proyecto </td>
    <td> <code> *:user_id </code> </td>
  </tr>
  <tr>
    <td> Escritura para cada usuario de un proyecto específico </td>
    <td>  <code> project_id:* </code> </td>
  </tr>
  <tr>
    <td> Escritura para cada usuario de cada proyecto </td>
    <td>  <code> *:* </code> </td>
  </tr>
</table>

Tabla 4: Permisos de acceso de escritura por opción



1. Autentique sus credenciales utilizando la información de las credenciales de servicio creadas.  Recibirá el URL de {{site.data.keyword.objectstorageshort}} y la señal de autenticación como salida.
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
