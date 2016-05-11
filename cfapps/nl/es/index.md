---

 

copyright:

  years: 2015 2016

 

---

{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}

# Creación de apps de Cloud Foundry
*Última actualización: 18 de abril de 2016*

Con {{site.data.keyword.Bluemix}}, puede crear su app en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. Una vez creada, puede seguir utilizando la interfaz de usuario o utilizar la interfaz de línea de mandatos cf o {{site.data.keyword.jazzhub_title}} para desarrollar, planificar, desplegar o realizar un seguimiento de la app.
{:shortdesc}

Para crear una app en {{site.data.keyword.Bluemix_notm}}, se comienza con un iniciador. Un *iniciador* es una plantilla que incluye servicios predefinidos y código de aplicación configurado con un determinado paquete de compilación. Hay dos tipos de iniciadores: contenedores modelo y tiempos de ejecución.

Un *contenedor modelo* es un contenedor para una aplicación y su entorno de tiempo de ejecución y servicios predefinidos asociados para un dominio concreto. Por ejemplo, el contenedor modelo de Mobile Cloud incluye un tiempo de ejecución Node.js, así como los servicios Mobile Data, Mobile Application Security y Push. También incluye un SDK y apps de ejemplo para empezar a desarrollar apps para móvil que accedan a estos servicios.

Un *tiempo de ejecución* es el conjunto de recursos que se utiliza para ejecutar una aplicación. {{site.data.keyword.Bluemix_notm}} proporciona entornos de tiempo de ejecución como contenedores para distintos tipos de apps. Los entornos de tiempo de ejecución están integrados como paquetes de compilación en {{site.data.keyword.Bluemix_notm}}, se configuran automáticamente y requieren muy poco o ningún mantenimiento.

Para empezar a crear la aplicación, siga los pasos siguientes:
  1. Vaya al panel de control en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.
  2. Pulse **CREAR UNA APP**.
  3. Pulse **WEB** y siga las instrucciones
para elegir un iniciador, especifique un nombre y seleccione cómo desea codificar.
  4. Cuando acabe con las instrucciones, pulse **VER
VISIÓN GENERAL DE LA APP**. Se visualiza la Visión general de su app en el panel de control.
  5. Puede añadir un servicio a la app pulsando **AÑADIR UN SERVICIO O API** en la Visión general de la app, en la interfaz de usuario de Bluemix. Examine y seleccione servicios del catálogo, o  desplácese hasta el final del catálogo y pulse **Servicios experimentales de {{site.data.keyword.Bluemix_notm}}** para examinar servicios experimentales.
También puede utilizar la interfaz de línea de mandatos cf. Consulte Opciones para trabajar con apps.
  6. En la Visión general de la app, pulse Añadir Git para guardar el origen de la aplicación en un
repositorio Git y crear un proyecto alojado en Git. También puede desplegar la aplicación desde {{site.data.keyword.jazzhub_title}}.

**Nota:** Si se bloquea un servicio enlazado con una app, esta puede dejar de ejecutarse o contener errores. {{site.data.keyword.Bluemix_notm}} no reinicia automáticamente la aplicación para solucionar los problemas. Considere la posibilidad de codificar su app para identificar y recuperarse de paradas, excepciones y
fallos de conexión. Para obtener más información, consulte el tema de resolución de problemas Las apps no se reinician automáticamente.

## Opciones para trabajar con apps

Después de crear la app, tiene algunas opciones para continuar añadiendo servicios a la app y para compilar y desplegar su app:

<dl><dt>Interfaz de línea de mandatos cf</dt>
<dd>Utilice la interfaz de línea de mandatos cf para actualizar su aplicación, crear una instancia de servicio o enlazar el servicio a su aplicación. También puede utilizar la interfaz de línea de mandatos cloud-cli para crear, actualizar y suprimir ofertas de servicio.</dd>
<dt>Interfaz de usuario de {{site.data.keyword.Bluemix_notm}}</dt>
<dd>Utilice la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} para compilar su aplicación, incluida la selección de servicios y tiempos de ejecución que desea combinar para solucionar el problema empresarial.</dd>
<dt>{{site.data.keyword.jazzhub_title}}</dt>
<dd>Utilice {{site.data.keyword.jazzhub_title}} para crear una aplicación en la nube y desplegarla en {{site.data.keyword.Bluemix_notm}}. Los servicios que suministra {{site.data.keyword.jazzhub_title}} incluyen Track & Plan y Delivery Pipeline, que se muestran en el catálogo de {{site.data.keyword.Bluemix_notm}}, en DevOps, así como Web IDE y el alojamiento de Git.</dd>
</dl>

## Consejos

Utilice los siguientes consejos para desarrollar apps web:

<dl><dt>Persistencia</dt>
<dd>No especifique ningún almacenamiento local para las apps. Cada instancia de la aplicación, aunque sólo haya una instancia en ejecución, se puede reiniciar o mover a otra máquina virtual en cualquier momento, normalmente para equilibrar la carga. Todo lo que se almacena en almacenamiento local se borra cuando la aplicación se mueve o se suprime. Utilice uno de los servicios de almacén de datos de Bluemix para conservar los datos.</dd>
<dt>Límites de recursos</dt>
<dd>Tenga en cuenta los límites sobre las cantidades de recursos que puede utilizar una cuenta de prueba. Los límites son los siguientes:
<table style="width:100%">
  <th>Tipo de recurso</th>	<th>Límite de cantidad</th>
<tr><td>Número de servicios que se utilizan en todas las apps</td> <td>10</td>
<tr><td>Memoria utilizada en todas las apps</td> <td>	2 G</td>
<tr><td>Número de rutas</td> <td>500</td>
</table>
</dd></dl>

*Tabla 1. Límites de recursos de {{site.data.keyword.Bluemix_notm}} para una cuenta de prueba*
