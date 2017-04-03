---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}  
{:screen: .screen}  
{:codeblock: .codeblock}  
{:pre: .pre}  

# {{site.data.keyword.dev_cli_short}}
{: #developercli}	

El {{site.data.keyword.dev_cli_long}} proporciona un enfoque basado en mandatos extensibles para crear, desarrollar y desplegar un proyecto web con el plugin `dev`. Ideal para desarrolladores que prefieren utilizar el control de línea de mandatos para desarrollar aplicaciones de microservicios completas. 

{: shortdesc}

El {{site.data.keyword.dev_cli_notm}} utiliza dos contenedores para facilitar la creación y la realización de pruebas de su aplicación. El primero es el contenedor de herramientas que contiene las utilidades necesarias para crear y probar la aplicación. El Dockerfile para este contenedor está definido por el parámetro [dockerfile-tools](#command-parameters). Puede considerarlo como un contenedor de desarrollo, ya que contiene las herramientas que suelen utilizarse para el desarrollo de un tiempo de ejecución determinado.

El segundo contenedor es el contenedor de ejecución. El formato de este contenedor es adecuado para desplegarlo y utilizarlo en, por ejemplo, {{site.data.keyword.Bluemix}}. Como resultado, este contenedor normalmente tendrá un punto de entrada definido que inicia su aplicación. Al seleccionar ejecutar la aplicación a través de {{site.data.keyword.dev_cli_short}}, utiliza este contenedor. El Dockerfile para este contenedor está definido por el parámetro [dockerfile-run](#run-parameters). 


## Adición de {{site.data.keyword.dev_cli_notm}}
{: #add-cli}


### Requisitos previos
{: #prereq}

Se exigen algunos requisitos previos para explorar completamente y utilizar correctamente el {{site.data.keyword.dev_cli_short}}, ya que es muy ampliable y le permite utilizar tecnologías complementarias adicionales.

1. Instale [Cloud Foundry CLI ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/cloudfoundry/cli#getting-started).

2. Instale la [CLI de {{site.data.keyword.Bluemix}} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://clis.ng.bluemix.net/ui/home.html).

3. Obtenga un [ID de {{site.data.keyword.Bluemix_notm}}](https://www.bluemix.net).

4. Opcional: Si planea ejecutar y depurar aplicaciones a nivel local, deberá instalar también [Docker ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.docker.com/get-docker). Esto solo es necesario para proyectos que no sean móviles.


### Instalación
{: #installation}

1. Instale el [{{site.data.keyword.dev_cli_short}} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in){: new_window} ejecutando el siguiente mandato:
 
	```
	bx plugin install dev -r Bluemix
	```
	{: codeblock}

2. 	Valide la correcta instalación ejecutando el siguiente mandato:  
 
	```
	bx dev
	```
	{: codeblock}
	

### Antes de empezar
{: #before-install}
	
1. Inicie sesión en {{site.data.keyword.Bluemix_notm}}.

	```
	bx login
	```
	{: codeblock}
	
	**Nota:** si se rechazan sus credenciales, puede que esté utilizando un ID federado. Siga estos pasos para autenticarse mediante un ID federado.
	
	<!-- 
	POINT TO BLUEMIX CLI LOG IN DOCUMENTATION !!!
	
	This link does not work in production yet --> 
	
	1. Inicie sesión en [{{site.data.keyword.iamshort}} ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://www.bluemix.net/iam/#/apikeys){: new_window}.
	2. Seleccione **Crear clave de API**.
		* Especifique un nombre y descripción para la clave de API
	3. Descargue su clave de API.
	4. Abra el archivo y copie el valor del campo `apiKey`.
	5. Inicie sesión utilizando el siguiente mandato:
	 
		```
		bx login --apikey <value>
		```
		{: codeblock}


## Mandatos
{: #commands}

Utilice los siguientes mandatos para crear un proyecto, desplegarlo, depurarlo y probarlo.

### Build
{: #build}

Puede crear su aplicación mediante el mandato `build`. El elemento de configuración `build-cmd-run` se utiliza para crear la aplicación. Los mandatos `test`, `debug` y `run` ejecutan una compilación del mismo modo que este mandato como parte de su funcionamiento normal, por lo que no es necesario ejecutar este mandato antes que estos.

Ejecute el siguiente mandato en el directorio del proyecto actual para crear la aplicación:  

```
bx dev build
```
{: codeblock}


[Parámetros del mandato de compilación](#command-parameters)


### Code
{: #code}

El mandato `code` le permite descargar el código de aplicación después del despliegue, para que pueda revisar de forma local o realizar cambios adicionales.

Ejecute el siguiente mandato para descargar el código de un proyecto específico.

```
bx dev code <projectName>
```
{: codeblock}


### Create
{: #create}

Cree un proyecto nuevo, solicitando toda la información necesaria, incluyendo el idioma, el nombre del proyecto y el tipo de patrón de aplicación. El proyecto se creará en el directorio actual.  

Para crear un proyecto nuevo en el directorio del proyecto actual y asociarle servicios, ejecute el siguiente mandato:

```
bx dev create
```
{: codeblock}


### Debug
{: #debug}

Puede depurar la aplicación a través del mandato `debug`. Primero se completa una compilación contra el proyecto utilizando el elemento de configuración `build-cmd-debug` como la instrucción de compilación. A continuación, se inicia un contenedor que expone un puerto o puertos de depuración tal y como se define en `container-port-map-debug`. Conecte su herramienta de depuración preferida al puerto o puertos y podrá depurar su aplicación de modo normal.

**Limitación**: actualmente los proyectos Swift no están disponibles para depuración.

Ejecute el siguiente mandato en el directorio del proyecto actual para depurar la aplicación:

```
bx dev debug
```
{: codeblock}	

Para salir de la sesión de depuración, utilice `CTRL-C`.


#### Parámetros del mandato de depuración
{: #debug-parameters}

Los siguientes parámetros son exclusivos del mandato `debug` y ayudan a depurar una aplicación. 

##### `container-port-map-debug`
{: #port-map-debug}

* Correlaciones de puertos para el puerto de depuración. El primer valor es el puerto que se utilizará en el sistema operativo del host, el segundo es el puerto del contenedor (host:container).
* Uso: `bx dev debug container-port-map-debug [7777:7777]`
 
##### `build-cmd-debug`
{: #build-cmd-debug}

* Utilizado para generar código para DEBUG.
* Uso: `bx dev debug build-cmd-debug build.command.sh`

##### `debug-cmd`
{: #debug-cmd}

* Utilizado para depurar código en el contenedor de herramientas. Esto es opcional si su `build-cmd-debug` iniciará la aplicación en depuración. 
* Uso: `bx dev debug debug-cmd /the/debug/command`

#### Depuración de aplicaciones locales:
{: #local-app-dev}

Para obtener más información sobre la depuración de aplicaciones locales, consulte [Depuración de aplicaciones locales](docs/cloudnative/dev_cli_local_debug.html#local-debug).


### Delete
{: #delete}

Este mandato le permite eliminar proyectos de su espacio {{site.data.keyword.Bluemix}}.

Ejecute el siguiente mandato para suprimir su proyecto de {{site.data.keyword.Bluemix}}:

```
bx dev delete <projectName>
```
{: codeblock}
 

**Nota** los servicios {{site.data.keyword.Bluemix}} **no** se eliminan.


### Help
{: #help}

De forma predeterminada, si no se pasa ninguna acción ni argumento, o si se proporciona la acción 'help', este mandato mostrará un texto "Help" general. La ayuda general mostrada incluye una descripción de los argumentos base, así como una lista de las acciones disponibles.  

Ejecute el siguiente mandato para visualizar la información de ayuda general:

```
bx dev help
```
{: codeblock}


### List
{: #list}

Puede listar todos sus proyectos {{site.data.keyword.Bluemix_notm}} en un espacio. 

Ejecute el siguiente mandato para listar sus proyectos:

```
bx dev list
```
{: codeblock}


<!--
### Editing a project
{: #edit}

You can edit a project, such as changing the name, pattern or starter type, or adding services to your project. Run the following command:

```
bx dev edit
```
{: codeblock}
-->


### Run
{: #run}

Puede ejecutar la aplicación mediante el mandato `run`. Primero se completa una compilación contra el proyecto utilizando el elemento de configuración `build-cmd-run` como la instrucción de compilación. A continuación, se inicia el contenedor de ejecución y expone los puertos tal y como se define en `container-port-map`. `run-cmd` se puede utilizar para invocar la aplicación si el contenedor de ejecución no contiene un punto de entrada para completar este paso. 

Ejecute el siguiente mandato en el directorio del proyecto actual para iniciar la aplicación:

```
bx dev run
```
{: codeblock}

Para salir de la sesión, utilice `CTRL-C`.


#### Parámetros de ejecución
{: #run-parameters}

Los siguientes parámetros son exclusivos del mandato `run` y ayudan a gestionar la aplicación dentro del contenedor de ejecución.

##### `container-name-run`
{: #container-name-run}
	
* Nombre del contenedor para el contenedor de ejecución.
* Uso: `bx dev run container-name-run <projectName>`

##### `container-path-run`
{: #container-path-run}

* Ubicación en el contenedor para compartir en ejecución.
* Uso: `bx dev run container-path-run [/path/to/app]`

##### `host-path-run`
{: #host-path-run}

* Ubicación en el sistema host para compartir en el contenedor en ejecución.
* Uso: `bx dev run host-path-run [/path/to/app/bin]`

##### `dockerfile-run`
{: #dockerfile-run}

* Archivo Docker para el contenedor en ejecución.
* Uso: `bx dev run dockerfile-run [/path/to/Dockerfile.yml]`

##### `image-name-run`
{: #image-name-run}

* Imagen para crear desde dockerfile-run.
* Uso: `bx dev run image-name-run [/path/to/image-name]`

##### `run-cmd`
{: #run-cmd}

* Parámetro opcional utilizado para ejecutar código en el contenedor de ejecución. Este es opcional si su imagen iniciará la aplicación. 
* Uso: `bx dev run run-cmd [/the/run/command]`
	
### Status
{: #status}

Puede consultar el estado de los contenedores utilizados por {{site.data.keyword.dev_cli_short}} tal y como se definen en `container-name-run` y `container-name-tools`. 

Ejecute el siguiente mandato en el directorio del proyecto actual para comprobar el estado de los contenedores:

```
bx dev status
```
{: codeblock}


[Parámetros del mandato de estado](#command-parameters)


### Stop
{: #stop}

Puede detener un contenedor mediante el mandato `stop`. El parámetro `container-name` le permite especificar el contenedor que se debe detener. Si no se especifica, el mandato stop detiene el contenedor de ejecución definido por `container-name-run`. 

Ejecute el siguiente mandato en el directorio del proyecto actual para detener un contenedor:

```
bx dev stop
```
{: codeblock}


#### Parámetro de detención adicional: 
{: #stop-parameter}

##### `container-name`
{: #container-name}

* Nombre del contenedor para el contenedor de herramientas.
* Uso: `bx dev stop container-name <demo-tools>` 

### Test
{: #test}

Puede probar la aplicación a través del mandato `test`. Primero se completa una compilación contra el proyecto utilizando el elemento de configuración `build-cmd-run` como la instrucción de compilación. A continuación, el contenedor de herramientas se utiliza para invocar `test-cmd` para la aplicación.

Ejecute el siguiente mandato para probar la aplicación: 

```
bx dev test
```
{: codeblock}


[Parámetros del mandato de prueba](#command-parameters)


## Parámetros para crear, depurar, ejecutar y probar
{: #command-parameters}

Los siguientes parámetros se pueden utilizar junto con los mandatos `build|debug|run|test` y se pueden especificar a través de línea de mandatos y/o actualizando directamente el archivo `cli-config.yml` del proyecto. Hay disponibles parámetros adicionales para los mandatos [`debug`](#debug-parameters) y [`run`](#run-parameters), y están documentados en sus respectivos apartados. 

**Nota**: los parámetros de mandato especificados en la línea de mandatos tienen prioridad sobre la configuración `cli-config.yml`.

##### `container-name-tools`  
{: #container-name-tools}

* Nombre del contenedor para el contenedor de herramientas.
* Uso: `bx dev <build|debug|run|test> container-name-tools [<demo-tools>]`
 
##### `host-path-tools`
{: #host-path-tools}

* Ubicación en el host para compartir para la compilación, depuración, pruebas.
* Uso: `bx dev <build|debug|run|test> host-path-tools [/path/to/build/tools]`

##### `container-path-tools`
{: #container-path-tools}

* Ubicación en el contenedor para compartir para la compilación, depuración, pruebas.
* Uso: `bx dev <build|debug|run|test> container-path-tools [/path/for/build]`

##### `container-port-map`
{: #container-port-map}

* Correlaciones de puertos para el contenedor. El primer valor es el puerto que se utilizará en el sistema operativo del host, el segundo es el puerto del contenedor (host:container).
* Uso: `bx dev <build|debug|run|test> container-port-map [8090:8090,9090,9090]`

##### `dockerfile-tools`
{: #dockerfile-tools}

* Archivo Docker para el contenedor de herramientas.
* Uso: `bx dev <build|debug|run|test> dockerfile-tools [path/to/dockerfile]`

##### `image-name-tools`
{: #image-name-tools}

* Imagen para crear desde dockerfile-tools.
* Uso: `bx dev <build|debug|run|test> image-name-tools [path/to/image-name]`

##### `build-cmd-run`
{: #build-cmd-run}

* Mandato para generar código para todos los usos menos DEBUG.
* Uso: `bx dev <build|debug|run|test> build-cmd-run [some.build.command]`

##### `test-cmd`
{: #test-cmd}

* Mandato para probar código en el contenedor de herramientas.
* Uso: `bx dev <build|debug|run|test> test-cmd [/the/test/command]`

