---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Acerca de {{site.data.keyword.openwhisk_short}}

{{site.data.keyword.openwhisk}} es una plataforma de cálculo dirigida por sucesos, también conocida como Computación sin servidor o Function as a Service (FaaS), que ejecuta código en respuesta a sucesos o invocaciones directas. La figura siguiente muestra la arquitectura de {{site.data.keyword.openwhisk}} de alto nivel.
{: shortdesc}

![Arquitectura de {{site.data.keyword.openwhisk_short}}](./images/OpenWhisk.png)

Como ejemplos de sucesos se pueden citar cambios en los registros de base de datos, lecturas de sensor IoT que sobrepasen una
temperatura determinada, nuevas confirmaciones de código en un repositorio GitHub o solicitudes HTTP sencillas desde apps web o de móvil. Los sucesos
de orígenes de sucesos externos e internos se ponen en el canal por medio de un desencadenante, y las reglas permiten acciones
de respuesta para dichos sucesos.

Las acciones pueden ser pequeños fragmentos de código JavaScript o código Swift, o bien código binario personalizado
incluido en un contenedor Docker. Las acciones en {{site.data.keyword.openwhisk_short}} se despliegan de forma instantánea y se ejecutan siempre que se active un desencadenante. Cuantos
más desencadenantes se activen, más acciones se invocan. Si no se activan desencadenantes, no se ejecuta código de acción, con lo que
no hay coste.

Además de asociar acciones a desencadenantes, es posible invocar directamente una acción utilizando
la API de {{site.data.keyword.openwhisk_short}}, CLI o el SDK de iOS. También se puede encadenar un conjunto de acciones
sin tener que escribir código. Cada acción de la cadena se invoca en secuencia con la salida de una acción pasada como
entrada para la siguiente secuencia.

Con los contenedores o máquinas virtuales de larga ejecución tradicionales, se recomienda desplegar varias MV o contenedores
para que sean resistentes a cortes de una única instancia. No obstante, {{site.data.keyword.openwhisk_short}} ofrece un modelo alternativo
sin sobrecarga de coste relacionada con la resistencia. La ejecución de acciones a demanda proporciona escalabilidad inherente y utilización óptima
ya que el número de acciones en ejecución siempre coincide con la tasa del desencadenante. Además, el desarrollador ahora solo se centra
en el código, y no se preocupa de la supervisión, parches y seguridad del servidor subyacente, ni de su infraestructura de almacenamiento, de red o del sistema operativo.

Las integraciones con servicios adicionales y proveedores de sucesos se pueden añadir con paquetes. Un paquete es una agrupación de
información de entrada y acciones. La información de entrada es un segmento de código que configura un origen de suceso externo
para activar sucesos desencadenantes. Por ejemplo, un desencadenante creado con información de entrada de cambios de Cloudant configura un
servicio para que active el desencadenante siempre que se modifique un documento o se añada a una base de datos Cloudant. Las acciones
en paquetes representan lógica reutilizable que un proveedor de servicios puede poner a disponibilidad de los desarrolladores
para que no solo puedan utilizar el servicio como un origen de sucesos, sino también invocar las API de dicho servicio.

Un catálogo de paquetes existente ofrece una forma rápida de mejorar las aplicaciones con prestaciones útiles, y para acceder
a servicios externos en el ecosistema. Algunos de los servicios externos que están habilitados para {{site.data.keyword.openwhisk_short}} son Cloudant, The Weather Company, Slack y GitHub.


## Funcionamiento de {{site.data.keyword.openwhisk_short}}
{: #openwhisk_how}

Como proyecto de código abierto, OpenWhisk aprovecha la tecnología de gigantes que incluyen Nginx, Kafka, Consul, Docker, CouchDB. Todos estos componentes se combinan para formar un “servicio de programación basado en sucesos sin servidor”. Para explicar detalladamente todos los componentes, haremos un seguimiento de una invocación de una acción a medida que fluye por el sistema. Una invocación en OpenWhisk es el núcleo del motor del sistema sin servidor: ejecutar el código que el usuario ha incorporado en el sistema y devolver los resultados de la ejecución.

### Creación de la acción

Para definir un poco de contexto en la explicación, en primer lugar vamos a crear una acción en el sistema. Luego utilizaremos dicha acción para explicar los conceptos cuando realicemos el seguimiento del flujo en el sistema. En los siguientes mandatos se da por supuesto que la [CLI de OpenWhisk está correctamente configurada](https://github.com/openwhisk/openwhisk/tree/master/docs#setting-up-the-openwhisk-cli).

Primero crearemos un archivo *action.js* con el siguiente código, que mostrará “Hello World” en stdout y devolverá un objeto JSON que contendrá “world” bajo la clave “hello”.
```javascript
function main() {
    console.log('Hello World');
    return { hello: 'world' };
}
```
{: codeblock}

Creamos la acción utilizando
```
wsk action create myAction action.js
```
{: pre}

Hecho. Ahora queremos invocar esta acción:
```
wsk action invoke myAction
```
{: pre}

## El flujo interno del proceso
¿Qué pasa realmente entre bastidores en OpenWhisk?

![Flujo del proceso de OpenWhisk](images/OpenWhisk_flow_of_processing.png)

### Entrar en el sistema: nginx

En primer lugar, la API de usuario de OpenWhisk se basa en HTTP y sigue un diseño RESTful. Por lo tanto, el mandato enviado mediante la CLI wsk es básicamente una solicitud HTTP realizada al sistema OpenWhisk. El mandato específico anterior se convierte a groso modo en:
```
POST /api/v1/namespaces/$userNamespace/actions/myAction
Host: $openwhiskEndpoint
```
{: screen}

Observe la variable *$userNamespace*. Un usuario tiene acceso al menos a un espacio de nombres. Para simplificar, supondremos que el usuario es el propietario del espacio de nombres en el que se coloca *myAction*.

El primer punto de entrada en el sistema se realiza a través de **nginx**, “un servidor proxy invertido y HTTP”. Se utiliza principalmente para la terminación SSL y para reenviar las llamadas HTTP adecuadas al siguiente componente.

### Entrar en el sistema: Controlador

Sin haber hecho demasiado con nuestra solicitud HTTP, nginx la reenvía al **Controlador**, el siguiente componente de nuestra ruta a través de OpenWhisk. Es una implementación basada en Scala de la API REST real (basada en **Akka** y **Spray**) y por lo tanto sirve como interfaz para todo lo que el usuario puede hacer, incluidas las solicitudes [CRUD](https://en.wikipedia.org/wiki/Create,_read,_update_and_delete) destinadas a las entidades de OpenWhisk y la invocación de acciones (que es lo que estamos haciendo).

En primer lugar, el Controlador determina lo que el usuario intenta hacer. Lo hace basándose en el método HTTP utilizado en la solicitud HTTP. En el caso anterior, el usuario emite una solicitud POST a una acción existente, que el Controlador convierte en una **invocación de una acción**.

Dado el papel central que juega el Controlador (de ahí su nombre), dicho componente participará de alguna manera en todos los pasos siguientes.

### Autenticación y autorización: CouchDB

Ahora el Controlador verifica quién es el usuario (*Autenticación*) y si tiene privilegio para hacer lo que quiere hacer con esta entidad (*Autorización*). Las credenciales incluidas en la solicitud se comparan con la base de datos llamada **subjects** de una instancia **CouchDB**.

En este caso, se comprueba que el usuario existe en la base de datos de OpenWhisk y que tiene privilegio para invocar la acción myAction, que damos por supuesto que es una acción en un espacio de nombres propiedad del usuario. Esto último otorga al usuario el privilegio de invocar la acción, que es lo que desea hacer.

Se abre la puerta al siguiente paso del proceso.

### Obtención de la acción: CouchDB… de nuevo

Como ahora el Controlador está seguro de que el usuario tiene permiso y privilegios para invocar la acción, carga esta acción (en este caso *myAction*) desde la base de datos **whisks** en CouchDB.

El registro de la acción contiene principalmente el código que se va a ejecutar (el mostrado anteriormente) y los parámetros predeterminados que el usuario desea pasar a la acción, junto con los parámetros que ha incluido en la solicitud de invocación real. También contiene las restricciones de recursos impuestas sobre su ejecución, como por ejemplo la memoria que tiene permitido consumir.

En este caso en concreto, nuestra acción no toma ningún parámetro (la definición de parámetros de la función es una lista vacía), por lo que daremos por supuesto que no hemos definido ningún parámetro predeterminado ni hemos enviado ningún parámetro específico a la acción, lo que constituye el caso más simple desde este punto de vista.

### Quién hay para invocar la acción: Consul

El Controlador (en concreto, la parte de equilibrio de carga del mismo) tiene todo lo necesario para que el código se pueda empezar a ejecutar. Debe saber quién está disponible para hacerlo. Se utiliza **Consul**, un servicio de descubrimiento, para realizar un seguimiento de los ejecutores disponibles en el sistema mediante la comprobación continua del estado del sistema. Estos ejecutores también se denominan **Invocadores**.

Ahora que sabe qué Invocadores están disponibles, el Controlador elige uno de ellos para invocar la acción solicitada.

En este caso supondremos que el sistema tiene 3 Invocadores disponibles, los Invocadores del 0 al 2, y que el Controlador ha elegido el *Invocador 2* para invocar la acción.

### Hagan cola: Kafka

A partir de ahora, la solicitud de invocación que se ha enviado está sujeta principalmente a dos problemas potenciales:

1. El sistema puede colgarse, con lo que se perdería la invocación.
2. El sistema puede estar sometido a una carga tan pesada que la invocación tenga que esperar a que terminen otras invocaciones.

La solución en ambos casos es **Kafka**, “un sistema de mensajería de tipo publicación-suscripción distribuido de alto rendimiento”. El Controlador y el Invocador solo se comunican a través de mensajes que Kafka guarda en almacenamiento intermedio de forma permanente. Esto incrementa la carga de almacenamiento intermedio en memoria, aumentando el riesgo de que se produzca una *OutOfMemoryException* del Controlador y del Invocador, así que se asegura que no se pierdan los mensajes en el caso de que se cuelgue el sistema.

Para que se invoque la acción, el Controlador publica un mensaje en Kafka que contiene la acción que se debe invocar y los parámetros que hay que pasar a dicha acción (en este caso, ninguno). Este mensaje se dirige al Invocador que ha elegido el Controlador de la lista que ha obtenido de Consul.

Cuando Kafka haya confirmado que ha recibido el mensaje, se responde a la solicitud HTTP al usuario con **ActivationId**. El usuario lo utilizará más adelante para acceder a los resultados de la invocación específica. Observe que se trata de un modelo de invocación asíncrona, donde la solicitud HTTP termina en cuanto el sistema acepta la solicitud de invocar la acción. Dispone de un modelo síncrono (que recibe el nombre de invocación de bloqueo), pero no se trata en este artículo.

### Invocación del código: Invocador

El **Invocador** es el centro de OpenWhisk. La función del Invocador es invocar una acción. También se implementa en Scala. Pero va mucho más allá. Para ejecutar acciones de forma aislada y segura utiliza **Docker**.

Docker sirve para configurar un nuevo entorno de encapsulación automática (denominado *contenedor*) para cada acción que se invoca de forma rápida, aislada y controlada. En pocas palabras, para cada invocación de una acción se genera un contenedor Docker, se inserta el código de la acción y se ejecuta utilizando los parámetros que se le han pasado; una vez obtenido el resultado, el contenedor se destruye. Aquí también se realiza gran parte de la optimización del rendimiento para reducir la sobrecarga y agilizar los tiempos de respuesta. 

En nuestro caso específico, como tenemos una acción basada en *Node.js*, el Invocador iniciará un contenedor Node.js, insertará el código procedente de *myAction*, lo ejecutará sin parámetros, extraerá el resultado, guardará los registros y destruirá el contenedor Node.js.

### Almacenamiento de los resultados: CouchDB de nuevo

Cuando el Invocador obtiene el resultado, se almacena en la base de datos **whisks** como una activación bajo el ActivationId que se muestra a continuación. La base de datos **whisks** se encuentra en **CouchDB**.

En nuestro caso específico, el Invocador obtiene el objeto JSON resultante de la acción, recupera el registro que ha escrito Docker, los coloca en el registro de activación y lo almacena en la base de datos. El código tendría este aspecto:

```json
{
   "activationId": "31809ddca6f64cfc9de2937ebd44fbb9",
   "response": {
       "statusCode": 0,
       "result": {
           "hello": "world"
       }
   },
   "end": 1474459415621,
   "logs": [
       "2016-09-21T12:03:35.619234386Z stdout: Hello World"
   ],
   "start": 1474459415595,
}
```
{: codeblock}

Observe cómo el registro contiene el resultado devuelto y los registros escritos. También contiene la hora de inicio y de finalización de la invocación de la acción. Hay más campos en un registro de activación; para simplificar se muestra una versión reducida.

Ahora puede volver a utilizar la API REST (volver al paso 1) para obtener su activación y, por lo tanto, el resultado de la acción. Para ello debe utilizar:

```bash
wsk activation get 31809ddca6f64cfc9de2937ebd44fbb9
```
{: pre} 

### Resumen

Hemos visto cómo una sencilla acción **wsk action invoke myAction** pasa por las distintas fases del sistema {{site.data.keyword.openwhisk_short}}. El propio sistema consta principalmente de sólo dos componentes personalizados, el **Controlador** y el **Invocador**. Todo lo demás ya se encuentra allí, desarrollado por los muchos miembros de la comunidad de código abierto.

Puede encontrar información adicional sobre {{site.data.keyword.openwhisk_short}} en los temas siguientes:

* [Nombre de entidad](./openwhisk_reference.html#openwhisk_entities)
* [Semánticas de acción](./openwhisk_reference.html#openwhisk_semantics)
* [Límites](./openwhisk_reference.md#openwhisk_syslimits)
* [API REST](./openwhisk_reference.md#openwhisk_ref_restapi)
