---

copyright:
  years: 2015, 2016
lastupdated: "2016-07-28"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Guía de inicio de {{site.data.keyword.weather_short}}
{: #insights_weather_overview}

Utilice {{site.data.keyword.weatherfull}} para incorporar datos
meteorológicos de The Weather Company (TWC) en las aplicaciones
{{site.data.keyword.Bluemix}}.
{:shortdesc}

**Atención:** Actualmente, el servicio {{site.data.keyword.weather_short}} **es posible que no** se pueda adquirir
o utilizar en los siguientes países o regiones: Afganistán, Armenia, Azerbaiyán,
Bahrein, Bangladesh, Bhutan, Brunei, Camboya, China, Chipre, Georgia,
Indonesia, Irán, Irak, Japón, Jordania, Kazajistán, Kuwait, Kirguizistán, Laos,
Líbano, Malasia, Maldivas, Mongolia, Myanmar, Nepal, Omán, Pakistán, Filipinas,
Qatar, Rusia, Arabia Saudí, Singapur, Corea del Sur, Sri Lanka, Siria,
Tayikistán, Timor Oriental, Turquía, Turkmenistán, Emiratos Árabes Unidos,
Uzbekistán, Vietnam, Yemen. Esta lista se actualiza cuando hay información adicional disponible.

Si tiene una aplicación existente que utiliza el
[servicio Insights for Weather](https://console.{DomainName}/docs/services/InsightsWeather/index.html){: new_window},
su app continuará funcionando sin modificaciones durante 90 días después de la introducción de
{{site.data.keyword.weather_short}}. Para aprovechar las API recientemente añadidas
y el modelo de tarifas mejorado, puede migrar la aplicación al nuevo servicio.

Antes de empezar, cree una aplicación web de {{site.data.keyword.Bluemix_notm}} en el panel de control con un tiempo de ejecución como Liberty for Java. Espere a que se suministre su app
y, a continuación, añada el servicio {{site.data.keyword.weather_short}} a la app.

Al enlazar la app a {{site.data.keyword.weather_short}}, está suministrando una
instancia de servicio con credenciales exclusivas. La app utiliza estas credenciales con las [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window} para recuperar datos meteorológicos.

Siga estos pasos para recuperar las credenciales de servicio de `VCAP_SERVICES`
e integrar la instancia de servicio con la app.

1. Vaya a la página de visión general de la aplicación.
2. Vaya a la sección **Variables de entorno**. Se muestra la información `VCAP_SERVICES` para cada uno de los servicios.
3. Anote los valores de nombre de usuario y contraseña del servicio {{site.data.keyword.weather_short}}.
Para probar las [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window},
debe introducir estas credenciales cuando se le solicite que inicie sesión.
Su `VCAP_SERVICES` es parecido al siguiente ejemplo:

```
{
{
   "weatherinsights": [
      {
         "name": "Weather Company Data for IBM Bluemix",
         "label": "weatherinsights",
         "plan": "Free",
         "credentials": {
            "username": "d40845df-8125-441f-8e7c-e650726ce721",
            "password": "tDV0HGZz3O",
            "host": "twcservice.mybluemix.net",
            "port": 443,
            "url": "https://d40845df-8125-441f-8e7c-e650726ce721:tDV0HGZz3O@twcservice.mybluemix.net"
         }
      }
   ]
}
```

**Nota:** Cada región es independiente. No es posible utilizar las credenciales de servicio facilitadas en una región para autenticarse en un servicio de otra región.
Si no se pueden entrar las credenciales correctas se genera un mensaje *No autorizado*
en el cuerpo de mensaje.

# rellinks
{: #rellinks}
## Ejemplos
{: #samples}
* [App de demostración de {{site.data.keyword.weather_short}}](http://weather-company-data-demo.{APPDomain}){: new_window}
* [Vídeo de {{site.data.keyword.weather_short}} Deep Dive](https://youtu.be/pZHXIibziUo){: new_window}
* [Práctica de Places Insights](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [App de ejemplo de {{site.data.keyword.Bluemix_notm}} + Weather](https://github.com/IBM-Bluemix/insights-weather){: new_window}
* [IBM Cloud - Bare Metal, NYC Taxi Data, e Insights for Weather (guía de aprendizaje de YouTube)](https://www.youtube.com/watch?v=Uwmzpx9DZ5c){: new_window}

## api
{: #api}
* [API REST](https://twcservice.{APPDomain}/rest-api/){: new_window}

## Nodos de ejecución compatibles
{: #buildpacks}
* [Liberty for Java](https://console.{DomainName}/docs/runtimes/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## General
{: #general}
* [Adición de un servicio a la aplicación](/docs/services/reqnsi.html){: new_window}
* [Desarrollo de principio a fin](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Hoja de precios de {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Requisitos previos de {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
