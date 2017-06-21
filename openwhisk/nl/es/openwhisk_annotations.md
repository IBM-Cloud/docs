---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Anotaciones en activos de OpenWhisk

Las acciones, desencadenantes, reglas y paquetes de OpenWhisk (conocidos de forma colectiva como activos) pueden contener `anotaciones`. Las anotaciones se adjuntan a los activos del mismo modo que se adjuntan parámetros con una `clave` que define un nombre y un `valor` que define el valor. Se recomienda definirlos desde la interfaz de línea de mandatos (CLI) mediante `--annotation` o `-a` para abreviar.
{: shortdesc}

Razón fundamental: se han añadido anotaciones a OpenWhisk para permitir que se experimente sin realizar cambios en el esquema del activo subyacente. En el momento de redactar este documento, no hemos definido de forma deliberada las `anotaciones` que se permiten. Cuando empecemos a utilizar anotaciones con frecuencia para impartir cambios semánticos empezaremos a documentarlas.

El uso principal de las anotaciones actualmente consiste en documentar acciones y paquetes. Verá que muchos de los paquetes del catálogo de OpenWhisk contienen anotaciones, como una descripción de las funciones que ofrecen sus acciones, los parámetros necesarios para enlazar el paquete y los parámetros de invocación, si un parámetro es "secreto" (por ejemplo, una contraseña) o no. Hemos ido inventando anotaciones a medida que ha sido necesario, por ejemplo para permitir la integración de la IU.

A continuación se muestra un ejemplo de conjunto de anotaciones para una acción `echo` que devuelve sus argumentos de entrada sin modificar (es decir, `function main(args) { return args }`). Esta acción puede resultar útil para registrar parámetros de entrada para ejemplos como parte de una secuencia o de una regla.

```
wsk action create echo echo.js \
    -a description 'Una acción que devuelve su entrada. Útil para registrar entrada para habilitar debug/replay.' \
    -a parameters  '[{ "required":false, "description": "Any JSON entity" }]' \
    -a sampleInput  '{ "msg": "Five fuzzy felines"}' \
    -a sampleOutput '{ "msg": "Five fuzzy felines"}'
```
{: pre}

Las anotaciones se han utilizado para describir paquetes son:

- `description`: una sucinta descripción del paquete
- `parameters`: una matriz que describe los parámetros que abarca el paquete (que se describen a continuación)

De forma similar, para acciones: 

- `description`: una sucinta descripción de la acción
- `parámetros`: una matriz que describe las acciones necesarias para ejecutar la acción
- `sampleInput`: un ejemplo que muestra el esquema de entrada con los valores típicos
- `sampleOutput`: un ejemplo que muestra el esquema de salida, generalmente para `sampleInput`

Las anotaciones que se han utilizado para describir parámetros incluyen:

- `name`: el nombre del parámetro
- `description`: una sucinta descripción del parámetro
- `doclink`: un enlace con más documentación sobre el parámetro (útil para señales OAuth, por ejemplo) 
- `required`: true para los parámetros obligatorios y false para los opcionales
- `bindTime`: true si se debe especificar el parámetro cuando se enlaza un paquete
- `type`: el tipo de parámetro, que puede ser `password`, `array` (aunque se puede utilizar en más situaciones)

Las anotaciones *no* se comprueban. Aunque puede suceder que se utilicen anotaciones para inferir si una composición de dos acciones en una secuencia es válida, por ejemplo, el sistema aún no lo hace.

## Anotaciones específicas de acciones de la web
{: #openwhisk_annotations_webactions}

La API principal se ha ampliado recientemente con características nuevas. Para permitir que paquetes y acciones participan en estas características, hemos incorporado las siguientes nuevas anotaciones con significado semántico. Estas anotaciones se deben establecer explícitamente en `true` para que tengan efecto. Si se cambia el valor `true` por `false`, el activo adjunto se excluirá de la nueva API. Las anotaciones no tienen ningún otro significado en el sistema. Las anotaciones son:

- `final`: solo se aplica a una acción. Convierte en inalterables todos los parámetros de acción ya definidos. Un parámetro de una acción que lleve la anotación no se puede modificar mediante parámetros durante la invocación una vez el parámetro tiene un valor definido mediante el paquete que lo contiene o la definición de la acción.
- `web-export`: solo se aplica a una acción. Si está definida, permite que las llamadas REST puedan acceder a su acción correspondiente *sin* autenticación. Las llamamos [*acciones de la web*](openwhisk_webactions.html) porque permiten utilizar acciones de OpenWhisk desde un navegador, por ejemplo. Es importante tener en cuenta que el *propietario* de la acción de la web es el responsable del coste de ejecutarlas en el sistema (es decir, el *propietario* de la acción también es el propietario del registro de activaciones).
- `require-whisk-auth`: se aplica a una acción. Si una acción lleva la anotación `web-export` y esta anotación es también `true`, solo puede acceder a la ruta un asunto autenticado. Es importante tener en cuenta que el *propietario* de la acción de la web es el responsable del coste de ejecutarlas en el sistema (es decir, el *propietario* de la acción también es el propietario del registro de activaciones).
- `raw-http`: solo se aplica a una acción en presencia de una anotación `web-export`. Si aparece, los parámetros de cuerpo y consulta de la solicitud HTTP se pasan parámetros como propiedades reservadas.

