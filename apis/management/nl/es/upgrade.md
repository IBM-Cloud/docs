---

copyright:
  years: 2017
lastupdated: "2017-04-11"

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Acceso a más características de gestión de API
{: #upgrade}

La gestión de API le permite controlar tasas de llamadas y OAuth y ver datos de análisis. Dispondrá de un mayor control sobre la gestión de las API si actualiza al servicio {{site.data.keyword.apiconnect_full}}. El servicio {{site.data.keyword.apiconnect_short}} ofrece más opciones de políticas de seguridad y un mayor control sobre los límites de tasas. Además, podrá configurar un portal de desarrollador completamente personalizable para poder socializar sus API y comunicarse con la comunidad de desarrolladores. Otras de sus ventajas son:
* Gestión del ciclo de vida 
* API compuestas
* Integración de servicios Web
* Mediación de protocolos
* Generación de API a partir de esquema
* Desarrollo de microservicios

La migración al servicio {{site.data.keyword.apiconnect_short}} es muy sencilla y no tienen que volver a crear ninguna de las API que gestiona actualmente con gestión de API. 

## Migración de API a {{site.data.keyword.apiconnect_short}}
{: #migrate_api}

Si decide actualizar a {{site.data.keyword.apiconnect_full}}, tendrá que migrar sus API de gestión de API al servicio {{site.data.keyword.apiconnect_short}}; para ello, siga estos pasos para cada una de las API:  

1. Descargue el documento Swagger correspondiente a la API desde gestión de API. 
    1. Abra la app y seleccione **Gestión de API**.
	2. Seleccione el separador **Explorador de API**. Aparecerá una lista de las API relacionadas con el proyecto. 
    2. Para descargar el documento Swagger correspondiente a su API, seleccione el icono que hay junto al nombre de la API.
2. Cree y prepare la instancia de {{site.data.keyword.apiconnect_short}}.  
    1. Cree una instancia del servicio {{site.data.keyword.apiconnect_short}} desde el catálogo de {{site.data.keyword.Bluemix_notm}}. 
	2. Seleccione su plan.
	3. Seleccione **+Añadir** para crear un catálogo.
	4. Especifique un nombre de visualización y un nombre para su catálogo y seleccione **Añadir**.
	5. Seleccione el catálogo que ha creado.
3. Importe el documento Swagger en la instancia de {{site.data.keyword.apiconnect_short}} siguiendo los pasos siguientes:
	1. En el panel de control del servicio {{site.data.keyword.apiconnect_short}}, seleccione **Ir a...(>>)** > **Borradores** en el menú. 
	2. Seleccione el separador API. 
	3. Seleccione **+Añadir** > **Importar API desde un archivo o URL**.
	4. Busque y seleccione el archivo Swagger que ha descargado desde gestión de API. Seleccione **Abrir**.

	5. Seleccione **Importar** para importar la API en el servicio {{site.data.keyword.apiconnect_short}}. 
4. Especifique los valores para la API. 
    1. Seleccione **Crear producto**.
	2. Seleccione el producto que ha creado para ver sus valores.
	3. Defina el límite de tasa para la API.
	4. Defina el nivel para la API.
5. Añada el punto final para la API, si es necesario.
    1. Seleccione la API. 
	2. Seleccione el separador Ensamblado. 
	3. Añada el punto final, si aún no se ha especificado.
	
 Después de migrar las API, podrá acceder a todas las características de gestión de API abriendo el mosaico del servicio {{site.data.keyword.apiconnect_short}} y también desde el panel de control de {{site.data.keyword.Bluemix_notm}}.  

 
