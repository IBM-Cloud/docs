---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Acerca de {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}

{: shortdesc}
El servicio {{site.data.keyword.mobileanalytics_full}} proporciona información esencial sobre el uso y el rendimiento de aplicaciones para los propietarios y los desarrolladores de aplicaciones para móviles. Gracias a {{site.data.keyword.mobileanalytics_short}}, los propietarios y los desarrolladores de aplicaciones pueden ver lo que sucede en el lado del usuario y aprovechar este conocimiento para compilar aplicaciones mejoradas que sean mucho más relevantes para los usuarios y que destaquen en el inmenso océano de aplicaciones para móviles. 

{: #overview}  
El servicio incluye la consola de {{site.data.keyword.mobileanalytics_short}}, en la que los desarrolladores y los propietarios de aplicaciones pueden supervisar el rendimiento de las aplicaciones para móviles, consultar las estadísticas de uso y buscar registros de dispositivo.  {{site.data.keyword.mobileanalytics_short}} proporciona SDK de cliente para iOS 8+ (solo Swift) y Android 4+.

<!-- Mobile Analytics Server SDKs - set of server SDKs to protect resources that are-->
<!--hosted on {{site.data.keyword.Bluemix_notm}}. Currently supported runtimes are-->
<!--Node.js and Java for Liberty.-->

Con el servicio de {{site.data.keyword.mobileanalytics_short}} puede hacer lo siguiente:
<!-- and includes the following capabilities: -->
<!-- * Near real-time analytics for client activity. Exp -->
<!--* Network latency analytics. GA only -->
<!-- * Client log search and download. Exp -->
<!--* Server log search and download. GA only -->
<!-- Crash and stack trace search. Exp -->

<dl>
	<dt>Obtener una perspectiva inmediata</dt>
		<dd>Consulte las métricas de rendimiento y uso en tiempo real.</dd>
	<dt>Efectuar implementaciones en cuestión de minutos</dt>
		<dd>Cree una instancia de servicio en {{site.data.keyword.Bluemix}}, añada el SDK al proyecto, pegue dos líneas de código a la aplicación y ya podrá recopilar numerosas métricas predefinidas.</dd>
	<dt>Recopile los datos que desee</dt>
		<dd>Instrumente apps con sucesos personalizados, descubra cómo interactúan los usuarios con la app, realice el seguimiento de las compras y supervise la actividad de la app.  
</dd>
<dt>Consultar de un vistazo las métricas de todas sus aplicaciones</dt>
	<dd>La consola de {{site.data.keyword.mobileanalytics_short}} ofrece gráficos <!-- both --> ya preparados <!--and custom-->, sin necesidad de escribir consultas.</dd>
<dt>Céntrese en lo que considere importante</dt>
	<dd>Filtre las métricas por tiempo, adaptador, aplicación, versión de aplicación, sistema operativo, versión de sistema operativo o por modelo de dispositivo.</dd>
<dt>Detectar problemas rápidamente</dt>
	<dd>Supervise el estado de bloqueo. Establezca activadores de alertas en las métricas esenciales y enrute alertas a cualquier punto final REST. </dd>
<dt>Identificación de la causa raíz del problema</dt>
	<dd>Utilice el registro personalizado en la aplicación y cargue de forma automática los registros para buscarlos desde la consola. Obtenga un mayor detalle de los eventos de bloqueo para consultar los seguimientos de pila. </dd>
</dl>
 

## Uso de métricas y eventos
{: #usingmetrics}

Gracias a las **métricas predefinidas** puede responder a las siguientes preguntas:

* ¿Cuántos usuarios nuevos tengo?  
* ¿Cuántas personas utilizan mi aplicación de forma activa?  
* ¿Con qué frecuencia utilizan mi aplicación? 
* ¿A qué hora del día utilizan mi aplicación?  
* ¿Qué modelos de dispositivo prefieren mis usuarios? 
* ¿Cuándo debería anular el soporte para los sistemas operativos existentes? 
* ¿Qué aplicaciones tienen problemas de rendimiento?  

Al añadir sus propios **sucesos personalizados**, puede responder a las siguientes preguntas: 

* ¿Qué características se utilizan más y cuáles menos?  
* ¿Desde dónde entran y salen los usuarios de mi app?  
* ¿Qué actividades ven más los usuarios?  
* ¿Completan los usuarios los flujos de trabajo de la app (por ejemplo, funnels de conversión)?   

Los registros de lado del cliente y los datos de uso se recopilan automáticamente y se envían al servicio de Mobile Analytics a petición. Los desarrolladores y administradores pueden utilizar el panel de control de servicio de {{site.data.keyword.mobileanalytics_short}} para ver datos recopilados por el SDK de cliente.

## Visualización de datos
{: data-visualization}

Todos los datos recopilados por el servicio de análisis se pueden visualizar mediante el panel de control de {{site.data.keyword.mobileanalytics_short}}, al que se puede acceder desde el panel de control de {{site.data.keyword.Bluemix_notm}} pulsando la instancia de mosaico de servicio de {{site.data.keyword.mobileanalytics_short}} de IBM. <!--You can also create custom charts, based on data that is collected by the analytics service in the dashboard.--> Además de una vista rápida de los análisis móviles, la función de análisis incluye la capacidad de realizar una búsqueda en bruto en los registros de clientes, en los datos de bloqueo de los clientes capturados, y cualquier dato adicional que proporcione de forma explícita mediante las llamadas de la función API del cliente que proveen al servicio de {{site.data.keyword.mobileanalytics_short}}. 

## Preguntas frecuentes de {{site.data.keyword.mobileanalytics_short}} 
{: #faq}

<dl>
	<dt>¿Qué es {{site.data.keyword.mobileanalytics_full}}?</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}} es un servicio que proporciona información histórica en tiempo real sobre el rendimiento de las aplicaciones para móviles y cómo se utilizan. Utilizando {{site.data.keyword.mobileanalytics_short}}, los desarrolladores de aplicaciones y los propietarios de aplicaciones pueden tomar decisiones de control de datos supervisando tendencias en usuarios activos, sesiones, plataformas móviles y bloqueos de aplicación. También puede establecer alertas sobre métricas seleccionadas que, una vez desencadenadas, envían mensajes a cualquier punto final de REST, incluido un servicio de envío por push o los servicios de mensajería interna.</dd>
	<dt>¿Qué puedo hacer con {{site.data.keyword.mobileanalytics_short}} para {{site.data.keyword.Bluemix_notm}}?</dt>
		<dd>Como gestor de producto de la aplicación para móviles, puede ver cuánta gente utilizar su aplicación (métricas de usuario) y cuándo la utilizan (métricas de sesión). Esta información se presenta como una serie temporal y se actualiza en tiempo real para que pueda ver el efecto de los cambios realizados en la aplicación. Puede filtrar para ver versiones específicas de la aplicación o sistemas operativos para tomar decisiones sobre el proceso de desuso y priorización. </dd>
		<dd>Como usuario de marketing de aplicaciones para móvil, puede utilizar métricas de usuario y sesión para supervisar la colaboración, gestionar la rotación y evaluar la eficacia de las tareas de marketing de aplicaciones para móviles observando los cambios a lo largo del tiempo y correlacionando con sus fechas de sucesos.</dd>
		<dd>Como desarrollador de aplicaciones para móviles, puede utilizar las métricas de bloqueos para descubrir y resolver problemas de rendimiento de aplicaciones para móviles antes de que decepcionen a los usuarios y dañen la reputación de la aplicación. Puede supervisar el recuento de bloqueos y el índice de bloqueos desde la consola de análisis y puede priorizar los bloqueos que afectan a la mayoría de los usuarios. Puede establecer alertas para enviar notificaciones o realizar acciones automatizadas cuando los bloqueos exceden un umbral determinado y puede resolver problemas accediendo a los detalles sobre las instancias de bloqueo para ver los registros de dispositivo y los seguimientos de pila de la aplicación.</dd>
	<dt>¿Necesito habilidades de analista de datos para utilizar Mobile Analytics?</dt>
		<dd>No, {{site.data.keyword.mobileanalytics_short}} ofrece una consola de análisis lista para usar para las partes interesadas del negocio y los desarrolladores de aplicaciones. No es necesario poseer habilidades de consulta.</dd>
	<dt>¿Puede realizar consultas personalizadas en mis datos analíticos?</dt>
		<dd>{{site.data.keyword.mobileanalytics_short}} no permite realizar consultas personalizadas, pero existe una consideración sobre esta característica en el futuro.</dd>
	<dt>¿Cómo puedo conectar mi aplicación a {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>[Descargue nuestro SDK para iOS o Android de código abierto](install-client-sdk.html), o utilice {{site.data.keyword.mobileanalytics_short}} [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/) para otras plataformas. </dd>
	<dt>¿En qué regiones de Bluemix está disponible {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>Actualmente, Mobile Analytics está disponible en Estados Unidos - Sur y en el Reino Unido. La disponibilidad en otras regiones está planificada pero todavía no se ha determinado el periodo de tiempo.</dd>
	<dt>¿Cuánto cuesta este servicio?</dt>
		<dd>Los 100 primeros millones de sucesos que se recopilan cada mes son gratuitos y, a partir de esa cantidad, el coste es de 1 $ por millón de sucesos.</dd>
	<dt>¿Qué es un suceso?</dt>
		<dd>Los sucesos actuales incluyen inicio de sesión de aplicación, fin de sesión de aplicación (incluido bloqueo de la aplicación), notificaciones de alertas y entradas de registro.</dd>
	<dt>¿Cómo puedo calcular cuándo me costará el servicio al mes?</dt>
		<dd>Puesto que el precio depende del número de sucesos que se envían al servicio por cuenta de cliente, estimar el precio significa estimar la cantidad de sucesos.  
<p>
El importe que se le cargará es la suma de sucesos de todas las aplicaciones que tenga conectadas a {{site.data.keyword.mobileanalytics_short}}. Para una determinada aplicación, el número de sucesos depende del grado de preparación que haya implementado dentro de la aplicación, del número de usuarios y del nivel de actividad de los usuarios.   
</p>
<p>
Utilice esta fórmula para calcular el uso:
sucesos por mes por aplicación = (usuarios por día)(sesiones por usuario por día)(días al mes)(sucesos por sesión)
</p>
<p>
Los sucesos por sesión pueden oscilar entre 2 y varios cientos, en función de las llamadas de red, analíticas personalizadas, capturas de registro y definiciones de alerta que haya configurado el desarrollador en la aplicación.
</p>
	<dt>¿Cuánto tiempo se conservan mis datos analíticos?</dt>
		<dd>Los datos se conservan al menos durante 30 días.</dd>
	<dt>¿Cuánto tiempo tardan los datos en visualizarse en la consola de {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>Los datos en la consola de {{site.data.keyword.mobileanalytics_short}} son casi en tiempo real, lo que significa que los datos se visualizan en un periodo de segundos de los sucesos reales.</dd>
	<dt>¿Cuál es la diferencia entre {{site.data.keyword.mobileanalytics_full}} y Mobile Analytics que se encuentran en MobileFirst Platform Foundation?</dt>
		<dd>El usuario y la sesión son similares a estas dos consolas, pero la analítica que se entrega con MobileFirst Platform Foundation contiene configuraciones y métricas adicionales que permiten a los clientes gestionar su propio clúster de análisis localmente. Además, la consola de analíticas de MobileFirst Platform Foundation desglosa las métricas para adaptadores y procedimientos de adaptadores, mientras que en el servicio de {{site.data.keyword.mobileanalytics_short}}, estas métricas se integran en tablas y gráficos de solicitudes de red.</dd>
	<dt>Estoy utilizando MobileFirst Platform Foundation localmente para desarrollar mis apps, pero no deseo alojar mi propio clúster de análisis. En su lugar, ¿puede utilizar {{site.data.keyword.mobileanalytics_full}}?</dt>
		<dd>Sí. Dispone de un par de opciones: si está utilizando MobileFirst Platform Foundation 7.x u 8.0 y sus apps están instrumentadas con SDK de MobileFirst Platform, puede configurar el servidor de MobileFirst para notificar datos de análisis a {{site.data.keyword.mobileanalytics_short}} para {{site.data.keyword.Bluemix_notm}}. Lea la publicación de blog [Configuring Mobile Analytics and Mobile Foundation Bluemix services ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/ "icono de enlace externo"){: new_window} para obtener más detalles. Como alternativa, puede instrumentar las apps utilizando el SDK de {{site.data.keyword.mobileanalytics_short}} de {{site.data.keyword.Bluemix_notm}} y notificar directamente al servicio de {{site.data.keyword.mobileanalytics_short}}.</dd>
	<!-- <dt>My instance of  {{site.data.keyword.mobileanalytics_short}} does not look like the screen shots in the catalog. What's going on?</dt> -->
		<!-- <dd>Most likely you are using the Classic view interface for {{site.data.keyword.Bluemix_notm}}. Classic view is deprecated, so {{site.data.keyword.mobileanalytics_short}} runs best in the new {{site.data.keyword.Bluemix_notm}} interface. If you are in Classic view, you will see a link in the {{site.data.keyword.Bluemix_notm}} header that says <strong>Try the new {{site.data.keyword.Bluemix_notm}}</strong>. Click that link to use the new interface.</dd> -->
</dl>


# rellinks
 {:class="linklist"}

## SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [SDK de Android ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core "icono de enlace externo"){: new_window} 
* [SDK de iOS ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core "icono de enlace externo"){: new_window}

<!-- {:elementKind="article" id="rellinks"} -->
