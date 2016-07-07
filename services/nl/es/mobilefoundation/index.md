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

*Última actualización: 15 de junio de 2016*
{: .last-updated}

{{site.data.keyword.mobilefoundation_long}} acelera la configuración de un entorno de
{{site.data.keyword.mfp_full}} desde el cual puede desarrollar, probar y operar aplicaciones móviles de empresa. {{site.data.keyword.mobilefoundation_short}} está disponible bajo dos de servicio distintos: Desarrollador y Aplicación profesional 1.
{:shortdesc}

El plan de Aplicación profesional 1 permite desplegar el servidor
de {{site.data.keyword.mobilefoundation_short}} en un grupo de contenedores escalable.
Utilizando el plan de aplicación Profesional 1 se puede gestionar una sola aplicación incorporada en una o todas las plataformas operativas soportadas como Android, iOS, Windows o Mobile Web. El plan Desarrollador no da soporte al despliegue de {{site.data.keyword.mobilefoundation_short}} en un grupo de contenedores con más de 1 nodo. Este plan está pensado para entornos de desarrollo y pruebas.

## Iniciación a {{site.data.keyword.mobilefoundation_short}}: Plan de desarrollador

Después de crear una instancia de {{site.data.keyword.mobilefoundation_short}}: Desarrollador, puede empezar a crear el canal móvil en tan solo unas pulsaciones. 

*	Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con la configuración predeterminada, pulse
**Iniciar servidor básico**.

  `La instancia de servidor básico incluye un nodo, 1 GB de memoria y 64 GB de capacidad de almacenamiento. `

* Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con configuración avanzada para la topología, seguridad y otros tipos de configuración del servidor, pulse
**Iniciar servidor con configuración avanzada**. Consulte [Ajuste de la configuración avanzada](c_using_mfs_p1.html#using_mfs_advanced_p1), para obtener más información.

## Iniciación a {{site.data.keyword.mobilefoundation_short}}: Plan de aplicación Profesional 1

Después de crear una instancia del servicio {{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1, puede empezar a crear el canal móvil realizando los pasos siguientes.

1.  Conéctese a un servicio {{site.data.keyword.dashdbshort}}: Transacciones empresariales en
{{site.data.keyword.Bluemix_notm}}.

    1.  Seleccione el {{site.data.keyword.Bluemix_notm}} `Espacio` donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}, en la lista de espacios disponible en la `Organización` actual.

    2.  Seleccione el {{site.data.keyword.dashdbshort_notm}} `Nombre de servicio` y las `Credenciales` para conectarse con la instancia de servicio de {{site.data.keyword.dashdbshort_notm}} existente.

    3.  Pruebe la conexión con la instancia del servicio {{site.data.keyword.dashdbshort_notm}}: Transacciones empresariales seleccionada pulsando **Probar conexión**. 

    4.  Pulse **Añadir**, seguido de **Continuar** en la ventana emergente que le solicita información sobre el servicio de {{site.data.keyword.dashdbshort_notm}} seleccionado. Esta acción crea las tablas necesarias en la instancia de servicio de base de datos de {{site.data.keyword.dashdbshort_notm}} configurada.

2.  Cree e inicie el servidor.

    * Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con la configuración predeterminada, pulse
**Iniciar servidor básico**.

      `La instancia de servidor básico incluye un nodo, 1 GB de memoria y 64 GB de capacidad de almacenamiento. `

    * Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con configuración avanzada para la topología, seguridad y otros tipos de configuración del servidor, pulse
**Iniciar servidor con configuración avanzada**. Consulte [Ajuste de la configuración avanzada](c_using_mfs_p2.html#using_mfs_advanced_p2), para obtener más información.

Vaya a [Utilización del servicio Mobile Foundation para configurar el servidor de MobileFirst en IBM Containers](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibm-containers/using-mobile-foundation/) para obtener más información sobre la iniciación a
{{site.data.keyword.mobilefoundation_short}}.

# Enlaces relacionados
{: #rellinks}

## Enlaces relacionados
{: #general}

*	[Documentación del producto de IBM MobileFirst Platform Foundation V8.0.0](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center](https://mobilefirstplatform.ibmcloud.com){: new_window}
