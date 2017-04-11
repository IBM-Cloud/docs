---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Desarrollo de dispositivos en {{site.data.keyword.iot_short_notm}}
{: #device_dev_index}

Un dispositivo es cualquier cosa que tenga una conexión a internet y que tenga datos que enviar o recibir de la nube. Puede utilizar dispositivos para enviar información de sucesos, como lecturas del sensor, a la nube y para aceptar mandatos de aplicaciones de la nube.

Los dispositivos publican datos en {{site.data.keyword.iot_short_notm}} mediante sucesos. El dispositivo controla el contenido del suceso y asigna un nombre a cada suceso que se envía. Cuando {{site.data.keyword.iot_short_notm}} recibe un suceso de un dispositivo, las credenciales de la conexión en la que se ha recibido el suceso se utilizan para determinar el dispositivo desde el que se ha enviado el suceso. Esta arquitectura impide que un dispositivo suplante a otro.

Para obtener más información sobre los conceptos clave, incluidos dispositivos, consulte [Acerca de Watson IoT Platform](https://console.ng.bluemix.net/docs/services/IoT/iotplatform_overview.html#watsoniotplatform_importantconcepts).


# Conexión del dispositivo a {{site.data.keyword.iot_short_notm}}
{: #device_connect}
Puede conectar su dispositivo a {{site.data.keyword.iot_short_notm}} mediante los protocolos HTTP o MQTT. Utilice HTTP si desea configurar un caso de ejemplo de tipo solicitud-respuesta, como por ejemplo cuando alguien realiza una compra y recibe un acuse de recibo. Utilice MQTT si desea configurar un caso de ejemplo de sucesos, como por ejemplo cuando alguien llama a un timbre y hace que se active una alerta en un dispositivo móvil.

Un dispositivo debe estar registrado con una organización para que se pueda conectar a {{site.data.keyword.iot_full}}. Para establecer una conexión segura con {{site.data.keyword.iot_short_notm}}, debe registrarse para una cuenta de Bluemix y crear su propia organización de {{site.data.keyword.iot_short_notm}}. Luego puede registrar su dispositivo utilizando el ID de esta organización. Los dispositivos registrados se identifican a sí mismos ante {{site.data.keyword.iot_short_notm}} con un identificador de dispositivo exclusivo, por ejemplo la dirección MAC, y una señal de autenticación que solo se acepta para dicho dispositivo. Después de haberse conectado de forma segura, utilice Bluemix para crear sus propias aplicaciones. Intente utilizar Node-RED para conectar sus aplicaciones entre sí.

Si desea conectar el dispositivo sin registrarlo, por ejemplo para ejecutar una prueba de concepto, puede hacerlo utilizando el ID de organización especial `QuickStart`. `QuickStart` es una instancia pública de recinto de seguridad de {{site.data.keyword.iot_short_notm}} que se ejecuta en la nube. Si no necesita establecer una conexión segura, puede utilizar `QuickStart` para probar la conectividad del dispositivo y experimentar con {{site.data.keyword.iot_short_notm}}. Cuando haya terminado de experimentar, vuelva a conectar el dispositivo de forma segura a la instancia específica de su propio ID de organización mediante TLS y su señal de autenticación.

Para obtener más información sobre cómo conectar el dispositivo a {{site.data.keyword.iot_short_notm}} mediante el protocolo HTTP, consulte [API REST HTTP para dispositivos](https://console.ng.bluemix.net/docs/services/IoT/devices/api.html).
Para obtener más información sobre cómo conectar el dispositivo a {{site.data.keyword.iot_short_notm}} mediante el protocolo MQTT, consulte [Conectividad MQTT para dispositivos](https://console.ng.bluemix.net/docs/services/IoT/devices/mqtt.html).

# Cómo empezar a desarrollar dispositivos
{: #get_started}
Si tiene un dispositivo que ya está listo para {{site.data.keyword.iot_short_notm}}, simplemente puede comenzar a utilizarlo.

Si el dispositivo no está listo, consulte las recetas disponibles en [developerWorks](https://developer.ibm.com/recipes/). Examine las recetas existentes para ver si hay alguna para su dispositivo y utilícela como ayuda para empezar a desarrollar. Incluso puede publicar sus propias recetas si lo desea.

Si no encuentra una receta para su dispositivo en concreto, IBM ofrece varias guías de programación y API que puede utilizar para empezar. Estas guías contienen bibliotecas de cliente, ejemplos e información que le puede ayudar a crear y desarrollar código para integrar y conectar sus dispositivos y aplicaciones a {{site.data.keyword.iot_short_notm}}. Actualmente están disponibles guías para los siguientes lenguajes de programación:

- Java
- Node.js
- Embedded C
- ARM mBed C++
- Python
- C#
- Node-RED

Para obtener más información y ver enlaces con las guías de programación disponibles, consulte [Bibliotecas de cliente para el desarrollo de {{site.data.keyword.iot_short_notm}}](../iot_platform_client_lib.html).

Si no encuentra una guía de programación de {{site.data.keyword.iot_short_notm}} adecuada, puede escribir su propio programa y utilizar el protocolo MQTT o HTTP para conectar el dispositivo a {{site.data.keyword.iot_short_notm}}.

MQTT es un estándar abierto gestionado por la organización de estándares OASIS y reconocido internacionalmente por ISO. Para obtener más información, consulte [OASIS Message Queuing Telemetry Transport ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=mqtt){: new_window}.

Dispone de una gran variedad de bibliotecas de cliente MQTT para diversos sistemas, incluidos los siguientes entornos:
- http://www.eclipse.org/paho/
- https://github.com/mqtt/mqtt.github.io/wiki/software?id=software

Para obtener más información sobre MQTT, consulte [Mensajería de MQTT](https://console.ng.bluemix.net/docs/services/IoT/reference/mqtt/index.html?pos=3).
