---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Iniciación a {{site.data.keyword.mobilefoundation_short}}
{: #gettingstartedtemplate}

Última actualización: 03 de agosto de 2016
{: .last-updated}

{{site.data.keyword.mobilefoundation_long}} acelera la configuración de un entorno de {{site.data.keyword.mfp_full}} desde el cual puede desarrollar, probar y operar aplicaciones móviles de empresa. {{site.data.keyword.mobilefoundation_short}} está disponible bajo dos de servicio distintos: Desarrollador y Aplicación profesional 1.
{:shortdesc}

<!-- The Professional 1 Application plan allows the {{site.data.keyword.mobilefoundation_short}} server to be deployed on a scalable container group.--> Utilizando el plan de aplicación Profesional 1 se puede gestionar una sola aplicación incorporada en una o todas las plataformas operativas soportadas como Android, iOS, Windows o Mobile Web. El plan de desarrollador <!-- does not support {{site.data.keyword.mobilefoundation_short}} deployment on a container group with more than 1 node. This plan --> está pensado para entornos de desarrollo y pruebas.

## Iniciación a {{site.data.keyword.mobilefoundation_short}}: Plan de desarrollador

Después de crear una instancia de {{site.data.keyword.mobilefoundation_short}}: Desarrollador, puede empezar a crear el canal móvil en tan solo unas pulsaciones. 

*	Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con la configuración predeterminada, pulse **Iniciar servidor básico**. 

  `La instancia de servidor básico incluye un nodo y 1 GB de memoria.`

* Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con configuración avanzada para la topología, seguridad y otros tipos de configuración del servidor, pulse **Iniciar servidor con configuración avanzada**. Consulte [Ajuste de la configuración avanzada](c_using_mfs_p1.html#using_mfs_advanced_p1), para obtener más información.

## Iniciación a {{site.data.keyword.mobilefoundation_short}}: Plan de aplicación Profesional 1

Después de crear una instancia del servicio {{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1, puede empezar a crear el canal móvil realizando los pasos siguientes.

1.  Conéctese a un servicio {{site.data.keyword.dashdbshort}}: Transacciones empresariales en {{site.data.keyword.Bluemix_notm}}. 

    1.  Seleccione la {{site.data.keyword.Bluemix_notm}} `Organización` donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}.

    + Seleccione el {{site.data.keyword.Bluemix_notm}} `Espacio` donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}, en la lista de espacios disponible en la `Organización` seleccionada.

    + Seleccione el {{site.data.keyword.dashdbshort_notm}} `Nombre de servicio` y las `Credenciales` para conectarse con la instancia de servicio de {{site.data.keyword.dashdbshort_notm}} existente.

    + Pruebe la conexión con la instancia del servicio {{site.data.keyword.dashdbshort_notm}}: Transacciones empresariales seleccionada pulsando **Probar conexión**. 

    + Pulse **Añadir**, seguido de **Continuar** en la ventana emergente que le solicita información sobre el servicio de {{site.data.keyword.dashdbshort_notm}} seleccionado. Esta acción crea las tablas necesarias en la instancia de servicio de base de datos de {{site.data.keyword.dashdbshort_notm}} configurada.

    **Nota:** Después de añadir una conexión {{site.data.keyword.dashdbshort_notm}} a la instancia {{site.data.keyword.mobilefoundation_short}} no podrá cambiarla.

2.  Cree e inicie el servidor.

    * Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con la configuración predeterminada, pulse **Iniciar servidor básico**. 

      `La instancia de servidor básico incluye un nodo y 1 GB de memoria.`

    * Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con configuración avanzada para la topología, seguridad y otros tipos de configuración del servidor, pulse **Iniciar servidor con configuración avanzada**. Consulte [Ajuste de la configuración avanzada](c_using_mfs_p2.html#using_mfs_advanced_p2), para obtener más información.

Vaya a [Utilización del servicio Mobile Foundation para configurar el servidor de MobileFirst<!-- on IBM Containers-->](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibm-containers/using-mobile-foundation/) Para obtener más información sobre cómo empezar a trabajar con {{site.data.keyword.mobilefoundation_short}}.


# Enlaces relacionados
{: #rellinks}

## Enlaces relacionados
{: #general}

*	[Documentación del producto de IBM MobileFirst Platform Foundation V8.0.0](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center](https://mobilefirstplatform.ibmcloud.com){: new_window}
