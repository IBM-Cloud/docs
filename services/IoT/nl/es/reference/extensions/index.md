---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integraciones de servicios externos
{: #ref-index}

La integración de servicios externos le permite acceder a los datos y operaciones de terceros o servicios externos dentro de la organización de {{site.data.keyword.iot_full}}.

## Jasper
{: #jasper}

Jasper es una plataforma de administración y gestión de dispositivos SIM. Jasper está integrado en el panel de instrumentos de {{site.data.keyword.iot_short_notm}}, lo que hace posible administrar dispositivos Jasper a través de su panel de instrumentos de la organización de {{site.data.keyword.iot_short_notm}}.

### Operaciones soportadas para Jasper

La integración incorporada de Jasper que proporciona nuestra plataforma proporciona soporte para las siguientes operaciones de Jasper:

- Ver datos de Jasper generales
  - Muestra el estado, el plan de tarifas, el uso de datos mensual hasta la fecha, el uso de SMS mensual hasta la fecha, el uso de voz mensual hasta la fecha, los límites por exceso de datos, la fecha de añadido y la fecha de modificación.
- Cambiar el estado de activación de SIM.
  - Puede seleccionar entre Inventario, Preparado para la activación, Activado, Desactivado y Retirado.
- Ver uso de SIM
  - Muestra la fecha de inicio de ciclo, los datos totales y facturables, los SMS totales y facturables y la voz total y facturable.
  - La fecha de inicio del ciclo puede establecerse con un formato AAAA-MM-DD.
- Enviar SMS a SIM
- Cambiar el plan de tarifas

Puede acceder a las operaciones soportadas en los detalles de dispositivo de un dispositivo conectado a Jasper una vez que finalicen los siguientes pasos de configuración.

### API REST para Jasper
Para acceder a la API REST para Jasper, consulte la sección sobre la extensión Jasper en la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}} ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Jasper_Extension){: new_window}.

### Configuración para Jasper

Para conectar el servicio de Jasper a la organización de {{site.data.keyword.iot_short_notm}}, hay dos etapas de configuración que debe realizar en primer lugar. Primero, el {{site.data.keyword.iot_short_notm}} debe estar conectado al servicio de Jasper y, a continuación, se deben configurar los dispositivos de {{site.data.keyword.iot_short_notm}}.


1. Habilitar la extensión de Jasper. Para habilitar la integración de Jasper con su organización de {{site.data.keyword.iot_short_notm}}, lleve a cabo los pasos siguientes:
  1. Desde el panel de instrumentos de {{site.data.keyword.iot_short_notm}}, seleccione **Extensiones**.
  2. En la página **Extensiones**, pulse **Añadir ampliación**.
  3. Pulse **Añadir** junto a Jasper.
  4. Especifique su nombre de usuario, contraseña, clave de acceso e ID de dominio de Jasper.
  5. Pulse **Terminado**.

2. Configurar los dispositivos
Puede configurar los dispositivos que están conectados a la organización de {{site.data.keyword.iot_short_notm}} y a la cuenta de Jasper para que muestren datos desde Jasper en el panel de instrumentos de {{site.data.keyword.iot_short_notm}}.  
**Importante:** La configuración de Jasper no se puede aplicar como parte del proceso de Añadir dispositivo. Sólo se pueden configurar con Jasper los dispositivos conectados previamente.  
Para configurar los dispositivos conectados a Jasper, lleve a cabo los pasos siguientes:
 1. En el separador Dispositivos del panel de instrumentos de {{site.data.keyword.iot_short_notm}}, busque el dispositivo conectado a Jasper que se debe configurar.
 2. Seleccione el dispositivo para abrir la vista *Obtener detalles de dispositivo*.
 3. Desplácese hacia abajo hasta *Configuración de ampliación*.
 4. Escriba la configuración de ampliación utilizando el siguiente formato de JSON y, a continuación, pulse **Confirmar cambios** para guardar la configuración.  

```json  
    {
        "jasper": {
            "iccid": "string"
        }
    }

```

Cuando la organización se ha configurado correctamente, se muestra la sección *Ampliaciones* debajo de la sección *Configuración de ampliaciones* de la vista *Detalle de dispositivo*.

## AT&T
{: #att}

### Operaciones soportadas para AT&T

La ampliación de AT&T permite realizar las siguientes operaciones de AT&T:

- Ver datos de AT&T generales
  - Muestra el estado, el plan de tarifas, el uso de datos mensual hasta la fecha, el uso de SMS mensual hasta la fecha, el uso de voz mensual hasta la fecha, los límites por exceso de datos, la fecha de añadido y la fecha de modificación.
- Cambiar el estado de activación de SIM.
  - Puede seleccionar entre Inventario, Preparado para la activación, Activado, Desactivado y Retirado.
- Ver uso de SIM
  - Muestra la fecha de inicio de ciclo, los datos totales y facturables, los SMS totales y facturables y la voz total y facturable.
  - La fecha de inicio del ciclo puede establecerse con un formato AAAA-MM-DD.
- Enviar SMS a SIM
- Cambiar el plan de tarifas

### API REST para AT&T
Para acceder a la API REST para AT&T, consulte la sección sobre la extensión AT&T en la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}} ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/AT&T_Extension){: new_window}.

### Configuración para AT&T

Para conectar la organización de {{site.data.keyword.iot_short_notm}} a AT&T, debe completar la configuración de la organización y la configuración del dispositivo.

Para configurar la plataforma de {{site.data.keyword.iot_short_notm}}, lleve a cabo los pasos siguientes:

1. Habilitar la extensión de AT&T. Para habilitar la integración de AT&T con la organización de {{site.data.keyword.iot_short_notm}}, lleve a cabo los pasos siguientes:
  1. Desde el panel de instrumentos de {{site.data.keyword.iot_short_notm}}, seleccione **Extensiones**.
  2. En la página **Extensiones**, pulse **Añadir ampliación**.
  3. Pulse **Añadir** junto a AT&T.
  4. Especifique su nombre de usuario, contraseña, clave de acceso e ID de dominio de AT&T.
  5. Pulse **Terminado**.

Para conectar la organización de {{site.data.keyword.iot_short_notm}} con la cuenta de AT&T, hay dos etapas de configuración que debe realizar en primer lugar. Complete la configuración de organización y, a continuación, configure los dispositivos.


2. Configurar los dispositivos
Puede configurar los dispositivos conectados a la organización de {{site.data.keyword.iot_short_notm}} y a la cuenta de AT&T para que muestren datos de AT&T en el panel de instrumentos de {{site.data.keyword.iot_short_notm}}.  
**Importante:** La configuración de AT&T no se puede aplicar como parte del proceso Añadir dispositivo. Sólo se pueden configurar los dispositivos conectados anteriormente con AT&T.  
Para configurar los dispositivos conectados a AT&T, lleve a cabo los pasos siguientes:
 1. En el separador Dispositivos del panel de instrumentos de {{site.data.keyword.iot_short_notm}}, busque el dispositivo conectado a AT&T que se debe configurar.
 2. Seleccione el dispositivo para abrir la vista *Obtener detalles de dispositivo*.
 3. Desplácese hacia abajo hasta *Configuración de ampliación*.
 4. Escriba la configuración de ampliación utilizando el siguiente formato de JSON y, a continuación, pulse **Confirmar cambios** para guardar la configuración.  

```json  
    {
        "atnt": {
            "iccid": "string"
        }
    }

```

Cuando la organización se ha configurado correctamente, se muestra la sección *Ampliaciones* debajo de la sección *Configuración de ampliaciones* de la vista *Detalle de dispositivo*.

## Conector ARM mbed
{: #arm}

El conector ARM mbed le permite conectar el dispositivo ARM mbed a su {{site.data.keyword.iot_short_notm}}. La extensión ARM mbed permite el portal ARM mbed y el {{site.data.keyword.iot_short_notm}} para enviar y recibir datos del portal ARM mbed.

### Definir configuración


1. Habilitar la extensión de conector de ARM mbed. Para habilitar la extensión de conector de ARM mbed, lleve a cabo los pasos siguientes:
  1. Desde el panel de instrumentos de {{site.data.keyword.iot_short_notm}}, seleccione **Configuración** y vaya a **Extensiones**.
  2. En el menú **Extensiones**, pulse **Añadir ampliación**.
  3. Pulse **Añadir** junto a la extensión de conector de ARM mbed.
  4. Especifique su clave de acceso e ID de dominio de ARM mbed. Puede encontrarlos mediante el portal de ARM mbed en https://connector.mbed.com.
  5. Compruebe que las credenciales sean correctas pulsando el botón **Comprobar conexión**.
  6. Pulse **Terminado**.

### Formato de carga útil

Hay dos tipos de mensajes de entrada de la plataforma ARM mbed: notificaciones y respuestas asíncronas. El {{site.data.keyword.iot_short_notm}} puede enviar mandatos a los dispositivos que están conectados a la plataforma ARM mbed.

#### Notificaciones

Las notificaciones las generan cambios en los datos de dispositivo o de sensor. Una vez que {{site.data.keyword.iot_short_notm}} procesa el mensaje, es para el tema de sucesos de dispositivos de la misma manera que un dispositivo conectado directamente al {{site.data.keyword.iot_short_notm}}. El tipo de suceso utilizado para las notificaciones que se originan en dispositivos conectados a la plataforma ARM mbed es `notify`.

El ejemplo de código siguiente muestra el formato de carga útil para una notificación enviada por la API de la plataforma ARM mbed:

```
{
  "ep":<endpoint/deviceID>,
  "path":<resource path>,
  "ct":<content type>,
  "payload":<Base64 encoded payload>,
  "max-age":<how long the payload is valid, in seconds>
}
```

#### Respuestas asíncronas

Cuando el {{site.data.keyword.iot_short_notm}} envía un mandato a un dispositivo conectado a la plataforma ARM mbed, el dispositivo envía un mensaje de confirmación al {{site.data.keyword.iot_short_notm}}. Este mensaje de confirmación se denomina *respuesta asíncrona* y utiliza el tipo de suceso `asyncResponse`.

El ejemplo de código siguiente muestra el formato de carga útil para una respuesta asíncrona enviada por el servicio de nube de ARM mbed:

```
{
  "id":<transaction id>,
  "status":<200 is command was sucessfully executed. Check other HTTP response codes>,
  "ct":<content type>,
  "max-age":<how long the payload is valid, in seconds>,
  "payload":<base64 encoded payload>,
  "ep":<endpoint/deviceID affected by the command>,
  "path":<resource path affected by the command>
}
```

#### Envío de mandatos a la plataforma ARM mbed

El {{site.data.keyword.iot_short_notm}} puede enviar mandatos a dispositivos conectados a la plataforma ARM mbed. Los mandatos enviados a la plataforma ARM mbed deben utilizar el siguiente formato JSON.

```
{
  "method":<PUT or POST>,
  "deviceId":<endpoint/deviceId>,
  "resourceId":<resource path>,
  "payload": <Base64 encoded payload>
}
```
El método elegido distingue entre mayúsculas y minúsculas. El '/' inicial de la vía de acceso de recurso se debe omitir.


La carga útil debe publicarse en el tema siguiente:

```
iot-2/type/<device_type>/id/<deviceId>/cmd/<command_type>/fmt/<command_format>
```


## Orange
{: #orange}

La extensión de Orange le permite ver datos de la tarjeta SIM desde dispositivos que están conectados a {{site.data.keyword.iot_short_notm}} y que tienen una tarjeta SIM de Orange instalada.

https://developer.ibm.com/iotplatform/2016/03/30/watson-iot-platform-integration-with-orange-beta/

### Operaciones soportadas para Orange

Si tiene un dispositivo que está conectado a su servicio de {{site.data.keyword.iot_short_notm}} y que tiene una tarjeta SIM de Orange, puede utilizar la extensión de Orange para ver los siguientes datos de la tarjeta SIM:

- Número de serie de SIM
- Estado de activación
- Último cambio de estado
- Última renovación de estado
- Estado de la ubicación

### API REST para Orange
Para acceder a la API REST para Orange, consulte la sección sobre la extensión Orange en la [documentación de la API REST HTTP de {{site.data.keyword.iot_short_notm}} ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Orange_Extension){: new_window}.

### Configuración para Orange

Para habilitar la extensión de Orange:

1. Desde el panel de instrumentos de {{site.data.keyword.iot_short_notm}}, seleccione **Extensiones**.
2. En la página **Extensiones**, pulse **Añadir ampliación**.
3. Pulse **Añadir** junto a la extensión de Orange.
4. Especifique el nombre de usuario y la contraseña de Orange.
6. Pulse **Terminado**.

Una vez que se haya habilitado la extensión de Orange, se debe configurar cada dispositivo con una tarjeta SIM de Orange para que visualice datos de la SIM de Orange.

1. En el separador Dispositivos del panel de instrumentos de {{site.data.keyword.iot_short_notm}}, busque el dispositivo SIM de Orange que se debe configurar.
2. Seleccione el dispositivo y desplácese hacia abajo hasta *Configuración de extensión*.
3. Escriba la configuración de ampliación utilizando el siguiente formato de JSON y, a continuación, pulse **Confirmar cambios** para guardar la configuración.

```  
    {
        "orange": {
            "serialnumber": "<número de serie de la SIM de Orange>"
        }
    }

```
Cuando la organización se ha configurado correctamente, se muestra la sección *Ampliaciones* debajo de la sección *Configuración de ampliaciones* de la vista *Detalle de dispositivo*.

## Almacenamiento de datos históricos
{: #historical_data}

La extensión de almacenamiento de datos históricos le permite ubicar y configurar servicios de almacenamiento de mensajes compatibles como, por ejemplo, [{{site.data.keyword.cloudantfull}}](../../cloudant_connector.html) o [{{site.data.keyword.messagehub_full}}](../../message_hub.html) para los datos de IoT.

## Paquetes de gestión de dispositivos personalizados
{: #device_mgmt}

La gestión de dispositivos es una característica principal de la {{site.data.keyword.iot_short_notm}}; sin embargo, se puede ampliar para desarrollar funciones adicionales. Los paquetes de gestión de dispositivos personalizados deben constar de un JSON válido y definir al menos una acción de gestión de dispositivos personalizada.

Para obtener más información sobre las funciones de gestión de dispositivos personalizadas, incluido un ejemplo del formato JSON necesario, consulte [extensiones personalizadas de gestión de dispositivos](../../devices/device_mgmt/custom_actions.html){: new_window}.

### Adición de un paquete de gestión de dispositivos personalizados

Los paquetes de gestión de dispositivos personalizados se pueden añadir mediante el panel de control de {{site.data.keyword.iot_short_notm}} o mediante la API.

Para añadir un paquete de gestión de dispositivos personalizados mediante el panel de control de {{site.data.keyword.iot_short_notm}}:

1. En el panel de control de {{site.data.keyword.iot_short_notm}}, pulse **Valores** en la barra de navegación.
2. Pulse **Paquetes de gestión de dispositivos personalizados**.
3. Pulse el botón **Añadir paquete**.
4. Seleccione el archivo de paquete y pulse **Abrir**.

Para añadir un paquete de gestión de dispositivos personalizados mediante la API, consulte la documentación de la API de [{{site.data.keyword.iot_short_notm}} ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

## Blockchain
{: #blockchain}

{{site.data.keyword.iot_short_notm}} con blockchain permite a los dispositivos de IoT proporcionar datos a transacciones de blockchain, lo que almacena los datos en el libro mayor inmutable de blockchain y los utiliza en reglas empresariales de contratos inteligentes. {{site.data.keyword.iot_short_notm}} correlaciona datos de dispositivo en el formato de datos que necesita el contrato inteligente de blockchain y los pasa a un tejido de blockchain para almacenarlos en el libro mayor de blockchain.

### Operaciones soportadas para Blockchain
- Desencadenar actualizaciones de contratos inteligentes con sucesos de dispositivo.
- Ejecutar la lógica empresarial de contratos inteligentes para actualizar el estado de libro mayor con datos de sucesos de dispositivos.
- Supervisar el blockchain, las transacciones y el estado del libro mayor con la IU de supervisión.

### Configuración para Blockchain

La integración de blockchain de {{site.data.keyword.iot_short_notm}} es una oferta de servicios que no está activada de forma predeterminada en {{site.data.keyword.iot_short_notm}}. Para activar la característica en la organización, lleve a cabo los pasos siguientes:
 1. Desde el panel de instrumentos de {{site.data.keyword.iot_short_notm}}, seleccione **Extensiones**.
 2. En la página **Extensiones**, pulse **Añadir ampliación**.
 3. Pulse **Añadir** junto a la extensión de Blockchain.
 4. En el mosaico de Blockchain, pulse **Configuración**.
 3. En la sección **Activar Blockchain**, pulse el enlace **Más información** para ir a la [página de ofertas de servicios Blockchain de IoT ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.ibm.com/internet-of-things/iot-news/announcements/private-blockchain/){: new_window}.
 4. Pulse **Inicio rápido del proyecto blockchain** para rellenar y enviar el formulario de *Exploración del potencial de IoT y Blockchain*.  
 5. Una vez aprobada la solicitud, IBM se pondrá en contacto con usted para activar la integración de blockchain para su organización.
 6. Vuelva al panel de control de {{site.data.keyword.iot_short_notm}} para que la organización finalice la configuración siguiendo los pasos de [integración de blockchain de {{site.data.keyword.iot_short_notm}}](../../bl_blockchain_integration.html).

<!-- ## The Weather Company
{: #weathercompany}

The Weather Company extension combines weather data with your existing {{site.data.keyword.iot_short_notm}} devices. Weather data from The Weather Company appears in the device details view if an update location request has been made by using the API, or if the device has already set its location by using a device management message.

**Note:** Only managed devices can set their own locations. All unmanaged devices must have their locations set manually by using the API. For more information on setting a device location, see [Update Location requests](../../devices/device_mgmt/index.html#update-location).

### REST APIs for The Weather Company
To access the REST API for The Weather Company, see the
Device Location Weather section in the [{{site.data.keyword.iot_short_notm}} HTTP REST API ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window} documentation.

### Weather Data

To view the weather data retrieved for a device location, find the device in the **Devices** pane and click it. In the detailed device view scroll down to the **Extensions** section. The following weather data is listed:

- Current weather.
- Current temperature.
- Predicted maximum and minimum temperature.
- Relative humidity.
- Pressure.
- Visibility.
- Wind speed.
- Wind direction.
- Latitude.
- Longitude.
-->

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->

## Correo electrónico
{: #email}

Se pueden añadir usuarios a {{site.data.keyword.iot_short_notm}} mediante invitaciones de correo electrónico. Para obtener información, consulte [Gestión de acceso de usuario](../../add_users.html).

Para utilizar la característica de invitación de correo electrónico, debe configurarse una extensión de correo electrónico para utilizar el servicio en línea SendGrid o el servicio SMTP (Simple Mail Transfer Protocol). La extensión también puede utilizar la aplicación SendGrid {{site.data.keyword.Bluemix_notm}}.

### Servicio en línea SendGrid 

Para configurar la extensión de correo electrónico para utilizar con el servicio en línea SendGrid, siga estos pasos: 

1. Recupere la clave de API autorizada de su cuenta en línea de SendGrid.
2. En el panel de control de {{site.data.keyword.iot_short_notm}}, pulse **Extensiones** en la barra de navegación.
3. En la sección **Correo electrónico**, pulse **Configurar**.
4. Seleccione **SendGrid con clave de API**
5. Escriba el nombre y la dirección de correo electrónico del administrador del sitio y la clave de API autorizada.

### Servicio SMTP

Para configurar la extensión de correo electrónico para utilizar con un servicio SMTP, siga estos pasos:

1. En el panel de control de {{site.data.keyword.iot_short_notm}}, pulse **Extensiones** en la barra de navegación.
2. En la sección **Correo electrónico**, pulse **Configurar**.
3. Seleccione **SMTP**.
4. Especifique los detalles de configuración de su servicio SMTP.

### Aplicación SendGrid {{site.data.keyword.Bluemix_notm}}

Para configurar la extensión de correo electrónico para utilizar con la aplicación SendGrid {{site.data.keyword.Bluemix_notm}}, siga estos pasos:

1. Cree una aplicación ficticia y vincúlela al servicio SendGrid.  
Para recuperar las credenciales de configuración, añada y vincule el servicio SendGrid a una app ficticia.

 1. Desde el panel de control de {{site.data.keyword.Bluemix_notm}}, pulse **Crear servicio**.
 2. Seleccione el servicio SendGrid desde el catálogo y pulse **Crear**.
 3. Desde el panel de control de {{site.data.keyword.Bluemix_notm}}, añada la aplicación {{site.data.keyword.sdk4nodefull}}.
 4. Pulse la aplicación {{site.data.keyword.sdk4nodefull}} desde el panel de control de {{site.data.keyword.Bluemix_notm}} y pulse **Enlazar un servicio o API**.
 5. Seleccione el servicio SendGrid y pulse **Añadir**.
 6. Se debe volver a transferir ahora la aplicación {{site.data.keyword.sdk4nodefull}}.
2. Prepárese para configurar el servicio de {{site.data.keyword.iot_short_notm}}.  
El {{site.data.keyword.iot_short_notm}} puede configurarse mediante el panel de control de {{site.data.keyword.iot_short_notm}} o utilizando la API de {{site.data.keyword.iot_short_notm}}.  
 1. Pulse la aplicación {{site.data.keyword.sdk4nodefull}} desde el panel de control de {{site.data.keyword.Bluemix_notm}}.
 2. Pulse **Variables de entorno** desde la barra de navegación.
 3. Copie el JSON mostrado a un archivo de texto temporal.  
 El archivo JSON debe tener el siguiente formato:
```
{
  "name": "SendGridServiceName",
  "label": "user-provided",
  "credentials": {
    "password": "xxx",
    "hostname": "smtp.sendgrid.net",
    "username": "username"
  }
}
```
3. Añada los datos de configuración a la organización de {{site.data.keyword.iot_short_notm}}.
 1. Abra el panel de control de {{site.data.keyword.iot_short_notm}}.
 2. Pulse **Extensiones** desde la barra de navegación.
 3. Pulse **Configurar** en el icono **Correo electrónico**.
 4. Seleccione **SendGrid con nombre de usuario**.
 5. Especifique los datos de configuración del archivo de texto temporal.
 6. Pulse **Terminado**.
