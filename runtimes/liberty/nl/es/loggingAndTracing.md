---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Registro y rastreo
{: #logging_tracing}

## Archivos de registro
{: #log_files}

Los registros estándares de Liberty, como `messages.log` o el directorio `ffdc`, están disponibles en IBM Bluemix en el directorio `logs` de cada instancia de aplicación. Se puede acceder a estos registros desde la consola de IBM Bluemix o mediante la CLI CF. Por ejemplo:

* Para acceder a registros recientes para una app, ejecute el mandato siguiente:

  ```
  $ cf logs --recent <appname>
  ```
  {: codeblock}

* Para ver el archivo `messages.log` de una app que se ejecuta en un nodo DEA, ejecute el mandato siguiente:

  ```
  $ cf files <appname> logs/messages.log
  ```
  {: codeblock}

* Para ver el archivo `messages.log` de una app que se ejecuta en una célula de Diego, ejecute el mandato siguiente:

  ```
  $ cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

El nivel de registro y otras opciones de rastreo se pueden establecer mediante el archivo de configuración de Liberty. Para obtener más información, consulte el tema sobre [Perfil de Liberty: rastreo y registro](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html). El rastreo también se puede ajustar en una instancia de aplicación en ejecución mediante la consola de IBM Bluemix.

## Utilización de las funciones de rastreo y volcado
{: #using_trace_and_dump}

La configuración de rastreo de Liberty se puede ajustar para una aplicación en ejecución directamente desde la consola de IBM Bluemix. La consola también proporciona la posibilidad de solicitar y descargar vuelcos de hebras y de almacenamiento dinámico. Para ajustar la configuración de rastreo o solicitar un vuelco, seleccione una aplicación Liberty en la consola de Bluemix y elija el menú `Tiempo de ejecución` en la navegación En la vista `Tiempo de ejecución`, seleccione una instancia y pulse el botón *RASTREO* o *VOLCADO*. Si el ajuste se realiza a nivel de rastreo, consulte [Perfil de Liberty: Rastreo y registro](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html) para ver la sintaxis de la especificación de rastreo.

### Diego: activación de vuelcos mediante SSH

Para una aplicación que se ejecuta en un célula de Diego, también se puede activar un vuelco de hebras y de almacenamiento dinámico mediante la CLI CF utilizando la característica SSH. Por ejemplo:

```
$ cf ssh <appname> -c "pkill -3 java"
```
{: codeblock}

Consulte la documentación siguiente para obtener detalles sobre cómo descargar los archivos de vuelco generados.

## Descargue archivos de volcado
{: #download_dumps}

De forma predeterminada, los diversos archivos de vuelco se colocan en el directorio `dumps` del contenedor de la aplicación.

### Aplicación DEA

Para una aplicación que se ejecuta en un nodo DEA, utilice la función "cf files" para ver y descargar los archivos de vuelco.

* Para ver los vuelcos generados, ejecute el siguiente mandato:

  ```
  $ cf files <appname> dumps
  ```
  {: codeblock}

* Para descargar un archivo de vuelco, ejecute los mandatos siguientes:

    1. Obtenga el GUID de la aplicación

      ```
      $ cf app <appname> --guid
      ```
      {: codeblock}

    2. Descargue el archivo de vuelco

      ```
      $ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
      ```
      {: codeblock}

### Aplicación Diego

Para una aplicación que se ejecuta en una célula de Diego, utilice la función "cf ssh" para ver y descargar los archivos de vuelco.

* Para ver los vuelcos generados, ejecute el siguiente mandato:

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* Para descargar un archivo de vuelco, ejecute el mandato siguiente:

  ```
  $ cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

También se puede utilizar `scp` y otras herramientas similares para ver y descargar los archivos de vuelco. Consulte el apartado sobre [Acceso a apps con SSH  ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) para obtener más información.

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
