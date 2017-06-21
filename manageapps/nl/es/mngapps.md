---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-11"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Detalles de app
{: #manageapps}

El panel de control Apps en la consola de {{site.data.keyword.Bluemix}} proporciona información de resumen de la aplicación que ha creado. La información de resumen incluye el nombre, el icono, el URL, el tiempo de ejecución, el estado de ejecución y las instancias de servicios vinculadas a la app. 
{:shortdesc}

Desde el panel de control Apps, puede ver el estado de cada aplicación.

**Detenido o Desconocido (gris)**

  La app se ha detenido o el estado es desconocido. El icono gris indica que la app está detenida o que se desconoce su estado.

**En ejecución (verde)**

  La app está ejecutándose. El icono verde indica que la app se ha iniciado y se están ejecutando todas las instancias.

*Número* **en ejecución (amarillo)**

  La app se ha iniciado pero no se están ejecutando todas las instancias. El icono amarillo indica que se están ejecutando menos del 100% de las instancias. El número de instancias que se están ejecutando y el número de instancias que no se han podido visualizar.

**No se está ejecutando (rojo)**

  La app no está ejecutándose. El icono rojo indica que la app se ha iniciado, pero que no hay ninguna instancia en ejecución.

Para ver más información sobre una app, pulse el nombre para abrir la página Visión general de la app.

Cuando se despliega una app, puede iniciar, detener, reiniciar o (en el caso de las apps web) modificar el número de instancias y la cantidad de memoria que utiliza la app. En este momento, para aplicaciones web, {{site.data.keyword.Bluemix_notm}} no escala automáticamente la app en función de su carga, por lo que deberá gestionar este aspecto usted mismo.

Las aplicaciones se pueden volver a desplegar si se realiza una actualización. El mecanismo por el que se actualiza la app es el mismo que se utiliza cuando se despliega originalmente. {{site.data.keyword.Bluemix_notm}} detiene
todas las instancias en ejecución y las reemplaza por instancias nuevas de forma automática.
