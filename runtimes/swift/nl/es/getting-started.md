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

# Iniciación a Swift en Bluemix

* {: download} Enhorabuena, ha desplegado una aplicación de ejemplo Hello World en {{site.data.keyword.Bluemix}}.  Para empezar a trabajar, siga los pasos de esta guía. O bien <a class="xref" href="http://bluemix.net" target="_blank" title="(Descargue el código de ejemplo)"><img class="hidden" src="../../images/btn_starter-code.svg" alt="Descargue el código de aplicación" />descargue el código de ejemplo</a> y explore por su cuenta.

Si sigue esta guía, configurará un entorno de desarrollo, desplegará una app localmente y en {{site.data.keyword.Bluemix}} e integrará un servicio de base de datos de {{site.data.keyword.Bluemix}} en su app.

## Requisitos previos
{: #prereqs}
* [Git ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://git-scm.com/downloads){: new_window}
* [CLI de Cloud Foundry ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/cloudfoundry/cli#downloads){: new_window}
* [Compilador de Swift ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://swift.org/download/) para su plataforma.

## 1. Clone la app de ejemplo
{: #clone}

Ahora está listo para empezar a trabar con la app Swift sencilla. Clone el repositorio y vaya al directorio donde se encuentra la app de ejemplo.
  ```
git clone https://github.com/IBM-Bluemix/get-started-swift
  ```
  {: pre}

  ```
cd get-started-swift
  ```
  {: pre}

  Lea detenidamente los archivos del directorio *get-started-swift* para familiarizarse con el contenido.

## 2. Ejecute la app localmente
{: #run_locally}

Cuando haya instalado el compilador de Swift y clonado el repositorio Git, podrá compilar y ejecutar la aplicación. Vaya al directorio raíz de este repositorio en el sistema y emita el siguiente mandato:
```
swift build
```
{: pre}

Este mandato puede tardar unos minutos en ejecutarse.

Cuando la aplicación se haya compilado correctamente, podrá ejecutar el archivo ejecutable que ha generado el compilador de Swift:
```
.build/debug/kitura-helloworld
```
{: pre}

Debería ver una salida similar a la siguiente:

```
Server is listening on port: 8080
```
{: screen}

Ver la app en http://localhost:8080

## 3. Prepare la app para el despliegue
{: #prepare}

Para desplegar en {{site.data.keyword.Bluemix_notm}}, puede resultarle útil configurar un archivo manifest.yml. El archivo manifest.yml incluye información básica sobre la app, como por ejemplo el nombre, la cantidad de memoria a asignar para cada instancia y la ruta. Encontrará un archivo manifest.yml de ejemplo en el directorio `get-started-swift`.

Abra el archivo manifest.yml y cambie el valor de `name` de `GetStartedSwift` por el nombre de su app, <var class="keyword varname" data-hd-keyref="app_name">app_name</var>.
{: download}

  ```
  applications:
   - name: GetStartedSwift
     random-route: true
     memory: 256M
     command: kitura-helloworld
     buildpack: swift_buildpack
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
  {: pre}

Sustituya *API-endpoint* en el mandato por un punto final de API de la siguiente lista.

|URL                             |Región          |
|:-------------------------------|:---------------|
| https://api.ng.bluemix.net     | EE.UU. Sur       |
| https://api.eu-gb.bluemix.net  | Reino Unido |
| https://api.au-syd.bluemix.net | Sidney         |

Inicie una sesión en su cuenta de {{site.data.keyword.Bluemix_notm}}

   ```
 cf login
   ```
   {: pre}

Desde el directorio *get-started-swift*, envíe por push la app a {{site.data.keyword.Bluemix_notm}}
   ```
 cf push
   ```
   {: pre}

Esto puede tardar un minuto. Si hay algún error en el proceso de despliegue puede utilizar el mandato `cf logs <Your-App-Name> --recent` para resolver el problema.

Cuando finalice el despliegue, verá un mensaje que indica que la app se está ejecutando.  Visualice la app en el URL que aparece en la salida del mandato push.  También puede emitir el mandato `cf apps` para ver el estado de su app y ver el URL.

## 5. Añada una base de datos
{: #add_database}

A continuación, añadiremos una base de datos NoSQL a esta aplicación y configuraremos la aplicación para que se pueda ejecutar localmente y en {{site.data.keyword.Bluemix_notm}}.

1. Inicie una sesión en {{site.data.keyword.Bluemix_notm}} en su navegador. Vaya al `Panel de control`. Seleccione su aplicación pulsando su nombre en la columna `Nombre`.
2. Pulse `Conexiones` y luego `Conectar nuevo`.
3. En la sección `Data & Analytics`, seleccione `BD Cloudant NoSQL`
4. Seleccione un plan de tarifas. Bluemix ofrece planes `Lite` gratuitos para un determinado grupo de sus servicios de nube con suficiente capacidad para comenzar
5. Seleccione `Volver a transferir` cuando se le solicite. {{site.data.keyword.Bluemix_notm}} reiniciará la aplicación y proporcionará las credenciales de base de datos para la aplicación mediante la variable de entorno `VCAP_SERVICES`. Esta variable de entorno sólo está disponible para la aplicación cuando se ejecuta en {{site.data.keyword.Bluemix_notm}}.

Las variables de entorno le permiten separar valores de despliegue del código fuente. Por ejemplo, en lugar codificar una contraseña de base de datos, puede guardarla en una variable de entorno a la que haga referencia en el código fuente. [Más información...](/docs/manageapps/depapps.html#app_env)
{: tip}

## 6. Utilice la base de datos
{: #use_database}

Ahora vamos a actualizar el código local para que apunte a esta base de datos. Cree un archivo json que contendrá las credenciales para los servicios que utilizará la aplicación. Este archivo SOLO se utilizará cuando la aplicación se ejecute localmente. Cuando se ejecute en {{site.data.keyword.Bluemix_notm}}, las credenciales se leerán de la variable de entorno VCAP_SERVICES.

Cree un archivo denominado `config.json` en el directorio `Sources` con el contenido siguiente (consulte config.json.example):
 ```
 {
    "vcap":{
       "services":{
          "cloudantNoSQLDB":[
             {
                "credentials":{
                   "host":"<host>",
                   "password":"<password>",
                   "port":443,
                   "url":"<url>",
                   "username":"<username>"
                },
                "label":"cloudantNoSQLDB",
                "name": "CloudantService"
             }
          ]
       }
    }
 }
 ```
{: pre}

Esta aplicación de ejemplo utiliza el paquete Swift-cfenv para interactuar con Bluemix para analizar las variables de entorno. [Más información...](https://packagecatalog.com/package/IBM-Swift/Swift-cfenv)

En la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, seleccione App -> Conexiones -> Cloudant -> Ver credenciales

Copie y pegue sólo las credenciales en los campos correspondientes en el archivo config.json local.

Compile y ejecute la aplicación localmente.
 ```
swift build  
 ```
 {: pre}

  ```
.build/debug/kitura-helloworld
 ```
 {: pre}

Visualice la app en: http://localhost:8080. Cualquier nombre que especifique en la app se añadirá ahora a la base de datos.

Esta aplicación de ejemplo utiliza el paquete Kitura-CouchDB para interactuar con Cloudant. [Más información...](https://packagecatalog.com/package/IBM-Swift/Kitura-CouchDB)
{: tip}

La app local y la app {{site.data.keyword.Bluemix_notm}} comparten la base de datos.  Visualice la app {{site.data.keyword.Bluemix_notm}} en el URL que aparece en la salida del mandato push anterior.  Los nombres que añada desde cualquiera de las apps deberían aparecer cuando renueve los navegadores.


Recuerde que, si no necesita la app en directo, debe detenerla para no incurrir en cargos inesperado.
{: tip}
