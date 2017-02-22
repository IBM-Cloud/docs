---

copyright:
  years: 2016, 2017
lastupdated:  "2017-01-17"

---

#	Utilización del plan Developer
{: #using_mobilefoundation_p1}

Después de crear la instancia de servicio {{site.data.keyword.mobilefoundation_short}}: Developer, en pocos segundos, puede acceder a la página `Visión general` en {{site.data.keyword.Bluemix_notm}}, que le ofrece guías de aprendizaje y vídeos para ayudarle a aprender a utilizar el servicio {{site.data.keyword.mobilefoundation_short}}.

## Inicio del servidor de {{site.data.keyword.mobilefirst}}
{: #start_mobilefoundation_p1}
* Para iniciar {{site.data.keyword.mfserver_short_notm}} con los valores predeterminados, pulse **Iniciar servidor básico**.

Esta selección suministra un {{site.data.keyword.mfserver_long_notm}} con la configuración siguiente:
*	1 GB de memoria. Este tamaño es suficiente para realizar actividades de desarrollo, de pruebas no muy exigentes y cargas de trabajo de producción a pequeña escala.

*	El `nombre de usuario` y la `contraseña` se generan de forma automática. Tiene acceso a ellos cuando el servidor está en ejecución.

Se inicia el proceso de suministro. Este proceso dura unos 10 minutos y un mensaje indica el progreso de la operación. Una vez finalizado, se muestra un panel de instrumentos en el que se puede ver lo siguiente:
*	El estado del servidor que se ejecuta (estado, tamaño).

*	La ruta creada para el servidor. Utilice esta ruta en su aplicación móvil para conectarse a {{site.data.keyword.mfserver_short_notm}}.

*	Su `nombre de usuario` y `contraseña` personal para acceder a la {{site.data.keyword.mfp_oc_short_notm}}. La `contraseña` está oculta. Pulse el icono **Mostrar contraseña** para visualizarla.

*	Pulse **Iniciar consola** para iniciar la {{site.data.keyword.mfp_oc_short_notm}}.


<!--This console runs inside the container.--> Con la consola, puede gestionar sus aplicaciones móviles y dispositivos móviles, utilizar su servidor como programa de fondo móvil, enviar notificaciones push, etc.

##  Adición de servidor de Mobile Analytics
{: #adding_analytics_server_dev}

 Ahora puede supervisar su aplicación móvil en el servidor de {{site.data.keyword.mobilefirst}} añadiendo un servidor de Mobile Analytics a la instancia de servicio de {{site.data.keyword.mobilefoundation_short}}. El plan Developer crea el servidor de Mobile Analytics en un grupo de contenedores con un nodo único que tiene 1 GB de memoria.

* Pulse **Añadir analíticas** para añadir el servidor de Mobile Analytics a la instancia de servicio de {{site.data.keyword.mobilefoundation_short}}.

Se inicia el proceso de suministro. Este proceso dura unos 10 minutos y un mensaje indica el progreso de la operación.  

* Inicie la consola de MobileFirst Analytics desde {{site.data.keyword.mfp_oc_short_notm}}.

* El inicio de sesión único está habilitado entre {{site.data.keyword.mfserver_short_notm}} y el servidor de Mobile Analytics. El servidor de Mobile Analytics está configurado con las mismas claves de LTPA y credenciales de usuario que {{site.data.keyword.mfserver_short_notm}}. Puede utilizar el mismo `nombre_usuario` y `contraseña` para iniciar sesión en la consola de Mobile Analytics como se solía iniciar sesión en {{site.data.keyword.mfp_oc_short_notm}}.

Para obtener más información sobre MobileFirst Analytics, puede consultar [MobileFirst Foundation Operational Analytics ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/analytics/ "Icono de enlace externo"){: new_window}.

**Nota:** El servidor de Mobile Analytics se elimina al suprimir la instancia de servicio de {{site.data.keyword.mobilefoundation_short}} o al intentar volver a crear {{site.data.keyword.mfserver_short_notm}}.

##  Supresión del servidor de Mobile Analytics
{: #deleting_analytics_server_dev}

Ahora puede suprimir el servidor de Mobile Analytics que se ha añadido a la instancia de servicio de {{site.data.keyword.mobilefoundation_short}}, desde el panel de instrumentos de servicio de {{site.data.keyword.mobilefoundation_short}}.

* Pulse **Suprimir Analytics** para suprimir el servidor de Mobile Analytics que se ha añadido a la instancia de servicio de {{site.data.keyword.mobilefoundation_short}}.

 Esto suprimirá el grupo de contenedores de análisis. El proceso de supresión de contenedores de análisis lleva unos 10 minutos. Puede renovar la pantalla para ver el estado actualizado. Una vez que se supriman los contenedores de análisis, se volverá a habilitar el botón **Añadir Analytics**, que puede utilizar para volver a añadir el servidor de Mobile Analytics si lo decide.


## Recreación del servidor de {{site.data.keyword.mobilefirst}}
{: #recreate_mobilefoundation_p1}

*	Pulse **Recrear** para volver a crear el servidor.

* Esta acción detiene el servidor existente y suprime los datos. Todos los datos del servidor móvil se pierden. Se crea una nueva instancia con una versión actualizada, si está disponible. Esta acción tarda unos minutos en completarse.

##	Ajuste de la configuración avanzada
{: #using_mfs_advanced_p1}

Utilice la opción **Iniciar servidor con configuración avanzada** en la página `Visión general` para crear el servidor con valores avanzados o personalizados. También puede actualizar los valores del servidor para personalizar su configuración desde el separador **Configuración**. {{site.data.keyword.mobilefoundation_short}} le ofrece acceso a algunos valores avanzados.

*	Desde el separador **Topología**, puede seleccionar el tamaño del servidor y el número de instancias que necesita. El valor predeterminado del servidor es de 1 GB, que es suficiente para el desarrollo y la realización de pruebas no muy exigentes.

  - Seleccione el tamaño correcto para su servidor en función de sus necesidades.

* **Nodos** muestra el número de nodos que se han creado. Este campo no es editable en
{{site.data.keyword.mobilefoundation_short}}: Developer. El número de nodos <!--in your {{site.data.keyword.IBM_notm}} container group--> toma el valor predeterminado de **1** en el plan Developer.

Consulte la [documentación de {{site.data.keyword.mobilefoundation_long}} ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html "Icono de enlace externo"){: new_window} para obtener más detalles.
