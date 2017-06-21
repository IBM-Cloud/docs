---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conexión de dispositivos
{: #iotplatform_task}

Antes de empezar a recibir datos desde los dispositivos de IoT, debe conectarlos a {{site.data.keyword.iot_full}}. La conexión de un dispositivo a {{site.data.keyword.iot_short_notm}} implica el registro del dispositivo con {{site.data.keyword.iot_short_notm}} y, a continuación, el uso de la información de registro para configurar el dispositivo para conectarlo a {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Antes de empezar
{: #byb}

Antes de iniciar el proceso de conexión, debe asegurarse de que los dispositivos cumplan los siguientes requisitos para comunicarse con {{site.data.keyword.iot_short_notm}}:

- El dispositivo debe poder comunicarse mediante protocolos HTTP o MQTT.
- Los mensajes del dispositivo deben ajustarse a los requisitos de carga útil de mensajes de {{site.data.keyword.iot_short_notm}}.

Para obtener más información, consulte [Desarrollo de dispositivos en Watson IoT Platform](https://console.ng.bluemix.net/docs/services/IoT/devices/device_dev_index.html).

Complete los pasos siguientes para conectar el dispositivo a {{site.data.keyword.iot_short_notm}}.

## Paso 1: Registro del dispositivo con {{site.data.keyword.iot_short_notm}}  
{: #iotplatform_subtask1}

El registro de un dispositivo implica la clasificación del dispositivo como un tipo de dispositivo, lo que le da un nombre al dispositivo, y proporciona una información de dispositivo. A continuación, proporcione una señal de conexión o acepte una señal generada por {{site.data.keyword.iot_short_notm}}.

Puede añadir dispositivos de uno en uno desde el panel de instrumentos de {{site.data.keyword.iot_short_notm}} o puede utilizar la [ API de {{site.data.keyword.iot_short_notm}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Bulk_Configuration){: new_window} para añadir uno o varios dispositivos a la vez.

Para añadir un dispositivo desde el panel de instrumentos de {{site.data.keyword.iot_short_notm}}:

1. Pulse sobre el mosaico del servicio de {{site.data.keyword.iot_short_notm}} en el panel de instrumentos de {{site.data.keyword.Bluemix}}.

2. En la página de servicio, pulse **Iniciar** para iniciar la administración de la organización de {{site.data.keyword.iot_short_notm}}.

  Se abre la consola web de {{site.data.keyword.iot_short_notm}} en un nuevo separador del navegador con el siguiente URL:

 ```
 https://org_id.internetofthings.ibmcloud.com/dashboard/#/overview
 ```

    Donde *org_id* es el ID de [la organización de {{site.data.keyword.iot_short_notm}}](iotplatform_overview.html#organizations){: new_window}.

3. En el panel de instrumentos Visión general, desde el panel del menú, seleccione **Dispositivos** y, a continuación, pulse **Añadir dispositivo**.
5. Seleccione o cree un tipo de dispositivo para el dispositivo que está añadiendo.  
Cada dispositivo conectado al {{site.data.keyword.iot_short_notm}} debe estar asociado con un tipo de dispositivo. Los tipos de dispositivos son grupos de dispositivos que comparten características comunes.  
Al añadir el primer dispositivo a la organización de {{site.data.keyword.iot_short_notm}}, no habrá disponibles tipos de dispositivos en el menú **Tipo de dispositivo**. Primero debe crear un tipo de dispositivo:
 1. Pulse **Crear tipo de dispositivo**.
 2. Especifique un nombre de tipo de dispositivo como, por ejemplo, `my_device_type` y una descripción para el tipo de dispositivo.   
 **Importante:** el nombre del tipo de dispositivo no debe tener más de 36 caracteres y sólo puede contener:
 <ul>
  <li>Caracteres alfanuméricos (a-z, A-Z, 0-9)</li>
  <li>Guiones (-)</li>
  <li>Signos de subrayado (&lowbar;)</li>
  <li>Puntos (.)</li>
  </ul>
 3. Opcional: Especifique los atributos y metadatos de tipo de dispositivo.    
 **Consejo:** Puede añadir y editar atributos y metadatos más tarde.
 4. Pulse **Crear** para añadir el nuevo tipo de dispositivo.
10. Pulse **Siguiente** para empezar el proceso de adición de su dispositivo con el tipo de dispositivo seleccionado.
11. Especifique un ID de dispositivo, como por ejemplo `my_first_device`.  
Este ID de dispositivo se utiliza para identificar el dispositivo en el panel de instrumentos de {{site.data.keyword.iot_short_notm}} y también un parámetro obligatorio para conectar el dispositivo a {{site.data.keyword.iot_short_notm}}.  
**Importante:** el ID de dispositivo no debe tener más de 36 caracteres y sólo puede contener:
 <ul>
 <li>Caracteres alfanuméricos (a-z, A-Z, 0-9)</li>
 <li>Guiones (-).</li>
 <li>Signos de subrayado (&lowbar;)</li>
 <li>Puntos (.)</li>  
 </ul>
 **Consejo:** para los dispositivos conectados a la red, el ID de dispositivo podría ser, por ejemplo, la dirección MAC del dispositivo sin dos puntos de separación.  
12. Opcional: Pulse **Campos adicionales** para añadir información de dispositivo, como por ejemplo el número de serie, el fabricante, el modelo, etc.  
 **Consejo:** Puede añadir y editar esta información más tarde.
12. Opcional: Especifique los metadatos JSON de dispositivo.  
 **Consejo:** Puede añadir y editar metadatos de dispositivo más tarde.
13. Pulse **Siguiente** para completar la adición de su dispositivo.
14. Verifique que la información de resumen sea correcta y, a continuación, pulse **Añadir** para añadir la conexión.  
**Consejo:** Tiene la opción de aceptar una señal de autenticación generada automáticamente o de proporcionar una señal de autenticación usted mismo.  
Si decide crear su propia señal, asegúrese de que tenga entre 8 y 36 caracteres de longitud y que solo contenga caracteres alfanuméricos y los siguientes caracteres especiales:
 - Guión (-)
 - Signo de subrayado (&lowbar;)
 - Signo de exclamación (!)
 - Carácter &
 - Signo de arroba (@)
 - Signo de interrogación (?)
 - Asterisco (\*)
 - Signo más (+)
 - Punto (.)
 - Paréntesis derecho e izquierdo .  

 **Importante:** la señal no debe contener secuencias de caracteres repetidos, palabras de diccionario, nombres de usuario ni otras secuencias predefinidas.
15. En la página de información de dispositivos, copie y guarde la siguiente información de dispositivos:  
 - ID de organización, como por ejemplo `tubo8x`
 - Tipo de dispositivo, como por ejemplo `my_device_type`
 - ID de dispositivo, como por ejemplo `my_first_device`
 - Método de autenticación, como por ejemplo `señal`
 - Señal de autenticación, como por ejemplo `PtBVriRqIg4uh)_- Kl`  
  **Consejo:** necesitará los valores de ID de organización, Señal de autenticación, Tipo de dispositivo e ID de dispositivo para configurar el dispositivo para conectarse a {{site.data.keyword.iot_short_notm}}.  

Enhorabuena, ha registrado el dispositivo. Ahora, puede configurar el dispositivo para conectarse a {{site.data.keyword.iot_short_notm}}

## Paso 2: Conexión de los dispositivos a {{site.data.keyword.iot_short_notm}}
{: #iotplatform_subtask2}

Después de registrar un dispositivo con {{site.data.keyword.iot_short_notm}}, puede utilizar la información de registro para conectar el dispositivo y empezar a recibir datos de dispositivo.

{{site.data.keyword.iot_short_notm}} da soporte a muchos tipos de dispositivo. El proceso básico para conectar un dispositivo normalmente incluye los pasos siguientes:
- Configure el dispositivo para la mensajería de MQTT y utilice ID de organización, Señal de autenticación, Tipo de dispositivo e ID de dispositivo para autenticarse.  
- Envíe mensajes de dispositivo a la organización de {{site.data.keyword.iot_short_notm}} utilizando el protocolo de MQTT.

**Consejo:** Muchas recetas de conexión están disponibles para los dispositivos utilizados de forma común. Para obtener una lista de recetas, consulte las [Recetas de conexión de dispositivos ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){: new_window} disponibles en IBM.com.

Se necesita la siguiente información al conectar el dispositivo:
- URL: *org_id*.messaging.internetofthings.ibmcloud.com  
Donde *org_id* es el ID de la organización de {{site.data.keyword.iot_short_notm}}.
- Puerto:
 - 1883
 - 8883 (cifrado)
 - 443 (websockets)
- Identificador de dispositivo: d:*org_id*:*device_type*:*device_id*  
Esta combinación de parámetros identifica de forma exclusiva el dispositivo.
- Nombre de usuario: use-token-auth  
Este valor indica que está utilizando la autorización de señales.
- Contraseña: *Señal de autenticación*  
Este valor es la señal exclusiva que ha definido o que se ha asignado al dispositivo al registrarlo.
- Formato del tema del suceso: iot-2/evt/*event_id*/fmt/*format_string*  
 Donde el *event_id* especifica el nombre del suceso que se muestra en {{site.data.keyword.iot_short_notm}}, y *format_string* es el formato del suceso, como por ejemplo JSON.
- Formato de mensaje:
   
 {{site.data.keyword.iot_short_notm}} JSON da soporte a varios formatos, como JSON y texto.

Para obtener más información sobre cómo conectar su dispositivo, consulte [Conectividad de MQTT para dispositivos](devices/mqtt.html) en la documentación técnica.

La documentación de la API [Administración de la organización ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window} también contiene la información necesaria.

## Recetas sobre la conexión de dispositivos

En las siguientes recetas se describe el flujo completo que se utiliza para registrar y conectar dispositivos a Watson IoT Platform.

- [Cómo registrar dispositivos en IBM Watson IoT Platform ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/how-to-register-devices-in-ibm-iot-foundation/){: new_window}

- [Conexión de Raspberry Pi como dispositivo a Watson IoT mediante Node-RED ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/deploy-watson-iot-node-on-raspberry-pi/){: new_window}

- [Conexión de un dispositivo Arduino Uno a IBM Watson IoT Platform ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/connect-an-arduino-uno-device-to-the-ibm-internet-of-things-foundation/){: new_window}

- [Conexión de Sense HAT Watson IoT mediante Node-RED ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/connecting-a-sense-hat-to-watson-iot-using-node-red/){: new_window}

- [Conexión de Raspberry Pi con Windows IoT Core como dispositivo a Watson IoT Platform ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-with-windows-iot-core-as-a-device-to-watson-iot-using-node-red/){: new_window}
