---

copyright:
  years: 2016
lastupdated: "2016-06-21"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Uso de Oracle JRE
{: #using_oraacle_jre}

Puede ejecutar la aplicación Liberty en Bluemix con el Oracle JRE si lo ha elegido.  Para ello, debe
* alojar el JRE en una ubicación desde la que pueda descargarlo el paquete de compilación,
* alojar un archivo index.yml que proporciona la ubicación del JRE de host, y
* configurar la aplicación para utilizar dicho JRE.

## Alojamiento del JRE e index.yml
{: #hosting_jre}

El archivo de Oracle JRE debe estar alojado en un servidor web, y el paquete de compilación de Liberty debe ser capaz de descargarlo desde dicho servidor. Puede alojarlo en el mismo Bluemix utilizando cualquiera de los recursos del servidor disponibles, o puede alojarlo en alguna ubicación disponible de forma pública.  El servidor debe estar configurado con un archivo index.yml que especifique los detalles sobre el archivo JRE. Complete los pasos que se muestran a continuación para alojar el JRE e index.yml:
  1. Adquiera el Oracle JRE.  Tenga en cuenta que el JRE debe ser la versión para utilizarlo en un SO Unix de 64 bits, y que debe ser un archivo tar.gz.
  2. Aloje el archivo JRE en una ubicación desde la que el paquete de compilación de Liberty pueda descargarlo. 
  3. Asegúrese de que se proporciona un archivo index.yml en la ubicación de alojamiento. El archivo index.yml debe contener una entrada que conste del ID de versión del Oracle JRE seguido por dos puntos y el URL completo de la ubicación de dicho archivo de JRE. El formato del index.yml es:
```
   ---
   jre_version: https://hostingLocation/jreName.tar.gz
```
{: codeblock}

    * Por ejemplo:
    ```
       ---
       1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```

## Configurar la app
{: #configure_app}

Deben establecerse dos variables de entorno en la aplicación Liberty. *JBP_CONFIG_OPENJDK* debe establecerse para especificar la ubicación del archivo index.yml y la variable de entorno de *JVM* debe estar establecida en *openjdk* para configurar el paquete de compilación para utilizar un JRE alternativo.

Para la variable JBP_CONFIG_OPENJDK, el valor es
```
   'repository_root: "https://locationToIndexYml"'
```
{: codeblock}

Para establecerlo, puede emitir un mandato como:
```
   $ cf se myApp JBP_CONFIG_OPENJDK 'repository_root: https://myHostingApp.ng.bluemix.net'
```
{: codeblock}

Tenga en cuenta que el URL *repository_root* no incluye 'index.yml', pero se detiene antes de su ubicación.

Para establecer el entorno de JVM, la variable emite un mandato como:
```
   $ cf se myApp JVM 'openjdk'
```
{: codeblock}

**Nota**: Debe volver a transferir la aplicación después de establecer las variables de entorno.

## Confirmación
{: #confirmation}

Para confirmar que se utiliza el JRE esperado, consulte staging_task.log en busca de un mensaje similar a
```
   -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}

# rellinks
{: #rellinks}
## general
{: #general}
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
