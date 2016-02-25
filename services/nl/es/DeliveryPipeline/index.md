{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

#Iniciación a {{site.data.keyword.deliverypipeline}} {: #delivery-pipeline}  

*Última actualización: 21 de enero de 2016*

Para automatizar las compilaciones y los despliegues en {{site.data.keyword.Bluemix}}, utilice el IBM Continuous {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}} (el servicio de {{site.data.keyword.deliverypipeline}}).
{: shortdesc} 

Cuando desarrolle una app en la nube, puede elegir entre distintos tipos de compilación. Proporcione el script de compilación y {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} lo ejecutará; no es necesario configurar sistemas de compilación. A continuación, con un solo clic puede desplegar automáticamente su app en uno o más espacios de {{site.data.keyword.Bluemix_notm}}, servidores de Cloud Foundry públicos o contenedores Docker en IBM Containers for {{site.data.keyword.Bluemix_notm}}.  

Los trabajos de compilación compilan y empaquetan el código fuente de su app desde repositorios gestión de control de origen (SCM) Git o Jazz. Los trabajos de compilación generan artefactos desplegables, como archivos WAR o contenedores Docker para IBM Containers. Además, puede ejecutar automáticamente pruebas de unidad en su compilación. Cada vez que cambia el código fuente, se desencadena una compilación.   

Un trabajo de despliegue toma la salida de un trabajo de compilación y lo despliega en IBM Containers o en servidores de Cloud Foundry como {{site.data.keyword.Bluemix_notm}}.  

Puede desplegar en una o más regiones y servicios. Por ejemplo, puede configurar el servicio de {{site.data.keyword.deliverypipeline}} de forma que los artefactos de desarrollo utilicen IBM Containers, que se prueben en una región y que se desplieguen en producción en varias regiones. Para obtener más información, consulte [Regiones](../../overview/index.html#ov_intro__reg).

1. Inicie sesión en {{site.data.keyword.Bluemix_notm}} y seleccione una organización y un espacio para su app.
1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, pulse **CREAR UNA APP**.
1. Seleccione una plantilla de app web o para móvil, seleccione un iniciador y pulse **CONTINUAR**.  Asigne un nombre a la app y pulse **FINALIZAR**.  
1. En la página Empezar a escribir código, desplácese hacia abajo y pulse **VER VISIÓN GENERAL DE LA APP**.  
1. En el Panel de control de la app {{site.data.keyword.Bluemix_notm}}, cree un proyecto alojado en Git para la app pulsando **AÑADIR GIT**. Asegúrese de que el recuadro de selección **Llene este repositorio con el paquete de aplicación de inicio y habilite {{site.data.keyword.deliverypipeline}} (Build & Deploy)** esté marcado y pulse **CONTINUAR**.   
1. Tras crearse el repositorio Git, pulse **CERRAR**. El enlace AÑADIR GIT se sustituye por el enlace EDITAR CÓDIGO y su URL de Git.  
1. Añada el servicio {{site.data.keyword.deliverypipeline}} al espacio o espacios asociados. Después de añadir este servicio, puede crear un conducto de despliegue en varias etapas en sus espacios de {{site.data.keyword.Bluemix_notm}} configurando y ejecutando etapas que contengan trabajos de compilación, prueba y despliegue.
    1. En el Panel de control de la app {{site.data.keyword.Bluemix_notm}}, pulse **AÑADIR UN SERVICIO O API**. Para la categoría, marque el recuadro de selección **DevOps** y, en el catálogo, pulse **Delivery Pipeline**.
    2. Seleccione un plan y pulse **CREAR**. Se abre el panel de control de {{site.data.keyword.deliverypipeline}} y muestra la app que ha creado anteriormente.     
  
En el Panel de control de {{site.data.keyword.deliverypipeline}}, puede ver sus proyectos de
{{site.data.keyword.jazzhub_short}} y los estados en los que se encuentran. Puede comprobar el estado de las compilaciones, la app desplegada y los despliegues recientes, o bien puede ver los registros y detalles de despliegue más recientes.  

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks">
<h2 class="topictitle2" id="d68e338">Enlaces relacionados</h2>
<aside>
<div class="linklist" id="general"><h3 class="linklistlabel">Enlaces relacionados</h3>
<ul>
<li><img src="./sout.gif" alt="">Requisitos previos de <a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(Se abre en un nuevo separador o ventana)">{{site.data.keyword.Bluemix_notm}}</a></li>
</ul>
</div>

<div class="linklist" id="samples">
<h3 class="linklistlabel">Guías de aprendizaje y ejemplos</h3>
<ul>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/devopsweb/" rel="external" title="(Se abre en un nuevo separador o ventana)">Clone, edite y despliegue una app</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditor" rel="external" title="(Se abre en un nuevo separador o ventana)">Desarrolle y despliegue una app Node.js</a></li>
<li><img src="./sout.gif" alt=""><a href="https://hub.jazz.net/tutorials/jazzeditorjava" rel="external" title="(Se abre en un nuevo separador o ventana)">Desarrolle y despliegue una app Java</a></li>
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/delivery%20pipeline%20service" rel="external" title="(Se abre en un nuevo separador o ventana)">developerWorks: {{site.data.keyword.Bluemix_notm}}Servicio de {{site.data.keyword.deliverypipeline}}</a></li>
</ul>
</div>
</aside>
</article>
