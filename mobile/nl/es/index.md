# Creación de apps para móvil
{: #mobile}

Con {{site.data.keyword.Bluemix_notm}} Mobile Services, puede incorporar servicios de nube integrados, gestionados y escalables a las aplicaciones móviles sin intervención de TI. Céntrese en crear sus apps para móvil en lugar de en solucionar la complejidad de gestionar la infraestructura de fondo.

<table><caption>Tabla 1. Contenedor modelo de Bluemix Mobile Services</caption>
<tr>
	<td>Cada uno de los Bluemix Mobile Services se puede utilizar de forma independiente. También puede utilizarlos juntos para obtener el mayor beneficio. Para comenzar, utilice el contenedor modelo de Bluemix Mobile Services para crear la app. Este contenedor modelo:
		<ul>
			<li>Crea un tiempo de ejecución Node.js con una aplicación de plantilla. Puede utilizar esta aplicación para proporcionar funciones de lado de servidor, como por ejemplo las API RESTful y los archivos estáticos. Puede obtener más información sobre el funcionamiento de esta aplicación en la sección Desarrollo del programa de fondo móvil. </li>
			<li>
Proporciona una instancia de cada uno de los Bluemix Mobile Services y enlaza el servicio con la aplicación Node.js. </li>
		</ul>
	</td>
	<td> <img src="images/mf_boiler_icon.png" alt="Servicios móviles de Bluemix" width="500"> Contenedor modelo de Bluemix Mobile Services </td>
</tr>
</table>

Una vez que utilice el contenedor modelo de Bluemix Mobile Services para crear la app, puede obtener ejemplos de HelloWorld para cada uno de los servicios o iniciar la instrumentación de la app existente para utilizar servicios de Bluemix.


## Visión general de los servicios
{: #services-overview}
Puede utilizar todos los Bluemix Mobile Services juntos utilizando el contenedor modelo de los Bluemix Mobile Services o bien puede utilizar servicios individuales desde el catálogo de Bluemix. El diagrama siguiente resalta todos los componentes de Bluemix Mobile Services.

![Arquitectura de servicios móviles de Bluemix](images/bms_architecture.jpg)

<table>
<caption>Tabla 2. Bluemix y sistemas empresariales</caption>
<th>Bluemix</th>
<th>Sistemas empresariales</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Icono de tiempo de ejecución de Node.js"><b>Node.js</b> <br/> Se proporciona un tiempo de ejecución de Node.js que aloja una aplicación plantilla como parte del contenedor modelo de Bluemix Mobile Services. Puede utilizar la aplicación de plantilla para proporcionar funciones de lado de servidor, como por ejemplo las API RESTful y los archivos estáticos. <br/>Por ejemplo, puede extender la aplicación Node.js para el proceso lógico personalizado o conectar con las API REST en la infraestructura existente de la empresa. Cada app que cree en Bluemix tiene un ID de aplicación exclusivo. La app para móvil utiliza este ID con SDK para acceder a los servicios asociados con dicha aplicación. La plataforma utiliza el ID de la app como contexto para funciones comunes, como por ejemplo la calibración y el registro.
Puede obtener más información sobre el funcionamiento de esta aplicación en la sección "Desarrollo del programa de fondo móvil".</td>
<td valign="top"><b>Proveedores de información</b> <br/>Puede utilizar un tiempo de ejecución de Node.js que está alojado en Bluemix para conectarse con cualquier tipo de proveedor de información:
<ul>
	<li>Programa de fondo de empresa</li>
	<li>Base de datos </li>
	<li>Otro servicio de terceros alojado</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="Icono de servicio de Mobile Client Access"> <b>Mobile Client Access</b><br/>Utilice el IBM Mobile Client Access para el servicio de Bluemix para proteger las aplicaciones Node.js y Java for Liberty alojadas en Bluemix. Al instrumentar la app para móvil con el SDK de Mobile Client Access, puede que necesite que los usuarios inicien sesión para acceder a Node.js o a los Bluemix Mobile Services. Además de las prestaciones de seguridad, Mobile Client Access también recopila datos analíticos, por lo que puede supervisar el rendimiento de la aplicación móvil y recopilar los registros del cliente y las estadísticas de uso. </td>
<td valign="top"><b>Proveedores de identidad de usuarios</b> <br/>Puede utilizar los siguientes proveedores de identidad: <ul><li>Facebook</li><li>Google</li></ul></td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="Icono de servicio de Push Notifications"> <b>Push Notifications</b><br/>El servicio de IBM Push Notifications for Bluemix proporciona una plataforma unificada para enviar y gestionar notificaciones push móviles que están pensadas para plataformas iOS y Android. Este servicio gestiona la correlación de los usuarios de aplicaciones en sus dispositivos, plataforma de dispositivos, y maneja la asignación de notificaciones push en los dispositivos. Con este servicio, puede enviar difusiones, unicasts (en función del userID, deviceID), y etiquetas (o temas) basadas en notificaciones push a sus usuarios de aplicación móvil.</td>
<td valign="top"><b>Proveedores de servicio Push</b><ul><li>Apple Push Notifications Service</li><li>Google Cloud Messaging</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Icono de servicio de Cloudant"><b>Cloudant NoSQLDB</b><br/> Cloudant es una base de datos de NoSQL como servicio (DBaaS). Está creada desde la base para escalar globalmente, ejecutarse sin parar y manejar una gran variedad de tipos de datos como JSON, texto completo y geoespacial. </td>
<td>Cloudant.com</td>
</tr>
</table>
