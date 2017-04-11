---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Mensajería de MQTT
{: #ref-mqtt}

MQTT es el protocolo primario que utilizan los dispositivos y las aplicaciones para comunicarse con el {{site.data.keyword.iot_full}}. MQTT es un protocolo de transporte de mensajería de publicación y suscripción diseñado para el intercambio eficiente de datos en tiempo real entre el sensor y los dispositivos móviles.
{:shortdesc}

MQTT se ejecuta sobre TCP/IP, y mientras sea posible codificar directamente a TCP/IP, también puede elegir utilizar una biblioteca que maneje los detalles del protocolo MQTT. Hay disponible una amplia gama de bibliotecas de cliente de MQTT. IBM contribuye al desarrollo y al soporte de varias bibliotecas de cliente, incluidas aquellas que están disponibles en los sitios siguientes:

- [Wiki de la comunidad MQTT ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/mqtt/mqtt.github.io/wiki){: new_window}
- [Proyecto Eclipse Paho ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](http://eclipse.org/paho/){: new_window}

## Soporte de versión
{: #version-support}
Para obtener información sobre las versiones de MQTT que reciben soporte de {{site.data.keyword.iot_short_notm}}, consulte [Estándares y requisitos](../standards_and_requirements.html#mqtt).

## Clientes de la aplicación, dispositivo y pasarela
{: #device-app-clients}

En {{site.data.keyword.iot_short_notm}}, las clases primarias de cosas son dispositivos y aplicaciones. Una pasarela es una subclase de dispositivo.

El cliente MQTT se identifica a sí mismo ante el servicio {{site.data.keyword.iot_short_notm}} como una clase de cosas. La clase de cosas determina las posibilidades del cliente cuando está conectado. La clase de cosas también determina el mecanismo para la autenticación de clientes.

Las aplicaciones y los dispositivos funcionan con distintos espacios de temas de MQTT.  Los dispositivos funcionan dentro de un espacio de tema del ámbito del dispositivo, mientras que las aplicaciones tienen acceso completo al espacio de temas para toda una organización. Para obtener más información consulte los siguientes temas:

- [Mensajería MQTT para dispositivos](../../devices/mqtt.html)
- [Mensajería MQTT para aplicaciones](../../applications/mqtt.html)
- [Mensajería MQTT para pasarelas](../../gateways/mqtt.html)

### Mensajes retenidos
{{site.data.keyword.iot_short_notm}} proporciona soporte limitado para la característica de mensajes retenidos de la mensajería MQTT. Si el distintivo de mensaje retenido está establecido en true en un mensaje MQTT que se envía desde un dispositivo, pasarela o aplicación a {{site.data.keyword.iot_short_notm}}, el mensaje se gestiona como un mensaje no retenido. Las organizaciones de {{site.data.keyword.iot_short_notm}} no tienen autorización para publicar mensajes retenidos. El servicio {{site.data.keyword.iot_short_notm}} modifica el distintivo de mensaje retenido cuando está establecido en true y procesa el mensaje como si el distintivo de mensaje retenido estuviera establecido en false.

## Niveles de calidad de servicio
{: #qos-levels}

El protocolo MQTT proporciona tres calidades de servicio para la entrega de mensajes entre clientes y servidores: "como máximo una vez", "como mínimo una vez" y "exactamente una vez".
Mientras que puede enviar sucesos y mandatos mediante cualquier calidad de nivel de servicio, deberá considerar cuidadosamente cuál es el nivel de servicio que mejor se ajusta a sus necesidades. La calidad de nivel de servicio '2' no es siempre una mejor opción que el nivel '0'.

### Como máximo una vez (QoS0)

La calidad de nivel de servicio "como máximo una vez" (QoS0) es la modalidad de transferencia más rápida y a veces se denomina "fire and forget". El mensaje se entrega como máximo una vez, o puede no entregarse en absoluto. La entrega a través de la red no se confirma y el mensaje no se almacena. El mensaje puede perderse si el cliente se desconecta o si falla el servidor.

El protocolo MQTT no necesita servidores para reenviar publicaciones a la calidad de nivel de servicio '0' a un cliente. Si el cliente está desconectado en el momento de que el servidor reciba la publicación, ésta se podría descartar, en función de la implementación del servidor.

**Consejo:** Al enviar datos en tiempo real en un intervalo, utilice la calidad de nivel de servicio 0. Si falta un único mensaje, no importa porque se enviará poco tiempo después otro mensaje que contiene datos más recientes. En este caso de ejemplo, el coste adicional de utilizar una calidad superior de servicio no produce ningún beneficio tangible.

### Como mínimo una vez (QoS1)

Con la calidad de nivel de servicio 1 (QoS1), el mensaje siempre se entregará al menos una vez. Si se produce una anomalía antes de que el remitente reciba un acuse de recibo, un mensaje puede entregarse varias veces. El mensaje debe estar almacenado de forma local en el remitente hasta que éste reciba confirmación de que el mensaje ha sido publicado por el receptor. El mensaje se almacena por si este debe volverse a enviar.

### Exactamente una vez (QoS2)

La calidad de nivel de servicio 2 "exactamente una vez" (QoS2) es la modalidad más segura, pero más lenta, de transferencia. El mensaje siempre se entrega exactamente una vez y también debe estar almacenado de forma local en el remitente, hasta que el remitente reciba confirmación de que el mensaje lo ha publicado el receptor. El mensaje se almacena por si este debe volverse a enviar. Con la calidad de nivel de servicio 2, se utiliza una secuencia de conformidad de conexión y de reconocimiento más sofisticada que para el nivel 1 para asegurarse de que los mensajes no estén duplicados.

**Consejo:** Al enviar mandatos, si desea confirmación de que sólo se accionará el mandato especificado, y de que se accionará sólo una vez, utilice la calidad de nivel de servicio 2. Este es un ejemplo de cuándo pueden resultar beneficiosas las sobrecargas adicionales de nivel 2 sobre otros niveles.

## Almacenamientos intermedios de suscripción y sesión limpia
{: #subscription-buffers-and-clean-session}

Cada suscripción desde un dispositivo o aplicación tiene asignada un almacenamiento intermedio de 5000 mensajes.  El almacenamiento intermedio permite que cada aplicación o dispositivo esté detrás de los datos en tiempo real que procesa, y para también construir un proceso de un máximo de 5000 mensajes pendientes para cada suscripción que ha realizado. Cuando el almacenamiento intermedio está lleno, se descartarán los mensajes más antiguos cuando se reciba un mensaje nuevo.

Utilice la opción de sesión limpia de MQTT para acceder al almacenamiento intermedio de suscripción. Cuando la sesión limpia se establezca en false, el suscriptor recibirá mensajes del almacenamiento intermedio. Cuando la sesión limpia se establezca en true, el almacenamiento intermedio se restablecerá.

**Nota:** Se aplicará el límite de almacenamiento intermedio de suscripción, independientemente de la calidad del valor de servicio utilizado. Es posible que un mensaje enviado al nivel 1 o 2 no se entregue a una aplicación que no puede mantenerse al día con la tasa de mensajes para la suscripción que ha realizado.

## Limitaciones de carga útil de mensajes
{: #message-payload}

El {{site.data.keyword.iot_short_notm}} da soporte al envío y recepción de mensajes en cualquier formato permitido por el estándar MQTT. MQTT es neutro desde el punto de vista de los datos, por lo que es posible enviar imágenes, textos en cualquier codificación, datos cifrados, y prácticamente cualquier tipo de datos en formato binario. Sin embargo, existen ciertas limitaciones para casos de uso específicos.   

También hay limitaciones de tamaño para la carga útil del mensaje en {{site.data.keyword.iot_short_notm}}.

### Restricciones de formato de la carga útil de mensaje

La carga útil de mensaje puede contener cualquier serie válida; sin embargo, los formatos JSON ("json"), texto ("text") y binario ("bin") son los que se utilizan con más frecuencia que otros tipos de formatos.

En la tabla siguiente se describen restricciones de carga útil de mensaje para distintos tipos de formato:

Formato de carga útil  | Directrices para casos de uso específicos
--------- | ----------  
JSON | JSON es el formato estándar para {{site.data.keyword.iot_short_notm}}. Si tiene la intención de utilizar los paneles de instrumentos, las placas y las tarjetas y las analíticas incorporadas de {{site.data.keyword.iot_short_notm}}, asegúrese de que el formato de carga útil de mensaje se ajusta al texto JSON bien formado.
Texto | Utilice la codificación de caracteres de UTF-8 válida.
Binario | Sin restricciones.


### Tamaño máximo de carga útil de mensaje

**Importante:** El tamaño de carga útil máximo en {{site.data.keyword.iot_short_notm}} es 131072 bytes. Los mensajes con una carga útil mayor que el límite se rechazarán. El cliente de conexión también está desconectado, y aparece un mensaje en los registros de diagnóstico, tal como se describe en el siguiente ejemplo de mensaje de dispositivo:

`Conexión cerrada desde x.x.x.x. El tamaño de mensaje es demasiado grande para este terminal.`

## Intervalo de estado activo de MQTT
{: #mqtt-keep-alive}

El de intervalo de estado activo de MQTT, que se mide en segundos, define el tiempo máximo que puede pasar sin comunicación entre el cliente y el intermediario. El cliente MQTT debe asegurarse de que, en ausencia de cualquier otra comunicación con el intermediario, se envíe un paquete PINGREQ. El intervalo de estado de actividad permite al cliente y al intermediario detectar que la red ha fallado, lo que da lugar a la interrupción de la conexión, sin necesidad de esperar a que se alcance el periodo de tiempo de espera excedido de TCP/IP.

Si los clientes MQTT de {{site.data.keyword.iot_short_notm}} utilizan suscripciones compartidas, el valor del intervalo de estado de actividad sólo se puede establecer entre 1 y 3600 segundos. Si se solicita el valor 0 o un valor mayor que 3600, el intermediario de {{site.data.keyword.iot_short_notm}} establece el intervalo de estado de actividad en 3600 segundos.
