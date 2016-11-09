---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

## Utilización de la API REST de Swift para acceder a {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}
*Última actualización: 19 de octubre de 2016*
{: .last-updated}

Puede utilizar la API REST de Swift con una interfaz de clientes de línea de mandatos, como por ejemplo cURL, o invocar la API desde la aplicación.
{: shortdesc}

### Construcción del URL de {{site.data.keyword.objectstorageshort}} {: #access-points}

Para interactuar con la API de {{site.data.keyword.objectstorageshort}}, genere el URL de {{site.data.keyword.objectstorageshort}} tal como se indica a continuación:
  ```
  https://<punto de acceso>/<versión de la API>/AUTH_<ID de proyecto>/<espacio de nombres del contenedor>/<object namespace>
  ```
  {: pre}

<table>
  <tr>
    <th> Partes del URL </th>
    <th> Definición</th>
  </tr>
  <tr>
    <td> Versión de API</td>
    <td> Versión 1: v1 </td>
  </tr>
  <tr>
    <td> Información sobre la cuenta</td>
    <td> Este es el ProjectID y el prefijo combinados. Se puede encontrar en la IU. </td>
  </tr>
  <tr>
    <td> Espacio de nombres del contenedor</td>
    <td> El nombre del contenedor. Se puede encontrar en la IU. </td>
  </tr>
  <tr>
    <td> Espacio de nombres de objeto</td>
    <td> El nombre de su archivo u objeto. Se puede encontrar en la IU. </td>
  </tr>
  <tr>
    <td> Punto de acceso</td>
    <td> Londres: https://lon.objectstorage.open.softlayer.com/
    <br> Dallas: https://dal.objectstorage.open.softlayer.com/ </br> </td>
  </tr>
</table>

*Tabla 1. Partes del URL de {{site.data.keyword.objectstorageshort}} explicadas*

Por ejemplo:

Partes del URL de ![{{site.data.keyword.objectstorageshort}} mostradas en una imagen de ejemplo](images/Swift_URL.png)


### API de {{site.data.keyword.objectstorageshort}} {: #openstack-reference}

Consulte la [Referencia completa de la API de OpenStack Swift](http://developer.openstack.org/api-ref-objectstorage-v1.html) para obtener una lista completa de las opciones y los ejemplos de la API REST de {{site.data.keyword.objectstorageshort}}.
