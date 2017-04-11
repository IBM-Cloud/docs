---

copyright:
  years: 2016, 2017
lastupdated: "2016-06-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visualización de datos de dispositivos
{: #visualizingdata_data}

Este ejemplo le ayuda a visualizar los datos históricos y en tiempo real desde los dispositivos registrados en la organización de {{site.data.keyword.iot_full}}.
{:shortdesc}

## Antes de empezar
{: #byb}

Para poder visualizar los datos, debe realizar las acciones siguientes:

- Registrar los dispositivos en la organización de {{site.data.keyword.iot_short_notm}}.
- Garantizar que los dispositivos estén enviando sucesos al {{site.data.keyword.iot_short_notm}}.
- [Descargar el ejemplo de visualización](https://github.com/ibm-messaging/iot-visualization/archive/v0.2.0.zip) desde el repositorio de github y extraer el archivo .zip.
- [Instalar la herramienta de línea de mandatos cf](../../starters/install_cli.html) desde {{site.data.keyword.Bluemix_notm}}.

## Ejecución del ejemplo en {{site.data.keyword.Bluemix_notm}}
{: #running_sample}

1. Cree una aplicación en {{site.data.keyword.Bluemix_notm}} utilizando el SDK Node.js. Anote el nombre de la aplicación y el nombre de host de la aplicación. Esta información es necesaria para cargar la aplicación en {{site.data.keyword.Bluemix_notm}}.
2. Enlace la aplicación node.JS a la instancia de {{site.data.keyword.iot_short_notm}} en el panel de instrumentos de {{site.data.keyword.Bluemix_notm}} completando los pasos siguientes:

  a. En el panel de control de {{site.data.keyword.Bluemix_notm}}, pulse la aplicación Node.JS que ha creado.

  b. Pulse **Enlazar un servicio o API** y, a continuación, seleccione el servicio de {{site.data.keyword.iot_short_notm}} y pulse **Añadir**.
3. Utilizando la herramienta de línea de mandatos cf, cambie el directorio al paquete de ejemplo de visualización extraído y ejecute el siguiente mandato para conectar a {{site.data.keyword.Bluemix_notm}}.
```
cf api https://api.ng.bluemix.net
```
4. A continuación, inicie sesión en {{site.data.keyword.Bluemix_notm}} utilizando:
```
cf login -u <your_bluemix_login_id>
```
Si no utiliza la organización ni el espacio predeterminados, puede utilizar:
```
cf target-o <your_bluemix_org> -s dev
```

5. Edite el archivo `manifest.yml` y actualice los nombres de host y de aplicación utilizando el formato siguiente:
```
aplicaciones:
 - cuota de disco: 1024M
   host: <your_bluemix_hostname>
   nombre: <your_bluemix_appname>
   mandato: node ap.js
   vía de acceso:
   dominio: mybluemix.net
   instancias: 1
   memoria: 128M
```
6. Despliegue el ejemplo de visualización utilizando el mandato siguiente:
```
cf push <your_application_name>
```
7. En su navegador, escriba la siguiente URL:
```
http://<your_application_name>.mybluemix.net
```

Todos los dispositivos de su organización se listan en el menú desplegable del dispositivo. Cuando esta opción esté seleccionada, debería ver la visualización de los datos en tiempo real que el dispositivo envía al servicio de {{site.data.keyword.iot_short_notm}}. Para ver los datos históricos, pulse el botón **Datos históricos**.

## Personalización del ejemplo
{: #customize_sample}

Esta aplicación de ejemplo es una aplicación web autónoma, grabada en la infraestructura node.js. El ejemplo muestra sucesos que se envían mediante dispositivos registrados en el {{site.data.keyword.iot_short_notm}}. En el ejemplo se utilizan las siguientes herramientas:

- Express: Infraestructura de la aplicación web Node.js
- JQuery: Llamadas a interfaz de usuario y Ajax
- Rickshaw: Herramienta de visualización gráfica
- Paho: Cliente MQTT

La aplicación de ejemplo está estructurada con los directorios siguientes:

- Public
- CSS: Hojas de estilo
- Images
- JS: archivos lógicos de JavaScript principales
- Historian: código para la visualización de historian
- Realtime: código para la visualización en tiempo real
- Uicontroller.js: código para controlar la interfaz de usuario
- Routes: lógica de direccionamiento y la aplicación web
- Utils: funciones de programas de utilidad, utilizadas para realizar llamadas de HTTP
- Views: archivos de interfaz de usuario, escritos en Jade
- La biblioteca de gráficos Rickshaw se utiliza para trazar el gráfico para datos en tiempo real e históricos.

## Personalización de la visualización de datos en tiempo real
{: #customize_real_time_display}

El directorio que contiene el código de visualización gráfica para los datos en tiempo real es `public/ja/realtime`. La lógica de gráficos se puede personalizar editando `public/js/historian/realtimeGraph.js`.

El archivo que hace referencia a la biblioteca de MQTT de Paho para suscribirse a los temas de dispositivos y recibir sucesos de dispositivos desde el {{site.data.keyword.iot_short_notm}} se puede encontrar en `public/js/historian/realtime.js`.

Los sucesos de dispositivos se pasan al archivo `realtimeGraph.js` para trazar el gráfico.

## Personalización de la visualización de datos históricos
{: #customize_historical_display}

El directorio que contiene el código de visualización gráfica para los datos de dispositivos históricos es `public/js/historian`. La lógica de gráficos se puede personalizar editando `public/js/historian/historianGraph.js`.

El archivo que controla las llamadas de API REST para recopilar datos de dispositivos históricos es `public/js/historian/historian.js`.

Los datos históricos se pasan al archivo `historianGraph.js` para trazar el gráfico.

Dispone de una guía del desarrollador más detallada en la wiki de visualización de
Github iot.
