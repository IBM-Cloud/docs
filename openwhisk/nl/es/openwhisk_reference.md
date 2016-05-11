---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock:.codeblock}
{:screen:.screen}
{:pre: .pre}

# Detalles del sistema {{site.data.keyword.openwhisk_short}}
{: #openwhisk_reference}
*Última actualización: 14 de abril de 2016*

En las secciones siguientes se proporcionan más detalles sobre el sistema {{site.data.keyword.openwhisk}}.
{: shortdesc}

## Entidades de {{site.data.keyword.openwhisk_short}}
{: #openwhisk_entities}

### Espacios de nombres y paquetes

Las acciones, desencadenantes y reglas de {{site.data.keyword.openwhisk_short}} pertenecen a un espacio de nombres y, opcionalmente, a un paquete.

Los paquetes pueden contener acciones e información de entrada. Un paquete no puede contener otro paquete, por lo que no se permite anidamiento de paquetes. Además, las entidades no tienen que estar obligatoriamente contenidas en un paquete.

En Bluemix, un par organización+espacio corresponde a un espacio de nombres de {{site.data.keyword.openwhisk_short}}. Por ejemplo,
la organización `BobsOrg` y el espacio `dev` corresponderían al espacio de nombres
`/BobsOrg_dev` de {{site.data.keyword.openwhisk_short}}.

Puede crear sus propios espacios de nombres si está autorizado a ello. El espacio de nombres `/whisk.system`
se reserva para entidades distribuidas con el sistema {{site.data.keyword.openwhisk_short}}.


### Nombres completos

El nombre completo de una entidad es `/namespaceName[/packageName]/entityName`. Observe que
se utiliza `/` para delimitar espacios de nombres, paquetes y entidades. Además, los espacios de nombres deben
tener una `/` como prefijo.

Por comodidad, el espacio de nombres se puede dejar fuera si es el *espacio de nombres por omisión* del usuario.

Por ejemplo, supongamos un usuario cuyo espacio de nombres por omisión es `/myOrg`. A continuación hay ejemplos
de los nombres completos de una serie de entidades y sus alias.

| Nombre completo | Alias | Espacio de nombres | Paquete | Nombre |
| --- | --- | --- | --- | --- |
| `/whisk.system/cloudant/read` | - | `/whisk.system` | `cloudant` | `read` |
| `/myOrg/video/transcode` | `video/transcode` | `/myOrg` | `video` | `transcode` |
| `/myOrg/filter` | `filter` | `/myOrg` | - | `filter` |

Usará este esquema de denominación cuando usa la CLI de {{site.data.keyword.openwhisk_short}}, entre otros lugares.

### Nombres de entidad

Los nombres de todas las entidades incluidas las acciones, desencadenantes, reglas, paquetes y los espacios de nombres están en una secuencia de caracteres que cumplen el formato siguiente:

* El primer carácter debe ser un carácter alfanumérico, un dígito o un subrayado.
* Los caracteres posteriores pueden ser alfanuméricos, dígitos y espacios, de cualquiera de lo siguiente: `_`, `@`, `.`, `-`.
* El último carácter no puede ser un espacio.

Concretamente, un nombre debe coincidir con la siguiente expresión regular (expresada mediante sintaxis de metacaracteres de Java):
`\A([\w]|[\w][\w@ .-]*[\w@.-]+)\z`.


## Semánticas de acción
{: #openwhisk_semantics}

En las secciones siguientes se describen los detalles sobre las acciones de
{{site.data.keyword.openwhisk_short}}.

### Falta de estado

Las implementaciones de acciones deberían ser sin estado, o *idempotent*. Aunque el sistema no impone esta propiedad,
no ha garantía de que cualquier estado mantenido por una acción esté disponible entre invocaciones.

Además, se puede dar la creación de varias instancias de una acción, teniendo cada creación de instancias su propio estado. Una
invocación de acción se podría asignar a cualquiera de estas creaciones de instancias.

### Entrada y salida de invocación

La entrada y salida de una acción es un diccionario de pares de clave/valor. La clave es una serie, y el valor un valor JSON válido.

### Ordenación de invocaciones de acciones
{: #openwhisk_ordering}

Las invocaciones de una acción no están ordenadas. Si el usuario invoca una acción dos veces desde la línea de mandatos
o la API de REST, la segunda invocación podría ejecutarse antes que la primera. Si las acciones tienen efectos secundarios,
se podrían observar en cualquier orden.

Además, no existe ninguna garantía de que las acciones se ejecuten de forma atómica. Dos acciones se pueden ejecutar de forma simultánea
y tener efectos secundarios que se entrelacen. Los efectos secundarios de simultaneidad dependerán de la implementación.

### Semánticas Una como máximo
{: #openwhisk_atmostonce}

El sistema admite como máximo una invocación de acciones.

Cuando se recibe una solicitud de invocación, el sistema registra la solicitud, y asigna una activación.

El sistema devuelve un ID de activación (en el caso de una invocación sin bloqueo) para confirmar que
la invocación se ha recibido. Tenga en cuenta que en ausencia de esta respuesta (quizás debido a la caída de una conexión de red),
es posible que se reciba la invocación.

El sistema intenta invocar la acción una vez, lo que tiene uno de los cuatro resultados siguientes:
- *success*: la invocación de la acción se ha completado correctamente.
- *application error*: la invocación de la acción ha sido correcta, pero la acción ha devuelto un valor de error a propósito,
por ejemplo debido a una condición previa de los argumentos que no se cumpla.
- *action developer error*: la acción se ha invocado, pero se ha completado de forma anómala, por ejemplo, la acción
no ha capturado una excepción o se ha producido un error de sintaxis.
- *whisk internal error*: el sistema no ha podido invocar la acción.
El resultado se registra en el campo `status` del registro de activación,
como documento en la sección siguiente.

Cada invocación que se recibe correctamente, y que se impute al usuario, tendrá un registro de activación.


## Registro de activación
{: #openwhisk_ref_activation}

Cada invocación de acción y activación de desencadenante tiene como resultado un registro de activación.

Un registro de activación contiene los campos siguientes:

- *activationId*: el ID de activación.
- *start* y *end*: indicaciones de fecha y hora que registran el inicio y final de la activación. Los valores
están en [formato de hora UNIX](http://pubs.opengroup.org/onlinepubs/9699919799/basedefs/V1_chap04.html#tag_04_15).
- *namespace* y `name`: el espacio de nombres y el nombre de la entidad.
- *logs*: una matriz de series con los registros generados por la acción durante su activación. Cada elemento de matriz corresponde
con una salida de línea de stdout o stderr para la acción, e incluye la hora y secuencia de la salida de registro. La estructura es de la siguiente manera: ```TIMESTAMP STREAM: LOG_OUTPUT```.
- *response*: un diccionario que define las claves `success`, `status` y `result`:
  - *status*: el resultado de activación, que puede ser uno de los valores siguientes: "success", "application error", "action developer error", "whisk internal error".
  - *success*: es `true` solo si el estado es `"success"`
- *result*: un diccionario que contiene el resultado de activación. Si la activación ha sido correcta, contiene el valor devuelto por
la acción. Si la activación no ha sido correcta, `result` tiene la garantía de contener la clave `error`,
generalmente con una explicación del fallo.


## Acciones JavaScript
{: #openwhisk_ref_javascript}

### Prototipo de función

Las acciones JavaScript de {{site.data.keyword.openwhisk_short}} se ejecutan en un tiempo de ejecución Node.js, actualmente en la versión 0.12.9.

Las acciones escritas en JavaScript se deben confinar a un único archivo. El archivo puede contener varias funciones pero,
por convenio, debe existir una función llamada `main` y es la que se llama cuando se invoca la acción. Por ejemplo,
a continuación se muestra un ejemplo de una acción con varias funciones.

```
function main() {
    return { payload: helper() }
}

function helper() {
    return new Date();
}
```
{: codeblock}

Los parámetros de entrada de la acción se pasan como un objeto JSON como un parámetro a la función
`main`. El resultado de la activación correcta también es un objeto JSON pero se devuelve de forma distinta,
según si la acción es síncrona o asíncrona, según se describe en la sección siguiente.


### Comportamiento síncrono y asíncrono

Es frecuente para funciones de JavaScript continuar la ejecución en una función de devolución de llamada incluso después del
retorno. Para ajustarse a esto, una activación de una acción de JavaScript puede ser *síncrona* o *asíncrona*.

Una activación de una acción de JavaScript es **síncrona** si la función main existe en una de las condiciones siguientes:

- La función main existe sin ejecutar una sentencia ```return```.
- La función main existe ejecutando una sentencia ```return``` que devuelve cualquier valor *excepto* ```whisk.async()``.

Aquí hay dos ejemplos de acciones síncronas.

```
// una acción síncrona
function main() {
  return {payload: 'Hello, World!'};
}
```
{: codeblock}

```
// una acción en la que cada vía tiene como resultado una activación síncrona
function main(params) {
  if (params.payload == 0) {
     return;
  } else if (params.payload == 1) {
     return whisk.done();    // indicates normal completion
  } else if (params.payload == 2) {
    return whisk.error();   // indicates abnormal completion
  }
}
```
{: codeblock}

Una activación de acción de JavaScript es **asíncrona** si la función main existe invocando
```return whisk.async();```.  En este caso, el sistema presupone que la acción aún está en ejecución, hasta que la acción ejecuta una de las siguientes:
- ```return whisk.done();```
- ```return whisk.error();```

A continuación se muestra un ejemplo de una acción que se ejecuta de forma asíncrona.

```
function main() {
    setTimeout(function() {
        return whisk.done({done: true});
    }, 100);
    return whisk.async();
}
```
{: codeblock}

Es posible que una acción sea síncrona en varias entradas y asíncrona en otras. A continuación se muestra un ejemplo.

```
  function main(params) {
      if (params.payload) {
         setTimeout(function() {
            return whisk.done({done: true});
         }, 100);
         return whisk.async();  // asynchronous activation
      }  else {
         return whisk.done();   // synchronous activation
      }
  }
```
{: codeblock}

- En este caso, la función `main` debería devolver `whisk.async()`. Cuando el resultado de la activación esté disponible, la función `whisk.done()` se debería invocar con el resultado pasado como objeto JSON. A esto se denomina
activación *asíncrona*.

Tenga en cuenta que, independientemente de si la activación es síncrona o asíncrona, la invocación de la acción puede ser o no de bloqueo (blocking o non-blocking).

### Métodos SDK adicionales

La función `whisk.invoke()` invoca otra acción. Acepta como argumento un diccionario que define los parámetros siguientes:

- *name*: nombre completo de la acción a invocar,
- *parameters*: un objeto JSON que representa la entrada a la acción invocada. Si se omite, tiene como valor predeterminado un objeto vacío.
- *apiKey*: la tecla de autorización con la que invocar la acción. Tiene como valor predeterminado `whisk.getAuthKey()`. 
- *blocking*: si la acción se debe invocar en modalidad de bloque o no bloqueo. Tiene como valor predeterminado
`false`, indicando una invocación que no es de bloqueo.
- *next*: una función de devolución de llamada opcional a ejecutar cuando se complete la invocación.

La firma para `next` es `function(error, activation)`, donde:

- `error` es `false` si la invocación ha sido correcta, y un valor verdadero si ha fallado, por lo general una serie que describe el error.
- En caso de errores, `activation` podría quedar sin definir, según la modalidad de error.
- Cuando está definida, `activation` es un diccionario con los campos siguientes:
  - *activationId*: el ID de activación:
  - *result*: si la acción se ha invocado en modalidad de bloqueo: el resultado de la acción como un objeto JSON, o
bien `undefined`.

La función `whisk.trigger()` activa un desencadenante. Acepta como argumento un objeto JSON con los parámetros siguientes:

- *name*: nombre completo del desencadenante a invocar.
- *parameters*: un objeto JSON que representa la entrada al desencadenante. Si se omite, tiene como valor predeterminado un objeto vacío.
- *apiKey*: la tecla de autorización con la que activar el desencadenante. Tiene como valor predeterminado `whisk.getAuthKey()`.
- *next*: una devolución de llamada opcional a ejecutar cuando se complete la acción.

La firma para `next` es `function(error, activation)`, donde:

- `error` es `false` si la activación ha sido correcta, y un valor verdadero si ha fallado, por lo general una serie que describe el error.
- En caso de errores, `activation` podría quedar sin definir, según la modalidad de error.
- Cuando está definida, `activation` es un diccionario con un campo `activationId` que contiene el id. de activación.

La función `whisk.getAuthKey()` devuelve la clave de autorización bajo la que se ejecuta la acción. Normalmente,
no necesita invocar esta función directamente, ya que se utiliza implícitamente por parte de las funciones
`whisk.invoke()` y `whisk.trigger()`.

### Entorno de tiempo de ejecución
{: #openwhisk_ref_runtime_environment}

Las acciones JavaScript se ejecutan en un entorno Node.js versión 0.12.9 con los paquetes siguientes disponibles para que los use la acción:

- apn
- async
- body-parser
- btoa
- cloudant
- commander
- consul
- cookie-parser
- cradle
- errorhandler
- express
- express-session
- jade
- log4js
- fusionar/fusión
- moment
- mustache
- nano
- node-uuid
- oauth2-server
- process
- request
- rimraf
- semver
- serve-favicon
- socket.io
- superagent
- swagger-tools
- tmp
- watson-developer-cloud
- when
- xml2js
- xmlhttprequest
- yauzl


## Acciones de Docker
{: #openwhisk_ref_docker}

Las acciones Docker ejecutan un binario proporcionado por el usuario en un contenedor Docker. El binario se ejecuta en una imagen Docker
basada en Ubuntu 14.04 LTD, por lo que el binario debe ser compatible con dicha distribución.

El parámetro "payload" de entrada de la acción se pasa como un argumento posicional al programa binario, y la salida estándar
de la ejecución del programa se devuelve en el parámetro "result".

El esqueleto de Docker es una forma cómoda de construir imágenes de Docker compatibles con {{site.data.keyword.openwhisk_short}}. Puede instalar el esqueleto con el mandato de CLI de `wsk sdk install docker`.

El programa binario principal se debe copiar al archivo `dockerSkeleton/client/clientApp`. Los archivos o bibliotecas
de acompañamiento pueden estar en el directorio `dockerSkeleton/client`.

También puede incluir los pasos de compilación o dependencias, modificando `dockerSkeleton/Dockerfile`. Por ejemplo, puede
instalar Python si su acción es un script Python.


## Límites del sistema
{: #openwhisk_syslimits}

{{site.data.keyword.openwhisk_short}} tiene algunos límites del sistema, incluyendo la cantidad de memoria que utiliza una acción y
cuántas invocaciones de acción se permiten por hora. En la tabla siguiente se proporciona una lista con los límites predeterminados.

| límite | descripción | configurable | unidad | predeterminado |
| ----- | ----------- | ------------ | -----| ------- |
| timeout | un contenedor no tiene permiso para ejecutarse más de N milisegundos | por acción |  milisegundos | 60000 |
| memory | un contenedor no tiene permiso para asignar más de n MB de memoria | por acción | MB | 256 |
| concurrent | no se permiten más de N activaciones simultáneas por espacio de nombres | por espacio de nombres | número | 100 |
| minuteRate | un usuario no puede invocar más de este número de acciones por minuto | por usuario | número | 120 |
| hourRate | un usuario no puede invocar más de este número de acciones por minuto | por usuario | número | 3600 |

### Tiempo de espera por acción (ms) (Predeterminado: 60s)
* El límite de tiempo de espera N está en el intervalo [100ms..300000ms] y se establece por acción, en milisegundos.
* Un usuario puede cambiar el límite cuando crea la acción.
* Un contenedor que se ejecuta más de N milisegundos, se finaliza.

### Memoria por acción (MB) (Predeterminado: 256MB)
* El límite de memoria M está en el intervalo [128MB..512MB] y se establece por acción en MB.
* Un usuario puede cambiar el límite cuando crea la acción.
* Un contenedor no puede tener más memoria asignada del límite.

### Por espacio de nombres, núm. invocaciones simultáneas (Predeterminado: 100)
* El número de activaciones que hay actualmente en proceso para un espacio de nombres no pueden ser más de 100.
* El límite predeterminado se puede configurar de forma estática por medio de whisk en consul kvstore.
* Un usuario no puede actualmente cambiar los límites.


### Invocaciones por minuto/hora (#) (Fijo: 120/3600)
* El límite de tasa N se establece en 120/3600, y limita el número de invocaciones de acción en espacios de tiempo de un minuto/hora.
* Un usuario no puede cambiar este límite cuando crea la acción.
* Una llamada de la CLI que supere este límite recibe un código de error que corresponde a TOO_MANY_REQUESTS.
