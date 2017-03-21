---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Iniciación a Mobile Foundation
{: #gettingstartedtemplate}

{{site.data.keyword.mobilefoundation_long}} acelera la configuración de un entorno de {{site.data.keyword.mfp_full}} desde el cual puede desarrollar, probar y operar aplicaciones móviles de empresa. {{site.data.keyword.mobilefoundation_short}} está disponible bajo dos de servicio distintos: Developer y Professional 1 Application.
{:shortdesc}

<!-- The Professional 1 Application plan allows the {{site.data.keyword.mobilefoundation_short}} server to be deployed on a scalable container group.--> Utilizando el plan Professional 1 Application se puede gestionar una sola aplicación incorporada en una o todas las plataformas operativas soportadas como Android, iOS, Windows o Mobile Web. El plan Developer <!-- does not support {{site.data.keyword.mobilefoundation_short}} deployment on a container group with more than 1 node. This plan --> está pensado para entornos de desarrollo y pruebas.

## Iniciación al plan Mobile Foundation: Developer
{: #gettingstartedtemplate_dev}

Después de crear una instancia de {{site.data.keyword.mobilefoundation_short}}: Developer, puede empezar a crear el canal móvil en tan solo unas pulsaciones.

*	Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con la configuración predeterminada, pulse **Iniciar servidor básico**.

  `La instancia de servidor básico incluye un nodo y 1 GB de memoria.`

* Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con configuración avanzada para la topología, seguridad y otros tipos de configuración del servidor, pulse **Iniciar servidor con configuración avanzada**. Consulte [Ajuste de la configuración avanzada](c_using_mfs_p1.html#using_mfs_advanced_p1), para obtener más información.

## Iniciación al plan Mobile Foundation: Professional 1 Application
{: #gettingstartedtemplate_prof}

Después de crear una instancia del servicio {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application, puede empezar a crear el canal móvil realizando los pasos siguientes.

1.  Conéctese a un servicio de {{site.data.keyword.dashdbshort}} for Transactions existente en {{site.data.keyword.Bluemix_notm}}.

    1.  Seleccione la `Organización` de {{site.data.keyword.Bluemix_notm}} donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}.

    + Seleccione el `Espacio` de {{site.data.keyword.Bluemix_notm}} donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}, en la lista de espacios disponible en la `Organización` seleccionada.

    + Seleccione el `Nombre de servicio` y las `Credenciales` de {{site.data.keyword.dashdbshort_notm}} para conectarse con la instancia de servicio {{site.data.keyword.dashdbshort_notm}} existente.

    + Pruebe la conexión a la instancia de servicio de {{site.data.keyword.dashdbshort_notm}} for Transactions seleccionada pulsando **Probar conexión**.

    + Pulse **Añadir**, seguido de **Continuar** en la ventana emergente que le solicita información sobre el servicio de {{site.data.keyword.dashdbshort_notm}} for Transactions seleccionado. Esta acción crea las tablas necesarias en la instancia de servicio de base de datos de {{site.data.keyword.dashdbshort_notm}} configurada.

    **Nota:** Después de añadir una conexión {{site.data.keyword.dashdbshort_notm}} a la instancia {{site.data.keyword.mobilefoundation_short}} no podrá cambiarla.

2.  Cree e inicie el servidor.

    * Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con la configuración predeterminada, pulse **Iniciar servidor básico**.

      `La instancia de servidor básico incluye un nodo y 1 GB de memoria.`

    * Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con configuración avanzada para la topología, seguridad y otros tipos de configuración del servidor, pulse **Iniciar servidor con configuración avanzada**. Consulte [Ajuste de la configuración avanzada](c_using_mfs_p2.html#using_mfs_advanced_p2), para obtener más información.

## Iniciación al plan Mobile Foundation: Developer Pro
{: #gettingstartedtemplate_devpro}

Después de crear una instancia del servicio de {{site.data.keyword.mobilefoundation_short}}: Developer Pro, puede empezar a crear el canal móvil realizando los pasos siguientes.

  1.  Conéctese a un servicio de {{site.data.keyword.dashdbshort}} for Transactions existente en {{site.data.keyword.Bluemix_notm}}.

      1.  Seleccione la `Organización` de {{site.data.keyword.Bluemix_notm}} donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}.

      + Seleccione el `Espacio` de {{site.data.keyword.Bluemix_notm}} donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}, en la lista de espacios disponible en la `Organización` seleccionada.

      + Seleccione el `Nombre de servicio` y las `Credenciales` de {{site.data.keyword.dashdbshort_notm}} para conectarse con la instancia de servicio {{site.data.keyword.dashdbshort_notm}} existente.

      + Pruebe la conexión a la instancia de servicio de {{site.data.keyword.dashdbshort_notm}} for Transactions seleccionada pulsando **Probar conexión**.

      + Pulse **Añadir**, seguido de **Continuar** en la ventana emergente que le solicita información sobre el servicio de {{site.data.keyword.dashdbshort_notm}} for Transactions seleccionado. Esta acción crea las tablas necesarias en la instancia de servicio de base de datos de {{site.data.keyword.dashdbshort_notm}} configurada.

      **Nota:** Después de añadir una conexión {{site.data.keyword.dashdbshort_notm}} a la instancia {{site.data.keyword.mobilefoundation_short}} no podrá cambiarla.

  2.  Cree e inicie el servidor.

      * Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con la configuración predeterminada, pulse **Iniciar servidor básico**.

      * Esta selección suministra un {{site.data.keyword.mfserver_long_notm}} con la configuración siguiente:

          - Un nodo con 1 GB de memoria. Este tamaño es suficiente para realizar actividades de desarrollo, de pruebas no muy exigentes y cargas de trabajo de producción a pequeña escala.

          -	El `nombre de usuario` y la `contraseña` se generan de forma automática. Tiene acceso a ellos cuando el servidor está en ejecución.

      * Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con configuración avanzada para la topología, seguridad y otros tipos de configuración del servidor, pulse **Iniciar servidor con configuración avanzada**. Consulte [Ajuste de la configuración avanzada](c_using_mfs_p3.html#using_mfs_advanced_p3), para obtener más información.

## Iniciación al plan Mobile Foundation: Professional Per Capacity
{: #gettingstartedtemplate_profper}

Después de crear una instancia del servicio de {{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity, puede empezar a crear el canal móvil realizando los pasos siguientes.

  1.  Conéctese a un servicio de {{site.data.keyword.dashdbshort}} for Transactions existente en {{site.data.keyword.Bluemix_notm}}.

      1.  Seleccione la `Organización` de {{site.data.keyword.Bluemix_notm}} donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}.

      + Seleccione el `Espacio` de {{site.data.keyword.Bluemix_notm}} donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}, en la lista de espacios disponible en la `Organización` seleccionada.

      + Seleccione el `Nombre de servicio` y las `Credenciales` de {{site.data.keyword.dashdbshort_notm}} para conectarse con la instancia de servicio {{site.data.keyword.dashdbshort_notm}} existente.

      + Pruebe la conexión a la instancia de servicio de {{site.data.keyword.dashdbshort_notm}} for Transactions seleccionada pulsando **Probar conexión**.

      + Pulse **Añadir**, seguido de **Continuar** en la ventana emergente que le solicita información sobre el servicio de {{site.data.keyword.dashdbshort_notm}} for Transactions seleccionado. Esta acción crea las tablas necesarias en la instancia de servicio de base de datos de {{site.data.keyword.dashdbshort_notm}} configurada.

      **Nota:** Después de añadir una conexión {{site.data.keyword.dashdbshort_notm}} a la instancia {{site.data.keyword.mobilefoundation_short}} no podrá cambiarla.

  2.  Cree e inicie el servidor.

      * Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con la configuración predeterminada, pulse **Iniciar servidor básico**.

      * Esta selección suministra un {{site.data.keyword.mfserver_long_notm}} con la configuración siguiente:
          -  2 nodos con 1 GB de memoria cada uno. Este tamaño es correcto para realizar actividades de desarrollo, de pruebas no muy exigentes y cargas de trabajo de producción a pequeña escala.

          -	El `nombre de usuario` y la `contraseña` se generan de forma automática. Tiene acceso a ellos cuando el servidor está en ejecución.

      * Para crear una instancia de servidor de {{site.data.keyword.mobilefirst_notm}} con configuración avanzada para la topología, seguridad y otros tipos de configuración del servidor, pulse **Iniciar servidor con configuración avanzada**. Consulte [Ajuste de la configuración avanzada](c_using_mfs_p4.html#using_mfs_advanced_p4), para obtener más información.

Vaya a [Utilización del servicio Mobile Foundation para configurar el servidor de MobileFirst<!-- on IBM Containers--> ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/bluemix/using-mobile-foundation/){: new_window} para obtener más información sobre la iniciación a {{site.data.keyword.mobilefoundation_short}}.

##  Limitaciones conocidas
{: #knownlimitations_mfp}

* La IU del servicio {{site.data.keyword.mobilefoundation_short}} no utiliza el patrón específico del entorno local seleccionado por el usuario para mostrar números.


# Enlaces relacionados
{: #rellinks  notoc}

## Enlaces relacionados
{: #general notoc}

*	[Documentación del producto IBM MobileFirst Platform Foundation V8.0.0 ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform Developer Center ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobilefirstplatform.ibmcloud.com){: new_window}
