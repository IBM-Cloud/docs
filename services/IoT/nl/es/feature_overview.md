---

copyright:
  years: 2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visión general de característica de {{site.data.keyword.iot_short_notm}}
{: #feature_overview}

Última actualización: 29 de junio de 2016
{: .last-updated}

El {{site.data.keyword.iot_full}} se crea en las siguientes áreas clave:

  1. Conexión: Conectar dispositivos y desarrollar aplicaciones.
  2. Gestión de información: Almacenar y revisar datos de dispositivos e integrar el {{site.data.keyword.iot_short_notm}} con otros servicios.
  3. Analíticas: Visualizar datos de dispositivos en tiempo real utilizando el panel de instrumentos {{site.data.keyword.iot_short_notm}}.
  4. Gestión de riesgos: Configurar la conectividad y la arquitectura seguras con control de acceso para usuarios y aplicaciones.

## Conectar
{: #connect}

{{site.data.keyword.iot_short_notm}} Connect es el punto de partida para cualquier servicio de {{site.data.keyword.iot_short_notm}}. La conexión de dispositivos, la creación de aplicaciones, el control de los dispositivos y la interacción con servicios de terceros están disponibles en Conectar {{site.data.keyword.iot_short_notm}}.

### Dispositivos de pasarela

Al utilizar una pasarela, puede conectar dispositivos al {{site.data.keyword.iot_short_notm}} que, de lo contrario, no se podrían conectar a Internet. Los dispositivos de pasarela combinan la función de un dispositivo y de una aplicación. Las pasarelas pueden recibir mandatos y enviar datos de dispositivo de la misma manera que un dispositivo, pero también pueden enviar mandatos a otros dispositivos a los que están conectados, de la misma forma que lo puede hacer una aplicación.

Los dispositivos que no se pueden conectar directamente a Internet se pueden conectar a un dispositivo de pasarela, y sus datos de dispositivo se pueden enviar al dispositivo de pasarela, que se podrá enviar al servicio de {{site.data.keyword.iot_short_notm}}.

### Gestión de dispositivos

Las funciones de gestión de dispositivos se proporcionan a través de la combinación de una API de gestión de dispositivos y un agente de gestión de dispositivos instalado en dispositivos. Los dispositivos gestionados pueden realizar acciones de gestión de dispositivos, que se pueden desencadenar mediante el panel de instrumentos de {{site.data.keyword.iot_short_notm}} principal.

La gestión de dispositivos le proporciona la posibilidad de rearrancar, descargar e instalar actualizaciones de firmware y restablecer dispositivos a los parámetros de fábrica de forma remota, todo desde dentro de la interfaz de usuario de {{site.data.keyword.iot_short_notm}}.

### Integraciones de servicios de terceros

La integración de servicio de terceros se crea en {{site.data.keyword.iot_short_notm}}, incluido el soporte para los servicios de ubicación meteorológica de The Weather Company, que le permite encontrar la información meteorológica actual en una ubicación de dispositivo.

---

## Gestión de la información
{: #information_management}

{{site.data.keyword.iot_short_notm}} Information Management controla los datos que envían los dispositivos después de alcanzar el servicio de {{site.data.keyword.iot_short_notm}}. La gestión de información incluye el almacenamiento y la transformación de datos.

### Memoria caché de sucesos del último dispositivo

Al utilizar la {{site.data.keyword.iot_short_notm}} Last Event Cache API, puede recuperar el último suceso que ha enviado un dispositivo. Esto funciona si el dispositivo está en línea o fuera de línea, lo que le permite recuperar el estado del dispositivo independientemente de la ubicación física del dispositivo o el estado de uso. Los últimos datos de sucesos de un dispositivo se pueden recuperar para cualquier suceso específico que se ha producido hasta hace un máximo de 365 días.

### Almacenamiento de datos de sucesos de dispositivo

Los datos de sucesos de dispositivo del servicio de {{site.data.keyword.iot_short_notm}} se pueden almacenar para su uso posterior. El almacenamiento de datos es un primer paso esencial para realizar un análisis detallado de dichos datos. Por ejemplo, puede realizar un seguimiento de los cambios durante periodos de tiempo más largos y almacenar conjuntos de datos que se utilizan con unas potentes herramientas de análisis, incluido el uso con las Watson API y el cálculo cognitivo.

---

## Análisis
{: #analytics}

### Visualizar datos de dispositivos en tiempo real

Puede visualizar y mostrar datos de dispositivos en tiempo real utilizando tarjetas del panel de instrumentos. Las tarjetas del panel de instrumentos supervisan y muestran datos de dispositivos en tiempo real, lo que le permite realizar un seguimiento de los dispositivos clave o de los datos de dispositivos. Estas visualizaciones se muestran en el panel de instrumentos principal de {{site.data.keyword.iot_short_notm}} para darle acceso rápido al contexto y al estado de datos de dispositivos en tiempo real.

---

## Gestión de riesgos
{: #risk_management}

### Conectividad y arquitectura seguras

La arquitectura del {{site.data.keyword.iot_short_notm}} está diseñada para evitar que los dispositivos suplanten a otros dispositivos, lo que mantiene la integridad de los datos de dispositivo. Los dispositivos se conectan con el {{site.data.keyword.iot_short_notm}} mediante una combinación de un ID de cliente y una señal de autenticación, que sólo conocerá usted. Una vez que se registren los dispositivos o que se generen claves de API, se añade sal y se aplica una función hash a la señal de autenticación para mantener la seguridad de las credenciales. La conectividad sobre TLS v1.2 está totalmente soportada.

---
