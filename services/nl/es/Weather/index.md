---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Guía de inicio de Insights for Weather
{: #insights_weather_overview}

*Última actualización: 19 de mayo de 2016*

Utilice {{site.data.keyword.weatherfull}} para incorporar datos
meteorológicos de The Weather Company (TWC) en las aplicaciones
{{site.data.keyword.Bluemix}}.
{:shortdesc}

**Nota:** El servicio Insights for Weather no está disponible actualmente en Japón. 

Antes de empezar, cree una aplicación web de {{site.data.keyword.Bluemix_notm}} en el panel de control con un tiempo de ejecución como Liberty for Java. Espere que su app se suministre y, a continuación, añada el servicio Insights for Weather a la app. 

Al enlazar la app a Insights for Weather, está
suministrando una instancia de servicio con credenciales exclusivas. La app utiliza estas credenciales con las [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window} para recuperar datos meteorológicos. 

Siga estos pasos para recuperar las credenciales de `VCAP_SERVICES` e integrar la instancia de servicio con su app. 

1. Vaya a la página de visión general de la aplicación.
2. Vaya a la sección **Variables de entorno**. Se muestra la información `VCAP_SERVICES` para cada uno de los servicios.
3. Anote los valores de nombre de usuario y contraseña del servicio Insights for Weather.
Para probar las [API REST](https://twcservice.{APPDomain}/rest-api/){:new_window},
debe introducir estas credenciales cuando se le solicite que inicie sesión.
Su `VCAP_SERVICES` es parecido al siguiente ejemplo:

```
{
   "weatherinsights": [
     {
      "name": "Insights for Weather",
      "label": "weatherinsights",
      "plan": "Free",
      "credentials": {
         "port": "443",
         "username": "fa7fed4b86baa0ec3e48e96b29cd2a03",
         "host": "twcservice.mybluemix.net",
         "password": "7abcxw29",
         "url": "https://fa7fed4b86baa0ec3e48e96b29cd2a03:7cunxw29@cdeservice.mybluemix.net"
      }
     }
   ]
}
```

**Nota:** Cada región es independiente. No es posible utilizar las credenciales de servicio facilitadas en una región para autenticarse en un servicio de otra región.
Si no se introducen las credenciales correctas, aparece un mensaje que indica que no está autorizado. 

# rellinks
{: #rellinks}
## Ejemplos
{: #samples}
* [Demostración de Insights for Weather](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Práctica de Places Insights](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [¿Cómo es el tiempo en Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

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
* [Adición de un servicio a la aplicación](../reqnsi.html){: new_window}
* [Desarrollo de principio a fin](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Hoja de precios de {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Requisitos previos de {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
