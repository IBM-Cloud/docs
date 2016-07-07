---

copyright:
  years: 2016

---

#	Utilización del plan de aplicación Profesional 1
{: #using_mobilefoundation_p2}

*Última actualización: 15 de junio de 2016*
{: .last-updated}

Tras crear la instancia del servicio {{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1, consulte el procedimiento siguiente para iniciarse en el uso del servicio. 

## Requisitos previos
{: #prerequisites_p2}

Tenga en cuenta lo siguiente antes de configurar la instancia del servicio
{{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1. 
* {{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1 solo se admite con planes de {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dashdbshort_notm}}: Transacciones empresariales (con soporte para OLTP). 

* La instancia de servicio {{site.data.keyword.dashdbshort_notm}} y sus credenciales deben estar disponibles para poder configurar los valores de su instancia de servicio {{site.data.keyword.mobilefoundation_short}}. 

**Nota**: La instancia de servicio  {{site.data.keyword.dashdbshort_notm}} puede existir en cualquier `Espacio` dentro de la `Organización` de {{site.data.keyword.Bluemix_notm}}.
Si elige desplegar el servicio de {{site.data.keyword.mobilefoundation_short}} en un {{site.data.keyword.Bluemix_notm}} `Espacio` distinto del que está el servicio {{site.data.keyword.dashdbshort_notm}}, debe asegurarse de tener los permisos para acceder al servicio de {{site.data.keyword.dashdbshort_notm}}.


## Adición de la conexión de base de datos
{: #configure_dashdb_p2}

###  Primeros pasos
{: #firststeps_p2}

Después de crear la instancia de servicio {{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1, acepte los términos de licencia para {{site.data.keyword.mfp_full_notm}} V8.0, para empezar.


### Configuración de la conexión con la instancia de servicio {{site.data.keyword.dashdbshort_notm}}
{: #connect_dashdb_p2}

Una vez que se haya creado la instancia de servicio {{site.data.keyword.mobilefoundation_short}}: Aplicación profesional 1, podrá ver la página *Visión general*, donde deberá especificar la información de conexión de la instancia de servicio
{{site.data.keyword.dashdbshort_notm}}: Transacciones empresariales. 

1.  Seleccione el {{site.data.keyword.Bluemix_notm}} `Espacio` donde existe la instancia del servicio {{site.data.keyword.dashdbshort_notm}}, en la lista de espacios disponible en la `Organización` actual.

+ Seleccione el {{site.data.keyword.dashdbshort_notm}} `Nombre de servicio` y las `Credenciales` para conectarse con la instancia de servicio de {{site.data.keyword.dashdbshort_notm}} existente.

+  Pruebe la coneción con la instancia del servicio {{site.data.keyword.dashdbshort_notm}}: Transacciones empresariales especificada. 

+  Pulse **Continuar**. Esta acción crea las tablas necesarias en la instancia de servicio de base de datos de {{site.data.keyword.dashdbshort_notm}} configuradas. 

**Nota**: no puede cambiar la instancia de servicio {{site.data.keyword.dashdbshort_notm}} que está configurada para que la utilice la instancia del servicio {{site.data.keyword.mobilefoundation_short}}. No obstante, puede utilizar la misma instancia de servicio {{site.data.keyword.dashdbshort_notm}} en varias instancias de servicio {{site.data.keyword.mobilefoundation_short}}, ya que cada instancia de servicio {{site.data.keyword.mobilefoundation_short}} crea su propio esquema en la instancia de servicio {{site.data.keyword.dashdbshort_notm}} seleccionada. 

* En varios segundos, puede acceder a la página `Visión general`, que le ofrece guías de aprendizaje y vídeos para ayudarle a aprender a utilizar el servicio {{site.data.keyword.mobilefoundation_short}}. 

## Inicio del servidor de {{site.data.keyword.mobilefirst}}
{: #start_mobilefoundation_p2}

* Para iniciar {{site.data.keyword.mfserver_short_notm}} con los valores predeterminados, pulse **Iniciar servidor básico**.

* Esta selección suministra un {{site.data.keyword.mfserver_long_notm}} con la configuración siguiente: 
    -  1 GB de memoria y 64 GB de almacenamiento. Este tamaño es suficiente para realizar actividades de desarrollo y de pruebas no muy exigentes. 

    -	El `nombre de usuario` y la `contraseña` se generan de forma automática. Tiene acceso a ellos cuando el servidor está en ejecución. 

Se inicia el proceso de suministro del servidor. Este proceso dura unos 10 minutos y un mensaje indica el progreso de la operación. Una vez finalizado, se muestra un panel de instrumentos en el que se puede ver lo siguiente: 

  -	El estado del servidor que se ejecuta (estado, tamaño, almacenamiento). 

  -	La ruta creada para el servidor. Utilice esta ruta para llegar al servidor móvil desde la red Internet pública. Las aplicaciones móviles utilizan esta ruta para acceder al servidor. 

  -	Su `nombre de usuario`` y `contraseña`` personal para acceder al {{site.data.keyword.mfp_oc_short_notm}}. La `contraseña` está oculta. Pulse **Mostrar contraseña** para visualizarla.

*	Pulse **Iniciar consola** para abrir la {{site.data.keyword.mfp_oc_short_notm}}.


Esta consola se ejecuta dentro del contenedor. Con la consola, puede gestionar sus aplicaciones móviles y dispositivos móviles, utilizar su servidor como programa de fondo móvil, enviar notificaciones push, etc. 

## Recreación del servidor de {{site.data.keyword.mobilefirst}}
{: #recreate_mobilefoundation_p2}

*	Pulse **Recrear** para volver a crear el servidor. 

* Esta acción detiene el servidor existente y lo suprime. Se crea una nueva instancia del servidor. Esta acción tarda unos minutos en completarse. 

**Nota**: todos los datos de su instancia de servidor anterior, incluyendo la información sobre aplicaciones y adaptadores, se conserva en la instancia del servicio {{site.data.keyword.dashdbshort_notm}} configurada; estos datos están disponibles para su uso una vez que se vuelva a crear el servidor. 

##	Ajuste de la configuración avanzada
{: #using_mfs_advanced_p2}

Utilice la opción **Iniciar servidor con configuración avanzada** en la página `Visión general` para crear el servidor con valores avanzados o personalizados. También puede actualizar los valores del servidor para personalizar su configuración desde la pestaña **Configuración**. {{site.data.keyword.mobilefoundation_short}} le ofrece acceso a algunos valores avanzados. 

*	Desde la pestaña **Topología**, puede seleccionar el tamaño del contenedor. El valor predeterminado del servidor es de 1 GB, que es suficiente para el desarrollo y la realización de pruebas no muy exigentes. 
  - Seleccione el tamaño correcto para su servidor en función de sus necesidades. 

  - **Nodos** muestra el número de nodos que se han creado. 
      - Puede configurar el número de nodos mínimo y máximo que necesite en su grupo de contenedores de {{site.data.keyword.IBM_notm}}. Los grupos de contenedores ofrecen gran disponibilidad y escalabilidad.

      - Se puede crear una granja de servidores de {{site.data.keyword.mobilefirst}} configurando el número de nodos aquí. 

Consulte la [Documentación de {{site.data.keyword.mobilefoundation_long}}](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}, para obtener más detalles. 
