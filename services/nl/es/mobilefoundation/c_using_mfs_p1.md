---

copyright:
  years: 2016

---

#	Utilización del plan de desarrollador
{: #using_mobilefoundation_p1}

*Última actualización: 15 de junio de 2016*
{: .last-updated}

Después de crear la instancia de servicio {{site.data.keyword.mobilefoundation_short}}: Desarrollador, acepte los términos de licencia para {{site.data.keyword.mfp_full_notm}} V8.0, para empezar.
Después de varios segundos, puede acceder a la página `Visión general` de
{{site.data.keyword.Bluemix_notm}}, que le ofrece guías de aprendizaje y vídeos para ayudarle a aprender a utilizar el servicio
{{site.data.keyword.mobilefoundation_short}}.

## Inicio del servidor de {{site.data.keyword.mobilefirst}}
{: #start_mobilefoundation_p1}
* Para iniciar {{site.data.keyword.mfserver_short_notm}} con los valores predeterminados, pulse **Iniciar servidor básico**.

Esta selección suministra un {{site.data.keyword.mfserver_long_notm}} con la configuración siguiente:
*	1 GB de memoria y 64 GB de almacenamiento. Este tamaño es suficiente para realizar actividades de desarrollo y de pruebas no muy exigentes.

*	El `nombre de usuario` y la `contraseña` se generan de forma automática. Tiene acceso a ellos cuando el servidor está en ejecución.

Se inicia el proceso de suministro. Este proceso dura unos 10 minutos y un mensaje indica el progreso de la operación. Una vez finalizado, se muestra un panel de instrumentos en el que se puede ver lo siguiente:
*	El estado del servidor que se ejecuta (estado, tamaño, almacenamiento).

*	La ruta creada para el servidor. Utilice esta ruta para llegar al servidor móvil desde la red Internet pública. Las aplicaciones móviles utilizan esta ruta para acceder al servidor.

*	Su `nombre de usuario` y `contraseña` personal para acceder al
{{site.data.keyword.mfp_oc_short_notm}}. La `contraseña` está oculta. Pulse **Mostrar contraseña** para visualizarla.

*	Pulse **Iniciar consola** para iniciar la {{site.data.keyword.mfp_oc_short_notm}}.


Esta consola se ejecuta dentro del contenedor. Con la consola, puede gestionar sus aplicaciones móviles y dispositivos móviles, utilizar su servidor como programa de fondo móvil, enviar notificaciones push, etc.

## Recreación del servidor de {{site.data.keyword.mobilefirst}}
{: #recreate_mobilefoundation_p1}

*	Pulse **Recrear** para volver a crear el servidor.

* Esta acción detiene el servidor existente y lo suprime. Todos los datos del servidor móvil se pierden. Se crea una nueva instancia del servidor. Esta acción tarda unos minutos en completarse.

##	Ajuste de la configuración avanzada
{: #using_mfs_advanced_p1}

Utilice la opción **Iniciar servidor con configuración avanzada** en la página `Visión general` para crear el servidor con valores avanzados o personalizados. También puede actualizar los valores del servidor para personalizar su configuración desde la pestaña **Configuración**. {{site.data.keyword.mobilefoundation_short}} le ofrece acceso a algunos valores avanzados.

*	Desde la pestaña **Topología**, puede seleccionar el tamaño del contenedor. El valor predeterminado del servidor es de 1 GB, que es suficiente para el desarrollo y la realización de pruebas no muy exigentes. 

  - Seleccione el tamaño correcto para su servidor en función de sus necesidades.


* **Nodos** muestra el número de nodos que se han creado. Este campo no es editable en
{{site.data.keyword.mobilefoundation_short}}: Desarrollador. El número de nodos en el grupo de contenedor de {{site.data.keyword.IBM_notm}} toma el valor predeterminado de **1** en el Plan de desarrollador.

Consulte la [Documentación de {{site.data.keyword.mobilefoundation_long}}](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window} para obtener más detalles.
