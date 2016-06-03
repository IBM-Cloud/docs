---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} Local
{: #local}
*Última actualización: 16 de mayo de 2016*

{{site.data.keyword.Bluemix}} local proporciona la potencia y la agilidad de la plataforma basada en nubes de {{site.data.keyword.Bluemix_notm}} para el centro de datos. Con {{site.data.keyword.Bluemix_notm}} local, puede proteger las cargas de trabajo más sensibles detrás del cortafuegos de la empresa, mientras que permanecen conectadas de forma segura y en sincronización con {{site.data.keyword.Bluemix_notm}} público.
{:shortdesc}

IBM® utiliza operaciones de nube como un servicio para supervisar y mantener el entorno, de modo que puede centrarse en la construcción de apps y servicios que se ejecutan en la parte superior del entorno. IBM también maneja actualizaciones a la plataforma, de modo que puede centrarse en la empresa.

Los entornos de {{site.data.keyword.Bluemix_notm}} local tienen los mismos estándares de seguridad que {{site.data.keyword.Bluemix_notm}} público en términos de seguridad operativa. Proporcione el hardware y la infraestructura, que le proporciona control sobre la infraestructura y la seguridad física. El acceso de desarrollador a {{site.data.keyword.Bluemix_notm}} local está controlado por las políticas de LDAP, que puede configurar el equipo de {{site.data.keyword.Bluemix_notm}} al configurar el entorno. En el entorno local, utilizando la página de administración, puede gestionar los roles y permisos de usuarios.

{{site.data.keyword.Bluemix_notm}} local se suministra con todos los tiempos de ejecución de {{site.data.keyword.Bluemix_notm}} incluidos y a los 64 GB de memoria de cálculo.

Además, hay un conjunto de servicios que están disponibles como servicios locales de {{site.data.keyword.Bluemix_notm}}. Revise la tabla siguiente para ver lo que se incluye y qué hay disponible para comprar.

*Tabla 1. Servicios y tiempos de ejecución locales*

| **Tipo** | **Nombre** | **Descripción** |
|----------|----------|-----------------|
|Incluido | Tiempos de ejecución de {{site.data.keyword.Bluemix_notm}} | Utilice los tiempos de ejecución para que su app esté activa y en funcionamiento con rapidez, sin necesidad de configurar y gestionar las máquinas ni los sistemas operativos. Todos los tiempos de ejecución de {{site.data.keyword.Bluemix_notm}} están disponibles para utilizarlos en la instancia de {{site.data.keyword.Bluemix_notm}} local.|
|Opcional | {{site.data.keyword.APIM}} | Utilice el servicio de {{site.data.keyword.APIMfull}}
para componer, gestionar y socializar API. Puede importar API con recursos utilizando un URL de proxy o ensamblando datos de fuentes de datos HTTP. La ventaja de utilizar el servicio de {{site.data.keyword.APIM}} es que puede gestionar cómo se utilizan las API. |
|Incluido | {{site.data.keyword.autoscaling}}| Aumente o reduzca de forma dinámica la capacidad de recursos de cálculo de la app en función de políticas. Con este servicio, dispone de un uso ilimitado del entorno de {{site.data.keyword.Bluemix}} local.|
|Opcional | {{site.data.keyword.datacshort}} | Este servicio proporciona una cuadrícula de datos en memoria que da soporte a casos de ejemplo de memoria caché distribuidos para las apps. Incluye 50 GB de memoria caché en memoria. |
|Opcional | {{site.data.keyword.sescashort}} | Para una mayor redundancia, {{site.data.keyword.sescashort}} proporciona una réplica de una sesión almacenada en la memoria caché. Por lo tanto en el caso de una caída de la red o una interrupción, la aplicación cliente mantiene el acceso a la sesión en la memoria caché. El servicio da soporte a casos de ejemplo de almacenamiento en caché de sesión para aplicaciones web y para móvil. |
|Opcional | {{site.data.keyword.iot_full}} | Este servicio permite a las apps comunicarse y consumir datos recopilados por los dispositivos, sensores y pasarelas conectados. La oferta de base local incluye un entorno inicial que permite la ejecución de una versión privada de IBM {{site.data.keyword.iot_full}} dentro del entorno local con una capacidad de 100.000 aplicaciones o dispositivos conectados simultáneamente y 1,6 TB de intercambio de datos. |


Hay componentes opcionales que se pueden adquirir para escalar y ampliar la capacidad de los recursos y servicios. Puede adquirir cualquiera de estos componentes poniéndose en contacto con el equipo de ventas de; vaya a [Póngase en contacto con nosotros](https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs) para obtener información acerca de cómo ponerse en contacto con un representante de ventas. Para aumentar el plan para un servicio, puede seleccionar el plan en el mosaico del servicio del catálogo.

*Tabla 2. Componentes opcionales para su adquisición*

| **Nombre** | **Descripción** |
|----------|-----------------|
|Configuración de una sola vez de acceso de {{site.data.keyword.Bluemix_notm}} local | Cargo de configuración de una sola vez para desplegar y configurar el entorno local. |
|Aumento de capacidad de 16 GB en recursos de cálculo de {{site.data.keyword.Bluemix_notm}} local | Extensión de los recursos del sistema de {{site.data.keyword.Bluemix_notm}} local para proporcionar 16 GB adicionales de capacidad de memoria. |
|Aumento de capacidad de 50 GB de Datos y Sesión de {{site.data.keyword.Bluemix_notm}} | Entorno que permite desplegar y ejecutar instancias de caché de datos y caché de sesión hasta una capacidad acumulativa de 50 GB. |
|Aumento de capacidad de 500 llamadas de API {{site.data.keyword.APIM}} de {{site.data.keyword.Bluemix_notm}} local | Un entorno que permite ejecutar una versión privada de {{site.data.keyword.APIM}} para {{site.data.keyword.Bluemix_notm}} con una capacidad de 500 llamadas de API por segundo. |
|Aumento incremental de {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.iot_short}} local | Un entorno adicional para la oferta de servicio base de {{site.data.keyword.iot_full}} local que permite ejecutar una versión privada de {{site.data.keyword.iot_full}} dentro del entorno local con una capacidad de  100.000 aplicaciones o dispositivos conectados simultáneamente y 0,5 TB de intercambio de datos. |


**Nota**: Los componentes de {{site.data.keyword.Bluemix_notm}} local pueden iniciar una capacidad configurada específica, como gigabytes o transacciones por segundo. Dado que la capacidad actual en la práctica para cualquier configuración del servicio de nube varía en función de muchos factores, la capacidad real en la práctica puede ser más o menos que la capacidad configurada.

### Catálogo sindicado

{{site.data.keyword.Bluemix_notm}} local incluye un catálogo privado y sindicado que muestra los servicios locales que están disponibles de forma exclusiva para el usuario. También incluye servicios adicionales que tiene disponibles para utilizar desde {{site.data.keyword.Bluemix_notm}} público.

El catálogo sindicado proporciona la función para crear apps híbridas que constan de servicios públicos y privados. Tiene la opción de decidir qué servicios públicos cumplen los requisitos de su empresa en función de sus criterios de privacidad de datos y de seguridad. Si es una instancia privada del servicio para el entorno local, verá una etiqueta "Local" con los mosaicos del servicio en el catálogo. De forma parecida, si es un servicio personalizado, verá "Personalizado" listado con el mosaico del servicio.  

*Tabla 3. Servicios disponibles para la sindicación desde {{site.data.keyword.Bluemix_notm}} público por región*

|Servicio	|Disponible en la región EE.UU. sur	|Disponible en la región Europa Reino Unido |Disponible en la región Australiana Sídney|
|:----------|:------------------------------|:------------------|:------------------|
|{{site.data.keyword.alchemyapishort}} 		|Sí	   	|Sí  		|Sí|
|{{site.data.keyword.alertnotificationshort}}		|Sí		|Sí			|Sí		|
|{{site.data.keyword.appseccloudshort}}		|Sí		|Sí		|Sí |
|{{site.data.keyword.hadoopst}}			|Sí		|No		|No |
|{{site.data.keyword.APIM}}			|Sí		|Sí		|Sí |
|{{site.data.keyword.rules_short}}		|Sí		|Sí		|Sí |
|{{site.data.keyword.cloudant}}			|Sí		|Sí		|Sí |
|{{site.data.keyword.conceptexpansionshort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.conceptinsightsshort}}	|Sí		|Sí		|Sí |
|{{site.data.keyword.dashdbshort}}		|Sí		|Sí		|Sí |
|{{site.data.keyword.dataworks_short}}		|Sí		|Sí		|No|
|{{site.data.keyword.DB2OnCloud_short}}		|Sí		|Sí		|Sí |
|{{site.data.keyword.dialogshort}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.documentconversionshort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.game}}			|No		|No		|Sí |
|{{site.data.keyword.geospatialshort_Geospatial}}	|Sí	|Sí		|Sí |
|{{site.data.keyword.GlobalizationPipeline_short}}	|Sí		| Sí		| Sí |
|{{site.data.keyword.identitymixershort}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.twittershort}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.weather_short}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.languagetranslationshort}}	|Sí		|Sí		|Sí |
|{{site.data.keyword.eventhubshort}}		|Sí		|No		|No|
|{{site.data.keyword.messagehub}}		|Sí		|Sí		|No|
|{{site.data.keyword.macm_short}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.manda}}			|Sí		|Sí		|Sí |
|{{site.data.keyword.amashort}}			|Sí		|Sí		|Sí |
|{{site.data.keyword.mqa}}			|Sí		|Sí		|Sí |
|{{site.data.keyword.mql}}			|Sí		|Sí		|Sí |
|{{site.data.keyword.nlclassifierlshort}} 	|Sí 		|Sí 		|Sí|
|{{site.data.keyword.personalityinsightsshort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.pm_short}}			|Sí		|Sí		|No |
|{{site.data.keyword.presenceinsightsshort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.mobilepush}}		|Sí		|Sí		|Sí |
|{{site.data.keyword.questionandanswershort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.relationshipextractionshort}}	|Sí	|Sí		|Sí|
|{{site.data.keyword.retrieveandrankshort}}	|Sí 		|Sí 		|Sí|
|{{site.data.keyword.runbook_short}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.SecureGateway}}		|Sí		|Sí		|Sí |
|{{site.data.keyword.ssofull}}			|Sí		|No		|No|
|{{site.data.keyword.speechtotextshort}}	|Sí 		|Sí	 	|Sí|
|{{site.data.keyword.streaminganalyticsshort}}	|Sí		|Sí		|Sí |
|{{site.data.keyword.texttospeechshort}} 	|Sí 		|Sí	 	|Sí|
|{{site.data.keyword.toneanalyzershort}} 	|Sí 		|Sí 		|Sí|
|{{site.data.keyword.tradeoffanalyticsshort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.visualinsightsshort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.visualrecognitionshort}}	|Sí 		|Sí	 	|Sí|
|{{site.data.keyword.iot_short}}		|Sí		|Sí		|No|
|{{site.data.keyword.workflow}}			|Sí		|Sí		|Sí |
|{{site.data.keyword.workloadscheduler}}	|Sí		|Sí		|Sí |

## Arquitectura de {{site.data.keyword.Bluemix_notm}} local
{: #localarch}

{{site.data.keyword.Bluemix_notm}} local forma parte de una máquina virtual que está detrás del cortafuegos de la empresa, lo que le permite disponer de la infraestructura de nube de alto rendimiento y más segura. IBM instala, supervisa de forma remota y gestiona
{{site.data.keyword.Bluemix_notm}} local en su centro de datos gracias a la tecnología Relay de IBM. Revise el diagrama
siguiente para obtener información sobre cómo se configura {{site.data.keyword.Bluemix_notm}} en su entorno local y
cómo IBM mantiene su instancia local:

![{{site.data.keyword.Bluemix_notm}} Local.](images/localarch.png "Diagrama de la arquitectura de Bluemix local")

*Figura 1. Arquitectura de {{site.data.keyword.Bluemix_notm}} local*

La máquina virtual inicial se ejecuta detrás del cortafuegos del cliente en una red que tiene conectividad saliente al centro de operaciones de IBM a través del Relé. Los componentes de la plataforma de {{site.data.keyword.Bluemix_notm}} y las funciones principales que dan soporte a los componentes de la plataforma, se ejecutan en una red de área local virtual aislada y privada (VLAN). {{site.data.keyword.Bluemix_notm}} Local utiliza una VLAN para la subred privada. El uso de una subred privada en lugar de una VLAN pública es más seguro y puede ayudar a evitar problemas de direccionamiento. El conjunto de funciones centrales que dan soporte
a la plataforma son:

<dl>
<dt>**Supervisión y registro**</dt>
<dd>Las funciones de supervisión y registro se despliegan en sus centros de datos por medio de Relay, y los datos permanecen en su
centro de datos. Las alertas se envía a las operaciones de IBM, según los criterios de alerta definidos. En las alertas que se envía a IBM no se incluye información confidencial en ningún caso.</dd>
<dt>**Red**</dt>
<dd>Relay es la red de entrega incluida en {{site.data.keyword.Bluemix_notm}} Local. Relay permite a IBM aportar
de forma automática y constante las actualizaciones más recientes a todos los despliegues locales, con lo que el cliente siempre
dispone de un sistema seguro y totalmente actualizado. El tráfico en este túnel es una actividad automatizada para el servicio y
mantenimiento de la plataforma, los recursos de cálculo y los servicios para su instancia. El tráfico incluye la prestación de supervisión
que utilizan las operaciones de IBM para llevar a cabo la determinación de problemas de su instancia local. Para obtener más información sobre
Relay, consulte [Relay](index.html#localrelay).</dd>
<dt>**Compute**</dt>
<dd>{{site.data.keyword.Bluemix_notm}} local utiliza entornos de ejecución centrados en la app basados en Cloud Foundry.</dd>
<dt>**Inteligencia de seguridad **</dt>
<dd><p>IBM utiliza la plataforma Radar Security Intelligence para obtener una arquitectura unificada para la integración
de varios componentes clave. Estos componentes incluyen información de seguridad y gestión de sucesos,
gestión de registros, detección de anomalías, actividades forenses de incidencias y gestión de configuración y vulnerabilidades. Bluemix también utiliza la información de seguridad de IBM QRadar y la gestión de sucesos (SIEM) para supervisar acciones de usuarios
privilegiados y los intentos de inicio de sesión tanto correctos como incorrectos de los desarrolladores de aplicaciones. Los informes de
QRadar proporcionan al cliente visibilidad sobre los datos de suceso a través de la sección Informes y registros en la página Administración. Para obtener información sobre los informes de seguridad, consulte [Visualización de informes](../admin/index.html#oc_report).</p>
<p>IBM BigFix garantiza que los arreglos de los sistemas operativos se aplican con la frecuencia adecuada. El proceso de aplicación de parches está automatizado, y la planificación se acuerda entre usted e IBM. Para obtener información sobre el mantenimiento y actualizaciones, consulte
[Mantenimiento de su instancia local](index.html#maintainlocal).</p>
</dd>
</dl>

Sus apps se despliegan dentro de contenedores virtuales que se ejecutan en máquinas virtuales de Cloud Foundry. Todos los componentes
de Cloud Foundry, como los controladores de nube, los gestores de estado, direccionadores y agentes de ejecución de droplet (DEA)
se despliegan cuando se configura {{site.data.keyword.Bluemix_notm}}. Los diversos componentes de gestión de {{site.data.keyword.Bluemix_notm}} también se incluyen en el despliegue de {{site.data.keyword.Bluemix_notm}}.

Los dispositivos DataPower proporcionan acceso a los dominios de aplicaciones de {{site.data.keyword.Bluemix_notm}}. Estos dispositivos se conectan a la red accesible desde la intranet. Sus usuarios que despliegan las apps y los servicios obtienen acceso de la red a la que se puede acceder desde la intranet. Debe proporcionar siete direcciones IP que tienen acceso a Internet de salida. Los dispositivos de DataPower se direccionan desde estas direcciones IP de cliente al despliegue de {{site.data.keyword.Bluemix_notm}} aislado. Para obtener más información sobre las especificaciones de red y los requisitos de infraestructura, consulte [Requisitos de infraestructura locales de {{site.data.keyword.Bluemix_notm}}](../local/index.html#localinfra).

### Relay (Relé)
{: #localrelay}

Relay es una prestación de entrega que se incluye en {{site.data.keyword.Bluemix_notm}} Local. Relay permite a IBM aportar
de forma automática y constante las actualizaciones más recientes a todos los despliegues locales, con lo que el cliente siempre
dispone de un sistema seguro y totalmente actualizado. El relé consigue una conectividad segura mediante un túnel VPN y una SSL abierta y saliente que se origina a partir de la máquina virtual inicial utilizando certificados específicos para cada instancia de {{site.data.keyword.Bluemix_notm}} local. Todos los releases iniciales de {{site.data.keyword.Bluemix_notm}} están disponibles en la máquina virtual inicial, que también actúa como una máquina agente de automatización para despliegues y actualizaciones. La conexión SSL se origina desde la máquina virtual inicial.  Una vez que se ha establecido una conexión segura en
el servidor de automatización de {{site.data.keyword.Bluemix_notm}}, se puede comprobar la aceptación y la coherencia
de los releases de {{site.data.keyword.Bluemix_notm}} y empieza el despliegue de las actualizaciones.

El tráfico en este túnel es una actividad automatizada para el servicio y
mantenimiento de la plataforma, los recursos de cálculo y los servicios para su instancia. El tráfico incluye la prestación de supervisión
que utilizan las operaciones de IBM para llevar a cabo la determinación de problemas de su instancia local. El puerto web de salida 443 se utiliza para esta conexión. IBM utiliza la función Relay para la entrega de actualizaciones de la plataforma por medio de actividades consistentes de
pruebas y validaciones. Este proceso asegura que todos los despliegues que se envía a sus entornos locales son estables y seguros.

Solo el equipo de IBM que trabaja junto con usted en su entorno local puede acceder de forma segura a su
instancia de {{site.data.keyword.Bluemix_notm}}. El acceso a su entorno local se protege mediante el uso de autenticación por dos factores, durante varios pasos en el proceso de conexión. IBM
proporciona una lista de los usuarios y los ID aprobados que pueden acceder a su entorno, y luego puede auditar los accesos a su entorno. Al generar
un informe de seguridad, puede detectar quién accede a su entorno, cuando y por qué. Para obtener información sobre la generación de
informes de seguridad, consulte [Informes de seguridad](../security/index.html#reports).

El entorno está completamente visible para usted, como administrador, para gestión de incidencias, problemas, cambios, capacidad y seguridad. Puede
acceder a la información sobre su entorno usando la página de Administración. La tecnología Relay mantiene actualizada la página Administración
con los datos más recientes. Para obtener más información sobre el acceso de usuario, los registros de seguridad, el control de catálogos sindicados y la comunicación sobre las actualizaciones y la reparación de problemas, consulte [Gestión de {{site.data.keyword.Bluemix_notm}} local y de {{site.data.keyword.Bluemix_notm}}dedicado](../admin/index.html#mng).

##Configuración de la instancia de {{site.data.keyword.Bluemix_notm}} local
{: #setuplocal}

{{site.data.keyword.Bluemix_notm}} local se ha diseñado para proporcionar una versión privada del producto {{site.data.keyword.Bluemix_notm}} público alojado en su propio hardware, gestionado por el usuario. Puede utilizar servicios y tiempos de ejecución de {{site.data.keyword.Bluemix_notm}} para satisfacer sus necesidades de cálculo en un entorno de nube seguro, alojado por el cliente y gestionado.

IBM le proporciona acceso a {{site.data.keyword.Bluemix_notm}} local mediante un inicio de sesión protegido por contraseña. Puede acceder a los servicios, tiempos de ejecución y recursos asociados, y desplegar y eliminar apps {{site.data.keyword.Bluemix_notm}}. Revise los pasos siguientes para trabajar con el representante de IBM para configurar la instancia local de {{site.data.keyword.Bluemix_notm}}.

Para configurar su versión privada de {{site.data.keyword.Bluemix_notm}}:

<ol>
<li>Revise los requisitos de infraestructura de <a href="index.html#localinfra">{{site.data.keyword.Bluemix_notm}} local</a> para configurar la instancia local.</li>
<li>Póngase en contacto con el representante designado de la cuenta de IBM o con el equipo de <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}</a> para empezar a trabajar.</li>
<li>Establezca su acuerdo de {{site.data.keyword.Bluemix_notm}} local con IBM, que incluye fechas de objetivo de entrega.
	<ol type="a">
	<li>Trabaje con IBM, a cargo del cliente, para configurar la instancia de {{site.data.keyword.Bluemix_notm}} local. El cargo mensual se basa en los servicios locales que desee utilizar, más una suscripción a todos los servicios públicos de {{site.data.keyword.Bluemix_notm}}. Recibirá una factura por todo lo que utilice por encima del acuerdo de suscripción.</li>
	<li>Identifique los plazos límite para cada fase de la configuración de la instancia de {{site.data.keyword.Bluemix_notm}} local.</li>
	</ol>
	</li>
<li>Una vez que se cree la plataforma y la cuenta, identifique las personas de la organización para los roles necesarios para configurar y activar la instancia local. Para obtener más información sobre los roles que asigne, consulte Roles y responsabilidades de <a href="index.html#rolesresponsibilities" target="_blank"> local y {{site.data.keyword.Bluemix_notm}}</a>.
</li>
<li>El usuario proporciona el hardware, e IBM le ayuda a definir y a establecer la conectividad de red entre su red corporativa y la instancia de {{site.data.keyword.Bluemix_notm}} local. Para obtener más información sobre los requisitos de la infraestructura, consulte requisitos de la infraestructura de <a href="index.html#localinfra">{{site.data.keyword.Bluemix_notm}} local</a>.
	<ol type="a">
	<li>IBM configura el acceso a la red y LDAP en función de lo que proporcione el usuario. Se ofrece acceso de administración a los contactos que designe el cliente. También debe designar un contacto para soporte y facturación.</li>
	<li>IBM configura un catálogo sindicado en el entorno local para mostrar los servicios locales y muchos de los servicios públicos de {{site.data.keyword.Bluemix_notm}}.</li>
	<li>El cliente debe validar la configuración de la red y del cortafuegos, además del punto final LDAP y el acceso.</li>
	</ol>
</li>
</ol>

Puede prever un proceso similar a la siguiente lista para el despliegue y la configuración iniciales de su entorno. Para obtener detalles sobre la persona responsable de cada tarea, consulte [Roles y responsabilidades](../local/index.html#rolesresponsibilities).

<ol>
<li>Proporcione la configuración de VMware que cumpla las especificaciones para calcular recursos, la red y el almacenamiento. Para obtener más información sobre los requisitos de la infraestructura, consulte <a href="../local/index.html#localinfra">Requisitos de infraestructura local de {{site.data.keyword.Bluemix_notm}}</a>.</li>
<li>Proporcione las credenciales de clúster de vCenter que utilizará la máquina virtual inicial. Debe proporcionar la siguiente información:
<ul>
<li>Nombre del clúster VMware</li>
<li>Credenciales del clúster vCenter incluidos el ID de usuario y la contraseña</li>
<li>Nombre o nombres del almacén de datos (nombre del LUN de almacenamiento)</li>
<li>ID de VLAN/grupo de puertos VMware</li>
<li>Nombre de agrupación de recursos</li>
</ul>
</li>
<li>Usted e IBM trabajan conjuntamente para validar las credenciales que ha proporcionado en la tarea anterior.</li>
<li>Debe proporcionar 7 direcciones IP en la red. Si tiene un proxy web protegido para permitir el acceso de salida a Internet para componentes internos de {{site.data.keyword.Bluemix_notm}}, debe proporcionar las credenciales para conectarse a él.
<p>**Nota**: Si el proxy web no es seguro, no necesita proporcionar las credenciales. Además, tenga en cuenta que no todos los clientes locales de {{site.data.keyword.Bluemix_notm}} utilizan un proxy web.</p></li>
<li>IBM proporciona una lista blanca de los URL que deben estar permitidos a través del proxy web antes de iniciar el despliegue.<br />
<p>**Nota**: La lista blanca de los URL no contiene sitios web como twitter.com, facebook.com y youtube.com. Si estos URL no están permitidos, es posible que determinados servicios y áreas de {{site.data.keyword.Bluemix_notm}} no es puedan utilizar.</p>
</li>
<li>Debe especificar los nombres de dominio para el despliegue, y los ID que desea utilizar. Obtendrá dos dominios definidos parcialmente al configurar la instancia local, y seleccione el prefijo para los dos dominios. Por ejemplo, seleccione el prefijo para <code>*mycompany*.bluemix.net</code> y <code>*mycompany*.mybluemix.net</code>. Y, a continuación, también puede seleccionar el dominio completo para crear un dominio personalizado.
<p>Puede elegir tantos dominios personalizados como desee. Sin embargo, el usuario es responsable de los certificados para los dominios personalizados. Para obtener información sobre cómo crear el dominio personalizado, consulte <a href="../manageapps/updapps.html#domain">Creación y utilización de un dominio personalizado</a>.</p></li>
<li>Puede elegir qué tecnología, IPSec o túnel OpenVPN utilizará para configurar el Relé para volver a conectarse al centro de operaciones de IBM.</li>
<li>IBM instala e inicia la máquina virtual inicial dentro del clúster de {{site.data.keyword.Bluemix_notm}}. Si proporciona su propio VMware, un representante de IBM ayuda a su representante del cliente a completar esta tarea.</li>
<li>IBM configura el Relé para comunicarse de nuevo con el centro de operaciones de IBM.</li>
<li>El repositorio de máquina virtual inicial detiene los artefactos de compilación actualizados.</li>
<li>Proporcione las credenciales para IBM para conectarse con la instancia de directorios LDAP corporativos.</li>
<li>IBM utiliza la automatización para desplegar la plataforma central de {{site.data.keyword.Bluemix_notm}}.</li>
<li>IBM despliega la plataforma principal que incluye los tipos de ejecución elásticos, la consola, la función de administración y la supervisión.</li>
<li>IBM configura el acceso administrativo al entorno.</li>
<li>IBM enlaza el catálogo sindicado desde el despliegue local a una instancia pública de {{site.data.keyword.Bluemix_notm}} para su uso de los servicios públicos. Hay disponible un conjunto de servicios públicos en la instancia local de forma predeterminada. Puede utilizar la página de administración para la gestión de catálogos para activar o desactivar los servicios para la instancia local.</li>
<li>Puede empezar a utilizar la instancia local supervisada por el equipo de operaciones de IBM para responder a las alertas.</li>
</ol>

Una vez que se configure la instancia de {{site.data.keyword.Bluemix_notm}}, puede supervisar y gestionar la instancia de {{site.data.keyword.Bluemix_notm}} utilizando la página Administración. Para obtener más información, consulte [Gestión de {{site.data.keyword.Bluemix_notm}} local y dedicado](../admin/index.html#mng). Para obtener información sobre las actualizaciones y el mantenimiento, consulte [Mantenimiento de la instancia local](index.html#maintainlocal).

##Roles y responsabilidades
{: #rolesresponsibilities}

Si establece una cuenta de {{site.data.keyword.Bluemix_notm}} local, puede identificar a las personas de su organización para los roles necesarios para configurar y activar la instancia.

###Roles

La lista siguiente muestra los roles y responsabilidades de cliente que se asignan:

<dl>
<dt>**Contacto de suministro**</dt>
<dd>Trabaja con el representante de IBM en el establecimiento del entorno de {{site.data.keyword.Bluemix_notm}} local, incluida la identificación de las personas adecuadas de la organización que trabajarán en cualquier aspecto del proyecto. La persona asignada a este rol supervisa la selección del patrón, las formas comerciales y la disposición de acceso a los recursos del cliente. El contacto de suministro es el contacto general para configurar la instancia local.</dd>
<dt>**Responsable de suministro**</dt>
<dd>Trabaja con el representante de IBM para seleccionar una topología y opción de despliegue que se ajuste a sus requisitos de seguridad. La persona asignada a este rol trabaja con el asesor de suministro de IBM para determinar qué patrones de despliegue consiguen los objetivos y las metas de conformidad.</dd>
<dt>**Especialista en redes**</dt>
<dd>Trabaja con el representante de IBM en los planes de red para el despliegue de {{site.data.keyword.Bluemix_notm}}. La persona asignada a este rol revisa las especificaciones de red necesarias para IBM y trabaja conjuntamente con IBM en un plan de implementación. Al final de la fase de instalación y de verificación, la persona asignada a este rol concluirá que la configuración de red está en conformidad con los estándares corporativos.</dd>
<dt>**Contacto de DevOps**</dt>
<dd>Trabaja con el representante de IBM para planificar y aplicar las actualizaciones de mantenimiento necesarias para la plataforma, servicios y tiempos de ejecución de {{site.data.keyword.Bluemix_notm}}. La persona asignada a este rol también trabaja con el representante de IBM en la configuración de la instancia de {{site.data.keyword.Bluemix_notm}} local.</dd>
<dt>**Especialista IaaS**</dt>
<dd>Trabaja con los representantes de IBM en el plan de despliegue para VMware. Normalmente se trata de algún administrador de VMware en el centro de datos. La persona asignada a este rol revisa los requisitos de infraestructura de <a href="../local/index.html#localinfra">{{site.data.keyword.Bluemix_notm}} local</a> y trabaja conjuntamente con IBM en un plan de implementación. Al final del despliegue, la persona asignada a este rol concluye que el despliegue cumple los estándares corporativos en la capa IaaS.</dd>
</dl>

Los representantes de los clientes trabajan con los especialistas de IBM que trabajan conjuntamente para asegurarse de que siempre tenga el soporte que necesita. Puede actualizar al nivel de soporte Premium para trabajar con un CSM (Client Success Manager) dedicado para su cuenta. Para obtener más información sobre los distintos niveles de soporte, consulte [Cómo obtener soporte](../support/index.html#contacting-support). El CSM completa los siguientes tipos de tareas:


<ul>
<li>Ofrece coordinación técnica entre usted e IBM.</li>
<li>Coordina actualizaciones, ayuda de expertos de IBM y una habilitación inicial de un ingeniero de soporte de {{site.data.keyword.Bluemix_notm}}.</li>
<li>Proporciona información sobre los tipos de soporte que están disponibles.</li>
<li>Actúa como punto de escalada inicial, si es necesario.</li>
</ul>

El equipo de soporte y operaciones de {{site.data.keyword.Bluemix_notm}} que trabaja con usted en la instancia de {{site.data.keyword.Bluemix_notm}} puede acceder a su entorno local, pero solo por los siguientes motivos:

<ul>
<li>Para responder a las alertas y realizar tareas de mantenimiento operativo</li>
<li>Para intentar reproducir un problema notificado en una incidencia de soporte</li>
</ul>

###Responsabilidades

Desde configurar su entorno hasta efectuar tareas de mantenimiento continuado, hay una gran variedad de tareas que deben llevar a cabo usted e IBM. En las tablas siguientes se describen las tareas necesarias, así como los encargados de llevar a cabo la tarea durante la fase inicial, de progresión y de finalización.

La fase inicial se utiliza para establecer el entorno de {{site.data.keyword.Bluemix_notm}} local. En este punto, ya ha revisado los [requisitos de la infraestructura local](../local/index.html#localinfra). Los objetivos principales de dicha fase son los siguientes:

- Revisar el acuerdo financiero y establecer las fechas objetivo para la entrega.
- Crear la plataforma {{site.data.keyword.Bluemix_notm}} y proporcionar acceso a tiempos de ejecución y servicios.
- Definir y establecer la conectividad de red entre su red corporativa y las operaciones de {{site.data.keyword.Bluemix_notm}}.
- Identificar y asignar roles al equipo de administración.

*Tabla 4. Tareas de fases iniciales*

| **Tarea** | **Detalles de la tarea** | **Parte responsable** |
|----------|------------------|-----------------------|
|Establecer estándares de conformidad | Identificar estándares gubernamentales, sectoriales y de propiedad corporativa necesarios para el entorno. | Cliente |
|Crear un plan de seguridad y de integración de conformidad | Crear un plan de seguridad e integración que incluya costes, planificación y recursos necesarios para conseguir la conformidad de seguridad. | IBM |
|Aprobación de un plan de conformidad | Aprobar el plan de conformidad. | Cliente |
|Crear una variación de tamaño para los entornos |  	Crear una variación de tamaño de los entornos en función de opciones predefinidas que tengan en cuenta los objetivos de alta disponibilidad y la recuperación en caso de error, así como el DEA inicial y el suministro de servicios necesario para dar soporte a las apps creadas con la plataforma. Usted e IBM trabajan conjuntamente para definir, por ejemplo, qué bases de datos son necesarias, qué servicios se ofrecen en el catálogo sindicado del cliente, entre otros. | Responsabilidad compartida de IBM y el cliente |
|Seleccionar una arquitectura | Seleccionar una arquitectura basada en opciones predefinidas que tengan en cuenta requisitos de alta disponibilidad y de recuperación en caso de desastre. | IBM |
|Definir objetivos de recuperación en caso de error | Definir los requisitos de recuperación en caso de error para el entorno. | Cliente |
|Crear un plan de recuperación en caso de error | Consultar y definir el plan de recuperación en caso de error. IBM crea un modelo de recuperación en caso de error y le consulta donde debe proporcionar comentarios y aprobar el plan. | Responsabilidad compartida de IBM y el cliente |
|Crear un plan de copia de seguridad y recuperación | Crear un plan de copia de seguridad y recuperación que defina la frecuencia y los requisitos para la distribución interna y externa de la copia de seguridad. IBM hace copia de seguridad de los componentes de la plataforma, de servicios de IBM y
metadatos de servicio, incluyendo los roles de usuario y otros elementos. Debe realizar una copia de seguridad de todos los datos específicos de app de los que sea responsable. | Responsabilidad compartida de IBM y el cliente |
|Identificar herramientas para la detección de sucesos y la determinación de problemas | identificar herramientas de IBM y de terceros utilizadas para la detección de sucesos y la determinación de problemas en el nivel de plataforma de {{site.data.keyword.Bluemix_notm}}. | IBM |
|Definir un plan de escalamiento | Definir el plan de escalamiento para seleccionar y resolver sucesos detectados desde los componentes de supervisión. | IBM |
|Firmar acuerdos de infraestructuras, plataformas y soporte | Firmar el acuerdo de suscripción, incluidos los términos y condiciones financieros del entorno. Firmar la suscripción de soporte. | Cliente |
|Obtener un entorno | Conseguir recursos informáticos, de redes y almacenamiento. Para obtener más información sobre los requisitos de la infraestructura del entorno, consulte los [requisitos de la infraestructura local](../local/index.html#localinfra). | Cliente |
|Instalar una solución VPN | Instalar una solución VPN bidireccional. | IBM |
|Instalar plataforma, aplicación, y componentes de supervisión y gestión | Instalar, configurar y verificar componentes de la plataforma, como BOSH Director, Cloud Controller, Health Manager, mensajería, routers, DEA y proveedores de servicios y los componentes de supervisión definidos en el plan de escalamiento y detección de problemas. | IBM |
|Instalar y configurar componentes de seguridad | Instalar y configurar componentes de seguridad enlazados con el plan de supervisión y escalamiento, incluyendo IBM QRadar, almacén de credenciales, sistema de prevención de intrusión, IBM BigFix e IBM Security Privileged Identity Management. | IBM |
|Configurar un servidor de inicio de sesión | Configurar el servidor de inicio de sesión para utilizarlo con el LDAP corporativo. | IBM |
|Instalar y configurar componentes personalizados |  	Instalar y configurar componentes personalizados que residen fuera del ámbito del producto y los servicios de {{site.data.keyword.Bluemix_notm}}. | Cliente |
|Conectar el conducto de {{site.data.keyword.Bluemix_notm}} | Conectar la integración continua y el conducto de entrega continua de {{site.data.keyword.Bluemix_notm}} con repositorios de IBM. | IBM |
|Personalizar componentes de soluciones externas | Personalizar equilibradores de carga para escenarios de recuperación en caso de error. | Cliente |
|Hacer un seguimiento del estado de la seguridad, la conformidad y los controles de auditoría  | Hacer un seguimiento del estado hasta el punto en que todas las herramientas y procesos estén en regla para conseguir la conformidad identificada. | Cliente |
|Revisar la infraestructura física | Revisar las instalaciones físicas que alojan los componentes de la solución para detectar amenazas y revisar los controles de seguridad para proteger el centro de datos. | Cliente |
|Inspeccionar el software de supervisión | Inspeccionar los componentes de supervisión y gestión, como se define en el plan de escalamiento y determinación de problemas. | Cliente |
|Inspeccionar el SO | Inspeccionar y asegurarse de que la imagen del sistema operativo cumple los estándares de conformidad. IBM proporciona acceso a la imagen del SO. | Responsabilidad compartida de IBM y el cliente |

A continuación tenemos la fase de progresión. En la fase de progresión se describe la relación de colaboración entre usted e IBM. Los objetivos principales de esta fase son los siguientes:

- Revisar la capacidad y coordinar los ajustes necesarios.
- Revisar el mantenimiento y las mejoras en la plataforma.
- Coordinar las actividades para la resolución de problemas y analizar las causas originarias.

*Tabla 5. Tareas de la fase de progresión*

| **Tarea** | **Detalles de la tarea** | **Parte responsable** |
|----------|------------------|-----------------------|
|Revisar informes de capacidad semanalmente | Revisar los informes de capacidad semanalmente y tomar acciones de corrección, si procede. | Cliente |
|Crear proyecciones mes a mes | Recopilar información y crear una proyección mes a mes de la capacidad y el consumo. | Responsabilidad compartida de IBM y el cliente |
|Revisar las proyecciones de capacidad | Revisar las proyecciones de capacidad relacionadas con sucesos externos que puedan afectar a la capacidad, así como la previsión de nuevos despliegues de apps. Trabajar con IBM para revisar las proyecciones y efectuar una planificación según convenga. | Responsabilidad compartida de IBM y el cliente |
|Ajustar la capacidad |  Añadir o eliminar capacidad a medida que cambien sus necesidades. | IBM |
|Publicar actualizaciones venideras y realizar mantenimiento | Crear documentación para el mantenimiento necesario de los componentes de IBM. | IBM |
|Realizar tareas de mantenimiento | Trabajar con IBM para planificar tareas de mantenimiento necesarias en un intervalo de 21 días. Puede proporcionar fechas que no le vayan bien en dicho período de 21 días, e IBM trabajará para planificar el mantenimiento según convenga. | Responsabilidad compartida de IBM y el cliente |
|Abordar fallos de aprovisionamiento | Corregir fallos de aprovisionamiento, si se producen, de los servicios creados por el cliente desplegados en el catálogo. | IBM |
|Realizar exploraciones de red y de IP | Realizar exploraciones diarias y mensuales de red y de IP. | Responsabilidad compartida de IBM y el cliente |
|Proporcionar acceso a los registros de auditoría | Proporcionar acceso a todos los registros de auditoría de seguridad y administración.   | Responsabilidad compartida de IBM y el cliente |
|Realizar pruebas | Realizar pruebas Key Controls over Operations (KCO) periódicas y pruebas de penetración de terceros. | Responsabilidad compartida de IBM y el cliente |
|Informes de estado, coordinación de auditorías y reuniones de conformidad  | Efectuar informes de estado, coordinación de auditorías externas y representación en reuniones de estado de revisión de conformidad. | IBM |
|Verificación de necesidades empresariales y de ocupación | Efectuar verificaciones de ocupación trimestrales y verificaciones de necesidades empresariales continuadas para los representantes de IBM que tienen acceso al entorno del cliente. | IBM |
|Resolución de vulnerabilidades de seguridad | Resolver vulnerabilidades de seguridad notificadas en la plataforma. | IBM |

La etapa final de la finalización representa el final de la relación entre usted e IBM {{site.data.keyword.Bluemix_notm}}. Las tareas principales de esta fase son las siguientes:

* Finalización del acuerdo financiero
* Eliminación de todas las conexiones de red
* Reciclaje de la infraestructura

*Tabla 6. Tareas de la fase de finalización*

| **Tarea** | **Detalles de la tarea** | **Parte responsable** |
|----------|------------------|-----------------------|
|Finalizar el acuerdo financiero | Debatir y acordar el contrato del acuerdo financiero. | Responsabilidad compartida de IBM y el cliente |
|Retirar el entorno | Cerrar el acceso y retirar las credenciales del entorno. | Responsabilidad compartida de IBM y el cliente |
|Finalizar el relé | Terminar la conexión del relé. | IBM |
|Reciclar la infraestructura | Reciclar la infraestructura de acuerdo con las directrices de la empresa. | Cliente |

## Requisitos de infraestructura de {{site.data.keyword.Bluemix_notm}} local
{: #localinfra}

En {{site.data.keyword.Bluemix_notm}} local, usted es
el propietario de la seguridad física y de la infraestructura para alojar la instancia local. IBM establece los siguientes requisitos mínimos para configurar {{site.data.keyword.Bluemix_notm}} local.

### Hardware

Aunque hay requisitos para el tipo y el tamaño del hardware disponible, puede elegir cualquier
combinación que cumpla los requisitos totales de los recursos definidos.

<dl>
<dt>**Hardware VMware ESXi**</dt>
<dd>
ESXi es una capa de virtualización que se ejecuta en servidores físicos y que abstrae el procesador,
la memoria, el almacenamiento y los recursos en varias máquinas virtuales. Elija cualquier combinación que cumpla los siguientes totales de recursos, con la condición de que el recuento mínimo de núcleos físicos por ESXi sea ocho. Las siguientes especificaciones son sólo para el tiempo de ejecución de núcleo de {{site.data.keyword.Bluemix_notm}}.
<ul>
<li>48 núcleos físicos a 2,0 o más GHz cada uno</li>
<li>756 GB de memoria RAM física</li>
<li>Tamaño total de almacenes de datos: 7,5 TB
<ul>
<li>7 TB de almacén de datos para alojar {{site.data.keyword.Bluemix_notm}}</li>
<li>500 GB de almacén de datos para alojar la máquina virtual inicial</li>
</ul>
</li>
</ul>
<p><strong>Nota:</strong> Si utiliza varios almacenes de datos, utilice el mismo prefijo para cada uno de ellos.</p>
</dd>
<dt>**Alta disponibilidad**</dt>
<dd>
Para poder dar soporte a un solo error de nodo debe tener n+1 ESXi. Por ejemplo, si se utilizan tres ESXi (es decir, 16x núcleos cada uno), se necesita un cuarto.
<p><strong>Nota:</strong> El administrador de VMware del cliente puede optar por aplicar
una migración tras error estricta de alta disponibilidad en el clúster para garantizar los recursos.</p>
</dd>
<dt>**Red**</dt>
<dd>
Entre los requisitos recomendados se incluye un grupo de puertos accesibles para el cliente con siete direcciones IP de red del cliente que tienen acceso saliente a Internet en la misma subred. La máquina virtual inicial utiliza dos puertos, tres puertos son direcciones IP virtuales utilizadas para los dominios, y las últimas dos son direcciones IP públicas para el DataPowers. A continuación, defina una segunda VLAN privada sólo entre los ESXi utilizados para {{site.data.keyword.Bluemix_notm}} Local. Esta VLAN se muestra como un grupo de puertos en VMware. {{site.data.keyword.Bluemix_notm}} local lo utiliza para la subred privada,
que es más segura y puede ayudar a evitar problemas de direccionamiento.<br />
<p>Se utilizarán los puertos siguientes:</p>
<ul>
<li>Puerto 443 para la conexión de relé
<p>**Nota**: Si elige utilizar un túnel IPSec en lugar de una OpenVPN, abra a continuación un puerto de cliente para esta conexión.</p></li>
<li>Puerto 389 o SSL 636 para la conexión LDAP o Active Directory</li>
</ul>
<p>**Nota**: IBM puede detectar si se ha perdido la conexión de red. En caso de que se pierda la conexión de red, IBM se pondrá en contacto con usted y trabajará con el especialista de red para resolver el problema.</p>
</dd>
<dt>**Enlaces de red**</dt>
<dd>Utilice dos o más interfaces de 1 a 10 Gbps, según la carga de trabajo esperada para el sistema.</dd>
</dl>

### Configuración de servidor de vCenter

Revise los siguientes requisitos relacionados con la versión, el centro de datos, la agrupación de recursos y el almacén de datos.

<dl>
<dt>**Versiones soportadas de VMware**</dt>
<dd>vCenter y ESXi 5.1, 5.5 y 6.0</dd>
<dt>**Tipos soportados de VMware**</dt>
<dd>vSphere Enterprise<br />
vSphere Enterprise más, si tiene pensado utilizar conmutadores virtuales distribuidos</dd>
<dt>**Centro de datos**</dt>
<dd>Cree un centro de datos (si no hay ninguno).</dd>
<dt>**Carpeta del centro de datos**</dt>
<dd>Cree una carpeta de la máquina virtual con el mismo nombre que el clúster si no tiene pensado otorgar un acceso de administrador
que se propague desde el centro de datos.</dd>
<dt>**Clúster**</dt>
<dd>Cree un clúster específicamente para {{site.data.keyword.Bluemix_notm}} local. Un ejemplo del nombre del clúster sería `bluemix`.</dd>
<dt>**Agrupación de recursos**</dt>
<dd>Cree una agrupación de recursos en el clúster de {{site.data.keyword.Bluemix_notm}} local. Un ejemplo del nombre de la agrupación de recursos sería `local`.</dd>
</dt>**Almacenes de datos**</dt>
<dd>Requiere 7,5 TB para el despliegue inicial de {{site.data.keyword.Bluemix_notm}}.<br />
<br />
**Nota**: Si utiliza más de un
almacén de datos, asegúrese de que todos ellos empiezan con el mismo prefijo. Un ejemplo de varios nombres de almacén de datos
con el mismo prefijo sería `almacén_datos_bluemix_01` y `almacén_datos_bluemix_02`.</dd>
<dt>**Red**</dt>
<dd>Debe tener una red accesible de cliente con capacidad de Internet de salida. La VLAN aloja la subred privada en la que se ejecutan
los componentes del Bluemix local. Todo el tráfico se direcciona desde la subred privada a la subred del cliente. Se utiliza una IP de subred
de cliente para todos los accesos al Bluemix local. A continuación, puede definir una segunda VLAN privada solo entre
el ESX que se utiliza para el Bluemix local. Esta VLAN se muestra como un grupo de puertos en VMware. El Bluemix local la utiliza
para la subred privada, que es más segura y puede ayudar a evitar problemas de direccionamiento.
<p>Si utiliza conmutadores distribuidos de vSphere (vDS), cree una carpeta para alogar los vDS, y colóquelos en la carpeta.</p>
</dl>

### Ancho de banda de red para Relay

El rendimiento recomendado es de 5 Mbps de subida y de 5 Mbps de bajada; puede esperar
un uso de datos mensual de 10 GB. IBM establece
ventanas acordadas cuando se entregan paquetes de datos grandes, que pueden tener un tamaño de 4 GB.

### Permisos de VMware

Establezca los siguientes roles y permisos. La propagación se establece
para cada permiso. Si el permiso se propaga, pasa por la jerarquía de objetos. Sin embargo, los permisos de un objeto hijo siempre sustituyen los permisos que se propagan desde un objeto padre.

<dl>
<dt>**Servidor vCenter**</dt>
<dd>Establezca el rol como de solo lectura y propagado.<br />
<br />
**Nota**: Este rol es necesario para recuperar estados de tareas de determinadas operaciones de disco.</dd>
<dt>**Centro de datos**</dt>
<dd>Crear el rol "{{site.data.keyword.Bluemix_notm}}" y otorgarle los permisos siguientes:
<ul>
<li>Para **Datastore**, establecer **Operaciones de archivo de bajo nivel** y **Actualizar archivos de máquina virtual**.</li>
<li>Para **vApp**, establecer **Importar**.</li>
<li>Para el grupo **dvPort**, establecer **Modificar**. Esto solo es para uso de vDS.</li>
</ul>
**Nota**: Este rol es necesario para poder dar soporte a las publicaciones de archivos en los almacenes de datos.</dd>
<dt>**Clúster**</dt>
<dd>Establezca el rol como administrador y propagado.</dd>
<dt>**Almacenes de datos**</dt>
<dd>Establezca el rol administrador y propagado para cada almacén de datos de {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>**Red**</dt>
<dd><ul>
<li>Para vSwitch, establecer grupos de puertos públicos y privados con el rol de administrador, no con el rol propagado.</li>
<li>Para la carpeta padre vDS, establecer como sólo lectura y propagado.</li>
<li>Para vDS, establecer grupos de puertos públicos y privados con el rol de administrador, no con el rol propagado.</li>
</ul>
</dd>
</dl>

### Aumento de la agrupación de agentes de ejecución de gotas (DEA)
Cada DEA está configurado con:
- 16 - 32 GB de RAM
- 2x - 4x vCPU
- 150 - 300 GB de almacenamiento

Por ejemplo, si el tamaño de host ESXi es de 256 GB de memoria con 16x núcleos, se añaden ocho DEA. Si el tamaño de host ESXi es de 64 GB de memoria con 8x núcleos, se deben añadir dos ESXi y cuatro DEA. Se necesita 1,5 TB más de almacenamiento para cada cuatro DEA. Este ejemplo se basa en un DEA configurado con 32 GB de RAM, 4x vCPU y 300 GB de almacenamiento.

## Mantenimiento de la instancia local
{: #maintainlocal}

IBM mantiene e instala actualizaciones y arreglos en los tiempos de ejecución y servicios de {{site.data.keyword.Bluemix_notm}}, como IBM considere adecuado. Es posible que los servicios no estén disponibles durante las ventanas de mantenimiento. Además, IBM trabaja con usted para planificar actualizaciones de mantenimiento para la plataforma {{site.data.keyword.Bluemix_notm}}.

Se requieren los siguientes tipos de mantenimiento para {{site.data.keyword.Bluemix_notm}} local:
<dl>
<dt>**Mantenimiento estándar para servicios**</dt>
<dd>Los servicios utilizan ventanas de mantenimiento estándar y predefinidas, lo cual podría hacer que los servicios no estén disponibles. IBM no requiere aprobación del cliente para realizar el mantenimiento de servicios, aunque intenta minimizar el impacto en los servicios.<br />
<br />
IBM envía mensajes de difusión general detallando los cambios planificados para cada ventana de mantenimiento en la página Estado. <br />
<br />
**Importante**: algunos servicios pueden no estar disponible durante el periodo de mantenimiento.</dd>

<dt>**Mantenimiento estándar para la plataforma de  {{site.data.keyword.Bluemix_notm}}**</dt>
<dd>Las actualizaciones de mantenimiento se aplican en función de la coordinación entre el usuario y IBM dentro de una ventana de 21 días. Proporcione a IBM ventanas de mantenimiento y fechas u horas específicas aprobadas previamente que pueden no funcionar para usted, e IBM trabaja para planificar actualizaciones durante o alrededor de las fechas seleccionadas. <br />
<p>Vaya a **ADMINISTRACIÓN > INFORMACIÓN DEL SISTEMA** para ver las actualizaciones de mantenimiento planificadas y pendientes. Para obtener más información sobre cómo establecer las ventanas preaprobadas, las fechas no disponibles y visualizar o aprobar actualizaciones de mantenimiento, consulte <a href="../admin/index.html#oc_schedulemaintenance">Actualizaciones de mantenimiento</a></p>.</dd>
</dl>

**Importante**: IBM se reserva el derecho de interrumpir servicios para aplicar mantenimiento emergencia si es necesario. IBM puede modificar las horas de mantenimiento planificadas, pero le notificará de cualquier cambio, así como la información de mantenimiento de emergencia.

Si hay un problema después de una actualización de mantenimiento, acuerda con el soporte de {{site.data.keyword.Bluemix_notm}} si le conviene permitir que IBM retrotraiga la actualización. Si se acuerda, IBM retrotrae la actualización para restaurar el entorno al estado anterior.

## Respuesta y soporte de incidencias
{: #incidentresponse}

### Problemas detectados por el cliente

Si detecta un problema que necesite la atención de operaciones y soporte de IBM puede ponerse en contacto con el soporte mediante diversos
métodos. Para obtener información sobre cómo contactar con el soporte, consulte [Cómo obtener soporte](../support/index.html#contacting-bluemix-support-local). Según la naturaleza del problema, el usuario, IBM o ambos pueden trabajar para solucionarlo.

### Incidencias críticas detectadas por IBM

Las incidencias críticas son urgentes, cortes de servicio inesperados y problemas de estabilidad que afectan a su
entorno o sus usuarios. Si IBM detecta una incidencia crítica en su entorno, se le envía una notificación en la página
**Estado**. También se puede revisar la página Estado para buscar problemas conocidos para la plataforma o
sus servicios. Para obtener más información sobre la página Estado, consulte [Visualización de estado](../admin/index.html#oc_status). 

Si quiere integrar sus notificaciones con un servicio web que admita ganchos (hooks), consulte
[Notificaciones y suscripciones de sucesos](../admin/index.html#oc_eventsubscription) para obtener información sobre
cómo ampliar las funciones de notificación.

![Proceso de respuesta de incidencias](images/incidentresponseprocess.png "Proceso de respuesta de incidencias")

*Figura 2. Proceso de respuesta de incidencias*

Según la naturaleza del problema, el usuario, IBM o ambos pueden trabajar para solucionarlo. Si tiene alguna pregunta relativa a la incidencia, o si necesita que un representante de IBM le ayude a resolver el problema, puede abrir una incidencia de soporte. Para obtener información sobre cómo contactar con el soporte, consulte [Cómo obtener soporte](../support/index.html#contacting-bluemix-support-local).

**Nota**: Las incidencias de soporte de gravedad 1 se supervisan 24 horas al día, 7 días por semana. Otras incidencias
se procesan desde las 22:00 del domingo (GMT) hasta las 00:00 del sábado (GMT). Para obtener más información sobre la gravedad de
las incidencias de soporte y cómo trabajar con soporte, consulte <a href="../support/index.html#contacting-bluemix-support-local">Contacto
con soporte</a>.

## Recuperación en caso de siniestro
{: #dr}

La recuperación tras desastre para {{site.data.keyword.Bluemix_short}} local puede configurarse de forma parecida a la forma en que funciona cuando utiliza
{{site.data.keyword.Bluemix_short}} público. {{site.data.keyword.Bluemix_short}} público proporciona una plataforma disponible de forma continua para la innovación con varias medidas libre de errores para garantizar que las organizaciones, los espacios y las apps estén siempre disponibles. El despliegue de apps en varias regiones geográficas permite la disponibilidad continua, que protege frente a la pérdida no planificada y simultánea de varios componentes de hardware o software, o la pérdida de todo un centro de datos, de modo que, incluso en el caso de un desastre natural en una ubicación geográfica, las instancias distribuidas de la app de {{site.data.keyword.Bluemix_notm}} público, situadas en ubicaciones geográficas alternativas, seguirán estando disponibles.
{: shortdesc}

La recuperación en caso de error de {{site.data.keyword.Bluemix_short}} local es posible gracias a la disponibilidad continua de sus apps, la alta disponibilidad inherente de la plataforma y la capacidad de restaurar la instancia en caso de error. Es responsable de habilitar una disponibilidad continua de sus apps desplegándolas en varias regiones. La alta disponibilidad está integrada en el nivel de la plataforma mediante tecnologías incluidas en Cloud Foundry y otros componentes. También puede trabajar conjuntamente con IBM para asegurarse de que se ha hecho una copia de seguridad correcta de sus datos en el caso de que necesite restaurar su instancia en cualquier momento.

### Habilitación de la disponibilidad continua para {{site.data.keyword.Bluemix_notm}} local
{: #enabling}

De forma predeterminada, {{site.data.keyword.Bluemix_notm}} público se despliega en varias ubicaciones geográficas. Sin embargo, debe llevar a cabo lo siguiente para habilitar las instancias de {{site.data.keyword.Bluemix_notm}} local distribuidas globalmente:

* Asegúrese de que los desarrolladores están desplegando apps en más de una región, ya sea a través de un proceso manual o automatizado. Las regiones seleccionadas deben estar a una distancia de más de 200 km entre ellas para garantizar que, en caso de desastre natural, ambas ubicaciones geográficas no se vean afectadas.
* Configure un equilibrador de carga global, como Akamai o Dyn, para que apunten a apps en al menos dos regiones distintas.

**Nota**: No todos los servicios de {{site.data.keyword.Bluemix_notm}} admiten la distribución regional. Al construir una app, si desea lograr la distribución geográfica, también debe asegurarse de que los servicios que se utilizan en la app tienen la sincronización de datos como característica clave.

#### Despliegue de apps de {{site.data.keyword.Bluemix_notm}} local en varias ubicaciones geográficas
{: #deploying}

Para efectuar un despliegue en una segunda ubicación o en varias ubicaciones, debe seguir un proceso similar al que siguió para habilitar la ubicación geográfica primaria:

1. Habilite un nuevo entorno local para alojar instancias adicionales de las apps. Para crear un nuevo entorno, póngase en contacto con el equipo de ventas de IBM para iniciar el proceso. Para obtener más información sobre la configuración de una instancia local, consulte [Configuración de {{site.data.keyword.Bluemix_notm}} local](../local/index.html#setuplocal). Debe iniciar sesión por separado para acceder a cada entorno. Cada ubicación física de los entornos alojados debe estar a una distancia mínima de 200 km de la ubicación original para garantizar la disponibilidad.
2. Obtenga el nombre de dominio exclusivo en el que se alojará la nueva app desplegada. Por ejemplo, si el dominio original es *mycompany.east.bluemix.net*, puede crear un nuevo entorno local con un nuevo dominio como *mycompany.west.bluemix.net* y desplegarlo en el nuevo dominio.
3. Efectúe un despliegue en la nueva ubicación cada vez que despliegue la app original. Para obtener más información sobre el despliegue, consulte [Carga de una app](../starters/upload_app.html).


#### Habilitación de un equilibrador de carga global para {{site.data.keyword.Bluemix_notm}} local
{: #glb}

Un equilibrador de carga global no solo garantiza una disponibilidad continua y es necesario para la recuperación en caso de error, sino que también presenta varias ventajas adicionales:

* Dirige a los usuarios a la región más próxima de {{site.data.keyword.Bluemix_notm}} de forma predeterminada
* Efectúa un enrutamiento en función del rendimiento
* Dirige de forma selectiva un porcentaje de tráfico a una nueva versión de una app
* Proporciona migración tras error de sitio en función de la comprobación del estado de la región
* Proporciona migración tras error de sitio en función de la comprobación del estado de la app
* Utiliza un direccionamiento ponderado entre los puntos finales

Puede elegir un equilibrador de carga global como Akamai o Dyn. Para obtener más información sobre cómo utilizar Akamai como equilibrador de carga global, consulte [Gestión de tráfico global](https://www.akamai.com/us/en/solutions/products/web-performance/global-traffic-management.jsp){: new_window}. Para obtener más información sobre cómo utilizar Dyn como equilibrador de carga global, consulte [4 Reasons Businesses Are Taking Global Load Balancing to the Cloud](http://dyn.com/blog/4-reasons-businesses-are-taking-global-load-balancing-to-the-cloud/){: new_window}.

### Alta disponibilidad
{: #ha}

Además de habilitar una disponibilidad continua, {{site.data.keyword.Bluemix_notm}} también proporciona alta disponibilidad en la plataforma mediante tecnologías integradas en Cloud Foundry y otros componentes.

Estas tecnologías incluyen:

<dl>
<dt>Escalabilidad de DEA en Cloud Foundry</dt>
<dd>Un <a href="https://docs.cloudfoundry.org/concepts/architecture/execution-agent.html" target="_blank">agente de ejecución de gotas (DEA)</a> de Cloud Foundry efectúa comprobaciones de estado en las apps que se ejecutan en él. Si se produce algún problema con la app o con el propio DEA, despliega instancias adicionales de la app en un DEA alternativo para solucionar el problema. Para obtener más información, consulte <a href="https://docs.cloudfoundry.org/concepts/high-availability.html" target="_blank">Configuración de CF para la alta disponibilidad con redundancia</a>.<br />
<p>Para asegurar la alta disponibilidad de las aplicaciones, serán necesarios suficientes recursos de cálculo para equilibrar la carga y también pueden ser necesarios recursos de cálculo adicionales para dar soporte a una posible anomalía. Si es necesario escalar el entorno aumentando la agrupación de DEA para que esté preparada para una anomalía o abordar un pico en la carga para las instancias de la app, puede trabajar con el representante de IBM para solicitar DEA adicionales y asegurarse de que tiene el hardware apropiado para dar soporte a los recursos añadidos.
</p>
</dd>
<dt>Copia de seguridad de metadatos</dt>
<dd>Se realiza una copia de seguridad de los metadatos en una ubicación secundaria, normalmente en una máquina virtual local. Si es posible, debe replicar la copia de seguridad a su propio entorno a una distancia mínima de 200 km.</dd>
</dl>

## Restauración de la instancia local
{: #restorelocal}

Se hace una copia de seguridad de forma regular de los valores, los metadatos y las configuraciones de {{site.data.keyword.Bluemix_notm}} local para prepararse ante cualquier interrupción no planificada del entorno. Los datos de cuya copia de seguridad es responsable incluyen datos de app, datos de servicios de bases de datos en la nube y almacenes de objetos.

Como parte de la copia de seguridad de los datos, que incluye metadatos del sistema y configuraciones, IBM lleva a cabo las tareas siguientes:

<ul>
<li>Cifra todas las copias de seguridad y gestiona las claves de cifrado</li>
<li>Supervisa y gestiona la actividad de copia de seguridad</li>
<li>Proporciona los archivos de copia de seguridad cifrados</li>
<li>Restaura los datos solicitados</li>
<li>Gestiona conflictos de planificación entre operaciones de copia de seguridad y de gestión de arreglos</li>
</ul>

Puesto que la protección de datos privados es crítica, IBM necesita su colaboración cuando se trabaja con la gestión de archivos de copia de seguridad, de modo que los archivos no se traspasen fuera de sus centros de datos. Específicamente, IBM le solicita que complete las tareas siguientes:

<ul>
<li>Mover una copia de los datos de copia de seguridad cifrados fuera del sitio, como lo haría para cualesquiera otros datos de copia de seguridad que gestione.</li>
<li>Proporcionar los archivos de copia de seguridad para el operador de IBM en caso de cualquier necesidad de restauración.</li>
</ul>


# rellinks
## general
* [Descubrir: {{site.data.keyword.Bluemix_notm}} Local](http://www.ibm.com/cloud-computing/bluemix/hybrid/local/)
* [Novedades de {{site.data.keyword.Bluemix_notm}}](../whatsnew/index.html)
* [Glosario de {{site.data.keyword.Bluemix_notm}}](../overview/glossary/index.html)
* [Gestión de {{site.data.keyword.Bluemix_notm}} local y {{site.data.keyword.Bluemix_notm}} dedicado](../admin/index.html#mng)
* [Cómo obtener soporte](../support/index.html#getting-customer-support)
