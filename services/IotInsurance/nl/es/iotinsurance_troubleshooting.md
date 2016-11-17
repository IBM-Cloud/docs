---

copyright:
  years: 2016
lastupdated: "2016-10-27"

---
<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}

# Resolución de problemas de {{site.data.keyword.iotinsurance_short}}
{: #ts}

A continuación se muestran las respuestas a las preguntas más habituales sobre resolución de problemas acerca del uso de {{site.data.keyword.iotinsurance_full}} en {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problema al desplegar las apps
{: #deployingapps}
Es posible que no pueda desplegar las apps para {{site.data.keyword.iotinsurance_short}} si no tiene suficiente memoria libre en su organización de {{site.data.keyword.Bluemix_notm}}. Puede reducir la memoria que utilizan sus apps o aumentar la cuota de memoria de su cuenta.
{:shortdesc}

Cuando abre el servicio {{site.data.keyword.iotinsurance_short}}, la función Desplegar no está habilitada y no puede desplegar ninguna app.
{: tsSymptoms}

Debe haber al menos 2 GB de memoria libre en su organización para habilitar la función Desplegar. Las cuentas de prueba tienen una cuota de memoria máxima de 2 GB. Si ha creado servicios o apps que no son de {{site.data.keyword.iotinsurance_short}}, su organización no tiene suficiente memoria para desplegar las apps de {{site.data.keyword.iotinsurance_short}}.
{: tsCauses}

Puede aumentar la cuota de memoria de su cuenta o reducir la memoria que utilizan sus servicios y aplicaciones.
- Para aumentar la cuota de memoria de su cuenta, puede [convertir su cuenta de prueba en una cuenta de pago](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).
- Para reducir la memoria en uso rápidamente, elimine todos los servicios y apps que no sean de {{site.data.keyword.iotinsurance_short}}. Reinicie el servicio {{site.data.keyword.iotinsurance_short}} para que los cambios entren en vigor.
- Para las cuentas de pago que tienen más de 2 GB de memoria total, es posible que pueda evitar tener que eliminar otros servicios o apps ajustando la cantidad de memoria que utilizan. Para obtener información, consulte [El límite memoria de la organización se ha excedido](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory).
{: tsResolve}

## Problemas de rendimiento 
{: #performance_issues}

Durante periodos de máxima actividad, podría experimentar un rendimiento más lento.
{:shortdesc}

Los sistemas ocupados que realicen llamadas a API frecuentes podrían sufrir retrasos en los tiempos de respuesta.
{: tsSymptoms}

De forma predeterminada, {{site.data.keyword.iotinsurance_short}} despliega una versión de prueba de {{site.data.keyword.cloudantfull}}. Esta versión limita el número de llamadas de API que se pueden realizar por segundo.
{: tsCauses}

Actualice a la versión estándar de {{site.data.keyword.cloudant}}.
{: tsResolve}

## Obtención de ayuda y soporte para {{site.data.keyword.iotinsurance_short}}
{: #gettinghelp}

Si tiene problemas o preguntas cuando se utiliza {{site.data.keyword.iotinsurance_full}}, puede comprobar {{site.data.keyword.Bluemix_notm}} u obtener ayuda buscando información o planteando preguntas a través de un foro. También puede abrir una incidencia de soporte.

* Puede comprobar si está disponible {{site.data.keyword.Bluemix_notm}} accediendo a la [página de estado de Bluemix](https://developer.ibm.com/bluemix/support/#status){:new_window}.

* Puede consultar los foros para ver si otros usuarios se han encontrado con el mismo problema. Al utilizar los foros para formular una pregunta, etiquete su pregunta para que lo puedan ver los equipos de desarrollo de {{site.data.keyword.Bluemix_notm}}.
  <!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->
* Si tiene preguntas técnicas sobre el desarrollo o el despliegue de una aplicación con {{site.data.keyword.iotinsurance_short}}, publique su pregunta en [Stack Overflow](http://stackoverflow.com/search?q=iot-insurance+ibm-bluemix){:new_window} y etiquete su pregunta con "ibm-bluemix" e "iot-for-insurance".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* Para preguntas acerca del servicio e instrucciones de iniciación, utilice el foro de [IBM developerWorks dW Answers](https://developer.ibm.com/answers/topics/iot-insurance/?smartspace=bluemix){:new_window}. Incluya las etiquetas "iot-for-insurance" y "bluemix".

Consulte [Obtención de ayuda](https://www.{DomainName}/docs/support/index.html#getting-help) para obtener más detalles sobre el uso de los foros.

* Si todavía no puede resolver el problema, puede abrir una incidencia de soporte de IBM. Para obtener información sobre cómo abrir una incidencia de soporte de IBM, o sobre los niveles de soporte y gravedad de las incidencias, consulte [Cómo obtener soporte](https://www.{DomainName}/docs/support/index.html#contacting-support).


# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}
* [Código de app para móvil de ejemplo en GitHub](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## Referencia de API
{: #api}
* [API de {{site.data.keyword.iotinsurance_short}}](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [Ejemplos de API de {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}

## Enlaces relacionados
{: #general}
* [Documentación de {{site.data.keyword.iot_full}}](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Foro de soporte para desarrolladores](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
  * [Foro de soporte de Stack Overflow](http://stackoverflow.com/questions/tagged/ibm-bluemix)
