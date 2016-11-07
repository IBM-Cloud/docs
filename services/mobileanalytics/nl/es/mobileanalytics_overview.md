---

copyright:
  years: 2015, 2016

---
{:shortdesc: .shortdesc}

# Acerca de {{site.data.keyword.mobileanalytics_short}}  
{: aboutmobileanalytics}
Última actualización: 29 de agosto de 2016
{: .last-updated}

{: shortdesc}
El servicio de {{site.data.keyword.mobileanalytics_full}} proporciona información esencial sobre el uso y el rendimiento de apps para los propietarios y los desarrolladores de apps móviles. Gracias a {{site.data.keyword.mobileanalytics_short}}, los propietarios y los desarrolladores de apps pueden ver lo que sucede en el lado del usuario y aprovechar este conocimiento para compilar apps mejoradas que sean mucho más relevantes para los usuarios y que destaquen en el inmenso océano de apps móviles. 

{: #overview}  
El servicio incluye la consola de {{site.data.keyword.mobileanalytics_short}}, en la que los desarrolladores y los propietarios de apps pueden supervisar el rendimiento de las aplicaciones móviles, consultar las estadísticas de uso y buscar registros de dispositivo.  {{site.data.keyword.mobileanalytics_short}} proporciona SDK de cliente para iOS 8+ (solo Swift) y Android 4+.

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
		<dd>Cree una instancia de servicio en {{site.data.keyword.Bluemix}}, añada el SDK al proyecto, pegue dos líneas de código a la app y ya podrá recopilar numerosas métricas predefinidas.</dd>
	<!--<dt>Collect any data you want</dt>-->
		<!--<dd>Instrument apps with custom events, discover how users are interacting with your app, track purchases, and monitor app activity.  
</dd>-->
<dt>Consultar de un vistazo las métricas de todas sus apps</dt>
	<dd>La consola de {{site.data.keyword.mobileanalytics_short}} ofrece gráficos <!-- both --> ya preparados <!--and custom-->, sin necesidad de escribir consultas.</dd>
<dt>Céntrese en lo que considere importante</dt>
	<dd>Filtre las métricas por tiempo, adaptador, app, versión de app, sistema operativo, versión de sistema operativo o por modelo de dispositivo.</dd>
<dt>Detectar problemas rápidamente</dt>
	<dd>Supervise el estado de bloqueo. Establezca activadores de alertas en las métricas esenciales y enrute alertas a cualquier punto final REST. </dd>
<dt>Identificación de la causa raíz del problema</dt>
	<dd>Utilice el registro personalizado en la app y cargue de forma automática los registros para buscarlos desde la consola. Obtenga un mayor detalle de los eventos de bloqueo para consultar los seguimientos de pila. </dd>
</dl>
 

## Uso de métricas y eventos
{: #usingmetrics}

Gracias a las **métricas predefinidas** puede responder a las siguientes preguntas:

* ¿Cuántos usuarios nuevos tengo?  
* ¿Cuántas personas utilizan mi app de forma activa?  
* ¿Con qué frecuencia utilizan mi app? 
* ¿A qué hora del día utilizan mi app?  
* ¿Qué modelos de dispositivo prefieren mis usuarios? 
* ¿Cuándo debería anular el soporte para los sistemas operativos existentes? 
* ¿Qué apps tienen problemas de rendimiento?  

<!--By adding your own **custom events** you can answer questions like:--> 

<!--* What features are used most and least?-->  
<!--* Where are users entering and leaving my app?-->  
<!--* What activities are users viewing most? --> 
<!--* Are users completing workflows in the app (for example, conversion funnels)? -->  

<!--Client-side logs and usage data are gathered automatically and sent to the Mobile Analytics -->
<!-- service on demand. Developers and -->
<!-- administrators can use the {{site.data.keyword.mobileanalytics_short}} service dashboard to view data that -->
<!-- is gathered by the client SDK. -->

<!--## Data visualization
{: data-visualization}

All data that is collected by the analytics service can be visualized through the {{site.data.keyword.mobileanalytics_short}} dashboard which is accessible from your {{site.data.keyword.Bluemix_notm}} dashboard by clicking your IBM {{site.data.keyword.mobileanalytics_short}} service tile instance. You can also create custom charts, based on data that is collected by the analytics service in the dashboard. In addition to an at-a-glance view of your mobile analytics, the analytics feature includes the capability to perform a raw search against client logs, captured client crash data, and any extra data that you explicitly provide through client API function calls that feed into the {{site.data.keyword.mobileanalytics_short}} service. -->

## Preguntas frecuentes de {{site.data.keyword.mobileanalytics_short}} 
{: #faq}

<dl>
	<dt>¿Qué es {{site.data.keyword.mobileanalytics_full}}?</dt>
		<dd>{{site.data.keyword.mobileanalytics_full}} es un servicio que proporciona información histórica en tiempo real sobre el rendimiento de las apps para móviles y cómo se utilizan.  Utilizando {{site.data.keyword.mobileanalytics_short}}, los desarrolladores de apps y los propietarios de apps puede tomar decisiones de control de datos supervisando tendencias en usuarios activos, sesiones, plataformas móviles y bloqueos de app. También puede establecer alertas sobre métricas seleccionadas que, una vez desencadenadas, envían mensajes a cualquier punto final de REST, incluido un servicio de envío por push o los servicios de mensajería interna.</dd>
	<dt>¿Qué puedo hacer con la versión beta de {{site.data.keyword.mobileanalytics_short}} para {{site.data.keyword.Bluemix_notm}}?</dt>
		<dd>Como gestor de producto de la app para móviles, puede ver cuánta gente utilizar su app (métricas de usuario) y cuándo la utilizan (métricas de sesión).  Esta información se presenta como una serie temporal y se actualiza en tiempo real para que pueda ver el efecto de los cambios realizados en la app.  Puede filtrar para ver versiones específicas de la app o sistemas operativos para tomar decisiones sobre el proceso de desuso y priorización. </dd>
		<dd>Como usuario de marketing de apps para móvil, puede utilizar métricas de usuario y sesión para supervisar la colaboración, gestionar la rotación y evaluar la eficacia de las tareas de marketing de apps para móviles observando los cambios a lo largo del tiempo y correlacionando con sus fechas de sucesos.</dd>
		<dd>Como desarrollador de apps para móviles, puede utilizar las métricas de bloqueos para descubrir y resolver problemas de rendimiento de apps para móviles antes de que decepcionen a los usuarios y dañen la reputación de la app. Puede supervisar el recuento de bloqueos y el índice de bloqueos desde la consola de análisis y puede priorizar los bloqueos que afectan a la mayoría de los usuarios. Puede establecer alertas para enviar notificaciones o realizar acciones automatizadas cuando los bloqueos exceden un umbral determinado y puede resolver problemas accediendo a los detalles sobre las instancias de bloqueo para ver los registros de dispositivo y los seguimientos de pila.</dd>
	<dt>¿Necesito habilidades de analista de datos para utilizar Mobile Analytics?</dt>
		<dd>No, {{site.data.keyword.mobileanalytics_short}} ofrece una consola de análisis lista para usar para las partes interesadas del negocio y los desarrolladores de apps. No es necesario poseer habilidades de consulta.</dd>
	<dt>¿Puede realizar consultas personalizadas en mis datos analíticos?</dt>
		<dd>La versión beta de {{site.data.keyword.mobileanalytics_short}} no permite realizar consultas personalizadas, pero existe una consideración sobre esta característica en el futuro.</dd>
	<dt>¿Cómo puedo conectar mi app a {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>[Descargue nuestro SDK para iOS o Android de código abierto](install-client-sdk.html), o utilice {{site.data.keyword.mobileanalytics_short}} [API REST](https://mobile-analytics-dashboard.stage1.ng.bluemix.net/analytics-service/) para otras plataformas. </dd>
	<dt>¿En qué regiones de Bluemix está disponible {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>En el momento de esta publicación, Mobile Analytics está disponible en el Sur de Estados Unidos y Reino Unido. La disponibilidad en otras regiones está planificada pero todavía no se ha determinado el periodo de tiempo.</dd>
	<dt>¿Cuánto cuesta este servicio?</dt>
		<dd>El servicio es gratuito para la versión beta.</dd>
	<dt>¿Cuánto tiempo se conservan mis datos analíticos?</dt>
		<dd>Para la versión beta, los datos se mantienen al menos 30 días.</dd>
	<dt>¿Cuánto tiempo tardan los datos en visualizarse en la consola de {{site.data.keyword.mobileanalytics_short}}?</dt>
		<dd>Los datos en la consola de {{site.data.keyword.mobileanalytics_short}} son casi en tiempo real, lo que significa que los datos se visualizan en un periodo de segundos de los sucesos reales.</dd>
	<dt>¿Cuál es la diferencia entre {{site.data.keyword.mobileanalytics_full}} y Mobile Analytics que se encuentran en MobileFirst Platform Foundation?</dt>
		<dd>El usuario y la sesión son similares a estas dos consolas, pero la analítica que se entrega con MobileFirst Platform Foundation contiene configuraciones y métricas adicionales que permiten a los clientes gestionar su propio clúster de análisis localmente. Además, la consola de analíticas de MobileFirst Platform Foundation desglosa las métricas para adaptadores y procedimientos de adaptadores, mientras que en el servicio de {{site.data.keyword.mobileanalytics_short}}, estamos planificando integrar estas métricas en tablas y gráficos de solicitudes de red en el servicio de {{site.data.keyword.mobileanalytics_short}} (después de la versión beta).</dd>
	<dt>Estoy utilizando MobileFirst Platform Foundation localmente para desarrollar mis apps, pero no deseo alojar mi propio clúster de análisis. En su lugar, ¿puede utilizar {{site.data.keyword.mobileanalytics_full}}?</dt>
		<dd>Sí. Dispone de dos opciones: si está utilizando MobileFirst Platform Foundation 7.x u 8.0 y sus apps están instrumentadas con SDK de MobileFirst Platform, puede configurar el servidor de MobileFirst para notificar datos de análisis a {{site.data.keyword.mobileanalytics_short}} para {{site.data.keyword.Bluemix_notm}}. Lea la publicación de blog [Configuring Mobile Analytics and Mobile Foundation Bluemix services](https://mobilefirstplatform.ibmcloud.com/blog/2016/07/11/analytics-bm-service/) para obtener más detalles. Como alternativa, puede instrumentar las apps utilizando el SDK de {{site.data.keyword.mobileanalytics_short}} de {{site.data.keyword.Bluemix_notm}} y notificar directamente al servicio de {{site.data.keyword.mobileanalytics_short}}.</dd>
	<dt>Estoy intentando utilizar {{site.data.keyword.mobileanalytics_short}} y veo un espacio en blanco donde deberían estar mis gráficos. ¿Qué pasa?</dt>
		<dd>Los más probable es que utilice la interfaz de vista clásica para {{site.data.keyword.Bluemix_notm}}. La vista clásica está en desuso, por lo que la versión beta de {{site.data.keyword.mobileanalytics_short}} se ejecuta en la nueva interfaz de {{site.data.keyword.Bluemix_notm}}. Si está en la vista clásica verá un enlace en la cabecera de {{site.data.keyword.Bluemix_notm}} que dice "Try the new {{site.data.keyword.Bluemix_notm}}!". Pulse este enlace para utilizar la nueva interfaz.</dd>
</dl>


# rellinks
 {:class="linklist"}

## SDK
{: rellink-sdk}
<!-- Links to SDK download and SDK Developer Guide -->
* [SDK de Android](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-core)  
* [SDK de iOS](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-core)  

<!-- {:elementKind="article" id="rellinks"} -->
