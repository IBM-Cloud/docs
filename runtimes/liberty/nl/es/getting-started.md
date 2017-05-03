---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:pre: .pre}
{:screen: .screen}
{:tip: .tip}
{:download: .download}
{:app_name: data-hd-keyref="app_name"}

# Iniciación a Liberty en Bluemix

* {: download} Enhorabuena, ha desplegado una aplicación de ejemplo Hello World en {{site.data.keyword.Bluemix}}.  Para empezar a trabajar, siga los pasos de esta guía. O bien <a class="xref" href="http://bluemix.net" target="_blank" title="(Descargue el código de ejemplo)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Descargue el código de aplicación" />descargue el código de ejemplo</a> y explore por su cuenta.

Si sigue esta guía, configurará un entorno de desarrollo, desplegará una app localmente y en {{site.data.keyword.Bluemix}} e integrará un servicio de base de datos de {{site.data.keyword.Bluemix}} en su app.

## Requisitos previos
{: #prereqs}

Necesitará las siguientes cuentas y herramientas:
* [Cuenta de {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/registration/)
* [CLI de Cloud Foundry ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Eclipse IDE for Java EE Developers ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://www.eclipse.org/downloads/packages/eclipse-ide-java-ee-developers/neon2){: new_window}
* [Git ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git-scm.com/downloads){: new_window}
* [Maven ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://maven.apache.org/download.cgi){: new_window}

Para desarrollar en Eclipse con {{site.data.keyword.eclipsetoolsfull}}, también tiene que [descargar las herramientas. ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix){: new_window}

## 1. Clone la app de ejemplo
{: #clone}

En primer lugar, clone el repositorio GitHub de la app de ejemplo.
  ```bash
git clone https://github.com/IBM-Bluemix/get-started-java
  ```
  {: pre}


## 2. Ejecute la app localmente mediante la línea de mandatos
{: #run_locally}

Utilice Maven para compilar el código fuente y ejecute la app resultante.

1. En la línea de mandatos, vaya al directorio en el que se encuentra la app de ejemplo.

  ```
cd get-started-java
  ```
  {: pre}

1. Utilice Maven para instalar dependencias y compilar el archivo .war.

  ```
mvn clean install
  ```
  {: pre}

1. Ejecute la app localmente en Liberty.
  ```
mvn install liberty:run-server
  ```
  {: pre}

Cuando aparezca el mensaje *The server defaultServer is ready to run a smarter planet.*, visualice la app en: http://localhost:9080/GetStartedJava.

Para detener la app, pulse *Control-C* en la ventana de línea de mandatos en la que ha iniciado la app.

## 3. Prepare la app para el despliegue
{: #prepare}

Para desplegar en {{site.data.keyword.Bluemix_notm}}, puede resultarle útil configurar un archivo manifest.yml. El archivo manifest.yml incluye información básica sobre la app, como por ejemplo el nombre, la cantidad de memoria a asignar para cada instancia y la ruta. Encontrará un archivo manifest.yml de ejemplo en el directorio `get-started-java`.

Abra el archivo manifest.yml y cambie el valor de `name` de `GetStartedJava` por el nombre de su app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: GetStartedJava
     random-route: true
     path: target/GetStartedJava.war
     memory: 512M
     instances: 1
  ```
  {: codeblock}

En este archivo manifest.yml, **random-rout: true** genera una ruta aleatoria para la app a fin de evitar que su ruta entre en conflicto con otras.  Si lo desea, puede sustituir **random-route: true** por **host: myChosenHostName**, especificando el nombre de host que elija. [Más información...](/docs/manageapps/depapps.html#appmanifest)
{: tip}

## 4. Despliegue en {{site.data.keyword.Bluemix_notm}}
{: #deploy}

Despliegue la app en una de las siguientes regiones de Bluemix. Para optimizar la latencia, elija la región más cercana a sus usuarios.

|Región          |Punto final de API                             |
|:---------------|:-------------------------------|
| EE.UU. Sur       |https://api.ng.bluemix.net     |
| Reino Unido | https://api.eu-gb.bluemix.net  |
| Sidney         | https://api.au-syd.bluemix.net |

1. Establezca el punto final de API sustituyendo `<API-endpoint>` por el punto final de su región.
  ```
cf api <API-endpoint>
  ```
  {: pre}

1. Inicie una sesión en su cuenta de {{site.data.keyword.Bluemix_notm}}.
  ```
cf login
  ```
  {: pre}

1. Desde el directorio `get-started-java`, envíe por push la aplicación a {{site.data.keyword.Bluemix_notm}}.
  ```
cf push
  ```
  {: pre}

El despliegue de la aplicación puede tardar unos minutos. Cuando finalice el despliegue, verá un mensaje que indica que la app se está ejecutando. Visualice su app en el URL que aparece en la salida del mandato push o bien visualice el estado de despliegue de la app y el URL con el siguiente mandato:
  ```
cf apps
  ```
  {: pre}

Puede solucionar errores del proceso de despliegue mediante el mandato `cf logs <Your-App-Name> --recent`.
{: tip}  

## 5. Desarrollo mediante Eclipse
{: #eclipse}

{{site.data.keyword.eclipsetoolsfull}} proporciona plug-ins que se pueden instalar en un entorno Eclipse existente para ayudarle a integrar el entorno de desarrollo integrado (IDE) con {{site.data.keyword.Bluemix_notm}}.

1. Asegúrese de tener [IBM Eclipse Tools for Bluemix](https://developer.ibm.com/wasdev/downloads/#asset/tools-IBM_Eclipse_Tools_for_Bluemix).

2. Importe el ejemplo `get-started-java` en Eclipse; para ello vaya a **Archivo > Importar > Maven > Proyectos Maven existentes**.

3. Cree una definición de servidor Liberty. Los pasos siguientes descargan un nuevo servidor Liberty.
  - En la vista **Ventana > Mostrar vista > Servidores**, pulse con el botón derecho y seleccione **Nuevo > Servidor**.
  - Seleccione **IBM > WebSphere Application Server Liberty**.
  - Seleccione **Instalar desde un archivo o repositorio**.
  - Cuando se le solicite, escriba una vía de acceso de destino a una carpeta nueva (/Users/username/liberty) donde desee instalar Liberty.
  - Seleccione **Descargar e instalar un nuevo entorno de ejecución desde ibm.com**.
  - Seleccione **WAS Liberty con Java EE 7 Web Profile**.
  - Continúe el asistente con las opciones predeterminadas para finalizar.

4. Ejecute la aplicación localmente en Liberty:
  - Cambie el navegador web por el valor predeterminado del sistema; para ello vaya a **Ventana > Navegador Web > Navegador web predeterminado del sistema**.
  - Pulse con el botón derecho en el ejemplo `GetStartedJava` y seleccione **Ejecutar como > Ejecutar en servidor**.
  - Busque y seleccione el servidor Liberty localhost y pulse **Finalizar**.

  En unos segundos, la aplicación se estará ejecutando en http://localhost:9080/GetStartedJava.

5. Actualice el código:
  - Abra `src/main/webapp/index.html` y cambie la cabecera `<h1>Welcome.</h1>` por `<h1>Welcome Jane.</h1>`.
  - Guardar los cambios. Liberty tomará los cambios automáticamente.
  - Renueve el navegador (http://localhost:9080/GetStartedJava) para ver los cambios.

6. Envíe por push los cambios a {{site.data.keyword.Bluemix_notm}}:
  - En el directorio `get-started-java` en la línea de mandatos, vuelva a compilar el archivo .war.
    ```
mvn clean install
    ```
    {: pre}
  - Envíe por push la aplicación a {{site.data.keyword.Bluemix_notm}}.
    ```
cf push
    ```
    {: pre}

Ahora ha ejecutado el código tanto localmente como en la nube.

## 6. Añada una base de datos
{: #add_database}

A continuación, añadiremos una base de datos NoSQL a esta aplicación y configuraremos la aplicación para que se pueda ejecutar localmente y en {{site.data.keyword.Bluemix_notm}}.

1. En el navegador, inicie una sesión en {{site.data.keyword.Bluemix_notm}} y vaya al panel de control. Seleccione su aplicación pulsando su nombre en la columna **Nombre**.
2. Pulse **Conexiones** y luego **Conectar nuevo**.
3. En la sección **Data & Analytics**, seleccione **BD Cloudant NoSQL** y cree el servicio.
4. Seleccione **Volver a transferir** cuando se le solicite. {{site.data.keyword.Bluemix_notm}} reiniciará la aplicación y proporcionará las credenciales de base de datos para la aplicación mediante la variable de entorno `VCAP_SERVICES`. Esta variable de entorno sólo está disponible para la aplicación cuando se ejecuta en {{site.data.keyword.Bluemix_notm}}.

Las variables de entorno le permiten separar valores de despliegue del código fuente. Por ejemplo, en lugar codificar una contraseña de base de datos, puede guardarla en una variable de entorno a la que haga referencia en el código fuente. [Más información...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 7. Utilice la base de datos
{: #use_database}
Ahora vamos a actualizar el código local para que apunte a esta base de datos. Guardaremos las credenciales correspondientes a los servicios en un archivo de propiedades. Este archivo SOLO se utilizará cuando la aplicación se ejecute localmente. Cuando se ejecute en {{site.data.keyword.Bluemix_notm}}, las credenciales se leerán de la variable de entorno `VCAP_SERVICES`.

1. En Eclipse, abra el archivo src/main/resources/cloudant.properties:
  ```
  cloudant_url=
  ```
  {: pre}

2. En su navegador, vaya a {{site.data.keyword.Bluemix_notm}} y seleccione **Apps > _su app_ > Conexiones > Cloudant > Ver credenciales**.

3. Copie y pegue sólo el `url` de las credenciales en el campo `url` del archivo `cloudant.properties` y guarde los cambios.
  ```
  cloudant_url=https://123456789 ... bluemix.cloudant.com
  ```
  {:pre}

4. Reinicie el servidor Liberty en Eclipse desde la vista `Servidores`.

  Renueve la vista del navegador en http://localhost:9080/GetStartedJava/. Cualquier nombre que especifique en la app se añadirá ahora a la base de datos.

  La app local y la app {{site.data.keyword.Bluemix_notm}} comparten la base de datos. Los nombres que añada desde cualquiera de las apps aparecerán cuando renueve los navegadores.


Recuerde que si no necesita la app en directo en {{site.data.keyword.Bluemix_notm}}, debe detener la app para no incurrir en cargos inesperados.
{: tip}  
