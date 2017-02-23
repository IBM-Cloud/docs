---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

# Control de acceso de pasarela (BETA)

**Importante**: esta característica está disponible actualmente como parte de una versión beta limitada.

Se autoriza a los dispositivos de pasarela para que actúen en nombre de otros dispositivos. Los grupos de recursos de pasarela definen los dispositivos de una organización en cuyo nombre puede actuar cada pasarela. Se puede asignar a las pasarelas el rol *Pasarela estándar*. Las pasarelas estándar solo pueden publicar o suscribirse a mensajes en nombre de los dispositivos de su grupo de recursos.
{: #shortdesc}


## Asignación de un rol a una pasarela

La asignación de un rol a una pasarela es obligatoria para que la pasarela tenga un grupo de recursos. Las pasarelas sin un grupo de recursos pueden actuar en nombre de todos los dispositivos de la organización. Al asignar el rol *Pasarela estándar* se crea de forma automática un nuevo grupo de recursos para la pasarela. Una vez se asigna una pasarela a un grupo de recursos, solo puede actuar en nombre de los dispositivos de ese grupo de recursos y de sí misma, incluso si se modifica su rol.

Para asignar un rol a una pasarela, utilice la siguiente API:

```
PUT /authorization/devices/{deviceId}/roles
```

Para obtener más información sobre el esquema de la solicitud, consulte la documentación de la API de [{{site.data.keyword.iot_full}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/put_authorization_devices_deviceId_roles).

## Adición de dispositivos a un grupo de recursos y eliminación de dispositivos del mismo

Para que una pasarela con el rol *Pasarela estándar* pueda actuar en nombre de un dispositivo, el dispositivo debe ser miembro del grupo de recursos asignado a la pasarela. Para añadir muchos dispositivos a un grupo de recursos simultáneamente, utilice la siguiente API:

```
 PUT /bulk/devices/{groupId}/add
```

El grupo al que van a añadir dispositivos debe estar especificado en la vía de acceso de la solicitud, y los dispositivos que se van a añadir deben estar especificados en el cuerpo de la solicitud. Para obtener más información sobre el esquema de la solicitud y las respuestas, consulte la documentación de la API de [{{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/put_bulk_devices_groupId_add).

Para eliminar varios dispositivos de un grupo de recursos, utilice la siguiente API:

```
PUT /bulk/devices/{groupId}/remove
```

Los dispositivos especificados en el cuerpo de la solicitud se eliminarán del grupo especificado en la vía de acceso de la solicitud. Para obtener más información sobre el esquema de la solicitud y la respuesta, consulte la documentación de la API de [{{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/put_bulk_devices_groupId_remove).

## Búsqueda de un grupo de recursos

Los grupos de recursos pueden tener etiquetas de búsqueda asociadas. Las etiquetas de búsqueda se puede utilizar para recuperar los detalles de un grupo de recursos utilizando la siguiente API:

```
GET /groups
```

Esta API devuelve los grupos de recursos asociados con la etiqueta de búsqueda utilizada. Si no se especifica ninguna etiqueta de búsqueda, se devuelven todos los grupos de recursos. <!-- For more information about the request schema, response, and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Para buscar el ID de un grupo de recursos, utilice la siguiente API:

```
GET /authorization/devices/{deviceId}
```

Esta API devuelve el identificador exclusivo del grupo o grupos de recursos de los que este dispositivo es miembro. Encontrará más información sobre esta API en la [documentación de API de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/get_authorization_devices_deviceId).

## Consulta de un grupo de recursos

Los grupos de recursos se pueden consultar con varios parámetros que devuelven todas las propiedades de todos los dispositivos del grupo, los identificadores exclusivos de todos los dispositivos del grupo o las propiedades del grupo de recursos.

Para que se devuelvan todas las propiedades de todos los dispositivos del grupo de recursos especificado, utilice la siguiente API:

```
GET /bulk/devices/{groupId}
```

Esta API devuelve la lista completa de propiedades de todos los miembros del grupo de recursos especificado. Para obtener más información sobre el esquema de la solicitud, respuestas y cómo pasar páginas de los resultados, consulte la [documentación de API de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/get_bulk_devices_groupId).

Para que se devuelvan solo los identificadores exclusivos de los miembros del grupo de recursos, utilice la siguiente API:

```
GET /bulk/devices/{groupId}/ids
```

Esta API devuelve los identificadores exclusivos de todos los dispositivos que son miembros del grupo de recursos. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Para que se devuelvan las propiedades del grupo de recursos, utilice la siguiente API:

```
GET /groups/{groupId}
```

Esta API devuelve las propiedades del grupo de recursos (nombre, descripción, etiquetas de búsqueda e identificador exclusivo) especificado en la vía de acceso, pero no devuelve la lista de miembros del grupo de recursos.
<!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Creación y supresión de un grupo de recursos.

Los grupos de recursos se pueden crear y suprimir de forma independiente de las pasarelas de conexión. Para crear un grupo de recursos, utilice la siguiente API:

```
POST /groups
```

Esta API crea un grupo de recursos y devuelve los detalles del grupo. <!-- For details on the request schema and the responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Para suprimir un grupo de recursos, utilice la siguiente API:

```
DELETE /groups/{groupId}
```

Esta API suprime el grupo de recursos especificado. Los dispositivos que han sido miembros del grupo se eliminan del grupo, pero, por lo demás, los propios dispositivos no se ven afectados.<!-- For more information, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Actualización de las propiedades de un grupo



  - /groups/{groupId}
    - PUT: actualiza las propiedades del grupo especificado.

## Recuperación y actualización de propiedades del dispositivo.

Hay varias formas de recuperar propiedades de un dispositivo mediante API; cada API devuelve información diferente. Para recuperar las propiedades de todos los dispositivos conectados a su organización {{site.data.keyword.iot_short_notm}}, utilice la siguiente API:

```
GET /authorization/devices:

```

Esta API devuelve las propiedades de todos los dispositivos conectados a la organización, incluidas sus propiedades relevantes de control de acceso (rol, estado, fecha de caducidad).<!-- For more information on responses and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Para recuperar propiedades del dispositivo sin recuperar la información relevante de control de acceso, utilice la siguiente API:

```
GET /authorization/devices/{deviceId}
```

Esta API devuelve todas las propiedades del dispositivo especificado, sin devolver la información de control de acceso. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} device model documentation](LINK TO DEVICE MODEL) and [API documentation](LINK TO CORRECT API). -->

Para recuperar la información de control de acceso de un dispositivo específico, utilice la siguiente API:

```
GET /authorization/devices/{deviceId}/roles:
```

Esta API recupera la información relevante de control de acceso del dispositivo especificado sin devolver otras propiedades del dispositivo.
<!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Las propiedades de un dispositivo se pueden actualizar de dos maneras. Las propiedades se pueden actualizar sin cambiar las propiedades de control de acceso o las propiedades de control de acceso se pueden actualizar directamente.

Para actualizar las propiedades del dispositivo sin que ello afecte a las propiedades de control de acceso, utilice la siguiente API:

```
PUT /authorization/devices/{deviceId}
```

Esta API solo actualiza las propiedades del dispositivo que no están asociadas al control de acceso.
<!-- For more information on request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Para actualizar únicamente las propiedades de control de accesos del dispositivo especificado, utilice la siguiente API:

```
PUT /authorization/devices/{deviceId}/withroles:
```

Esta API solo actualizará las propiedades de control de acceso del dispositivo especificado. <!-- For more information on the request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->
