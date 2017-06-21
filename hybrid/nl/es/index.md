---


copyright:
  years: 2015, 2017
lastupdated: "2017-04-18"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# Gestión de {{site.data.keyword.Bluemix_notm}} Local y {{site.data.keyword.Bluemix_notm}} Dedicado
{: #mng}

Si tiene acceso de administrador para {{site.data.keyword.Bluemix}} Local o {{site.data.keyword.Bluemix_notm}} Dedicado, vaya a la página **Administración** para gestionar recursos, supervisar el uso de cuota, administrar permisos de usuarios, planificar las notificaciones de actualización, ver informes y registros de seguridad, etc. Puede gestionar sus organizaciones mediante la creación de espacios y la configuración de [roles y permisos de usuarios](/docs/admin/index.html#oc_useradmin); consulte [Gestión de las organizaciones](/docs/admin/orgs_spaces.html).
{:shortdesc}

{: #ld_table1}

| ¿Qué puedo hacer? | Detalles |    
|----------------|---------|
|Supervisar el uso del sistema | Pulse **ADMINISTRACIÓN &gt; USO**. Visualice la información del sistema, supervise el uso de la CPU y planifique el uso para tomar las mejores decisiones para su empresa. Consulte [Visualización de información de uso](/docs/admin/index.html#oc_resource).|
|Gestionar el catálogo | Pulse **ADMINISTRACIÓN &gt; GESTIÓN DE CATÁLOGO** para gestionar qué servicios están visibles a sus usuarios y organizaciones. Consulte [Gestión de su catálogo](/docs/admin/index.html#oc_catalog).|
|Administrar organizaciones | Pulse **ADMINISTRACIÓN &gt; ADMINISTRACIÓN DE ORGANIZACIÓN ** para crear organizaciones, supervisar cuotas para organizaciones y realizar rápidamente las decisiones basadas en necesidades. Consulte [Administración de organizaciones](/docs/admin/index.html#oc_organizations).|
|Crear espacios y asignar roles de usuario | Pulse **Cuenta** &gt; **Gestionar organizaciones** para crear espacios dentro de sus organizaciones. Añada usuarios y asigne roles de organización y de espacio a los usuarios. Consultar [Gestión de sus organizaciones](/docs/admin/orgs_spaces.html). |
|Gestionar permisos de usuarios administrativos | Pulse **ADMINISTRACIÓN &gt; ADMINISTRACIÓN DE USUARIOS** para añadir usuarios, eliminar usuarios y ajustar permisos de usuario. Consultar [Gestión de usuarios y permisos](/docs/admin/index.html#oc_useradmin). |
|Revisar informes y registros | Pulse **ADMINISTRACIÓN &gt; INFORMES Y REGISTROS** para ver informes de seguridad y registros de auditoría para su instancia. Ver [Visualización de informes](/docs/admin/index.html#oc_report). |
|Ver información del sistema | Pulse **ADMINISTRACIÓN &gt; INFORMACIÓN DEL SISTEMA** para ver información del sistema como actualizaciones de mantenimiento pendientes, el nombre y la versión de la instancia, la región, el URL de API, el URL de CLI, los detalles de configuración de LDAP, las correlaciones de usuario y de grupo, las estadísticas y los dominios compartidos. Consulte [Visualización de información del sistema](/docs/admin/index.html#oc_system). |
|Ampliar notificaciones y configurar suscripciones de notificaciones | Pulse **ADMINISTRACIÓN &gt; INFORMACIÓN DEL SISTEMA &gt; *Number* pendientes**. Puede usar webhooks para integrar con el servicio web que quiera para configurar la suscripción a notificación de sucesos para una actualización o incidencia. Consulte [Suscripción de notificaciones](/docs/admin/index.html#oc_eventsubscription). |
{: caption="Tabla 1. Tareas administrativas para gestionar la instancia local o dedicada de Bluemix" caption-side="top"}

<!-- staging only for WoW start -->

**Consejo**: El panel de control Infraestructura de la consola {{site.data.keyword.Bluemix_notm}} sólo está disponible en cuentas enlazadas en entornos de {{site.data.keyword.Bluemix_notm}} Público.


<!-- staging only for WoW end -->


## Suscripción de notificaciones
{: #oc_eventsubscription}

Siempre pueda saber el estado de su entorno comprobando la página Estado. A medida que se producen, las
incidencias y los sucesos planificados de actualización disruptiva de mantenimiento se informan en la página Estado. {{site.data.keyword.Bluemix_notm}} también envía notificaciones al área de notificaciones de la página de administración para sucesos tales como actualizaciones de mantenimiento programadas o pendientes.

### Notificaciones

Puede ver notificaciones para el entorno local o dedicado para supervisar el estado del entorno. Revise la
tabla siguiente para obtener información sobre los distintos tipos de notificaciones y dónde se publica cada tipo de notificación.

{: #ld_table2}

| **Tipo de suceso** | **Método de notificación** |       
|-----------------|-------------------|
| Actualizaciones de mantenimiento | Para ver un listado completo y el historial de notificaciones pendientes y completas, pulse **ADMINISTRACIÓN &gt; INFORMACIÓN DEL SISTEMA** &gt; *Número* **pendientes**. Los sucesos planificados de actualización disruptiva de mantenimiento también se informan mediante alertas en la página Estado. Pulse **Soporte** &gt; **Estado**. Puede ampliar la capacidad de notificación configurando una suscripción que envíe un mensaje de correo electrónico a los destinatarios que usted elija. También puede configurar una suscripción que utilice a webhooks para integrar las notificaciones de la página de administración con el servicio de su elección.|
| Incidencias críticas | Se alerta sobre incidencias críticas en la página Estado. Pulse **Soporte** &gt; **Estado**. Puede ampliar la capacidad de notificación configurando una suscripción a una notificación que envíe un mensaje de correo electrónico a los destinatarios que usted elija. También puede configurar una suscripción que utilice a webhooks para integrar las notificaciones de la página de administración con el servicio de su elección.  |  
| Sucesos de umbral | Puede configurar una suscripción de notificación que envía un mensaje de correo electrónico a un destinatario de su elección cuando se alcancen en el entorno los umbrales para la cuota de organización, el disco físico, la memoria física, el disco reservado o la memoria reservada. O bien, puede configurar una suscripción que utilice a webhooks para integrar las notificaciones con el servicio de su elección.  |  
| Estado de {{site.data.keyword.Bluemix_notm}} | Siempre puede ver el estado más reciente de la plataforma, servicios y de su instancia {{site.data.keyword.Bluemix_notm}} en la página Estado. Pulse **Soporte** &gt; **Estado**.  |
{: caption="Tabla 2. Tipos de sucesos y métodos de notificación" caption-side="top"}

### Configuración de suscripciones de notificaciones
{: #seteventsub}

Puede ampliar la funcionalidad de las notificaciones que se envían a las páginas Administración y Estado usando las
suscripciones de notificaciones. Utilice las suscripciones de la notificación para configurar un correo electrónico personalizado o utilizar webhooks para integrar una herramienta de su elección.
 * Si selecciona la opción de correo electrónico, las notificaciones se envían a las direcciones de correo electrónico especificadas. Puede seleccionar notificaciones de incidencias, actualizaciones de mantenimiento o umbrales. Se envía una notificación de correo electrónico inicial. A continuación, si se modifica el suceso, se envía otra notificación con el cambio cada vez que se realice.  
 * Si selecciona la opción de webhooks, las notificaciones se redireccionan directamente a un destino de su elección, como un número de teléfono (por mensaje SMS). Puede personalizar el tipo de notificación, específicamente actualizaciones de mantenimiento, alertas de incidencias críticas, o umbrales. Puede personalizar si desea recibir notificaciones nuevas o notificaciones sobre los cambios a las suscripciones, y qué información se incluye en el cuerpo de cada notificación.

**Nota**: los usuarios con permiso de superusuario (`ops.admin`) son los únicos que pueden configurar suscripciones de notificaciones.

Para crear una suscripción de correo electrónico o webhook desde la página **Suscripciones de notificaciones**, siga estos pasos:

1. Vaya a la página **Suscripciones de notificaciones**.  Vaya a **INFORMACIÓN DEL SISTEMA &gt; Entorno &gt; Suscripciones**.
2. Pulse **Añadir suscripción**.
3. Rellene el formulario de suscripción de notificaciones.

  * Para crear suscripciones a notificaciones por correo electrónico sobre actualizaciones o incidencias de mantenimiento, consulte la información de la [Tabla 3](index.html#emailnotmaintinc).
  * Para crear suscripciones a notificaciones por correo electrónico sobre umbrales, consulte la información de la [Tabla 4](index.html#emailnottrhesh).
  * Para crear suscripciones de notificaciones de webhook sobre las actualizaciones o incidentes de mantenimiento, consulte la información de la [Tabla 5](index.html#webhooknotsub).
  * Para crear suscripciones de notificaciones de webhook sobre los umbrales, consulte la información de la [Tabla 6](index.html#webhooknotthresh).

4. Una vez que haya completado el formulario, puede elegir las opciones siguientes:

  * Pulse **Guardar** para guardar la suscripción en la lista de suscripciones a notificaciones.
  * Pulse **Guardar y probar** para guardar y probar la notificación.
  * Pulse **Guardar y cerrar** para guardar la suscripción en su lista de suscripciones a notificaciones y regresar a la página anterior.

{: #emailnotmaintinc}

| **Campo** | **Descripción** |
|-----------------|-------------------|
| Habilitado | Seleccione la opción para habilitar las notificaciones por correo electrónico. Anule la selección para inhabilitar la notificación por correo electrónico. Las suscripciones están habilitadas de forma predeterminada. |
| Tipo | Seleccione **Correo electrónico**. |
| Suceso | Seleccionar la suscripción a notificaciones para un suceso de **Mantenimiento** o **Incidencia**. |
| Combinar notificaciones | Seleccione la opción para combinar las notificaciones de incidencias de todas las regiones en una única notificación. Esta opción solo está disponible para incidencias. |
| Asunto | Especifique la línea de asunto del correo electrónico. Este campo es necesario.  |
| Cuerpo | Especifique el texto del cuerpo del mensaje que se debe enviar en el correo electrónico. Puede utilizar los valores de carga útil de IBM para rellenar la notificación por correo electrónico con información pertinente. Consulte la tabla [Valores de la sección de carga útil de mantenimiento e incidentes](index.html#payload) para identificar qué valores puede utilizar. Utilice etiquetas HTML básicas para estructurar el correo electrónico. Este campo es necesario. |
| Para | Especifique la dirección o direcciones de correo electrónico utilizando una lista separada por comas de los destinatarios de notificación por correo electrónico. Expanda las opciones "C/o" o "C/co" para enviar una copia del mensaje a otros destinatarios. Este campo es necesario. |
| Descripción | Añada una descripción única para la suscripción que está creando. |
{: caption="Tabla 3. Campos para suscripciones a notificaciones por correo electrónico sobre los umbrales" caption-side="top"}


{: #emailnottrhesh}

| **Campo** | **Descripción** |
|-----------------|-------------------|
| Habilitado | Seleccione la opción para habilitar las notificaciones por correo electrónico. Anule la selección para inhabilitar la notificación por correo electrónico. Las suscripciones están habilitadas de forma predeterminada. |
| Tipo | Seleccione **Correo electrónico**. |
| Suceso | Seleccione **Umbral**. |
| Umbral | Seleccione el tipo de umbral sobre el que desea que se le notifique: Cuota de organización, Disco físico, Memoria física, Disco reservado o Memoria reservada. |
| Dirección de umbral | Seleccione la dirección en la que desea que se muevan los datos, ya sea Ascendente o Descendente, cuando pasa el valor Notificar al aumentar/bajar que haya establecido. Por ejemplo, si el valor Notificar al aumentar/bajar es 50%, y la dirección es descendente, sólo se le notificará si el porcentaje de uso va desde 50% o más a menos de 50%. Si establece la dirección en ascendente, se le notificaría cuando el porcentaje de uso vaya de menos de 50% a más de 50%.   |
| Notificar al aumentar por encima de (%) | Especifique el porcentaje de umbral en el que desea que se le notifique. Si ha elegido la propiedad Ascendente en el campo Dirección de umbral, la notificación de correo electrónico se enviará cuando el umbral supere este porcentaje. |
| Notificar al bajar por debajo de (%) | Especifique el porcentaje de umbral en el que desea que se le notifique. Si ha elegido la propiedad Descendente en el campo Dirección de umbral, la notificación de correo electrónico se enviará cuando el umbral caiga por debajo de este porcentaje. |
| Descripción | Añada una descripción única para la suscripción que está creando. |
| Asunto | Especifique la línea de asunto del correo electrónico. Este campo es necesario.  |
| Cuerpo de mensaje | Especifique el texto del cuerpo del mensaje que se debe enviar en el correo electrónico. Puede utilizar los valores de carga útil de IBM para rellenar la notificación por correo electrónico con información pertinente. Consulte la tabla [Valores de la sección de carga útil](index.html#threshpayload) para identificar qué valores puede utilizar. Utilice etiquetas HTML básicas para estructurar el correo electrónico. Este campo es necesario. |
| Para | Especifique la dirección o direcciones de correo electrónico utilizando una lista separada por comas de los destinatarios de notificación por correo electrónico. Expanda las opciones "C/o" o "C/co" para enviar una copia del mensaje a otros destinatarios. Este campo es necesario. |
{: caption="Tabla 4. Campos para suscripciones a notificaciones por correo electrónico sobre las actualizaciones o los incidentes de mantenimiento" caption-side="top"}

Los datos del umbral se recopilan una vez cada 6 horas. Solamente se enviará una notificación una vez cuando el valor sobrepase el valor de umbral que haya establecido. Si elige ascendente, no se envía una nueva notificación a menos que el valor caiga por debajo del umbral y, a continuación, aumente de nuevo por encima del umbral. Del mismo modo, si ha elegido descendente, sólo se le notificará si el valor sube por encima del umbral establecido y, a continuación, cae por debajo del umbral de nuevo. 

Si no desea esperar 6 horas para que se envíe la notificación cuando se alcanza el umbral, una vez que complete los campos del formulario, puede pulsar **Guardar y probar** para recibir una notificación de prueba con datos de ejemplo.  

Una notificación de umbral de Cuota de organización incluye sólo las organizaciones que han sobrepasado el porcentaje de umbral especificado en el período de tiempo de 6 horas que se corresponde con dicha notificación. Las organizaciones que han sobrepasado un umbral durante los períodos de tiempo de las 6 horas anteriores no estarán incluidas, aunque sigan por encima o por debajo del umbral.  Los tres recursos que componen la cuota de una organización (memoria, servicios y rutas reservados) se consideran independientemente al determinar si se debería enviar o no una notificación de cuota de organización. Por ejemplo, si la cantidad de memoria reservada que utiliza una organización supera el 50% de la cuota de la organización, el umbral de una Cuota de organización configurado con un valor de 50% daría lugar a que se envíe una notificación.  Si el número de servicios utilizados por la misma organización supera el 50% de la cuota de la organización en un momento posterior, aunque la cantidad de memoria utilizada permanezca sin cambios, la misma suscripción de umbral de la Cuota de organización también daría como resultado que se envíe una notificación.

{: #webhooknotsub}

| **Campo** | **Descripción** |
|-----------------|-------------------|
| Habilitado | Seleccione la opción para habilitar la notificación. Anule la selección para inhabilitar la notificación. Las suscripciones están habilitadas de forma predeterminada. |
| Tipo | Seleccione **Webhook** |
| Suceso | Seleccionar la suscripción a notificaciones para un suceso de **Mantenimiento** o **Incidencia**. |
| Autorización | Seleccione si desea habilitar la autorización.  Las opciones son: **Básica** o **Ninguna**. |
| Nombre de usuario | Si elige la autorización **Básica**, especifique el nombre de usuario para el servicio web. Si no quiere usar sus credenciales personales, puede configurar un ID funcional a usar específicamente con {{site.data.keyword.Bluemix_notm}}. |
| Contraseña | Si elige la autorización **Básica**, especifique la contraseña para el servicio web. |
| Descripción | Añada una descripción única para la suscripción que está creando. |
| Nuevo suceso | Seleccione esta opción para habilitar la notificación para nuevos sucesos de mantenimiento o de incidencia. Anule la selección para inhabilitar la notificación. |
| Método | Seleccione **GET**, **POST** o **PUT**. |
| URL | Especificar el URL al que conectar su servicio web. |
| Propiedad de respuesta | Este campo opcional es el nombre de propiedad que identifica el recurso que crea el servicio web cuando se envía una solicitud POST o PUT. Si proporciona una propiedad de respuesta para un nuevo suceso y decide crear una suscripción para un cambio a un suceso, también debe proporcionarla para la suscripción Cambiar a suceso. En función del servicio web que esté utilizando, puede especificarlo como parte del URL o como un valor de carga útil.  |
| Carga útil | Si ha seleccionado el método POST o PUT, especifique las propiedades específicas del servicio web que usa, junto con los valores de carga útil utilizados para la notificación a IBM. Consulte la tabla [Valores de la sección de carga útil de mantenimiento e incidentes](index.html#payload) para identificar qué valores puede utilizar. Si no especifica información en esta sección, recibirá una notificación que no tiene información adicional. |
| Cambiar a suceso | Seleccione esta opción para crear suscripciones de notificación acerca de los cambios realizados en los sucesos de mantenimiento o incidencia para los que ha creado suscripciones. Anule la selección para inhabilitar la notificación. |
| Utilizar valores y carga útil desde Nuevo suceso | Utiliza el contenido de los campos Método, URL y Carga útil desde la sección Nuevo suceso. Tenga en cuenta que si esta opción está seleccionada, estos campos no estarán disponibles para su posterior edición en la sección Cambiar a suceso. |
| Método | Seleccione **GET**, **POST** o **PUT**. |
| URL | Especificar el URL al que conectar su servicio web. |
| Carga útil | Si ha seleccionado el método POST o PUT, especifique las propiedades específicas del servicio web que usa, junto con los valores de carga útil utilizados para la notificación a IBM. Consulte la tabla [Valores de la sección de carga útil de mantenimiento e incidentes](index.html#payload) para identificar qué valores puede utilizar. Si no especifica información en esta sección, recibirá una notificación que no tiene información adicional. |
| Combinar notificaciones | Seleccione la opción para combinar las notificaciones de incidencias de todas las regiones en una única notificación. Esta opción solo está disponible para incidencias. |
{: caption="Tabla 5. Campos de formulario para una suscripción a notificaciones de webhook sobre el mantenimiento o los incidentes" caption-side="top"}


{: #webhooknotthresh}

| **Campo** | **Descripción** |
|-----------------|-------------------|
| Habilitado | Seleccione la opción para habilitar la notificación. Anule la selección para inhabilitar la notificación. Las suscripciones están habilitadas de forma predeterminada. |
| Tipo | Seleccione **Webhook**. |
| Suceso | Seleccione **Umbral**. |
| Umbral | Seleccione el tipo de umbral sobre el que desea que se le notifique: Cuota de organización, Disco físico, Memoria física, Disco reservado o Memoria reservada.|
| Dirección de umbral | Seleccione si desea ver los datos del umbral en orden Ascendente o Descendente.  |
| Notificar al bajar por debajo de (%) | Si ha seleccionado la **Dirección de umbral** **Descendente**, especifique el porcentaje de umbral en el que desea que se le notifique. Cuando el umbral cae por debajo de este porcentaje, se enviará la notificación de webhook. |
| Notificar al aumentar por encima de (%) | Si ha seleccionado la **Dirección de umbral** **Ascendente**, especifique el porcentaje de umbral en el que desea que se le notifique. Cuando el umbral está por encima de este porcentaje, se enviará la notificación de webhook. |
| Descripción | Añada una descripción única para la suscripción que está creando. |
| Autorización | Seleccione si desea habilitar la autorización.  Las opciones son: **Básica** o **Ninguna**. |
| Nombre de usuario | Si elige la autorización básica, especifique el nombre de usuario para el servicio web. Si no quiere usar sus credenciales personales, puede configurar un ID funcional a usar específicamente con {{site.data.keyword.Bluemix_notm}}. |
| Contraseña | Si elige la autorización básica, especifique la contraseña para el servicio web. |
| Método | Seleccione **GET**, **POST** o **PUT**. |
| URL | Especificar el URL al que conectar su servicio web. |
{: caption="Tabla 6. Campos de formulario para una suscripción a notificaciones de webhook sobre umbrales" caption-side="top"}

Los datos del umbral se recopilan una vez cada 6 horas. Solamente se enviará una notificación una vez cuando el valor sobrepase el valor de umbral que haya establecido. No se enviará una notificación nueva a menos que el valor caiga por debajo del umbral, si ha elegido ascendente y, a continuación, aumenta por encima del umbral de nuevo. Del mismo modo, si ha elegido descendente, sólo se le volverá a notificar si el valor sube por encima del umbral establecido y, a continuación, cae por debajo del umbral de nuevo. 

Si no desea esperar 6 horas para que se envíe la notificación cuando se alcanza el umbral, una vez que complete los campos del formulario, puede pulsar **Guardar y probar** para guardar y probar la notificación con datos de ejemplo.

Una notificación de umbral de Cuota de organización incluye sólo las organizaciones que han sobrepasado el porcentaje de umbral especificado en el período de tiempo de 6 horas que se corresponde con dicha notificación. Las organizaciones que han superado un umbral durante los períodos de tiempo de las 6 horas anteriores no se incluirán, aunque sigan por encima/por debajo del umbral.  Los tres recursos que forman la cuota, la memoria reservada, los servicios y las rutas de una organización se consideran de forma independiente al determinar si se debería enviar la notificación de cuota de una organización. Por ejemplo, si la cantidad de memoria reservada que utiliza una organización supera el 50% de la cuota de la organización, el umbral de una Cuota de organización configurado con un valor de 50% daría lugar a que se envíe una notificación.  Si el número de servicios utilizados por la misma organización supera el 50% de la cuota de la organización en un momento posterior, aunque la cantidad de memoria utilizada permanezca sin cambios, la misma suscripción de umbral de la Cuota de organización también daría como resultado que se envíe una notificación.

{: #payload}

| **Valor de IBM** | **Descripción** | **Tipo de suceso** |
|----------------|----------------|------------------------|
| {{content.category}} | Servicios afectados | Incidencia |
| {{content.disruption}} | Componentes afectados | Actualización de mantenimiento |
| {{content.message}} | Descripción del mensaje |   Actualización de mantenimiento e incidencia |
| {{content.scheduleWindow.start}} | Fecha de inicio planificada para la actualización | Actualización de mantenimiento |
| {{content.scheduleWindow.end}} | Fecha de finalización planificada para la actualización | Actualización de mantenimiento |
| {{content.severity}} | Puntuación de gravedad | Incidencia |
| {{content.subCategoryName}} | Componentes afectados | Incidencia |
| {{content.title}} | Título de mensaje | Actualización de mantenimiento e incidencia |
| {{region}} | Región afectada | Actualización de mantenimiento e incidencia |
| {{status}} | Estado de la actualización | Actualización de mantenimiento |
| {{type}} | Actualización o incidencia | Actualización de mantenimiento e incidencia |
{: caption="Tabla 7. Valores de la sección de carga útil de incidencia y de mantenimiento" caption-side="top"}


{: #threshpayload}

| **Valor de IBM** | **Descripción** | **Tipo de suceso** |
|----------------|----------------|------------------------|
| {{content.org_quota}} | Umbral de cuota de organización | Umbral |
| {{content.physical_disk}} | Umbral de disco físico | Umbral |
| {{content.physical_memory}} | Umbral de memoria física | Umbral |  
| {{content.reserved_disk}} | Umbral de disco reservado | Umbral |
| {{content.reserved_memory}} | Umbral de memoria reservada | Umbral |
{: caption="Tabla 8. Valores de la sección de carga útil del umbral" caption-side="top"}

Cuando se guarda su suscripción de notificaciones, recibe notificaciones a través del método que haya configurado. Las notificaciones se siguen publicando en las siguientes ubicaciones:  
 * En la página Estado para incidencias
 * En la página Estado para sucesos planificados de actualización disruptiva de mantenimiento
 * En el área Notificaciones de la página Administración para actualizaciones de mantenimiento

Puede seleccionar cualquier suscripción de notificaciones guardada, ver la actividad reciente o realizar cambios según necesite. Pulse para expandir la entrada de una actividad reciente para ver los detalles del historial.

## Actualizaciones de mantenimiento
{: #oc_schedulemaintenance}

Puede ver las actualizaciones de mantenimiento planificadas y pendientes, si tiene permiso de superusuario (`ops.admin`) haciendo clic en **ADMINISTRACIÓN &gt; INFORMACIÓN DEL SISTEMA &gt; *Número* de pendientes** para acceder a la página **Actualizaciones del sistema**.  Todos los usuarios de su entorno pueden ver los sucesos de actualización de mantenimiento disruptiva planificados pulsando **Soporte** &gt; **Estado**.

**Nota**: consulte la siguiente sección sobre la [configuración de ventanas de mantenimiento aprobadas con anterioridad](index.html#preapprovedmaintenance) para empezar. Estas ventanas deben establecerse para que IBM planifique el mantenimiento para el entorno.

<dl>
<dt>Actualizaciones no disruptivas</dt>
<dd>Una actualización no disruptiva no afecta al entorno, a las aplicaciones en ejecución o al acceso de los usuarios a las aplicaciones. Este tipo de actualización no requiere aprobación caso por caso y se aplicará durante las ventanas de mantenimiento disponibles y con aprobación previa que establece desde la página Actualizaciones del sistema.</dd>
<dt>Actualizaciones disruptivas</dt>
<dd>Una actualización disruptiva puede afectar al entorno, a las aplicaciones en ejecución o al acceso de los usuarios a las aplicaciones. Debe planificar y aprobar cada una de estas ventanas de mantenimiento dentro de la ventana de mantenimiento de 21 días asignada. Puede seleccionar la fecha y hora de despliegue sugeridas, la opción para cualquier ventana ya aprobada, o bien abrir el calendario y seleccionar tres fechas y horas específicas para que IBM pueda elegir la planificación de la actualización.</dd>
</dl>


### Configuración de ventanas de mantenimiento con aprobación previa
{: #preapprovedmaintenance}

Está planificada la ejecución de actualizaciones de mantenimiento no disruptivas durante las ventanas de tiempo preaprobadas. De forma predeterminada, se crean para el sistema dos ventanas de actualizaciones disponibles cada semana. Estas ventanas se suelen establecer para recurrir durante la noche de cada sábado y domingo. Puede cambiar los valores predeterminados de una de las siguientes formas:
 * Edite las ventanas de actualización predeterminadas seleccionando un día distinto o una hora de inicio distinta, o los dos
 * Cree una ventana de actualización y, a continuación, suprima la ventana de actualización predeterminada

Para guardar los cambios, debe seguir cumpliendo el mínimo de tiempo necesario cada semana.

Debe establecer un mínimo de 12 horas disponibles a la semana durante un mínimo de dos días durante cada semana. Por ejemplo, puede establecer ventanas de seis horas en dos días independientes, o puede establecer ventanas de cuatro horas en tres días independientes. Para asegurarse de que las ventanas proporcionan el tiempo suficiente para aplicar una actualización, cada ventana debe tener una duración mínima de 4 horas.  

**Nota**: los usuarios con permiso de superusuario (`ops.admin`) son los únicos que pueden planificar y aprobar actualizaciones de mantenimiento.

1. Vaya a **ADMINISTRACIÓN &gt; INFORMACIÓN DEL SISTEMA &gt; *Número* de pendientes &gt; Gestionar disponibilidad**.
2. Expanda la sección **Gestionar ventanas de actualización disponibles**.
3. Pulse **Añadir nuevo** ![Añadir nuevo](images/add-new.png).
4. Establezca la primera ventana de disponibilidad seleccionando la frecuencia, duración y hora de inicio para la ventana.
5. Opcional: seleccione **Marcar como preferido** si le gustaría establecer su ventana de disponibilidad recurrente como la hora preferida para que se planifiquen los despliegues. Las ventanas preferidas tienen prioridad, siempre que sea posible.
6. Pulse **Enviar**.
7. Repita este proceso hasta que haya satisfecho los requisitos mínimos para las ventanas semanales.

### Configuración de ventanas de mantenimiento no disponibles
{: #blockpreapprovedmaintenance}

Puede elegir establecer ventanas de tiempo de actualización no disponibles específicas en las que el entorno no está disponible para actualizaciones de mantenimiento no disruptivas. Por ejemplo, puede elegir vacaciones o un fin de semana con mucho tráfico cuando no desea que se aplique ningún mantenimiento para garantizar que las aplicaciones están disponibles para los usuarios.

Debe establecer un mínimo de 12 horas disponibles a la semana durante un mínimo de dos días durante cada semana. Si intenta crear una ventana de actualización no disponible, es posible que no pueda guardar los cambios si esta ventana nueva hace que el sistema caiga por debajo del mínimo semanal requerido. En este caso, primero debe eliminar algunas de las ventanas de actualización no disponible existentes o añadir más ventanas de actualización disponible antes de guardar la nueva ventana de actualización no disponible. Consulte [Configuración de ventanas de mantenimiento con aprobación previa](index.html#preapprovedmaintenance) para obtener más información.

1. Vaya a **ADMINISTRACIÓN &gt; INFORMACIÓN DEL SISTEMA &gt; *Número* de pendientes &gt; Gestionar disponibilidad**.
2. Expanda la sección **Gestionar ventanas de actualización no disponibles**.
3. Pulse **Añadir nuevo** ![Añadir nuevo](images/add-new.png).
4. Establezca una ventana no disponible seleccionando la frecuencia, duración y hora de inicio para la ventana.
5. Pulse **Enviar**.

### Planificación y aprobación de actualizaciones
{: #scheduleandapprove}

Después de establecer las ventanas de mantenimiento con aprobación previa, las actualizaciones no disruptivas se planificarán automáticamente durante estas horas. La aprobación explícita para estos tipos de actualizaciones no es necesaria. Sin embargo, puede ver los detalles para cada actualización de mantenimiento incluyendo lo que se está actualizando, el tiempo que tardará la actualización y cuando se ha planificado la actualización.

Para ver los detalles para una actualización no disruptiva, realice los siguientes pasos:

1. Vaya a **ADMINISTRACIÓN &gt; INFORMACIÓN DEL SISTEMA &gt; *Número* de pendientes**.
2. Identifique todas las filas que tengan **Planificación de cliente necesaria** establecida en **No**.
3. Seleccione la fila para esa actualización para ver los detalles.

Una actualización disruptiva puede afectar al entorno, a las aplicaciones en ejecución o al acceso de los usuarios a las aplicaciones. Debe planificar y aprobar cada una de estas ventanas de mantenimiento dentro de la ventana de mantenimiento de 21 días asignada. Puede seleccionar la fecha y hora de despliegue sugeridas, la opción para cualquier ventana ya aprobada, o bien abrir el calendario y seleccionar tres fechas y horas específicas para que IBM pueda elegir la planificación de la actualización.

Para las actualizaciones disruptivas que no requieran su aprobación, realice los siguientes pasos:

1. Vaya a **ADMINISTRACIÓN &gt; INFORMACIÓN DEL SISTEMA &gt; *Número* de pendientes**.
2. Identifique todas las filas que tengan **Planificación de cliente necesaria** establecida en **Sí**.
3. Seleccione la fila para esa actualización para revisar los detalles para la actualización incluida la descripción de la actualización, la fecha y hora sugerida para la actualización, los componentes afectados y la duración para la actualización.
4. Seleccione **Planificar y aprobar**.
5. Elija entre las siguientes opciones: **Fecha sugerida**, **Fechas alternativas** o **Cualquier ventana ya aprobada**. Si selecciona **Fechas alternativas**, puede abrir el calendario para seleccionar tres opciones entre las que IBM pueda elegir.
6. Opcional: en la lista de fechas alternativas seleccionadas en el calendario, seleccione las que desee establecer como fechas preferidas para el despliegue. Cada fecha seleccionada se anota como preferida para el desplegador que planifica el despliegue. IBM intentará planificar el mantenimiento durante las ventanas de actualización preferidas.
7. Seleccione **Enviar** cuando haya finalizado.

Basándose en la selección, la actualización se planifica para el despliegue durante la fecha sugerida que acepte, durante una de las ventanas con aprobación previa, o en una de las fechas y horas seleccionadas. Cuando la actualización ha sido planificada para el despliegue por IBM, verá la fecha planificada reflejada en los detalles para la actualización en la página **Actualizaciones del sistema**. Puede volver a plantificar un despliegue ya planificado únicamente si queda un día (24 horas) para la fecha y hora de inicio planificadas. Una vez que haya vuelto a plantificar un despliegue, no podrá volver a planificarlo de nuevo.


## Visualización de la información del sistema
{: #oc_system}

Para ver información del sistema, pulse **ADMINISTRACIÓN &gt; INFORMACIÓN DEL SISTEMA**.

Puede visualizar diversas secciones, incluidas las actualizaciones del sistema pendientes, la información general del sistema, la información de API y CLI, y
los detalles de configuración de LDAP.

### Actualizaciones del sistema pendientes

En la sección Actualizaciones, puede ver el número de notificaciones de actualizaciones pendientes
que requieren acción por su parte. Hay dos tipos que se pueden ver:

<dl>
<dt>Actualizaciones no disruptivas</dt>
<dd>Una actualización no disruptiva no afecta al entorno, a las aplicaciones en ejecución o al acceso de los usuarios a las aplicaciones. Este tipo de actualización no requiere aprobación caso por caso. Estas actualizaciones se aplican en las ventanas de mantenimiento disponibles y con aprobación previa que establece desde la página Actualizaciones del sistema.</dd>
<dt>Actualizaciones disruptivas</dt>
<dd>Una actualización disruptiva puede afectar al entorno, a las aplicaciones en ejecución o al acceso de los usuarios a las aplicaciones. El usuario tiene la capacidad de planificar y aprobar cada una de estas actualizaciones de mantenimiento con la ventana de mantenimiento de 21 días asignada para asegurarse de que la actualización no se aplica durante las horas empresariales críticas. Puede seleccionar una fecha y hora de despliegue sugerida basándose en las ventanas de actualización con aprobación previa, o puede seleccionar dos horas y fechas adicionales para que IBM elija una de ellas para aplicar la actualización.</dd>
</dl>

Para obtener más información sobre el establecimiento de ventanas de mantenimiento preaprobadas y el establecimiento de fechas no disponibles específicas para mantenimiento, consulte [Actualizaciones de mantenimiento](index.html#oc_schedulemaintenance).

### Información general del sistema

En la sección Información general, puede ver la siguiente información:

- Información básica sobre el build de {{site.data.keyword.Bluemix_notm}}.
- Información de API (versión, URL, región y enlace a la documentación de CLI).
- Información de dominio compartido sobre el sistema y el servicio.
- Estadísticas sobre el número total de apps, usuarios y organizaciones.

### Detalles de configuración de LDAP

En la sección Detalles de la configuración de LDAP, puede seleccionar el servidor de LDAP
y ver información sobre las correlaciones de usuarios y grupos. Si utiliza el WebID de
{{site.data.keyword.IBM}}, se indica en esta sección.

## Visualización de uso e informes
{: #oc_resource}

Puede ver distintos tipos de información de uso para su instancia local o dedicada y cuenta de {{site.data.keyword.Bluemix_notm}}. También puede descargar y ver informes de seguridad y registros para la instancia de {{site.data.keyword.Bluemix_notm}}.

- Información de recursos, incluyendo espacio en disco, uso de CPU, uso de red y tiempos de respuesta medios. Consulte [Uso de recursos](index.html#resourceusage).
- Uso de cuenta por org, incluyendo el número de apps de tiempo de ejecución con uso, el número total de GB-horas de tiempo de ejecución y el número de instancias de servicio con uso. Consulte [Uso de la cuenta](index.html#accountusage).
- Uso de cuota de memoria de org, memoria de app asignada en base al total de la cuota de memoria usada y una vista del uso GB-hora por app para una org específica. También puede ver el uso de la cuota para todas las organizaciones de la página Administración de organización en la sección **Supervisión de cuota**. Consulte [Administración de organización](../admin/index.html#orgusage).


### Uso de recursos
{: #resourceusage}

Para ver información de uso de recurso, pulse **ADMINISTRACIÓN &gt; Uso de recursos**.

En la sección **Uso de recursos**, puede ver la siguiente información:

- Información de uso de recurso, como, por ejemplo, la cantidad de memoria y espacio en disco que se puede reservar y la cantidad disponible físicamente, así como la cantidad de memoria y espacio en disco reservada actualmente y la cantidad utilizada físicamente.  Puede ver información sobre el promedio de uso de la CPU de todos los agentes de ejecución de gotas (DEA). Para obtener información más detallada sobre el uso de la memoria, el disco y la CPU, consulte [Detalles de memoria, disco y CPU](index.html#resourceusagedetails).
- Información sobre uso de red correspondiente a entrada y salida de ancho de banda durante las últimas 6 horas o el último día. Los datos que se muestran se basan en la suma del tráfico de entrada y de salida de las redes públicas y privadas.
- Tiempo de respuesta promedio para {{site.data.keyword.Bluemix_notm}} durante los últimos 10 minutos, la última hora o el último día.
- Promedio de transacciones por segundo para {{site.data.keyword.Bluemix_notm}} durante los últimos 10
minutos, hora y día.


#### Detalles de memoria, disco y CPU del sistema
{: #resourceusagedetails}

En la sección **Uso de recursos**, puede ver un resumen de las cantidades **Reservadas** y **Físicas** para la memoria y el disco.    
	<dl>
	<dt><strong>Físico</strong></dt>
	<dd>La cantidad de memoria o espacio en disco adquirida para su entorno.</dd>
	<dt><strong>Reservado</strong></dt>
	<dd>La cantidad total de memoria o espacio en disco disponible para su reserva por parte de todas las aplicaciones desplegadas y en ejecución del entorno. Puesto que las aplicaciones no suelen utilizar toda la memoria que tienen reservada, el valor físico suele ser inferior al valor reservado.</dd>
	</dl>

Además de la representación gráfica, podrá ver el porcentaje de memoria y espacio en disco que utiliza su entorno. También puede ver la cantidad reservada y la cantidad física, en GB, del uso actual comparado con la cantidad disponible.

Para ver el uso de memoria, disco, o CPU mediante DEA, pulse **Desglose**.  

Para ver información más detallada sobre el uso de memoria física y reservada o el uso del disco en el tiempo, pulse **Historial.** Puede especificar el marco temporal para ver un intervalo semanal o mensual. La vista Uso histórico muestra un gráfico del uso de memoria o de disco durante el tiempo que elija.  
	<dl>
	<dt><strong>Límite reservado</strong></dt>
	<dd>El límite reservado, que se muestra como una línea de puntos horizontal, es la cantidad total de memoria o de espacio de disco que se puede reservar colectivamente para todas las aplicaciones que se ejecutan en el entorno.</dd>
	<dt><strong>Reservado</strong></dt>
	<dd>El área reservada muestra la memoria o el espacio de disco reservado colectivamente en estos momentos para todas las aplicaciones que se ejecutan en el entorno.
	<p>Para ver las organizaciones que han reservado la mayor parte de la memoria en un momento determinado, pase el puntero del ratón sobre el punto del área reservada asociado con el momento en cuestión. A continuación, puede pulsar una organización en el gráfico circular mostrado para ver más información sobre la organización en cuestión.</p></dd>
	<dt><strong>Límite físico</strong></dt>
	<dd>El límite físico, que se muestra como una línea de puntos horizontal, muestra la cantidad de memoria física o de espacio de disco adquirido para su entorno.</dd>
	<dt><strong>Físico</strong></dt>
	<dd>El área Físico muestra la cantidad de memoria o espacio de disco que se está utilizando en realidad.</dd>
	</dl>
	
#### Detalles de utilización del servicio
{: #servicesresourceusage}

El separador **Servicio** muestra la utilización total del servicio con relación a la capacidad máxima que tiene para un servicio dedicado. Por ejemplo, si tiene un servicio Cloudant dedicado, y está utilizando 500 GB de los 1000 GB que tiene como capacidad disponible, verá un gráfico que mostrará que está utilizando un 50% del total de su capacidad. El color del gráfico cambia en base a lo cerca que está a su límite de capacidad. El color amarillo indica que ha utilizado entre el 70% y el 84% de su capacidad, y el color rojo se utiliza cuando llega al 85% o más de su capacidad disponible. 

**Nota**: Actualmente, la información de consumo del servicio podría no estar disponible en todos los entornos. Esta característica está disponible para Cloudant, MessageHub, API Connect y Session Cache. 


### Uso de cuenta
{: #accountusage}

Puede ver el uso mensual de su cuenta para su entorno local o dedicado. Puede utilizar estos datos para identificar cuánto cargar
a organizaciones específicas según su uso. Todos los usuarios de la consola administrativa que tienen asignado el permiso **Usuarios** con acceso de **lectura** pueden ver los datos de uso de la cuenta. Además, los gestores de facturación de las organizaciones pueden ver los datos del uso de cuenta de las organizaciones, incluso si el gestor de facturación no tiene asignado el permiso **Usuarios** de la consola administrativa. Como administrador de la consola administrativa (permiso de superusuario), puede asignar el rol de gestor de facturación para organizaciones pulsando **Cuenta** &gt; **Gestionar organizaciones**.

Para ver los datos de uso de la cuenta, siga estos pasos:

<ol>
<li>Pulse <strong>Cuenta</strong> &gt; <strong>Panel de control de uso</strong>.</li>
<li>Seleccione la organización para la que quiere ver los datos.</li>
<li>Puede ver los detalles de uso de las categorías siguientes:
<ul>
<li>Apps de tiempo de ejecución que tienen uso</li>
<li>Uso total de apps de tiempo de ejecución en GB-horas</li>
<li>Instancias de servicio que tienen uso</li>
</ul>
</li>
<li>Opcional: ver sus datos para un mes concreto usando el menú <strong>Su actividad de nube</strong> para seleccionar el mes que quiera.</li>
<li>Opcional: pulse <strong>EXPORTAR DATOS</strong>, y seleccione <strong>CSV</strong> o <strong>JSON</strong> para exportar sus datos para el
mes seleccionado a un archivo <code>CSV</code> o <code>JSON</code>.</li>
</ol>

También puede ver el uso mensual y los cargos asociados al nivel de cuenta para sus ejecutables, apps y servicios sindicados desde
el {{site.data.keyword.Bluemix_notm}} público. Puede utilizar estos datos para identificar cuánto cargar
a organizaciones específicas según su uso.

<ol>
<li>Pulse <strong>Cuenta</strong> &gt; <strong>Panel de control de uso</strong>.</li>
<li>Pulse <strong>Público</strong>.</li>
<li>Seleccione la organización para la que quiere ver los datos.</li>
<li>Puede ver los detalles de uso de las categorías siguientes:
<ul>
<li>Apps de tiempo de ejecución que tienen uso</li>
<li>Uso total de apps de tiempo de ejecución en GB-horas</li>
<li>Instancias de servicio que tienen uso</li>
<li>Un resumen de cargo para todos los ejecutables sindicados, servicios y apps</li>
</ul>
</li>
<li>Opcional: ver sus datos para un mes específico, seleccionando el mes que quiera del gráfico de barras. Los datos del mes actual
se muestran de forma predeterminada.</li>
<li>Opcional: pulse <strong>EXPORTAR DATOS</strong>, y seleccione <strong>CSV</strong> o <strong>JSON</strong> para exportar sus datos para el
mes seleccionado a un archivo <code>CSV</code> o <code>JSON</code>.</li>
</ol>


### Uso de la organización
{: #orgusage}

Para ver el uso por organización, pulse **ADMINISTRACIÓN &gt; ADMINISTRACIÓN DE ORGANIZACIÓN**, y luego seleccione una
organización de la **Lista de organizaciones**. En la página **Gestionar organizaciones** para la
organización que ha seleccionado, puede ver la información de uso siguiente:

- Número de servicios que hay actualmente en uso.
- Número de rutas que hay actualmente en uso.
- Gráfico de cuota de memoria que muestra qué parte de la cuota está en uso y qué parte no se usa actualmente.
- Gráfico de asignación de aplicaciones que muestra qué aplicaciones se incluyen en la cuota de memoria utilizada.
- Gráfico de uso de aplicaciones medidas que muestra un informe de tres meses de los GB-horas usados por app desplegada. Puede
seleccionar la **Vista de lista** para ver los datos de todas las aplicaciones, incluyendo la asignación de memoria por app y
el uso de GB-hora medido para los últimos tres meses.

Para obtener más información sobre la visualización del uso por organización, el ajuste de planes de cuota y la gestión de sus
organizaciones, consulte [Administración de organizaciones](../admin/index.html#oc_organizations).

### Reports
{: #oc_report}

Puede ver informes de seguridad y registros, como por ejemplo DataPower&trade;, el cortafuegos y la auditoría de inicio de sesión, para
la instancia de {{site.data.keyword.Bluemix_notm}}. Para visualizar informes y registros, pulse **ADMINISTRACIÓN &gt; INFORMES Y REGISTROS**.

Seleccione una de las opciones siguientes:

- Puede seleccionar fechas de inicio y finalización en los campos para filtrar los informes y registros que se muestran.
- Puede expandir y visualizar distintos informes desde el panel de navegación.
- Puede buscar dentro del conjunto de informes y registros. La búsqueda se aplica a los nombres de informes y al contenido de texto que se incluye en los informes y los registros. También puede optar por filtrar
la búsqueda por **Sucesos de administración**, **Informes de DataPower**, **Cortafuegos** y **Auditoría
de inicio de sesión**.
- Cuando visualice un informe o un registro, puede pulsar el icono ![Descargar](images/icon_download.png)
para descargar el informe.

La tabla siguiente muestra la lista de los informes de seguridad generados para {{site.data.keyword.Bluemix_notm}} local y {{site.data.keyword.Bluemix_notm}} dedicado. La mayoría de los informes se generan a diario. Sin embargo, los informes de cifrado y sucesos de gestión de claves se generan mensualmente. Todos los informes se conservan 90 días en la consola administrativa para su recuperación. Transcurridos 90 días, los informes están disponibles fuera de línea desde {{site.data.keyword.Bluemix_notm}} durante 9 meses. En total, los informes están disponibles para su recuperación un máximo de un año.


{: #ld_table9}

| **Categoría** | **Informe** | **Descripción** |      
|-----------------|-------------------|---------------------|
| Cortafuegos | Inicios de sesión de cortafuegos | Sucesos relacionados con el inicio de sesión del administrador en los dispositivos de cortafuegos Vyatta. |
| Cortafuegos | Denegaciones de cortafuegos | Sucesos generados por los dispositivos cortafuegos Vyatta cuando se deniega una solicitud de acceso acuerdo con las reglas vigentes del cortafuegos. |
| Sucesos de inicio de sesión del administrador de {{site.data.keyword.Bluemix_notm}} | Inicio de sesión de los administradores de {{site.data.keyword.Bluemix_notm}} | Sucesos generados por el sistema operativo cuando un administrador inicia una sesión SSH en cada sistema {{site.data.keyword.Bluemix_notm}}. |
| Sucesos de inicio de sesión de desarrollador de apps de {{site.data.keyword.Bluemix_notm}} | Inicio de sesión de desarrolladores de apps de {{site.data.keyword.Bluemix_notm}} | Sucesos generados por el componente de inicio de sesión de la plataforma {{site.data.keyword.Bluemix_notm}} cuando un usuario de la plataforma {{site.data.keyword.Bluemix_notm}} inicia sesión mediante la línea de mandatos, las API REST o la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. |
| Sucesos administrativos del administrador de {{site.data.keyword.Bluemix_notm}} | Sucesos administrativos del sistema operativo de los administradores de {{site.data.keyword.Bluemix_notm}} | Sucesos generados por el sistema operativo cuando un administrador realiza una acción durante una sesión de trabajo actual. |
| Sucesos administrativos de desarrollador de apps de {{site.data.keyword.Bluemix_notm}} | Sucesos administrativos de {{site.data.keyword.Bluemix_notm}} (Cloud Foundry) | Sucesos relacionados con operaciones realizadas por el usuario de la plataforma {{site.data.keyword.Bluemix_notm}} utilizando la línea de mandatos, las API REST o la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. |
| Sucesos administrativos de la base de datos del administrador de {{site.data.keyword.Bluemix_notm}} | Sucesos administrativos de la base de datos | Sucesos relacionados con las operaciones realizadas por un administrador de bases de datos en las bases de datos internas de {{site.data.keyword.Bluemix_notm}}. |
| Sucesos de administración | Sucesos de gestión de usuarios | Sucesos relacionados con acciones de gestión de usuarios realizadas en la página Administración. |
| Sucesos de administración | Catalog | Sucesos relacionados con cambios en el catálogo de servicios. |
| Sucesos de administración | Sucesos de gestión de informes de seguridad | Sucesos relacionados con acciones de gestión de informes de seguridad realizadas en la página Administración. |
| Revisiones de acceso | Informe de revisiones de acceso | Revisiones para accesos privilegiados. |
| Gestión de cambios | Gestión de cambios de software | Actividad de gestión de cambios. |
| Gestión de claves | Gestión de certificados SSL personalizados | Certificados SSL personalizados cargados y almacenados. |
| Cifrado | Cifrado data-in-transit (datos en tránsito) | Cifrado data-in-transit (datos en tránsito) configurado. |
| Antivirus | Informe de exploración de antivirus | Software antivirus vigente. |
| Gestión de arreglos de software | Informe de app de parches | Arreglos de software aplicados. |
| Gestión de incidentes de seguridad | Informe de solución de incidentes de seguridad | Pruebas de incidentes de seguridad para la gestión de incidentes de seguridad. |
{: caption="Tabla 9. Lista de informes de seguridad" caption-side="top"}

## Visualización del estado
{: #oc_status}

Puede ver el estado para el entorno {{site.data.keyword.Bluemix_notm}} y para la consola de administración.

### Estado de entorno de {{site.data.keyword.Bluemix_notm}}

Puede supervisar el estado para su instancia de {{site.data.keyword.Bluemix_notm}} utilizando la página Estado de {{site.data.keyword.Bluemix_notm}}. Pulse **Soporte** &gt; **Estado**.

La página Estado es el recurso central para buscar notificaciones y anuncios sobre sucesos clave que afectan a la plataforma {{site.data.keyword.Bluemix_notm}} y a los servicios principales de {{site.data.keyword.Bluemix_notm}}. Puede suscribirse a un hilo RSS para recibir notificaciones de forma que no tenga que comprobar si se han publicado. Para obtener más información sobre la página Estado y la configuración del hilo RSS, consulte [Visualización de {{site.data.keyword.Bluemix_notm}}](../support/index.html#viewing-bluemix-status).

### Estado de consola de administración

Después del despliegue inicial del entorno {{site.data.keyword.Bluemix_notm}}, se lleva a cabo automáticamente una comprobación de verificación en los componentes que se utilizan para administrar el entorno. Puede ir a la página Comprobación de verificación de consola de administración para comprobar el estado de los componentes después de ejecutar la comprobación de verificación. Para acceder a la página, vaya a <code>https://console.&lt;subdominio&gt;.bluemix.net/check</code>, donde `<subdominio>` es el nombre de la instancia local o dedicada.

Puede ejecutar una verificación en cualquier momento. Debe iniciar la sesión para seleccionar la opción para ejecutar la verificación. Si encuentra errores al añadir un usuario, editar una organización o gestionar los servicios, ejecute esta comprobación para identificar si cualquiera de los componentes está fallando o está desconectado. Puede abrir una incidencia de soporte con la información de la comprobación para resolver el problema rápidamente.

## Gestión del catálogo
{: #oc_catalog}

Puede gestionar qué servicios de {{site.data.keyword.Bluemix_notm}} podrán ver los usuarios en el Catálogo de {{site.data.keyword.Bluemix_notm}}. Pulse **ADMINISTRACIÓN &gt; GESTIÓN DE CATÁLOGOS**.

Seleccione un mosaico de servicio para editar la visibilidad del plan de servicio. Para editar la visibilidad, seleccione una de las siguientes opciones:

- Para mostrar el servicio oculto para que esté visible para los usuarios en el
Catálogo, seleccione **HABILITAR TODOS LOS PLANES**.
- Para ocultar el servicio de los usuarios en el Catálogo de {{site.data.keyword.Bluemix_notm}},
seleccione **INHABILITAR TODOS LOS PLANES**.
- Para controlar la visibilidad de un plan individual, seleccione el nombre del plan y utilice el menú desplegable para seleccionar **Habilitar para todas las organizaciones**, **Inhabilitar para todas las organizaciones** o **Habilitar plan para organizaciones específicas**.

<!-- staging only start -->

También puede gestionar el orden de prioridad de los paquetes de compilación que deben elegirse en base a la compatibilidad para los desarrolladores cuando crean apps.

1. Vaya a **ADMINISTRACIÓN &gt; GESTIÓN DE CATÁLOGOS**
2. Vaya a la sección **Compute**.
3. Seleccione **Prioridad de paquete de compilación**.
4. Seleccione la opción de paquete de compilación al que desee dar una mayor o menor prioridad dentro de la lista.
5. Con la opción seleccionada, utilice las flechas para mover la opción dentro de la lista.

<!-- staging only end -->

### Registro de un intermediario de servicio
{: #servicebrokerui}

Si tiene un servicio que quiere mostrar en su catálogo de {{site.data.keyword.Bluemix_notm}}, debe implementar y registrar un [intermediario de servicio ![icono de enlace externo](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/services/api.html){: new_window}. Tras registrar su intermediario, puede elegir las organizaciones que pueden tener acceso al
servicio en su instancia dedicada o local.

Los métodos para trabajar con su intermediario de servicio varían según la cantidad de servicios que gestiona, o si ya se ha registrado con
{{site.data.keyword.Bluemix_notm}}.

- Si su intermediario de servicio gestiona un servicio, puede utilizar la interfaz de usuario para registrarlo tras haber implementado
la [API de intermediario de servicio ![icono de enlace externo](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/services/api.html){: new_window}. Consulte [Registro de un intermediario de servicio que gestiona un servicio](index.html#registerbrokerui).
- Si su intermediario de servicio gestiona varios servicios, utilice la CLI cf con el plug-in [CLI admin de {{site.data.keyword.Bluemix_notm}}](../cli/plugins/bluemix_admin/index.html) (submandato `ba`) o use la [API de servicio personalizado](index.html#servicebrokerapi).
- Si su intermediario de servicio ya está registrado y quiere actualizarlo o suprimirlo, utilice la CLI cf con el plugin [CLI admin de {{site.data.keyword.Bluemix_notm}}](../cli/plugins/bluemix_admin/index.html) (submandato `ba`) o use la [API de servicio personalizado](index.html#servicebrokerapi).

#### Registro de un intermediario de servicio que gestiona un servicio
{: #registerbrokerui}

<!-- staging only start -->

Revise la siguiente información y complete los pasos para registrar el intermediario de servicio:

**Antes de empezar**: <a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">Implemente la API del intermediario de servicio de Cloud Foundry <img src="../icons/launch-glyph.svg" alt="icono de enlace externo"></a> para habilitar la comunicación entre su servicio y {{site.data.keyword.Bluemix_notm}}. La API del intermediario de servicio es un conjunto de puntos finales de REST que {{site.data.keyword.Bluemix_notm}} consume.

Cuando implementa el intermediario de servicio, en la respuesta JSON de <code>GET /v2/catalog</code>, debe proporcionar
las definiciones para su servicio y planes de servicio, incluyendo la información de servicio que quiere visualizar. Por ejemplo, revise
el JSON de ejemplo siguiente de la respuesta del catálogo (GET):

```
{
"services":[
   {
      "bindable":true,
      "description":"Cool Service is an analytics and data warehousing solution.",
      "id":"cool-service-id",
      "name":"coolservice",
      "metadata":{
         "displayName":"Cool Service",
         "serviceMonitorApi":"https://myservicesstatus.mybluemix.net/healthcheck/",
         "providerDisplayName":"Cool company",
         "longDescription":"Cool Service is a data warehousing and analytics solution. You can quickly move your data into a next-generation columnar in-memory database and start running complex analytical queries.",
         "bullets":[
            {
               "title":"Fast and Simple",
               "description":"Cool Service uses dynamic in-memory columnar technology and innovations, such as parallel vector processing and actionable compression to rapidly scan and return relevant data."
            },
            {
               "title":"Connectivity",
               "description":"Cool Service is built to let you connect easily and to all of your services and applications. You can start analyzing your data immediately with familiar tools."
            }
         ],
         "featuredImageUrl":"http://path/to/icon_64x64.png",
         "imageUrl":"http://path/to/icon_50x50.png",
         "mediumImageUrl":"http://path/to/icon_32x32.png",
         "smallImageUrl":"http://path/to/icon_24x24.png",
         "documentationUrl":"http://path/to/documentation.html",
         "instructionsUrl":"http://path/to/servicesample.md",
         "termsUrl":"http://path/to/terms_of_agreement.pdf",
         "media":[
            {
               "type":"youtube",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/youtube/video",
               "caption":"Using Cool Service in 60 Seconds"
            },
            {
               "type":"image",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/image_file.png",
               "caption":"Cool Service connects applications"
            },
            {
               "type":"video",
               "thumbnailUrl":"http://path/to/thumb.png",
               "caption":"Cool Service works with tables",
               "source":[
                  {
                     "type":"video/mp4",
                     "url":"http://path/to/video_file.mp4"
                  },
                  {
                     "type":"video/ogg",
                     "url":"http://path/to/video_file.ogg"
                  }
               ]
            }
         ]
      },
      "plans":[
         {
            "name":"smallplan",
            "description":"Dedicated schema and tablespace per service instance on a shared server. 1GB and 10GB of compressed database storage can hold up to 5GB and 50GB of uncompressed data respectively based on typical compression ratios.",
            "free":false,
            "id":"cool-service-plan-id",
            "metadata":{
               "bullets":[
                  "1 GB Min per instance. 10 GB Max per instance."
               ],
               "costs":[
                  {
                     "unitId":"INSTANCES_PER_MONTH",
                     "unit":"MONTHLY",
                     "partNumber":"D15UTLL"
                  }
               ],
               "displayName":"Small"
            }
         }
      ]
   }
]
}
```
{: codeblock}

Las siguientes tablas pueden ayudarle a rellenar el archivo JSON.


{: #ld_table10}

| **Campos JSON** | **Descripción** |
|-----------------|-----------------|
|bindable   | Un valor booleano que indica si las instancias de servicio se pueden vincular a las aplicaciones.  |
|descripción | La descripción del servicio que se muestra cuando se utiliza el mandato cf marketplace o cuando se pasa el ratón sobre el icono de servicio en el catálogo de la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. Puede añadir una única frase a la descripción. |
|name | El nombre del servicio que se muestra en la interfaz de la línea de mandatos cf. El nombre debe ser exclusivo en {{site.data.keyword.Bluemix_notm}}, debe estar en minúsculas y no puede contener espacios. No se puede cambiar el nombre del servicio una vez registrado el servicio con {{site.data.keyword.Bluemix_notm}}. |
|id  | El ID del servicio. El ID debe ser exclusivo en {{site.data.keyword.Bluemix_notm}} y debe ser un GUID (identificador exclusivo global). No se puede cambiar el ID del servicio una vez registrado el servicio con {{site.data.keyword.Bluemix_notm}}. |
|metadata | Los metadatos del plan del servicio que se muestran en el catálogo de {{site.data.keyword.Bluemix_notm}} y en la hoja de precios. El campo Metadatos es un campo opcional. Puede especificar campos adicionales para los metadatos. Consulte la tabla [Campos de metadatos](index.html#metadatafields) para obtener más información. |
|plans | Una matriz de definiciones del plan de servicio. Consulte la tabla [Campos de plan](index.html#planfields) para obtener más información. |
{: caption="Tabla 10. Campos JSON" caption-side="top"}


{: #metadatafields}

| **Valores de metadatos** | **Descripción** |
|---------------------|-----------------|
|displayName          | El nombre del plan que se muestra en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. Este nombre se muestra tanto en la página de detalles de servicio del catálogo como en la hoja de precios. Escriba en mayúsculas solo la inicial del nombre de plan. No utilice "Predeterminado" como nombre de plan predeterminado; utilice "Estándar" en su lugar. |
|providerDisplayName | El nombre del proveedor de servicios |
|longDescription | La descripción detallada del servicio. Considere la posibilidad de utilizar dos frases en el caso de una descripción larga. |
|plans                | Una matriz de definiciones del plan de servicio. Cada entrada de matriz del campo de planes consta de los siguientes campos: nombre, descripción, gratuito, ID y metadatos. Consulte la tabla [Campos de plan](index.html#planfields) para obtener más información. |
|bullets | Una matriz de series de caracteres que se muestra para un servicio. Puede utilizar viñetas (bullets) para proporcionar información adicional a la descripción larga. El campo bullets debe incluir al menos dos elementos de viñeta. Cada viñeta incluye el campo título y descripción. |
|imageUrl | El URL de una imagen PNG grande (50 x 50 píxeles). |
|smallImageUrl | El URL de una imagen PNG pequeña (24 x 24 píxeles). |
|mediumImageUrl | El URL de una imagen PNG mediana (32 x 32 píxeles). |
|featuredImageUrl | El URL de imagen destacada (64 x 64 píxeles). |
|documentationUrl | El URL de la documentación sobre el servicio. |
|termsUrl | El URL a los archivos PDF que contienen las condiciones del acuerdo. |
|media (opcional) | Una matriz de elementos para visualizar los vídeos y las capturas de pantalla que incorpora el servicio en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. Un elemento de soporte que contiene los siguientes campos: type (imagen, youtube, vídeo), thumbnailUrl (el URL de la imagen de vista previa del elemento de soporte), url (el URL de la captura de pantalla o del vídeo de YouTube), source (los orígenes de los vídeos que no están alojados en YouTube. El "tipo" de fuente del vídeo debe estar soportado por HTML5. Incluye el "tipo" y el "url" del vídeo)y caption (el título del elemento de soporte. Los títulos resultan útiles para las personas con discapacidades para entender los elementos de soporte).. |
|serviceKeysSupported | Un valor booleano que indica si se admite la API de las claves de servicio. La API de las claves de servicio se utiliza para habilitar un servicio que se utilizará fuera de {{site.data.keyword.Bluemix_notm}}. El valor predeterminado es false. |
|plan_updateable | Un valor booleano que indica si cambia el plan de soporte del servicio. El valor predeterminado es false. |
|embeddableDashboard (opcional) | Un campo que indica cómo se muestra el panel de control del servicio en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. Si no especifica este campo, el panel de control se incorpora, pero está restringido a una anchura mínima de 960px, y el panel de instrumentos tiene relleno horizontal adicional alrededor de la trama de información. Puede utilizar los valores true, false, drilldown o launch. Puede utilizar los siguientes campos para este valor: true, false, drilldown y launch.  |
|notCreatable (opcional) | Un valor booleano que indica si las instancias del servicio se pueden crear desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} y desde la interfaz de línea de mandatos cf. El valor true significa que las instancias de servicio no se pueden crear desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} ni desde la interfaz de línea de mandatos cf. El valor predeterminado es false. |
|notCreatableMessage (opcional) | Un mensaje que se muestra en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} si no se pueden crear instancias de servicio. Si no especifica este campo, se mostrará el siguiente mensaje: Para que se le avise cuando está disponible, confirme su dirección de correo electrónico o escriba una nueva dirección. |
|notCreatableRobotMessage (opcional) | Un mensaje que se muestra en formato de bocadillo en la página de detalles del servicio en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. El mensaje se utiliza para indicar que un servicio puede tener un problema u otro motivo que provoque que no esté disponible. Puede especificar un mensaje para describir el motivo. Si no especifica este campo, se mostrará el siguiente mensaje predeterminado: Este servicio no está disponible actualmente. |
|apiReferenceUrl (opcional) | El URL de la trama de información del área Referencia de API de la página de detalles del servicio en el Catálogo. Si no se utiliza para la página de detalles del servicio en el catálogo, puede introducir el valor numérico asignado a la documentación de la API REST para el servicio al registrarlo en el microservicio de la documentación de la API REST de {{site.data.keyword.Bluemix_notm}}. Esto hará que se visualice la documentación de la API REST en el panel de control del servicio. |
|sdkDownloadUrl (opcional) | El URL de la página web que se abre cuando se pulsa el botón Descargar SDK. El botón Descargar SDK está en el mosaico de servicio de la página de visión general de la aplicación en el Panel de control. La página web se abre en un nuevo separador del navegador. |
|serviceMonitorApi    | El URL a una API que devuelve los datos JSON, tal como se muestra en el siguiente ejemplo, que informa del estado del servicio. Debe tener serviceMonitorApi o serviceMonitorApp en los metadatos de servicio. Consulte el siguiente ejemplo de código para ver un ejemplo. |
|serviceMonitorApp    | El URL a una aplicación que se puede desplegar en {{site.data.keyword.Bluemix_notm}} y enlazarse a un servicio para proporcionar la salida específica del estado del servicio. La aplicación debe devolver el mismo formato de datos JSON que serviceMonitorApi. Debe tener serviceMonitorApi o serviceMonitorApp en los metadatos de servicio. Consulte el siguiente ejemplo de código para ver un ejemplo. |
{: caption="Tabla 11. Campos de metadatos" caption-side="top"}


```
{
    "service": "servicename",
    "version": 1,
    "health": [
        {
            "plan": "starter",
            "status": 0,
            "serviceinput": "count(*) from healthcheck",
            "serviceoutput": "10…or error 1234 database not running",
            "responsetime": 4
        },
        {
            "plan": "enterprise",
            "status": 1,
            "serviceinput": "count(*)fromhealthcheck",
            "serviceoutput": "10…orerror1234databasenotrunning",
            "responsetime": 4
        }
    ]
}
```
{: pre}

El siguiente ejemplo muestra cómo la respuesta JSON de GET /v2/catalog está correlacionada con la página de información de servicio en el catálogo de {{site.data.keyword.Bluemix_notm}}:

![Detalles de servicio en el catálogo.](images/metadata.png "Vista de detalles del servicio de catálogo de Bluemix")


{: #planfields}

| **Valores del plan** | **Descripción** |
|---------------------|-----------------|
|name       | El nombre del plan del servicio que se utiliza en la interfaz de la línea de mandatos cf. Por ejemplo, el nombre del plan se muestra en la salida del mandato cf marketplace. El nombre del plan debe estar en minúsculas y no puede contener espacios, además debe ser exclusivo en el servicio.  |
|descripción       | La descripción del plan del servicio. La descripción se muestra después de seleccionar un plan en la página de información del servicio en el catálogo de {{site.data.keyword.Bluemix_notm}}. |
|gratuito      | Un valor booleano que indica si el plan del servicio es gratuito. El valor predeterminado es true. |
|id       | El ID del plan del servicio. El ID debe ser exclusivo y debe ser un GUID.  |
|metadatos (opcional)    | Los metadatos del plan del servicio que se muestran en el catálogo de {{site.data.keyword.Bluemix_notm}} y en la hoja de precios. El campo Metadatos es un campo opcional. Puede especificar los siguientes campos en el campo de metadatos: displayName, type (subscription, reservable, planDetails), bullets, costs (unitId, unit, partNumber) y paidOnly. Consulte la tabla [Campos de metadatos de plan](index.html#planmetadata) para obtener más información. |
{: caption="Tabla 12. Campos del plan" caption-side="top"}


{: #planmetadata}

| **Valores de metadatos de plan** | **Descripción** |
|------------------------|-----------------|
|displayName             | El nombre del plan que se muestra en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. Este nombre se muestra tanto en la página de detalles de servicio del catálogo como en la hoja de precios.   |
|type                    | El tipo de plan. En este campo puede utilizar los siguientes valores: suscripción (un plan de suscripción. El valor predeterminado es false.), reservable (un plan reservable. Este valor se utiliza solo cuando el plan es un plan de suscripción; es decir, el valor de plan.metadata.subscription es true. El valor predeterminado es false.), planDetails (descripción y cantidad detalladas de los recursos que se pueden utilizar en el plan. Este valor se utiliza solo cuando el plan es reservable; es decir, el valor de plan.metadata.reserveable es true.) |
|bullets                 | Una descripción de los recursos que se pueden utilizar con el plan. La descripción se muestra en la columna **Características** de la página de detalles de servicio del catálogo y en la hoja de precios. |
|costs                   | La información del coste del servicio se muestra en la columna Precio de la página de detalles del servicio del catálogo y en la hoja de precios. Cada entrada de matriz contiene los siguientes campos: unitId (el ID de la unidad. Utilice la forma en plural y escriba todas las letras en mayúsculas. Para los planes gratuitos, este campo es opcional), unit (la métrica utilizada para calcular los costes del servicio. El valor de este campo se utiliza en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} para representar la métrica de cargos)y partNumber (el identificador `part_number` que utiliza el sistema de facturación. Para los planes gratuitos, este campo es opcional).   |
|paidOnly (opcional)     | Un valor booleano que indica si este plan de servicio está disponible solo para cuentas de pago de {{site.data.keyword.Bluemix_notm}}. Un valor de **true** significa que el plan de servicio solo es para cuentas de pago y no se puede añadir a las cuentas de prueba. Un valor **false** significa que el plan de servicio se puede añadir tanto a la cuenta de pago como a la cuenta de prueba. El valor predeterminado es **false**.	  |
{: caption="Tabla 13. Campos de metadatos de plan" caption-side="top"}

El siguiente ejemplo muestra cómo la respuesta JSON de GET /v2/catalog está correlacionada con la página de información de servicio en el catálogo de {{site.data.keyword.Bluemix_notm}}. Específicamente, el funcionamiento de los campos de metadatos del plan descritos en el mapa de la tabla anterior a la interfaz de usuario:

![Detalles de metadatos del plan en el catálogo.](images/plan_metadata.png "Vista de valores de metadatos del plan del catálogo de Bluemix")


<!-- staging only end -->

<ol>
<li>Tras implementar la API del intermediario de servicio, acceda a <strong>ADMINISTRACIÓN</strong> &gt; <strong>GESTIÓN DEL CATÁLOGO</strong>.</li>
<li>Pulse <strong>REGISTRAR UN INTERMEDIARIO DE SERVICIO</strong>.</li>
<li>Complete el formulario especificando los valores en los campos siguientes:
<ul>
<li>Nombre de intermediario de servicio</li>
<li>URL de intermediario de servicio</li>
<li>Nombre de usuario del intermediario de servicio</li>
<li>Contraseña del intermediario de servicio</li>
</ul>
</li>
<li>Pulse <strong>CONECTAR</strong>.</li>
<li>Revise la información de su servicio, incluyendo los planes disponibles, el icono y la descripción del servicio.<br />
<p><strong>Nota</strong>: si necesita cambiar la información del catálogo para el servicio, actualice su intermediario de servicio e
inicie el proceso de registro otra vez rellenado el formulario.</p>
</li>
<li>Pulse <strong>REGISTRAR</strong>.</li>
<li>Elija para habilitar todos los planes o solo los planes específicos para su servicio. De forma predeterminada se inhabilitan
todos los planes.</li>
<li>Habilite la instancia de servicio para todas las organizaciones o para organizaciones específicas.</li>
</ol>

Ahora puede ver su servicio en la categoría Servicios personalizados en su catálogo de {{site.data.keyword.Bluemix_notm}}. Acceda a **ADMINISTRACIÓN &gt; GESTIÓN DEL CATÁLOGO**, y seleccione el mosaico en el catálogo. Puede habilitar distintos planes y editar la visibilidad del plan para sus organizaciones en cualquier momento.


## Administración de organizaciones
{: #oc_organizations}

Puede gestionar sus organizaciones creando y suprimiendo organizaciones, añadiendo o eliminando gestores para organizaciones y supervisando el uso de la cuota para tomar las mejores decisiones en su negocio.

Pulse **ADMINISTRACIÓN &gt; ADMINISTRACIÓN DE LA ORGANIZACIÓN**.

Puede expandir y visualizar diversas secciones. También puede revisar y gestionar los planes de cuotas de sus organizaciones.

### Creación de organizaciones

Para crear una organización y añadir gestores, realice los pasos siguientes:

1. Pulse <strong>CREAR ORGANIZACIÓN</strong>.
2. Especifique un nombre para la organización
3. Especifique el nombre o correo electrónico de la persona que quiera añadir como gestor. Puede añadir más de un gestor especificando y seleccionando varios nombres.
4. Pulse <strong>CREAR ORGANIZACIÓN</strong> para guardar los cambios y crear la organización.

### Creación de espacios

Puede crear espacios en la organización; por ejemplo, un espacio *dev* como entorno de desarrollo, un espacio *test* como entorno de prueba y un espacio *production* como entorno de producción. Luego puede asociar sus apps a los espacios. Complete los siguientes pasos para crear un espacio:

1. En la barra de menús, pulse **Cuenta** &gt; **Gestionar organizaciones**.
2. Seleccione la organización a la que desea añadir un espacio.
3. Pulse **Crear un espacio**.
4. Especifique un nombre de espacio.
5. Pulse **Crear**.

### Supervisión de cuota

Puede expandir la sección **Supervisión de cuota** para ver la siguiente información:

- El uso de memoria del entorno detalla el uso de memoria de todo el entorno de sistema. El gráfico muestra la siguiente información:
<ul>
<li>La memoria física que está en uso y el límite de memoria física que está disponible</li>
<li>La cuota de memoria reservada actualmente y el límite de memoria que se puede reservar</li>
<li>La cuota total de memoria de sus organizaciones</li>
</ul>
En el gráfico se muestran los siguientes tipos de uso de memoria.

	<dl>
	<dt><strong>Física utilizada</strong></dt>
	<dd>Memoria física utilizada por el entorno.</dd>
	<dt><strong>Límite físico</strong></dt>
	<dd>Memoria física total disponible en el entorno.</dd>
	<dt><strong>Cuota reservada</strong></dt>
	<dd>La suma de la memoria reservada para todas las aplicaciones desplegadas en todas las organizaciones. La suma de la cuota reservada puede superar el límite físico de memoria de su entorno. Por ejemplo, si tiene un límite de memoria física de 16 GB, puede reservar 4 GB de memoria para un total de cinco aplicaciones distintas. La cuota que se reserva sobrepasa el límite físico de memoria. Sin embargo, en muchos casos, es posible que las aplicaciones no utilicen la cuota total reservada de forma individual para cada aplicación. Además, es posible que no todas las aplicaciones utilicen su cuota total de memoria reservada a la vez.</dd>
	<dt><strong>Límite de reserva</strong></dt>
	<dd>La memoria total se puede reservar en todas las aplicaciones de su entorno.</dd>
	<dt><strong>Cuota total</strong></dt>
	<dd>La cuota de memoria total en todas las organizaciones.</dd>
	</dl>
	**Nota**: los datos se actualizan de forma automática cada 4 horas. Pulse **Volver a calcular** si desea actualizar los datos de la página antes de que se actualice de forma automática.

- Uso de memoria de la organización. En esta sección se proporcionan detalles del uso de memoria a nivel de organización. Puede ver la cuota de memoria total, la cuota que se ha reservado y la memoria física utilizada por cada organización. En el gráfico se proporciona información que aparece ordenada por la reserva de memoria más alta por organización; la organización que reserva la cantidad de memoria más elevada aparece en primer lugar de forma predeterminada. Puede ordenar por **Uso de memoria más alto** y **Asignación de memoria excesiva**.

	<dl>
	<dt><strong>Uso de memoria máximo</strong></dt>
	<dd>Utilice esta opción para identificar la organización que reserva la mayor cantidad de memoria. Ordene por uso de memoria más alto para identificar las organizaciones que han reservado la mayor cantidad de memoria. La lista está ordenada por cuota reservada. </dd>
	<dt><strong>Asignación de memoria excesiva</strong></dt>
	<dd>Utilice esta opción para identificar las organizaciones que tienen una cuota de memoria total superior a la necesaria. Ordene por uso de memoria excesivo para identificar las organizaciones que utilizan la cantidad de memoria más pequeña para la cuota que se les ha asignado. </dd>
	</dl>

### Gestión de cuotas
{: #manageorgquota}

Una cuota representa los límites de recursos para las organizaciones del entorno se asignan cuando se crea la organización. Cualquier aplicación o servicio de un espacio de la organización contribuye al uso de la cuota asignada. Siga estos pasos para gestionar la cuota de una organización:

<ol>
<li>Pulse la barra del gráfico de la organización que desea editar en la sección Uso de memoria de la organización, o bien seleccione el nombre de la organización en la sección Lista de organizaciones. En la página Información de la organización, puede cambiar el nombre de la organización y añadir o eliminar gestores.
<p><strong>Nota</strong>: Si selecciona un plan de cuotas insuficiente para el uso actual de la organización, recibirá un mensaje.</p></li>
<li>Pulse <strong>Cloud Foundry</strong> o <strong>Contenedores</strong>.  De forma predeterminada, se abrirá la página de cuota de Cloud Foundry. 
<ul>
<li>En la página Cloud Foundry, puede seleccionar un plan y ver los detalles de la cuota de los siguientes recursos:
<ul>
<li>Servicios</li>
<li>Rutas</li>
<li>Cuota de memoria</li>
<li>Asignación de aplicaciones</li>
</ul>
</li>
<li>En la página <strong>Contenedores</strong> puede asignar valores, que deben ser enteros, para los campos siguientes:
<dl class="parml">
<dt class="pt dlterm">Límite de imágenes</dt>
<dd class="pd">El número máximo de imágenes de contenedor que puede tener en su registro privado. Una imagen de contenedor es la base para cada contenedor que cree. Una imagen se crea desde un Dockerfile, que es un archivo de solo lectura que alberga el sistema operativo y la app y todas sus dependencias y describe cómo está configurado un contenedor. Las imágenes se comparten entre todos los miembros de una organización.</dd>
<dt class="pt dlterm">Asignación de memoria predeterminada</dt>
<dd>La cantidad de memoria de contenedor que se asigna automáticamente cuando se crea un nuevo espacio. Cuando cree un contenedor, deberá elegir un tamaño de contenedor. El tamaño determina la cantidad de memoria que puede utilizar el contenedor en el host y cuenta en el cálculo del límite de memoria del contenedor. </dd>
<dt class="pt dlterm">Asignación de memoria máxima</dt>
<dd>La cantidad máxima de memoria de contenedor que se puede asignar entre todos los espacios de una organización.</dd>
<dt class="pt dlterm">IP flotantes predeterminadas</dt>
<dd>El número de direcciones IP públicas que se asignan automáticamente cuando se crea un nuevo espacio. Puede enlazar direcciones IP públicas a contenedores individuales y a grupos de contenedores para que resulten accesibles desde Internet.</dd>
<dt class="pt dlterm">IP flotantes máximas</dt>
<dd>El número máximo de direcciones IP públicas que puede asignar entre todos los espacios de una organización.</dd>
</dl>
<strong>Nota</strong>: si aún no tiene contenedores en su entorno o si aún no tiene los contenedores del entorno configurados, recibirá un mensaje de error.
<p>Para obtener más información sobre contenedores, consulte [Acerca de los contenedores de IBM](/docs/containers/container_ov.html). Para obtener más información sobre cuotas de contenedor, consulte [Cuota y cuentas de Bluemix](/docs/containers/container_planning_org_ov.html#container_planning_quota).</p>
<strong>Nota:</strong> Los contenedores no están disponibles en la región Sídney de {{site.data.keyword.Bluemix_notm}}.</li>
</ul>
<li>Para guardar los cambios que haya efectuado en la página Gestionar
organización, pulse <strong>GUARDAR</strong>.</li>
</ol>


### Gestión de sus organizaciones desde la lista de organizaciones
{: #manageorgfrolis}

En la sección Lista de organizaciones, puede ver todas las organizaciones del entorno
de {{site.data.keyword.Bluemix_notm}}, y puede realizar acciones para organizaciones individuales pulsando en el nombre de la organización.

- Para suprimir la organización, pulse el icono **Suprimir** ![Suprimir](images/icon_trash.svg) en la columna Acciones.
- Para ver el plan de cuotas y uso de una organización, pulse el nombre de la organización en la lista. En la página **Gestionar organizaciones** para la
organización que ha seleccionado, puede ver la información de uso siguiente:

  - Número de servicios que hay actualmente en uso.
  - Número de rutas que hay actualmente en uso.
  - Gráfico de cuota de memoria que muestra qué parte de la cuota está en uso y qué parte no se usa actualmente.
  - Gráfico de asignación de aplicaciones que muestra qué aplicaciones se incluyen en la cuota de memoria utilizada.
  - Gráfico de uso de aplicaciones medidas que muestra un informe de tres meses de los GB-horas usados por app desplegada. Puede
seleccionar la **Vista de lista** para ver los datos de todas las aplicaciones, incluyendo la asignación de memoria por app y
el uso de GB-hora medido para los últimos tres meses.

- Para editar el nombre de la organización y añadir o eliminar gestores, pulse el nombre de la organización en la lista y siga las indicaciones en pantalla.
- Para ver información sobre un determinado usuarios de la organización que está visualizando, pulse el nombre del usuario para ver Información de usuario. Luego puede pulsar el nombre de la organización para volver a ver la Información de organización. 

## Gestión de usuarios y permisos
{: #oc_useradmin}

Puede añadir usuarios de forma individual o en grupos. Normalmente, los usuarios se añaden a la instancia de
{{site.data.keyword.Bluemix_notm}} desde el registro de usuarios de la empresa a través de LDAP (Lightweight Directory Access Protocol). También puede ver permisos de usuario. Si tiene asignado el permiso **Superuser**, también puede establecer y gestionar permisos de otros usuarios. Pulse **ADMINISTRACIÓN &gt; ADMINISTRACIÓN DE USUARIOS**.

La página Administración de usuarios muestra todos los usuarios para la instancia local o dedicada. Los permisos de cada usuario se muestran utilizando iconos en la tabla. Los permisos pueden ser los siguientes: Ninguno, **Superusuario**, **Acceso básico**, **Catálogo**, **Informes** y **Usuarios**.
Los permisos **Superuser** y **Basic Access** se pueden establecer en **Activado** o en
**Desactivado**, mientras que los permisos restantes se habilitan o inhabilitan con tipos de acceso específicos, incluyendo acceso de
**Lectura** o **Escritura** para dicho permiso, tal como representan los iconos. Consulte [Permisos](#permissions) para ver las descripciones
de cada tipo y las explicaciones de los iconos.

### Trabajar con usuarios
{: #workwithusers}

Según su acceso de **Lectura** o **Escritura** para los permisos de usuarios, puede buscar usuarios existentes, eliminar usuarios y añadir usuarios individualmente o por un grupo. Si tiene permiso de
**Superuser**, tendrá acceso completo para realizar cualquier tarea para la gestión de usuarios en el entorno. Revise las tareas de gestión de usuarios siguientes y el nivel de acceso necesario para realizar cada tarea:

* Localizar usuarios. Si tiene acceso de **Lectura** o **Escritura** y conoce todo o parte del nombre de usuario, puede localizar usuarios en la tabla mediante el campo **Buscar**. También puede filtrar la lista de usuarios por organización y permisos. Para filtrar una lista de usuarios, siga estos pasos:
  <ol>
  <li>Pulse <strong>Filtro</strong>.</li>
  <li> Pulse <strong>Organizaciones</strong> o <strong>Permisos</strong>, en función del filtro que desee aplicar.
  <dl>
	<dt><strong>Organización</strong></dt>
	<dd>Para filtrar usuarios por su organización, empiece a escribir el nombre de la organización en el campo <strong>Organización</strong> y seleccione la organización de la lista. A continuación, seleccione el rol o los roles asignados a los usuarios de la organización.</dd>
	<dt><strong>Permisos</strong></dt>
	<dd>Para filtrar usuarios por permisos, primero seleccione el tipo de usuario o usuarios. Por ejemplo, supongamos que desea ver todos los superusuarios. Para los permisos que no sean <strong>Superusuario</strong> o <strong>Acceso básico</strong>, también puede seleccionar el tipo de acceso, por ejemplo, <strong>Lectura</strong> o <strong>Escritura</strong>.</dd>
	</dl></li>
  <li>Pulse <strong>Aplicar</strong>.</li>
   </ol>

   La ventana Administración de usuarios muestra los filtros establecidos y los usuarios resultantes de los filtros especificados. A continuación, puede buscar un usuario en la tabla filtrada. También puede modificar la lista de filtros especificados eliminando una opción de filtro de la lista.

* Añadir un único usuario. Si tiene el permiso **Superuser** o el permiso **Users** con acceso de **Escritura**, puede añadir usuarios.

  1. Para añadir un único usuario desde el directorio LDAP, pulse **Añadir usuario**.
  2. En el campo **Buscar**, escriba la dirección de correo electrónico para el usuario y, a continuación, seleccione el usuario en la lista rellenada.
  3. A continuación, en el campo **Organización**, elija la organización a la que desea añadir el usuario especificando el nombre de organización y seleccionándolo en la lista rellenada.
  4. Para añadir el usuario a la organización seleccionada, pulse **Añadir usuario**.

  **Nota**: cuando la operación de adición es satisfactoria, el usuario se añade a la tabla para que lo pueda ver y buscar. Cuando se añaden usuarios, no tienen ningún permiso asignado.

* Añadir un grupo de usuarios desde el directorio LDAP. Si tiene el permiso **Superuser** o el permiso **Users** con acceso de **Escritura**, puede añadir usuarios.

  1. Pulse **Añadir grupo de usuarios**.
  2. En el campo **Buscar**, escriba un nombre de grupo en el que buscar y seleccione el nombre de grupo en la lista rellenada.
  3. A continuación, desde el campo **Organización**, elija la organización a la que desea añadir el grupo de usuarios entrando el nombre de organización y seleccionándola de la lista rellenada.
  4. Para añadir el grupo de usuarios a la organización seleccionada, pulse **Añadir usuarios**.

  **Nota**: los grupos de más de 50 usuarios se añaden mediante un trabajo por lotes en segundo plano. Cuando la operación de añadir finaliza correctamente, el usuario o grupo se añade a la tabla para que lo pueda ver y buscar. Cuando se añaden usuarios, no tienen ningún permiso asignado.

* Añada un grupo de usuarios importando una hoja de cálculo que incluya ID de usuario, direcciones de correo electrónico de usuario y la organización a la que tiene previsto añadir el usuario. Si tiene el permiso **Superuser** o el permiso **Users** con acceso de **Escritura**, puede añadir usuarios.

**Nota**: escriba los ID de usuario que coincidan con los valores utilizados en el registro de usuario.

  1. Pulse **Importar usuarios**.
  2. Pulse **Descargar plantilla (.CSV)** para descargar una hoja de cálculo con las columnas necesarias que puede rellenar, o bien puede crear su propia plantilla utilizando una hoja de cálculo que incluya las cabeceras de columna necesarias: **ID de usuario**, **Correo electrónico** y **Organización**.  También se incluyen dos columnas opcionales en la plantilla: **Nombre** y **Apellido**.
  3. Rellene los valores de usuario para las columnas necesarias. Si no utiliza un directorio LDAP, utilice las cabeceras de columnas necesarias y opcionales para los usuarios que importe.
  4. Guarde el archivo y pulse **Cargar archivo**.

  **Nota**: las columnas dentro de la hoja de cálculo puede estar en cualquier orden siempre que tenga todas las columnas necesarias. Si la importación se realiza correctamente, recibirá un mensaje de confirmación que indica que se han añadido todos los usuarios. Si la importación ha sido satisfactoria para algunos usuarios pero no para otros, revise los mensajes de error para realizar una acción en los usuarios que no se han podido añadir.

* Eliminar usuarios. Si tiene el permiso **Superuser** o el permiso **Users** con acceso de **Escritura**, puede eliminar usuarios del entorno de forma permanente.

    1. Localice el usuario y pulse el icono ![Suprimir](images/icon_trash.svg).
    2. Pulse **Eliminar**.

* La edición de permisos y organizaciones a las que pertenecen los usuarios requiere que tenga el permiso **Superuser**. Para editar permisos para los usuarios, localice el usuario y pulse sobre el nombre de usuario. En la página **Editar usuario**, puede habilitar o inhabilitar permisos:

    * Seleccione **Activado** en la lista para habilitar el permiso **Superuser** o
**Basic Access**.
    * Seleccione **Leer** en la lista para que el usuario tenga el acceso
**Lectura** (solo lectura) sobre dicho permiso, o seleccione **Escribir** para asignar el
acceso **Escritura** (editar o añadir y eliminar) para dicho permiso.
    * Seleccione **Desactivado** para inhabilitar cualquier de estos permisos.

    **Nota**: el establecimiento del permiso **Superuser** en **Activado** establece todos los demás permisos con acceso de **Escritura**.

* Para añadir o eliminar un usuario de una organización específica, debe tener el permiso
**Superuser** o el permiso **Users** con el acceso **Escritura**.

    1. Para añadir un usuario a una organización, seleccione el nombre de usuario en la tabla para acceder a la página **Editar usuario**. A continuación, utilice el campo de búsqueda para localizar una organización, seleccione la organización en la lista y pulse **Guardar**.
    2. Para eliminar un usuario de una organización, seleccione el nombre de usuario de la tabla para acceder a la página **Editar usuario**. A continuación, pulse ![Eliminar](images/icon_remove.svg) para la organización de la que desea eliminar el usuario y pulse **Guardar**.
    
* Para ver información sobre la organización a la que está asignado el usuario, pulse el nombre de la organización para ver Información de la organización. Luego puede pulsar el nombre del usuario para volver a ver la Información de usuario. 

### Permisos
{: #permissions}

Es posible asignar a los usuarios los permisos siguientes con niveles de acceso específicos (lectura o escritura) que permiten al usuario realizar tareas específicas en la consola de administración.


{: #ld_table14}

| **Permiso de usuario** | **Descripción** |       
|-----------------|-------------------|
| Superuser | Los usuarios con el permiso **Superuser** establecido en **Activado** pueden editar los permisos de otros usuarios. Si tiene el permiso activado, tendrá habilitado de forma automática el acceso completo a todos los demás permisos. Además de las tareas descritas para cada permiso en esta tabla, también puede configurar suscripciones de notificaciones para que se le avise directamente sobre incidencias o mantenimiento, mantenimiento planificado, ejecutar comprobaciones de verificación sobre componentes de consola y crear organizaciones y espacios para el entorno. Este permiso equivale al rol de administrador (admin) de la consola de administración.  |
| Basic Access | Los usuarios con el permiso **Basic Access** establecido en **Activado** pueden ver la opción de la página Administración en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}. Los usuarios que tienen el permiso habilitado pueden acceder a los mosaicos [Información del sistema](#oc_system) y [Uso de recursos](#oc_resource). Sin este permiso, los usuarios no pueden ver ni acceder a la opción de menú Administración. Este permiso equivale al rol de administrador (admin) de la consola de administración. Este permiso equivale al permiso de inicio de sesión utilizado previamente para la consola de administración. |
| Catalog | A los usuarios con el permiso **Catalog** se les puede asignar el acceso de **Lectura** o **Escritura** (modificar) los servicios que están disponibles en la instancia local o dedicada. El acceso de lectura permite que el usuario pueda acceder al mosaico Gestión de catálogos para ver los servicios disponibles. El acceso de escritura permite que el usuario pueda acceder al mosaico [Gestión de catálogos](#oc_catalog) para ver servicios, editar la visibilidad de los servicios, registrar servicios personalizados y controlar la lista de prioridades del paquete de compilación. |  
| Reports | A los usuarios con el permiso **Reports** se les puede asignar acceso **Lectura** o **Escritura** (modificar) sobre los informes de seguridad. El acceso de lectura permite que el usuario pueda acceder al mosaico Informes y registros para descargar informes. El acceso de escritura permite que el usuario pueda ver el mosaico [Informes y registros](#oc_report), así como utilizar la CLI para cargar nuevos informes y crear nuevas categorías para que los usuarios accedan a ellas. |
| Users | A los usuarios con el permiso **Users** se les puede asignar el acceso de **Lectura** (ver) sobre la lista de usuarios o de **Escritura** (añadir o eliminar) sobre los usuarios. Este permiso no le permite definir permisos para otros usuarios. El acceso de escritura permite que el usuario pueda añadir nuevos usuarios al entorno, suprimir usuarios del entorno y añadir usuarios existentes a las organizaciones que ya existen en el entorno. Además, el acceso de **Escritura** permite que el usuario pueda añadir nuevas organizaciones, suprimir organizaciones y editar los usuarios dentro de las organizaciones. |
{: caption="Tabla 14. Permisos" caption-side="top"}

## Utilización de API REST 
{: #auth_adminapi}

Para utilizar los mandatos de API REST, primero debe autenticarse. Para generar y dar soporte a las sesiones, puede utilizar mandatos cURL para llevar a cabo las tareas siguientes:

* [Inicio de sesión en la consola de administración](#auth_loginapi) 
* [Almacenamiento del ID de usuario y de la contraseña](#auth_setuidpw)
* [Almacenamiento de cookies](#auth_apistorecook)
* [Reutilización de cookies](#auth_apireusecook)

### Inicio de sesión en la consola de administración
{: #auth_loginapi}

Para poder ejecutar cualquier solicitud de la API `Admin`, debe iniciar una sesión en la consola de administración. 

Para iniciar la sesión en la Consola de administración, puede utilizar la autenticación de acceso básica en el
punto final `https://console.<region>.bluemix.net/login`. El servidor devuelve una cookie con la sesión. Utilice dicha cookie para todas las operaciones con la consola de administración.

**Nota:** La sesión deja de ser válida si no se utiliza durante unas cuantas horas.

Para iniciar una sesión en la consola de administración, ejecute el mandato siguiente:

`curl --user <id_usuario>:<contraseña> -c ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/login | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">--user <em>id_usuario</em>:<em>contraseña</em></dt>
<dd class="pd">Acepta el ID de usuario y la contraseña y envía una cabecera de autorización básica.</dd>
<dt class="pt dlterm">-c <em>nombre_archivo</em></dt>
<dd class="pd">Almacena el ID de usuario y la contraseña especificados como una cookie en el archivo especificado.</dd>
<dt class="pt dlterm">-b <em>nombre_archivo</em></dt>
<dd class="pd">Recupera el ID de usuario y la contraseña especificados como una cookie en el archivo especificado.</dd>
<dt class="pt dlterm">--header</dt>
<dd class="pd">Envía una cabecera de aceptación.</dd>
</dl>

El siguiente ejemplo muestra la salida de este mandato:
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*apellido*",
        "givenName": "*nombre*"
    }
}
```
{: screen}

### Almacenamiento del ID de usuario y de la contraseña
{: #auth_setuidpw}

También puede almacenar el ID de usuario y la contraseña de forma que no tenga que especificarlos manualmente cada vez que inicie sesión.  Para almacenar el ID de usuario y la contraseña para su reutilización, utilice el siguiente ejemplo de cURL:

`curl -X GET -H "Authorization: Basic <redacted>" -H "Accept: application/json" "http://localhost:3000/login"`
{: codeblock}

Para configurar su información de inicio de sesión en un archivo independiente y, a continuación, invocar el archivo para que no tenga que volver a especificarla para cada solicitud de autenticación, utilice la opción `--netrc` que se proporciona mediante el mandato cURL.

Para utilizar la opción `--netrc` con cURL, cree en primer lugar un archivo en el directorio de inicio del usuario de una de las siguientes maneras:
* En un sistema Unix, cree un archivo denominado .netrc 
* En un sistema Windows, cree un archivo denominado _netrc. 

En el archivo, especifique la siguiente información:

`machine console.<region>.bluemix.net
login <id>
password <password>`
{: codeblock}

Al invocar un mandato cURL, añada el siguiente argumento: `--netrc`.
<p>Para utilizar un archivo netrc situado en un directorio diferente, utilice la opción `--netrc-file [file]`, donde `[file]` es la ubicación del archivo netrc.</p>
</li>
</ol>


### Almacenamiento de cookies
{: #auth_apistorecook}

Al iniciar sesión en la consola de administración, el servidor devolverá una cookie con la sesión. Dicha cookie se necesita como parte del proceso de inicio de sesión para las próximas invocaciones de API para todas las operaciones con la consola de administración. Puede almacenar cookies para utilizarlas más adelante.

Para almacenar cookies una vez que haya iniciado sesión, utilice la opción `-c`, tal como se muestra en el siguiente ejemplo de CURL:

`curl --user <id_usuario>:<contraseña> -c ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/login | python -m json.tool`
{: codeblock}

### Reutilización de cookies
{: #auth_apireusecook}

Para reutilizar cookies, utilice la opción `-b` con el nombre de archivo de la cookie que haya asignado con la opción `-c`, tal como se muestra en el siguiente ejemplo de CURL:

`curl --user <id_usuario>:<contraseña> -b ./cookies.txt`
{: codeblock}

## Gestión de usuarios con la API REST de administración

{: #usingadminapi}

Puede utilizar la API REST `Admin` para añadir y eliminar usuarios de la instancia de
{{site.data.keyword.Bluemix_notm}}.
Se proporcionan puntos finales de la API REST `Admin` y respuestas JSON a modo experimental para habilitar operaciones básicas desde una línea de mandatos. Los puntos finales y URL de los ejemplos de esta información pueden cambiar o pueden ser retirados previo aviso.

Si tiene el permiso **Superuser** o el permiso **Users** con el acceso **Escritura**, puede añadir o eliminar usuarios. Debe tener el permiso **Superuser** para poder editar los permisos de otros usuarios.

Aunque puede optar por utilizar otras herramientas, las herramientas siguientes constituyen requisitos previos para utilizar los ejemplos siguientes; utilice también otras herramientas.
* cURL, para especificar solicitudes de la API REST como mandatos. cURL es un programa de utilidad gratuito que puede utilizar para enviar solicitudes HTTP a un servidor y recibir las respuestas del servidor a través de una interfaz de línea de mandatos. Puede descargar cURL desde el [sitio de descargas de cURL ![icono de enlace externo](../icons/launch-glyph.svg)](http://curl.haxx.se/download.html){: new_window}.
* Python, para utilizar la herramienta JSON pretty-print de Python. Esta herramienta opcional toma texto JSON como entrada y genera información de salida de fácil lectura. Puede descargar Python desde el [sitio de descargas de Python ![icono de enlace externo](../icons/launch-glyph.svg)](https://www.python.org/downloads){: new_window}.


### Listado de organizaciones
{: #listingorg}

Cuando añada un usuario, debe especificar una organización. Puede utilizar la API REST `Admin` para obtener una lista de todas las organizaciones. Debe tener el permiso
**Users** con acceso **Lectura** para poder listar
organizaciones. Para listar todas las organizaciones, ejecute el mandato siguiente:

`curl -b ./cookies.txt https://<su_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>nombre_archivo</em></dt>
<dd class="pd">Pasa el ID de usuario y la contraseña que se han almacenado anteriormente con la opción <samp class="ph codeph">-c</samp> en el archivo al servidor HTTP como una cookie.</dd>

</dl>

Para cada organización, los resultados incluyen la siguiente información:
* `"guid"`, GUID de la organización
* `"name"`, nombre de la organización

El siguiente ejemplo muestra la salida de este mandato:
```
{
     "resources": [
         {
             "guid": "05af098d-d476-4fb0-8b87-a84350e72af3",
             "name": "org-1"
         },
         {
             "guid": "5129a5a8-37c2-4ee4-a9b2-bebae3531db5",
             "name": "org-2"
         },

		 		 ....

		 ],
		 "total_results": 284
}
```
{: screen}

### Listado de usuarios
{: #listingusr}

Puede determinar si un usuario ya se ha añadido al entorno de
{{site.data.keyword.Bluemix_notm}} mediante
la API REST de `Admin` para obtener una lista de los usuarios registrados. Debe tener
el permiso **Users** con acceso **Lectura** para poder listar usuarios registrados.
Para listar todos los usuarios, ejecute el mandato siguiente:

`curl -b ./cookies.txt https://<su_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>nombre_archivo</em></dt>
<dd class="pd">Pasa el ID de usuario y la contraseña que se han almacenado anteriormente con la opción <samp class="ph codeph">-c</samp> en el archivo al servidor HTTP como una cookie.</dd>
</dl>

Para cada usuario registrado, los resultados incluyen la siguiente información:
* `"first_name"` (nombre) y `"last_name"` (apellido)
* `"user_id"`, ID de usuario y dirección de correo electrónico
* `"guid"`, GUID de la organización.
* `"permissions"` asignados al usuario para la consola de administración.

El siguiente ejemplo muestra la salida de este mandato:

```
{
    "next_url": "/codi/v1/users?results_per_page=100&amp;page=2",
    "prev_url": "",
    "resources": [
        {
            "active": true,
            "created_at": "2015-04-08T17:38:51.788Z",
            "created_by": "",
            "first_name": "some first name",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "some last name",
            "permissions": [
                {
                    "display": "ops.admin"
                },
                {
                    "display": "ops.catalog.write"
                },
                {
                    "display": "ops.reports.write"
                },
                {
                    "display": "ops.catalog.read"
                },
                {
                    "display": "ops.users.write"
                },
                {
                    "display": "ops.reports.read"
                },
                {
                    "display": "ops.login"
                },
                {
                    "display": "ops.users.read"
                }
            ],
            "user_id": "someid@us.ibm.com"
        },
		 		 ...


     }
    ],
    "total_pages": 395,
    "total_results": 39421
}

```
{: screen}

### Adición de un usuario

Puede utilizar la API REST `Admin` para añadir usuarios a la instancia de
{{site.data.keyword.Bluemix_notm}}. Debe tener el permiso
**Users** con acceso **Escritura** para añadir usuarios, o el permiso
**Superuser** (ops.admin) para la consola de administración. Además, como administrador, puede permitir que miembros de la organización que no tienen permiso `user` ni `superuser` sobre la consola de administración general puedan añadir nuevos usuarios únicamente a su organización. Utilice el mandato de API siguiente para esta función específica para gestores de la organización:

```
PUT console.<subdominio>.bluemix.net/codi/env_config/allow_managers?flag=<TRUE o FALSE>
```
{: screen}

Puede añadir un usuario o una lista de usuarios. Puede añadir usuarios a una única
organización, o a varias organizaciones. Para añadir un usuario, debe proporcionar la información siguiente:

* Nombre y apellido del usuario. Especifique
`"nombre"` y `"apellido"` de [Listado de usuarios](index.html#listingusr).
* Dirección de correo electrónico e ID de usuario: especifique el `"id_usuario"` del [Listado de usuarios](index.html#listingusr) tanto para la dirección de correo electrónico como para el ID de usuario.
* `"guid"`. Especifique el GUID de la organización de [Listado de organizaciones](index.html#listingorg).

Debe proporcionar la información en un archivo JSON.

`curl -b ./cookies.txt https://<su_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>nombre_archivo</em></dt>
<dd class="pd">Pasa el ID de usuario y la contraseña que se han almacenado anteriormente con la opción <samp class="ph codeph">-c</samp> en el archivo al servidor HTTP como una cookie.</dd>
</dl>

<ol>
<li>Cree un archivo JSON que contenga la información en un formato JSON adecuado.
<p>Por ejemplo, cree un archivo llamado `user.json` con el siguiente contenido:</p>
<pre>
{
    "members": [
        {
            "emails": [
                "some_user_id@domain.com"
            ],
            "first_name": "Some_first_name",
            "last_name": "Some_last_name",
            "user_id": "some_user_id@domain.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</pre>
</li>
<li>Publique el contenido del archivo JSON en el punto final del usuario ejecutando el mandato siguiente:<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<su_host>.ibm.com/codi/v1/users
</code>
</li>
</ol>

<dl class="parml">
<dt class="pt dlterm">-v </dt>
<dd class="pd">Especifica salida detallada.</dd>
<dt class="pt dlterm">-X POST</dt>
<dd class="pd">Especifica una solicitud POST, alterando temporalmente la solicitud GET predeterminada.</dd>
<dt class="pt dlterm">-H "Content-Type: application/json"</dt>
<dd class="pd">Especifica la cabecera content-type, que en este caso es JSON.</dd>
<dt class="pt dlterm">-d *datos*</dt>
<dd class="pd">Especifica los datos, en este caso el archivo `user.json`, que se van a enviar en la solicitud POST al servidor HTTP.</dd>
</dl>

El siguiente ejemplo muestra la salida de este mandato:

```
* Connected to localhost (127.0.0.1) port 3000 (#0)
 > POST /codi/v1/users HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 > Content-Type: application/json
 > Content-Length: 333
 >
 * upload completely sent off: 333 out of 333 bytes
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < vary: X-HTTP-Method-Override
 < content-type: application/json
 < date: Wed, 22 Apr 2015 19:32:54 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

### Eliminación de un usuario

Puede utilizar la API REST `Admin` para eliminar usuarios de la instancia de
{{site.data.keyword.Bluemix_notm}}. Debe tener el permiso **Users** con acceso **Escritura** para poder eliminar usuarios.

Para eliminar un usuario, debe especificar el ID del usuario. Ejecute el mandato siguiente:

`curl -v -b ./cookies.txt -X DELETE https://<su_host>.ibm.com/codi/v1/users?user_id=<some_user_id@domain.com>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-X DELETE</dt>
<dd class="pd">Especifica una solicitud DELETE.</dd>
</dl>

El siguiente ejemplo muestra la salida de este mandato:

```
 * connect to ::1 port 3000 failed: Connection refused
 *   Trying 127.0.0.1...
 * Connected to localhost (127.0.0.1) port 3000 (#0)
 > DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 >
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < content-type: application/json
 < date: Wed, 22 Apr 2015 21:01:09 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 1922 msec
 <
 ```
{: screen}

## API para métricas (experimental)
{: #envappmetricsapi}

Puede utilizar tres API experimentales para recopilar métricas sobre el entorno o las aplicaciones. Estas API devuelven una matriz de puntos de datos correspondientes a las métricas que ha solicitado durante el periodo de tiempo especificado.

Se puede acceder a las API para métricas que se describen en las secciones desde el punto final específico de la región, por ejemplo: 

`https://console.<region>.bluemix.net/admin/metrics`
{: codeblock}

**Notas**:

1. Un usuario puede realizar un máximo de 200 solicitudes de API para métricas por hora.
2. Cada solicitud de API devuelve un máximo de 200 puntos de datos por solicitud. Si hay más datos disponibles, se proporciona un URL en la respuesta para cargar el siguiente conjunto de datos.
3. Cada solicitud de API necesita que un usuario tenga al menos Acceso básico a la consola de administración.  Es posible que se necesiten permisos adicionales, como se especifica más abajo.

## Obtención de métricas sobre el entorno 

Puede utilizar la API de entorno experimental para obtener información sobre el entorno durante el periodo de tiempo que especifique. Se devuelven los puntos de datos disponibles dentro del periodo de tiempo que especifique. Se registran datos cada hora aproximadamente. Si, por ejemplo, ha solicitado seis horas de datos de CPU para el entorno, la respuesta incluirá datos de CPU correspondientes a cada una de las seis horas solicitadas.


### Puntos finales del entorno 

Puede utilizar el punto final siguiente para invocar este mandato de API: `/api/v1/env`

**Nota**: Es necesario uno de los siguientes permisos para acceder a estos puntos finales: **acceso básico**, **lectura de usuario**, **escritura de usuario**, o **Superusuario**

### Parámetros de consulta de métricas del entorno

Con los siguientes parámetros de consulta puede obtener métricas correspondientes a CPU, disco, memoria, red, cuota y apps:

<dl class="parml">
<dt class="pt dlterm">métrica</dt>
<dd class="pd">Uno o varios de los siguientes valores, separados por comas: `memory`, `disk`, `cpu`, `network`, `quota` y `apps`.</dd>
<dt class="pt dlterm">startTime</dt>
<dd class="pd">El primer punto en el tiempo a partir del que se devuelven datos. Si no se especifica startTime, se incluye el punto de datos más antiguo disponible. Por ejemplo, para obtener datos entre las 2 PM y las 5 PM, especifique para startTime el valor 2 PM.</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">El último punto en el tiempo a partir del que se devuelven datos. Si no se especifica endTime, se utiliza el punto de datos más reciente. Por ejemplo, para obtener datos entre las 2 PM y las 5 PM, especifique para endTime el valor 5 PM.</dd>
<dt class="pt dlterm">sort</dt>
<dd class="pd">El orden en el que se devuelven los datos. Los valores válidos son `asc` (ascendente) y `desc` (descendente). El valor predeterminado es descendente, que devuelve en primer lugar los datos más recientes. </dd>
</dl>

El ejemplo siguiente utiliza los parámetros de consulta para obtener métricas sobre el entorno:

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/env?metric=cpu,network,disk,apps,memory
```
{: codeblock}


### Formato de los datos de las métricas del entorno

En las secciones siguientes se proporciona al formato de los datos.

 * Para obtener registros de datos sobre el uso de memoria, utilice el siguiente formato de datos:
 
```
{
  "sample_time": 1477494000000,
  "memory": {
    "total": {
      "physical": {
        "total_gb": 1728,
        "used": {
          "value_gb": 673.68,
          "percent": 38.99
        }
      },
    "allocated": {
        "reserved_gb": 3456,
        "total_allocated": {
          "value_gb": 2575.18,
          "percent": 74.51
        }
      },
    },
  	"cell": {
      "physical": {
        "total_gb": 864,
      "used": {
          "value_gb": 336.84,
        "percent": 38.99
      }
      },
    "allocated": {
        "reserved_gb": 1728,
      "total_allocated": {
          "value_gb": 1287.59,
        "percent": 74.51
      }
      },
    },
    "dea": {
      "physical": {
      	"total_gb": 864,
      "used": {
          "value_gb": 336.84,
        "percent": 38.99
      }
      },
    "allocated": {
        "reserved_gb": 1728,
      "total_allocated": {
          "value_gb": 1287.59,
        "percent": 74.51
      }
      },
    },
    "memory_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "percent": "47"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "percent": "51"
      },
      {
        "name": "dea_next/2",
        "type": "dea",
        "ip": "169.53.230.49",
        "percent": "45"
      },
      {
        "name": "dea_next/3",
        "type": "dea",
        "ip": "169.44.109.231",
        "percent": "43"
      }
    ]
  }
}
```
{: screen}

 * Para obtener registros de datos sobre el uso de disco, utilice el siguiente formato de datos:
 
```
{
  "sample_time": 1477494000000,
  "disk": {
    "total": {
      "physical": {
        "total_gb": 16200,
        "used": {
          "value_gb": 1614,
          "percent": 9.96
        }
      },
    "allocated": {
        "reserved_gb": 32400,
        "total_allocated": {
          "value_gb": 3979,
          "percent": 12.28
        }
      },
    },
    "cell": {
      "physical": {
        "total_gb": 8100,
      "used": {
          "value_gb": 807,
        "percent": 9.96
      }
      },
    "allocated": {
        "reserved_gb": 16200,
      "total_allocated": {
          "value_gb": 1989.5,
        "percent": 12.28
      }
      },
    },
    "dea": {
      "physical": {
        "total_gb": 8100,
      "used": {
          "value_gb": 807,
        "percent": 9.96
      }
      },
    "allocated": {
        "reserved_gb": 16200,
      "total_allocated": {
          "value_gb": 1989.5,
        "percent": 12.28
      }
      },
    },
    "disk_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "percent": "13"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "percent": "14"
      },
      {
        "name": "dea_next/2",
        "type": "dea",
        "ip": "169.53.230.49",
        "percent": "13"
      },
      {
        "name": "dea_next/3",
        "type": "dea",
        "ip": "169.44.109.231",
        "percent": "12"
      }
    ]
  }
}
```
{: screen}

 * Para obtener registros de datos sobre el uso de CPU, utilice el siguiente formato de datos:
 
```
{
  "sample_time": 1477494000000,
  "cpu": {
    "total": {
      "average_percent_cpu_used": 14.725
    },
    "cell": {
      "average_percent_cpu_used": 19
    },
    "dea": {
      "average_percent_cpu_used": 10.45
    },
    "cpu_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "sys_percent": "8.4",
        "user_percent": "2.7",
        "wait_percent": "0.0"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "sys_percent": "7.4",
        "user_percent": "2.4",
        "wait_percent": "0.0"
      },
      {
        "name": "cell/1",
        "type": "cell",
        "ip": "169.53.230.49",
        "sys_percent": "5.3",
        "user_percent": "1.9",
        "wait_percent": "0.0"
      },
      {
        "name": "cell/2",
        "type": "cell",
        "ip": "169.44.109.231",
        "sys_percent": "8.2",
        "user_percent": "22.6",
        "wait_percent": "0.0"
      }
    ]
  }
}
```
{: screen}

 * Para obtener registros de datos sobre la red, utilice el siguiente formato de datos:
 
```
{
  "sample_time": 1477494000000,
  "network": {
    "datapower": {
    "response_times": [
      {
        "proxy": "custom_certificates",
        "ten_seconds_ms": "0",
        "one_minute_ms": "0",
        "ten_minutes_ms": "0",
        "one_hour_ms": "0",
        "one_day_ms": "0"
      },
      {
        "proxy": "bluemix",
        "ten_seconds_ms": "90",
        "one_minute_ms": "89",
        "ten_minutes_ms": "83",
        "one_hour_ms": "85",
        "one_day_ms": "95"
      }
      ],
        "transactions": [
      {
        "proxy": "custom_domains",
        "ten_seconds_ms": "0",
        "one_minute_ms": "0",
        "ten_minutes_ms": "0",
        "one_hour_ms": "0",
        "one_day_ms": "0"
      },
      {
        "proxy": "bluemix",
        "ten_seconds_ms": "697",
        "one_minute_ms": "747",
        "ten_minutes_ms": "802",
        "one_hour_ms": "794",
        "one_day_ms": "730"
      }
      ],
        "bandwidth": {
        "in_kbps": 10855,
        "out_kbps": 38090
      }
  }
}
```
{: screen}

* Para recopilar registros de datos sobre el uso de cuota, utilice el siguiente formato de datos:
 
```
{
  "sample_time": 1477494000000,
  "quota": {
    "reserved_memory": {
      "total_bytes": 33176474877952
    },
    "services": {
      "total": 111650
    },
    "routes": {
      "total": 1675000
    }
  }
}
```
{: screen}

* Para obtener registros de datos sobre las aplicaciones, utilice el siguiente formato de datos:
 
```
{
  "sample_time": 1477494000000,
  "apps": {
    "count": 1406,
    "allocation": {
      "memory_gb": 571.8,
      "disk_gb": 1204
    }
  }
}
```
{: screen}

### Formato de respuesta de las métricas del entorno

```
{
   docs: [],
   next_url:
}
```
{: screen}

## Recopilación de métricas sobre sus organizaciones

Se registran datos para todas las organizaciones aproximadamente cada hora. Una solicitud de una métrica particular devuelve información correspondiente a todas las organizaciones de cada muestra de datos del período de tiempo que especifique, que se guarda en orden descendente mediante la métrica solicitada. Por ejemplo, solicitando todas las organizaciones por memoria durante un periodo de tiempo de 6 horas en un entorno que tiene 200 apps, se devuelven 1200 registros, en grupo de 200.

Para reducir la cantidad de información que se devuelve para cada muestra de datos en el periodo de tiempo solicitado, puede especificar una opción de recuento. Siguiendo con el ejemplo anterior, si añadimos una opción de recuento de 5 se devuelven 30 registros que representan las 5 primeras organizaciones por memoria para cada muestra de datos.

### Puntos finales de las organizaciones 

Puede utilizar los siguientes puntos finales para invocar este mandato de API:
* `/api/v1/org/memory/physical`
* `/api/v1/org/memory/reserved`
* `/api/v1/org/disk/physical`
* `/api/v1/org/disk/reserved`

**Nota**: Es necesario uno de los siguientes permisos para acceder a estos puntos finales: **lectura de usuario**, **escritura de usuario**, o **Superusuario**

### Parámetros de consulta de las organizaciones
 
Utilice los siguientes parámetros de consulta para recopilar métricas para las organizaciones:

<dl class="parml">
<dt class="pt dlterm">startTime</dt>
<dd class="pd">El primer punto en el tiempo a partir del que se devuelven datos. Si no se especifica startTime, se incluye el punto de datos más antiguo disponible. Por ejemplo, para obtener datos entre las 2 PM y las 5 PM, especifique para startTime el valor 2 PM.</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">El último punto en el tiempo a partir del que se devuelven datos. Si no se especifica endTime, se utiliza el punto de datos más reciente. Por ejemplo, para obtener datos entre las 2 PM y las 5 PM, especifique para endTime el valor 5 PM.</dd>
<dt class="pt dlterm">count</dt>
<dd class="pd">El número de registros que se devolverán para cada muestra de datos.
</dd>
<dt class="pt dlterm">minValue</dt>
<dd class="pd">El valor más pequeño a devolver para la métrica especificada.  Si no se especifica ningún minValue, se devolverán todos los valores.  Por ejemplo, para recopilar organizaciones utilizando al menos 20000 bytes de memoria física, especifique un minValue de 20000.
</dd>
</dl>

El siguiente ejemplo recopila métricas sobre las organizaciones:

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/org/memory/physical?count=5&startTime=2016-12-02T16:54:09.467Z
```
{: codeblock}

### Formato de respuesta de las organizaciones

```
{
   docs: [],
   next_url:
}
```
{: screen}

Cada documento que se devuelve representa las métricas solicitadas para una organización en cada muestra de datos, en el momento de realizar la solicitud.

## Obtención de métricas sobre las aplicaciones

Se registran datos para todas las aplicaciones aproximadamente cada hora. Una solicitud de una métrica en particular devuelve información correspondiente a todas las apps en cada muestra de datos del periodo de tiempo que especifique, que se guarda en orden descendente por orden de métrica solicitada. Por ejemplo, si se solicitan todas las apps por CPU durante un periodo de tiempo de 6 horas y hay 200 apps, se devuelven 1200 registros, en grupos de 200.

Para reducir la cantidad de información que se devuelve para cada muestra de datos en el periodo de tiempo solicitado, puede especificar una opción de recuento. Siguiendo con el ejemplo anterior, si añadimos una opción de recuento de 5 se devuelven 30 registros que representan las 5 primeras aplicaciones por CPU para cada muestra de datos.

### Puntos finales de las aplicaciones 

Puede utilizar los siguientes puntos finales para invocar este mandato de API:
* `/api/v1/app/cpu/physical` 
* `/api/v1/app/memory/physical`
* `/api/v1/app/memory/reserved`
* `/api/v1/app/disk/physical`
* `/api/v1/app/disk/reserved`

**Nota**: Es necesario uno de los siguientes permisos para acceder a estos puntos finales: **lectura de usuario**, **escritura de usuario**, o **Superusuario**

### Parámetros de consulta de aplicaciones
 
Utilice los siguientes parámetros de consulta para obtener métricas correspondientes a las aplicaciones:

<dl class="parml">
<dt class="pt dlterm">startTime</dt>
<dd class="pd">El primer punto en el tiempo a partir del que se devuelven datos. Si no se especifica startTime, se incluye el punto de datos más antiguo disponible. Por ejemplo, para obtener datos entre las 2 PM y las 5 PM, especifique para startTime el valor 2 PM.</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">El último punto en el tiempo a partir del que se devuelven datos. Si no se especifica endTime, se utiliza el punto de datos más reciente. Por ejemplo, para obtener datos entre las 2 PM y las 5 PM, especifique para endTime el valor 5 PM.</dd>
<dt class="pt dlterm">count</dt>
<dd class="pd">El número de registros que se devolverán para cada muestra de datos.
</dd>
<dt class="pt dlterm">minValue</dt>
<dd class="pd">El valor más pequeño a devolver para la métrica especificada. Si no se especifica ningún minValue, se devolverán todos los valores. Por ejemplo, para recopilar aplicaciones utilizando al menos 20000 bytes de memoria física, especifique un minValue de 20000.
</dd>
</dl>

El siguiente ejemplo recopila métricas sobre las aplicaciones:

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/app/cpu/physical?count=5&startTime=2016-12-02T16:54:09.467Z
```
{: codeblock}


### Formato de respuesta de aplicaciones

```
{
   docs: [],
   next_url:
}
```
{: screen}

Cada documento que se devuelve representa las métricas solicitadas para una aplicación en cada muestra de datos, en el momento de realizar la solicitud.


## API de servicio personalizado
{: #servicebrokerapi}

Hay tres API que puede utilizar para registrar o crear un servicio, actualizar un servicio y suprimir un servicio.

Todas las API son relativas a <code>https://console.&lt;subdomain&gt;.bluemix.net/</code>.

<dl>
<dt><strong>&lt;subdominio&gt;</strong></dt>
<dd>Este valor es el nombre de la instancia local o dedicada. El nombre del subdominio de la instancia {{site.data.keyword.Bluemix}} se ha asignado
durante la incorporación.</dd>
</dl>

## Registro de un nuevo servicio

Utilice la siguiente API y ejemplos de código para registrar un nuevo servicio.

### Ruta
{: #registerroute}

```
POST /codi/v1/serviceBrokers
```
{: screen}

### Solicitud
{: #registerrequest}

{: #ld_table15}

| **Nombre** | **Descripción** |
|-----------------|-------------------|
| name | Nombre del intermediario de servicio. |
| auth_username | Nombre de usuario utilizado para conectarse con el intermediario de servicio. |
| auth_password | Contraseña utilizada para conectarse con el intermediario de servicio. |
| broker_url | URL utilizada para conectarse al intermediario de servicio. |
| owningOrganization | Organización inicial con la que incluir en la lista blanca el servicio. |
{: caption="Tabla 15. Campos" caption-side="top"}

#### Cuerpo
{: #registerbody}

```
{
  "name" : "Service broker's name",
  "auth_username" : "username",
  "auth_password" : "password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### Cabeceras
{: #registerheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Respuesta
{: #registerresponse}

#### Estado
{: #registerstatus}

```
201 Created
```
{: screen}

#### Cuerpo
{: #registerbody2}

```
{
    "_id": "2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "proxy_broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "auth_username": "username",
    "created_on": "2016-09-30T16:45:56.304Z"
}

```
{: screen}

## Actualización de un servicio

Utilice la siguiente API y ejemplos de código para actualizar un servicio.

### Ruta
{: #updateroute}

`PUT /codi/v1/serviceBrokers`
{: screen}

### Solicitud
{: #updaterequest}

{: #ld_table16}

| **Nombre** | **Descripción** |
|-----------------|-------------------|
| name | Nombre del intermediario de servicio. Este nombre no puede modificarse a partir del nombre con el que se ha creado el servicio. |
| auth_username | Nombre de usuario utilizado para conectarse con el intermediario de servicio. |
| auth_password | Contraseña utilizada para conectarse con el intermediario de servicio. |
| broker_url | URL utilizada para conectarse al intermediario de servicio. |
| owningOrganization | Organización inicial con la que incluir en la lista blanca el servicio. |
{: caption="Tabla 16. Solicitudes" caption-side="top"}

#### Cuerpo
{: #updatebody}

```
{
  "name" : "Service Broker's name",
  "auth_username" : "username",
  "auth_password" : "newPassword",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### Cabeceras
{: #updateheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Respuesta
{: #updateresponse}

#### Estado
{: #updatestatus}

```
201 Created
```
{: screen}

#### Cuerpo
{: #updatebody2}

```
{
    "_id": "2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "proxy_broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "auth_username": "username",
    "created_on": "2016-09-30T16:45:56.304Z"
}
```
{: screen}

## Supresión de un servicio

Utilice la siguiente API y ejemplos de código para suprimir un servicio.


{: #ld_table17}

| **Nombre** | **Descripción** |
|-----------------|-------------------|
| name | Nombre del intermediario de servicio. Este nombre no puede modificarse a partir del nombre con el que se ha creado el servicio. |
{: caption="Tabla 17. Parámetro" caption-side="top"}

### Ruta

```
DELETE /codi/v1/serviceBrokers?name=name of service broker
```
{: screen}

### Solicitud
{: #deleterequest}

#### Cabeceras
{: #deleteheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Respuesta
{: #deleteresponse}

#### Estado
{: #deletestatus}

```
204 No Content
```
{: screen}

### Gestión de usuarios con la CLI cf
{: #usingadmincli}

Puede gestionar usuarios del entorno de
{{site.data.keyword.Bluemix_notm}} mediante la interfaz
de línea de mandatos de Cloud Foundry con el plug-in CLI de
administración de {{site.data.keyword.Bluemix_notm}}. Debe descargar este plugin para su interfaz de línea de mandatos de Cloud Foundry.

Antes de empezar, instale la interfaz de línea de mandatos cf. El plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}} necesita
cf versión 6.11.2 o posterior. [Descargue la interfaz de línea de mandatos
de Cloud Foundry ![icono de enlace externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}.

**Restricción:** Cygwin no admite la interfaz de línea de mandatos de Cloud Foundry. Utilice esta interfaz en una ventana de línea de mandatos que no sea la ventana de Cygwin.

#### Adición del plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}}

Una vez instalada la interfaz de línea de mandatos cf, puede añadir el plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}}.

**Nota**: si ha instalado previamente el plugin Admin de {{site.data.keyword.Bluemix_notm}}, es posible que
tenga que desinstalarlo, suprimir el repositorio y luego volver a instalarlo para obtener las actualizaciones más recientes.

Siga estos pasos para añadir el repositorio e instalar
el plug-in:

<ol>
<li>Para añadir el repositorio de plugins de la administración de {{site.data.keyword.Bluemix_notm}}, ejecute el siguiente mandato:<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdominio&gt;</dt>
<dd class="pd">Subdominio del URL correspondiente a la instancia de {{site.data.keyword.Bluemix_notm}}.</dd>
</dl>
</li>
<li>Para instalar el plugin de la CLI de administración de {{site.data.keyword.Bluemix_notm}}, ejecute el mandato siguiente:<br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

Para ver una lista de submandatos disponibles de los plugins que tiene instalados, ejecute el siguiente mandato:

```
cf plugins
```
{: codeblock}

Para ver una lista de los grupos de mandatos disponibles para el plugin {{site.data.keyword.Bluemix_notm}} Admin, ejecute el siguiente mandato:

```
cf ba
```
{: codeblock}

Para obtener más ayuda sobre un mandato, utilice la opción `-help`.

Para obtener más información sobre cómo trabajar con el plug-in CLI de administración de {{site.data.keyword.Bluemix_notm}}, consulte Administración de [{{site.data.keyword.Bluemix_notm}}](../cli/plugins/bluemix_admin/index.html).
