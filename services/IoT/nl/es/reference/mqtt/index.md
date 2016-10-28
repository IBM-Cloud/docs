---

copyright:
  years: 2015, 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Mensajería de MQTT
{: #ref-mqtt}
Última actualización: 13 de septiembre de 2016
{: .last-updated}

MQTT es el protocolo primario que utilizan los dispositivos y las aplicaciones para comunicarse con el {{site.data.keyword.iot_full}}. MQTT es un protocolo de transporte de mensajería de publicación y suscripción diseñado para el intercambio eficiente de datos en tiempo real entre el sensor y los dispositivos móviles.
{:shortdesc}

MQTT se ejecuta sobre TCP/IP, y mientras sea posible codificar directamente a TCP/IP, también puede elegir utilizar una biblioteca que maneje los detalles del protocolo MQTT. Hay disponible una amplia gama de bibliotecas de cliente de MQTT. IBM contribuye al desarrollo y al soporte de varias bibliotecas de cliente, incluidas aquellas que están disponibles en los sitios siguientes:

- [Wiki de comunidad de MQTT](https://github.com/mqtt/mqtt.github.io/wiki)
- [Proyecto de Eclipse Paho](http://eclipse.org/paho/)

## Soporte de versión
{: #version-support}

{{site.data.keyword.iot_short_notm}} da soporte a las versiones siguientes del protocolo de mensajería MQTT:

Versión de MQTT | Desviaciones | Notas
--- | --- | ---
[3.1.1](https://www.oasis-open.org/standards#mqttv3.1.1) (recomendado) | Los mensajes conservados no están soportados, por ejemplo, suscripciones compartidas. | <ul><li>Estándar OASIS.<li>Estándar ISO (ISO/IEC PRF 20922) <li>Interoperatividad mejorada entre varios clientes y servidores debido a una definición más precisa del protocolo comparado con V3.1.   <li>La longitud máxima del identificador de cliente de MQTT (ClientId) se ha aumentado a 256 desde el límite de 23 caracteres que ha impuesto V3.1. </br>El servicio de {{site.data.keyword.iot_short_notm}} normalmente requiere ID de cliente más grandes (ClientId). </br>Los ID de cliente grandes están soportados independientemente de la versión del protocolo MQTT, aunque algunas bibliotecas de clientes de V3.1 comprueban la longitud del valor ClientId y aplican el límite de 23 caracteres.</ul>
3.1 | - | MQTT V3.1 es la versión del protocolo más en uso hoy día.

{{site.data.keyword.iot_short_notm}} da soporte a cualquier contenido permitido por el estándar MQTT. MQTT es neutro desde el punto de vista de los datos, por lo que es posible enviar imágenes, textos en cualquier codificación, datos cifrados, y prácticamente cualquier tipo de datos en formato binario. Para obtener más información sobre el estándar MQTT, consulte los siguientes recursos:
- [MQTT.org](http://mqtt.org/)
- [HiveMQ: Introducción a MQTT](http://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt)

## Clientes de la aplicación, dispositivo y pasarela
{: #device-app-clients}

En {{site.data.keyword.iot_short_notm}}, las clases primarias de cosas son dispositivos y aplicaciones. Una pasarela es una subclase de dispositivo.

La clase de cosas que el cliente de MQTT se identifica en sí mismo en el servicio a medida que determina las capacidades del cliente al conectarse. La clase de cosas también determina el mecanismo para la autenticación de clientes.

Las aplicaciones y los dispositivos también funcionan con distintos espacios de temas de MQTT. Los dispositivos funcionan dentro de un espacio de tema del ámbito del dispositivo, mientras que las aplicaciones tienen acceso completo al espacio de temas para toda una organización. Para obtener más información consulte los siguientes temas:

- [Dispositivos](../../devices/mqtt.html)
- [Aplicaciones](../../applications/mqtt.html)
- [Pasarelas](../../gateways/mqtt.html)

## Niveles de calidad de servicio
{: #qos-levels}

El protocolo MQTT proporciona tres calidades de servicio para la entrega de mensajes entre clientes y servidores: "como máximo una vez", "como mínimo una vez" y "exactamente una vez".
Mientras que puede enviar sucesos y mandatos mediante cualquier calidad de nivel de servicio, deberá considerar cuidadosamente si el nivel de servicio correcto se ajusta a sus necesidades. La calidad de nivel de servicio 2 no es siempre una mejor opción que el nivel cero.

### Como máximo una vez (QoS0)

La calidad de nivel de servicio "como máximo una vez" (QoS0) es la modalidad de transferencia más rápida y a veces se denomina "fire and forget". El mensaje se entrega como máximo una vez, o puede no entregarse en absoluto. La entrega a través de la red no se confirma y el mensaje no se almacena. El mensaje puede perderse si el cliente se desconecta o si falla el servidor.

El protocolo MQTT no necesita servidores para reenviar publicaciones a la calidad de nivel de servicio cero a un cliente. Si el cliente está desconectado en el momento de que el servidor reciba la publicación, ésta se podría descartar, en función de la implementación del servidor.

**Consejo:** Al enviar datos en tiempo real en un intervalo, utilice la calidad de nivel de servicio 0. Si falta un único mensaje, no importa porque se enviará poco tiempo después otro mensaje que contiene datos más recientes. En este caso de ejemplo, el coste adicional de utilizar una calidad superior de servicio no produce ningún beneficio tangible.

### Como mínimo una vez (QoS1)

Con la calidad de nivel de servicio 1 (QoS1), el mensaje siempre se entregará al menos una vez. Si se produce una anomalía antes de que el remitente reciba un acuse de recibo, un mensaje puede entregarse varias veces. El mensaje debe estar almacenado de forma local en el remitente hasta que éste reciba confirmación de que el mensaje ha sido publicado por el receptor. El mensaje se almacena por si este debe volverse a enviar.

### Exactamente una vez (QoS2)

La calidad de nivel de servicio "exactamente una vez" (QoS2) es la modalidad más lenta y más segura de transferencia. El mensaje siempre se entrega exactamente una vez y también debe estar almacenado de forma local en el remitente, hasta que el remitente reciba confirmación de que el mensaje lo ha publicado el receptor. El mensaje se almacena por si este debe volverse a enviar. Con la calidad de nivel de servicio 2, se utiliza una secuencia de conformidad de conexión y de reconocimiento más sofisticada que para el nivel 1 para asegurarse de que los mensajes no estén duplicados.

**Consejo:** Al enviar mandatos, si desea confirmación de que sólo se accionará el mandato especificado, y de que se accionará sólo una vez, utilice la calidad de nivel de servicio 2. Este es un ejemplo de cuándo pueden resultar beneficiosas las sobrecargas adicionales de nivel 2 sobre otros niveles.

## Almacenamientos intermedios de suscripción y sesión limpia
{: #subscription-buffers-and-clean-session}

Cada suscripción desde un dispositivo o aplicación tiene asignada un almacenamiento intermedio de 5000 mensajes. El almacenamiento intermedio permite que cada aplicación o dispositivo esté detrás de los datos en tiempo real que procesa, y para también construir un proceso de un máximo de 5000 mensajes pendientes para cada suscripción que ha realizado. Cuando el almacenamiento intermedio está lleno, se descartarán los mensajes más antiguos cuando se reciba un mensaje nuevo.

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
