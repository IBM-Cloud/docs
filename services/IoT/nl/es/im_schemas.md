---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Crear esquemas de tipo de dispositivo
{: #iotrtinsights_task}

Para utilizar características de {{site.data.keyword.iot_short}} como, por ejemplo, reglas y acciones, debe crear un esquema para correlacionar las propiedades de dispositivos a nombres de propiedades sencillos para el usuario, para establecer las unidades de datos para las propiedades, y para especificar un tipo de mensaje para utilizar con el esquema.
{: shortdesc}

**Importante:** Los esquemas son necesarios para utilizar reglas y acciones. Para obtener información, consulte [Cloud Analytics](cloud_analytics.html#rules).

**Importante:** Las características de análisis se fusionan desde el servicio de {{site.data.keyword.iotrtinsights_full}}. Si la organización de {{site.data.keyword.iot_short_notm}} se utiliza como un origen de datos para una instancia existente de {{site.data.keyword.iotrtinsights_short}}, Cloud y Edge Analytics no se habilitarán hasta que se hayan migrado las instancias existentes de {{site.data.keyword.iotrtinsights_short}}. Siga utilizando el panel de control de {{site.data.keyword.iotrtinsights_short}} para sus necesidades de análisis hasta que se haya completado la migración. Para obtener más información, consulte el [Blog de IBM Watson IoT Platform ![icono de enlace externo](../../icons/launch-glyph.svg)](https://developer.ibm.com/iotplatform/2016/04/28/iot-real-time-insights-and-watson-iot-platform-a-match-made-in-heaven/){: new_window} en IBM developerWorks y los paneles de control de instancias existentes de {{site.data.keyword.iotrtinsights_short}}.  

## Adición de un esquema de dispositivo
{: #add_schema}

Para añadir un esquema:  
1. Vaya a **Dispositivos > Gestionar esquemas** y pulse **Añadir esquema**.  
2. Seleccione un tipo de dispositivo para asociarlo con este esquema de mensaje. **Importante:** Sólo se puede definir un esquema para un tipo de dispositivo.

3. Añada una o varias propiedades.  
    Puede seleccionar propiedades desde un dispositivo conectado, crear propiedades virtuales que modifiquen o combinen propiedades existentes, o añadir propiedades manualmente.  

    **Consejo:** Las propiedades disponibles se definen en la carga útil de los mensajes enviados por un dispositivo. Para obtener información sobre el formato de carga útil de {{site.data.keyword.iot_short}}, consulte el tema [Carga útil del mensaje](reference/mqtt/index.html#message-payloadl "Carga útil del mensaje.").   
  <dl>
  <dt>Añadir una propiedad manualmente</dt>
  <p><b>Consejo:</b> Para crear una estructura de propiedad anidada, añada en primer lugar una propiedad que tenga el tipo de datos Padre. En la tabla de propiedades, podrá pulsar ![Añadir icono hijo.](images/add_child.png "Añadir hijo") para añadir una o varias propiedades hijo.</p>
  <dd>
  <ol>
    <li>Seleccione el separador **Manual**.</li>
    <li>Defina los siguientes detalles de propiedades:
    <ul>  
      <li>Nombre: Un nombre descriptivo para la propiedad utilizada en los paneles de instrumentos, menús y asistentes de {{site.data.keyword.iot_short}}.</li>
      <li>Tipo de datos: El tipo de datos de la propiedad:  
   `Serie`, `Entero`, `Flotante` o `Padre`.</li>
   <!--<li>Event - A specific event to collect data for. Leave blank to collect for all events.</li>-->
   <li>Propiedad: El identificador de la propiedad, como por ejemplo:  
 `temp` o `speed`  </br> Para obtener información sobre cómo identificar las propiedades desde los mensajes de dispositivo, consulte [Identificación de propiedades para los dispositivos](#identify-datapoints "Identificar propiedades.").</li>
  <li>Unidad de datos - Opcional: La unidad de datos de la propiedad. Por ejemplo:  
     `C` o `Mph`  </li>
     <li> Posiciones decimales - Opcional, sólo flotante: El número de decimales a incluir en los datos de dispositivo.</li>
    </ul>
    </li>
    <li>Pulse **Finalizar** para crear la propiedad.</li>
  </ol>
  </dd>
  <dt>Crear una propiedad virtual</dt>
  <dd> Por ejemplo, si la propiedad de dispositivo temp vuelve a un valor de temperatura en Fahrenheit, y desea utilizar Celsius en su lugar, puede crear una propiedad virtual *temp_c* que tenga la siguiente función *temp_c=(temp-32)/1.8*. A continuación, puede utilizar la propiedad virtual *temp_c* en lugar de la propiedad en tiempo real *temp* en las condiciones de reglas.  
  Para crear una propiedad virtual:
  <ol>
    <li>Seleccione el separador **Propiedad virtual**.</li>  
    <li>Defina los siguientes detalles de propiedades:
    <ul>
    <li>Nombre: Un nombre descriptivo para la propiedad utilizada en los paneles de instrumentos, menús y asistentes de {{site.data.keyword.iot_short}}.</li>
    <li>Tipo de datos: El tipo de datos de la propiedad:  
 `Flotante` o `Entero`.</li>
 <li>Propiedad: Un identificador de propiedad para la propiedad virtual. Por ejemplo:  
`temp_virt`</li>
    <li>Cálculo: Añada uno o varios componentes para definir una función válida. También puede utilizar propiedades, valores numéricos y operadores matemáticos como +, -, \*, /, (, y ).  
    Pulse **Avanzado** para ver un conjunto de fórmulas que puede utilizar con series de puntos de datos en dispositivos de extremo. Para obtener más información sobre las fórmulas avanzadas, consulte [Cálculos avanzados para propiedades virtuales de extremo](im_vir_calculations.html).  
    **Importante:** las condiciones de regla que comparan propiedades en función de fórmulas avanzadas no reciben soporte.</li>
    <li>Unidad de datos - Opcional: La unidad de datos de la propiedad. Por ejemplo: `C` o `Mph`</li>
    <li> Posiciones decimales - Opcional, sólo flotante: El número de decimales a incluir en los datos de dispositivo.</li>
   </ul>
   </li>
   <li>Pulse **Finalizar** para crear la propiedad.</li>
  </ol>
  </dd>
  <dt>Seleccionar propiedades de un dispositivo conectado</dt>
  <dd>
  <ol>
    <li>Seleccione el separador **From Connected**.</li>  
    <li>Seleccione una o varias propiedades para añadirlas al esquema. Estas propiedades pueden editarse más adelante para establecer atributos como, por ejemplo, el nombre y la unidad de datos.  
<!--**Important:** Each property must be unique for a schema. If you select multiple occurrences of the same property for different events, only one of the selected properties is added to the schema.</li>-->
  <li>Pulse **Aceptar** para crear las propiedades.</li>
  </ol>
  </dd>
    <dd>Se añadirán las propiedades seleccionadas y la descripción se establecerá en el nombre de la propiedad. Pulse la propiedad en la lista para editarla, y añada atributos adicionales, como por ejemplo tipo de sensor, tipo de datos y número de posiciones decimales.</dd>
  </dl>
8. Pulse **Finalizar** para crear el esquema de mensajes.

## Identificación de las propiedades para los dispositivos.
{: #identify-datapoints}
   Las propiedades para un dispositivo se pueden encontrar en el panel de instrumentos de {{site.data.keyword.iot_short}}.

1. En el panel de instrumentos de {{site.data.keyword.iot_short}}, vaya a **Dispositivos**.
2. Pulse un dispositivo para abrir una página que muestra detalles para el dispositivo.
3. Desplácese hacia abajo a la sección **Información de sensor** para ver una lista de las propiedades disponibles para un dispositivo conectado.
