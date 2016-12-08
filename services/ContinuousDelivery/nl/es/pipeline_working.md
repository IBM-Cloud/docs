---



copyright:

  years: 2015, 2016



---


{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:shortdesc: .shortdesc}

# Cómo trabajar con {{site.data.keyword.deliverypipeline}} {: #pipeline-working}  

Última actualización: 18 de noviembre de 2016
{: .last-updated}

Para automatizar las compilaciones y los despliegues en {{site.data.keyword.Bluemix}}, utilice {{site.data.keyword.deliverypipeline}} for {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Con {{site.data.keyword.deliverypipeline}}, puede elegir entre varios tipos de compilación. Proporcione el script de compilación y {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}} lo ejecutará; no es necesario configurar sistemas de compilación. A continuación, con un solo clic puede desplegar automáticamente su app en uno o más espacios de {{site.data.keyword.Bluemix_notm}}, servidores de Cloud Foundry públicos o contenedores Docker en IBM Containers for {{site.data.keyword.Bluemix_notm}}.  

Los trabajos de compilación compilan y empaquetan el código fuente de su app desde repositorios Git. Los trabajos de compilación generan artefactos desplegables, como archivos WAR o contenedores Docker para IBM Containers. Además, puede ejecutar automáticamente pruebas de unidad en su compilación. Puede configurar sus trabajos de compilación de modo que cada vez que se envíe una confirmación se desencadene una compilación. 

Un trabajo de despliegue toma la salida de un trabajo de compilación y lo despliega en IBM Containers o en servidores de Cloud Foundry como {{site.data.keyword.Bluemix_notm}}.  

Puede desplegar en una o más regiones y servicios. Por ejemplo, puede configurar {{site.data.keyword.deliverypipeline}} para que utilice uno o varios servicios, realice pruebas en una región y despliegue a producción en varias regiones. Para obtener más información, consulte [Regiones](/docs/overview/whatisbluemix.html#ov_intro_reg).

Hay varias formas para crear un conducto, incluida la adición de un conducto a una aplicación existente y la creación de un conducto sin una aplicación existente. Si aún no tiene un servicio de {{site.data.keyword.deliverypipeline}} en la organización, puede ir al catálogo, pulsar {{site.data.keyword.deliverypipeline}} y pulsar Crear. 

Complete estos pasos para configurar un {{site.data.keyword.deliverypipeline}} para una aplicación existente:    

1. En el Panel de control de la app {{site.data.keyword.Bluemix_notm}}, pulse en la app. 
1. En el menú de la barra de menús de {{site.data.keyword.Bluemix_notm}}, pulse **Servicios** y luego pulse **DevOps**.
1. Pulse **Conductos** y luego pulse **Crear un conducto**.

Para [crear un conducto (el enlace se abre en una nueva ventana)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} configurado para desplegar una aplicación Cloud Foundry, siga estos pasos:     

1. Pulse **Cloud Foundry**.  
1. Si desea utilizar otro nombre para el conducto, cambie el nombre predeterminado.  
1. Si desea utilizar otro nombre para la aplicación, cambie el nombre predeterminado. Este es el nombre de la aplicación en la que se despliega el conducto.  
1. Si no tiene una cadena de herramientas, se crea automáticamente una cadena de herramientas con un nombre predeterminado. Si desea utilizar otro nombre para la cadena de herramientas, cámbiele el nombre. Con la cadena de herramientas, puede ampliar las prestaciones del conducto integrándolo con otras herramientas y servicios. 

 **Consejo**: Los conductos y las cadenas de herramientas pertenecen a las organizaciones (orgs). Si pertenece a una org que tiene cadenas de herramientas, puede utilizar dichas cadenas de herramientas aunque no las haya creado. 
 
1. Seleccione la cadena de herramientas que desea utilizar o escriba un nombre para la nueva cadena de herramientas que desea crear.
1. Especifique la ubicación del repositorio GitHub.

 **Sugerencia**: si no tiene autorización de {{site.data.keyword.Bluemix_notm}} para acceder a GitHub, se le solicitará que pulse **Autorizar** para ir al sitio web de GitHub. Si no tiene ninguna sesión de GitHub activa, se le solicitará que inicie sesión. Pulse **Autorizar aplicación** para permitir que {{site.data.keyword.Bluemix_notm}} acceda a su cuenta de GitHub. Si tiene una sesión activa de GitHub pero no ha introducido recientemente su contraseña, es posible que se le solicite que introduzca la contraseña de GitHub para confirmarla.

   * Si tiene un repositorio de GitHub y desea utilizarlo, seleccione **Enlazar** para el tipo de repositorio. Busque la ubicación del repositorio o seleccione el repositorio en la lista de repositorios disponibles.
   
   * Si desea crear un repositorio GitHub vacío, seleccione **Nuevo** para el tipo de repositorio. Escriba un nombre para el repositorio.
   
   * Si desea crear un clon de un repositorio GitHub, seleccione **Copiar** para el tipo de repositorio. Busque la ubicación del repositorio o seleccione el repositorio en la lista de repositorios disponibles.
   
   * Si desea bifurcar un repositorio GitHub de forma que pueda aportar cambios a través de solicitudes de extracción, seleccione **Bifurcar**.Busque la ubicación del repositorio o seleccione el repositorio en la lista de repositorios disponibles.
 
1. Pulse **Crear**. El conducto se crea, se configura y se visualiza en la página Visión general de la cadena de herramientas. ![Mosaico de conductos](images/cd_pipeline.png)

Para crear un [conducto vacío (el enlace se abre en una ventana nueva)](https://console.ng.bluemix.net/devops/pipelines/dashboard/create){: new_window} sin etapas preconfiguradas:

1. Pulse **Personalizado**.
1. Si desea utilizar otro nombre para el conducto, cambie el nombre predeterminado.  
1. Si no tiene una cadena de herramientas, se crea automáticamente una cadena de herramientas con un nombre predeterminado. Si desea utilizar otro nombre para la cadena de herramientas, cámbiele el nombre. Con la cadena de herramientas, puede ampliar las prestaciones del conducto integrándolo con otras herramientas y servicios. 
1. Seleccione la cadena de herramientas que desea utilizar o escriba un nombre para la nueva cadena de herramientas que desea crear.
1. Pulse **Crear**. Se crea un conducto vacío y se representa como un mosaico en la página Visión general de la cadena de herramientas.

En el mosaico de {{site.data.keyword.deliverypipeline}}, puede cambiar la configuración, comprobar el estado de las compilaciones, la app desplegada y los despliegues recientes, consultar los registros y detalles de despliegue más recientes o suprimir el conducto.   

<article class="topic reference nested1" aria-labelledby="d68e338" lang="en-us" id="rellinks" role="article">
<h2 class="topictitle2" id="d68e338">Enlaces relacionados</h2>
<aside role="complementary" aria-labelledby="related_links">
<div class="linklist" id="general"><h3 class="linklistlabel" id="related_links">Enlaces relacionados</h3>
<ul>
<li><img src="./sout.gif" alt="">Requisitos previos de <a href="https://developer.ibm.com/bluemix/support/#prereqs" rel="external" title="(Se abre en un nuevo separador o ventana)">{{site.data.keyword.Bluemix_notm}}</a></li>
<li><img src="./sout.gif" alt=""><a href="https://www.ibm.com/devops/method/content/deliver/practice_delivery_pipeline/" rel="external" title="(Se abre en un nuevo separador o ventana)">Método IBM Bluemix Garage: Conducto de entrega</a></li>
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
