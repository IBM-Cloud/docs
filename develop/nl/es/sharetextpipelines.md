---

copyright:
  years: 2015, 2016
lastupdated: "2016-12-21"

---

{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Compartición de conductos en proyectos de ejemplo de {{site.data.keyword.jazzhub_short}} {: #share-pipeline}

Para proyectos de ejemplo desplegados en {{site.data.keyword.Bluemix_notm}} por medio del botón Desplegar en {{site.data.keyword.Bluemix_notm}}, puede definir las configuraciones de interconexión (conductos) de {{site.data.keyword.jazzhub_short}} como archivos YAML. Los conductos definidos como texto se pueden compartir, de forma que las personas que bifurcan (fork) su proyecto no tengan que configurar sus propios conductos. Esta característica está en desarrollo: el formato de YAML y la implementación podrían cambiar en cualquier momento. Actualmente, esta característica solo está disponible para proyectos con repositorios Git y GitHub cuyo objetivo sea {{site.data.keyword.Bluemix_notm}}. 
{: shortdesc} 

En el directorio raíz de proyecto del ejemplo, debe tener una carpeta con el nombre `.bluemix` que contenga un archivo `pipeline.yml`.

Cuando se clona un proyecto utilizando el botón Desplegar en {{site.data.keyword.Bluemix_notm}}, {{site.data.keyword.jazzhub_short}} crea un conducto basado en el archivo `pipeline.yml`. 

Ejemplo: 
``` 
<sample root>
	.bluemix
		pipeline.yml
	<other sample content>
```
{: codeblock} 

El formato del archivo YAML es un único documento YAML que contiene una especificación de conducto. En el ejemplo siguiente de conducto de {{site.data.keyword.jazzhub_short}} se crea una app Java con Ant en una fase. A continuación, en otra fase, el conducto despliega la app en {{site.data.keyword.Bluemix_notm}}. 

``` 
---
stages:
- name: Build Stage
  inputs:
  - type: git
    branch: master
  triggers:
  - type: commit
  properties:
  - name: APP_VERSION
    value: '1.0'
    type: text
  jobs:
  - name: Build
    type: builder
    artifact_dir: output
    build_type: ant
    script: |-
      #!/bin/bash
      ant
    enable_tests: true
    test_file_pattern: tests/TEST-*.xml
- name: Deploy Stage
  inputs:
  - type: job
    stage: Build Stage
    job: Build
  triggers:
  - type: stage
  jobs:
  - name: Deploy to dev
    type: deployer
    target:
      url: https://api.ng.bluemix.net
      organization: uateam@ca.ibm.com
      space: dev
      application: JavaSampleUnitTest
    script: |
      cf push "${CF_APP}"
      # View logs
      #cf logs "${CF_APP}" --recent
```
{: codeblock} 

##Sintaxis del archivo YAML {: #yaml-syntax}

Los conductos se pueden representar textualmente mediante la sintaxis siguiente.

Pipeline:
```
---
stages:
<sequence of stages>
```
{: codeblock} 

Stage: 
```
---
name: <name>
[inputs:
	<sequence of inputs>]
[triggers:
	<sequence of triggers>]
[properties:
	<sequence of properties>]
[jobs:
	<sequence of jobs>]
```
{: codeblock} 

Input:
```
type: 'git' | 'job'
[branch: <branch name>] ;only for Git inputs
stage: <stage name>		  ;only for job inputs
job: <job name>			   	;only for job inputs
```
{: codeblock} 

Trigger:
```
type: 'commit' | 'stage'
[enabled: 'true | 'false'] ;true is assumed if not specified
```
{: codeblock} 	
	
Property:
```
name: <property name>
value: <property value>
[type: 'text' | 'secure' | 'text_area' | 'file'] ;text is assumed if not specified
```
{: codeblock} 

Job:
```
[name: <job name>]
type: 'builder' | 'deployer' | 'tester'
fail_stage: 'true' | 'false'
[extension_id: <extension id>] ;extension jobs only
[working_dir: <working dir path>] ;builder and tester only
[artifact_dir: artifact path>] ;builder only
[build_type: <build type>] ;builder only
[script: <script>] ;not for extension jobs
[enable_tests: 'true' | 'false'] ;builder and tester only
[test_file_pattern: <pattern>] ;builder and tester only
[target: <target>] ;deployer and extension jobs only
*[<extension property name>: <value>] ;extension jobs only
```
{: codeblock} 

Target:
```
url: <target url>
organization: <org name>
space: <space name>
[application: <application name>]
```
{: codeblock} 

##Trabajos y definiciones de extensión {: #extension-jobs} 

Las definiciones de extensión definen un conjunto de propiedades que están disponibles para los trabajos de extensión. Un trabajo se trata como un trabajo de extensión cuando se especifica la propiedad `extension_id`. Para averiguar qué propiedades están disponibles para una extensión consulte su documentación. 

##Interacción con conductos mediante el uso de un archivo YAML {: #pipeline-yaml} 

**VARIABLES DE ENTORNO Y RESOLUCIÓN** 
<!-- Formating for this? -->

Antes de crear el conducto desde un archivo `pipeline.yml`, la función Desplegar en {{site.data.keyword.Bluemix_notm}} sustituye cualquier variable de entorno del archivo por la información que especifique en la interfaz de {{site.data.keyword.Bluemix_notm}} (por ejemplo, su organización). Los valores de YAML se sustituyen solo si únicamente constan de una variable de entorno. 

```
{
  "project_id": "_ljkahfliasdlk",
  "env": {
     "CF_ORGANIZATION" : "user@se.ibm.com"
  },
  "config": {
    "format" : "yaml",
    "content" : "
      ...
        target:
          url: http://api.ng.bluemix.net
          organization: ${CF_ORGANIZATION}
        script: \"echo ${CF_ORGANIZATION}\"                
      ...
    "
  }
}
```
{: codeblock} 

En dicho ejemplo, la organización de destino se resuelve contra el URL de destino, y el valor que persiste en la configuración de interconexión es el GUID de la organización. La aparición dentro del script de despliegue no se sustituye.

El URL de destino se debe especificar como una variable de entorno o un valor real, y o bien se deben especificar los GUID o los nombres de organización y espacio. Si se proporciona un valor, el otro se sustituye.

Variable | Descripción 
---------------- | ---------------- 
CF_TARGET_URL |	URL objetivo de Bluemix
CF_ORGANIZATION	| Nombre de org.
CF_ORGANIZATION_ID	| GUID de org.
CF_SPACE |	Nombre de espacio
CF_SPACE_ID |	GUID de espacio
CF_APP	| Nombre de app

{: caption="Table 1. Environment variables" caption-side="top"}

**GENERACIÓN DE UN ARCHIVO YAML DESDE UN CONDUCTO** 

Puede generar un archivo YAML desde un conducto. 

Genere el archivo a partir de un conducto existente con URL con el siguiente formato:

```
<DevOps Services domain>/pipeline/user/project/yaml
```
{: codeblock} 

Esta llamada no precisa de una cabecera de aceptación (accept). Puede utilizar esta llamada desde un navegador. 

**Nota:** Por motivos de seguridad, los valores de la propiedad del entorno secure-stage se omiten de los archivos YAML generados del conducto. 
