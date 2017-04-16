---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Iniciación a {{site.data.keyword.deliverypipeline}} {: #delivery-pipeline}  

Última actualización: 15 de septiembre de 2016
{: .last-updated}

Para automatizar las compilaciones y los despliegues en {{site.data.keyword.Bluemix}}, utilice el IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Esta información se aplica tanto a {{site.data.keyword.deliverypipeline}} como a {{site.data.keyword.deliverypipeline}} Next.

Con el servicio de {{site.data.keyword.deliverypipeline}}, puede elegir entre varios tipos de compilación. Proporcione el script de compilación y {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} lo ejecutará; no es necesario configurar sistemas de compilación. A continuación, con un solo clic puede desplegar automáticamente su app en uno o más espacios de {{site.data.keyword.Bluemix_notm}}, servidores de Cloud Foundry públicos o contenedores Docker en IBM Containers for {{site.data.keyword.Bluemix_notm}}.  

Los trabajos de compilación compilan y empaquetan el código fuente de su app desde repositorios gestión de control de origen (SCM) Git o Jazz. Los trabajos de compilación generan artefactos desplegables, como archivos WAR o contenedores Docker para IBM Containers. Además, puede ejecutar automáticamente pruebas de unidad en su compilación. Cada vez que cambia el código fuente, se desencadena una compilación.

Un trabajo de despliegue toma la salida de un trabajo de compilación y lo despliega en IBM Containers o en servidores de Cloud Foundry como {{site.data.keyword.Bluemix_notm}}.  

Puede desplegar en una o más regiones y servicios. Por ejemplo, puede configurar el servicio de {{site.data.keyword.deliverypipeline}} de forma que los artefactos de desarrollo utilicen IBM Containers, que se prueben en una región y que se desplieguen en producción en varias regiones. Para obtener más información, consulte [Regiones](../../overview/index.html#ov_intro__reg).

Hay varias formas para crear un conducto, incluida la adición de un conducto a una aplicación existente y la creación de un conducto sin una aplicación existente. Si aún no tiene un servicio de {{site.data.keyword.deliverypipeline}} en la organización, puede ir al catálogo, pulsar {{site.data.keyword.deliverypipeline}} o {{site.data.keyword.deliverypipeline}} Next y pulsar Crear.

Complete estos pasos para configurar un {{site.data.keyword.deliverypipeline}} para una aplicación existente:    

1. En el Panel de control de la app de {{site.data.keyword.Bluemix_notm}}, en el separador Visión general, en **Continuous Delivery**, cree un proyecto alojado por Git para la app pulsando **Añadir un repositorio Git y un conducto** o **Añadir Git**, en función del contexto.
1. Asegúrese de que el recuadro de selección **Rellenar el repositorio con el paquete de apps del iniciador y habilitar el conducto (Build & Deploy)** esté seleccionado y, a continuación, pulse **CONTINUAR**. Es posible que tenga que verificar su dirección de correo electrónico para continuar.  
1. Tras crearse el repositorio Git, pulse **CERRAR**. El botón Añadir Git se sustituye mediante un botón Editar código y el URL de Git.  
1. Para abrir el conducto, pulse **Editar código** y, a continuación, pulse **Build & Deploy**. Para ejecutar el conducto por primera vez, envíe un cambio al repositorio Git.

Después de añadir este servicio, puede crear un conducto de despliegue en varias etapas en sus espacios de {{site.data.keyword.Bluemix_notm}} configurando y ejecutando etapas que contengan trabajos de compilación, prueba y despliegue. En el Panel de control de {{site.data.keyword.deliverypipeline}}, puede ver sus proyectos de
{{site.data.keyword.jazzhub_short}} y los estados en los que se encuentran. Puede comprobar el estado de las compilaciones, la app desplegada y los despliegues recientes, o bien puede ver los registros y detalles de despliegue más recientes.  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks" role="article">
<h2 class="topictitle2" id="d68e338">Enlaces relacionados</h2>
<aside role="complementary" aria-labelledby="related_links">
<div class="linklist" id="general"><h3 class="linklistlabel" id="related_links">Enlaces relacionados</h3>
<ul>
<li><img src="./sout.gif" alt="">Requisitos previos de <a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(Se abre en un nuevo separador o ventana)">{{site.data.keyword.Bluemix_notm}}</a></li>
<li><img src="./sout.gif" alt=""><a href="https://www.ibm.com/devops/method/content/deliver/practice_delivery_pipeline/" rel="external" title="(Se abre en un nuevo separador o ventana)">IBM Bluemix Garage Method: Conducto de entrega</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">Guías de aprendizaje y ejemplos</h3>
<ul>

<!--
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Opens in a new tab or window)">Clone, edit, and deploy an app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Node.js app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Opens in a new tab or window)">Develop and deploy a Java app</a></li>
-->

<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(Se abre en un nuevo separador o ventana)">developerWorks: {{site.data.keyword.Bluemix_notm}}Servicio de {{site.data.keyword.deliverypipeline}}</a></li>
</ul>
</div>
</aside>
</article>
