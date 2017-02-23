---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-12"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visión general de característica de {{site.data.keyword.iot_short_notm}}
{: #feature_overview}

El {{site.data.keyword.iot_full}} se crea en las siguientes áreas clave:

  1. Conexión: Conectar dispositivos y desarrollar aplicaciones.
  2. Gestión de información: Almacenar y revisar datos de dispositivos e integrar el {{site.data.keyword.iot_short_notm}} con otros servicios.
  3. Analíticas: Visualizar datos de dispositivos en tiempo real utilizando el panel de instrumentos {{site.data.keyword.iot_short_notm}}.
  4. Gestión de riesgos: Configurar la conectividad y la arquitectura seguras con control de acceso para usuarios y aplicaciones.

## Conectar
{: #connect}

{{site.data.keyword.iot_short_notm}} Connect es el punto de partida para cualquier servicio de {{site.data.keyword.iot_short_notm}}. La conexión de dispositivos, la creación de aplicaciones, el control de los dispositivos y la interacción con servicios de terceros están disponibles en Conectar {{site.data.keyword.iot_short_notm}}.

### Dispositivos de pasarela

Al utilizar una pasarela, puede conectar dispositivos al {{site.data.keyword.iot_short_notm}} que, de lo contrario, no se podrían conectar a Internet. Las pasarelas disponen de todas las funciones de un dispositivo, pero también puede publicar y suscribirse en nombre de los dispositivos que tienen conectados. Los dispositivos de pasarela permiten que los grupos de sensores que no se pueden conectar a Internet se conecten a {{site.data.keyword.iot_short_notm}} enviando sus datos a una pasarela. Para obtener más información, consulte [desarrollo para pasarelas](https://console.ng.bluemix.net/docs/services/IoT/gateways/gw_dev_index.html).

### Gestión de dispositivos

Las funciones de gestión de dispositivos se proporcionan a través de una API de gestión de dispositivos y un agente de gestión de dispositivos instalado en dispositivos. Los dispositivos con un agente de gestión de dispositivos pueden realizar acciones de gestión de dispositivos, que se pueden desencadenar mediante el panel de instrumentos principal de {{site.data.keyword.iot_short_notm}} o la API de gestión de dispositivos. Las acciones de gestión de dispositivos incluyen rearrancar, descargar e instalar actualizaciones de firmware y restablecer dispositivos a los parámetros de fábrica. La gestión de dispositivos también se pueden ampliar para que incluya acciones personalizadas de gestión de dispositivos. Para obtener más información, consulte la [documentación de gestión de dispositivos](https://console.ng.bluemix.net/docs/services/IoT/devices/device_mgmt/index.html).

### Integraciones de extensiones y servicios

La integración de extensiones y servicios permite añadir servicios externos y extensiones definidas por el usuario de servicios principales a una instancia de {{site.data.keyword.iot_short_notm}}. Los servicios externos que se pueden integrar con {{site.data.keyword.iot_short_notm}} incluyen los servicios de información meteorológica de The Weather Company, que le permiten consultar información meteorológica actual en la ubicación del dispositivo, datos de Jasper SIM y {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}. Para obtener más información sobre integraciones y extensiones de servicios de terceros, consulte [integración de servicios externos](https://console.ng.bluemix.net/docs/services/IoT/reference/extensions/index.html).

---

## Gestión de la información
{: #information_management}

{{site.data.keyword.iot_short_notm}} Information Management controla los datos que envían los dispositivos después de alcanzar el servicio de {{site.data.keyword.iot_short_notm}}. La gestión de información incluye el almacenamiento y la transformación de datos.

### Memoria caché de sucesos del último dispositivo

Al utilizar la {{site.data.keyword.iot_short_notm}} Last Event Cache API, puede recuperar el último suceso que ha enviado un dispositivo. Esto funciona si el dispositivo está en línea o fuera de línea, lo que le permite recuperar el estado del dispositivo independientemente de la ubicación física del dispositivo o el estado de uso. Los últimos datos de sucesos de un dispositivo se pueden recuperar para cualquier suceso específico que se ha producido hasta hace un máximo de 365 días.

### Almacenamiento de datos de sucesos de dispositivo

Los datos de sucesos de dispositivo del servicio de {{site.data.keyword.iot_short_notm}} se pueden almacenar para su uso posterior. El almacenamiento de datos es un primer paso esencial para realizar un análisis detallado de dichos datos.  Por ejemplo, puede realizar un seguimiento de los cambios durante periodos de tiempo más largos y almacenar conjuntos de datos que se utilizan con unas potentes herramientas de análisis, incluido el uso con las API de Watson y la informática cognitiva. Para obtener más información, consulte [conexión de un servicio historian de {{site.data.keyword.cloudant_short_notm}}](https://console.ng.bluemix.net/docs/services/IoT/cloudant_connector.html) o [conexión de un servicio historian de {{site.data.keyword.messagehub}}](https://console.ng.bluemix.net/docs/services/IoT/message_hub.html).

---

## Análisis
{: #analytics}

### Visualizar datos de dispositivos en tiempo real

Puede visualizar y mostrar datos de dispositivos en tiempo real utilizando tarjetas del panel de instrumentos. Las tarjetas del panel de instrumentos supervisan y muestran datos de dispositivos en tiempo real, lo que le permite realizar un seguimiento de los dispositivos clave o de los datos de dispositivos. Estas visualizaciones se muestran en el panel de instrumentos principal de {{site.data.keyword.iot_short_notm}} para darle acceso rápido al contexto y al estado de datos de dispositivos en tiempo real. Para obtener más información, consulte [visualización de datos en tiempo real](https://console.ng.bluemix.net/docs/services/IoT/data_visualization.html).

### Analíticas de extremo y de nube

Al utilizar cloud analytics de {{site.data.keyword.iot_short_notm}}, especifique condiciones de reglas basadas en datos de dispositivos en tiempo real y que activen alertas y acciones opcionales cuando se cumplan. Por ejemplo, puede crear una regla para asegurarse de que cuando el dispositivo se ha eliminado o cuando se dispara la temperatura del dispositivo, se envíe una alerta al panel de control del dispositivo de un usuario, y se envíe un correo electrónico al administrador. Para obtener más información, consulte la [documentación de analíticas de nube](https://console.ng.bluemix.net/docs/services/IoT/cloud_analytics.html).

Con las analíticas de extremo, mueva el proceso de desencadenamiento de reglas de analíticas desde la nube a una pasarela habilitada para analíticas de extremo que pueden reducir drásticamente la cantidad de tráfico de datos de dispositivo en la nube haciendo que el proceso de analíticas se cierre en el dispositivo. Para obtener más información, consulte la [documentación de analíticas de extremo](https://console.ng.bluemix.net/docs/services/IoT/edge_analytics.html).

---

## Gestión de riesgos
{: #risk_management}

### Conectividad y arquitectura seguras

La arquitectura del {{site.data.keyword.iot_short_notm}} está diseñada para evitar que los dispositivos suplanten a otros dispositivos, lo que mantiene la integridad de los datos de dispositivo. Los dispositivos se conectan con el {{site.data.keyword.iot_short_notm}} mediante una combinación de un ID de cliente y una señal de autenticación, que sólo conocerá usted. Una vez que se registren los dispositivos o que se generen claves de API, se añade sal y se aplica una función hash a la señal de autenticación para mantener la seguridad de las credenciales.

El complemento Risk and Security Management le permite mejorar la seguridad de {{site.data.keyword.iot_short_notm}} para asegurarse de que todos los puntos de conexión entre el servidor y los dispositivos se autentican con credenciales probadas. Con este complemento se utilizan certificados y autenticación TLS (seguridad de capa de transporte) sobre el uso de {{site.data.keyword.iot_short_notm}} de ID de usuario y señales. Durante la comunicación entre los dispositivos y el servidor, a cualquier dispositivo que no tenga certificados válidos con acceso al servidor, configurado en el complemento Risk and Security Management, se le deniega el acceso, aunque utilice ID de usuario y contraseñas válidos.

---
