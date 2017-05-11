---

copyright:
  years: 2017
lastupdated: "2017-04-13"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Mis API
{: #manage_api}

Utilice el separador **Ver API gestionadas** para ver el estado general de las API que gestiona y de las que ha gestionado pero actualmente no están expuestas. En el separador **API compartidas**, puede ver todas las API que se han compartido con su organización de {{site.data.keyword.Bluemix_notm}} a través de la gestión de API o del servicio {{site.data.keyword.apiconnect_short}}. 

Puede ver juntas todas las API que gestiona con la gestión de API en el panel de control de API.  

## Visualización de las API gestionadas
{: #view_api}

Aquí puede ver las API creadas para acciones de {{site.data.keyword.openwhisk_short}} y otras fuentes externas.

1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, seleccione el icono **Menú** > **Servicios** > **API**.
2. Para seleccionar su origen, pulse **Gestionar API**. Se muestra una lista de las API que se gestionan actualmente. Los tipos de API incluyen los siguientes: 
    * Puntos finales definidos por el usuario - Estas entradas son API que están fuera del entorno de {{site.data.keyword.Bluemix_notm}} y de las que hace un seguimiento su punto final de URL.  
    * Apps de {{site.data.keyword.openwhisk_short}} - Estas entradas son acciones de {{site.data.keyword.openwhisk_short}} acomodadas dentro de una API. 

Seleccione el nombre de una API para ver más detalles sobre la misma. 

## Creación de API gestionadas
{: #create_mgd_api}

Puede añadir una API a la lista sin abandonar la lista de API gestionadas seleccionando **Crear API gestionada**.

Después de seleccionar si desea crear una API de {{site.data.keyword.openwhisk_short}} o una de proxy (externa), especifique la información correspondiente a la nueva API.  

Este es el único lugar donde puede añadir una API de proxy, o API externa. Una API externa es una que no se crea ni se almacena en el espacio de la organización de {{site.data.keyword.Bluemix_notm}}. Puede gestionar una API externa especificando el URL de su punto final externo. Esto se resultará útil si prueba la gestión de API para ver si se ajusta a sus necesidades, o si ya tiene API en ejecución con URL existentes que no desea interrumpir.  

Consulte [Gestión de API](manage_apis.html) para obtener más información sobre los valores necesarios para crear las API. 

## Cómo trabajar con API compartidas
{: #share_api}

En el separador **Explorar API compartidas** puede ver las API que otros han creado y que han compartido con usted. También puede crear claves de API para las API asociadas con acciones de {{site.data.keyword.openwhisk_short}} y con el servicio {{site.data.keyword.appconserviceshort}}. 

1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Menú** > **Servicios** > **API**.
2. Seleccione **Explorar API compartidas** en la navegación. Aquí se muestran todas las API que puede consumir. 
3. Para consumir una API, selecciónela para abrir su portal de desarrollador, donde se puede suscribir a un plan para utilizarla.  
4. Después de seleccionar la API que desea gestionar, consulte [Gestión de API](manage_apis.html) para obtener más información sobre cómo realizar las tareas siguientes: 
    * Ver la utilización de una API
    * Crear claves de API
    * Utilice el Explorador de API para ver documentación y probar la API.
