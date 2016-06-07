---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Acerca de Insights for Weather
{: #about_weather}

*Última actualización: 19 de mayo de 2016*

Utilice {{site.data.keyword.weatherfull}} para incorporar datos
meteorológicos de The Weather Company (TWC) en las aplicaciones
{{site.data.keyword.Bluemix}}.
{:shortdesc}

Puede añadir observaciones del tiempo y previsiones para su aplicación {{site.data.keyword.Bluemix_notm}} y mostrar los datos del tiempo para una zona especificada por una geolocalización utilizando las [API REST de Insights for Weather](https://twcservice.{APPDomain}/rest-api/){:new_window}.
The Weather Company es el proveedor
más completo de datos meteorológicos históricos y previstos. Se capturan datos para todas las formas de tiempo meteorológico,
incluyendo precipitaciones, presión barométrica, viento y tormentas eléctricas.

Puede utilizar las API REST para recuperar la información siguiente:

* Una previsión meteorológica por hora para las próximas 24 horas que se inicie a partir del momento actual
para un geolocalización especificada.
* Una previsión meteorológica diaria para los próximos 10 días que incluye previsiones para los segmentos de
día y noche para un geolocalización especificada. Esta previsión incluye la serie de texto narrativo
de previsión de un máximo de 256 caracteres con unidades de medida apropiadas para la ubicación y en
el idioma solicitado.
* Los datos meteorológicos actuales observados para un geolocalización especificada. Estos datos meteorológicos
incluyen temperatura, precipitación, dirección y velocidad de vientos, humedad, presión barométrica,
punto de condensación, visibilidad y radiación ultravioleta (UV).
* Los datos meteorológicos observados para una geolocalización especificada y un rango de tiempo
especificado. Estos datos se obtienen de estaciones de observación física. Esta
API devuelve observaciones meteorológicas para las condiciones actuales y observaciones anteriores
hasta e incluyendo las 24 horas anteriores.

Para obtener más información sobre las frases y los iconos de meteorología de The Weather Company,
consulte [Código de icono, frases e imágenes](https://docs.google.com/document/d/1MZwWYqki8Ee-V7c7InBuA5CDVkjb3XJgpc39hI9FsI0/edit?pli=1){:new_window}.
También puede [descargar un conjunto de iconos](https://twcdocs.mybluemix.net/download/weatherinsightsicons.zip){:new_window} para utilizarlos en la aplicación.

## Modelo de precios
{: #pricing_models}

El modelo de precios se basa en las llamadas diarias a las API de Insights for Weather que se cargan mensualmente en el cliente. Puede probar los datos meteorológicos en las aplicaciones para cualquier área geográfica, tipo de previsión
u observaciones de series temporales con solo una restricción en el número de llamadas. Los planes
Free, Base y Premium se pueden adquirir sin contrato. Estos planes permite que la aplicación realice
500, 5.000, o 50.000 llamadas de
API por día respectivamente.

También se pueden adquirir varios planes Premium para cada instancia de servicio que se despliegue durante
el periodo de facturación. Si la aplicación utiliza
más de 50.000 llamadas por día o más de 1.000 llamadas por minuto, necesita un contrato con IBM
para la prestación de servicios en curso.

Cuando la aplicación alcanza el límite de llamadas de API que se permiten realizan basándose en el plan
que ha seleccionado, la siguiente llamada de API no se puede realizar de forma satisfactoria hasta que
se permite que la aplicación solicite más llamadas de API.

Por ejemplo, si está utilizando el plan Base, la aplicación puede realizar 500 llamadas de API en un minuto
incluso aunque supere el límite del plan, pero no se permitirá la siguiente llamada de API hasta
5 minutos después. Por lo tanto, es posible que un usuario advierta un retraso en
la renovación de los datos meteorológicos en la aplicación. Debe asegurarse de desarrollar la aplicación para que maneje estos límites y no solicite
ráfagas de llamadas de API. En su lugar, puede supervisar el uso de llamadas de la API para la aplicación. Puede verificar si la aplicación
alcanza el límite del plan comprobando el número de elementos devueltos por la llamada de API.

## Comentarios y soporte
{: #feedback_support}

Si tiene dudas técnicas sobre cómo crear una aplicación con Insights for Weather, publique su consulta
en [Stack Overflow](http://stackoverflow.com/search?q=weather+bluemix){:new_window} y etiquete su pregunta con **bluemix** y **weather**.

Si tiene algún problema con el servicio, utilice el [foro de IBM developerWorks Answers](https://developer.ibm.com/answers/topics/insights-weather/?smartspace=bluemix){:new_window}.
Incluya las etiquetas
**insights-weather** y **bluemix** para permitir que IBM le proporcione un soporte mejor. 

Para obtener información sobre la resolución de problemas con Bluemix, consulte [Resolución de problemas](https://console.{DomainName}/docs/troubleshoot/troubleshoot.html){: new_window}. Para obtener detalles sobre la búsqueda de información y la realización de preguntas a través de foros y sobre cómo contactar con el soporte, consulte [Obtención de soporte al cliente](https://console.{DomainName}/docs/support/index.html#getting-customer-support){: new_window}.
