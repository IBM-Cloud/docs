{:new_window: target="_blank"} 
{:shortdesc: .shortdesc}

#{{site.data.keyword.Bluemix_notm}} dedicado
{: #dedicated}

*Última actualización: 20 de octubre de 2015*

{{site.data.keyword.Bluemix}} es una plataforma de estándares abiertos basada en la nube para crear, ejecutar y gestionar aplicaciones. {{site.data.keyword.Bluemix_notm}} dedicado le ofrece la potencia y simplicidad de {{site.data.keyword.Bluemix_notm}} en su propio entorno SoftLayer dedicado, que se conecta de forma segura tanto al entorno público de {{site.data.keyword.Bluemix_notm}} como a su propia red.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} dedicado incluye un catálogo privado que muestra los servicios dedicados que tiene disponibles de forma exclusiva. También incluye servicios adicionales sindicados disponibles que puede utilizar desde {{site.data.keyword.Bluemix_notm}} público.

{{site.data.keyword.Bluemix_notm}} dedicado se basa en SoftLayer para ofrecerle una infraestructura de nube de alto rendimiento. Cada centro de datos dispone de servicios de seguridad 24 horas, 7 días `por semana y rigurosos controles. El cliente e IBM acceden a la instancia dedicada de {{site.data.keyword.Bluemix_notm}} a través de un túnel VPN y de una VLAN privada.

![{{site.data.keyword.Bluemix_notm}} dedicado](images/detaileddedicated.png "{{site.data.keyword.Bluemix_notm}} dedicado")

*Figura 1. Diagrama detallado de {{site.data.keyword.Bluemix_notm}} dedicado*

Los entornos de {{site.data.keyword.Bluemix_notm}} dedicado tiene los mismos estándares de seguridad que {{site.data.keyword.Bluemix_notm}} público en la infraestructura y en la seguridad física y operativa. Sin embargo, el acceso de desarrollador a {{site.data.keyword.Bluemix_notm}} dedicado está controlado por políticas de LDAP, que las pueden configurar el equipo de {{site.data.keyword.Bluemix_notm}} al configurar el entorno. En el entorno dedicado, puede gestionar los roles y permisos de usuarios. Consulte [Gestión de usuarios y permisos](../admin/index.html#oc_useradmin) para ver más detalles.

{{site.data.keyword.Bluemix_notm}} dedicado se suministra con todos los tiempos de ejecución de {{site.data.keyword.Bluemix_notm}} incluidos y
128 GB de memoria de aplicación.

Además, hay un conjunto de servicios incluidos de forma predeterminada y servicios opcionales que puede elegir para su instancia dedicada.  

| **Tipo**        | **Nombre**            | **Descripción** |      
|-----------------|-------------------|-------------------|
| Incluido | {{site.data.keyword.autoscaling}} | Aumente o reduzca de forma dinámica la capacidad de cálculo de la aplicación en función de políticas. Con este servicio, dispone de un uso ilimitado del entorno {{site.data.keyword.Bluemix_notm}} dedicado.  |
| Incluido | {{site.data.keyword.datacshort}} | Este servicio proporciona una cuadrícula de datos en memoria que da soporte a casos de ejemplo de memoria caché distribuidos para las apps. Incluye 50 GB de memoria caché en memoria.  |
| Incluido | {{site.data.keyword.cloudant}} | La base de datos NoSQL de IBM
que ofrece una capa de datos JSON de alto rendimiento (compatible
con CouchDB). Incluye 1,6 TB y un máximo de 3.000 solicitudes de API por segundo. |
| Opcional | {{site.data.keyword.sqldb}} | La base de datos de IBM {{site.data.keyword.sqldbfull}} para {{site.data.keyword.Bluemix_notm}} añade una base de datos relacional con todas sus funciones a la aplicación. {{site.data.keyword.sqldb}} ofrece una base de datos gestionada para manejar las exigentes cargas de trabajo transaccionales y web de la empresa. |
| Opcional | {{site.data.keyword.mql}} | IBM {{site.data.keyword.mqlfull}} for {{site.data.keyword.Bluemix_notm}} es un servicio de mensajería basado en la nube que proporciona mensajería flexible y fácil de usar para apps {{site.data.keyword.Bluemix_notm}}. {{site.data.keyword.mql}} proporciona una solución fácil de administrar para la mensajería. Puede utilizar {{site.data.keyword.mql}} para aumentar el nivel de respuesta y de escalado de sus apps y puede compartir y descargar trabajo entre apps con una sencilla y potente API. |
| Opcional | {{site.data.keyword.dashdbshort}} | Utilice dashDB para almacenar datos relacionales, que incluye tipos especiales como datos geoespaciales. A continuación, analice esos datos con SQL o análisis integrados avanzados como análisis predictivo y minería de datos, análisis con R y análisis geoespaciales. |

*Tabla 1. Servicios dedicados*

##Configuración de {{site.data.keyword.Bluemix_notm}} dedicado
{: #setupdedicated}

{{site.data.keyword.Bluemix_notm}} dedicado se ha diseñado para proporcionar una versión privada del producto {{site.data.keyword.Bluemix_notm}} público. Puede utilizar los servicios y tiempos de ejecución de {{site.data.keyword.Bluemix_notm}} para satisfacer sus requisitos de cálculo en una cuenta SoftLayer alojada en IBM.

IBM le proporciona acceso a {{site.data.keyword.Bluemix_notm}} dedicado mediante un inicio de sesión protegido por contraseña. Puede acceder a los servicios, tiempos de ejecución y recursos asociados, y desplegar y eliminar apps {{site.data.keyword.Bluemix_notm}}. IBM se beneficia de varias ubicaciones de SoftLayer para ofrecer {{site.data.keyword.Bluemix_notm}} dedicado, de modo que puede obtener su versión privada en una ubicación cercana.

Para configurar su versión privada de {{site.data.keyword.Bluemix_notm}}:

<ol>
<li>Póngase en contacto con el representante designado de la cuenta de IBM o con el equipo de <a href="https://console.ng.bluemix.net/?direct=classic/#/contactUs/cloudOEPaneId=contactUs" target="_blank">{{site.data.keyword.Bluemix_notm}}</a> para empezar a trabajar.</li>
<li>El cargo mensual se basa en los servicios dedicados que desee utilizar, más una suscripción a todos los servicios públicos de {{site.data.keyword.Bluemix_notm}}. Recibirá una factura por todo lo que utilice por encima del acuerdo de suscripción.<ol type="a">
	<li>Trabaje con IBM, a cargo del cliente, para configurar la instancia de {{site.data.keyword.Bluemix_notm}} dedicado.
	El cargo mensual se basa en los servicios dedicados que desee utilizar, más una suscripción a todos los servicios públicos de {{site.data.keyword.Bluemix_notm}}. Recibirá una factura por todo lo que utilice por encima del acuerdo de suscripción.</li>
	<li>Identifique plazos límite para cada fase de la configuración de la instancia de {{site.data.keyword.Bluemix_notm}} dedicado.</li>
	</ol>
	</li>
<li>Seleccione la <a href="http://www.softlayer.com/data-centers" target="_blank">ubicación del centro de datos SoftLayer</a> para su instancia dedicada. A partir de aquí se crea la plataforma dedicada y la cuenta. Para la cuenta, identifique las personas de la organización para los roles necesarios para configurar y activar la instancia dedicada. Para cada rol hay un representante de IBM correspondiente.<br />
<p>Roles del cliente:</p>
<dl>
<dt>**Contacto de suministro**</dt>
<dd>Trabaja con el representante de IBM en el establecimiento del entorno de {{site.data.keyword.Bluemix_notm}} dedicado, incluida la identificación de las personas adecuadas de la organización que trabajarán en cualquier aspecto del proyecto. Este rol supervisa la selección del patrón, las formas comerciales y la disposición de acceso a los recursos del cliente. El contacto de suministro es el contacto general para configurar la instancia dedicada.</dd>
<dt>**Responsable de suministro**</dt>
<dd>Trabaja con el representante de IBM para seleccionar una topología y opción de despliegue que se ajuste a sus requisitos de seguridad. Este rol funciona con el asesor de suministro de IBM para determinar qué patrones de despliegue consiguen los objetivos y las metas de conformidad.</dd>
<dt>**Especialista de red**</dt>
<dd>Trabaja con el representante de IBM en los planes de red para el despliegue de {{site.data.keyword.Bluemix_notm}}. Este rol proporciona los requisitos al representante de IBM y trabaja con él en un plan de implementación. Al final de la fase de instalación y de verificación, este rol "concluirá" que la configuración de red está en conformidad con los estándares corporativos.</dd>
<dt>**Contacto de DevOps**</dt>
<dd>Trabaja con el representante de IBM para planificar y aplicar las actualizaciones de mantenimiento necesarias para la plataforma, servicios y tiempos de ejecución de {{site.data.keyword.Bluemix_notm}}. Este rol también trabaja con el representante de IBM en la configuración de la instancia de {{site.data.keyword.Bluemix_notm}} dedicado.</dd>
</dl>
<p>Roles de IBM:</p>
<dl>
<dt>**Gestor de suministro de IBM**</dt>
<dd>Trabaja con el contacto de suministro del cliente para establecer el entorno del cliente.</dd>
<dt>**Asesor de conformidad de IBM**</dt>
<dd>Trabaja con el representante de conformidad de cliente para seleccionar una topología y una opción de despliegue que cumpla los requisitos de seguridad.</dd>
<dt>**Especialista de red de IBM**</dt>
<dd>Trabaja con el especialista de red de cliente para establecer los planes de red para el despliegue. Este rol funciona con el cliente para recopilar requisitos y crear un plan de implementación. Este rol también realiza las pruebas automatizadas para verificar el resultado físico del plan de implementación.</dd>	
<dt>**Contacto de DevOps de IBM**</dt>
<dd>Trabaja con el contacto de DevOps del cliente en la instalación y en el mantenimiento en curso de la topología de despliegue. Este rol funciona con el cliente para planificar y llevar a cabo las actualizaciones necesarias para la plataforma y los servicios.</dd>
</dl>
</li>
<li>Defina y establezca la conectividad de red entre su red corporativa y la instancia de {{site.data.keyword.Bluemix_notm}} dedicado.<ol type="a">
	<li>IBM instala la infraestructura de supervisión y seguridad para la instancia dedicada.</li>
	<li>IBM instala los servicios dedicados de arrendatario único que seleccione.</li>
	<li>El cliente proporciona la configuración de la red y puntos finales para elementos tales como direcciones IP o cortafuegos y acceso a LDAP para la integración en {{site.data.keyword.Bluemix_notm}}.</li>
	</ol>
</li>
<li>Identifique y asigne roles para el equipo de administración del entorno.<ol type="a">
	<li>IBM configura el acceso a la red y LDAP en función de lo que proporcione el usuario. Se ofrece acceso de administración a los contactos que designe el cliente. También debe designar un contacto para soporte y facturación. </li>
	<li>IBM configura un catálogo sindicado en el entorno dedicado para mostrar los servicios dedicados y muchos de los servicios públicos de {{site.data.keyword.Bluemix_notm}}.</li>
	<li>El cliente debe validar la configuración de la red y del cortafuegos, además del punto final LDAP y el acceso.</li>
	</ol>
</li>
</ol>

##Mantenimiento de la instancia dedicada
{: #maintaindedicated}

IBM mantiene e instala actualizaciones y arreglos como cambios de IBM adecuados para la plataforma de {{site.data.keyword.Bluemix_notm}} dedicado, tiempos de ejecución y servicios.

**Importante**: IBM se reserva el derecho de interrumpir servicios para aplicar mantenimiento emergencia si es necesario. IBM puede modificar las horas de mantenimiento planificadas, pero le notificará cualquier cambio, así como la información de mantenimiento de emergencia.

Se requieren los siguientes tipos de mantenimiento para {{site.data.keyword.Bluemix_notm}} dedicado:
<dl>
<dt>**Ventanas de mantenimiento estándar**</dt>
<dd>Los servicios utilizan ventanas de mantenimiento estándar y predefinidas, lo cual podría hacer que los servicios no estén disponibles. IBM no requiere aprobación del cliente para realizar el mantenimiento, pero intenta minimizar el impacto en los servicios.<br />
<br />
IBM envía mensajes de difusión general de los cambios planificados para cada ventana de mantenimiento, por correo electrónico, por teléfono o mediante otros métodos.<br />
<br />
**Importante**: Es posible que algún servicio no esté disponible durante el periodo de mantenimiento.</dd>

<dt>**Ventana de cambio mensual**</dt>
<dd>La ventana de mantenimiento mensual se aplica en función de la coordinación entre el usuario y IBM dentro de una ventana de 21 días. Puede proporcionar a IBM horas o fechas específicas dentro de la ventana de 21 días que puede que no funcionen para el usuario. IBM intenta planificar actualizaciones alrededor de esas horas. En función de las solicitudes, IBM se comunicará con la ventana de mantenimiento planificada. No se espera que las ventanas de cambio mensual produzcan un impacto en la ejecución del entorno dedicado de Bluemix.<br />
<br />
**Nota:** Si no solicita una hora específica para la actualización, se aplicará automáticamente el mantenimiento al final de la ventana.<br />
<br />
Vaya a **ADMINISTRACIÓN > INFORMACIÓN DEL SISTEMA** para ver las actualizaciones pendientes, establecer fechas no disponibles y aprobar actualizaciones. Para obtener más información sobre las notificaciones y la planificación de actualizaciones pendientes, consulte <a href="../admin/index.html#oc_system">Visualización de información del sistema</a>.</dd>
	
<dt>**Otro**</dt>
<dd>IBM intenta limitar todo el mantenimiento que pueda afectar a los servicios, en particular a la disponibilidad del entorno {{site.data.keyword.Bluemix_notm}} dedicado, los tiempos de ejecución y los servicios, a las actualizaciones estándar y mensuales. Es posible que, de forma excepcional, se utilicen otras ventanas de cambios para la gestión del entorno. IBM hará todo lo posible para minimizar el impacto en su entorno durante estas ventanas de cambios y se lo notificará por adelantado. </dd>
</dl>

Para configurar el mantenimiento de la instancia dedicada, póngase en contacto con el representante designado de su cuenta de IBM para identificar una ventana acordada para el mantenimiento estándar.
