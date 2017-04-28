---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Guía de aprendizaje del iniciador Web Basic
{: #tutorial}

En la siguiente guía de aprendizaje encontrará los pasos a seguir para crear un proyecto desde el iniciador Web Basic. Incluye la instalación de las herramientas necesarias y los pasos a seguir para ejecutar el código del proyecto. 

Puede crear un proyecto utilizando la [{{site.data.keyword.dev_console}}](#create-devex) basada en la web o la [{{site.data.keyword.dev_cli_notm}}](#create-cli) de mandatos.


## Instalación de herramientas del desarrollador
{: #dev_tools}

Asegúrese de instalar las [herramientas de desarrollador necesarias ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](get_code.html#prereq-dev-tools){: new_window}.


## Creación de un proyecto mediante la {{site.data.keyword.dev_console}}
{: #create-devex}

1. Cree un proyecto en la {{site.data.keyword.dev_console}} de {{site.data.keyword.Bluemix}}:

	1. En la página [**Iniciación** ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/developer/getting-started/) de la {{site.data.keyword.dev_console}}, pulse **Crear proyecto**.

		De forma alternativa, puede pulsar **Crear proyecto** desde la página **Proyectos**.

	2. Seleccione **App web** y pulse **Siguiente**.

	3. Seleccione **Basic Web** y pulse **Siguiente**.

	4. Especifique el nombre del proyecto. En esta guía de aprendizaje, utilizaremos `WebBasicProject`.   

	5. Especifique un nombre de host exclusivo. En esta guía de aprendizaje, utilizaremos `devhost` 

	6. Seleccione el lenguaje de la plataforma. En esta guía de aprendizaje, utilizaremos `Swift`.
   
	7. Pulse **Crear**.

2. Opcional: añada capacidad de datos:

	1. Pulse **Ver** para **Datos** en la página **Visión general del proyecto**.

      De forma alternativa, puede seleccionar **Crear** o **Añadir existente** en la página **Prestaciones > Data**.

   2. Especifique el nombre del servicio y pulse **Crear**.

3. Genere el código del proyecto:

	1. Pulse **Obtener el código** en la página **Visión general del proyecto** para seleccionar el lenguaje.
   
		Como alternativa, pulse la página **Código**.
      
	2. Pulse **Generar código**.
   
	3. Cuando se haya generado el código, pulse **Descargar código** para descargar el archivo del proyecto.

4. Empiece a trabajar con el proyecto descargado: 

	1. Expanda el archivo archivado. 
	
	2. Vaya al directorio del nuevo proyecto. 
	
	3. Utilice {{site.data.keyword.dev_cli_notm}} para continuar. 

5. Opcional: [Actualización del proyecto](project_overview_page.html#update_language) para generar un nuevo lenguaje.


## Creación de un proyecto mediante la {{site.data.keyword.dev_cli_notm}}
{: #create-cli}

1. Asegúrese de instalar [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. En la solicitud de terminal, vaya al directorio local que prefiera y ejecute el siguiente mandato.
  
	```
	bx dev create
	```
	{: codeblock}


3. Proporcione los siguientes valores cuando se le solicite:

	* Seleccione un patrón: 1 (para web)
	* Seleccione un iniciador: 1 (para Basic Web)
	* Seleccione un lenguaje: 2 (para Swift)
	* Especifique un nombre para el proyecto: `WebBasicProjectCLI`
	* Especifique un nombre de host para el proyecto: `myhost`

4. Si desea añadir servicios al proyecto, escriba `y` en la solicitud de preguntas y responda el resto de las preguntas.

5. Cuando `WebBasicProjectCLI` se haya guardado correctamente, vaya a la carpeta `WebBasicProjectCLI`.

6. Añada su propio código y ejecute el proyecto.
 
	1. Ejecute el proyecto con el siguiente mandato:
 
		```
		bx dev run
		```
		{: codeblock}


## Ejecución de un proyecto web
{: #run}

### Localmente
{: #local notoc}

1. Instale las dependencias del nodo:

  ```
  npm install
  ```
  {: codeblock}

2. Empaquete el código frontal en un módulo:

  ```
  node_modules/.bin/gulp
  ```
  {: codeblock}

3. Compile el servidor:

  ```
  swift build
  ```
  {: codeblock}

4. Ejecute la aplicación:

  ```
  .build/debug/WebBasicProjectCLI
  ```
  {: codeblock}

5. Abra el navegador en `http://localhost:8080`.


### Utilización de {{site.data.keyword.dev_cli_short}}
{: #dev notoc}

1. Instale las dependencias del nodo:

  ```
  npm install
  ```
  {: codeblock}

2. Empaquete el código frontal en un módulo:

  ```
  gulp
  ```
  {: codeblock}

3. Ejecute la compilación:

  ```
  bx dev run
  ```
  {: codeblock}

4. Abra el navegador en `http://localhost:8080`.


## Ejecución del proyecto en Xcode
{: #Xcode}

1. Cree un proyecto Xcode.

	Antes de poder desarrollar en Xcode, necesitará utilizar el gestor de paquetes de Swift para crear un proyecto Xcode.
	
	```
	swift project generate-xcodeproj
	```
	{: codeblock}

2. Cambie el destino activo por el ejecutable:

	A continuación, abra el proyecto en Xcode y asegúrese de que el destino activo sea el ejecutable. Puede mantener pulsada la tecla de opción mientras pulsa el menú desplegable para seleccionar el ejecutable activo deseado.

3. Pulse **ejecutar**.

4. Abra el navegador en `http://localhost:8080`.

