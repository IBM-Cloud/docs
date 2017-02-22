---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Configuración de la CLI para utilizar mandatos de Swift y Cloud Foundry

Para interactuar con el servicio de {{site.data.keyword.objectstorageshort}} utilizando mandatos de Swift o Cloud Foundry, debe instalar el software de requisito previo.
{: shortdesc}


## Instalación del cliente de Swift {: #install-swift-client}

Si no lo ha hecho aún, instale el siguiente software de requisito previo.
* Python 2.7 o posterior
* Paquete setuptools
* Paquete pip
* CLI de Cloud Foundry


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

Para obtener más información sobre los requisitos previos, consulte [la documentación de Openstack](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}.


## Configuración del cliente {: #setup-swift-client}

Para configurar el cliente de Swift, debe `exportar` la información de autenticación. Puede [generar credenciales](/docs/services/ObjectStorage/os_credentials.html) mediante la CLI utilizando los mandatos de Cloud Foundry o cURL o mediante la IU de {{site.data.keyword.Bluemix_notm}}. El cliente toma la información de las variables de entorno de la tabla siguiente.

<table>
<caption> Tabla 1. Descripciones y variables de entorno</caption>
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
    <td> URL del punto final. Asegúrese de que <code>/v3</code> esté añadido al final del URL. </td>
  </tr>
</table>



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
