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


# Concesión de acceso de escritura

Un usuario de {{site.data.keyword.objectstorageshort}} con un [rol de administrador](/docs/services/ObjectStorage/os_access_types.html) puede conceder acceso de escritura a otro usuario y manipular las combinaciones de ACL de escritura.
{: shortdesc}

<table>
<caption> Tabla 1. Permisos de acceso de escritura por opción</caption>
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
    <td> <code> &#42;:user_id </code> </td>
  </tr>
  <tr>
    <td> Escritura para cada usuario de un proyecto específico </td>
    <td>  <code> project_id:&#42; </code> </td>
  </tr>
  <tr>
    <td> Escritura para cada usuario de cada proyecto </td>
    <td>  <code> &#42;:&#42; </code> </td>
  </tr>
</table>



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

2. Conceda acceso de escritura ejecutando el siguiente mandato.

    Mandato Swift:

    ```
    swift post <nombre_contenedor> --write-acl "<ID_usuario>:<ID_proyecto>"
    ```
    {: pre}

    Mandato cURL:

    ```
    curl -i <URL_ALMACENAMIENTO_SO> -X POST -H "Content-Length: 0" -H "X-Container-Write: <ID_usuario>:<ID_proyecto>" -H "X-Auth-Token: <SEÑAL_AUTENTICACIÓN_SO>"
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
