---

copyright:
  years: 2016
lastupdated: "2016-10-26"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}


# Acerca de {{site.data.keyword.iotinsurance_short}}
{: #about}
Última actualización: 21 de octubre de 2016
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} es una instancia de producción de IoT integrada que recopila y analiza datos de contexto completos de asegurados para proporcionar evaluaciones de riesgos personalizadas, protección en tiempo real y reducciones del coste de la póliza.
{: shortdesc}

{{site.data.keyword.iotinsurance_short}} proporciona una vista de contexto completa de los activos y de la situación del asegurado, incluida información como la ubicación, el tiempo, el tráfico y el bienestar general. El análisis en profundidad de esta información permite al asegurador proporcionar evaluación de riesgos personalizada y protección en tiempo real para el asegurado. Entre los beneficios del asegurado se incluye evitar riesgos en la forma de alertas previas, recomendaciones personalizadas y procesamiento y acuerdo de reclamaciones racionalizadas. Entre los beneficios para el asegurador se incluyen la satisfacción del cliente, su lealtad y la reducción de gastos utilizando evitar reclamaciones y la automatización de procesos.

## Arquitectura
{: #architecture}

![Arquitectura de {{site.data.keyword.iotinsurance_short}}. En este diagrama se describe el cuerpo principal del tema.](images/IoT4I_architecture.svg "Arquitectura de {{site.data.keyword.iotinsurance_short}}")

Los componentes de {{site.data.keyword.iotinsurance_short}} trabajan juntos como se describe en esta sección. Esta organización también se muestra en el diagrama de arquitectura. El panel de control de {{site.data.keyword.iotinsurance_short}} muestra los datos almacenados en la base de datos de {{site.data.keyword.iot_short_notm}} y {{site.data.keyword.cloudantfull}}. Los dispositivos inteligentes del usuario, conectados a través de la nube de Wink, envían datos al transformador, que procesa los datos y los envía a {{site.data.keyword.iot_short_notm}}. El motor de coberturas procesa los datos y, si cumplen los criterios de cobertura, se envían a través de API al motor de acción. El motor de acción utiliza {{site.data.keyword.mobilepushfull}} para enviar notificaciones a la aplicación móvil del usuario. El usuario también puede utilizar la aplicación móvil para responder a las alertas u ofertas. La respuesta se procesa mediante el servicio {{site.data.keyword.amafull}} y se devuelve a través de API a {{site.data.keyword.iot_short_notm}} y, a continuación al panel de control {{site.data.keyword.iotinsurance_short}}.

## Panel de control del seguro
{: #insurance_dashboard}
El Panel de control del seguro proporciona a los usuarios de la empresa de seguros, como por ejemplo a los agentes, una visión completa de lo que está ocurriendo con los activos asegurados de sus clientes. Pueden ver las coberturas y los sucesos en los niveles de país, estado o cuenta.

El panel de control de seguro de ejemplo se carga con datos simulados para mostrarle un ejemplo del tipo de información que puede recopilar y analizar.

## Aplicación móvil de muestra
{: #mobileapp}
La aplicación móvil de muestra es donde los asegurados como, por ejemplo, los propietarios de casas, ven y responden a la información que {{site.data.keyword.iotinsurance_short}} envía de los sensores de sus hogares.

Al utilizar un dispositivo móvil, los propietarios de casas autorizan al servicio a conectarse a la nube del proveedor del sensor para enviar y recibir datos. Por ejemplo, un propietario de casa puede recibir una notificación en la app de inicio para móvil cuando el sensor detecta una fuga de agua. Para obtener más información, consulte [Instalación y conexión de la app para móvil de ejemplo](iotinsurance_mobile_app.html}).

## API REST y en tiempo real
{: #rest_api}
Las API REST las utiliza la app de inicio para móvil, el panel de control del seguro, el motor de coberturas y el controlador de riesgos. Permiten a los usuarios conocer las asociaciones que existen entre dispositivos y coberturas y acciones. Al utilizar estas API, los programadores pueden crear nuevos usuarios, generar datos de suceso, crear y registrar coberturas nuevas y captar datos de suceso.

La API a la que accede desde la consola de servicio está personalizada para la instancia de {{site.data.keyword.iotinsurance_short}}.

En la página de la API, puede:  
  - Ver todas las llamadas de API disponibles y la documentación asociada.
  - Intentar llamadas de API individuales.  Seleccione una llamada de API para mostrar toda la información y, a continuación, pulse **Probarlo**.

Hay disponibles ejemplos de API para ayudarle a comenzar con casos de ejemplo comunes. Para obtener más información, consulte [Ejemplos de la API de {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).


## Transformer
{: #transformer}
Transformer solicita nueva información de la API de servidor de nube y la transforma para que coincidan los datos en {{site.data.keyword.iotinsurance_short}}. Los datos se publicarán para el resto de la implementación de {{site.data.keyword.iotinsurance_short}} que se utilizará. Los usuarios deben autorizar al componente Transformer para acceder a los datos de nube del sensor y procesar los datos registrados. La autorización se otorga utilizando la app de inicio para móvil. Wink es el único proveedor de nube soportado en este momento.

## Motor de coberturas
{: #shield_engine}
En función de la información almacenada en un suceso, el motor de coberturas determina si se ha producido algún riesgo como por ejemplo una fuga de agua. Si se identifica un riesgo, se pasará al motor de acción. 

## Motor de acción
{: #action_engine}
El motor de acción determina las acciones a tomar en base a la información especificada en la cobertura.

Puede crear coberturas nuevas en JavaScript utilizando la API de {{site.data.keyword.iotinsurance_short}}.

## Coberturas
{: #shields}
Una cobertura es una protección específica que adquiere un cliente del proveedor del seguro. Por ejemplo, un propietario de casa adquiere el seguro en su hogar para ponerle coberturas contra fuego, daños por agua, robos, y otros riesgos. La solución {{site.data.keyword.iotinsurance_short}} proporciona una cobertura incorporada contra el agua. Se alertará a los clientes y estos pueden responder cuando un suceso que implique agua amenace sus hogares. Al utilizar la API REST, los desarrolladores pueden añadir más coberturas.
Las coberturas se ejecutan en el motor de análisis de {{site.data.keyword.iotinsurance_short}}. El motor de análisis identifica el tipo de riesgo (por ejemplo, *Se ha detectado agua*), la cuenta de usuario del sensor que ha enviado el riesgo, y las coberturas asociadas con la cuenta. Se puede realizar la acción en función de dicha información.

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
