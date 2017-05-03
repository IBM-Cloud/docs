---

copyright:
  years: 2017
lastupdated: "2017-04-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Iniciación a Tomcat en Bluemix
{: #getting_started}

* {: download} Enhorabuena, ha desplegado una aplicación de ejemplo Hello World en {{site.data.keyword.Bluemix}}.  Para empezar a trabajar, siga los pasos de esta guía. O bien <a class="xref" href="http://bluemix.net" target="_blank" title="(Descargue el código de ejemplo)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Descargue el código de aplicación" />descargue el código de ejemplo</a> y explore por su cuenta.

Si sigue esta guía, configurará un entorno de desarrollo, desplegará una app localmente y en {{site.data.keyword.Bluemix}} e integrará un servicio de base de datos de {{site.data.keyword.Bluemix}} en su app.

## Requisitos previos
{: #prereqs}

Necesitará lo siguiente:
* [Cuenta de {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [CLI de Cloud Foundry ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git-scm.com/downloads){: new_window}
* [Maven ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://maven.apache.org/download.cgi){: new_window}
* [Apache Tomcat versión 8.0.41 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://tomcat.apache.org/download-80.cgi#8.0.41 ){: new_window}


## 1. Clone la app de ejemplo
{: #clone}

Ahora está listo para empezar a trabar con la app Tomcat de ejemplo. Clone el repositorio y vaya al directorio donde se encuentra la app de ejemplo.
```
git clone https://github.com/IBM-Bluemix/get-started-tomcat
```
{: pre}

```
cd get-started-tomcat
```
{: pre}

Lea detenidamente los archivos del directorio *get-started-tomcat* para familiarizarse con el contenido.

## 2. Ejecute la app localmente
{: #run_locally}

Debe instalar las dependencias y compilar un archivo .war según se indica en el archivo pom.xml para ejecutar la app.

Instale las dependencias.

```
mvn clean install  
```
{: pre}


Copie GetStartedTomcat.war del directorio `target` en el directorio `tomcat-install-dir` `webapps`.

Ejecute la app.  
```
<tomcat-install-dir>/bin/startup.bat|.sh
```
{: screen}

Visualice la app en: http://localhost:8080/GetStartedTomcat/

Utilice `shutdown.bat|.sh` para detener la app.  Es posible que tenga que obtener permiso de ejecución de mandatos.
{: tip}

## 3. Prepare la app para el despliegue en {{site.data.keyword.Bluemix_notm}}
{: #prepare}

Para desplegar en {{site.data.keyword.Bluemix_notm}}, puede resultarle útil configurar un archivo manifest.yml. El archivo manifest.yml incluye información básica sobre la app, como por ejemplo el nombre, la cantidad de memoria a asignar para cada instancia y la ruta. Encontrará un archivo manifest.yml de ejemplo en el directorio `get-started-tomcat`.

Abra el archivo manifest.yml y cambie el valor de `name` de `GetStartedTomcat` por el nombre de su app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
  - name: GetStartedTomcat
    random-route: true
    memory: 256M
    path: target/TomcatHelloWorldApp.war
    buildpack: java_buildpack
  ```
  {: codeblock}

En este archivo manifest.yml, **random-rout: true** genera una ruta aleatoria para la app a fin de evitar que su ruta entre en conflicto con otras.  Si lo desea, puede sustituir **random-route: true** por **host: myChosenHostName**, especificando el nombre de host que elija. [Más información...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Despliegue la app
{: #deploy}

Puede utilizar la CLI de Cloud Foundry para desplegar apps.

Elija el punto final de la API

```
cf api <API-endpoint>
```
{:pre}

Sustituya *API-endpoint* en el mandato por un punto final de API de la siguiente lista.

|URL                             |Región          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | EE.UU. Sur       |
| https://api.eu-gb.bluemix.net  | Reino Unido |
| https://api.au-syd.bluemix.net | Sidney         |


Inicie una sesión en su cuenta de {{site.data.keyword.Bluemix_notm}}:

```
cf login
```
{: pre}

Desde el directorio *get-started-tomcat*, envíe por push la app a {{site.data.keyword.Bluemix_notm}}
```
cf push
```
{: pre}

Esto puede tardar un par de minutos. Si hay algún error en el proceso de despliegue puede utilizar el mandato `cf logs <Your-App-Name> --recent` para resolver el problema.

Cuando finalice el despliegue, verá un mensaje que indica que la app se está ejecutando.  Visualice la app en el URL que aparece en la salida del mandato push.  También puede emitir el mandato
  ```
cf apps
  ```
  {: pre}
  para ver el estado de su app y ver el URL.

## 6. Desarrollo en Eclipse
{: #developing_in_eclipse}

IBM® Eclipse Tools for {{site.data.keyword.Bluemix}} proporciona plug-ins que se pueden instalar en un entorno Eclipse existente para ayudarle a integrar el entorno de desarrollo integrado (IDE) con {{site.data.keyword.Bluemix_notm}}.

Descargue e instale [las herramientas IBM Eclipse para Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix).

Importe este ejemplo en Eclipse con la opción `Archivo` -> `Importar` -> `Maven` -> `Proyectos Maven existentes`.

Cree una definición de servidor Tomcat:
  - En la vista `Servidores`, pulse con el botón derecho en -> `Nuevo` -> `Servidor`.
  - Seleccione `Apache` -> `Servidor Tomcat v8.0`.
  - Elija su `tomcat-install-dir`.
  - Continúe el asistente con las opciones predeterminadas para finalizar.

Ejecute la aplicación localmente en el servidor Apache:
  - Pulse con el botón derecho en el ejemplo `GetStartedTomcat` y seleccione la opción `Ejecutar como` -> `Ejecutar en servidor`.
  - Busque y seleccione el servidor Tomcat y pulse Finalizar.
  - En unos segundos, la aplicación debería ejecutarse http://localhost:8080/TomcatHelloWorldApp/

Cree una definición de servidor de {{site.data.keyword.Bluemix_notm}}:
  - En la vista `Servidores`, pulse con el botón derecho en -> `Nuevo` -> `Servidor`.
  - Seleccione `IBM` -> `IBM Bluemix` y siga los pasos del asistente.
  - Escriba sus credenciales y pulse `Siguiente`
  - Seleccione su `organización` y `espacio` y pulse `Finalizar`

Ejecute la aplicación en {{site.data.keyword.Bluemix_notm}}:
  - Pulse con el botón derecho en el ejemplo `GetStartedTomcat` y seleccione la opción `Ejecutar como` -> `Ejecutar en servidor`.
  - Busque y seleccione `IBM Bluemix` y pulse Finalizar.
  - Un asistente le guiará con las opciones de despliegue. Asegúrese de elegir un `Nombre` exclusivo para la aplicación.
  - En unos minutos, la aplicación debería ejecutarse en el URL elegido.

Ahora ha ejecutado el código localmente y en la nube.

## 7. Añada una base de datos
{: #add_database}

A continuación, añadiremos una base de datos NoSQL a esta aplicación y configuraremos la aplicación para que se pueda ejecutar localmente y en Bluemix.

1. Inicie una sesión en {{site.data.keyword.Bluemix_notm}} en su navegador. Vaya al `Panel de control`. Seleccione su aplicación pulsando su nombre en la columna `Nombre`.
2. Pulse `Conexiones` y luego `Conectar nuevo`.
2. En la sección `Data & Analytics`, seleccione `BD Cloudant NoSQL` y `Crear` para crear el servicio.
3. Seleccione `Volver a transferir` cuando se le solicite. {{site.data.keyword.Bluemix_notm}} reiniciará la aplicación y proporcionará las credenciales de base de datos para la aplicación mediante la variable de entorno `VCAP_SERVICES`. Esta variable de entorno sólo está disponible para la aplicación cuando se ejecuta en {{site.data.keyword.Bluemix_notm}}.

Las variables de entorno le permiten separar valores de despliegue del código fuente. Por ejemplo, en lugar codificar una contraseña de base de datos, puede guardarla en una variable de entorno a la que haga referencia en el código fuente. [Más información...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 8. Utilice la base de datos
{: #use_database}
Ahora vamos a actualizar el código local para que apunte a esta base de datos. Guardaremos las credenciales correspondientes a los servicios en un archivo de propiedades. Este archivo SOLO se utilizará cuando la aplicación se ejecute localmente. Cuando se ejecute en {{site.data.keyword.Bluemix_notm}}, las credenciales se leerán de la variable de entorno VCAP_SERVICES.

1. Abra Eclipse y abra el archivo src/main/resources/cloudant.properties:
  ```
  cloudant_url=
  ```
  {: pre}

2. En el navegador, abra la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, seleccione App -> Conexiones -> Cloudant -> Ver credenciales

3. Copie y pegue sólo el `url` de las credenciales en el campo `url` del archivo `cloudant.properties` y guarde los cambios.  El resultado se parecerá al siguiente:
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```

4. Reinicie el servidor Tomcat en Eclipse desde la vista `Servidores`.

  Renueve la vista del navegador en http://localhost:8080/GetStartedTomcat/. Cualquier nombre que especifique en la app se añadirá ahora a la base de datos.

  La app local y la app {{site.data.keyword.Bluemix_notm}} comparten la base de datos.  Visualice la app {{site.data.keyword.Bluemix_notm}} en el URL que aparece en la salida del mandato push anterior.  Los nombres que añada desde cualquiera de las apps deberían aparecer cuando renueve los navegadores.

Recuerde que si no necesita la app en directo en {{site.data.keyword.Bluemix_notm}}, debe detenerla para no incurrir en cargos inesperados.
{: tip}  
