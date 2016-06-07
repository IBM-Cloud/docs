---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Uso y creación de paquetes de {{site.data.keyword.openwhisk_short}}
{: #openwhisk_packages}
*Última actualización: 28 de marzo de 2016*

En {{site.data.keyword.openwhisk}}, puede utilizar paquetes para agrupar un conjunto de acciones relacionadas y
compartirlas con otros.

Un paquete puede incluir *actions* y *feeds* (acciones e información de entrada).
- Una acción es un segmento de código que se ejecuta en {{site.data.keyword.openwhisk_short}}. Por ejemplo, el paquete Cloudant
incluye acciones para leer y escribir registros en una base de datos Cloudant.
- La información de entrada se utiliza para configurar un origen de suceso externo para activar sucesos desencadenantes. Por ejemplo,
el paquete Alarma incluye información de entrada que puede activar un desencadenante en una frecuencia especificada.

Toda entidad de {{site.data.keyword.openwhisk_short}}, incluyendo los paquetes, pertenecen a un *namespace*,
y el nombre completo de una entidad es `/namespaceName[/packageName]/entityName`. Para obtener más información, consulte
las [Directrices de denominación](./openwhisk_reference.html#openwhisk_entities).

En las secciones siguientes se describe cómo examinar paquetes y usar para ellos los desencadenantes e información de entrada. Además,
si está interesado en contribuir al catálogo con sus propios paquetes, lea las secciones sobre creación y compartición de paquetes.

## Examinar paquetes
{: #openwhisk_packagedisplay}

Hay varios paquetes registrados con {{site.data.keyword.openwhisk_short}}. Puede obtener una lista de paquetes de un espacio de nombres,
lista de las entidades de un paquete y obtener una descripción de las entidades individuales en un paquete.

1. Obtener una lista de paquetes en el espacio de nombres `/whisk.system`.

  ```
  wsk package list /whisk.system
  ```
  {: pre}
  ```
  packages
  /whisk.system/alarms                                              shared
  /whisk.system/cloudant                                            shared
  /whisk.system/github                                              shared
  /whisk.system/samples                                             shared
  /whisk.system/slack                                               shared
  /whisk.system/util                                                shared
  /whisk.system/watson                                              shared
  /whisk.system/weather                                             shared
  ```
  {: screen}

2. Obtener una lista de entidades en el paquete `/whisk.system/cloudant`.

  ```
  wsk package get --summary /whisk.system/cloudant
  ```
  {: pre}
  ```
  package /whisk.system/cloudant: Cloudant database service
     (params: {{site.data.keyword.Bluemix_notm}}ServiceName host username password dbname includeDoc overwrite)
   action /whisk.system/cloudant/read: Read document from database
   action /whisk.system/cloudant/write: Write document to database
   feed   /whisk.system/cloudant/changes: Database change feed
  ```
  {: screen}

  Esta salida muestra que el paquete Cloudant proporciona dos acciones, `read` y `write`, y un
elemento de información de entrada de desencadenante llamado `changes`. El elemento de información de entrada
`changes` provoca que los desencadenantes se activen cuando se añaden documentos a la base de datos Cloudant especificada.

  El paquete Cloudant también define los parámetros `username`, `password`, `host` y `port`. Estos parámetros se deben especificar para acciones e información de entrada para que tenga sentido. Los parámetros permiten
que las acciones funcionen en una cuenta Cloudant específica, por ejemplo.

3. Obtener una descripción de la acción `/whisk.system/cloudant/read`.

  ```
  wsk action get --summary /whisk.system/cloudant/read
  ```
  {: pre}
  ```
  action /whisk.system/cloudant/read: Read document from database
     (params: dbname includeDoc id)
  ```
  {: screen}

  Esta salida muestra que la acción `read` de Cloudant precisa de tres parámetros, incluyendo la base de datos y
el ID de documento a recuperar.


## Invocación de acciones de un paquete
{: #openwhisk_package_invoke}

Puede invocar acciones de un paquete, simplemente como el resto de acciones. Los próximos pasos muestran cómo invocar
la acción `greeting` en el paquete `/whisk.system/samples` con distintos parámetros.

1. Obtener una descripción de la acción `/whisk.system/samples/greeting`.

  ```
  wsk action get --summary /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  action /whisk.system/samples/greeting: Print a friendly greeting
     (params: name place)
  ```
  {: screen}

  Observe que la acción `greeting` acepta dos parámetros: `name` y `place`.

2. Invoque el acción sin ningún parámetro.

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting
  ```
  {: pre}
  ```
  {
      "payload": "Hello, stranger from somewhere!"
  }
  ```
  {: screen}

  La salida es un mensaje genérico porque no se han especificado parámetros.

3. Invoque el acción con parámetros.

  ```
  wsk action invoke --blocking --result /whisk.system/samples/greeting --param name Mork --param place Ork
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Mork from Ork!"
  }
  ```
  {: screen}

  Observe que la salida utiliza los parámetros `name` y `place` que se pasaron a la acción.


## Creación y utilización de enlaces de paquete
{: #openwhisk_package_bind}

Aunque puede utilizar las entidades en un paquete directamente, es posible que acabe pasando siempre los mismos parámetros a la acción. Puede evitarlo enlazando a un paquete y especificando parámetros predeterminados. Esos parámetros se heredan por las acciones del paquete.

Por ejemplo, en el paquete `/whisk.system/cloudant`, puede establecer los valores
`username`, `password` y `dbname` predeterminados en un enlace de paquete, y dichos valores
se pasan automáticamente a cualquier acción del paquete.

En el ejemplo sencillo siguiente, enlaza al paquete `/whisk.system/samples`.

1. Enlazar al paquete `/whisk.system/samples` y establecer un valor de parámetro `place` predeterminado.

  ```
  wsk package bind /whisk.system/samples valhallaSamples --param place Valhalla
  ```
  {: pre}
  ```
  ok: created binding valhallaSamples
  ```
  {: screen}

2. Obtener una descripción del enlace de paquete.

  ```
  wsk package get --summary valhallaSamples
  ```
  {: pre}
  ```
  package /myNamespace/valhallaSamples
   action /myNamespace/valhallaSamples/greeting: Print a friendly greeting
   action /myNamespace/valhallaSamples/wordCount: Count words in a string
   action /myNamespace/valhallaSamples/helloWorld: Print to the console
   action /myNamespace/valhallaSamples/echo: Returns the input arguments, unchanged
  ```
  {: screen}

  Tenga en cuenta que todas las acciones del paquete `/whisk.system/samples` están disponibles en el enlace del
paquete `valhallaSamples`.

3. Invocar una acción en el enlace de paquete.

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Valhalla!"
  }
  ```
  {: screen}

  Observe en el resultado que la acción hereda el parámetro `place` que ha establecido cuando ha
creado el enlace del paquete `valhallaSamples`.

4. Invoque una acción y sobrescriba el valor de parámetro predeterminado.

  ```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin --param place Asgard
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Odin from Asgard!"
  }
  ```
  {: screen}

  Fíjese que el valor del parámetro `place` especificado con la invocación de la acción sobrescribe
el valor predeterminado establecido en el enlace del paquete `valhallaSamples`.


## Creación y uso de información de entrada de desencadenante
{: #openwhisk_package_trigger}

La información de entrada ofrece una forma cómoda de configurar un origen de suceso externo para activar dichos sucesos
para un desencadenante de {{site.data.keyword.openwhisk_short}}. En este ejemplo se muestra cómo utilizar la información de entrada del paquete Alarms para activar un desencadenante cada segundo,
y usar una regla para invocar una acción cada segundo.

1. Obtener una descripción de la información de entrada en el paquete `/whisk.system/alarms`.

  ```
  wsk package get --summary /whisk.system/alarms
  ```
  {: pre}
  ```
  package /whisk.system/alarms
   feed   /whisk.system/alarms/alarm
  ```
  {: screen}

  ```
  wsk action get --summary /whisk.system/alarms/alarm
  ```
  {: pre}
  ```
  action /whisk.system/alarms/alarm: Fire trigger when alarm occurs
     (params: cron trigger_payload)
  ```
  {: screen}

  La información de entrada `/whisk.system/alarms/alarm` acepta dos parámetros:
  - `cron`: una especificación crontab de cuándo activar el desencadenante.
  - `trigger_payload`: el valor de parámetro payload a establecer en cada suceso desencadenante.

2. Crear un desencadenante que se active cada ocho segundos.

  ```
  wsk trigger create everyEightSeconds --feed /whisk.system/alarms/alarm -p cron '*/8 * * * * *' -p trigger_payload '{"name":"Mork", "place":"Ork"}'
  ```
  {: pre}
  ```
  ok: created trigger feed everyEightSeconds
  ```
  {: screen}

3. Crear un archivo 'hello.js' con el código de acción siguiente.

  ```
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

4. Asegúrese de que la acción exista.

  ```
  wsk action update hello hello.js
  ```
  {: pre}

5. Crear una regla que invoque la acción `hello` cada vez que se active el desencadenante
`everyEightSeconds`.

  ```
  wsk rule create --enable myRule everyEightSeconds hello
  ```
  {: pre}
  ```
  ok: created rule myRule
  ok: rule myRule is activating
  ```
  {: screen}

6. Comprobar que la acción se está invocando, sondeando los registros de activación.

  ```
  wsk activation poll
  ```
  {: pre}

  Debería ver activaciones cada ocho segundos para el desencadenante, la regla y la acción. La acción recibe los
parámetros `{"name":"Mork", "place":"Ork"}` en cada invocación.


## Creación de un paquete
{: #openwhisk_packages_create}

Un paquete se utiliza para organizar un conjunto de acciones y elementos de información de entrada relacionados.
También permite la compartición de los parámetros entre todas las entidades del paquete.

Para crear un paquete personalizado con una acción sencilla en él, pruebe el ejemplo siguiente:

1. Cree un paquete llamado "custom".

  ```
  wsk package create custom
  ```
  {: pre}
  ```
  ok: created package custom
  ```
  {: screen}

2. Obtenga un resumen del paquete.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
  ```
  {: screen}

  Fíjese que el paquete está vacío.

3. Cree un archivo llamado `identity.js` que contenga el código de acción siguiente. Esta acción
devuelve todos los parámetros de entrada.

  ```
  function main(args) { return args; }
  ```
  {: codeblock}

4. Crear una acción `identity` en el paquete `custom`.

  ```
  wsk action create custom/identity identity.js
  ```
  {: pre}
  ```
  ok: created action custom/identity
  ```
  {: screen}

  La creación de una acción en un paquete precisa que se añada un nombre de paquete como prefijo del nombre de la acción. No se permite
anidamiento de paquetes. Un paquete solo puede contener acciones y no puede contener otros paquetes.

5. Obtenga otra vez un resumen del paquete.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
   action /myNamespace/custom/identity
  ```
  {: screen}

  Ahora podrá ver la acción `custom/identity` en su espacio de nombres.

6. Invocar la acción en el paquete.

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {}
  ```
  {: screen}


Puede establecer parámetros predeterminados para todas las entidades de un paquete. Esto se hace estableciendo los parámetros a nivel de
paquete, que se heredan para todas las acciones del paquete. Para ver cómo funciona, pruebe el ejemplo siguiente:

1. Actualizar el paquete `custom` con dos parámetros: `city` y `country`.

  ```
  wsk package update custom --param city Austin --param country USA
  ```
  {: pre}
  ```
  ok: updated package custom
  ```
  {: screen}

2. Mostrar los parámetros en el paquete y acción, y ver cómo la acción `identity` del paquete hereda los parámetros del paquete.

  ```
  wsk package get custom parameters
  ```
  {: pre}
  ```
  ok: got package custom, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

  ```
  wsk action get custom/identity parameters
  ```
  {: pre}
  ```
  ok: got action custom/identity, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
  ```
  {: screen}

3. Invocar la acción de identidad sin parámetros para comprobar que la acción realmente hereda los parámetros.

  ```
  wsk action invoke --blocking --result custom/identity
  ```
  {: pre}
  ```
  {
      "city": "Austin",
      "country": "USA"
  }
  ```
  {: screen}

4. Invocar la acción de identidad con algunos parámetros. Los parámetros de invocación se fusionan con los parámetros del paquete; los parámetros de invocación prevalecen sobre los parámetros del paquete.

  ```
  wsk action invoke --blocking --result custom/identity --param city Dallas --param state Texas
  ```
  {: pre}
  ```
  {
      "city": "Dallas",
      "country": "USA",
      "state": "Texas"
  }
  ```
  {: screen}


## Compartición de un paquete
{: #openwhisk_packages_share}

Tras depurar y probar las acciones y la información de entrada que comprende un paquete, éste se puede compartir con todos los usuarios
de {{site.data.keyword.openwhisk_short}}. La compartición del paquete posibilita que los usuarios enlacen al paquete, invoquen acciones
en el mismo y creen reglas de {{site.data.keyword.openwhisk_short}} y acciones de secuencia.

1. Compartir el paquete con todos los usuarios:

  ```
  wsk package update custom --shared
  ```
  {: pre}
  ```
  ok: updated package custom
  ```
  {: screen}

2. Mostrar la propiedad `publish` del paquete para verificar que ahora es true.

  ```
  wsk package get custom publish
  ```
  {: pre}
  ```
  ok: got package custom, projecting publish
  true
  ```
  {: screen}


Ahora otros pueden utilizar su paquete `custom`, incluyendo el enlace al paquete o directamente invocando una
acción sobre él. Otros usuarios deben conocer los nombres completos del paquete para enlazar o invocar acciones sobre él. Las acciones
e información de entrada dentro de un paquete compartido son *públicas*. Si el paquete es privado,
todo su contenido es también privado.

1. Obtener una descripción del paquete para mostrar los nombres completos del paquete y la acción.

  ```
  wsk package get --summary custom
  ```
  {: pre}
  ```
  package /myNamespace/custom
   action /myNamespace/custom/identity
  ```
  {: screen}

  En el ejemplo anterior, se trabaja con el espacio de nombres `myNamespace` y este espacio de nombres aparece en el nombre completo.

