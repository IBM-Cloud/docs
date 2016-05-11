---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Creación de desencadenantes y reglas
{: #openwhisk_triggers}
*Última actualización: 22 de febrero de 2016*

Los desencadenantes y reglas de {{site.data.keyword.openwhisk}} aportan prestaciones dirigidas por sucesos a la plataforma. Los sucesos de orígenes de sucesos externos e internos se ponen en el canal por medio de un desencadenante, y las reglas permiten sus acciones de respuesta para dichos sucesos.
{: shortdesc}

## Desencadenantes

Los desencadenantes son un canal con nombre para una clase de sucesos. A continuación se muestran ejemplos de desencadenantes:
- Un desencadenante de sucesos de actualización de ubicación.
- Un desencadenante de subidas de documento a un sitio web.
- Un desencadenante de correos electrónicos de entrada.

Los desencadenantes se pueden activar (*fired*) mediante un diccionario de pares de clave/valor. Este diccionario se denomina
a veces *event*. Como con las acciones, cada activación de un desencadenante tiene como resultado un ID de activación.

Los desencadenantes se pueden activar de forma explícita mediante un usuario o de parte de un usuario por parte de un origen de suceso externo.
La *información de entrada* es una forma cómoda de configurar un origen de sucesos externo para activar sucesos desencadenantes
que {{site.data.keyword.openwhisk_short}} pueda consumir. Estos son algunos ejemplos de información de entrada:
- Información de entrada de cambio de datos de Cloudant que activa un suceso desencadenante cada vez que se añade o modifica un
documento en una base de datos.
- Una información de entrada Git que desencadena un suceso por cada confirmación contra un repositorio Git.

## Rules

Una regla asocia un desencadenante a una acción, con cada activación del desencadenante que hace que se invoque la acción
correspondiente con un suceso de desencadenante como entrada.

Con el conjunto adecuado de reglas, es posible que un único suceso desencadenante invoque varias acciones, o que
una acción se invoque como respuesta a sucesos de distintos desencadenantes.

Por ejemplo, pensemos en un sistema con las acciones siguientes:
- Acción `classifyImage`, que detecta los objetos de una imagen y los clasifica.
- Acción `thumbnailImage`, que crea una versión de miniatura de una imagen.

Además, supongamos que hay dos orígenes de sucesos que activan los desencadenantes siguientes:
- El desencadenante `newTweet` que se activa cuando se publica un nuevo tweet.
- El desencadenante `imageUpload` que se activa cuando se sube una imagen a un sitio web.

Puede configurar reglas para que un único suceso desencadenante invoque varias acciones, y hacer que varios desencadenantes
invoquen la misma acción:
- Regla `newTweet -> classifyImage`.
- Regla `imageUpload -> classifyImage`.
- Regla `imageUpload -> thumbnailImage`.

Las tres reglas establecen el comportamiento siguiente: las imágenes en ambos tweets y las imágenes subidas se clasifican, las imágenes
subidas se clasifican y se genera una versión de miniatura. 

## Creación y activación de desencadenante
{: #openwhisk_triggers}

Los desencadenantes se pueden activar cuando se producen determinados sucesos, o bien se pueden activar manualmente.

Como ejemplo, cree un desencadenante para enviar actualizaciones de ubicación de usuario y activar manualmente el desencadenante.

1. Especifique el mandato siguiente para crear el desencadenante:
 
  ```
  wsk trigger create locationUpdate
  ```
  {: pre}
 
  ```
  ok: created trigger locationUpdate
  ```
  {: screen}

2. Compruebe que ha creado el desencadenante mostrando una lista del conjunto de desencadenantes.

  ```
  wsk trigger list
  ```
  {: pre}
 
  ```
  triggers
  /someNamespace/locationUpdate                            private
  ```
  {: screen}

  Hasta ahora ha creado un "canal" con nombre, para el que se pueden activar sucesos.

3. A continuación, active el suceso desencadenante especificando el nombre de desencadenante y los parámetros:

  ```
  wsk trigger fire locationUpdate --param name "Donald" --param place "Washington, D.C."
  ```
  {: pre}

  ```
  ok: triggered locationUpdate with id fa495d1223a2408b999c3e0ca73b2677
  ```
  {: screen}

   Los sucesos que active para el desencadenante statusUpdate actualmente no hacen nada. Para ser útil, el
desencadenante necesita una regla que la asocie con una acción.


## Uso de reglas para asociar desencadenantes y acciones
{: #openwhisk_rules}

Las reglas se utilizan para asociar un desencadenante con una acción. Cada vez que se activa un suceso desencadenante, la acción
se invoca con parámetros de suceso.

Como ejemplo, cree una regla que invoque la acción hello siempre que se publique una actualización de ubicación. 

1. Cree el archivo 'hello.js' con el código de acción que usaremos:
  ```
  function main(params) {
     return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

2. Asegúrese de que la acción de desencadenante exista.
  ```
  wsk trigger update locationUpdate
  ```
  {: pre}
  
  ```
  wsk action update hello hello.js
  ```
  {: pre}

3. Cree y habilite la regla. Los tres parámetros son el nombre de la regla, el desencadenante y la acción.
  ```
  wsk rule create --enable myRule locationUpdate hello
  ```
  {: pre}

4. Activar el desencadenante locationUpdate. Cada vez que activa un suceso, la acción hello se invoca con los parámetros de suceso.
  ```
  wsk trigger fire locationUpdate --param name "Donald" --param place "Washington, D.C."
  ```
  {: pre}
  
  ```
  ok: triggered locationUpdate with id d5583d8e2d754b518a9fe6914e6ffb1e
  ```
  {: screen}

5. Compruebe que la acción se ha invocado, revisando la activación más reciente.
  ```
  wsk activation list --limit 1 hello
  ```
  {: pre}
  
  ```
  activations
  9c98a083b924426d8b26b5f41c5ebc0d             hello
  ```
  {: screen}
  
  ```
  wsk activation result 9c98a083b924426d8b26b5f41c5ebc0d
  ```
  {: pre}
  ```
  {
     "payload": "Hello, Donald from Washington, D.C."
  }
  ```
  {: screen}

  Verá que la acción hello ha recibido la carga del suceso y ha devuelto la serie prevista.

  Puede crear varias reglas que se asocien con el mismo desencadenante con distintas acciones.
