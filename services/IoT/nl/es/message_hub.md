---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Conexión y configuración de un servicio de historian mediante {{site.data.keyword.messagehub}}  
{: #messagehub_main}

La conexión de {{site.data.keyword.messagehub_full}} a {{site.data.keyword.iot_short}} proporciona un bus de mensajes escalable de alto rendimiento para el almacenamiento de datos históricos. {{site.data.keyword.messagehub}} se crea en Apache Kafka, que es un sistema de mensajería de alto rendimiento de código abierto que proporciona una plataforma de baja latencia para manejar canales de información de datos en tiempo real.

## Antes de empezar  
{: #byb}

Antes de conectar un {{site.data.keyword.messagehub}} al servicio de {{site.data.keyword.iot_short}}, lleve a cabo las tareas siguientes:

- Configure {{site.data.keyword.messagehub}} en el mismo espacio de {{site.data.keyword.Bluemix_notm}} como su {{site.data.keyword.iot_short_notm}} utilizando el Catálogo de {{site.data.keyword.Bluemix_notm}}. Para obtener más información sobre {{site.data.keyword.messagehub}}, consulte el [Iniciación a {{site.data.keyword.messagehub}}](https://console.{DomainName}/docs/services/MessageHub/index.html).

- Asegúrese de que tenga privilegios de desarrollador en la organización de {{site.data.keyword.Bluemix_notm}} y de que haya iniciado sesión mediante {{site.data.keyword.Bluemix_notm}}. Si no ha iniciado sesión a través de {{site.data.keyword.Bluemix_notm}}, o no tiene privilegios de desarrollador en esta organización de {{site.data.keyword.Bluemix_notm}}, no podrá autorizar el enlace de {{site.data.keyword.messagehub}} y {{site.data.keyword.iot_short_notm}}.

## Conectar

Para conectar {{site.data.keyword.messagehub}} para el almacenamiento de datos históricos:

1. En el panel de control de {{site.data.keyword.iot_short}}, pulse **Extensiones** en la barra de navegación.
2. En el mosaico Almacenamiento de datos históricos, pulse **Configuración**.
4. Seleccione el servicio de {{site.data.keyword.messagehub}} al que se desea conectar.  
Todos los servicios disponibles de {{site.data.keyword.messagehub}} del mismo espacio de {{site.data.keyword.Bluemix_notm}} que el servicio de {{site.data.keyword.iot_short}} se listan en la sección Configurar el almacenamiento de datos históricos.
5. Seleccione las opciones de configuración de {{site.data.keyword.messagehub}}:
 1. Seleccione un huso horario.  
 Las indicaciones de fecha y hora en los datos del dispositivo que se envían al {{site.data.keyword.messagehub}} se convierten al huso horario seleccionado.
 2. Seleccione un tema predeterminado.  
 Los sucesos de dispositivos se envían al tema predeterminado si hay uno definido aquí. Para utilizar las asignaciones de temas más granulares, deje el tema predeterminado en blanco y añada reglas de envío personalizadas.
 3. Opcional: Especifique las reglas de envío personalizadas.  
 Especifique reglas adicionales para el reenvío de sucesos de dispositivo. Sólo se reenviarán los sucesos que coincidan con las reglas de reenvío personalizadas.  
 **Nota:** Un suceso puede coincidir con varias reglas de envío y se pueden reenviar a varios temas de {{site.data.keyword.messagehub}}.
 4. Opcional: Configurar temas.  
 Para crear los temas con más de las dos particiones predeterminadas, puede especificar la configuración de partición.
 5. Pulse **Listo**.
5. Pulse en **Autorizar**.
6. En el recuadro de diálogo Autorización, pulse **Confirmar**.

Sus datos de dispositivo ahora están almacenados en el {{site.data.keyword.messagehub}}.
