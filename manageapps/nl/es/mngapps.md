---

copyright:
  years: 2015, 2017
lastupdated: "2015-03-17"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

#Gestión de app
{: #manageapps}

Puede utilizar el panel de control de la interfaz de usuario de {{site.data.keyword.Bluemix}} para ver y gestionar sus apps y servicios y para supervisar el uso de recursos mediante los indicadores de cuota.
{:shortdesc}

La sección de la aplicación del panel de control proporciona información resumida de las apps que ha creado. La información resumida incluye nombre, icono, URL, tiempo de ejecución y estado de ejecución de la aplicación y de las instancias de servicio que están enlazadas a la aplicación. Se utilizan distintos colores para indicar el estado de ejecución cada aplicación.

**Detenido o Desconocido (gris)**

  La app se ha detenido o el estado es desconocido. El icono gris indica que la aplicación está detenida, o que el estado es desconocido.

**En ejecución (verde)**

  La app está ejecutándose. El icono verde indica que la aplicación se ha iniciado y se están ejecutando todas las instancias.

*Número* **en ejecución (amarillo)**

  La app se ha iniciado pero no se están ejecutando todas las instancias. El icono amarillo indica que se están ejecutando menos del 100% de las instancias. El número de instancias que se están ejecutando y el número de instancias que no se han podido visualizar.

**No se está ejecutando (rojo)**

  La app no está ejecutándose. El icono rojo indica que la aplicación se ha iniciado, pero que no hay ninguna instancia en ejecución.

En el catálogo de {{site.data.keyword.Bluemix_notm}} puede ver los servicios e iniciadores disponibles. También puede seleccionar un iniciador para crear una aplicación, enlazar un servicio y gestionar la aplicación. Después enlazar un a una aplicación, puede gestionar las instancias de servicio existentes que están enlazadas a la aplicación actual y crear instancias de servicio para la aplicación. También puede desenlazar o suprimir la instancia de servicio de una aplicación o seleccionar otro plan de servicio.

Para ver más información sobre una aplicación, pulse el mosaico para abrir la página Visión general de la app.

**Nota:** Solo puede ver los recursos de una organización a la vez. Si es miembro de varias organizaciones, puede conmutar entre organizaciones
pulsando el icono **CAMBIAR ORGANIZACIÓN** que hay junto
a la organización actual visualizada en la cabecera del panel de control.

Cuando se despliega una aplicación, puede iniciar, detener, reiniciar o (en el caso de las apps web) modificar el número de instancias y la cantidad de memoria que utiliza la aplicación. En este momento, para app web, {{site.data.keyword.Bluemix_notm}} no escala automáticamente la aplicación en función de su carga, por lo que deberá gestionar este aspecto usted mismo.

Las aplicaciones se pueden volver a desplegar si se realiza una actualización. El mecanismo por el que se actualiza la aplicación es el mismo que se utiliza cuando se despliega originalmente. {{site.data.keyword.Bluemix_notm}} detiene
todas las instancias en ejecución y las reemplaza por instancias nuevas de forma automática.
