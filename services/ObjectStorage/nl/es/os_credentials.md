---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Generación de credenciales de servicio {: #credentials}

Las credenciales de servicio se utilizan para proporcionar autenticación y seguridad para el servicio. Puede generar credenciales nuevas mediante la CLI o la IU de {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}


## Para añadir credenciales a la IU:

1. En el separador **Credenciales de servicio** del panel de control de instancias del servicio, pulse **Nueva credencial** y dele un nombre.
2. Opcional: En el campo de texto **Añadir parámetros de configuración en línea**, introduzca la información de credencial del rol con el [tipo de acceso](/docs/services/ObjectStorage/os_access_types.html) que desee dar. La información debe seguir el formato de las cargas útiles de JSON.
    - Para crear un usuario administrativo: `{"role":"admin"}`
    - Para crear un usuario no administrativo: `{"role":"member"}`
3. Pulse **Añadir**.


## Para añadir credenciales utilizando mandatos de Cloud Foundry en la CLI:

1. Si no ha iniciado la sesión en {{site.data.keyword.Bluemix_notm}}, inicie la sesión como usuario con rol de desarrollador. Debe encontrarse en el espacio de la instancia de servicio que desee gestionar.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Generar credenciales de servicio. Dé un nombre a la credencial sustituyendo la variable
`service-key-name`. Opcionalmente, también puede asignar un [rol de usuario](/docs/services/ObjectStorage/os_access_types.html).

  ```
  cf create-service-key "<nombre_instancia_servicio>" <service-key-name> -c '{"role":"<rol_usuario>"}'
  ```
  {: pre}

  Ejemplo:
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
  ```
  {: screen}

3. Valide las credenciales de la clave que ha creado.

  ```
  cf service-keys <nombre_instancia_servicio>
  ```
  {: pre}

  Clave de ejemplo para una instancia con el nombre Object-Storage-Acl-Test para un usuario con un rol de miembro:

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



#### Para añadir credenciales utilizando mandatos de cURL en la CLI:

1. Si no ha iniciado la sesión en {{site.data.keyword.Bluemix_notm}}, inicie la sesión como usuario con rol de desarrollador. Debe encontrarse en el espacio de la instancia de servicio que desee gestionar.

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Ejecute el siguiente mandato para generar credenciales de servicio.

  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<guid_instancia_servicio>",   "name: <nombre_instancia_servicio>", "role: <rol_usuario>"}' -X POST -H "Authorization: <señal_portador>" -H "Content-Type: <content_type" -H "Cookie: <cookie>"
  ```
  {: pre}

  <table>
  <caption> Tabla 1. Variables de credenciales de servicio de cURL explicadas </caption>
    <tr>
      <th> Variable  </th>
      <th> Explicación </th>
    </tr>
    <tr>
      <td> ```https://api.ng.bluemix.net/v2/service_keys``` </td>
      <td> El punto final de la clave de servicio.  </td>
    </tr>
    <tr>
      <td><i> service_instance_guid </i></td>
      <td> Se puede encontrar en el URL.  </td>
    </tr>
    <tr>
      <td><i> name </i></td>
      <td> El nombre de la instancia de servicio. </td>
    </tr>
    <tr>
      <td><i> role </i></td>
      <td> Especifique el <a href= /docs/services/ObjectStorage/os_constructing.html>rol de usuario</a> como admin o member. </td>
    </tr>
    <tr>
      <td><i> señal_portador </i></td>
      <td> La señal que ha recibido al autenticar la instancia con Keystone. </td>
    </tr>
  </table>

3. Valide las credenciales ejecutando el mandato siguiente.

  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <señal_bearer>" -H "Cookie: "
  ```
  {: screen}
