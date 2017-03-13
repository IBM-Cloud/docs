---

copyright:
  years: 2017
lastupdated: "2017-02-28"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Iniciación a {{site.data.keyword.mqa}} (En desuso)
{: #gettingstartedtemplate}

**El servicio de {{site.data.keyword.mqafull}} está en desuso.** Para obtener más información sobre el estado y las fechas, consulte la [entrada del blog Retirada de Bluemix Mobile Quality Assurance ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://www.ibm.com/blogs/bluemix/?p=72728){: new_window}.
{:deprecated}

{{site.data.keyword.mqafull}} ayuda a los equipos a capturar datos sobre la experiencia del usuario y de los responsables de realizar pruebas para crear y distribuir apps para móvil de alta calidad.
{: shortdesc}

Para empezar a utilizar de inmediato el servicio de {{site.data.keyword.mqa}}, siga estos pasos:

1. Después de crear una instancia <!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->del servicio de {{site.data.keyword.mqa}}, puede acceder a la consola de {{site.data.keyword.mqa}} pulsando el mosaico en el panel de control de la sección **Servicios** de {{site.data.keyword.Bluemix}}.

	El servicio de {{site.data.keyword.mqa}} se lanzará.

2. Añada una app para móvil a la instancia de {{site.data.keyword.mqa}} seleccionando **Añadir App de MQA** y proporcionando un nombre para la app.

3. Descargue los {{site.data.keyword.mqa}} [SDK de cliente ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://www.ibm.com/support/docview.wss?uid=swg27044490){: new_window} y complete la preparación de la app siguiendo uno de los siguientes procedimientos:

	* [Preparar MQA con una app Android](mqa_inst_app_android.html)
	* [Preparar MQA con una app iOS](mqa_inst_app_ios.html)
	* [Preparar MQA con una app Cordova](mqa_inst_app_cord.html)

	Se utiliza un solo SDK para instrumentar las apps de preproducción y de producción. Puede utilizar el parámetro `MODE:` para especificar *QA* para el modo de pre-producción o especificar *MARKET* para el modo de producción. Especifique el modo de preproducción para que los encargados de realizar pruebas internas puedan ofrecer información detallada sobre los errores y bloqueos que se producen en la app. Especifique el modo de producción para que los usuarios puedan proporcionar información detallada sobre la app. Si la app está en producción, {{site.data.keyword.mqa}} facilita la obtención de información de los usuarios desde la misma app.

4. Una vez que haya preparado la app, verá información de calidad más detallada para ella seleccionando una de las siguientes opciones en la interfaz de la instancia de servicio de {{site.data.keyword.mqa}}:

	<dl>
		<dt><strong>Sesiones</strong></dt>
		<dd>Revise la información sobre bloqueos, errores, comentarios y estado del dispositivo durante la sesión. Consulte [Ver detalles de la sesión ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ViewingSessionDetails.html){: new_window} en IBM Knowledge Center para obtener más información.</dd>
		<dt>![](/images/cap_crashicon.jpg) <strong>Bloqueos</strong></dt>
		<dd>Revise la información sobre la causa de los bloqueos. Consulte los [informes de bloqueo ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_CrashReports.html){: new_window} en IBM Knowledge Center para obtener más información.</dd>
		<dt>![](/images/cap_bugicon.jpg) <strong>Errores</strong></dt>
		<dd>Revise la información que ofrecen los usuarios, como informes sobre errores, capturas de pantalla y detalles del dispositivo. Consulte los [informes sobre errores ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_BugReports.html){: new_window} en IBM Knowledge Center para obtener más información.</dd>
		<dt>![](/images/cap_feedbackicon.jpg) <strong>Comentarios</strong></dt>
		<dd>Revise las respuestas con comentarios de los usuarios para ver quién ha escrito el comentario y cuándo lo ha hecho. Consulte los [comentarios de usuarios ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/c_UserFeedback.html){: new_window} en IBM Knowledge Center para obtener más información.</dd>
		<dt><strong>Puntuación de opinión (si está configurada)</strong></dt>
		<dd>Revise la puntuación según la opinión de los usuarios a las versiones durante el tiempo para supervisar, calibrar y mejorar la calidad de la app. Consulte la [opinión general de los usuarios ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/UserSentiment.html){: new_window} en IBM Knowledge Center para obtener más información.</dd>
		<dt><strong>Dispositivos registrados</strong></dt>
		<dd>Revise la lista de dispositivos que se han utilizado durante una sesión de prueba e información sobre estos dispositivos. Consulte [Ver información del dispositivo ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/t_ManagingDevices.html){: new_window} en IBM Knowledge Center para obtener más información.</dd>
	</dl>

	Estas métricas incluyen los siguientes datos:

	* Datos de preproducción de bloqueos, errores, comentarios y sesiones.
	* Datos de producción de bloqueos, comentarios, opiniones y sesiones.

	![Captura de pantalla de la interfaz donde puede visualizar medidas de calidad de una app.](images/quality_metrics_saas4.gif)

	Al visualizar esta información para sus apps, puede determinar si hay que seguir investigando determinados problemas. Por ejemplo, si la frecuencia de bloqueos de una app se dispara, puede pulsar la tasa de bloqueos para ver información más detallada sobre informes de bloqueo correspondientes a dicha app.

5. Para ver la puntuación general de opinión de la app, debe configurar el análisis de opinión:

	1. En la sección *Puntuación de opinión*, pulse el enlace para configurar el análisis de opinión de la app seleccionada.

	2. En la página Detalles de la aplicación, [configure el análisis de opinión ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://www.ibm.com/support/knowledgecenter/SSJML5_6.0.0/com.ibm.mqa.uau.saas.doc/topics/tEnablingUserSentiment.html){: new_window} y guarde los cambios.


# Enlaces relacionados
{: #rellinks notoc}

## Guías de aprendizaje y ejemplos
{: #samples notoc}

* [Vídeo: Iniciación a Mobile Quality Assurance in Bluemix ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://www.youtube.com/watch?v=zHRfGatcKPM){: new_window}  
* [Vídeo: Análisis de opinión en Mobile Quality Assurance ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://www.youtube.com/watch?v=uhkqb8BIn6k){: new_window}
* [developerWorks: Añadir IBM Mobile Quality Assurance al régimen de calidad móvil ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://www.ibm.com/developerworks/library/mo-mqa/index.html){: new_window}
* [developerWorks: Crear apps para móvil que funcionan: Cinco consejos de un panel de expertos ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://www.ibm.com/developerworks/library/mo-mqa-tips/index.html){: new_window}
* [developerWorks: Crear una app para móvil que no es perfecta ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://www.ibm.com/developerworks/library/mo-build-imperfect-mobile-app/){: new_window}
* [developerWorks: Retos y prácticas recomendadas de DevOps para apps para móvil ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](http://www.ibm.com/developerworks/library/mo-bestdevops-mobileapps/index.html){: new_window}
* [Ejemplo: bluelist-mqa ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://hub.jazz.net/project/mobilecloud/bluelist-mqa/overview){: new_window}
