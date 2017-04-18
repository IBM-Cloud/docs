---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-04"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Iniciación a {{site.data.keyword.iotinsurance_short}}
{: #gettingstarted}

{{site.data.keyword.iotinsurance_full}} es un servicio de {{site.data.keyword.Bluemix_notm}} que puede utilizar para recopilar, gestionar y analizar datos de asegurados conectados. {{site.data.keyword.iotinsurance_short}} le ofrece la capacidad de proporcionar evaluación de riesgos personalizada, protección en tiempo real y reducciones del coste de la póliza.
{:shortdesc}

Para utilizar este servicio, debe desplegar los servicios y las apps necesarias y, a continuación, configurar los servicios. Encontrará una descripción general de los servicios y aplicaciones, así como un diagrama de la arquitectura, en [Acerca de {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html)

**Requisitos previos:** Antes de comenzar, asegúrese de que se cumplan los siguientes requisitos previos:
- Debe haber una instancia del [servicio {{site.data.keyword.iotinsurance_short}}](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/) en su espacio de {{site.data.keyword.Bluemix_notm}}.
- Debe haber al menos 2 GB de memoria libre en su organización de {{site.data.keyword.Bluemix_notm}} para habilitar la función Desplegar.

## Despliegue de los servicios y aplicaciones necesarios
{: #deploying_services}

1. Para desplegar todos los servicios y las aplicaciones necesarios, en la [consola de {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/#all-items), pulse el servicio de {{site.data.keyword.iotinsurance_short}} y, a continuación, pulse **Desplegar**.

  {{site.data.keyword.iotinsurance_short}} despliega todos los servicios y las aplicaciones de Node.js que necesita. Enlaza automáticamente las aplicaciones a los servicios.

  Cada instancia de servicio utiliza el plan de servicio predeterminado. Puede actualizar cualquier plan de servicio más tarde desde la consola del servicio. También puede utilizar una instancia existente de un servicio suprimiendo la nueva instancia y conectando manualmente la instancia existente al servicio {{site.data.keyword.iotinsurance_short}}. Para obtener más información sobre las aplicaciones, consulte [Acerca de {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

  **Nota**: {{site.data.keyword.iotinsurance_short}} ya no despliega {{site.data.keyword.amafull}} ni {{site.data.keyword.mobilepushfull}}. Las versiones anteriores de {{site.data.keyword.iotinsurance_short}} utilizaban el servicio {{site.data.keyword.amashort}} para procesar las respuestas desde la aplicación móvil. Este proceso sigue funcionando para todas las instancias existentes de {{site.data.keyword.iotinsurance_short}}. Sin embargo, debe crear un proceso de autenticación personalizado para utilizar la aplicación móvil con las nuevas instancias de {{site.data.keyword.iotinsurance_short}}. Opcionalmente, también puede [crear una instancia de {{site.data.keyword.mobilepushshort}}](https://console.ng.bluemix.net/docs/services/mobilepush/index.html), configurarla y enlazarla a la API de {{site.data.keyword.iotinsurance_short}}.

2. Compruebe que el panel de control de {{site.data.keyword.iotinsurance_short}} sea funcional y que tenga acceso a las API.
  1. Abra el panel de control de {{site.data.keyword.iotinsurance_short}} pulsando **Abrir**. Acepte las credenciales prerrellenadas pulsando **Iniciar sesión**.
  2. Vuelva a la consola de servicio de {{site.data.keyword.iotinsurance_short}} y visualice las API pulsando **API**.

  **Nota:** después del despliegue, puede acceder al panel de control o las API directamente especificando sus respectivos URL en el navegador. Cuando se utiliza este método, debe especificar las credenciales del servicio {{site.data.keyword.iotinsurance_short}}. Para localizar sus credenciales, vuelva a la consola de servicio de {{site.data.keyword.iotinsurance_short}}. Pulse el separador **Credenciales de servicio** y, a continuación, pulse **Ver credenciales**. Tome nota del ID y contraseña de usuario.


<!--
## Configuring
{: #iot4i_configservices}



### Configuring {{site.data.keyword.amashort}}
{: #config_ama}
1. Return to your Bluemix console. All apps and services that were deployed by {{site.data.keyword.iotinsurance_short}} are displayed.

2. Copy the URL of the {{site.data.keyword.iotinsurance_short}} API application. Right-click the API application and select **Copy Link Location**.

3. Open the {{site.data.keyword.amashort}} service. The service is available in the Services section of your {{site.data.keyword.Bluemix_notm}} console.

4. Enable authentication by clicking **On**.

5. In the **Custom** section, enter the following authentication credentials:

  - **Realm name**: `IoT4I`

  - **Custom Identity Provider Url**: Paste the URL of the API application that you copied in a previous step.

  - **Your Web Application Redirect URIs**: Leave this field blank.

6. Save your settings. You can now return to the {{site.data.keyword.iotinsurance_short}} service console or your {{site.data.keyword.Bluemix_notm}} console.
-->


## Creación y configuración de {{site.data.keyword.mobilepushshort}}
{: #config_push}
Para habilitar las notificaciones push para una app para móvil existente, opcionalmente puede crear una instancia del servicio {{site.data.keyword.mobilepushshort}}, enlazarla a la API de {{site.data.keyword.iotinsurance_short}} y añadir un archivo PKCS (Public Key Cryptography Standards) 12. Para obtener información sobre la app para móvil, consulte [Instalación y conexión de la app para móvil de ejemplo](iotinsurance_mobile_app.html). Para obtener información sobre {{site.data.keyword.mobilepushshort}}, consulte [Iniciación a las notificaciones push](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

Para configurar el servicio después de la creación, realice los siguientes pasos:

  1. Abra el servicio {{site.data.keyword.mobilepushshort}}.
  2. Pulse **Configurar**.
  3. En la sección Certificado de notificaciones push de Apple, suba el archivo PKCS 12 para su app para móvil y especifique la contraseña.


Qué hacer a continuación
{: #whats_next}
Obtenga más información de lo que puede hacer con {{site.data.keyword.iotinsurance_short}}.

- Utilice las instrucciones y las API del Kit de herramientas de cobertura para crear un [usuario y una asociación de coberturas](iotinsurance_shield_toolkit.html).
<!-- - Install and connect the [sample mobile app](iotinsurance_mobile_app.html). -->
- Descargue o visualice todas las [API en el sitio de GitHub ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}.

# Enlaces relacionados
{: #rellinks}

## Guías de aprendizaje y ejemplos
{: #samples}
* [Biblioteca de coberturas de {{site.data.keyword.iotinsurance_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-shields){: new_window}
* [Código de aplicación móvil de ejemplo en GitHub ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## Referencia de API
{: #api}
* [API de {{site.data.keyword.iotinsurance_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://iot4i-api-docs.mybluemix.net/){:new_window}
* [Ejemplos de API de {{site.data.keyword.iotinsurance_short}} ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples){:new_window}


## Enlaces relacionados
{: #general}
* [Documentación de {{site.data.keyword.iot_full}}](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Foro de soporte para desarrolladores ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix]){:new_window}
* [Foro de soporte de Stack Overflow ![Icono de enlace externo](../../icons/launch-glyph.svg)](http://stackoverflow.com/questions/tagged/ibm-bluemix){:new_window}
