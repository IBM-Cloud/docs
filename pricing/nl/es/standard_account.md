---



copyright:

  years: 2016, 2017
lastupdated: "2017-02-02"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Cuenta Estándar Beta de {{site.data.keyword.Bluemix_notm}} de IBM 
{: #betaintro}

La cuenta Estándar Beta de {{site.data.keyword.Bluemix}} presenta una nueva cuenta gratuita, que ofrece una nueva forma de trabajo en la nube pública de {{site.data.keyword.Bluemix_notm}}. La cuenta Estándar no caduca nunca, lo que la diferencia de la cuenta de prueba de {{site.data.keyword.Bluemix_notm}} de 30 días. Puede seguir trabajando en sus aplicaciones de {{site.data.keyword.Bluemix_notm}} sin ninguna preocupación sobre las restricciones de tiempo.
{:shortdesc}

La participación en la cuenta Estándar Beta es sólo por invitación. Una vez que acepte la invitación y que cree la cuenta Estándar, puede invitar a sus amigos y colegas para que participen en Beta.  

## Presentación de la cuenta Estándar de {{site.data.keyword.Bluemix_notm}}
{: #standardaccount}

Puede que se pregunte sobre qué diferencia hay entre la cuenta Estándar y la cuenta de prueba. Las tablas siguientes resumen los detalles clave sobre la cuenta Estándar de {{site.data.keyword.Bluemix_notm}}. 

|¿Qué novedades hay en una cuenta Estándar? |    
|-----------------|
| La cuenta no caduca nunca. |
| Las aplicaciones de Cloud Foundry pueden acceder hasta un máximo 256 MB de memoria de tiempo de ejecución gratuita e instantánea.  |
| Puede acceder a planes Lite gratuitos para Cloudant NoSQL DB y a la Plataforma Internet de las cosas con más servicios gratuitos disponibles muy pronto. |
| Sus aplicaciones entrarán en suspensión si no hay actividad de desarrollo durante 10 días. |
| Las instancias de servicio se suprimirán tras 30 días de inactividad. |
{:caption="Table 1. What's new in a Standard Account" caption-side="top"}

|¿Qué es lo que no cambia cuando se convierte una cuenta de prueba? | 
|-----------------|
|La cuenta es gratuita. No necesita una tarjeta de crédito. |
|Cualquier instancia Lite de Cloudant NoSQL DB y de la Plataforma Internet de las cosas. Se puede transferir a su nueva cuenta una instancia de Lite para cada uno de estos servicios. |
|Los valores de acceso de su organización, espacios y miembros de equipo asociados siguen siendo los mismos. Se puede transferir una organización a su cuenta nueva. |
|El nivel de soporte de {{site.data.keyword.Bluemix_notm}} sigue siendo el mismo. |
{:caption="Table 2. What's not changing" caption-side="top"}

**Nota** Si la cuenta de prueba no se convierte, verá un mensaje que le dirá el motivo. Puede que tenga más de una organización en la cuenta de prueba existente o aplicaciones que no se puedan transferir. Puede realizar la acción apropiada y volver a intentar convertir la cuenta.

Cuando se haya registrado para una cuenta Estándar, puede invitar a los miembros del equipo a colaborar en su organización y espacios, a ver su uso, a crear espacios, a actualizar el perfil de la cuenta y a gestionar su organización. Para obtener más información,
consulte [Configuración de la cuenta](/docs/admin/adminpublic.html#account).

### Planes de Lite
{: #liteplans}
   
Los planes de Lite, que también están disponibles en una cuenta de pago según uso, están estructurados como una cuota gratuita. Puede trabajar en sus proyectos sin preocuparse, sin el riesgo de generar una factura accidentalmente. La cuota puede funcionar durante un periodo de tiempo específico, por ejemplo, un mes, o sobre una base de uso único. A continuación se mencionan algunos ejemplos de las cuotas del plan de Lite:

<ul>
<li>Número máximo de dispositivos registrados.</li>
<li>Número máximo de enlaces de aplicaciones.</li>
<li>Límite de almacenamiento de datos cifrados, como por ejemplo, 1 GB.</li>
<li>Capacidad de rendimiento suministrada.</li>
</ul> 

En una cuenta Estándar, puede utilizar cualquier cosa del Catálogo de {{site.data.keyword.Bluemix_notm}} que tiene un plan de Lite. Los planes de Lite son fáciles de encontrar. De forma predeterminada, cuando abra el Catálogo, todos los servicios de que tengan un plan de Lite se muestran y se identifican con una etiqueta de Lite ![etiqueta de Lite](../icons/Lite.svg). Seleccione un servicio para ver los detalles de la cuota para el plan de Lite asociado.

### ¿Qué hay disponible en la cuenta Estándar?
{: #whatsavailable}

En una cuenta Estándar, las aplicaciones de Cloud Foundry pueden acceder hasta un máximo de 256 MB de memoria de tiempo de ejecución instantánea. Si supera la cuota asignada, puede detener algunas de las aplicaciones para liberar memoria de tiempo de ejecución. 

Durante la cuenta Estándar Beta, los servicios siguientes ofrecen un plan Lite:

<ul>
<li>Cloudant NoSQL DB</li>
<li>Plataforma Internet de las cosas</li>
</ul>

Permanezca atento a las novedades que iremos añadiendo a esta lista de servicios.

Cuando se alcancen los límites de la cuota, se detendrá la aplicación o se inhabilitará el servicio. Si el plan de Lite especifica que la cuota se proporciona de forma mensual, el uso de los recursos se restablecerá el día 1 de cada mes cuando vuelva a trabajar con el servicio. Cuando esté llegando al límite de una cuota, o cuando esté en el límite de la misma, recibirá un correo electrónico de notificación. 

Puede suministrar 1 instancia por plan de Lite. 

**Nota**: Estas limitaciones se aplican únicamente a la cuenta Estándar. Puede actualizar a una cuenta de pago según uso o de facturación por suscripción en cualquier momento. Pague sólo lo que utilice más allá de las concesiones gratuitas. Para obtener más información sobre las cuentas Pago según uso y Suscripción, consulte [Cómo se le factura](/docs/pricing/index.html#pay-accounts).

### Actividad de desarrollo
{: #devactivity}

Para ayudar a los usuarios de la cuenta Estándar a gestionar mejor sus recursos, hemos creado varias características de eficiencia que se basan en la actividad de despliegue y en el uso:

 * Las apps entrarán en suspensión tras 10 días de inactividad de desarrollo. Esto ayuda a la hora de trabajar en una nueva app, porque así no llegará al límite de cuota de memoria de 256 MB. Para reactivar las apps, empiece trabajando en ellas de nuevo en la línea de mandatos de Cloud Foundry o en la consola de {{site.data.keyword.Bluemix_notm}}. 
 
 A continuación hay una lista de todos los mandatos que reactivarán la app:
  * cf push
  * cf restate
  * cf restart
  * cf ssh
  * cf scale
  * cf stop
  * cf start
  * cf create-route
  * cf map-route
  * cf unmap-route
  * cf delete-route
  * cf enable-ssh
  * cf disable-ssh

 **Nota** Si la app ya tiene habilitado ssh, los mandatos `cf enable-ssh` y `cf disable-sh` no reactivarán la app. 

 * Los servicios del plan de Lite se suprimirán si no hay ninguna actividad en ellos durante 30 días. Entonces, no tendrá que suprimir las instancias inactivas cuando desee crear una nueva instancia. En este momento, sólo está utilizando esta característica el servicio de la Plataforma Internet de las cosas. 
 
 Mantenga activa la instancia Lite de la Plataforma Internet de las cosas iniciando sesión en el panel de control de la instancia de servicio de la Plataforma Internet de las cosas.
 
### Participación en la cuenta Estándar Beta
{: #betainvitation}

Si ha seleccionado participar en la Beta, se enviará una invitación a la dirección de correo electrónico asociada con la cuenta de prueba de {{site.data.keyword.Bluemix_notm}}. Cuando reciba la invitación, lleve a cabo las instrucciones del correo electrónico para registrarse para la cuenta Estándar. 

¿Está interesado en participar en la oferta de la cuenta Estándar Beta? Pregunte a sus amigos y colegas. Si se les ha invitado a unirse a Beta y han creado sus cuentas Estándar, ellos también pueden invitarle a usted. 
