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


# Tipos de acceso

Los usuarios de {{site.data.keyword.objectstorageshort}} pueden ser administrativos o no administrativos. Las listas de control de acceso las habilitan los usuarios administrativos a nivel de contenedor.
{: shortdesc}

<table>
<caption> Tabla 1. Roles de usuario definidos </caption>
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


Puede gestionar usuarios de {{site.data.keyword.objectstorageshort}} a través de la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, la API de Cloud Foundry o la CLI de Cloud Foundry.
