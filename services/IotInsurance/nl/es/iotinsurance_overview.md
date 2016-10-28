---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}


# Acerca de {{site.data.keyword.iotinsurance_short}}
{: #about_servicename}
Última actualización: 15 de septiembre de 2016
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} es una instancia de producción de IoT integrada que recopila y analiza datos de contexto completos de asegurados para proporcionar evaluaciones de riesgos personalizadas, protección en tiempo real y reducciones del coste de la póliza.
{: shortdesc}

{{site.data.keyword.iotinsurance_short}} proporciona una vista de contexto completa de los activos y de la situación del asegurado, incluida información como la ubicación, el tiempo, el tráfico y el bienestar general. El análisis en profundidad de esta información permite al asegurador proporcionar evaluación de riesgos personalizada y protección en tiempo real para el asegurado. Entre los beneficios del asegurado se incluye evitar riesgos en la forma de alertas previas, recomendaciones personalizadas y procesamiento y acuerdo de reclamaciones racionalizadas. Entre los beneficios para el asegurador se incluyen la satisfacción del cliente, su lealtad y la reducción de gastos utilizando evitar reclamaciones y la automatización de procesos.

## Flujo de proceso
{: #processFlow}
El asegurador tiene una instancia dentro del intermediario de servicio de {{site.data.keyword.Bluemix_notm}}. Los clientes del asegurador tienen sensores en sus casas, conectados a la nube del proveedor del sensor. Desde sus dispositivos móviles, los propietarios de casas autorizan al servicio de {{site.data.keyword.iotinsurance_short}} a recibir datos de sensores de {{site.data.keyword.iotinsurance_short}}. El servicio de {{site.data.keyword.iotinsurance_short}} se conecta a la nube del proveedor del sensor y extrae datos para cada usuario y los envía al servidor de IoT. Si el sensor muestra que se cumplen los parámetros especificados en las coberturas del asegurador en el hogar del cliente, las notificaciones se enviarán al panel de control del asegurador y al dispositivo del cliente.

## Componentes
{: #components}

### Panel de control del seguro
{: #insurance_dashboard}
El Panel de control del seguro proporciona a los usuarios de la empresa de seguros, como por ejemplo a los agentes, una visión completa de lo que está ocurriendo con los activos asegurados de sus clientes. Pueden ver las coberturas y los sucesos en los niveles de país, estado o cuenta.

El panel de control de seguro de ejemplo se carga con datos simulados para mostrarle un ejemplo del tipo de información que puede recopilar y analizar.

### App de inicio para móvil
{: #mobileapp}
La app de inicio para móvil es donde los asegurados como, por ejemplo, los propietarios de casas, ven y responden a la información que {{site.data.keyword.iotinsurance_short}} envía de los sensores de sus hogares.

Al utilizar un dispositivo móvil, los propietarios de casas autorizan al servicio a conectarse a la nube del proveedor del sensor para enviar y recibir datos. Por ejemplo, un propietario de casa puede recibir una notificación en la app de inicio para móvil cuando el sensor detecta una fuga de agua. Para obtener más información, consulte [Instalación y conexión de la app de inicio para móvil](iotinsurance_mobile_app.html}).

### API REST
{: #rest_api}
La API REST la utiliza la app de inicio para móvil, el panel de control del seguro, el motor de coberturas y el controlador de riesgos. Permite a los usuarios conocer las asociaciones que existen entre dispositivos y coberturas y acciones. Al utilizar esta API, los programadores pueden crear nuevos usuarios, generar datos de suceso, crear y registrar coberturas nuevas y captar datos de suceso.

La API a la que accede desde la consola de servicio está personalizada para la instancia de {{site.data.keyword.iotinsurance_short}}.

En la página de la API, puede:  
  - Ver todas las llamadas de API disponibles y la documentación asociada.
  - Intentar llamadas de API individuales.  Seleccione una llamada de API para mostrar toda la información y, a continuación, pulse **Probarlo**.

Hay disponibles ejemplos de API para ayudarle a comenzar con casos de ejemplo comunes. Para obtener más información, consulte [Ejemplos de la API de {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).

### Proveedor de nube
{: #cloudprovider}
Los usuarios deben autorizar al componente Transformer para acceder a los datos de nube del sensor y procesar los datos registrados. La autorización se otorga utilizando la app de inicio para móvil. Wink es el único proveedor de nube soportado en este momento.

### Transformer
{: #transformer}
Transformer solicita nueva información de la API de servidor de nube y la transforma para que coincidan los datos en {{site.data.keyword.iotinsurance_short}}. Los datos se publicarán para el resto de la implementación de {{site.data.keyword.iotinsurance_short}} que se utilizará.

### Motor de análisis
{: #analytics_engine}
En función de la información almacenada en un suceso, el motor de análisis determina si se ha producido algún riesgo como por ejemplo una fuga de agua. Si se identifica un riesgo, se pasará al controlador de riesgos. El Motor de acción visualiza los datos de la base de datos para determinar la acción a realizar en función de la información especificada en la cobertura.

Puede crear coberturas nuevas en JavaScript utilizando la API de {{site.data.keyword.iotinsurance_short}}.

### Coberturas
{: #shields}
Una cobertura es una protección específica que adquiere un cliente del proveedor del seguro. Por ejemplo, un propietario de casa adquiere el seguro en su hogar para ponerle coberturas contra fuego, daños por agua, robos, y otros riesgos. La solución {{site.data.keyword.iotinsurance_short}} proporciona una cobertura incorporada contra el agua. Se alertará a los clientes y estos pueden responder cuando un suceso que implique agua amenace sus hogares. Al utilizar la API REST, los desarrolladores pueden añadir más coberturas.
Las coberturas se ejecutan en el motor de análisis de {{site.data.keyword.iotinsurance_short}}. El motor de análisis identifica el tipo de riesgo (por ejemplo, *Se ha detectado agua*), la cuenta de usuario del sensor que ha enviado el riesgo, y las coberturas asociadas con la cuenta. Se puede realizar la acción en función de dicha información.
