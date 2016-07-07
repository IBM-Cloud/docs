---

copyright:
  years: 2015-2016

---

<!-- Attribute definitions -->
{:codeblock: .codeblock}

# Cómo empezar con el ejemplo de Hello Bluemix for Android
{: #gettingstarted-android}
*Última actualización: 27 de mayo de 2016*
{: .last-updated}  

Si desea empezar a trabajar con una aplicación para Android nueva, puede utilizar la app HelloWorld. Esta app muestra cómo conectar con el programa de fondo de {{site.data.keyword.Bluemix}} desde una app para móvil sin autenticación. La app la tiene instalado el SDK. Cuando esté listo, puede obtener las bibliotecas específicas que desee utilizar en la app.

1. Cree el programa de fondo móvil en {{site.data.keyword.Bluemix_notm}}.
    1. En la sección Contenedores modelo del catálogo de {{site.data.keyword.Bluemix_notm}}, pulse MobileFirst Services Starter.
    2. Especifique un nombre y un host para la app y pulse **Crear**.
    3. Pulse **Finalizar**.
2. Obtenga el proyecto de GitHub. De forma opcional, utilice el mandato git clone para obtener el proyecto. En el sistema, abra el terminal y, a continuación, escriba el siguiente mandato:
    ```
    git clone https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld.git
    ```

3. Inicialice el proyecto sustituyendo &lt;RUTA_APLICACIÓN&gt; e &lt;ID_APLICACIÓN&gt; por la ruta de la aplicación y el GUID del bloque `try` de la función `BMSClient.getInstance().initialize()`:
```
// initialize SDK with IBM Bluemix application ID and route
BMSClient.getInstance().initialize(this, "<RUTA_APLICACIÓN>", "<ID_APLICACIÓN>");
```
4. Ejecute el ejemplo en el entorno de desarrollo.
En la barra de herramientas de Android Studio, pulse el botón **Play** y seleccione un simulador.
5. En el simulador, pulse **Ping
                {{site.data.keyword.Bluemix_notm}}**. La app de ejemplo envía una solicitud Get al tiempo de ejecución de `Node.js` en {{site.data.keyword.Bluemix_notm}}. Si la solicitud es satisfactoria, la conexión se verifica y el texto del simulador se actualiza.

  **Nota:** El código de tiempo de ejecución de `Node.js` se proporciona en el contenedor modelo de MobileFirst Services Starter. Si la aplicación de fondo no se ha creado con el contenedor modelo de MobileFirst Services Starter, la aplicación no se conectará satisfactoriamente.

  Cuando se conecte correctamente a {{site.data.keyword.Bluemix_notm}} desde la app móvil en Android Studio, se mostrará el siguiente mensaje:

  `Yay! You are connected`
  {: screen}

  ![Aplicación Hello World conectada correctamente a {{site.data.keyword.Bluemix_notm}}](images/yayconnected.jpg "Figura 1. Aplicación Hello World conectada correctamente a Bluemix")

  Si la conexión falla, verá:
  `Bummer. Something went wrong`
  {: screen}

  ![Aplicación Hello World no conectada a Bluemix](images/bummer_android.jpg "Figura 2. Aplicación Hello World no conectada a Bluemix")

  Puede resolver los problemas de la conexión fallida de la forma siguiente:
   * Compruebe que ha pegado correctamente los valores de ruta y de GUID:
   * Revise el registro de depuración para obtener más información.


## Pasos siguientes:
{: #next}
Para obtener información sobre cómo obtener el SDK e integrarlo en la app para móvil, consulte la información sobre la configuración de los servicios de Bluemix.
   * [Mobile Client Access](../../services/mobileaccess/index.html)
   * [Push](../../services/mobilepush/index.html)

# rellinks

## samples
   * [Ejemplo de Hello Bluemix](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-helloworld)

## sdk
   * [Core SDK](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)

## api
   * [API principal](https://www.{DomainName}/docs/api/content/api/mobilefirst/android/core-api-doc/overview-summary.html)
