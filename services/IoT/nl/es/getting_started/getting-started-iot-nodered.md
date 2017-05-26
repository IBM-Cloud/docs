---

copyright:
  years: 2017
lastupdated: "2017-04-24"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciación al iniciador de {{site.data.keyword.iot_short_notm}}
{: #gettingstartedtemplate}
<!-- Provide an appropriate ID above -->

Comience a trabajar con {{site.data.keyword.iot_full}} utilizando el proyecto GitHub Iniciador de {{site.data.keyword.iot_short_notm}}. Mediante el iniciador, puede simular rápidamente un dispositivo, crear tarjetas, generar datos y empezar a analizar y a visualizar datos en el panel de control de {{site.data.keyword.iot_short_notm}}.   
{:shortdesc}

## Visión general
{: #overview}  

El iniciador despliega y conecta automáticamente estos servicios: 
<dl>
<dt>**{{site.data.keyword.iot_short_notm}}**</dt>
<dd>Un servicio web IoT que incluye gestión de pasarelas, gestión de dispositivos y acceso a aplicaciones. Mediante {{site.data.keyword.iot_short_notm}}, puede recopilar datos de dispositivo conectados y ejecutar análisis en datos en tiempo real desde la organización.
</dd>
<dt>**{{site.data.keyword.sdk4nodefull}}**</dt>
<dd>El entorno de ejecución en el que se ejecuta Node-RED. </br>Para obtener más información, consulte la [documentación del iniciador de {{site.data.keyword.sdk4nodefull}}](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html).</dd>
<dd>Node-RED es una herramienta para la conexión conjunta de dispositivos de hardware, API y servicios en línea de una interesante nueva forma. Puede utilizar Node-RED para crear un termostato simulado que envíe datos simulados a su servicio de
{{site.data.keyword.iot_short_notm}}. Puede crear tarjetas para mostrar datos en tiempo real en el panel de control de
{{site.data.keyword.iot_short_notm}}. </br>Para obtener más información, consulte la
[Documentación de Node-RED](https://console.ng.bluemix.net/docs/starters/Node-RED/nodered.html#nodered).</dd>
<dt>**{{site.data.keyword.cloudantfull}}**</dt><dd>La base de datos en la que Node-RED almacena los metadatos. </dd>
</dl>

## Antes de empezar
{: #byb}  

- Cuentas necesarias  
Antes de empezar, necesita una [cuenta de IBM Bluemix](https://bluemix.net/registration).

- Navegación  
Para moverse fácilmente entre las tareas del proceso siguiente, abra el panel de control de {{site.data.keyword.Bluemix_notm}}, el panel de control de {{site.data.keyword.iot_short_notm}} y la aplicación Node-RED en distintos separadores del navegador. 
<dl>
<dt>*Panel de control de {{site.data.keyword.Bluemix_notm}}*</dt>
<dd>Consulte el estado del despliegue, lea la documentación e inicie los paneles de control. </dd>
<dt>*Panel de control de {{site.data.keyword.iot_short_notm}}*</dt>
<dd>Defina tipos de dispositivo, registre dispositivos, supervise los datos entrantes del sensor, cree tarjetas de visualización de datos y consulte visualizaciones de datos en tiempo real. </dd>
<dt>*Node-RED*</dt>
<dd>Configure y ejecute el flujo del simulador de dispositivo y trabaje con otros flujos para procesar los datos procedentes de {{site.data.keyword.iot_short_notm}}.</dd>
</dl>

## Paso 1: Despliegue del iniciador de {{site.data.keyword.iot_short_notm}}
{: #deployStarter}

Siga estos pasos para desplegar la aplicación de ejemplo del iniciador: 

1. Despliegue la aplicación del iniciador. 
 1. Pulse <a href="https://bluemix.net/devops/setup/deploy?repository=https://github.com/ibm-watson-iot/iot-platform-bluemix-starter"><img src="https://bluemix.net/devops/graphics/create_toolchain_button.png" height=25></a> para crear una nueva cadena de herramientas de entrega continua en Bluemix:  (a través de entrega continua)  
 **Consejo:** si prefiere realizar el despliegue desde la línea de mandatos, puede [buscar el iniciador de {{site.data.keyword.iot_short_notm}}](https://github.com/ibm-watson-iot/iot-platform-bluemix-starter) en la organización de IBM Watson IoT en GitHub.
 2. Cuando se le solicite, inicie una sesión en IBM Bluemix.
 3. Si hace falta, seleccione la organización de Bluemix en la que desea desplegar la aplicación del iniciador. 
 4. Conserve el nombre de la cadena de herramientas o actualícelo si es necesario. Se utiliza como nombre de app predeterminado y la raíz del URL de la app: `<app-name>.mybluemix.net`
 5. Pulse **Crear**.  
**Consejo:** Pulse el mosaico **Delivery Pipeline** para supervisar el progreso del primer despliegue. 
 6. Cuando finalice el despliegue, pulse **Ver app** para abrir la nueva aplicación Node-RED en un nuevo separador. 
2. Localice los servicios de la app del iniciador. 
 1. En el menú de Bluemix, seleccione **Panel de control**.
 2. Localice los siguientes servicios bajo *Todos los servicios*:
    - iot-starter
    - iotp-starter-cloudantNoSQLDB
 3. Localice la cadena de herramientas bajo *Todas las apps*:
    - default-toolchain-{id}}


## Paso 2: Definición de un dispositivo simulado en {{site.data.keyword.iot_short_notm}}
{: #definingsimdev}

Siga los pasos siguientes para simular un escenario que utilice un termostato para supervisar la temperatura, la humedad y la ubicación de una sala de estar. 

1.	Inicie el panel de control de {{site.data.keyword.iot_short_notm}}. 
  1. En el panel de control de Bluemix, bajo *Todos los servicios*, pulse el nombre de la instancia de {{site.data.keyword.iot_short_notm}}.
**Consejo:** El nombre de la instancia suele incluir `iotp-starter`.
  2. Pulse **Iniciar** para abrir el panel de control de {{site.data.keyword.iot_short_notm}} en un nuevo separador del navegador.    
De forma predeterminada se muestra la página `Todos los paneles`. 
2. Cree un tipo de dispositivo. 
  1.	En el menú principal, seleccione **Dispositivos** y pulse **Añadir dispositivo**.
  2.	En la página Añadir dispositivo, pulse **Crear tipo de dispositivo**.
  3.	En la página Crear tipo de dispositivo, pulse **Crear tipo de dispositivo**.
  4. Escriba un nombre exclusivo (por ejemplo, `Termostato`) para el tipo de dispositivo y pulse **Siguiente**.
  5. Opcional: la definición de una plantilla y de metadatos de las dos páginas siguientes es opcional y se puede omitir de forma segura pulsando **Siguiente** en cada página. 
  6.	Pulse **Crear** para añadir el tipo de dispositivo.
3.	Añada un dispositivo que utilice el tipo de dispositivo recién creado. 
  1. En la página Añadir dispositivo, el tipo de dispositivo que acaba de crear se muestra en la lista de tipos de dispositivo. Pulse **Siguiente** para añadir un dispositivo que utilice este tipo de dispositivo.
  2. Escriba un ID de dispositivo exclusivo (por ejemplo `LivingRoomThermo1`).
  3. Opcional: la especificación de datos descriptivos en la página Añadir dispositivo o la entrada de metadatos del dispositivo en la siguiente página es opcional; puede omitir de forma segura estas páginas pulsando **Siguiente** en cada página. 
  4. En la página Seguridad, pulse **Siguiente** para generar una señal de autenticación para el dispositivo. 
  5. En la página Resumen, verifique que la información sea correcta y pulse **Añadir** para añadir el dispositivo. Pulse **Atrás** para volver a una página anterior. 
4.	Anote la información que se muestra en la página Sus credenciales de dispositivo.    
Necesita la siguiente información para configurar el simulador y visualizar los datos: 
 - ID de organización
 - Tipo de dispositivo
 - ID de dispositivo
 - Método de autenticación
 - Señal de autenticación

## Paso 3: Configuración y ejecución del simulador de dispositivo Node-RED.   
{: #confignodered}  
Configure el simulador de dispositivo Node-RED
para enviar mensajes de dispositivo MQTT con información sobre temperatura y humedad a {{site.data.keyword.iot_short_notm}}. 

1. Inicie el editor de flujo de Node-RED. 
  1. En el panel de control de Bluemix, bajo *Todas las apps*, pulse el nombre de la cadena de herramientas.
  
**Consejo:** El nombre de la cadena de herramientas suele incluir `default-toolchain...`.
  2. En el panel de control de la cadena de herramientas, abra la instancia de Node-RED pulsando **Rutas** y seleccionando el enlace de la ruta.   
  2. Pulse **Ir a su editor de flujo de Node-RED** para abrir el editor.
2. Despliegue el dispositivo. 
  1. En el flujo del simulador de dispositivo, realice una doble pulsación en el nodo azul **Enviar a plataforma IBM IoT**. 
  2. Compruebe que la autenticación esté establecida en **Servicio Bluemix**.
  3. Escriba el **Tipo de dispositivo** y el **ID de dispositivo** del dispositivo y pulse **Listo**.
  4. Para desplegar el dispositivo, pulse **Desplegar**.
3. Configure el flujo del supervisor de temperatura de Node-RED. 
  1. En el flujo del simulador de dispositivo, realice una doble pulsación en el nodo azul **IBM IoT App In**. 
  2. En Autenticación, seleccione **Servicio Bluemix**.
  3.	Seleccione **Todos** para Tipo de dispositivo, ID de dispositivo, Suceso y Formato. 
  4.	Pulse **Listo**.
  5.  Para desplegar el supervisor, pulse **Desplegar**.
4. Valide la conexión del dispositivo.
  1.	Abra el panel de control de {{site.data.keyword.iot_short_notm}}.  
**Consejo:** Si el panel de control de {{site.data.keyword.iot_short_notm}} aún no se ha abierto en otro separador, vuelva al panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el nombre de la instancia de {{site.data.keyword.iot_short_notm}} y pulse **Iniciar panel de control**.
  2. En el menú principal, seleccione **Dispositivos**.
  3. Pulse el nombre del dispositivo que ha añadido.
   
La información del dispositivo muestra el estado de conexión del dispositivo. 
  4.	En el editor de flujo de Node-RED, realice una doble pulsación en el nodo **Enviar datos**, defina el valor de repetición en **Intervalo** y defina la frecuencia en cada `3` segundos. 
  5. Pulse **Listo**.
  6. Para desplegar los cambios, pulse **Desplegar**.  
La carga útil contiene puntos de datos, como los que se muestran en el siguiente ejemplo: 
```
{"d":{"temp":15,"humidity":50,"location":{"longitude":-98.49,"latitude":29.42}}}
```
  7. Opcional: abra el separador Depuración para verificar que se estén creando mensajes. 
    1. En el menú situado en la sección de la cabecera, seleccione **Ver**.
    2. Seleccione **Mostrar barra lateral**.
    3. Pulse el separador Depuración para ver los mensajes.
  8. En la página Información de dispositivo {{site.data.keyword.iot_short_notm}}, compruebe que puede ver los puntos de datos del dispositivo en la sección de información del sensor. 


## Paso 4: Creación de tarjetas en {{site.data.keyword.iot_short_notm}} para mostrar datos en tiempo real  
{: #createcards}  
Cree un panel y tarjetas para mostrar datos del dispositivo en el panel de control de
{{site.data.keyword.iot_short_notm}}. Para obtener más información sobre paneles y tarjetas, consulte [Visualización de datos en tiempo real utilizando paneles y tarjetas](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html).

1. Cree un panel
  1. Abra el panel de control de {{site.data.keyword.iot_short_notm}}.  
  **Consejo:** Si el panel de control de {{site.data.keyword.iot_short_notm}} aún no se ha abierto en otro separador, vuelva al panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el nombre de la instancia de {{site.data.keyword.iot_short_notm}} y pulse **Iniciar panel de control**.  
  2. Cree un panel que albergará las tarjetas de los dispositivos simulados. 
    1. Si aún no se muestra la página Todos los paneles, seleccione **Paneles** en el menú principal del panel de control de {{site.data.keyword.iot_short_notm}} y pulse **Crear nuevo panel**.
    2. Escriba un nombre para el panel (por ejemplo `Entorno doméstico`) y pulse **Siguiente**.
    3. En la página siguiente, pulse **Enviar**.  
  3. Pulse el panel que acaba de crear para abrirlo. 
2. Cree una tarjeta para visualizar la temperatura
  1. Pulse **Añadir nueva tarjeta** y seleccione el tipo de tarjeta **Gráfico de líneas** en la sección Dispositivos.
  2. Seleccione el dispositivo en la lista de dispositivos y pulse **Siguiente**.
  3. Pulse **Conectar nuevo conjunto de datos**.
  4. En la página Crear tarjeta de valores, seleccione o escriba los siguientes valores y pulse **Siguiente**.
    - Suceso: actualizar
    - Propiedad: temp
    - Nombre: Temperatura
    - Tipo: Float
    - Unidad: °C
    - Precisión: 2
    - Mínimo: 0
    - Máximo: 50
  5. En la página Vista previa de la tarjeta, seleccione **L** para el tamaño del gráfico de líneas y pulse **Siguiente**.
  6. En la página de información de la tarjeta, cambie el nombre de la tarjeta por **Temperatura** y pulse **Enviar**.   
La tarjeta de temperatura aparece en el panel de control e incluye un gráfico de líneas de los datos de temperatura en tiempo real. 
3. Cree una tarjeta para visualizar la humedad
  1. Pulse **Añadir nueva tarjeta** y seleccione el tipo de tarjeta **Indicador** en la sección Dispositivos.
  2. Seleccione el dispositivo en la lista y pulse **Siguiente**.
  3. Pulse **Conectar nuevo conjunto de datos**.
  4. En la página Crear tarjeta de valores, seleccione o escriba los siguientes valores y pulse **Siguiente**.Suceso: actualizar
     - Propiedad: humedad
     - Nombre: Humedad
     - Tipo: Float
     - Unidad: %
     - Precisión: 1
     - Mínimo: 10
     - Máximo: 95
  5. En la página Vista previa de la tarjeta, seleccione **M** para el tamaño del indicador y pulse **Siguiente**.
  6. En la página de información de la tarjeta, cambie el nombre de la tarjeta por **Humedad** y pulse **Enviar**.   
La tarjeta de humedad aparece en el panel de control e incluye un medidor que muestra los datos activos de humedad.   

<!-- 4. Create a card to display location
  1. Click **Add New Card**, and then select the **Value** card type, which is located in the Devices section.
  2. Select your device from the list, then click **Next**.
  3. Click **Connect new data set**.
  4. In the Create Value Card page, select or enter the following values.
     - Event: update
     - Property: location.latitude
     - Name: Latitude
     - Type: Float
     - Unit: "°N"
     - Precision: 2
     - Min: -180
     - Max: 180
  5. Click **Connect new data set**.
  6. In the Create Value Card page, select or enter the following values and click **Next**.
     - Event: update
     - Property: location.longitude
     - Name: Longitude
     - Type: Float
     - Unit: "°E"
     - Precision: 2
     - Min: -180
     - Max: 180
  7. In the Card Preview page, select **M** as the text size, and click **Next**.
  8. In the Card Information page, change the name of the card to **Location** and click **Submit**.   
The location card appears on the dashboard and shows the live latitude and longitude of the device.-->

## Qué hacer a continuación  
{: #whats-next}  
Ahora que el dispositivo simulado envía datos a {{site.data.keyword.iot_short_notm}}, puede seguir iterando en su proyecto IoT.
 - Observe cómo las tarjetas muestran los datos que genera el flujo de node-RED.   
Node-Red continúa enviando datos hasta que lo detiene. Para detener los datos simulados, siga estos pasos: 
    1.	En el editor de flujo de Node-RED, realice una doble pulsación en el nodo **Enviar datos** gris, defina el valor de repetición en **Intervalo** y defina la frecuencia en cada **3** segundos. 
    2. Pulse **Listo**.
    3. Para desplegar los cambios, pulse **Desplegar**.

 - Conecte un dispositivo físico.   
[Busque las recetas de IoT](https://developer.ibm.com/recipes/?post_type=tutorials&s=watson+iot) para conectar un dispositivo físico, como Raspberry Pi, y para enviar datos a {{site.data.keyword.iot_short_notm}}.

 - Explore las opciones de visualización.   
[Despliegue una aplicación node.js de ejemplo para visualizar datos del dispositivo.](https://www.bluemix.net/docs/services/IoT/visualizingdata_sample.html).

 -	Proteja con contraseña el editor de flujos de Node-RED.    
De forma predeterminada, el editor se abre para cualquiera que desee acceder y modificar flujos. Para proteger el editor con contraseña, realice las tareas siguientes: 
    1.	En el panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el nombre de la aplicación del iniciador para abrir las páginas de la aplicación. 
    2. Pulse **Tiempo de ejecución** para visualizar la página Tiempo de ejecución. 
    3. Pulse **Variable de entorno** para visualizar la página Variables de entorno. 
    4. En la sección **Definido por el usuario**, pulse **Añadir** y especifique las siguientes variables definidas por el usuario:
         -	NODE_RED_USERNAME - nombre de usuario para proteger el editor
         -	NODE_RED_PASSWORD - contraseña para proteger el editor
    3.	Pulse **Guardar**.
