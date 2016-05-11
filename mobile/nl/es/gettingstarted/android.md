<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Cómo empezar con el ejemplo HelloWorld
{: #gettingstarted-android}
*Última actualización: 28 de enero de 2016*  

Si desea empezar a trabajar con una aplicación para Android nueva, puede utilizar la app HelloWorld. Esta app muestra cómo conectar con el programa de fondo de {{site.data.keyword.Bluemix}} desde una app para móvil sin autenticación. La app la tiene instalado el SDK. Cuando esté listo, puede obtener las bibliotecas específicas que desee utilizar en la app.

1. Cree el programa de fondo móvil en {{site.data.keyword.Bluemix_notm}}.
    1. En la sección Contenedores modelo del catálogo de {{site.data.keyword.Bluemix_notm}}, pulse MobileFirst Services Starter.
    2. Especifique un nombre y un host para la app y pulse **Crear**.
    3. Pulse **Finalizar**.
2. Obtenga el proyecto de GitHub. De forma opcional, utilice el mandato git clone para obtener el proyecto. En el sistema, abra el terminal y, a continuación, escriba el siguiente mandato:
```
git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld.git
```
Antes de empezar, descargue el archivo `Gradle.zip` e instale Gradle extrayendo el archivo comprimido descargado en el directorio que desee. Android Studio podría solicitar un GRADLE HOME cuando se importe el ejemplo por primera vez. Establezca esa vía de acceso al directorio bin que se encuentra en el archivo `Gradle.zip` extraído. El archivo `build.gradle` compila automáticamente el proyecto recuperando las dependencias necesarias.
3. Inicialice el proyecto.
Para inicializar el SDK, sustituya &lt;RUTA_APLICACIÓN&gt; e &lt;ID_APLICACIÓN&gt; por la ruta de la aplicación y el GUID del bloque try dentro de la función `BMSClient.getInstance().initialize()`:
```
// initialize SDK with IBM Bluemix application ID and route
BMSClient.getInstance().initialize(this, "<RUTA_APLICACIÓN>", "<ID_APLICACIÓN>");
```{: codeblock}

4. Ejecute el ejemplo en el entorno de desarrollo.
En la barra de herramientas de Android Studio, pulse el botón de reproducción y seleccione un simulador.
En el simulador, pulse **Ping
                {{site.data.keyword.Bluemix_notm}}**. La app de ejemplo envía una solicitud Get a un recurso protegido en el tiempo de ejecución de Node.js en {{site.data.keyword.Bluemix_notm}}. Si la solicitud es satisfactoria, la conexión se verifica y el texto del simulador se actualiza.
<br/>**Nota:** El código de tiempo de ejecución de Node.js se proporciona en el contenedor modelo de MobileFirst Services Starter. Si la aplicación de fondo no se ha creado con el contenedor modelo de MobileFirst Services Starter, la aplicación no se conectará correctamente.<br/>
Cuando se conecte correctamente a {{site.data.keyword.Bluemix_notm}} desde la app para móviles en Android Studio, verá un mensaje parecido al siguiente: "¡Se ha conectado!":<br/>
![La aplicación Hello World se ha conectado correctamente a {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figura 1. La aplicación Hello World se ha conectado correctamente a Bluemix")

5. Resolver problemas.<br/>Si la conexión falla, se muestra un mensaje parecido al siguiente: "Algo salió mal":</br>
![Aplicación Hello World no conectada a Bluemix](images/bummer_android.jpg "Figura 2. Aplicación Hello World no conectada a Bluemix")
<br/>
Compruebe los siguientes puntos:
 * Compruebe que ha pegado correctamente los valores de ruta y de GUID:
 * También puede consultar el registro de depuración para obtener más información.

## Pasos siguientes:
{: #next}
Para obtener información sobre cómo obtener el SDK e integrarlo en la app para móvil, consulte la información sobre la configuración de los servicios de Bluemix.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Ejemplo HelloWorld](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [API principal](https://classicdocs.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
