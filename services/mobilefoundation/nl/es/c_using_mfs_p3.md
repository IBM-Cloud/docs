---

copyright:
  years: 2016, 2017
lastupdated:  "2017-02-17"

---

#	Utilización del plan Developer Pro
{: #using_mobilefoundation_p3}

{{site.data.keyword.mobilefoundation_short}}: Developer Pro es adecuado para el desarrollo en equipo y pruebas; este plan no es adecuado para producción.

Después de crear la instancia de servicio {{site.data.keyword.mobilefoundation_short}}: Developer Pro, en pocos segundos, puede acceder a la página `Visión general` en {{site.data.keyword.Bluemix_notm}}, que le ofrece guías de aprendizaje y vídeos para ayudarle a aprender a utilizar el servicio {{site.data.keyword.mobilefoundation_short}}.

## Requisitos previos
{: #prerequisites_p3}

Tenga en cuenta lo siguiente antes de configurar la instancia del servicio {{site.data.keyword.mobilefoundation_short}}: Developer Pro.
* {{site.data.keyword.mobilefoundation_short}}: Developer Pro solo se admite con planes de {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional (con soporte para OLTP).

* Deberá tener acceso a las credenciales de la instancia de servicio {{site.data.keyword.dashdbshort_notm}} antes de poder configurar los valores de su instancia de servicio {{site.data.keyword.mobilefoundation_short}}.

**Nota**: La instancia de servicio {{site.data.keyword.dashdbshort_notm}} puede existir en cualquier `Espacio` dentro de la `Organización` de {{site.data.keyword.Bluemix_notm}} o de cualquier otra `Organización` a la que tenga acceso. Asegúrese de que dispone de los permisos para acceder al `Espacio` donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}.


## Adición de la conexión de base de datos
{: #configure_dashdb_p3}

###  Primeros pasos
{: #firststeps_p3}

Tras crear la instancia del servicio {{site.data.keyword.mobilefoundation_short}}: Developer Pro, siga el procedimiento para iniciarse en el uso del servicio.

### Configuración de la conexión con la instancia de servicio dashDB
{: #connect_dashdb_p3}

Una vez que se haya creado la instancia de servicio de {{site.data.keyword.mobilefoundation_short}}: Developer Pro, verá la página *Visión general*, donde deberá especificar la información de conexión de la instancia de servicio de {{site.data.keyword.dashdbshort_notm}} for Transactions, a la que se debe conectar la instancia de servicio de {{site.data.keyword.mobilefoundation_short}}.

**Nota:** Si ya tiene una instancia de servicio {{site.data.keyword.dashdbshort_notm}} for Analytics: Enterprise for Transactions, puede configurarla para utilizar lo mismo para conectarse a la instancia de servicio de {{site.data.keyword.mobilefoundation_short}}.

También puede crear una nueva instancia de servicio de {{site.data.keyword.dashdbshort_notm}} for Transactions, si aún no tiene ninguna existente.

Siga estos pasos para crear una nueva instancia de servicio de dashDB for Transactions:

1. En la página *Visión general*, seleccione la sección **Crear nuevo servicio**.

+ Seleccione `Sí` en la opción **Configuración de alta disponibilidad**, si desea una instancia de servicio altamente disponible de {{site.data.keyword.dashdbshort_notm}} for Transactions.

+ Revise los detalles del plan y pulse **Crear**.

Se ha creado una nueva instancia de servicio de {{site.data.keyword.dashdbshort_notm}} for Transactions: EnterpriseForTransactions2.8.500, que proporciona una instancia dedicada de {{site.data.keyword.dashdbshort_notm}} con RAM de 8 GB y 2 vCPUs, y 500 GB de almacenamiento.

Siga estos pasos para conectarse a una instancia de servicio existente de {{site.data.keyword.dashdbshort_notm}} o a la instancia de servicio de {{site.data.keyword.dashdbshort_notm}} for Transactions que acaba de crear:

1. Seleccione la `Organización` de {{site.data.keyword.Bluemix_notm}} donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}.

+ Seleccione el `Espacio` de {{site.data.keyword.Bluemix_notm}} donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}, en la lista de espacios disponible en la `Organización` seleccionada.   
**Nota:** Si no ve la `Organización` y el `Espacio` donde existe su instancia del servicio {{site.data.keyword.dashdbshort_notm}} consulte si es miembro de la `Organización` y del `Espacio`. Se requiere el rol de *Desarrollador* para acceder a la organización y al espacio, ya que el servicio de {{site.data.keyword.mobilefoundation_short}} accede a las credenciales desde el servicio de {{site.data.keyword.dashdbshort_notm}}.

+ Seleccione el `Nombre de servicio` y las `Credenciales` de {{site.data.keyword.dashdbshort_notm}} para conectarse con la instancia de servicio {{site.data.keyword.dashdbshort_notm}} existente.

+  Pruebe la conexión a la instancia de servicio especificada de {{site.data.keyword.dashdbshort_notm}}.

+  Pulse **Añadir**. Esta acción crea las tablas necesarias en la instancia de servicio de base de datos de {{site.data.keyword.dashdbshort_notm}} configurada.

En varios segundos, puede acceder a la página `Visión general`, que le ofrece guías de aprendizaje y vídeos para ayudarle a aprender a utilizar el servicio {{site.data.keyword.mobilefoundation_short}}.

**Nota**: no puede cambiar la instancia de servicio {{site.data.keyword.dashdbshort_notm}} que está configurada para que la utilice la instancia del servicio {{site.data.keyword.mobilefoundation_short}}. No obstante, puede utilizar la misma instancia de servicio {{site.data.keyword.dashdbshort_notm}} en varias instancias de servicio {{site.data.keyword.mobilefoundation_short}}, ya que cada instancia de servicio {{site.data.keyword.mobilefoundation_short}} crea su propio esquema en la instancia de servicio {{site.data.keyword.dashdbshort_notm}} seleccionada.

## Inicio del servidor de MobileFirst
{: #start_mobilefoundation_p3}

* Para iniciar {{site.data.keyword.mfserver_short_notm}} con los valores predeterminados, pulse **Iniciar servidor básico**.

* Esta selección suministra un {{site.data.keyword.mfserver_long_notm}} con la configuración siguiente:
    - Un nodo con 1 GB de memoria. Este tamaño es suficiente para realizar actividades de desarrollo, de pruebas no muy exigentes y cargas de trabajo de producción a pequeña escala.

    -	El `nombre de usuario` y la `contraseña` se generan de forma automática. Tiene acceso a ellos cuando el servidor está en ejecución.

Se inicia el proceso de suministro del servidor. Este proceso dura unos 10 minutos y un mensaje indica el progreso de la operación. Una vez finalizado, se muestra un panel de instrumentos en el que se puede ver lo siguiente:

  -	El estado del servidor que se ejecuta (estado, tamaño).

  -	Se ha creado la ruta para el servidor. Utilice esta ruta en su aplicación móvil para conectarse a {{site.data.keyword.mfserver_short_notm}}.

  -	Su `nombre de usuario` y `contraseña` personal para acceder a la {{site.data.keyword.mfp_oc_short_notm}}. La `contraseña` está oculta. Pulse el icono **Mostrar contraseña** para visualizarla.

*	Pulse **Iniciar consola** para abrir la {{site.data.keyword.mfp_oc_short_notm}}.


<!--This console runs inside the container.--> Con la consola, puede gestionar sus aplicaciones móviles, adaptadores y dispositivos móviles, utilizar su servidor como programa de fondo móvil, enviar notificaciones push, etc.

##  Adición de servidor de Mobile Analytics
{: #adding_analytics_server_p3}

 Ahora puede supervisar su aplicación móvil en el servidor de {{site.data.keyword.mobilefirst}} añadiendo un servidor de Mobile Analytics a la instancia de servicio de {{site.data.keyword.mobilefoundation_short}}.

 El plan Developer Pro crea el servidor de Mobile Analytics en un grupo de contenedores, el usuario puede personalizar la configuración seleccionando el número de nodos de contenedores en el grupo de contenedores.

 Los usuarios también pueden adjuntar volúmenes a los contenedores para persistir datos. El volumen seleccionado no se puede cambiar. 20 GB es el espacio de compartición de archivos predeterminado disponible para el usuario. Si el usuario necesita espacio de almacenamiento adicional para persistir datos analíticos, necesitará adquirir compartición de archivos adicional y crear un volumen utilizando esta compartición de archivos. Puede seleccionar este nuevo volumen al desplegar el servidor de análisis.

 Para obtener más información sobre cómo añadir volúmenes a {{site.data.keyword.containerlong}}, consulte [Almacenamiento de datos permanentes en un volumen mediante el Panel de control de {{site.data.keyword.Bluemix_notm}} ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://console.ng.bluemix.net/docs/containers/container_volumes_ui.html){: new_window}.

* Pulse **Añadir analíticas** para añadir el servidor de Mobile Analytics a la instancia de servicio de {{site.data.keyword.mobilefoundation_short}}.

* Puede elegir la configuración del servidor de Mobile Analytics, se admite un mínimo de 1 GB y un máximo de 2 GB de memoria para la configuración del servidor de Mobile Analytics. En este plan, el servidor de Mobile Analytics solo admite un único nodo.

Se inicia el proceso de suministro. Este proceso dura unos 10 minutos y un mensaje indica el progreso de la operación.  

* Inicie la consola de MobileFirst Analytics desde {{site.data.keyword.mfp_oc_short_notm}}.

* El inicio de sesión único está habilitado entre {{site.data.keyword.mfserver_short_notm}} y el servidor de Mobile Analytics. El servidor de Mobile Analytics está configurado con las mismas claves de LTPA y credenciales de usuario que {{site.data.keyword.mfserver_short_notm}}. Puede utilizar el mismo `nombre_usuario` y `contraseña` para iniciar sesión en la consola de Mobile Analytics como se solía iniciar sesión en {{site.data.keyword.mfp_oc_short_notm}}.

Para obtener más información sobre MobileFirst Analytics, puede consultar [MobileFirst Foundation Operational Analytics ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/){: new_window}.

**Nota:** El servidor de Mobile Analytics se elimina al suprimir la instancia de servicio de {{site.data.keyword.mobilefoundation_short}} o al intentar volver a crear {{site.data.keyword.mfserver_short_notm}}.

##  Supresión del servidor de Mobile Analytics
{: #deleting_analytics_server_p3}

Ahora puede suprimir el servidor de Mobile Analytics que se ha añadido a la instancia de servicio de {{site.data.keyword.mobilefoundation_short}}, desde el panel de instrumentos de servicio de {{site.data.keyword.mobilefoundation_short}}.

* Pulse **Suprimir Analytics** para suprimir el servidor de Mobile Analytics que se ha añadido a la instancia de servicio de {{site.data.keyword.mobilefoundation_short}}.

 Esto suprimirá el grupo de contenedores de análisis. El proceso de supresión de contenedores de análisis lleva unos 10 minutos. Puede renovar la pantalla para ver el estado actualizado. Una vez que se supriman los contenedores de análisis, se volverá a habilitar el botón **Añadir Analytics**, que puede utilizar para volver a añadir el servidor de Mobile Analytics si lo decide.

## Recreación del servidor de MobileFirst
{: #recreate_mobilefoundation_p3}

*	Pulse **Recrear** para volver a crear el servidor.

* Esta acción detiene el servidor existente y suprime los datos. Se crea una nueva instancia con una versión actualizada, si está disponible. Esta acción tarda unos minutos en completarse.

**Nota**: todos los datos de su instancia de servidor anterior, incluyendo la información sobre aplicaciones y adaptadores, se conserva en la instancia del servicio {{site.data.keyword.dashdbshort_notm}} configurada; estos datos se utilizan para volver a crear el servidor.

##	Ajuste de la configuración avanzada
{: #using_mfs_advanced_p3}

Utilice la opción **Iniciar servidor con configuración avanzada** en la página `Visión general` para crear el servidor con valores avanzados o personalizados. También puede actualizar los valores del servidor para personalizar su configuración desde el separador **Configuración**. {{site.data.keyword.mobilefoundation_short}} le ofrece acceso a algunos valores avanzados.

*	Desde el separador **Topología**, puede seleccionar el tamaño del servidor y la memoria que necesita. El servidor predeterminado se crea con 1 GB de memoria.
  - Puede cambiar la memoria de su servidor en función de sus necesidades a un máximo de 2 GB.

  - **Nodos** muestra el número de nodos que se han creado. Este campo no se puede editar en {{site.data.keyword.mobilefoundation_short}}: Developer. De forma predeterminada, el número de nodos <!--in your {{site.data.keyword.IBM_notm}} container group--> es **1** en el plan Developer.

Consulte la [documentación de {{site.data.keyword.mobilefoundation_long}} ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}, para obtener más detalles.
