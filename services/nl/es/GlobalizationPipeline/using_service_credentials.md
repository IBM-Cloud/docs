---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Uso de {{site.data.keyword.GlobalizationPipeline_full}} fuera de {{site.data.keyword.Bluemix_notm}}
{: #globalizationpipeline_external}

*Última actualización: 27 de junio de 2016*
{: .last-updated}

Muchos servicios de {{site.data.keyword.Bluemix_notm}}, incluyendo {{site.data.keyword.GlobalizationPipeline_full}}, se pueden utilizar desde una aplicación local que aloja entorno o incluso desde otra plataforma de nube sin tener que alojar la aplicación en {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Para utilizar {{site.data.keyword.GlobalizationPipeline_full}} fuera de {{site.data.keyword.Bluemix_notm}}, lleve a cabo los pasos siguientes:

1. Vaya al catálogo de {{site.data.keyword.Bluemix_notm}} y seleccione el servicio de **{{site.data.keyword.GlobalizationPipeline_short}}** desde la categoría **DevOps**.

2. En la página de catálogo del servicio de {{site.data.keyword.GlobalizationPipeline_full}}, rellene la información necesaria. Para el campo **Conectar a**, elija la opción para **Dejar sin enlazar**.

3. Pulse **Crear** para añadir el servicio a la organización de {{site.data.keyword.Bluemix_notm}}. Se le llevará al panel de control de {{site.data.keyword.GlobalizationPipeline_full}}.

4. Desde el panel de control, pulse el separador **Credenciales de servicio**.  

El separador **Credenciales de servicio** muestra todas las credenciales que están disponibles para dicha instancia del servicio concreta. Mediante el uso de estas credenciales y el URL de servicio que se proporciona, puede acceder a la API de {{site.data.keyword.GlobalizationPipeline_full}} y hacer uso de sus características desde la aplicación en cualquier entorno de alojamiento.

Para obtener más información sobre la API RESTful de {{site.data.keyword.GlobalizationPipeline_full}}, consulte la [Referencia de API](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}.
