---

copyright:
  years: 2016
lastupdated: "2016-10-26"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Iniciación a {{site.data.keyword.iotinsurance_short}}

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

2. Compruebe que el panel de control de {{site.data.keyword.iotinsurance_short}} sea funcional y que tenga acceso a las API.
  1. Abra el panel de control de {{site.data.keyword.iotinsurance_short}} pulsando **Abrir**. Acepte las credenciales prerrellenadas pulsando **Iniciar sesión**.
  2. Vuelva a la consola de servicio de {{site.data.keyword.iotinsurance_short}} y visualice las API pulsando **API**.

  **Nota:** después del despliegue, puede acceder al panel de control o las API directamente especificando sus respectivos URL en el navegador. Cuando se utiliza este método, debe especificar las credenciales del servicio {{site.data.keyword.iotinsurance_short}}. Para localizar sus credenciales, vuelva a la consola de servicio de {{site.data.keyword.iotinsurance_short}}. Pulse el separador **Credenciales de servicio** y, a continuación, pulse **Ver credenciales**. Tome nota del ID y contraseña de usuario.

## Configuración de los servicios
{: #iot4i_configservices}
Realice las siguientes tareas para configurar los servicios:

### Configuración de {{site.data.keyword.amashort}}
{: #config_ama}
1. Vuelva a la consola de Bluemix. Se muestran todas las aplicaciones y servicios desplegados mediante {{site.data.keyword.iotinsurance_short}}.

1. Copie el URL de la aplicación de API {{site.data.keyword.iotinsurance_short}}. Pulse con el botón de derecho del ratón en la aplicación de API y seleccione **Copiar ubicación del enlace**.

2. Abra el servicio {{site.data.keyword.amashort}}. El servicio está disponible en la sección Servicios de la consola de {{site.data.keyword.Bluemix_notm}}.

3. Habilite la autenticación pulsando **Activado**.

4. En la sección **Personalizado**, pulse **Configurar** y especifique las siguientes credenciales de autenticación:

  - **Nombre de reino**: `IoT4I`

  - **URL de proveedor de identidad personalizado**: Pegue el URL de la aplicación de API que ha copiado en el primer paso.

  - **URI de redireccionamiento de la aplicación web**: Deje este campo en blanco.

5. Guarde los valores. Ahora puede volver a la consola de servicio de {{site.data.keyword.iotinsurance_short}} o a la consola de {{site.data.keyword.Bluemix_notm}}.

### Configuración de {{site.data.keyword.mobilepushshort}}
{: #config_push}
Para habilitar las notificaciones push para una app para móvil existente, debe configurar el servicio {{site.data.keyword.mobilepushshort}} y añadir un archivo PKCS (Public Key Cryptography Standards) 12. Para obtener información sobre la app para móvil, consulte [Instalación y conexión de la app para móvil de ejemplo](iotinsurance_mobile_app.html). Para obtener información sobre {{site.data.keyword.mobilepushshort}}, consulte [Iniciación a las notificaciones push](https://console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html).

  1. Abra el servicio {{site.data.keyword.mobilepushshort}}.
  2. Pulse **Configurar**.
  3. En la sección Certificado de notificaciones push de Apple, suba el archivo PKCS 12 para su app para móvil y especifique la contraseña.


Qué hacer a continuación
{: #whats_next}
Obtenga más información de lo que puede hacer con {{site.data.keyword.iotinsurance_short}}.

- Utilice las instrucciones y las API del Kit de herramientas de cobertura para crear un [usuario y una asociación de coberturas](iotinsurance_shield_toolkit.html).
- Instale y conecte la [app para móvil de ejemplo](iotinsurance_mobile_app.html).
- Descargue o visualice todas las [API en el sitio de GitHub](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/#iot-for-insurance-api-examples).

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
