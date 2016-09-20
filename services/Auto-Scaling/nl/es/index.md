{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Iniciación al servicio {{site.data.keyword.autoscaling}}
{: #autoscaling}

*ültima actualización: 18 de enero de 2015*

En {{site.data.keyword.Bluemix_notm}}, puede gestionar automáticamente la capacidad de su aplicación. Utilice el servicio {{site.data.keyword.autoscalingfull}} para aumentar y reducir automáticamente la capacidad de cálculo de su aplicación. El número de instancias de aplicación se ajustan de forma dinámica según la política de {{site.data.keyword.autoscaling}} que defina.
{:shortdesc} 

## Utilización del servicio {{site.data.keyword.autoscaling}} en {{site.data.keyword.Bluemix_notm}}
{: #as-service}

Para utilizar el servicio {{site.data.keyword.autoscaling}}, siga estos pasos:

1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, pulse *Añadir un servicio o API* y seleccione el servicio {{site.data.keyword.autoscaling}} en la sección DevOps del catálogo de servicios. Se abre una nueva ventana que presenta una visión general del servicio {{site.data.keyword.autoscaling}}.
2. Seleccione la aplicación que quiera enlazar el servicio de {{site.data.keyword.autoscaling}} y pulse *Crear*. <br/>
*Recuerde:* Sólo puede enlazar un servicio {{site.data.keyword.autoscaling}} a una aplicación. Si la aplicación ya está enlazada a otro servicio {{site.data.keyword.autoscaling}}, no seleccione la aplicación en este caso. De lo contrario, se generará el error CWSCV2004E.<br/>Se muestra la ventana Volver a transferir aplicación.
3. En la ventana Volver a transferir aplicación, pulse *Volver a transferir* para volver a transferir la aplicación antes de utilizar el nuevo servicio {{site.data.keyword.autoscaling}} que acaba de añadir. Cuando se termine de volver a transferir la aplicación, puede empezar a configurar el servicio {{site.data.keyword.autoscaling}} para la aplicación.
4. Para configurar el servicio {{site.data.keyword.autoscaling}} para una aplicación, en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} pulse la aplicación a la que desea enlazar el servicio {{site.data.keyword.autoscaling}}.
5. En la sección de servicios del Panel de control, pulse el icono del servicio *Auto-Scaling*.
6. Si aún no lo ha hecho, defina la política de {{site.data.keyword.autoscaling}} para la aplicación pulsando *Crear política de {{site.data.keyword.autoscaling}}*.

Ahora puede configurar la política de {{site.data.keyword.autoscaling}}, ver estadísticas de medidas o ver el historial de escalado de la aplicación.
<dl>
<dt>Configuración de directiva</dt>
<dd>Utilice esta sección para crear o editar las reglas de escalado para especificar las condiciones bajo las que se deben activar determinadas actividades de escalado.<ul>
<li> En las aplicaciones de Liberty for Java™, puede definir reglas de escalado para el almacenamiento dinámico de JVM, la memoria y el rendimiento.
<li> En las aplicaciones de Node.js, puede definir reglas de escalado para la memoria.
<li> En las aplicaciones de Ruby, puede definir reglas de escalado para la memoria.</ul>
*Nota:* Es posible definir varias reglas de escalado para más de un tipo de métrica. Sin embargo, el servicio {{site.data.keyword.autoscaling}} no detecta conflictos entre políticas de escalado. Al definir la política de escalado, debe asegurarse de que las diversas reglas de escalado no entran en conflicto entre ellas. De lo contrario, es posible que el número total de instancias fluctúe al alza o a la baja porque la aplicación escala verticalmente durante un minuto y horizontalmente el siguiente.<br/><br/>
Si la carga de la aplicación cambia significativamente durante la hora punta y el tiempo libre, puede crear una planificación de escalado para manejar los distintos requisitos de escalado para los diferentes periodos de tiempo. Utilice el parámetro Recuento mínimo de instancias especificado en una planificación para definir la línea base del número de instancias de la aplicación, mientras las reglas de escalado dinámico se siguen aplicando a la planificación para desencadenar las acciones de escalado horizontal y vertical.</dd>
<dt>Estadísticas de métrica</dt>
<dd>Muestra las estadísticas de métrica de las instancias de la aplicación. Puede ver el promedio y seleccionar una instancia específica para ver sus estadísticas.</dd>
<dt>Historial de escalado</dt>
<dd>Muestra el historial de escalado de las aplicaciones.<ul>
<li> Semana pasada: muestra el historial de escalado de la semana pasada.
<li> Mes pasado: muestra el historial de escalado del mes pasado.
<li> Rango personalizado: puede definir el periodo de tiempo.</ul>
*Nota:* Es posible filtrar el registro del historial seleccionando la opción: Estado de escalado o Escalado vertical/horizontal.</dd>
</dl>


## Campos de política para el servicio {{site.data.keyword.autoscaling}}
{: #policyfields}

| Nombre de campo  | Descripción |
|-------------|----------------------|
|*Recuento máximo de instancias permitidas* |	El número máximo de instancias de la aplicación que se pueden iniciar. Si el número actual de instancias de la aplicación es igual que este valor, el servicio {{site.data.keyword.autoscaling}} no escala horizontalmente la aplicación. Recuento mínimo predeterminado de instancias: El número mínimo de instancias de la aplicación que se pueden iniciar. Si el número de instancias es igual que este valor, el servicio {{site.data.keyword.autoscaling}} no vuelve a escalar verticalmente la aplicación. |
| *Tipo de métrica*	| 	Los tipos de métrica admitidas que se pueden supervisar. Para obtener más información, consulte la Tabla 2. |
| *Escalar horizontalmente* | 	Especifica el umbral que desencadena una acción de escalado horizontal y el número de instancias que se aumentan cuando se desencadena una acción de escalado horizontal. |
| *Escalar verticalmente* |	Especifica el umbral que desencadena una acción de escalado vertical y el número de instancias que se reducen cuando se desencadena una acción de escalado vertical. |
| *Ventana de estadísticas* |	La duración del periodo anterior en que se reconocen los valores de métrica recibidos como válidos. Los valores de métrica son válidos solo si las indicaciones de hora y fecha se incluyen en ese periodo. La unidad del parámetro Ventana de estadísticas es el segundo. |
| *Duración de la infracción*	| La duración del periodo anterior en que se puede desencadenar una acción de escalado. Una acción de escalado se desencadena cuando se recopilan valores de métrica que están por encima del umbral superior, o por debajo del inferior, más tiempo del especificado. La unidad del parámetro de Duración de la infracción es el segundo. |
| *Periodo de enfriamiento del escalado vertical* | Después de producirse una acción de escalado vertical, se ignorarán otras solicitudes de escalado mientras dure el periodo especificado por Periodo de enfriamiento del escalado vertical. La unidad de este parámetro es segundo. |
| *Periodo de enfriamiento del escalado horizontal*	| Después de producirse una acción de escalado horizontal, se ignorarán otras solicitudes de escalado mientras dure el periodo especificado por Periodo de enfriamiento del escalado horizontal. La unidad de este parámetro es segundo. |
| *Huso horario *	| El huso horario en el que se aplica la planificación. |
| *Hora de inicio*  |	La hora de inicio de una planificación recurrente. |
| *Hora de finalización *    |	La hora de finalización de una planificación recurrente.	|
| *Repetición activada *	|	El día de la semana en el que se aplica una planificación recurrente. |
| *Recuento mínimo de instancias * |	El número mínimo de instancias que se pueden iniciar para la aplicación durante el periodo de tiempo especificado en la planificación. |
| *Hora y fecha de inicio* |	La fecha y hora de inicio de la planificación configurada en una fecha específica. |
| *Hora y fecha de finalización* |	La fecha y hora de finalización de la planificación configurada en una fecha específica.	|

Tabla 1. Campos en la política de escalado

| Nombre de métrica | Descripción | Tipo de aplicación admitido |
|-------------|----------------------| ------------------- |
| *Almacenamiento dinámico de JVM* |	El porcentaje de uso de la memoria de almacenamiento dinámico de JVM.	| Liberty for Java |
| *Memoria*   |	El porcentaje de uso de la memoria.	|  Liberty for Java<br/> Node.js <br/> Ruby <br/> |
| *Rendimiento* | Número de solicitudes procesadas por segundo.| Liberty for Java |
| *Tiempo de respuesta* |	Tiempo de respuesta de las solicitudes procesadas.	| Liberty for Java |

Tabla 2. Nombres de métrica admitidos

## Mensajes de error
{: #errmsgs}
Esta sección enumera los mensajes de avisos y error que genera el servicio {{site.data.keyword.autoscaling}}.
 
### CWSCV2004E Hay otro servicio {{site.data.keyword.autoscaling}} enlazado a la aplicación.
**Sólo puede enlazar un servicio {{site.data.keyword.autoscaling}} a una aplicación. Este error se produce cuando se quiere enlazar el servicio {{site.data.keyword.autoscaling}} a una aplicación que ya está enlazada a otro servicio {{site.data.keyword.autoscaling}}. **

Seleccione otra aplicación sin ningún otro servicio {{site.data.keyword.autoscaling}} enlazado y enlace el servicio {{site.data.keyword.autoscaling}} de destino a esta aplicación.
Si encuentra este error en todos los demás casos, póngase en contacto con el soporte de IBM.

### CWSCV6001E El servidor de API no puede analizar las series JSON de entrada para la API: {0}.
**Este problema se produce al analizar series JSON de entrada.**

Revise el documento JSON de entrada con API y corrija el error.

### CWSCV6002E El servidor de API no puede analizar las series JSON de salida para la API: {0}.
**Este problema se produce al analizar series JSON de entrada.**

Póngase en contacto con el administrador de nube para obtener más información.

### CWSCV6003E Error de formato de las series JSON de entrada: {0} en JSON de entrada para la API: {1}.
**Se ha encontrado un error de formato al analizar las series JSON de entrada.**

Revise el documento JSON de entrada con API y corrija el error.

### CWSCV6004E Error de formato de las series JSON de salida: {0} en JSON de salida para la API: {1}.
**Se ha encontrado un error de formato al analizar las series JSON de salida.**

Póngase en contacto con el administrador de nube para obtener más información.

### CWSCV6005E Se ha producido un error interno del servidor durante
{0}.
**El error interno de servidor se ha producido al procesar la solicitud.**

Póngase en contacto con el administrador de nube para obtener más información.

### CWSCV6006E No se ha podido realizar la llamada a las API de CloudFoundry: {0}
**Se ha producido un error en las llamadas a las API de CloudFoundry.**

Póngase en contacto con el administrador de nube para obtener más información.

### CWSCV6007E No se ha encontrado la aplicación: {0}
**No se ha encontrado la aplicación.**

Revise la información de la aplicación para obtener más información.

### CWSCV6008E Se ha producido el siguiente error al recuperar información de la aplicación {0}: {1}
**La recuperación de información de la aplicación ha fallado con algunos errores.**

Revise la información de la aplicación para obtener más información.

### CWSCV6009E No se ha encontrado el servicio: {0} para la app {1}.
**No se ha podido encontrar el servicio para esta aplicación.**

Revise el enlace de servicio de esta aplicación para obtener más información.

### CWSCV6010E No se ha encontrado la política para la app {0}.
**No se ha podido encontrar la política para esta aplicación.**

Revise la configuración de la aplicación para obtener más información.

### CWSCV6011E La autenticación interna ha fallado durante {0}
**La autenticación interna ha fallado.**

Póngase en contacto con el administrador de nube para obtener más información.


# rellinks
## ejemplos
* [Guías de aprendizaje: Convierta su aplicación en elástica en {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Cloud Foundry Architecture Labs](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
* [Rest API of IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}}](https://www.{DomainName}/docs/api/content/api/auto-scaling/index.html){:new_window}

## general
* [{{site.data.keyword.Bluemix_notm}} Hoja de precios de ](https://console.{DomainName}/pricing/){:new_window}
* [{{site.data.keyword.Bluemix_notm}}  Requisitos previos](https://developer.ibm.com/bluemix/support/#prereqs){:new_window}
* [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}

