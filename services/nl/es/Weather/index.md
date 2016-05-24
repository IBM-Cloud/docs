---

copyright: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Guía de inicio de Insights for Weather
{: #insights_weather_overview}

*Última actualización: 06 de abril de 2016*

Utilice {{site.data.keyword.weatherfull}} para incorporar datos
meteorológicos de The Weather Company (TWC) en las aplicaciones
{{site.data.keyword.Bluemix}}.
{:shortdesc}

En las siguientes instrucciones se indica el proceso para crear una aplicación, enlazarla con el servicio Insights for Weather y recuperar las credenciales del servicio para interactuar con las [API REST](https://twcservice.{APPDomain}/rest-api/).

### Crear una aplicación
{: #create_an_app}

Para la demostración, crearemos una aplicación utilizando el tiempo de ejecución de Liberty for Java, pero el proceso general siguiente se puede aplicar a otros tiempos de ejecución. 

1. Si no tiene una aplicación existente, en el panel de control, pulse **CREATE APP**.
2. Cuando se le solicite que elija la plantilla de aplicación, pulse **WEB**.
3. Cuando se le solicite que elija un iniciador, pulse **Liberty for Java**.
4. Pulse **Continuar**.
5. En el campo de **Nombre de aplicación**, especifique el nombre de la aplicación.
6. Pulse **Finalizar**. Espere a que la aplicación esté disponible.

### Añadir el servicio Insights for Weather
{: #add_insights_for_weather_service}

Siga estos pasos para añadir el servicio Insights for Weather a la aplicación. 
1. Abra el menú **Catálogo**.
2. En la sección **Datos & Análisis**, pulse **Insights for Weather**. 
3. En la lista desplegable **App**, seleccione la aplicación.
4. Pulse **UTILIZAR**.
5. Cuando se le solicite, pulse **Volver a transferir** para reiniciar la aplicación.

### Recuperar las credenciales de Insights for Weather
{: #retrieve_weather_credentials}

Al enlazar la aplicación a Insights for Weather, está
suministrando una instancia de servicio con credenciales exclusivas. Estas credenciales se almacenan en
`VCAP_SERVICES` en la aplicación y son esenciales para soportar
la interacción entre los servicios. 

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

# rellinks
## Ejemplos
* [Demostración de Insights for Weather](http://insights-for-weather-demo.mybluemix.net/){: new_window}
* [Práctica de Places Insights](https://github.com/IBM-Bluemix/places-insights-lab){: new_window}
* [¿Cómo es el tiempo en Bluemix?](https://developer.ibm.com/bluemix/2015/12/08/insights-weather-sample-overview){: new_window}

## api
* [API REST](https://twcservice.{APPDomain}/rest-api/){: new_window}

## Nodos de ejecución compatibles{:id="buildpacks"}
* [Liberty for Java](https://console.{DomainName}/docs/starters/liberty/index.html){: new_window}
* [Node.js](https://console.{DomainName}/docs/runtimes/nodejs/index.html){: new_window}
* [Ruby](https://console.{DomainName}/docs/runtimes/ruby/index.html){: new_window}
* [Go](https://console.{DomainName}/docs/runtimes/go/index.html){: new_window}
* [PHP](https://console.{DomainName}/docs/runtimes/php/index.html){: new_window}
* [Python](https://console.{DomainName}/docs/runtimes/python/index.html){: new_window}

## General
* [Acerca de Insights for Weather](https://console.{DomainName}/docs/services/Weather/weather_overview.html){: new_window}
* [Adición de un servicio a la aplicación](https://console.{DomainName}/docs/services/reqnsi.html#add_service){: new_window}
* [Desarrollo de principio a fin](https://console.{DomainName}/docs/cfapps/ee.html){: new_window}
* [Hoja de precios de {{site.data.keyword.Bluemix_notm}}](https://console.{DomainName}/pricing/){: new_window}
* [Requisitos previos de {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
