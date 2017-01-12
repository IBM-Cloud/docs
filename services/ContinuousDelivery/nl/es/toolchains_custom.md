---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Configuración de cadenas de herramientas personalizadas (Experimental)
{: #toolchains-custom}
Última actualización: 27 de Abril 2016
{: .last-updated}

La creación de una cadena de herramientas personalizada puede ayudarle a mejorar el flujo de trabajo de DevOps. Puede empezar a trabajar de forma rápida con una de las plantillas de cadena de herramientas existente, o puede personalizar una de las plantillas para crear una cadena de herramientas más adecuada como punto de partida.
{:shortdesc}

Existen muchas formas de [crear y desplegar una cadena de herramientas](https://daily-console.stage1.ng.bluemix.net/docs/toolchains/toolchains_setup.html){: new_window}. En esta guía se explican los pasos a seguir para crear una cadena de herramientas personalizada que se puede desplegar utilizando un botón [Desplegar en {{site.data.keyword.Bluemix_notm}}](https://daily-console.stage1.ng.bluemix.net/docs/develop/deploy_button.html){: new_window}. Después de algunas tareas de configuración, podrá compartir fácilmente un proyecto GitHub con una cadena de herramientas que podrá desplegar en {{site.data.keyword.Bluemix_notm}}.


## Iniciación
{: #toolchains_custom_gettingstarted}

Para crear una cadena de herramientas personalizada, empezaremos clonando una plantilla de cadena de herramientas. La clonación de una plantilla existente le proporciona un punto de partida desde el que empezar la personalización. 

1. Mediante el cliente Git que elija, escriba el siguiente mandato para clonar la plantilla [Cadena de herramientas simple](https://github.com/open-toolchain/simple-toolchain){: new_window} en GitHub.

 ```
 git clone https://github.com/open-toolchain/simple-toolchain.git
 ```
 {: pre}

 Esta plantilla despliega una aplicación Hello World básica desde un único repositorio GitHub e incluye una cadena de herramientas simple preconfigurada para entrega continuada, control de código fuente, seguimiento de problemas y edición en línea. 

2. **(Opcional)**: si prefiere comenzar con una plantilla de cadena de herramientas más compleja, puede clonar la [cadena de herramientas nativa de la nube para Microservices](https://github.com/open-toolchain/toolchain-demo){: new_window}.

 ```
 git clone https://github.com/open-toolchain/toolchain-demo.git
 ```
 {: pre}

 Esta plantilla despliega un almacén en línea que se compone de tres microservicios, cada uno contenido en su propio repositorio GitHub. También se incluye una cadena de herramientas más compleja que está preconfigurada para entrega continua, control de código fuente, despliegues blue-green, prueba funcional, seguimiento de problemas, edición en línea y mensajería. 

Independientemente de la plantilla que elija, los principios básicos que se describen en esta guía para crear un cadena de herramientas personalizada serán muy parecidos. 

Después de clonar la plantilla, tendrá un repositorio GitHub básico con un archivo *Readme* y un directorio `.bluemix` que contiene todos los archivos de configuración necesarios para hacer que la cadena de herramientas funcione. Como mínimo, el directorio `.bluemix` debe contener lo siguiente:

* toolchain.yml
* deploy.json
* pipeline.yml

Cada uno de estos archivos se explica en las secciones siguientes, junto con algunas configuraciones adicionales que quizás se deban añadir a medida que evoluciona la cadena de herramientas. 

## Visión general de los archivos de configuración
{: #toolchains_custom_config_files}

Los archivos de configuración de la cadena de herramientas se componen principalmente de archivos en formato YAML. Cada archivo contiene metadatos que describen distintos aspectos de la cadena de herramientas. Esto incluye información general sobre la cadena de herramientas, los repositorios GitHub que se van a incluir, detalles sobre cómo se debe crear y dónde se debe desplegar y detalles de configuración para las diversas herramientas que se incluirán en la cadena de herramientas. Conforme la cadena de herramientas pasa a ser más compleja, los archivos de configuración también se deben adaptar. Es importante que los archivos permanezcan bien formateados para reducir el riesgo de que se inserten errores. 

Estas son algunas directrices a tener en cuenta cuando se trabaja con un archivo YAML: 

* No se permiten tabuladores. Solo se deben utilizar espacios. 
* Todas las propiedades y listas debe especificarse con un sangrado de uno o varios espacios.
* Todas las claves y propiedades son sensibles a mayúsculas y minúsculas.

Para comprobar su trabajo, se recomienda utilizar un sencillo validador de YAML como este [Analizador YAML](http://wiki.ess3.net/yaml/){: new_window} para evitar este tipo de errores.

  
## toolchain.yml
{: #toolchains_custom_toolchain_yml}

El archivo `toolchain.yml` es la base de la cadena de herramientas. Las características específicas de la cadena de herramientas, incluidos repositorios que obtener, servicios que incluir y detalles de la compilación, se describen en este archivo. Para facilitar la estructura de su contenido, se puede dividir en varias secciones.

1\. **Información de introducción de la cadena de herramientas:**

 En esta sección se proporcionan detalles sobre la cadena de herramientas que se presentan al usuario en la página de creación de la cadena de herramientas. Debe incluir un nombre para la cadena de herramientas, junto con una descripción que explique la finalidad de la cadena de herramientas o qué hará cuando se despliegue. También se puede incluir una imagen para mostrar un logotipo o una representación visual de la cadena de herramientas.

 Además de proporcionar contenido de introducción para su cadena de herramientas, esta sección también incluye una clave denominada `required` que define las integraciones de herramientas que se pueden configurar en el momento de la creación en la página de creación de la cadena de herramientas. El hecho de permitir que una herramienta se configure en el momento de la creación le permite crear una cadena de herramientas que se puede reutilizar fácilmente. Para cada herramienta que se puede configurar en la página de creación de la cadena de herramientas, añada la clave padre de la herramienta definida en el archivo `toolchain.yml` como propiedad de la clave `required`. 

 Este fragmento de código muestra un ejemplo de esta sección:

 ```
 ---
 name: "Simple Toolchain"
 description: "This Hello World application uses Node.js and includes a toolchain that is preconfigured for continuous delivery, source control, issue tracking, and online editing.\n\nTo get started, click **Create**."
 version: 0.1
 # Generate base64 representation of image at http://www.askapache.com/online-tools/base64-image-converter/
 image: data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAY4AAA...
 required:
  - deploy
  - hello-world-repo
  ```
 {: codeblock}

 **Nota:** Las imágenes deben convertirse primero a una representación de base 64 mediante una herramienta como [AskApache](http://www.askapache.com/online-tools/base64-image-converter/).

2\. **Definiciones del repositorio GitHub:**

 Una cadena de herramientas puede proporcionar entrega continua para tantos repositorios GitHub como se desee. Cada repositorio se debe definir en esta sección del archivo `toolchain.yml`. 

 Para empezar, para cada repositorio GitHub que se vaya a añadir a la cadena de herramientas, añadir una clave padre que represente el nombre del repositorio GitHub con las siguientes propiedades:

| Elemento | Clave/propiedad | Valor | Descripción |
|------|--------------|-------|-------------|
| repo-name | clave |  | Nombre reposit. |
| service_id | propiedad | <`githubpublic` , `githubprivate`> | Tipo repositorio GitHub   |
| parameters: | clave |  |  |
| repo_name | propiedad |  | **COMMENT:  Cómo se debe definir     ** |
| repo_url | propiedad |  | URL del reposit. GitHub      |
| type | propiedad | <`new` , `fork` , `clone` , `link`> | Cómo se debe crear el repositorio |
| has_issues | propiedad | <`true` , `false`> | Problemas de uso de GitHub |

 **Nota:** Si define varios repositorios y los configura como `has_issues: true`, solo se añadirá una instancia del rastreador de problemas de GitHub a la cadena de herramientas que realizará el seguimiento de los problemas de todos los repositorios establecidos en `true`.

 Este fragmento de código muestra un ejemplo de esta sección:

 ```
 # Github repos
 hello-world-repo:
   service_id: githubpublic
   parameters:
 	repo_name: "hello-world-{{name}}"
 	repo_url: https://github.com/open-toolchain/node-hello-world
 	type: clone
 	has_issues: true
 ```
 {: codeblock}

3\. **Información del conducto: **

 La entrega continua es posible gracias del conducto. En esta sección se definen los detalles de configuración que se utilizan para crear y desplegar el código en cada uno de los repositorios GitHub. 

 Para empezar, para cada repositorio GitHub que se haya definido en la cadena de herramientas, añada una clave padre que represente el nombre de su conducto. Se recomienda deducir esta clave a partir del nombre del repositorio GitHub. Añada las siguientes propiedades: 

| Elemento | Clave/propiedad | Valor | Descripción |
|------|--------------|-------|-------------|
| pipeline-name | clave |  | Nombre del conducto |
| service_id | propiedad | <`pipeline`> | Nombre del servicio que se va a utilizar |
| parameters | clave |  |  |
| name | propiedad | <`repo_name`> | Igual que el nombre definido en la sección del repos. #Github |
| ui-pipeline | propiedad | <`true` , `false`> |  |
| configuration | clave |  |  |
| content | propiedad | <`$file(pipeline.yml)`> | Archivo que contiene la definición del conducto |
| env | clave |  |  |
| REPO_NAME | clave | <`repo-name-key`> | Mismo nombre que la clave padre del repositorio GitHub |
| CF_APP_NAME |  propiedad | <`"{{deploy.parameters.repo-name-key}}"`> | Nombre que utiliza Cloud Foundry.  Debe incluir el nombre de la clave padre del repositorio GitHub |
| PROD_SPACE_NAME | propiedad | <`"{{deploy.parameters.prod-space}}"`> | Nombre del espacio de {{site.data.keyword.Bluemix_notm}} en el que se va a desplegar |
| PROD_ORG_NAME | propiedad | <`"{{deploy.parameters.prod-organization}}"`> | Nombre de la organización de {{site.data.keyword.Bluemix_notm}} en la que se va a desplegar |
| PROD_REGION_ID | propiedad | <`"{{deploy.parameters.prod-region}}"`> | Nombre de la región de {{site.data.keyword.Bluemix_notm}} en la que se va a desplegar |
| execute | propiedad | <`true` , `false`> | Iniciar conducto después de la creación |
| services | propiedad | <`repo-name-key`> |  Clave padre del repositorio GitHub |
| hidden | propiedad | <`[form, description]`> |  |

 Encontrará información sobre cómo crear un archivo `pipeline.yml` en una [sección posterior](#toolchains_custom_pipeline_yml)

 Este fragmento de código muestra un ejemplo de esta sección:

 ```
 # Pipelines
 hello-world-build:
   service_id: pipeline
   parameters:
 	name: "hello-world-{{name}}"
 	ui-pipeline: true
 	configuration:
 	 content: $file(hello-world.pipeline.yml)
 	 env:
 	  HELLO_WORLD_REPO: "hello-world-repo"
 	  CF_APP_NAME: "{{deploy.parameters.hello-world-name}}"
 	  PROD_SPACE_NAME: "{{deploy.parameters.prod-space}}"
 	  PROD_ORG_NAME: "{{deploy.parameters.prod-organization}}"
 	  PROD_REGION_ID: "{{deploy.parameters.prod-region}}"
 	 execute: true
 	services: ["hello-world-repo"]
   hidden: [form, description]
 ```
 {: codeblock}

4\. **Destalles del despliegue:**

 Como parte del proceso de entrega continua, una cadena de herramientas se puede configurar de modo que despliegue la aplicación en cualquier región, organización o espacio de {{site.data.keyword.Bluemix_notm}} al que tenga acceso el usuario que despliega la cadena de herramientas. Los detalles específicos sobre dónde desplegar la aplicación se pueden puede seleccionar en la página de creación de la cadena de herramientas.   

 ![Valores de configuración del conducto de entrega](images/deploy_configuration.png)

 En esta sección del archivo `toolchain.yml` se definen las etapas del conducto que se puede configurar en la página de creación de la cadena de herramientas. 

 Para empezar, se utiliza la clave padre `deploy` para identificar las propiedades de configuración del despliegue. Las siguientes propiedades componen el resto de la sección:

| Elemento | Clave/propiedad | Valor | Descripción |
|------|--------------|-------|-------------|
| desplegar | clave |  | Nombre de la sección de despliegue |
| schema | propiedad | <`deploy.json`> | Archivo que define el diseño de la IU para configurar los detalles del despliegue |
| service-category | propiedad | <`pipeline`> | Servicio que utilizará las configuraciones de despliegue |
| parameters | clave |  |  |
| prod-region | propiedad | <`"{{region}}"`> | Define la región de {{site.data.keyword.Bluemix_notm}} para la etapa de producción |
| prod-organization | propiedad | <`"{{organization}}"`> | Define la organización de {{site.data.keyword.Bluemix_notm}} para la etapa de producción |
| prod-space | propiedad | <`prod`> | Define el espacio de {{site.data.keyword.Bluemix_notm}} para la etapa de producción |
| github-repo-name | propiedad | <`"{{repo-name-key.parameters.repo_name}}"`> | Variable para pasar el nombre del repositorio GitHub a la página de creación de la cadena de herramientas |

 Encontrará información sobre cómo crear un archivo `deploy.json` en una [sección posterior](#toolchains_custom_deploy_json)

 En el ejemplo siguiente se define una sola etapa que se despliega en un entorno de producción.

 ```
 #Deployment
 deploy:
   schema: deploy.json
   service-category: pipeline
   parameters:
 	prod-region: "{{region}}"
 	prod-organization: "{{organization}}"
 	prod-space: prod
 	hello-world-name: "{{hello-world-repo.parameters.repo_name}}"
 ```
 {: codeblock}

 Básicamente el ejemplo de código se puede utilizar tal cual y sólo requiere una ligera modificación. Para personalizar esta sección, se debe actualizar `github-repo-name` para que se ajuste al nombre del repositorio. Los detalles del archivo [`deploy.json`](#toolchains_custom_deploy_json) también se tienen que actualizar. 

 Para crear un conducto más complejo que incluye una fase de desarrollo, control de calidad y producción, se pueden sustituir las siguientes propiedades bajo la clave `parameters`. 

 ```
   parameters:
 	dev-region: "{{region}}"
 	qa-region: "{{region}}"
 	prod-region: "{{region}}"
 	dev-organization: "{{organization}}"
 	qa-organization: "{{organization}}"
 	prod-organization: "{{organization}}"
 	dev-space: dev
 	qa-space: qa
 	prod-space: prod
 ```
 {: codeblock}

5\. **Configuraciones de la herramienta**

 Después de configurar los componentes principales de la cadena de herramientas, puede empezar a incluir otras integraciones de la herramienta que le ayudará a añadir más funcionalidad y utilidad a la cadena de herramientas. En todas las herramientas se debe añadir una entrada al archivo `toolchain.yml`, y algunas también necesitarán un archivo de configuración YAML que se debe crear en el directorio `.bluemix`. 

 * **Slack**

	toolchain.yml
	```
	messaging:
	  service_id: slack
	  include: slack.yml
	```
	{: codeblock}
	
	slack.yml
	```
	---
	parameters:
	  api_token: ""
	  channel_name: ""
	```
	{: codeblock}
	
 * **Sauce Labs**

	toolchain.yml
	```
	test:
	  service_id: saucelabs
	  include: saucelabs.yml
	```
	{: codeblock}
	
	saucelabs.yml
	```
	---
	parameters:
	  username: ""
	  key: ""
	```
	{: codeblock}
	
 * **PagerDuty**

	toolchain.yml
	```
	alerting:
	  service_id: pagerduty
	  include: pagerduty.yml
	```
	{: codeblock}

	pagerduty.yml
	```
	---
	parameters:
	  site_name: ""
	  api_key: ""
	  service_name: ""
	  user_email: ""
	  user_phone: ""
	```
	{: codeblock}
	
 * **Eclipse Orion Web IDE**

	toolchain.yml
	```
	webide:
	  service_id: orion
	```
	{: codeblock}


## pipeline.yml
{: #toolchains_custom_pipeline_yml}

El archivo `pipeline.yml` contiene todos los detalles de la configuración correspondientes a las etapas del conducto. El archivo `pipeline.yml` se puede crear de dos maneras. 

1. Cree el archivo `pipeline.yml` manualmente. Encontrará los detalles y la sintaxis para crear el archivo `pipeline.yml` en el apartado [Compartición de conductos en proyectos de ejemplo de DevOps Services](https://new-console.ng.bluemix.net/docs/develop/sharetextpipelines.html){: new_window}.

2. Genere el archivo `pipeline.yml` a partir de un proyecto existente de DevOps Services. Para ello: 
	
	1. Cree un nuevo [proyecto de DevOps Services](https://hub.jazz.net/create){: new_window}.
	
	2. Abra el proyecto y pulse **Creación y despliegue**
	
	3. Configure todas las etapas necesarias para el conducto.
	
	4. En la barra de direcciones del navegador, añada `/yaml` al URL del proyecto y pulse Intro.
	
	5. Guarde el archivo `pipeline.yml` resultante en el directorio `.bluemix` del repositorio GitHub.

Si la cadena de herramientas contiene más de un conducto, proporcione nombres exclusivos para cada archivo `pipeline.yml`. 

A continuación puede ver un ejemplo de archivo `pipeline.yml`:

```
---
stages:
- name: BUILD
  inputs:
  - type: git
	branch: master
	service: ${HELLO_WORLD_REPO}
  triggers:
  - type: commit
  jobs:
  - name: Build
	type: builder
- name: DEPLOY
  inputs:
  - type: job
	stage: BUILD
	job: Build
  triggers:
  - type: stage
  properties:
  - name: CF_APP_NAME
	value: undefined
	type: text
  - name: APP_URL
	value: undefined
	type: text
  jobs:
  - name: Deploy
	type: deployer
	target:
	  region_id: ${PROD_REGION_ID}
	  organization: ${PROD_ORG_NAME}
	  space: ${PROD_SPACE_NAME}
	  application: ${CF_APP_NAME}
	script: |
	  #!/bin/bash
	  # Push app
	  export CF_APP_NAME="$CF_APP"
	  cf push "${CF_APP_NAME}"
	  export APP_URL=http://$(cf app $CF_APP_NAME | grep urls: | awk '{print $2}')
	  # View logs
	  #cf logs "${CF_APP_NAME}" --recent
```
{: codeblock}		


## deploy.json
{: #toolchains_custom_deploy_json}

En la página de creación de la cadena de herramientas, cuando se seleccionas Delivery Pipeline en la sección Integraciones configurables, la sección se expande para mostrar los siguientes elementos que se pueden configurar para la herramienta:

	* El nombre de la aplicación
	* La región, la organización y el espacio en los que se desplegarán las etapas del conducto. 

![Valores de configuración del conducto de entrega](images/deploy_configuration.png)

El diseño de esta sección en la interfaz de usuario se define mediante el esquema `deploy.json`. 

Dentro del esquema, se deben actualizar las siguientes propiedades para que se ajusten a los detalles de la aplicación:

	* Título
	* Descripción
	* Descripción larga
	* Todas las instancias de `hello-world-name` y los detalles asociados se deben modificar para que se ajusten a la aplicación. 

A continuación puede ver un ejemplo de archivo `deploy.json`:

```
{
    "$schema": "http://json-schema.org/draft-04/schema#",
    "title": "Hello World Deploy Stage",
    "description": "hello-world simple toolchain",
    "longDescription": "The Delivery Pipeline for Devops Services allows you to automate your continuous deployment setup hello-world.",
    "type": "object",
    "properties": {
        "prod-region": {
            "description": "The bluemix region",
            "type": "string"
        },
        "prod-organization": {
            "description": "The bluemix org",
            "type": "string"
        },
       "prod-space": {
            "description": "The bluemix space",
            "type": "string"
        },
       "hello-world-name": {
            "description": "hello world app name",
            "type": "string"
        }
    },
    "required": ["prod-region", "prod-organization", "prod-space", "hello-world-name"],
    "form": [
       {
          "type": "validator",
          "url": "/devops/setup/bm-helper/helper.html"
       },        
        {
          "type": "text",
          "readonly": false,
          "title": "Hello World App Name",
          "key": "hello-world-name"
        },
        {
            "type": "table",
            "columnCount": 4,
            "widths": ["15%", "28%", "28%", "28%"],
            "items": [
                {
                  "type": "label",
                  "title": ""
                },
                {
                  "type": "label",
                  "title": "Region"
                },
                {
                  "type": "label",
                  "title": "Organization"
                },
                {
                  "type": "label",
                  "title": "Space"
                },
                {
                  "type": "label",
                  "title": "Prod Stage"
                },
                {
                  "type": "select",
                  "key": "prod-region"
                },
                {
                  "type": "select",
                  "key": "prod-organization"
                },
                {
                  "type": "select",
                  "key": "prod-space",
                  "readonly": false
                }
            ]
        }
    ]
}
```
{: codeblock}
