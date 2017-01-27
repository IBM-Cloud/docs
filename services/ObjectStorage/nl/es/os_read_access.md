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


# Concesión de acceso de lectura

Un usuario de {{site.data.keyword.objectstorageshort}} con [rol de administrador](/docs/services/ObjectStorage/os_access_types.html) puede conceder acceso de lectura a un contenedor para otro usuario y manipular las combinaciones de ACL de lectura.
{: shortdesc}

<table>
<caption> Tabla 1. Permisos de acceso de lectura por opción</caption>
  <tr>
    <th> Permiso </th>
    <th> Opciones de ACL de lectura </th>
  </tr>
  <tr>
    <td> Lectura para todos los usuarios a los que se hace referencia para la afiliación de cuentas </td>
    <td> <code> .r,&#42;  </code> </td>
  </tr>
  <tr>
    <td> Lectura y lista para todos los usuarios a los que se hace referencia y se incluyen en la lista </td>
    <td> <code> .r:&#42;,.rlistings </code> </td>
  </tr>
  <tr>
    <td> Lectura y lista para un usuario especificado en un proyecto específico </td>
    <td> <code> project_id:user_id </code> </td>
  </tr>
  <tr>
    <td> Lectura y lista para un usuario especificado en cada proyecto </td>
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> Lectura y lista para cada usuario de un proyecto especificado </td>
    <td> <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> Lectura y lista para cada usuario del proyecto  </td>
    <td> <code> &#42;:&#42; </code> </td>
  </tr>
</table>



1. Autenticar las credenciales. Puede utilizar las credenciales que se encuentran en el separador de credenciales de servicio de la IU o bien puede generar credenciales nuevas. Para obtener más información sobre la generación de nuevas credenciales, consulte [Generación de credenciales de servicio](/docs/services/ObjectStorage/os_credentials.html). Recibirá el URL de {{site.data.keyword.objectstorageshort}} y la señal de autenticación como salida.

    Mandato Swift:

    ```
    export OS_USER_ID=<user_id>
    export OS_PASSWORD=<password>
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

    Ejemplo: El valor `X-Container-Read` muestra el contenedor y el acceso a los que se otorga acceso de lectura. 

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
