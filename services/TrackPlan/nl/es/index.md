{:shortdesc: .shortdesc}
{:screen: .screen}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

#Iniciación al servicio {{site.data.keyword.trackplan}} {: #track-plan}  

*Última actualización: 21 de enero de 2016*

Para visualizar, editar y planificar tareas, utilice {{site.data.keyword.trackplanlong}} (el servicio {{site.data.keyword.trackplan}}). Puede realizar el seguimiento de su trabajo y el trabajo de su equipo, crear defectos, ver qué está entrando, mantener la lista de tareas pendientes y planificar el trabajo para futuros sprints.
{: shortdesc}

El servicio {{site.data.keyword.trackplan}} enlaza planes y código de forma que los planes estén sincronizados con el progreso del equipo de desarrollo. Con el servicio, puede crear historias, tareas y defectos para describir un proyecto y realizar su seguimiento. También puede planificar y gestionar el registro de reserva, versiones y sprints del producto.

1. Inicie sesión en {{site.data.keyword.Bluemix_notm}} y seleccione una organización y un espacio para su app.
1. En el Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse **CREAR UNA APP**.
1. Seleccione una plantilla de app web o para móvil, seleccione un iniciador y pulse **CONTINUAR**. Asigne un nombre a la app y pulse **FINALIZAR**.
1. En la página Empezar a escribir código, desplácese hacia abajo y pulse **VER VISIÓN GENERAL DE LA APP**.
1. En el Panel de control de la app {{site.data.keyword.Bluemix_notm}}, cree un proyecto alojado en Git para la app pulsando **AÑADIR GIT**. Asegúrese de que el recuadro de selección **Llene este repositorio con el paquete de aplicación de inicio y habilite Delivery Pipeline (Build & Deploy)** esté marcado y pulse **CONTINUAR**. Tras crearse el repositorio Git, pulse **CERRAR**. El enlace AÑADIR GIT se sustituye por el enlace EDITAR CÓDIGO y su URL de Git.
1. Añada el servicio {{site.data.keyword.trackplan}} al espacio para poder gestionar el trabajo del equipo.
    1. En el Panel de control de la app {{site.data.keyword.Bluemix_notm}}, pulse **AÑADIR UN SERVICIO O API**. Para la categoría, seleccione **DevOps**, y, en el catálogo, pulse **Track & Plan**. 
    2. En la página {{site.data.keyword.trackplan}}, seleccione un plan y pulse **CREAR**.    
1. En la lista de apps, en la columna Estado, cambie el estado del servicio {{site.data.keyword.trackplan}} pulsando el estado actual, que en este caso es **DESACTIVADO**. Se abre la página Configuración del proyecto en {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.jazzhub_short}}.
    1. Seleccione la opción para habilitar el servicio {{site.data.keyword.trackplan}}. Si es necesario, actualice la región, organización o espacio
    2. Pulse **GUARDAR**.  
1. Vuelva al Panel de control de {{site.data.keyword.Bluemix_notm}} y pulse el icono de servicio {{site.data.keyword.trackplan}}. El estado del servicio {{site.data.keyword.trackplan}} cambia a **ACTIVO** para la app.
1. En la lista de apps, en la columna Elemento de trabajo, pulse **CREAR** para empezar a utilizar el servicio {{site.data.keyword.trackplan}}.  

En el Panel de control de {{site.data.keyword.Bluemix_notm}}, puede ver una lista de los proyectos de {{site.data.keyword.jazzhub_short}} y su recuento de miembros y visibilidad, y muestra si el servicio {{site.data.keyword.trackplan}} está habilitado. Puede crear elementos de trabajo para cualquiera de sus proyectos de {{site.data.keyword.jazzhub_short}}, o bien ir a las herramientas de planificación.   

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
<li><img src="./sout.gif" alt=""><a href="http://www.ibm.com/developerworks/topics/track%20and%20plan%20service" rel="external" title="(Se abre en un nuevo separador o ventana)">developerWorks: servicio de {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.trackplan}}</a></li>
</ul>
</div>
</aside>
</article>
