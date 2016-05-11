---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Acerca de {{site.data.keyword.openwhisk}}

*Última actualización: 22 de febrero de 2016*

En las secciones siguientes se proporcionan detalles sobre {{site.data.keyword.openwhisk}}.
{: shortdesc}

## Funcionamiento de {{site.data.keyword.openwhisk_short}}
{: #openwhisk_how}

{{site.data.keyword.openwhisk_short}} es una plataforma de cálculo dirigida por sucesos que ejecuta código en respuesta
a sucesos o invocaciones directas.

La figura siguiente muestra la arquitectura de {{site.data.keyword.openwhisk_short}} de alto nivel.

![Arquitectura de {{site.data.keyword.openwhisk_short}} ](OpenWhisk.png)

Como ejemplos de sucesos se pueden citar cambios en los registros de base de datos, lecturas de sensor IoT que sobrepasen una
temperatura determinada, nuevas confirmaciones de código en un repositorio GitHub o solicitudes HTTP sencillas desde apps web o de móvil. Los sucesos
de orígenes de sucesos externos e internos se ponen en el canal por medio de un desencadenante, y las reglas permiten acciones
de respuesta para dichos sucesos.

Las acciones pueden ser pequeños fragmentos de código JavaScript o código Swift, o bien binarios personalizados
incluidos en un contenedor Docker. Las acciones en {{site.data.keyword.openwhisk_short}} se despliegan de forma instantánea y se ejecutan siempre que se active un desencadenante. Cuantos
más desencadenantes se activen, más acciones se invocan. Si no se activan desencadenantes, no se ejecutan código de acción, con lo que
no hay coste.

Además de asociar acciones a desencadenantes, es posible invocar directamente una acción utilizando
la API de {{site.data.keyword.openwhisk_short}}, CLI o el SDK de iOS. También se puede encadenar un conjunto de acciones
sin tener que escribir código. Cada acción de la cadena se invoca en secuencia con la salida de una acción pasada como
entrada para la siguiente secuencia.

Con los contenedores o máquinas virtuales de larga ejecución tradicionales, se recomienda desplegar varias MV o contenedores
para que sean resistentes a cortes de una única instancia. No obstante, {{site.data.keyword.openwhisk_short}} ofrece un modelo alternativo
sin sobrecarga de coste relacionada con la resistencia. Al ejecución de acciones a demanda proporciona escalabilidad inherente y utilización óptima
ya que el número de acciones en ejecución siempre coincide con la tasa del desencadenante. Además, el desarrollador ahora solo se centra
en su código, y no se preocupa de la supervisión, parches y seguridad del servidor subyacente, ni de su infraestructura de almacenamiento, de red o del sistema operativo.

Las integraciones con servicios adicionales y proveedores de sucesos se pueden añadir con paquetes. Un paquete es una agrupación de
información de entrada y acciones. La información de entrada es un segmento de código que configura un origen de suceso externo
para activar sucesos desencadenantes. Por ejemplo, un desencadenante creado con información de entrada de cambios de Cloudant configura un
servicio para que active el desencadenante siempre que se modifique un documento o se añada a una base de datos Cloudant. Las acciones
en paquetes representan lógica reutilizable que un proveedor de servicios puede hacer disponible para que los desarrolladores
no solo puedan utilizar el servicio como un origen de sucesos, sino que también invoquen las API de dicho servicio.

Un catálogo de paquetes existente ofrece una forma rápida de mejorar las aplicaciones con prestaciones útiles, y para acceder
a servicios externos en el ecosistema. Algunos de los servicios externos que están habilitados para
{{site.data.keyword.openwhisk_short}} son Cloudant, The Weather Company, Slack y GitHub.


## Casos de uso común
{: #openwhisk_use_cases}

El modelo de ejecución ofrecido por {{site.data.keyword.openwhisk_short}} admite diversos casos de uso. En las secciones siguientes
se incluyen ejemplos típicos.

### Descomposición de aplicaciones en microservicios
La naturaleza modular e inherentemente escalable de {{site.data.keyword.openwhisk_short}} hace que sea adecuado para
implementar partes granulares de lógica en acciones. Por ejemplo, {{site.data.keyword.openwhisk_short}} puede ser
útil para eliminar tareas de carga intensa, que pudieran tener picos (de fondo) del código de la interfaz e implementar dichas tareas
como acciones.

### Programa de fondo móvil
Muchas aplicaciones de móvil precisan de lógica en el lado del servidor. Dado que los desarrolladores de entornos móviles no suelen tener
experiencia en la gestión de la lógica en el parte del servidor y se centrarán más en la ejecución de las apps en el dispositivo,
usar {{site.data.keyword.openwhisk_short}} como programa de fondo en la parte del servidor es una solución. Además,
el soporte integrado para Swift permite a los desarrolladores reutilizar sus habilidades de programación existentes en iOS.

### Proceso de datos
Con la cantidad de datos ahora disponible, el desarrollo de aplicaciones precisa de la capacidad de procesar nuevos datos, y
potencialmente reaccionar a ellos. Este requisito incluye el proceso tanto de registros de base de datos estructurado, como de documentos no estructurados, imágenes o vídeos.

### IoT
De forma inherente, los escenarios de Internet de las cosas suelen ser controlados por sensores. Por ejemplo, una acción
en {{site.data.keyword.openwhisk_short}} se podría desencadenar si fuera necesario reaccionar a un sensor que supera una
temperatura concreta.



