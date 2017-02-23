---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-14"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conexión de la aplicación

Para conectar la aplicación a {{site.data.keyword.iot_full}}, debe conectarse utilizando las claves y las señales de la API o enlazando la aplicación directamente a {{site.data.keyword.iot_short_notm}} en {{site.data.keyword.Bluemix_notm}}. Utilice el panel de control de acceso para otorgar acceso.
{:shortdesc}

## Conexión de la clave de API
{: #api-key}
Las claves de API se utilizan al conectar aplicaciones a la organización de {{site.data.keyword.iot_short_notm}}. Las aplicaciones requieren una clave de API para conectarse a una organización y una señal de autenticación exclusiva que se debe utilizar con dicha clave de API.  

Para obtener más información sobre las conexiones de la aplicación, consulte [Conectividad de MQTT para aplicaciones](https://docs.internetofthings.ibmcloud.com/applications/mqtt.html) en la documentación del desarrollador.

Para crear un nuevo par de clave y señal de autenticación de API:  
1.	En el panel de control de {{site.data.keyword.iot_short_notm}}, vaya a **Apps > Claves de API**.  
2.	Pulse **Generar clave de API**.  
**Importante:** Tome nota del par clave y señal de API. Las señales de autenticación no son recuperables. Si pierde u olvida esta señal, tendrá que volver a registrar la clave de API para generar una nueva señal de autenticación.
 - Un ejemplo de una clave de API sería `a-organization_id-a84ps90Ajs`  
 - Un ejemplo de una señal sería `MP$08VKz!8rXwnR-Q*`  
3.	Añada un comentario para identificar la clave de API en el panel de instrumentos, como por ejemplo: Clave para conectar mi aplicación.
4.	Pulse **Finalizar**.



## Conexión de enlace de Bluemix
{: #bluemix-binding}
Se pueden enlazar aplicaciones a la organización de {{site.data.keyword.iot_short_notm}} desde {{site.data.keyword.Bluemix_notm}}. Al enlazar la aplicación, sólo puede comunicarse con instancias de servicio en el mismo espacio u organización. Encontrará todos los datos necesarios para que la app se comunique con la instancia de servicio en la variable de entorno VCAP_SERVICES. Si su app está enlazada a varios servicios, la variable VCAP_SERVICES contiene la información de conexión para cada instancia de servicio.  

Sin embargo, puede utilizar instancias de servicio de otros espacios u organizaciones de la misma forma que lo hace una app externa. En lugar de crear un enlace, utilice las credenciales para configurar directamente la instancia de la app. Para obtener más información, consulte [Solicitud de una nueva instancia de servicio](https://console.{DomainName}/docs/services/reqnsi.html#req_instance) en la documentación de {{site.data.keyword.Bluemix_notm}}.

Para ver los detalles para las aplicaciones de Bluemix que están enlazadas a la instancia de servicio de Bluemix asociada con la organización, vaya a **Apps > Apps Bluemix**.  
