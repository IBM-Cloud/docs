---

copyright:

years: 2015, 2017

lastupdated: "2017-03-16"


---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Conexión de pasarelas
{: #IoT_connectGateway}

Antes de empezar a recibir datos de dispositivos conectados a las pasarelas, debe conectar la pasarela a {{site.data.keyword.iot_full}}. La conexión de una pasarela a {{site.data.keyword.iot_short_notm}} implica crear un tipo de dispositivo de pasarela y registrar la pasarela con {{site.data.keyword.iot_short_notm}}. A continuación, puede utilizar la información de registro para conectar la pasarela a {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

Las pasarelas son una clase especializada de dispositivos de {{site.data.keyword.iot_short_notm}}. Las pasarelas sirven como puntos de acceso al {{site.data.keyword.iot_short_notm}} para otros dispositivos.


## Antes de empezar
{: #Prerequisites}

Los dispositivos de pasarela tienen permisos adicionales cuando se comparan con dispositivos normales y pueden realizar las funciones siguientes:
- Registrar nuevos dispositivos en {{site.data.keyword.iot_short_notm}}
- Enviar y recibir datos de su propio sensor como un dispositivo conectado directamente,
- Enviar y recibir datos en nombre de los dispositivos
- Ejecutar un agente de gestión de dispositivos, para que se pueda gestionar, y también gestionar los dispositivos conectados.  
Para la información de desarrollador de pasarela, consulte [Conectividad de MQTT para pasarelas](mqtt.html).

También puede utilizar pasarelas para realizar analíticas de extremo en los datos que están enviando los dispositivos de pasarela. Para obtener más información, consulte [Analíticas de extremo](../edge_analytics.html) e [Instalación de Edge Analytics Agent](#edge).

## Paso 1: Registro de la pasarela con {{site.data.keyword.iot_short_notm}}  
{: #register_gateway}

El registro de una pasarela implica la clasificación del dispositivo como un tipo de pasarela, lo que da a la pasarela un nombre, y proporciona información de pasarela. A continuación, proporcione una señal de conexión o acepte una señal generada por {{site.data.keyword.iot_short_notm}}.


**Consejo:** Puede añadir pasarelas de una en una desde el panel de instrumentos de {{site.data.keyword.iot_short_notm}}, o puede utilizar la API de [API de Administración de organización ![Icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Bulk_Configuration/post_bulk_devices_add){: new_window} para añadir una o varias pasarelas a la vez.

Para añadir una pasarela desde el panel de instrumentos de {{site.data.keyword.iot_short_notm}}:

1. En el panel de instrumentos de {{site.data.keyword.iot_short_notm}}, seleccione **Dispositivos**.
2. Pulse **Añadir dispositivo**.
3. Seleccione o cree un tipo de dispositivo para el dispositivo que está añadiendo.  
Cada dispositivo conectado al {{site.data.keyword.iot_short_notm}} debe estar asociado con un tipo de dispositivo. Los tipos de dispositivos son grupos de dispositivos que comparten características comunes.  
 1. Pulse **Crear tipo de dispositivo** y, a continuación, **Crear tipo de pasarela**.
 2. Especifique un nombre de tipo de dispositivo como, por ejemplo, `my_gateway_type` y una descripción para el tipo de pasarela.   
 **Importante:** el nombre del tipo de dispositivo no debe tener más de 36 caracteres y sólo puede contener:
 <ul>
  <li>Caracteres alfanuméricos (a-z, A-Z, 0-9)</li>
  <li>Guiones (-)</li>
  <li>Signos de subrayado (&lowbar;)</li>
  <li>Puntos (.)</li>
  </ul>3. Opcional: Especifique los metadatos y los atributos de tipo de pasarela.    
 **Consejo:** Puede añadir y editar atributos y metadatos más tarde.
 4. Pulse **Crear** para añadir el nuevo tipo de pasarela.
10. Pulse **Siguiente** para comenzar el proceso de adición del dispositivo de pasarela con el tipo de pasarela seleccionado.
11. Especifique un ID de dispositivo como por ejemplo `my_gateway_device`.  
El ID de dispositivo se utiliza para identificar el dispositivo de pasarela en el panel de instrumentos de {{site.data.keyword.iot_short_notm}} y también es un parámetro obligatorio para conectar el dispositivo de pasarela a {{site.data.keyword.iot_short_notm}}.  
**Importante:** el ID de dispositivo no debe tener más de 36 caracteres y sólo puede contener:
 <ul>
 <li>Caracteres alfanuméricos (a-z, A-Z, 0-9)</li>
 <li>Guiones (-).</li>
 <li>Signos de subrayado (&lowbar;)</li>
 <li>Puntos (.)</li>  
 </ul>
 **Consejo:** para los dispositivos conectados a la red, el ID de dispositivo podría ser, por ejemplo, la dirección MAC del dispositivo sin dos puntos de separación.  
12. Opcional: Pulse **Campos adicionales** para añadir información de dispositivo de pasarela, como por ejemplo el número de serie, el fabricante, el modelo, etc.  
 **Consejo:** Puede añadir y editar esta información más tarde.
12. Opcional: Especifique los metadatos JSON de dispositivo.  
 **Consejo:** Puede añadir y editar metadatos de dispositivo más tarde.
13. Pulse **Siguiente** para completar la adición del dispositivo de pasarela.
14. Verifique que la información de resumen sea correcta y, a continuación, pulse **Añadir** para añadir el dispositivo de pasarela.  
**Consejo:** Tiene la opción de aceptar una señal de autenticación generada automáticamente o de proporcionar una señal de autenticación usted mismo. Si decide crear su propia señal, asegúrese de que se encuentre entre los 8 y 36 caracteres, que contenga una mezcla de letras en mayúscula y minúscula, números, y guión, subrayado o punto. La señal no debe contener secuencias de caracteres repetidos, palabras de diccionario, nombres de usuario ni otras secuencias predefinidas.
15. En la página de información de dispositivos, copie y guarde la siguiente información de dispositivos:  
 - ID de organización, como por ejemplo `tubo8x`
 - Tipo de dispositivo, como por ejemplo `my_gateway_type`
 - ID de dispositivo. **Consejo:** Para dispositivos conectados a la red, esto podría ser, por ejemplo, la dirección MAC sin dos puntos de separación.
 - Método de autenticación, como por ejemplo `señal`
 - Señal de autenticación, como por ejemplo `PtBVriRqIg4uh)_- Kl`  
  **Consejo:** necesitará los valores de ID de organización, Señal de autenticación, Tipo de dispositivo e ID de dispositivo para configurar el dispositivo para conectarse a {{site.data.keyword.iot_short_notm}}.  

Enhorabuena, ha registrado el dispositivo de pasarela. Ahora puede configurar el dispositivo de pasarela para conectarse a {{site.data.keyword.iot_short_notm}}

Consulte la receta [Cómo registrar pasarelas en IBM Watson IoT Platform ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/how-to-register-gateways-in-ibm-watson-iot-platform/){:new_window} para ver instrucciones paso a paso sobre cómo registrar una pasarela.

## Paso 2: Conexión de la pasarela a {{site.data.keyword.iot_short_notm}}
{: #connect_gateway}

Después de registrar una pasarela con {{site.data.keyword.iot_short_notm}}, utilice la información de registro para conectar la pasarela a {{site.data.keyword.iot_short_notm}} y empezar a recibir datos de dispositivos conectados a la pasarela.

Para obtener información sobre la conexión de la pasarela a {{site.data.keyword.iot_short_notm}}, consulte [Conectividad de MQTT para pasarelas](mqtt.html).

**Consejo:** Hay un rango de recetas disponibles para conectar dispositivos a {{site.data.keyword.iot_short_notm}}. Para obtener una lista de recetas, consulte las [Recetas de conexión de dispositivos ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window} disponibles en IBM.com.


## Paso 3: Conexión de dispositivos a través de la pasarela
{: #gateway_devices}

Los dispositivos que están conectados a la pasarela se añaden automáticamente a {{site.data.keyword.iot_short_notm}} cuando la pasarela publica mensajes desde el dispositivo. Tanto el tipo de dispositivo como el propio dispositivo se crean automáticamente cuando la pasarela publica un mensaje para una combinación de tipo de dispositivo e ID de dispositivo que todavía no existe.

Para obtener información sobre el registro automático de dispositivos y la publicación y recepción de datos para dispositivos conectados, consulte [Conectividad de MQTT para pasarelas](mqtt.html).


Cuando un dispositivo se ha conectado satisfactoriamente a la pasarela, se muestra en el panel de instrumentos de su organización de {{site.data.keyword.iot_short_notm}}.

Consulte la receta [Conexión de Raspberry Pi como pasarela a Watson IoT ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-as-a-gateway-to-watson-iot-using-node-red/){:new_window} para ver el flujo detallado y una descripción.

**Nota:** En el panel de instrumentos de {{site.data.keyword.iot_short_notm}}, los dispositivos y las pasarelas que se conectan directamente al {{site.data.keyword.iot_short_notm}} muestran un icono de estado para indicar que están conectados. El panel de instrumentos muestra dispositivos que se conectan indirectamente a través de una pasarela como desconectados, ya que no saben la conectividad de dispositivos a la pasarela.


## Instalación de Edge Analytics Agent
{: #edge}

Edge Analytics Agent (EAA) es un componente de software creado en la parte superior de un motor de streaming, que está optimizado para llevar a cabo operaciones de analíticas de extremo en una pasarela subiendo y gestionando las reglas de analíticas de extremo desde el panel de instrumentos de {{site.data.keyword.iot_short_notm}}. Para obtener más información sobre analíticas de extremo, consulte [Edge Analytics](../edge_analytics.html).

### Instalación de EAA
{: #eaa_install}

Para instalar EAA en la pasarela:
1. En el panel de control de {{site.data.keyword.iot_short}}, vaya a **Reglas**.
2. Pulse **Descargar Edge Agent** para ir a la [Comunidad de IBM Edge Analytics ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true){:new_window}.
3. Vaya a la sección **Archivos** y descargue los directorios comprimidos adecuados para el tipo de pasarela.  
La solución Edge Analytics está disponible como SDK para dispositivos que dan soporte a Java o como DSLink para dispositivos de pasarela Cisco.
4. Para obtener información sobre cómo instalar y configurar el componente de software EAA en la pasarela, consulte la siguiente información:
 - SDK  
 Consulte el PDF, el archivo readme y los enlaces de vídeo disponibles en la comunidad.  
 Receta [Edge Recipe for SDK - Iniciación (SDK) ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/getting-started-with-the-ibm-edge-analytics-sdk-in-watson-iot-platform/){:new_window}.
 - DSLink  
 Receta [Iniciación a Edge Analytics en Watson IoT Platform ![Icono de enlace externo](../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/?post_type=pnext_tutorial&p=19472){:new_window}.

### Valores de configuración de EAA
{: #eaa_configuration}

Puede utilizar el archivo config.properties de EAA para establecer parámetros de configuración de software básicos.

Para actualizar la configuración de EAA:
1. En el sistema de pasarela en el que se está ejecutando el EAA, localice el archivo config.properties de EAA.  
Por ejemplo:
`../dglux-server/dslinks/ibm-watson-iot-edge-analytics-dslink-java-0.0.1/config.properties`
2. Antes de empezar a editar los valores, realice una copia de seguridad del archivo.
3. Abra el archivo config.properties para su edición.
4. Edite los parámetros de configuración para su entorno:
 <dl>
 <dt>DataDirectSendEnable</dt>
 <dd>BOOLEAN (true|false)</br>
 TRUE (valor predeterminado): Envíe todos los datos a {{site.data.keyword.iot_short_notm}}.</br>
 FALSE: Envíe únicamente datos a {{site.data.keyword.iot_short_notm}} si las reglas se establecen en el motor. </dd>
 <dt>MonitorInterval</dt>
 <dd>INTEGER (milisegundos)</br>
 El tiempo en milisegundos antes de que se envíe un nuevo mensaje de supervisión a {{site.data.keyword.iot_short_notm}}. </br>
 Establezca un valor pequeño para informar de las métricas de supervisión más a menudo. Establezca un valor grande para tener información de supervisión más detallada en {{site.data.keyword.iot_short_notm}}. </br>
 DEFAULT: 60000    </br>
 RECOMMENDED RANGE: [1000, 360000]</dd>
 <dt>MonitorLogDesample</dt>
 <dd>INTEGER  </br>
 La frecuencia de eliminación de rastreo entre el número de mensajes de supervisión enviados a {{site.data.keyword.iot_short_notm}} en comparación con los mensajes especificados en el registro local. Por ejemplo, si `MonitorLogDesample` se establece en 10, sólo se grabará una entrada de registro local por cada diez mensajes que se envíen a {{site.data.keyword.iot_short_notm}}. </br>Un gran número mantiene en tamaño pequeño el registro local. Un número pequeño proporciona un registro local más detallado.</br>
 DEFAULT: 10</br>
 RECOMMENDED RANGE: [1, 100]</dd>
 <dt>MemoryAlertThreshold</dt>
 <dd>INTEGER (Megabytes)</br>
 El umbral de memoria de almacenamiento dinámico de la JVM libre en el que se envía un mensaje de registro de aviso de memoria al registro de diagnóstico de {{site.data.keyword.iot_short_notm}}. La alerta está controlada por la supervisión. </br>Un valor pequeño reduce el número de mensajes de alerta enviados a {{site.data.keyword.iot_short_notm}}. Un valor grande le proporciona un aviso anterior si el servidor de EAA se está ejecutando en problemas de memoria.</br>**Consejo:** Puede utilizar las reglas de [analíticas de nube](../cloud_analytics.html) para configurar acciones de alerta como notificaciones de correo electrónico para que le avisen de problemas de memoria. Para obtener información sobre las propiedades disponibles que puede utilizar para crear reglas, consulte [Métricas de diagnóstico de Edge Analytics Agent](../edge_analytics.html#eaa_metrics).</br>
  DEFAULT: 10</br>
 RECOMMENDED RANGE: [10 o 5 % de la memoria total, 200]</dd>
 </dl>
5. Guardar el archivo editado y, a continuación, reiniciar EAA.

Archivo config.properties de EAA de ejemplo
```
#######################################################################
# Engine Parameters
#######################################################################
# DataDirectSendEnable
#                    - BOOLEAN(true|false) Establézcalo en true para reenviar todos
#                      los datos; Establézcalo en false para inhabilitar el envío directo de datos
#                      a IOTP cuando no haya reglas establecidas en el
#                      motor.
#                      DEFAULT: true
#######################################################################
DataDirectSendEnable=true

#######################################################################
# Monitoring Parameters
#######################################################################
# MonitorInterval    - INTEGER Intervalo de tiempo en milisegundos antes de que se genere
#                      un nuevo mensaje de supervisión. Establézcalo en un valor
#                      pequeño para informar a las métricas del supervisor con más
#                      frecuencia. Establézcalo en un valor grande para tener información
#                      de supervisión más detallada en IoTP.
#                      DEFAULT: 60000    RECOMMEND: [1000, 360000]
# MonitorLogDesample - INTEGER La frecuencia de eliminación de rastreo del número de
#                      mensajes de supervisión enviados a IOTP frente al registro local,
#                      p. ej. el número de N mensajes de supervisión, donde
#                      EAA sólo daría como resultado uno al registro de Información para
#                      cada N mensajes. Establézcalo en grande para mantener el tamaño
#                      del registro pequeño. Establézcalo en pequeño para tener información
#                      de supervisión detallada en el registro local.
#                      DEFAULT: 10       RECOMMEND: [1, 100]
# MemoryAlertThreshold
#                    - INTEGER La memoria de almacenamiento dinámico de JVM libre en megabytes bajo
#                      la que se generaría un mensaje de registro y se enviaría al registro
#                      de diagnóstico de IOTP. La alerta la controla la
#                      supervisión. Establézcalo en pequeño para eliminar mensajes de alerta
#                      innecesarios en IoTP. Establézcalo en grande para recibir la primera alerta
#                      cuando el sistema esté a punto de colgarse. Se recomienda establecer en
#                      Min(Max(10 MB, 5 % de la memoria total), 200 MB).
#                      DEFAULT: 10       RECOMMEND: [10, 200]
#######################################################################

MonitorInterval=60000
MonitorLogDesample=10
MemoryAlertThreshold=10
```
