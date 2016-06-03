---

copyright:
  years: 2015, 2016

---


{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


#Servicios
{: #services}
*Última actualización: 20 de enero de 2016*

Puede encontrar servicios disponibles en el **Catálogo** en **Servicios** en la interfaz de usuario de {{site.data.keyword.Bluemix}}.
{:shortdesc}


Los servicios predefinidos están disponibles en {{site.data.keyword.Bluemix_notm}} para app móviles. {{site.data.keyword.Bluemix_notm}} le permite fácilmente implementar, alojar y escalar estos servicios móviles para sus apps móviles. Puede centrarse en la lógica de la aplicación y en el diseño de la aplicación.

{{site.data.keyword.Bluemix_notm}} aloja y gestiona servicios de middleware para app web. Los desarrolladores de aplicaciones pueden especificar los servicios de middleware que precisan. {{site.data.keyword.Bluemix_notm}} suministra automáticamente nuevas instancias de los servicios middleware especificados y enlaza las instancias de servicio a la aplicación.

{{site.data.keyword.Bluemix_notm}} muestra los servicios de dos formas: por categoría de servicio y por tipo de soporte de servicio.



<dl>
<dt><strong>Categoría</strong></dt>
<dd>Los servicios de {{site.data.keyword.Bluemix_notm}} están organizados en distintas categorías. En cada categoría de servicio, primero se muestran los servicios creados por IBM, seguidos de los servicios de terceros y, finalmente, los servicios de la comunidad.</dd>
<dt><strong>Soporte</strong></dt>
<dd>Se proporcionan varios niveles de soporte para los servicios de {{site.data.keyword.Bluemix_notm}}. En la tabla siguiente se describe la información de soporte general para los servicios de {{site.data.keyword.Bluemix_notm}}:

</dd>
</dl>



|Tipo	|Descripción	|Detalles de soporte|
|:------|:--------------|:--------------|
|IBM	|Un servicio proporcionado por IBM y disponible generalmente.	|Se da soporte a los problemas que se determinen que son un defecto de un servicio proporcionado por IBM disponible generalmente. Se proporciona soporte en función de la gravedad que establezca. Para obtener más información sobre la gravedad de las incidencias, consulte [Cómo obtener soporte](../support/index.html#contacting-bluemix-support){: new_window}.|
|Otro proveedor	|Un servicio que está proporcionado por una empresa que no es IBM.	|El soporte para servicios de terceros está proporcionado por un proveedor de servicios. Si IBM investiga un problema y se determina que el problema es un defecto de un servicio de terceros, IBM no está obligado a proporcionar un arreglo. IBM compartirá análisis con el proveedor de servicios de terceros si es necesario.|
|Comunidad	|Un servicio que está proporcionado por una comunidad de código abierto.	|El soporte para servicios de la comunidad se proporciona a través de la Comunidad de desarrolladores de {{site.data.keyword.Bluemix_notm}}. Si IBM investiga un problema y se determina que el problema es un defecto de un servicio de comunidad, IBM no está obligado a proporcionar un arreglo.|
|Beta	|Servicio que no está listo para producción que está en una etapa de prueba de desarrollo. Un servicio beta puede ayudar a los equipos de desarrollo y marketing a evaluar el valor de los servicios antes de que el servició esté generalmente disponible.	|Se da soporte a los problemas que se determinen que son un defecto de un servicio beta proporcionado por IBM, aunque IBM no está obligado a proporcionar un arreglo. Además, se asignará una incidencia de problema con una gravedad de 3 o 4 cuando proceda. Para obtener información sobre la gravedad de las incidencias, consulte [Cómo obtener soporte](../support/index.html#contacting-bluemix-support){: new_window}.|
*Tabla 1. Información de soporte de los servicios de {{site.data.keyword.Bluemix_notm}}*




{{site.data.keyword.Bluemix_notm}} también dispone de servicios experimentales que puede probar. Para ver todos los servicios experimentales, contenedores modelo y tiempos de ejecución disponibles, inicie una sesión en {{site.data.keyword.Bluemix_notm}}, desplácese hasta el final del Catálogo y pulse **{{site.data.keyword.Bluemix_notm}}Catálogo de Lab**.

Los servicios experimentales pueden no ser estables y es posible que cambien de modo que no sean compatibles con versiones anteriores. No se recomienda utilizar estos servicios en entornos de producción. El soporte para servicios experimentales se proporciona a través de la Comunidad de desarrolladores de {{site.data.keyword.Bluemix_notm}}. Si IBM investiga un problema y se determina que el problema es un defecto de servicio experimental, IBM no está obligado a proporcionar un arreglo.

Para utilizar un servicio en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, en la interfaz de línea de mandatos cf, en IBM {{site.data.keyword.Bluemix_notm}} DevOps Services o en cualquier herramienta soportada, realice los pasos siguientes:

1. Cree una instancia del servicio. En la mayoría de los casos, la instancia de servicio se puede crear al crear la aplicación.

2. Identifique la aplicación que utiliza la nueva instancia de servicio. En el caso de app web, puede especificar más de una aplicación para utilizar la misma instancia de servicio, normalmente para uso compartido de datos.

3. Escriba su propio código en la aplicación para interactuar con el servicio.

##Servicios por región

No todos los servicios están disponibles en cada región de {{site.data.keyword.Bluemix_notm}}. La siguiente tabla muestra los servicios proporcionados por IBM.



|Servicio	|Disponible en la región EE.UU. sur	|Disponible en la región Europa Reino Unido |Disponible en la región Australiana Sídney|
|:----------|:------------------------------|:------------------|:------------------|
|{{site.data.keyword.activedeployshort}}	|Sí		|Sí		|No|
|{{site.data.keyword.alchemyapishort}} 		|Sí	   	|Sí  		|Sí|
|{{site.data.keyword.appsecshort}}		|Sí		|No		|No|
|{{site.data.keyword.alertnotificationshort}}|Sí		|No			|No		|
|{{site.data.keyword.APS_DA}}			|Sí		|No		|No|
|{{site.data.keyword.APS_MA}}			|Sí		|No		|No|
|{{site.data.keyword.amashort}}			|Sí		|Sí		|Sí|
|{{site.data.keyword.hadoopst}}			|Sí		|No		|No|
|{{site.data.keyword.APIM}}			|Sí		|Sí		|No|
|{{site.data.keyword.autoscaling}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.bigicloudst}}		|Sí		|No		|No|
|{{site.data.keyword.rules_short}}		|Sí		|Sí		|No|
|{{site.data.keyword.cloudint}}			|Sí		|Sí		|No|
|{{site.data.keyword.cloudant}}			|Sí		|Sí		|No|
|{{site.data.keyword.conceptexpansionshort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.conceptinsightsshort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.dashdbshort}}		|Sí		|Sí		|No|
|{{site.data.keyword.datacshort}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.DB2OnCloud_short}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.deliverypipeline}}		|Sí		|Sí		|No|
|{{site.data.keyword.dialogshort}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.documentconversionshort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.creshort}}			|Sí		|No		|No|
|{{site.data.keyword.game}}			|Sí		|Sí		|Sí|
|{{site.data.keyword.geospatialshort_Geospatial}}	|Sí	|Sí		|No|
|{{site.data.keyword.globalizationshort}}	|Sí		|No		|No|
|{{site.data.keyword.dataworks_short}}		|Sí		|Sí		|No|
|{{site.data.keyword.twittershort}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.weather_short}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.IntegrationTestingshort}}	|Sí		|Sí		|No|
|{{site.data.keyword.iot_short}}		|Sí		|No		|No|
|{{site.data.keyword.keymanagementserviceshort}}|No		|Sí		|No|
|{{site.data.keyword.languagetranslationshort}}	|Sí		|Sí		|No|
|{{site.data.keyword.messagehub}}		|Sí		|Sí		|No|
|{{site.data.keyword.messageresonanceshort}}	|Sí		|Sí		|No|
|{{site.data.keyword.APS_MAiOS}} 		|Sí		|No		|No|
|{{site.data.keyword.macm_short}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.mobilemam}}		|Sí		|Sí		|No|
|{{site.data.keyword.mobiledata}}		|Sí		|Sí		|No|
|{{site.data.keyword.manda}}			|Sí		|Sí		|No|
|{{site.data.keyword.mqa}}			|Sí		|Sí		|No|
|{{site.data.keyword.mql}}			|Sí		|Sí		|No|
|{{site.data.keyword.nlclassifierlshort}} 	|Sí 		|Sí 		|Sí|
|{{site.data.keyword.objectstorageshort}}	|Sí		|No		|No|
|{{site.data.keyword.personalityinsightsshort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.mobilepush}}Push		|Sí		|Sí		|No|
|Push para iOS 8					|Sí		|Sí		|No|
|{{site.data.keyword.questionandanswershort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.rapidApps}}		|Sí		|Sí		|No|
|{{site.data.keyword.relationshipextractionshort}}	|Sí	|Sí		|Sí|
|{{site.data.keyword.retrieveandrankshort}}	|Sí 		|Sí 		|Sí|
|{{site.data.keyword.SecureGateway}}		|Sí		|Sí		|No|
|{{site.data.keyword.servicediscoveryshort}}	|Sí		|No		|No|
|{{site.data.keyword.sescashort}}		|Sí		|Sí		|Sí|
|{{site.data.keyword.ssofull}}			|Sí		|No		|No|
|{{site.data.keyword.speechtotextshort}}	|Sí 		|Sí	 	|Sí|
|{{site.data.keyword.sqldb}}			|Sí		|Sí		|No|
|{{site.data.keyword.staticanalyzershort}}	|Sí		|Sí		|No|
|{{site.data.keyword.streaminganalyticsshort}}	|Sí		|No		|No|
|{{site.data.keyword.texttospeechshort}} 	|Sí 		|Sí	 	|Sí|
|{{site.data.keyword.times}}			|Sí		|Sí		|No|
|{{site.data.keyword.toneanalyzershort}} 	|Sí 		|Sí 		|Sí|
|{{site.data.keyword.trackplan}}		|Sí		|Sí		|No|
|{{site.data.keyword.tradeoffanalyticsshort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.visualinsightsshort}}	|Sí		|Sí		|Sí|
|{{site.data.keyword.visualizationrenderingshort}} |Sí		|Sí		|No|
|{{site.data.keyword.workflow}}			|Sí		|Sí		|No|
|{{site.data.keyword.workloadscheduler}}	|Sí		|Sí		|No|
|{{site.data.keyword.xpagesservice_short}}	|Sí		|Sí		|No|
*Tabla 2. Disponibilidad del servicio*


# Cómo añadir un servicio a la aplicación
{: #add_service}
*Última actualización: 8 de marzo de 2016*

{{site.data.keyword.Bluemix}} tiene una lista de servicios y los gestiona en nombre de los desarrolladores. Para añadir un servicio a la aplicación para utilizar, debe solicitar una instancia de dicho servicio y configurar la aplicación para que actúe con el servicio.

Puede ver todos los servicios disponibles en {{site.data.keyword.Bluemix_notm}} de las maneras siguientes:

* Desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. Consulte el Catálogo de {{site.data.keyword.Bluemix_notm}}.
* Desde la interfaz de línea de mandatos cf. Utilice el mandato **cf marketplace**.
* Desde la propia aplicación. Utilice la [GET /v2/services Services API](http://apidocs.cloudfoundry.org/197/services/list_all_services.html){: new_window}.

Puede seleccionar el servicio que necesita cuando desarrolla app. En la selección,
{{site.data.keyword.Bluemix_notm}} plan del servicio interactúa con el servicio y realiza los pasos necesarios para suministrar los recursos al servicio. El proceso de suministro puede ser diferente para distintos tipos de servicios. Por ejemplo, un servicio de base de datos crea una base de datos y un servicio de notificación push para app móviles genera información de configuración.

{{site.data.keyword.Bluemix_notm}} proporciona los recursos de un servicio a su aplicación mediante una instancia de servicio. Una instancia de servicio se puede compartir entre app web.

También puede utilizar servicios que estén alojados en otras regiones si estos servicios están disponibles en dichas regiones. Estos servicios deben estar accesibles en Internet y tener puntos finales API. Debe codificar manualmente la aplicación para que utilice estos servicios de la misma forma que codifica app externas o herramientas de terceros para que utilicen servicios {{site.data.keyword.Bluemix_notm}}. Para obtener más información, consulte [Habilitación de app externas y de herramientas de terceros para utilizar servicios {{site.data.keyword.Bluemix_notm}}](#accser_external).



## Solicitud de una nueva instancia de servicio
{: #req_instance}

Para solicitar una nueva instancia de servicio, debe utilizar la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} o la interfaz de la línea de mandatos
cf.

**Nota:** Cuando especifique el nombre de servicio, no utilice caracteres que no sean alfabéticos o caracteres numéricos, puesto que los resultados podrían ser erróneos.

Si utiliza la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} para solicitar una instancia de servicio, siga los siguientes pasos:

1. En el **Catálogo** de {{site.data.keyword.Bluemix_notm}}, pulse el mosaico correspondiente al servicio que desea añadir. Se abre la página de detalles del servicio.

2. En el panel Añadir servicio, seleccione una aplicación a la que desee enlazar esta instancia de servicio de la lista de la **App**.

3. Especifique un nombre en el campo **Nombre de servicio**. Se proporciona un nombre de servicio predeterminado. Puede modificar el nombre en el campo o dejarlo tal cual.

4. Rellene los otros campos o selecciones y, a continuación, pulse **CREAR**.

Si utiliza la interfaz de línea de mandatos cf para solicitar una instancia de servicio, siga los siguientes pasos:

1. Utilice el mandato **cf marketplace** para encontrar el nombre y el plan del servicio que necesita.

2. Utilice el mandato siguiente para crear una instancia de servicio, done nombre_servicio es el nombre del servicio, plan_servicio es el plan del servicio e
instancia_servicio es el nombre que desea utilizar para esta instancia de servicio.

    ```
    cf create-service nombre_servicio plan_servicio instancia_servicio
    ```

3. Utilice el siguiente mandato para enlazar una instancia de servicio a una aplicación, donde nombre_app es el nombre de la aplicación e instancia_servicio es el nombre de la instancia de servicio.

    ```
    cf bind-service nombre_app instancia_servicio
    ```

Se pueden enlazar una instancia de servicio únicamente a aquellas instancias de aplicaciones que se encuentran en el mismo espacio u organización. No obstante, puede utilizar instancias de servicio de otros espacios y organizaciones de la misma forma que lo hace una app externa. En lugar de crear
un enlace, utilice las credenciales para configurar directamente su instancia de app. Para obtener más información sobre cómo utilizan las apps externas
los servicios de {{site.data.keyword.Bluemix_notm}}, consulte [Habilitación de apps externas para
usar servicios de {{site.data.keyword.Bluemix_notm}} ](#accser_external){: new_window}.


## Configuración de la aplicación para interactuar con un servicio 
{: #config}

Después de enlazar una instancia de servicio a una aplicación, debe configurar la aplicación para que interactúe con el servicio.

Cada servicio puede requerir un mecanismo diferente para comunicarse con las app. Estos mecanismos están documentados como parte de la definición de servicio con fines informativos cuando desarrolle app. Para una mayor coherencia, los mecanismos son necesarios para que la aplicación interactúe con el servicio.

* Para interactuar con servicios de base de datos, utilice la información que {{site.data.keyword.Bluemix_notm}} proporciona como, por ejemplo, el ID de usuario, la contraseña y el URI de acceso para la aplicación.
* Para interactuar con los servicios de dispositivos móviles de fondo, utilice la información que {{site.data.keyword.Bluemix_notm}} proporciona como la identidad de la aplicación (ID de app), la información de seguridad que es específica del cliente y el URI de acceso para la aplicación. Los servicios móviles suelen funcionar compartiendo el contexto entre sí, de forma que la información contextual como, por ejemplo, el nombre del desarrollador de la aplicación y el usuario que utilizan la aplicación, se pueden compartir entre el conjunto de servicios.
* Para interactuar con app web o código en la nube del servidor para app móviles, utilice la información que {{site.data.keyword.Bluemix_notm}} proporciona como las credenciales de tiempo de ejecución de la variable de entorno *VCAP_SERVICES* de la aplicación. El valor de la variable de entorno *VCAP_SERVICES* es la serialización del objeto JSON. La variable contiene los datos de tiempo de que son necesarios para interactuar con los servicios a los que la aplicación se enlaza. El formato de los datos es diferente para diferentes servicios. Es posible que necesite leer la documentación del servicio para saber lo que puede esperar y cómo interpretar cada información.

Si se bloquea un servicio enlazado con una aplicación, ésta podría dejar de funcionar o tener errores. {{site.data.keyword.Bluemix_notm}} no reinicia automáticamente la aplicación para solucionar los problemas. Escriba código en la aplicación para identificar y recuperarse de caídas, excepciones y fallos de conexión. Para obtener más información, consulte el tema de resolución de problemas [Las apps no se reiniciarán automáticamente](../troubleshoot/index.html#ts_topmenubar).

## Habilitación de apps externas para utilizar servicios de {{site.data.keyword.Bluemix_notm}}
{: #accser_external}

Es posible que tenga app que se crearon y ejecutaron fuera de {{site.data.keyword.Bluemix_notm}},
o puede que utilice herramientas de terceros. Si los servicios de {{site.data.keyword.Bluemix_notm}} proporcionan puntos finales que están accesibles en Internet, puede utilizarlos con las apps locales o herramientas de terceros.

Para habilitar una app externa o una herramienta de terceros para que utilice un servicio {{site.data.keyword.Bluemix_notm}}, siga estos pasos:

1. Solicite una instancia del servicio.
    1. En el Panel de control de la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, pulse **Utilizar servicios o API**. Se visualiza el Catálogo.
    2. En el Catálogo, seleccione el servicio que desee pulsando el título del servicio. Se abre la página de detalles del servicio.
    3. En la ventana Añadir servicio, mantenga la selección de la lista **App**: como **Dejar sin enlazar**. Esta selección significa que el servicio no se conectará a una app de {{site.data.keyword.Bluemix_notm}}.
    4. Realice las selecciones que necesite. A continuación, pulse **CREAR**. Se creará una instancia de servicio y se mostrará el Panel de control del servicio.
2. En el panel de navegación izquierdo del Panel de control del servicio, puede seleccionar **Credenciales de servicio** para visualizar o añadir credenciales en formato JSON. Utilice la clave API que se muestra como credenciales para conectarse a la instancia del servicio.

La aplicación que se ejecuta fuera de {{site.data.keyword.Bluemix_notm}} ahora puede acceder al servicio de {{site.data.keyword.Bluemix_notm}}.

**Nota:** Si desea suprimir instancias de servicio o comprobar la información de facturación, debe volver al Panel de control de la interfaz de usuario para gestionar las instancias de servicio.

## Creación de una instancia del servicio proporcionada por el usuario
{: #user_provide_services}

Es posible que tenga recursos gestionados fuera de {{site.data.keyword.Bluemix_notm}}. Si tiene credenciales para acceder a estos recursos externos desde Internet, puede crear instancias de servicio proporcionadas por el usuario de {{site.data.keyword.Bluemix_notm}} para representar y comunicarse con los recursos externos.

Para crear una instancia de servicio proporcionada por el usuario y enlazarla a una aplicación, siga los pasos siguientes:

1. Cree una instancia de servicio proporcionada por el usuario mediante el mandato **cf create-user-provided-service** o el mandato **cf
cups** :
    * Para crear una instancia de servicio general proporcionada por el usuario, utilice la opción **-p** y separe los nombres de los parámetros por comas. La interfaz de línea de mandatos cf le solicitará de uno en uno cada parámetro. Por ejemplo:
        ```
        cf cups testups1 -p "host, port, dbname, username, password"
        host> pubsub01.example.com
        port> 1234
        dbname> sampledb01
        username> pubsubuser
        password> p@$$w0rd
        Creating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * Para crear una instancia de servicio que proporcione información a software de gestión de registros de un otro proveedor, utilice la opción **-l** y especifique el destino que proporciona el software de gestión de registro del otro proveedor. Por ejemplo:

        ```
        cf cups testups2 -l syslog://example.com
        Creating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

    Si desea actualizar uno o varios parámetros de la instancia de servicio proporcionada por el usuario, utilice el mandato **cf update-user-provided-service** o el mandato
**cf uups**.

    * Para actualizar una instancia de servicio general proporcionada por el usuario, utilice la opción **-p** y especifique las claves y valores de parámetros en un objeto json. Por ejemplo:

        ```
        cf uups testups1 -p "{\"username\":\"pubsubuser2\",\"password\":\"p@$$w0rd2\"}"
        Updating user provided service testups1 in org my-org / space dev as user@sample.com...
        OK
        ```

    * Para crear una instancia de servicio que proporcione información a software de gestión de registros de un otro proveedor, utilice la opción -l. Por ejemplo:

        ```
        cf uups testups2 -l syslog://example2.com
        Updating user provided service testups2 in org my-org / space dev as user@sample.com...
        OK
        ```

2. Enlace la instancia de servicio a la aplicación con el mandato cf bind-service. Por ejemplo:

	```
	cf bind-service myapp testups1
	Binding service testups1 to app myapp in org my-org / space dev as user@sample.com...
	OK
	```

Ahora puede configurar la aplicación para que utilice recursos externos. Para obtener información sobre cómo configurar la aplicación para que interactúe con un servicio, consulte [Configuración de la aplicación para que interactúe con un servicio](#config){: new_window}.

## Utilización de servicios en otra región
{: #cross_region_service}

Si tiene una instancia de servicio creada y enlazada a apps en una región, puede utilizar eta instancia de servicio en otra región mediante uno de los métodos siguientes:

  * Utilice las credenciales del servicio para configurar directamente su instancia de app. Para obtener detalles, consulte
[Habilitación de apps externas para usar el servicio de {{site.data.keyword.Bluemix_notm}}
](#accser_external){: new_window}.
  * Crear un servicio proporcionado por el usuario como un puente.
    
	Supongamos que va a iniciar la región en la que desea utilizar la instancia de servicio. Para utilizar una instancia de servicio existente en otra región, siga estos pasos:

      1. Vaya a la región en la que reside la instancia de servicio. En la barra de menús superior de {{site.data.keyword.Bluemix_notm}}, expanda **Región** o pulse el icono **Región** y seleccione la región en la que reside la instancia de servicio.

      2. Recupere las credenciales y los parámetros de conexión de la variable de entorno VCAP_SERVICES de la instancia de servicio de la región en la que existe el servicio. Siga estos pasos:

	       1. En el Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el icono de la aplicación. Se muestra la página Visión general.
	       2. En el panel de navegación izquierdo, pulse **Variables de entorno**. Se muestran los detalles de la variable de entorno *VCAP_SERVICES* en el panel derecho. Registre el contenido JSON correspondiente a la instancia de servicio.

      3. Vaya a la región en la que desea utilizar la instancia de servicio. En la barra de menús superior de {{site.data.keyword.Bluemix_notm}}, expanda **Región** o pulse el icono **Región** y seleccione la región en la que desea utilizar la instancia de servicio.

      4. Cree una instancia de servicio suministrada por el usuario utilizando las credenciales y los parámetros de conexión que ha registrado de la variable de entorno *VCAP_SERVICES*. Para obtener información sobre cómo crear una instancia de servicio proporcionada por el usuario, consulte el tema sobre [creación de una instancia de servicio proporcionada por el usuario](#user_provide_services){: new_window}.

      5. Enlace la instancia de servicio proporcionada por el usuario a la app con el siguiente mandato:

	     ```
	     cf bind-service myapp user-provided_service_instance
	     ```






## Utilización de servicios en otro servicio
{: #s2s_binding}

La autorización de acceso a servicio proporciona una forma para que un servicio acceda a otro servicio
directamente. Puede autorizar y configurar un acceso de instancia de servicio a otras instancias de servicio en
el Panel de control de {{site.data.keyword.Bluemix_notm}}.

Para utilizar una instancia de servicio de otro servicio, siga estos pasos:

1. En el Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse
el mosaico para el servicio al que desee acceder. Se mostrará el panel de control para el servicio.
2. En el panel de navegación de la izquierda, pulse *Gestionar* para autorizar el enlace desde otras instancias de servicio utilizando la consola de la instancia de servicio.
3. Si desea denegar a otros servicios el acceso a la instancia de servicio, pulse *Autorización de acceso de servicio* en el panel de navegación izquierdo y, a continuación, utilice *Revocar* para eliminar el enlace de servicio. 

# rellinks
{: #rellinks}

## general
{: #general}

* [Enlace de un servicio mediante la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}](../cfapps/ee.html#ee_bindui)
* [Recuperación de VCAP_SERVICES](../cli/vcapsvc.html#retrieving)


