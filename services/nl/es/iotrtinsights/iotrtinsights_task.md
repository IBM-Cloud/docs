---

copyright:
  años: 2015,2016

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Conexión y visualización de los dispositivos
{: #iotrtinsights_task}
*Última actualización: 11 de febrero de 2016*

{{site.data.keyword.iotrtinsights_short}} utiliza {{site.data.keyword.iot_short}} para el acceso de los dispositivos y la recuperación de datos. Los dispositivos que se conectan a {{site.data.keyword.iot_short}} se conectarán automáticamente a {{site.data.keyword.iotrtinsights_short}}.
{: shortdesc}

Si está conectando un nuevo tipo de dispositivo, debe configurar también el esquema de mensaje para correlacionar los puntos de datos del dispositivo, establecer las unidades y denominar el tipo de dispositivo. Si los dispositivos son de un tipo de dispositivo ya configurado, sus datos se mostrarán automáticamente en el panel de control.

## Añadir un nuevo dispositivo
{: #iotrtinsights_subtask}

Para añadir un nuevo dispositivo:  
La adición de un nuevo dispositivo es un proceso de dos pasos. En primer lugar, añada el dispositivo a {{site.data.keyword.iot_short}} y, a continuación, configure cómo consume y muestra los datos de dispositivos {{site.data.keyword.iotrtinsights_short}}.
1. Añadir dispositivos a {{site.data.keyword.iot_short}}.
> **Consejo:** Si ha desplegado la aplicación telefónica Internet of Things, ya se ha añadido un dispositivo iotphone al *iot-phone-iotf-service* {{site.data.keyword.iot_short}} y puede omitir este paso.  

  Para añadir dispositivos nuevos a su {{site.data.keyword.iot_short}}, consulte la documentación de [{{site.data.keyword.iot_full}}](https://www.ng.bluemix.net/docs/services/IoT/index.html) y las fórmulas de conexión de dispositivos de [{{site.data.keyword.iot_short}}](https://developer.ibm.com/recipes/?post_type=tutorials&s=IoTF).
2. Configurar el dispositivo en {{site.data.keyword.iotrtinsights_short}}.  
  1. Inicie la sesión en la consola de {{site.data.keyword.iotrtinsights_short}} como un usuario administrador.
  9. Vaya a **Dispositivos > Examinar dispositivos** y verifique que se lista el dispositivo recién añadido.
  > **Consejo:** La lista de dispositivos se renueva desde el origen de datos una vez por minuto. Pulse **Renovar** para actualizar la lista de dispositivos inmediatamente.
  3. Vaya a **Dispositivos > Gestionar esquemas** y pulse **Añadir nuevo esquema de mensaje**.  
  4. Especifique un nombre para el esquema de mensaje, como por ejemplo:
  `Nuevo esquema de mensaje`.
  5. Pulse **Enlazar nuevo origen de datos** y seleccione el origen de datos y el tipo de dispositivo que se corresponde con su instancia y dispositivo de {{site.data.keyword.iot_short}}. Opcionalmente, especifique un nombre de suceso para recopilar datos solo para dicho suceso, o deje el comodín `+` para recopilar todos los sucesos. Obtenga más información sobre cómo identificar los tipos de sucesos para su dispositivo [aquí](#identify-datapoints "Identificar puntos de datos.").  
  >**Importante:** Cada esquema de mensaje debe tener una combinación exclusiva de orígenes de datos, tipos de dispositivos y nombres de sucesos. Para crear más de un esquema para una combinación de tipos de dispositivos y un origen de datos específicos, especifique un nombre de suceso exclusivo para cada esquema de mensaje en lugar de utilizar el comodín `+` predeterminado.   
  6. Añadir uno o varios puntos de datos que desee incluir en los paneles de control del dispositivo.
    Puede seleccionar puntos de datos desde un dispositivo conectado, o añadir puntos de datos manualmente. Los puntos de datos disponibles se definen en la carga útil de los mensajes enviados por un dispositivo. Para obtener más información sobre el formato de carga útil de {{site.data.keyword.iot_short}}, consulte el tema [Carga útil de mensaje](https://docs.internetofthings.ibmcloud.com/messaging/payload.html "Carga útil de mensaje.") en la documentación de {{site.data.keyword.iot_short}}.   
    > **Consejo:** Puede crear manualmente puntos de datos virtuales que modifiquen o combinen puntos de datos existentes que sean de tipo entero o flotante. Por ejemplo, si la temperatura del punto de datos de dispositivo devuelve un valor de temperatura en Fahrenheit, y desea utilizar Celsius en su lugar, puede crear un punto de datos virtual *temp_c* con la siguiente función *temp_c=(temp-32)/1.8*. A continuación, puede utilizar el punto de datos *temp_c* virtual en lugar del punto de datos *temp* en tiempo real en las condiciones de la regla. En los paneles de control, los puntos de datos virtuales se identifican mediante un subrayado discontinuo.    

  <dl>
  <dt>Seleccionar desde un dispositivo conectado</dt>
  <dd>
  <ol>
    <li>Pulse **Seleccionar desde el dispositivo conectado**.</li>  
    <li>En el diálogo Añadir puntos de datos, seleccione uno o varios puntos de datos a añadir y, a continuación, pulse **Aceptar**.</li>   
    <li>Los puntos de datos seleccionados se añaden con la descripción establecida en el nombre del punto de datos. Pulse el punto de datos de la lista para editarlo, y añada atributos adicionales como, por ejemplo, el tipo de sensor, el tipo de datos y el número de posiciones decimales.</li>
  </ol>
  </dd>
  <dt>Añadir manualmente</dt>
  <p><b>Consejo:</b> Para crear una [estructura de punto de datos anidado](schemas.html), añada en primer lugar un punto de datos que tenga el tipo de datos Padre. En la tabla de puntos de datos, podrá, a continuación, pulsar el icono ![Añadir hijo.](images/add_child.png "Añadir hijo") para añadir uno o varios puntos de datos hijos.</p>
  <dd>
  <ol>
    <li>Pulse **Añadir manualmente**.</li>
    <li>Seleccione **Punto de datos en tiempo real** o **Punto de datos virtual**</br></li>
    <li>Defina la siguiente información del punto de datos:
    <ul>  
     <li> Punto de datos - El identificador del punto de datos que ha ubicado [en el {{site.data.keyword.iot_short}} panel de control](#identify-datapoints "Identificar puntos de datos."). Por ejemplo:  
   `id`, `ts`, `lat`  </li>
     <li>Descripción - Una descripción breve del punto de datos. Esta descripción se utiliza al visualizar los puntos de datos en paneles de control.</li>
     <li>Función del punto de datos virtual - Añada uno o varios componentes para definir una función válida. Puede utilizar puntos de datos, valores numéricos y operadores matemáticos como por ejemplo +, -, \*, /, (, y ) para crear la función. </li>
     <li>Tipo de datos - El tipo de datos del punto de datos:  
   `Cadena`, `Entero`, `Flotante` o `Padre`.</li>
     <li>Tipo de sensor - Opcionalmente, seleccione cómo interpretar el punto de datos en los paneles de control. Según el tipo y la combinación del tipo de sensor, pueden estar disponibles opciones de visualización adicionales para los widgets del panel de control. Para obtener más información sobre los tipos de sensores y las opciones de visualización, consulte [Widgets de panel de control](dashboards.html#dashboard-widget "Widgets de panel de control").</li>
     <li>Icono Punto de datos - Opcionalmente, seleccione un icono que represente el punto de datos en los widgets del panel de control.</li>
     <li>Valor mínimo/valor máximo - Solo opcional, entero y flotante: Si se especifica un valor máximo y mínimo, los datos de dispositivos se pueden visualizar como un medidor en los paneles de control.</li>
     <li>Unidad de datos - Opcional: La unidad de datos del punto de datos. Por ejemplo:  
     `C`, `Mph`  </li>
     <li> Posiciones decimales - Solo opcional, flotante: El número de decimales a incluir en los datos del dispositivo.</li>
    </ul>
    </li>
  </ol>
  </dd>
  </dl>
   8. Pulse **Aceptar** para crear el esquema de mensaje.
   9. Vaya a **Dispositivos > Examinar dispositivos** y pulse el dispositivo recién añadido para verificar que se muestran datos de dispositivos en tiempo real y que los puntos de datos estén correlacionados correctamente.

## Identificación de puntos de datos y sucesos en el panel de control de {{site.data.keyword.iot_short}}.
{: #identify-datapoints}
   Los puntos de datos y los tipos de sucesos para un dispositivo se pueden encontrar en el panel de control de {{site.data.keyword.iot_short}}.
   >**Consejo:** Si está utilizando la aplicación telefónica Internet of Things como su dispositivo IoT, puede utilizar el suceso sensorData y los siguientes puntos de datos para configurar el esquema de mensajes:
   >- d.id - ID de dispositivo
   >- d.ts - Indicación de fecha y hora
   >- d.lat - Latitud
   >- d.lng - Longitud
   >- d.ax - Aceleración X
   >- d.ay - Aceleración Y
   >- d.az - Aceleración Z
   >- d.oa - Movimiento Alfa
   >- d.ob - Movimiento Beta
   >- d.og - Movimiento Gamma
   >Donde d.*punto de datos* indica que el punto de datos está anidado en un punto de datos d de tipo de padre en la carga útil del mensaje.

   1. Desde el panel de control de Bluemix, pulse el mosaico Internet of Things.  
   >**Nota:** Si está utilizando la aplicación telefónica Internet of Things, pulse el mosaico *iot-phone-iotf-service*.  
   2. Pulse **Iniciar panel de control** para abrir el panel de control de {{site.data.keyword.iot_short}}.
   3. Vaya a la página **Dispositivos**.
   4. Pulse el dispositivo para abrir la página de detalles del dispositivo.
     Desplácese hacia abajo a la sección **Información de sensor** para ver una lista de los sucesos disponibles y de los puntos de datos para el dispositivo. Esta información es necesaria al configurar el dispositivo en {{site.data.keyword.iotrtinsights_short}}.
