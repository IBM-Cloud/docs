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
{:note:.deprecated}

# Resolución de problemas
{: #ts}

Se documentan algunos problemas conocidos con el {{site.data.keyword.dev_cli_notm}}, junto con sus soluciones temporales.
{:shortdesc}

<!-- Add a headings and paragraphs about troubleshooting for your service, or a list of known issues and workarounds. -->

## Problemas conocidos
{: #knownissues}

En las secciones siguientes se describen problemas conocidos y posibles soluciones.


### El nombre de host da un error al crear un proyecto con un patrón no móvil
{: #hostname}

Es posible que le aparezca el siguiente error si utiliza {{site.data.keyword.dev_cli_short}} para crear un proyecto desde los patrones de app web, BFF o microservicio:

```
El nombre de host <myHostname> ya se ha utilizado.
```
{: codeblock}


#### Motivo
{: #hostname-cause}
   
Este error se debe a una señal de inicio de sesión caducada.


#### Resolución 
{: #hostname-resolution}

Vuelva a iniciar la sesión. 

```
bx login
```
{: codeblock}


### Fallos generales con el {{site.data.keyword.dev_cli_short}}
{: #general}

Es posible que le aparezca el siguiente error si utiliza los mandatos crear, suprimir, listar o codificar de {{site.data.keyword.dev_cli_short}}:

```
No se ha podido <command> el proyecto.
```
{: codeblock}


#### Motivo
{: #hostname-cause}
   
Este error se debe a una señal de inicio de sesión caducada.


#### Resolución 
{: #hostname-resolution}

Vuelva a iniciar la sesión. 

```
bx login
```
{: codeblock}


### Error de intermediario de servicio al añadir la prestación de {{site.data.keyword.objectstorageshort}}
{: #os}

Es posible que le aparezca el siguiente error si utiliza {{site.data.keyword.dev_cli_short}} para crear dos proyectos con la prestación {{site.data.keyword.objectstorageshort}}:

```
FALLIDO
Error de intermediario de servicio: {"description"=>"No puede crear esta instancia de Object Storage. Todas las organizaciones que utilicen el servicio de Object Storage están limitadas a unan instancia del plan gratuito."}
```
{: codeblock}


#### Motivo
{: #os-cause}
   
Este error se debe al servicio de {{site.data.keyword.objectstorageshort}} que permite solo una instancia del plan de {{site.data.keyword.objectstorageshort}} gratuito.


#### Resolución 
{: #os-resolution}

Se le solicitará que elija otro plan para evitar este error.


### Erro al obtener el código durante la creación del proyecto
{: #code}

Es posible que le aparezca el siguiente error si utiliza {{site.data.keyword.dev_cli_short}} para crear un proyecto:
	
```
FALLIDO
Se ha creado el proyecto, pero no se ha podido obtener el código
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
	

#### Motivo
{: #code-cause}

Este error se debe a un tiempo de espera interno excedido. 
	

#### Resolución 
{: #code-resolution}

Puede obtener el código de una de las siguientes formas:

* Ejecute el siguiente mandato utilizando la CLI:

	```
	bx dev code <your-project-name>
	```
	{: codeblock}
	
	`<your-project-name>` debe sustituirse por el nombre de proyecto que ha utilizado durante la creación del proyecto.

* Utilice la {{site.data.keyword.dev_console}}.

	1. Seleccione el [proyecto ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](https://console.{DomainName}/developer/projects) en la {{site.data.keyword.dev_console}} y pulse **Obtener el código**.

	2. Pulse **Generar código**.

	3. Después de generar el código, pulse **Descargar código**.


### Error al ejecutar `bx dev run` para proyectos de Node.js 
{: #node}

Es posible que le aparezca el siguiente error si ejecuta `bx dev run` con {{site.data.keyword.dev_cli_short}} para proyectos web o BFF de Node.js:

```
module.js:597
  return process.dlopen(module, path._makeLong(filename));
                 ^

Error: /app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/appmetrics.node: invalid ELF header
    at Error (native)
    at Object.Module._extensions..node (module.js:597:18)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)

    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/index.js:25:13)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
```
{: codeblock}


#### Motivo
{: #node-cause}
   
Este error se debe a que el módulo `appmetrics` se ha instalado en otra arquitectura. Los módulos npm nativos instalados en una arquitectura no funcionarán en otra. Las imágenes de Docker incluidas se basan en el kernel de Linux.


#### Resolución 
{: #node-resolution}

Suprima la carpeta `node_modules` y vuelva a ejecutar `bx dev run`.


<!--
## Troubleshooting techniques
{: #tstechniques}
-->

<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->


## Obtención de ayuda y soporte
{: #gettinghelp}

Si tiene problemas o preguntas sobre el uso de la {{site.data.keyword.dev_console}} de {{site.data.keyword.Bluemix_notm}} o {{site.data.keyword.dev_cli_notm}}, puede obtener ayuda buscando información o formulando preguntas a través de un foro. También puede abrir una incidencia de soporte.

Cuando utilice los foros para formular preguntas, etiquete la pregunta de modo que los equipos de desarrollo de {{site.data.keyword.Bluemix_notm}} la vean. 

<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->

Si tiene preguntas técnicas sobre el desarrollo o el despliegue de una aplicación con la {{site.data.keyword.dev_console}} o {{site.data.keyword.dev_cli_notm}}:

* Publique la pregunta en [Stack Overflow ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://stackoverflow.com/search?q=bluemix-dev-services+ibm-bluemix) y etiquete la pregunta con `bluemix-dev-services` e `ibm-bluemix`.
* Publique la pregunta en [Slack ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://ibm-cloud-tech.slack.com/) en el canal `bluemix-dev-services`. [Inicie sesión en ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](http://ibm.biz/IBMCloudNativeSlack) hoy mismo.


<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
<!--
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/bluemix-dev-services/?smartspace=bluemix) forum. Include the  "bluemix-dev-services" and "bluemix" tags.
* -->

Consulte [Obtención de ayuda ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](/docs/support/index.html#getting-help) para obtener más información detallada sobre el uso de los foros.

Para obtener información sobre cómo abrir una incidencia de soporte de {{site.data.keyword.IBM}}, o sobre los niveles de soporte y gravedades de las incidencias, consulte [Cómo obtener soporte ![Icono de enlace externo](../icons/launch-glyph.svg "Icono de enlace externo")](/docs/support/index.html#contacting-support).

<!--Add a heading and content for how to get help. (Support not available for experimental.) Use this template for experimental services:  -->

