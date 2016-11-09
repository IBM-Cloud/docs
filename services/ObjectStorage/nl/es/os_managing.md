---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Gestión de {{site.data.keyword.objectstorageshort}} entre regiones {: #multi-regions}
*Última actualización: 19 de octubre de 2016*
{: .last-updated}

El servicio de {{site.data.keyword.objectstorageshort}} da soporte a las regiones de almacenamiento Dallas y Londres. Estas regiones de almacenamiento son independientes de la región {{site.data.keyword.Bluemix_notm}}, como por ejemplo EE.UU.-Sur y Reino Unido, en la que se crea la instancia de servicio de {{site.data.keyword.objectstorageshort}}. Si crea una instancia en la región de {{site.data.keyword.Bluemix_notm}} EE.UU.-Sur, puede leer y grabar datos en cualquier región de almacenamiento Dallas o Londres.
{: shortdesc}

Para la región {{site.data.keyword.Bluemix_notm}} EE.UU.-Sur, la región de almacenamiento Dallas es el valor predeterminado. Para la región {{site.data.keyword.Bluemix_notm}} Reino Unido, la región de almacenamiento Londres es el valor predeterminado.  La interfaz de usuario de {{site.data.keyword.objectstorageshort}} siempre se lanza en la región de almacenamiento predeterminada de la región {{site.data.keyword.Bluemix_notm}}. Para conmutar regiones, pulse la lista desplegable de Región de {{site.data.keyword.objectstorageshort}} y seleccione otra región.

**Nota:** El servicio de {{site.data.keyword.objectstorageshort}} NO da soporte a la réplica de la región de almacenamiento cruzada.

### Acceso de varias regiones

Para utilizar el servicio de {{site.data.keyword.objectstorageshort}}, debe [autenticarse con OpenStack Keystone](../ObjectStorage/os_security.html#keystone-authentication){: new_window}. Una vez que se haya autenticado correctamente, estarán disponibles en la respuesta `X-Subject-Token` y los puntos finales de {{site.data.keyword.objectstorageshort}}. Cada región de almacenamiento tiene un [punto de acceso](../ObjectStorage/os_api.html#access-points) distinto.


Por ejemplo, para crear un contenedor denominado `my_container` en la región de almacenamiento Dallas, especifique un punto de acceso Dallas en el mandato curl como se indica a continuación:

  ```
  curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
Recibirá el resultado siguiente:

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

Para crear un contenedor denominado `my_container` en la región de almacenamiento Londres, especifique un punto de acceso Londres en el mandato curl como se indica a continuación:

  ```
  curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
Recibirá el resultado siguiente:

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

**Nota:** El `X-Subject-Token` adquirido desde Keystone, etiquetado como `X-Trans-ID` en el ejemplo, funciona entre regiones de almacenamiento.
