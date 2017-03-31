---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-10"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Note to writers - index.md and iot4egettingstarted.md are (almost) duplicates and a change to one should be made to both. index.md appears within the product app as the getting started page. iot4egettingstarted.md appears as the top level topic in the docs toc. -->

# Creación de apps con el iniciador de {{site.data.keyword.iotelectronics}}

{{site.data.keyword.iotelectronics_full}} es una solución integrada de extremo a extremo que permite a las apps comunicarse con, controlar, analizar y actualizar dispositivos conectados. El iniciador incluye una app de inicio que le permite crear y controlar dispositivos simulados y una app para móvil de ejemplo que le permite controlar estos dispositivos desde el dispositivo móvil.
{:shortdesc}

## Antes de empezar

Antes de empezar, debe desplegar una instancia de {{site.data.keyword.Bluemix_notm}} en su organización de {{site.data.keyword.iotelectronics}}. Al desplegar una instancia, se despliegan automáticamente las aplicaciones de componente y los servicios del iniciador.

 Puede [encontrar el {{site.data.keyword.iotelectronics}} iniciador](https://console.{DomainName}/catalog/starters/iot-for-electronics-starter/) en la sección Contenedores modelo del catálogo {{site.data.keyword.Bluemix_notm}}.

## Iniciación a {{site.data.keyword.iotelectronics}}
Para empezar, realice las tareas siguientes:

1. [Habilite las comunicaciones móviles y la seguridad](iotelectronics_config_mca.html) configurando {{site.data.keyword.amafull}}.
2. [Cree dispositivos simulados](iot4ecreatingappliances.html) mediante la aplicación web de inicio {{site.data.keyword.iotelectronics}}. Para fines de demostración, las lavadoras se utilizan como el dispositivo simulado dentro del iniciador de {{site.data.keyword.iotelectronics}}. El dispositivo que elija para conectarse puede ser cualquier tipo de dispositivo electrónico inteligente.
3. [Descargue y conecte](iotelectronics_config_mobile.html) la app para móvil de ejemplo.


## Qué hacer a continuación
Vea lo que puede hacer con {{site.data.keyword.iotelectronics}}.

- [Explorar la app de inicio](iot4ecreatingappliances.html) para experimentar cómo una empresa de producción puede supervisar dispositivos conectados a {{site.data.keyword.iot_short_notm}}.
- [Explorar la app para móvil](iotelectronics_config_mobile.html) para experimentar cómo pueden registrar e interactuar con sus dispositivos los propietarios de aplicaciones.
- [Explorar y gestionar datos](iotelectronics_dashboard.html) de los dispositivos registrados en {{site.data.keyword.iot_short_notm}}.
- [Explorar las API![icono de enlace externo](../../icons/launch-glyph.svg)](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html){:new_window} para descubrir cómo puede personalizar y ampliar sus apps de {{site.data.keyword.iotelectronics}}.

# Enlaces relacionados
{: #rellinks}
<!-- Related Links last updated 23 October 2016 - new API source -->
## Documentación de la API
{: #api}
* [API de {{site.data.keyword.iotelectronics}} ![icono de enlace externo](../../icons/launch-glyph.svg)](https://broker-uss-iot4e.electronics.internetofthings.ibmcloud.com/public/iot4eregistrationapi.html){:new_window}
* [API de {{site.data.keyword.iot_short}} ![icono de enlace externo](../../icons/launch-glyph.svg)](https://developer.ibm.com/iotfoundation/recipes/api-documentation/){:new_window}


## Componentes
{: #general}

* [Documentación de {{site.data.keyword.iotelectronics}}](iotelectronics_overview.html){:new_window}
* [Documentación de {{site.data.keyword.iot_full}}](https://console.ng.bluemix.net/docs/services/IoT/index.html){:new_window}
*  [Documentación de {{site.data.keyword.amashort}}](https://console.ng.bluemix.net/docs/services/mobileaccess/overview.html){:new_window}
* [Documentación de {{site.data.keyword.sdk4nodefull}}](https://console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime){:new_window}

## Ejemplos
{: #samples}
* [App para móvil de ejemplo](https://console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html){:new_window}
