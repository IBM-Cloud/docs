---

copyright:
  years: 2016

---

#	Utilización de {{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1
{: #using_mobilefoundation_p2}


Tras crear la instancia del servicio {{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1, consulte el procedimiento siguiente para iniciarse en el uso del servicio. 

## Requisitos previos
{: #prerequisites_p2}

Tenga en cuenta lo siguiente antes de configurar la instancia del servicio
{{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1. 
* {{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1 solo se admite con planes de {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dashdbshort_notm}}: Transacciones empresariales (con soporte para OLTP). 

* La instancia de servicio {{site.data.keyword.dashdbshort_notm}} y sus credenciales deben estar disponibles para poder configurar los valores de su instancia de servicio {{site.data.keyword.mobilefoundation_short}}. 

**Nota**: la instancia de servicio {{site.data.keyword.dashdbshort_notm}} puede existir en cualquier
*Espacio* dentro de la *Organización* de {{site.data.keyword.Bluemix_notm}}.   

## Configuración de la instancia de servicio {{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1
{: #configure_dashdb_p2}

###  Primeros pasos
{: #firststeps_p2}

Tras la creación de la instancia de servicio {{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1, realice los pasos siguientes para iniciarse en el uso del servicio: 

* Acepte los términos de la licencia para {{site.data.keyword.mfp_full_notm}} V8.0.0.0.

* Especifique sus credenciales de {{site.data.keyword.Bluemix_notm}}. Al hacer esto, autoriza al servicio para que pueda realizar cambios en su espacio de {{site.data.keyword.Bluemix_notm}} y crear {{site.data.keyword.containerlong}} que aloja su servidor de
{{site.data.keyword.mobilefirst_notm}}. 


### Configuración de la conexión con la instancia de servicio {{site.data.keyword.dashdbshort_notm}}
{: #connect_dashdb_p2}

Una vez que se haya creado la instancia de servicio {{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1, podrá ver la página *Visión general*, donde deberá especificar la información de conexión de la instancia de servicio
{{site.data.keyword.dashdbshort_notm}}: Transacciones empresariales. 

* Especifique la **Organización** y el **Espacio** de {{site.data.keyword.Bluemix_notm}} donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}: Transacciones empresariales. 
* Elija el **Nombre de servicio** de la instancia del servicio {{site.data.keyword.dashdbshort_notm}} que desee utilizar con la instancia del servicio {{site.data.keyword.mobilefoundation_short}} en el menú desplegable, si ha creado más de una instancia de servicio {{site.data.keyword.dashdbshort_notm}}. 
* Seleccione las **Credenciales** para la instancia de servicio {{site.data.keyword.dashdbshort_notm}} seleccionada. 

* Pulse **Probar conexión** para verificar que la instancia de servicio {{site.data.keyword.dashdbshort_notm}} está disponible y pulse **Guardar**. 

**Nota**: no podrá cambiar esta instancia de servicio {{site.data.keyword.dashdbshort_notm}} que está configurada para que la utilice la instancia del servicio {{site.data.keyword.mobilefoundation_short}}. No obstante, podrá utilizar la misma instancia de servicio
{{site.data.keyword.dashdbshort_notm}} en varias instancias de servicio {{site.data.keyword.mobilefoundation_short}}, ya que cada instancia de servicio {{site.data.keyword.mobilefoundation_short}} creará su propio esquema en la instancia de servicio
{{site.data.keyword.dashdbshort_notm}} seleccionada. 

* Después de varios segundos, puede acceder a la página *Visión general*, que le ofrece guías de aprendizaje y vídeos para ayudarle a aprender a utilizar el servicio {{site.data.keyword.mobilefoundation_short}}. 

### Inicio del servidor de {{site.data.keyword.mobilefirst}}
{: #start_mobilefoundation_p2}

* Para iniciar {{site.data.keyword.mfserver_short_notm}} con los valores predeterminados, pulse **Iniciar servidor básico**.

![Iniciar servidor básico](images/start_basic_server.png "Figura 1. Iniciar servidor básico")
{: screen}
* Esta selección suministra un {{site.data.keyword.mfserver_long_notm}} con la configuración siguiente: 
    -  1 GB de memoria y 64 GB de almacenamiento. Este tamaño es suficiente para realizar actividades de desarrollo y de pruebas no muy exigentes. 

    -	El *nombre de usuario* y la *contraseña* se generan de forma automática. Tiene acceso a ellos cuando el servidor está en ejecución.

Se inicia el proceso de suministro del servidor. Este proceso dura unos 10 minutos y un mensaje indica el progreso de la operación. Una vez finalizado, se muestra un panel de instrumentos en el que se puede ver lo siguiente:

  -	El estado del servidor que se ejecuta (estado, tamaño, almacenamiento).

  -	La ruta creada para el servidor. Utilice esta ruta para llegar al servidor móvil desde la red Internet pública. Las aplicaciones móviles utilizan esta ruta para acceder al servidor.

  -	Su *nombre de usuario* y *contraseña* personal para acceder al
{{site.data.keyword.mfp_oc_short_notm}}. La *contraseña* está oculta. Pulse el icono de ojo del título para visualizarla.

*	Pulse **Iniciar consola** para abrir la {{site.data.keyword.mfp_oc_short_notm}}.

![Iniciar consola](images/launch_console.png "Figura 2. Iniciar consola")
{: screen}

Esta consola se ejecuta dentro del contenedor. Con la consola, puede gestionar sus aplicaciones móviles y dispositivos móviles, utilizar su servidor como programa de fondo móvil, enviar notificaciones push, etc. 

### Recreación del servidor de {{site.data.keyword.mobilefirst}}
{: #recreate_mobilefoundation_p2}

*	Pulse **Recrear** para volver a crear el servidor. 

![Recrear](images/recreate.png "Figura 3. Recrear")
{: screen}

* Esta acción detiene el servidor existente y lo suprime. Se crea una nueva instancia del servidor. Esta acción tarda unos minutos en completarse.

**Nota**: todos los datos de su instancia de servidor anterior, incluyendo la información sobre aplicaciones y adaptadores, se conservan en la instancia del servicio {{site.data.keyword.dashdbshort_notm}} configurada; estará disponible para su uso una vez que se vuelva a crear el servidor. 

##	Ajuste de la configuración avanzada
{: #using_mfs_advanced_p2}

Utilice la opción **Iniciar servidor con configuración avanzada** en la página *Visión general* para crear el servidor con valores avanzados o personalizados. También puede actualizar los valores del servidor para personalizar su configuración desde la pestaña **Configuración**. {{site.data.keyword.mobilefoundation_short}} le ofrece acceso a algunos valores avanzados. 

*	Desde la pestaña **Topología**, puede seleccionar el Tamaño de topología del contenedor. El valor predeterminado del servidor es de 1 GB, que es suficiente para el desarrollo y la realización de pruebas no muy exigentes; no obstante, es posible que necesite más capacidad para realizar, por ejemplo, pruebas de carga. 
  - Seleccione el tamaño correcto para su servidor en función de sus necesidades. 

  - **Nodos** muestra el número de nodos que se han creado. 
      - Puede configurar el número de nodos mínimo y máximo que necesite en sus grupos de contenedores de {{site.data.keyword.IBM_notm}}.
Los grupos de contenedores ofrecen gran disponibilidad y escalabilidad.

      - Se puede crear una granja de servidores de {{site.data.keyword.mobilefirst}} configurando el número de nodos aquí. 

Consulte la [Documentación de {{site.data.keyword.mobilefoundation_long}}](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window} para obtener más detalles. 
