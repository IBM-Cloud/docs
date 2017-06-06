---



copyright:

  years: 2015，2017

lastupdated: "2017-05-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Creación de apps de Cloud Foundry

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
  5. Puede añadir un servicio a la app pulsando **AÑADIR UN SERVICIO O API** en la Visión general de la app, en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. Examine y seleccione servicios del catálogo, o desplácese hasta el final del catálogo y pulse **Servicios experimentales de {{site.data.keyword.Bluemix_notm}}** para examinar servicios experimentales. También puede utilizar la interfaz de línea de mandatos cf. Consulte Opciones para trabajar con apps.
  6. En la página de Visión general de la aplicación, desplácese a la tarjeta "Entrega continua" y pulse **Habilitar**. 
El código fuente de su aplicación se guardará en un repositorio en Git Repos and Issue Tracking, que se aloja en Bluemix. También se creará una cadena de herramientas abierta que utilizará dicho repositorio y un conducto de entrega para desarrollar y desplegar su app. Para obtener más información sobre el servicio Continuous Delivery, consulte <a href="https://console.ng.bluemix.net/docs/services/ContinuousDelivery/index.html#cd_getting_started">Iniciación a Continuous Delivery</a>.

**Nota:** Si se bloquea un servicio enlazado con una app, esta puede dejar de ejecutarse o contener errores. {{site.data.keyword.Bluemix_notm}} no reinicia automáticamente la app para solucionar los problemas. Considere la posibilidad de codificar su app para identificar y recuperarse de paradas, excepciones y
fallos de conexión. Para obtener más información, consulte el tema de resolución de problemas Las apps no se reinician automáticamente.

## Opciones para trabajar con apps

Después de crear la app, tiene algunas opciones para continuar añadiendo servicios a la app y para compilar y desplegar su app:

<dl><dt>Interfaz de línea de mandatos cf</dt>
<dd>Utilice la interfaz de línea de mandatos cf para actualizar su aplicación, crear una instancia de servicio o enlazar el servicio a su aplicación. También puede utilizar la interfaz de línea de mandatos cloud-cli para crear, actualizar y suprimir ofertas de servicio.</dd>
<dt>Interfaz de usuario de {{site.data.keyword.Bluemix_notm}}</dt>
<dd>Utilice la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} para compilar su aplicación, incluida la selección de servicios y tiempos de ejecución que desea combinar para solucionar el problema empresarial.</dd>
<dt>{{site.data.keyword.contdelivery_full}}</dt>
<dd>Utilice {{site.data.keyword.contdelivery_short}} para automatizar las compilaciones, las pruebas de unidad, los despliegues entre otras tareas. Edite y envíe el código a través de un potente IDE basado en web. Cree cadenas de herramientas para habilitar las integraciones de herramientas que dan soporte a las tareas de desarrollo, despliegue y funcionamiento. El servicio Continuous Delivery incluye Delivery Pipeline, el IDE web de Eclipse Orion y Git Repos and Issue Tracking. Para obtener más información, consulte <a href="https://console.ng.bluemix.net/docs/services/ContinuousDelivery/index.html#cd_getting_started">Iniciación a Continuous Delivery</a>.</dd>
</dl>

## Consejos

Utilice los siguientes consejos para desarrollar apps web:

<dl><dt>Persistencia</dt>
<dd>No especifique ningún almacenamiento local para las apps. Cada instancia de la aplicación, aunque sólo haya una instancia en ejecución, se puede reiniciar o mover a otra máquina virtual en cualquier momento, normalmente para equilibrar la carga. Todo lo que se almacena en almacenamiento local se borra cuando la aplicación se mueve o se suprime. Utilice uno de los servicios de almacén de datos de {{site.data.keyword.Bluemix_notm}} para conservar los datos.</dd>
<dt>Límites de recursos</dt>
<dd>Tenga en cuenta los límites sobre las cantidades de recursos que puede utilizar una cuenta de prueba. Los límites son los siguientes:
<table style="width:100%">
<caption>Tabla 1. Límites de recursos de {{site.data.keyword.Bluemix_notm}} para una cuenta de prueba</caption>
  <th>Tipo de recurso</th>	<th>Límite de cantidad</th>
<tr><td>Número de servicios que se utilizan en todas las apps</td> <td>10</td>
<tr><td>Memoria utilizada en todas las apps</td> <td>	2 G</td>
<tr><td>Número de rutas</td> <td>500</td>
</table>
</dd></dl>
