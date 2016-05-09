---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Creación e invocación de acciones de {{site.data.keyword.openwhisk_short}}
{: #openwhisk_actions}

*Última actualización: 22 de marzo de 2016*

Las acciones son fragmentos de código sin estado que se ejecutan en la plataforma {{site.data.keyword.openwhisk}}. Una
acción puede ser una función JavaScript, una función Swift o un programa ejecutable personalizado
empaquetado en un contenedor Docker. Por ejemplo, una acción se puede utilizar para detectar las caras de una imagen, agregar un
conjunto de llamadas de API o publicar un Tweet.
{:shortdesc}

Las acciones se pueden invocar explícitamente, o ejecutarse como respuesta a un suceso. En cualquier caso, la ejecución de una
acción tiene como resultado un registro de activación que se identifica mediante un ID de activación exclusivo. La entrada a una
acción y el resultado de la acción son un diccionario de pares de clave/valor, en el que la clave es una serie y
el valor es un valor JSON válido.

Las acciones se pueden componer de llamadas a otras acciones, o de una secuencia definida de acciones.

## Creación e invocación de acciones de JavaScript
{: #openwhisk_create_action_js}

Las secciones siguientes le guían en la forma de trabajar con acciones en JavaScript. Empezando por la creación e invocación de una acción
sencilla, pasaremos a añadir parámetros a una acción e invocarla con parámetros, establecer parámetros predeterminados e invocarlos, crear acciones asíncronas y, finalmente, trabajar con secuencia de acciones.


### Creación e invocación de una acción JavaScript sencilla
{: #openwhisk_single_action_js}

Revise los pasos y ejemplos siguientes para crear su primera acción JavaScript.

1. Cree un archivo JavaScript con el contenido siguiente. Para este ejemplo, el nombre de archivo es 'hello.js'.
  
  ```
  function main() {
      return {payload: 'Hello world'};
  }
  ```
  {: codeblock}

  El archivo JavaScript podría tener funciones adicionales. No obstante, por convenio, debe existir una función
llamada `main` para proporcionar un punto de entrada para la acción.

2. Crear una acción desde la función JavaScript siguiente. Para este ejemplo, la acción se llama 'hello'.

  ```
  wsk action create hello hello.js
  ```
  {: pre}
  ```
  ok: created action hello
  ```
  {: screen}

3. Listar las acciones que ha creado:
  
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  hello       private
  ```
  {: screen}

  Puede ver la acción `hello` que acaba de crear.

4. Tras crear su acción, puede ejecutarla en la nube en {{site.data.keyword.openwhisk_short}} con el mandato 'invoke'. Puede
invocar acciones con una invocación *blocking* o *non-blocking*, especificando un distintivo en el mandato. Una invocación
de bloqueo (blocking) espera hasta que la acción se ejecute completamente, y devuelve un resultado. En este ejemplo se utiliza
el parámetro de bloqueo, `-blocking`:

  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
  response:
  {
      "result": {
          "payload": "Hello world"
      },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

  La salida del mandato son dos elementos de información importantes:
  * El ID de activación (`44794bd6aab74415b4e42a308d880e5b`)
  * El resultado de la invocación

  El resultado en este caso es la serie `Hello world` devuelta por la función JavaScript. El ID de activación se puede
utilizar para recuperar los registros o el resultado de la invocación a posteriori.  

5. Si no necesita el resultado de la acción inmediatamente, puede omitir el distintivo `--blocking`
para hacer una invocación sin bloqueo. Puede obtener el resultado posteriormente, usando el ID de activación. Observe el ejemplo siguiente:

  ```
  wsk action invoke hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: screen}

  ```
  wsk activation result 6bf1f670ee614a7eb5af3c9fde813043
  ```
  {: pre}
  ```
  {
      "payload": "Hello world"
  }
  ```
  {: screen}

6. Si olvida registrar el ID de activación, puede obtener una lista de activaciones ordenadas de la más reciente a la más antigua. Ejecute el mandato siguiente para obtener una lista de sus activaciones:

  ```
  wsk activation list
  ```
  {: pre}
  ```
  activations
  44794bd6aab74415b4e42a308d880e5b         hello
  6bf1f670ee614a7eb5af3c9fde813043         hello
  ```
  {: screen}

### Paso de parámetros a una acción
{: #openwhisk_adding_parameters_js}

Los parámetros se pueden pasar a la acción cuando se invoca.

1. Usar parámetros en la acción. Por ejemplo, actualizar el archivo 'hello.js' con el contenido siguiente:
  
  ```
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

  Los parámetros de entrada se pasan como un parámetro de objeto JSON a la función `main`. Fíjese
cómo los parámetros `name` y `place` se recuperan del objeto `params` en este ejemplo.

2. Actualizar la acción `hello` e invocar la acción, mientras se pasan los valores de los parámetros `name` y `place`. Observe el ejemplo siguiente:
  
  ```
  wsk action update hello hello.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Vermont'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  Fíjese en el uso de la opción `--param` para especificar un nombre y valor, y la opción
`--result` para mostrar solo el resultado de la invocación.

### Configuración de los parámetros predeterminados
{: #openwhisk_binding_actions}

Las acciones se pueden invocar con varios parámetros con nombre. Recuerde que la acción `hello`
del ejemplo anterior espera dos parámetros: *name* (nombre) de una persona y *place* (lugar) del que es.

En lugar de pasar todos los parámetros a una acción cada vez, puede enlazar determinados parámetros. El ejemplo siguiente enlaza
el parámetro *place* para que el valor predeterminado de la acción sea el lugar (place) "Vermont":
 
1. Actualizar la acción usando la opción `--param` para enlazar valores de parámetros.

  ```
  wsk action update hello --param place 'Vermont'
  ```
  {: pre}

2. Invocar la acción, pasando solo el parámetro `name` esta vez.

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie'
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  Tenga en cuenta no necesitaba especificar el parámetro place al invocar la acción. Los parámetros enlazados aún se pueden
sobrescribir especificando el valor de parámetro en el momento de la invocación.

3. Invoca la acción, pasando los valores `name` y `place`. El segundo sobrescribe el
valor enlazado a la acción.

  ```
  wsk action invoke --blocking --result hello --param name 'Bernie' --param place 'Washington, DC'
  ```
  {: pre}
  ```
  {  
      "payload": "Hello, Bernie from Washington, DC"
  }
  ```
  {: screen}

### Creación de acciones asíncronas
{: #openwhisk_asynchrony_js}

Las funciones de JavaScript que continúan su ejecución en una función de devolución de llamada podrían necesitar devolver el resultado
de la activación tras el retorno de la función `main`. Puede lograrlo usando las funciones `whisk.async()` y
`whisk.done()` en su acción.

1. Guardar el contenido siguiente en un archivo llamado `asyncAction.js`.

  ```
  function main() {
      setTimeout(function() {
          return whisk.done({done: true});
      }, 20000);
      return whisk.async();
  }
  ```
  {: codeblock}

  Observe que la función `main` retorna inmediatamente, y el valor de retorno `whisk.async()`
indica que la activación debería continuar la ejecución.

  La función `setTimeout()` de JavaScript en este caso espera 20 segundos antes de invocar la función de devolución de llamada,
en la que la llamada a `whisk.done()` indica que la activación está completada.

2. Ejecute los mandatos siguientes para crear la acción e invocarla:

  ```
  wsk action create asyncAction asyncAction.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result asyncAction
  ```
  {: pre}
  ```
  {
      "done": true
  }
  ```
  {: screen}

  Tenga en cuenta que ha realizado una invocación de bloqueo de una acción asíncrona.

3. Recupere el registro de activación para ver cuánto tiempo ha tardado la activación en completarse:

  ```
  wsk activation list --limit 1 asyncAction
  ```
  {: pre}
  ```
  activations
  b066ca51e68c4d3382df2d8033265db0             asyncAction
  ```
  {: screen}


  ```
  wsk activation get b066ca51e68c4d3382df2d8033265db0
  ```
  {: pre}
 ```
  {
      "start": 1455881628103,
      "end":   1455881648126,
      ...
  }
  ```
  {: screen}

  Si se comparan los registros de fecha y hora de `start` y `end` en el registro de activación,
puede ver que esta activación ha tardado poco más de 20 segundos en completarse.


### Uso de acciones para invocar una API externa
{: #openwhisk_apicall_action}

Los ejemplos hasta ahora han sido funciones JavaScript autocontenidas. También puede crear una acción que invoque una API externa.

En este ejemplo se invoca a un servicio Yahoo Weather para obtener la meteorología actual de una ubicación específica. 

1. Guardar el contenido siguiente en un archivo llamado `weather.js`.
  ```
    var request = require('request');
    
    function main(msg) {
        var location = msg.location || 'Vermont';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';
    
        request.get(url, function(error, response, body) {
            var condition = JSON.parse(body).query.results.channel.item.condition;
            var text = condition.text;
            var temperature = condition.temp;
            var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
            whisk.done({msg: output});
        });
    
        return whisk.async();
    }
  ```
  {: codeblock}

  Tenga en cuenta que la acción en este ejemplo utiliza la biblioteca `request` de JavaScript para
realizar una solicitud HTTP a la API Yahoo Weather, y extra campos del resultado JSON. Las
[Referencias](./openwhisk_reference.html#runtime_ref_runtime_environment) detallan los paquetes Node.js que
puede utilizar en sus acciones.
  
  En este ejemplo también se muestra la necesidad de acciones asíncronas. La acción devuelve `whisk.async()` para
indicar que el resultado de esta acción no está aún disponible cuando la función retorna. En su lugar, el
resultado está disponible en la devolución de llamada `request` tras completarse la llamada HTTP, y la pasa como
argumento a la función `whisk.done()`.

2. Ejecute los mandatos siguientes para crear la acción e invocarla:
  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location 'Brooklyn, NY'
  ```
  {: pre}
  ```
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```
  {: screen}

### Creación de secuencias de acciones
{: #openwhisk_create_action_sequence}

Puede crear una acción que encadene juntas una secuencia de acciones.

Se proporcionan varias acciones de utilidad en un paquete llamado `/whisk.system/util` que puede utilizar para crear su
primera secuencia. Puede obtener más información sobre los paquetes en la sección [Paquetes](./openwhisk_packages.html).

1. Mostrar las acciones del paquete `/whisk.system/util`.
  
  ```
  wsk package get --summary /whisk.system/util
  ```
  {: pre}
  ```
  package /whisk.system/util
   action /whisk.system/util/cat: Concatenar matrices de series, y dividir líneas en una matriz
   action /whisk.system/util/head: Filtrar los K primeros elementos de matriz y descartar el resto
   action /whisk.system/util/date: Obtener la fecha y hora actual
   action /whisk.system/util/sort: Ordenar matriz
  ```
  {: screen}

  Usaremos las acciones `cat` y `sort` en este ejemplo.

2. Crear una secuencia de acciones para que el resultado de una acción se pase como argumento a la acción siguiente.
  
  ```
  wsk action create myAction --sequence /whisk.system/util/cat,/whisk.system/util/sort
  ```
  {: pre}

  Esta secuencia de acciones convierte algunas líneas de texto en una matriz, y ordena las líneas.

3. Antes de invocar la secuencia de acciones, cree un archivo de texto llamado 'haiku.txt' con algunas líneas de texto:

  ```
  Over-ripe sushi,
  The Master
  Is full of regret.
  ```
  {: codeblock}

4. Invoque la acción:
  
  ```
  wsk action invoke --blocking --result myAction --param payload "$(cat haiku.txt)"
  ```
  {: pre}
  ```
  {
      "length": 3,
      "lines": [
          "Is full of regret.",
          "Over-ripe sushi,",
          "The Master"
      ]
  }
  ```
  {: screen}

  En el resultado, puede ver que las líneas se ordenan.

**Nota**: Para obtener más información sobre la invocación de secuencias de acciones con varios parámetros con nombre,
consulte [Establecimiento de parámetros predeterminados](./openwhisk_actions.html##openwhisk_binding_actions)

## Creación de acciones Swift
{: #openwhisk_actions_swift}

El proceso de creación de acciones Swift es parecido a de las acciones JavaScript. En las secciones siguientes se proporcionar una guía
para la creación e invocación de una única acción Swift, y se añaden parámetros a dicha acción.

También puede usar el recinto de pruebas [Swift Sandbox](https://swiftlang.ng.bluemix.net) en línea para probar
el código Swift sin tener que instalar Xcode en su máquina.

### Creación e invocación de una acción
{: #openwhisk_actions_invoke_swift}

Una acción es sencillamente una función Swift de nivel superior. Por ejemplo, cree un archivo llamado
`hello.swift` con el contenido siguiente:

```
  func main(args: [String:Any]) -> [String:Any] {
      if let name = args["name"] as? String {
          return [ "greeting" : "Hello \(name)!" ]
      } else {
          return [ "greeting" : "Hello stranger!" ]
      }
  }
```
{: codeblock}

Tenga en cuenta que al igual que las acciones JavaScript, las acciones Swift siempre consumen un
diccionario y generan un diccionario.

Puede crear una acción de {{site.data.keyword.openwhisk_short}} llamada `helloSwift` desde esta función, según se indica a continuación:

```
wsk action create helloSwift hello.swift
```
{: pre}

Cuando se utiliza la línea de mandatos y un archivo de origen `.swift`, no es necesario especificar que
está creando una acción Swift (al contrario de lo que sucede con una acción JavaScript); la herramienta lo determina
a partir de la extensión de archivo.

La invocación de la acción es la misma para acciones Swift que para acciones JavaScript:

```
wsk action invoke --blocking --result helloSwift --param name World
```
{: pre}

```
  {
      "greeting": "Hello World!"
  }
```
{: screen}

**Atención:** Acciones Swift se ejecutan en un entorno Linux. Swift en Linux aún está en desarrollo, y
{{site.data.keyword.openwhisk_short}} suele utilizar el release disponible más reciente, que no es necesariamente estable. Además, la versión
de Swift que se utiliza con {{site.data.keyword.openwhisk_short}} podría no ser coherente con versiones de Swift de releases estables
de XCode en MacOS.

## Creación de acciones Docker
{: #openwhisk_actions_docker}

Con acciones Docker de {{site.data.keyword.openwhisk_short}}, puede escribir sus acciones en cualquier lenguaje.

Su código se compila en un binario ejecutable y se incluye en una imagen Docker. El programa binario interactúa con el sistema
aceptando la entrada desde `stdin` y respondiendo por medio de `stdout`.

Como requisito previo, debe tener una cuenta de Docker Hub.  Para configurar un ID y cuenta gratuitos de Docker, acceda a
[Docker Hub](https://hub.docker.com){: new_window}.

Para las instrucciones siguientes, supondremos que el ID de usuario es "janesmith" y la contraseña es "janes_password".  Suponiendo que
la CLI ya se ha configurado, son necesarios tres pasos para configurar un binario personalizado para que lo use
{{site.data.keyword.openwhisk_short}}.  Tras hacerlo, la imagen de Docker subida se podrá utilizar como una acción.

1. Descargar el esqueleto de Docker. Puede descargarlo usando la CLI de la siguiente manera:

  ```
  wsk sdk install docker
  ```
  {: pre}
  ```
  El esqueleto Docker estará ahora instalado en el directorio actual.
  ```
  {: screen}

  ```
  ls dockerSkeleton/
  ```
  {: pre}
  ```
  Dockerfile      README.md       buildAndPush.sh client          server
  ```
  {: screen}

  El esqueleto es una plantilla de contenedor de Docker en la que puede inyectar código en forma de binarios personalizados.

2. Configure su binario personalizado en el esqueleto blackbox. El esqueleto ya incluye un programa en C que puede usar.

  ```
  cat ./dockerSkeleton/client/example.c
  ```
  {: pre}
  {: pre}
  ```
  #include <stdio.h>
  
  int main(int argc, char *argv[]) {
      printf("Hello %s from arbitrary C program!\n",
             (argc == 1) ? "anonymous" : argv[1]);
  }
  ```
  {: screen}

  Puede modificar este valor cuando sea necesario.

3. Construya la imagen de Docker y súbala mediante un script proporcionado. Antes debe ejecutar `docker login` para
la autenticación y, a continuación, ejecute el script con el nombre de imagen elegido.

  ```
  docker login -u janesmith -p janes_password
  ```
  {: pre}
  ```
  cd dockerSkeleton
  ```
  {: pre}
  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}

  Tenga en cuenta que parte del archivo example.c está compilado como parte del proceso de compilación de imagen de Docker,
por lo que no necesita C compilado en su máquina.

4. Para crear una acción a partir de una imagen de Docker en lugar de un archivo JavaScript proporcionado, añada
`--docker` y sustituya el nombre del archivo JavaScript por el nombre de la imagen de Docker.

  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```
  {
      "msg": "Hello Rey from arbitrary C program!\n"
  }
  ```
  {: screen}


Podrá obtener más información sobre la creación de acciones de Docker en la sección
[Referencias](./openwhisk_reference.html#openwhisk_ref_docker).


## Supervisión de salida de acción
{: #openwhisk_actions_polling}

Las acciones de {{site.data.keyword.openwhisk_short}} se podrían invocar por otros usuarios, en respuesta a varios sucesos,
o como parte de una secuencia de acciones. En tales casos, puede ser útil supervisar las invocaciones.

Puede utilizar la CLI de {{site.data.keyword.openwhisk_short}} para ver el resultado de la salida de las acciones a medida que se invocan.

1. Emita el siguiente mandato desde un shell:
  ```
  wsk activation poll
  ```
  {: pre}

  Este mandato inicia un bucle de sondeo que comprueba continuamente los registros de las activaciones.

2. Cambie a otra ventana e invoque la acción:

  ```
  wsk action invoke /whisk.system/samples/helloWorld --param payload Bob
  ```
  {: pre}
  ```
  ok: invoked /whisk.system/samples/helloWorld with id 7331f9b9e2044d85afd219b12c0f1491
  ```
  {: screen}

3. Observe el registro de activación en la ventana de sondeo:

  ```
  Activation: helloWorld (7331f9b9e2044d85afd219b12c0f1491)
    2016-02-11T16:46:56.842065025Z stdout: hello bob!
  ```
  {: screen}

  De la misma forma, cuando ejecute el programa de utilidad de sondeo, verá en tiempo real los registros de las acciones que
ejecute de su parte, en {{site.data.keyword.openwhisk_short}}.

## Supresión de acciones
{: #openwhisk_delete_action}

Puede realizar una limpieza mediante la supresión de acciones que no quiera usar.

1. Ejecute el mandato siguiente para suprimir una acción:
  ```
  wsk action delete hello
  ```
  {: pre}
  ```
  ok: deleted hello
  ```
  {: screen}

2. Compruebe que la acción ya no aparece en la lista de acciones.
  ```
  wsk action list
  ```
  {: pre}
  ```
  actions
  ```
  {: screen}
