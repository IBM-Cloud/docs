---

copyright:
  years: 2015, 2016
lastupdated: "2016-08-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Acerca de {{site.data.keyword.weather_short}}
{: #about_weather}

Utilice {{site.data.keyword.weatherfull}} para incorporar datos
meteorológicos de The Weather Company (TWC) en las aplicaciones
{{site.data.keyword.Bluemix}}.
{:shortdesc}

Puede añadir observaciones del tiempo y previsiones a su aplicación {{site.data.keyword.Bluemix_notm}}
y mostrar los datos del tiempo para una zona especificada por una
geolocalización utilizando las [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window}.
The Weather Company es el proveedor
más completo de datos meteorológicos históricos y previstos. Se capturan datos para todas las formas de tiempo meteorológico,
incluyendo precipitaciones, presión barométrica, viento y tormentas eléctricas.

Puede utilizar las API REST para recuperar la información siguiente:

* Una previsión meteorológica para las siguientes 48 horas que se inicie a partir del momento actual para una geolocalización especificada.
* Una previsión diaria para cada uno de los próximos 3, 5, 7 o 10 días a partir del día actual que incluye previsiones para los segmentos de día y noche para una geolocalización especificada. Esta previsión incluye la serie de texto narrativo
de previsión de un máximo de 256 caracteres con unidades de medida apropiadas para la ubicación y en
el idioma solicitado.
* Una previsión diaria para cada uno de los próximos 3, 5, 7 o 10 días a partir del día actual, que divide cada previsión diariamente en segmentos de mañana, tarde, noche y madrugada.
* Los datos meteorológicos actuales observados para un geolocalización especificada. Estos datos meteorológicos
incluyen temperatura, precipitación, dirección y velocidad de vientos, humedad, presión barométrica,
punto de condensación, visibilidad y radiación ultravioleta (UV).
* Los datos meteorológicos observados para una geolocalización especificada hasta e incluyendo las 24 horas anteriores. Estos datos se obtienen de estaciones de observación física.
* Las alertas meteorológicas emitidas por el gobierno, incluidas las observaciones, los avisos, las sentencias y las advertencias meteorológicas emitidos por el National Weather Service (EE.UU.), Environment Canada y MeteoAlarm (Europa).
* Servicios de almanaque que proporcionan datos meteorológicos diarios o mensuales históricos que se obtienen de estaciones de observación del National Weather Service desde un periodo de tiempo que comprende de 10 a 30 años o más.
* Servicios de correlación de ubicación que proporcionan la capacidad para buscar un nombre de ubicación o un geocódigo (latitud y longitud) para recuperar un conjunto de ubicaciones que coincidan con la solicitud.

## Modelo de precios
{: #pricing_models}

El modelo de tarifas se basa en el número de llamadas por minuto en las API REST. Se cobrará al cliente de forma mensual. Los planes Gratuito y Base le permiten
realizar un máximo de 10 llamadas de API por minuto. Los planes Estándar y Premium
le permiten realizar 150 y 375 llamadas de API por minuto, respectivamente. Cada plan tiene
un número máximo de llamadas de API permitidas.

Puede probar los datos meteorológicos en las aplicaciones para cualquier área geográfica, tipo de previsión
u observaciones de series temporales con solo una restricción en el número de llamadas. Los planes Gratuito, Base, Estándar y Premium se pueden adquirir sin contrato. El plan Gratuito permite a la app realizar 10.000 llamadas. Los planes
restantes permiten a la app realizar 150.000, 2 millones
o 5 millones de llamadas de API al mes, respectivamente.

También se pueden adquirir varios planes de pago para cada instancia de servicio que se despliegue
durante el periodo de facturación. Si la app utiliza más de 10.000 llamadas,
necesita un contrato con IBM para la prestación de servicios en curso.

Cuando la aplicación alcanza el límite de llamadas de API por minuto que se permiten realizan basándose en el plan
que ha seleccionado, la siguiente llamada de API no se puede realizar de forma satisfactoria hasta que
se permite que la aplicación solicite más llamadas de API.

Por ejemplo, si está utilizando el plan Estándar, la app *puede* realizar 500 llamadas de API
en un minuto aunque supere el límite del plan (150 llamadas por minuto),
pero no se permitirá la siguiente llamada de API hasta
5 minutos después. Por lo tanto, es posible que un usuario advierta un retraso en
la renovación de los datos meteorológicos en la aplicación.
Debe asegurarse de desarrollar la aplicación para que maneje estos límites y no solicite
ráfagas de llamadas de API. En su lugar, puede supervisar el uso de llamadas de la API para la aplicación.
Puede verificar si la aplicación
alcanza el límite del plan comprobando el número de elementos devueltos por la llamada de API.

Cuando la aplicación alcanza el límite de llamadas de API al mes que se permite realizar
basándose en el plan que ha seleccionado, las siguientes llamadas de API se cobrarán a una tasa media
de 1,70 $ por 10.000 llamadas de API.

## Comentarios y soporte
{: #feedback_support}

Puede obtener ayuda buscando información o haciendo una pregunta en un foro. También puede abrir una incidencia de soporte. 

Cuando utilice los foros para hacer una pregunta, etiquete la pregunta para que puedan verla los equipos de desarrollo de
{{site.data.keyword.Bluemix_notm}}. 

* Si tiene dudas técnicas sobre cómo desarrollar o desplegar una app con {{site.data.keyword.weather_short}},
publique su consulta en [Stack Overflow](https://stackoverflow.com/questions/tagged/ibm-bluemix+weather){:new_window}
y etiquete su pregunta con **ibm-bluemix** y **weather**.
* Si tiene problemas con el servicio o al obtener instrucciones de inicio, utilice el
[Foro de respuestas de IBM developerWorks](https://developer.ibm.com/answers/topics/weather/?smartspace=bluemix){:new_window}. Incluya los códigos **bluemix** y **weather**. 
* Si tiene preguntas sobre la migración de la app de Insights for Weather a {{site.data.keyword.weather_short}},
póngase en contacto con nosotros en [IBM developerWorks](http://www.ibm.com/developerworks){:new_window}.

Consulte [Obtención de ayuda](https://console.{DomainName}/docs/support/index.html#getting-help){: new_window} para obtener más detalles sobre el uso de los foros. 

Consulte [Cómo obtener soporte](https://console.{DomainName}/docs/support/index.html#contacting-support){: new_window} para obtener información sobre la apertura de una incidencia de soporte de IBM o sobre los niveles de soporte y gravedad de incidencias. 
