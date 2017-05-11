---

copyright:
  years: 2017
lastupdated: "2017-04-12"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Creación de API desde acciones de {{site.data.keyword.openwhisk_short}}
{: #manage_openwhisk_apis}

Las acciones de OpenWhisk se pueden beneficiar de la gestión por parte de la función de gestión de API. 

Con la gestión de API, puede exponer una acción de {{site.data.keyword.openwhisk_short}} como una API. Después de definir la API, puede aplicar políticas de seguridad y de limitación de tasas, ver el uso de la API y los registros de respuestas y definir políticas de compartición de API.   

Para crear una API de {{site.data.keyword.openwhisk_short}}, siga los pasos siguientes:

1. En el panel de control de {{site.data.keyword.openwhisk_short}}, pulse el separador **API**. Si ya tiene API de {{site.data.keyword.openwhisk_short}} creadas, se muestra una lista de sus API de {{site.data.keyword.openwhisk_short}}. Si aún no tiene ninguna API de {{site.data.keyword.openwhisk_short}}, se muestra la pantalla de iniciación.  
2. Pulse **Crear una API de {{site.data.keyword.openwhisk_short}}**. Se muestra la ventana Crear API para {{site.data.keyword.openwhisk_short}}.  
3. Rellene los campos de la sección Información de API y luego pulse **Crear operación**. Se muestra la ventana Crear operación. Se crean operaciones para definir el punto final, la vía de acceso https y el método para la API. 
4. En la ventana "Crear operación", rellene los campos necesarios y seleccione **Crear**. La operación se añade a la tabla Operaciones que invocan acciones de {{site.data.keyword.openwhisk_short}}. 
5. Especifique el resto de la información que desee. También puede añadir o actualizar el resto de la información más tarde cuando gestione las API. 
6. Pulse **Guardar**. Se abre la página de visión general de la gestión de API correspondiente a su API y se muestra toda la información que acaba de definir. 
7. Continúe gestionando la API con [Gestionar API](manage_apis.html).
