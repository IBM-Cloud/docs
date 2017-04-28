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

# Guía de aprendizaje del iniciador BFF Basic
{: #tutorial}

En la siguiente guía de aprendizaje encontrará los pasos a seguir para crear un proyecto desde el iniciador BFF Basic Starter, incluidas las herramientas que debe tener instaladas y, por lo tanto, los pasos para ejecutar el código del proyecto.

Tiene la opción de crear un proyecto utilizando la [{{site.data.keyword.dev_console}}](#create-devex) basada en la web o la [{{site.data.keyword.dev_cli_notm}}](#create-cli) de mandatos.

## Instalación de herramientas del desarrollador
{: #dev_tools}

Asegúrese de haber instalado las [herramientas de desarrollador necesarias ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](get_code.html#prereq-dev-tools){: new_window}.


## Creación de un proyecto mediante la {{site.data.keyword.dev_console}}
{: #create-devex}

1. Cree un proyecto en la {{site.data.keyword.dev_console}} de {{site.data.keyword.Bluemix}}.

	1. En la página [**Iniciación** ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://console.ng.bluemix.net/developer/getting-started/) de la {{site.data.keyword.dev_console}}, pulse **Crear proyecto**.

		De forma alternativa, puede pulsar **Crear proyecto** desde la página **Proyectos**.

	2. Seleccione **Programa de fondo para programa de usuario** y pulse **Siguiente**.

	3. Seleccione **Programa de fondo básico** y pulse **Siguiente**.

	4. Especifique el nombre del proyecto. En esta guía de aprendizaje, utilizaremos `BFFProject`.   

	5. Especifique un nombre de host exclusivo. En esta guía de aprendizaje, utilizaremos `devhost` 

	6. Seleccione el lenguaje de la plataforma. En esta guía de aprendizaje, utilizaremos `Node`.
   
	7. Pulse **Crear**.

2. Opcional: Añada la capacidad de Datos.

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


## Creación de un proyecto mediante {{site.data.keyword.dev_cli_notm}}
{: #create-cli}

1. Asegúrese de haber instalado [{{site.data.keyword.dev_cli_short}}](dev_cli.html).

2. En la solicitud de terminal, vaya al directorio local que prefiera y ejecute el siguiente mandato.
  
	```
	bx dev create
	```
	{: codeblock}
	
3. Proporcione los siguientes valores cuando se le solicite:

	* Seleccione un patrón: 3 (para Programa de fondo para programa de usuario)
	* Seleccione un iniciador: 1 (para Programa de fondo básico)
	* Seleccione un lenguaje: 1 (para Node)
	* Especifique un nombre para el proyecto: `BFFProjectCLI`
	* Especifique un nombre de host para el proyecto: `myhost`

4. Si desea añadir servicios al proyecto, escriba `y` en la solicitud de preguntas y responda el resto de las preguntas.

5. Cuando `BFFProjectCLI` se haya guardado correctamente, vaya a la carpeta `BFFProjectCLI`.

6. Añada su propio código y ejecute el proyecto.
 
	1. Ejecute el proyecto con el siguiente mandato:

 		```
		bx dev run
		```
		{: codeblock}


## Ejecución de un proyecto de BFF
{: #running-bff}

### Localmente
{: #bff-local}

1. Compile el servidor:

  ```
  swift build
  ```
  {: codeblock}

2. Ejecute la aplicación. Por ejemplo, suponiendo que su aplicación se llama `MyServer`:

  ```
  .build/debug/MyServer
  ```
  {: codeblock}

3. Puede ejecutar curl en el servidor con `curl http://localhost:8080`.


### Utilización del plugin de Bluemix
{: #using-blumix}

1. Ejecute la compilación:

	```
	bx dev run
	```
	{: codeblock}

2. Puede ejecutar curl en el servidor con: 
  
	```
	curl http://localhost:8080
	```
	{: codeblock}
