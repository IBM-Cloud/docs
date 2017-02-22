---

 

copyright:

  years: 2016, 2017
lastupdated: "2017-01-04"


---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Creación e invocación de acciones de {{site.data.keyword.openwhisk_short}}
{: #openwhisk_actions}


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

Las secciones siguientes le guían en la forma de trabajar con acciones en JavaScript. Comience con la creación e invocación de una acción simple. A continuación, continúe con la adición de parámetros a una acción y la invocación de la acción con parámetros. Después, establezca parámetros predeterminados e invóquelos. A continuación, cree acciones asíncronas y, finalmente, trabaje con secuencias de acciones.


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

3. Mostrar una lista de las acciones que ha creado:
  
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

4. Tras crear su acción, puede ejecutarla en la nube en OpenWhisk con el mandato 'invoke'. Puede
invocar acciones con una invocación *blocking* (es decir, estilo solicitud/respuesta) o *non-blocking*, especificando un distintivo en el mandato. Una solicitud de invocación de bloqueo *esperará* a que el resultado de la activación esté disponible. El período de espera es inferior a 60 segundos o el [límite de tiempo](./openwhisk_reference.html#openwhisk_syslimits_timeout) configurado en la acción. El resultado de la activación se devuelve si está disponible en el período de espera. De no ser así, la activación se sigue procesando en el sistema y se devuelve un ID de activación para poder buscar el resultado más tarde, como en las solicitudes que no son de bloqueo (consulte [aquí](#watching-action-output) para ver consejos sobre la supervisión de activaciones).

  Este ejemplo utiliza el parámetro blocking, `--blocking`:

  ```
  wsk action invoke --blocking hello
  ```
  {: pre}
  ```
  ok: invoked hello with id 44794bd6aab74415b4e42a308d880e5b
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
  * El resultado de la invocación si está disponible en el período de espera previsto.

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

3.  Los parámetros se puede proporcionar explícitamente en la línea de mandatos o por medio de un archivo que contenga los parámetros que se quiere especificar

  Para pasar los parámetros directamente a través de la línea de mandatos, especifique un par clave/valor para el distintivo `--param`:
  ```
  wsk action invoke --blocking --result hello --param name Bernie --param place Vermont
  ```
  {: pre}

  Para poder utilizar un archivo que contenga parámetros, crear un archivo que contenga los parámetros en formato JSON. Luego se debe pasar el nombre del archivo al distintivo `param-file`:

  Archivo de parámetros de ejemplo denominado parameters.json:
  ```
  {
      "name": "Bernie",
      "place": "Vermont"
  }
  ```
  {: codeblock}

  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
  ```
  {: pre}

  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  Fíjese en el uso de la opción
`--result` para mostrar solo el resultado de la invocación.

### Configuración de los parámetros predeterminados
{: #openwhisk_binding_actions}

Las acciones se pueden invocar con varios parámetros con nombre. Recuerde que la acción `hello`
del ejemplo anterior espera dos parámetros: *name* (nombre) de una persona y *place* (lugar) del que es.

En lugar de pasar todos los parámetros a una acción cada vez, puede enlazar determinados parámetros. El ejemplo siguiente enlaza
el parámetro *place* para que el valor predeterminado de la acción sea el lugar (place) "Vermont":
 
1. Actualizar la acción usando la opción `--param` para enlazar valores de parámetros o pasando un archivo que contiene los parámetros a `--param-file`

  Para especificar parámetros predeterminados explícitamente en la línea de mandatos, especifique un par clave/valor para el distintivo `param`:

  ```
  wsk action update hello --param place Vermont
  ```
  {: pre}

  Para pasar parámetros desde un archivo hay que crear un archivo con el contenido deseado en formato JSON.
  Luego se debe pasar el nombre del archivo al distintivo `-param-file`:

  Archivo de parámetros de ejemplo denominado parameters.json:
  ```
  {
      "place": "Vermont"
  }
  ```
  {: codeblock}

  ```
  wsk action update hello --param-file parameters.json
  ```
  {: pre}

2. Invocar la acción, pasando solo el parámetro `name` esta vez.

  ```
  wsk action invoke --blocking --result hello --param name Bernie
  ```
  {: pre}
  ```
  {
      "payload": "Hello, Bernie from Vermont"
  }
  ```
  {: screen}

  Observe que no ha necesitado especificar el parámetro place al invocar la acción. Los parámetros enlazados aún se pueden
sobrescribir especificando el valor de parámetro en el momento de la invocación.

3. Invocar la acción, pasando los valores `name` y `place`. El segundo sobrescribe el
valor enlazado a la acción.

  Utilización del distintivo `--param`:

  ```
  wsk action invoke --blocking --result hello --param name Bernie --param place "Washington, DC"
  ```
  {: pre}

  Utilización del distintivo `--param-file`:

  Archivo parameters.json:
  ```
  {
    "name": "Bernie",
      "place": "Vermont"
  }
  ```
  {: codeblock}


  ```
  wsk action invoke --blocking --result hello --param-file parameters.json
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

Las funciones de JavaScript que se ejecutan de forma asíncrona podrían necesitar devolver el resultado de la activación tras el retorno de la función `main`. Puede realizar esto devolviendo un Promise en la acción.

1. Guardar el contenido siguiente en un archivo llamado `asyncAction.js`.

  ```
  function main(args) {
       return new Promise(function(resolve, reject) {
         setTimeout(function() {
           resolve({ done: true });
         }, 2000);
      })
   }
  ```
  {: codeblock}

  Observe que la función `main` devuelve un Promise, que indica que la activación aún no se ha completado, pero que se espera que lo haga en el futuro.

  La función `setTimeout()` de JavaScript en este caso espera dos segundos antes de invocar la función de devolución de llamada.  Esto representa el código asíncrono y va dentro de la función de devolución de llamada del Promise.

  La devolución de llamada del Promise tiene dos argumentos, resolve y reject, ambos son funciones.  La llamada a `resolve()` rellena el Promise e indica que la activación se ha completado con normalidad.

  Una llamada a `reject()` se puede utilizar para rechazar el Promise e indicar que la activación se ha completado de forma anómala.

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
puede ver que esta activación ha tardado poco más de 2 segundos en completarse.


### Uso de acciones para invocar una API externa
{: #openwhisk_apicall_action}

Los ejemplos hasta ahora han sido funciones JavaScript autocontenidas. También puede crear una acción que invoque una API externa.

En este ejemplo se invoca a un servicio Yahoo Weather para obtener la meteorología actual de una ubicación específica. 

1. Guardar el contenido siguiente en un archivo llamado `weather.js`.
  
  ```
  var request = require('request');
  
  function main(params) {
      var location = params.location || 'Vermont';
        var url = 'https://query.yahooapis.com/v1/public/yql?q=select item.condition from weather.forecast where woeid in (select woeid from geo.places(1) where text="' + location + '")&format=json';
  
      return new Promise(function(resolve, reject) {
          request.get(url, function(error, response, body) {
              if (error) {
                  reject(error);
                }
                else {
                  var condition = JSON.parse(body).query.results.channel.item.condition;
                    var text = condition.text;
                    var temperature = condition.temp;
                    var output = 'It is ' + temperature + ' degrees in ' + location + ' and ' + text;
                    resolve({msg: output});
                }
          });
      });
  }
  ```
  {: codeblock}
  
  Tenga en cuenta que la acción en este ejemplo utiliza la biblioteca `request` de JavaScript para
realizar una solicitud HTTP a la API Yahoo Weather, y extra campos del resultado JSON. Las
[Referencias](./openwhisk_reference.html#openwhisk_ref_javascript_environments) detallan los paquetes Node.js que
puede utilizar en sus acciones.
  
  En este ejemplo también se muestra la necesidad de acciones asíncronas. La acción devuelve un Promise para
indicar que el resultado de esta acción no está aún disponible cuando la función retorna. En su lugar, el
resultado está disponible en la devolución de llamada `request` tras completarse la llamada HTTP, y la pasa como
argumento a la función `resolve()`.
  
2. Ejecute los mandatos siguientes para crear la acción e invocarla:
  
  ```
  wsk action create weather weather.js
  ```
  {: pre}
  ```
  wsk action invoke --blocking --result weather --param location "Brooklyn, NY"
  ```
  {: pre}
  ```
  {
      "msg": "It is 28 degrees in Brooklyn, NY and Cloudy"
  }
  ```
  {: screen}

### Empaquetado de una acción como un módulo Node.js
{: #openwhisk_js_packaged_action}

Como alternativa a grabar todo el código de acción en un único archivo de origen JavaScript, puede grabar una acción como un paquete `npm`. Piense como ejemplo un directorio con los archivos siguientes:

En primer lugar, `package.json`:

```
{
  "name": "my-action",
  "version": "1.0.0",
  "main": "index.js",
  "dependencies" : {
    "left-pad" : "1.1.3"
  }
}
```
{: codeblock}

A continuación, `index.js`:

```
function myAction(args) {
    const leftPad = require("left-pad")
    const lines = args.lines || [];
    return { padded: lines.map(l => leftPad(l, 30, ".")) }
}

exports.main = myAction;
```
{: codeblock}

Tenga en cuenta que la acción se expone a través de `exports.main`; el manejador de acciones en sí puede tener cualquier nombre, siempre que cumpla con la firma habitual de aceptar un objeto y devolverlo (o una `Promesa` de un objeto).

Para crear una acción OpenWhisk desde este paquete:

1. Instale en primer lugar todas las dependencias localmente

  ```
  npm install
  ```
  {: pre}

2. Cree un archivo `.zip` que contenga todos los archivos (incluidas todas las dependencias):

  ```
  zip -r action.zip *
  ```
  {: pre}

3. Cree la acción:

  ```
  wsk action create packageAction --kind nodejs:6 action.zip
  ```
  {: pre}

  Tenga en cuenta que al crear una acción desde un archivo `.zip` utilizando la herramienta CLI, debe proporcionar explícitamente un valor para el distintivo `--kind`.

4. Puede invocar la acción como cualquier otra:

  ```
  wsk action invoke --blocking --result packageAction --param lines "[\"and now\", \"for something completely\", \"different\" ]"
  ```
  {: pre}
  ```
  {
      "padded": [
          ".......................and now",
          "......for something completely",
          ".....................different"
      ]
  }
  ```
  {: screen}

Finalmente, tenga en cuenta que mientras que la mayoría de los paquetes de `npm` instalan orígenes JavaScript en `npm install`, algunos también instalan y compilan artefactos binarios. La carga del archivo de archivado no da soporte en este momento a las dependencias binarias, sino únicamente a las dependencias de JavaScript. Las invocaciones de acción pueden fallar si el archivo incluye dependencias binarias.

## Creación de secuencias de acciones
{: #openwhisk_create_action_sequence}

Puede crear una acción que encadene juntas una secuencia de acciones.

Se proporcionan varias acciones de utilidad en un paquete llamado `/whisk.system/utils` que puede utilizar para crear su
primera secuencia. Puede obtener más información sobre los paquetes en la sección [Paquetes](./openwhisk_packages.html).

1. Mostrar las acciones del paquete `/whisk.system/utils`.
  
  ```
  wsk package get --summary /whisk.system/utils
  ```
  {: pre}
  ```
  package /whisk.system/utils: Building blocks that format and assemble data
   action /whisk.system/utils/head: Extract prefix of an array
   action /whisk.system/utils/split: Split a string into an array
   action /whisk.system/utils/sort: Sorts an array
   action /whisk.system/utils/echo: Returns the input
   action /whisk.system/utils/date: Current date and time
   action /whisk.system/utils/cat: Concatenates input into a string
  ```
  {: screen}
  
  En este ejemplo utilizará las acciones `split` y `sort`.
  
2. Crear una secuencia de acciones para que el resultado de una acción se pase como argumento a la acción siguiente.
  
  ```
  wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort
  ```
  {: pre}
  
  Esta secuencia de acciones convierte algunas líneas de texto en una matriz, y ordena las líneas.
  
3. Invoque la acción:
  
  ```
  wsk action invoke --blocking --result sequenceAction --param payload "Over-ripe sushi,\nThe Master\nIs full of regret."
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

**Nota**: los parámetros que se pasan entre acciones de la secuencia son explícitos, salvo los predeterminados.
Por tanto, los parámetros que se pasan a la secuencia de acción solo están disponibles para la primera acción de la secuencia.
El resultado de la primera acción de la secuencia se convierte en el objeto JSON de entrada de la segunda acción de la secuencia (y así sucesivamente).
Este objeto no incluye ninguno de los parámetros pasados a la secuencia originalmente, a menos que la primera acción los incluya explícitamente en el resultado.
Los parámetros de entrada a una acción se fusionan con los parámetros predeterminados de la acción, dando prioridad a los primeros y sustituyendo los parámetros predeterminados coincidentes.
Para obtener más información sobre la invocación de secuencias de acciones con varios parámetros con nombre, consulte [Establecimiento de parámetros predeterminados](./openwhisk_actions.html#openwhisk_binding_actions).

## Creación de acciones Python
{: #openwhisk_actions_python}

El proceso de creación de acciones Python es parecido al de las acciones JavaScript. En las secciones siguientes se proporciona una guía para la creación e invocación de una única acción Python, y se añaden parámetros a dicha acción.

### Creación e invocación de una acción
{: #openwhisk_actions_python_invoke}

Una acción es simplemente una función Python de nivel superior, que implica que es necesario disponer de un método denominado
`main`. Por ejemplo, cree un archivo denominado `hello.py` con el contenido siguiente:

```
def main(dict):
        name = dict.get("name", "stranger")
        greeting = "Hello " + name + "!"
    print(greeting)
        return {"greeting": greeting}
```
{: codeblock}

Las acciones Python siempre consumen un
diccionario y generan un diccionario.

Puede crear una acción OpenWhisk denominada `helloPython` a partir de esta función de la siguiente manera:

```
wsk action create helloPython hello.py
```
{: pre}

Cuando se utiliza la línea de mandatos y un archivo de origen `.py`, no es necesario especificar que
está creando una acción Python (al contrario de lo que sucede con una acción JavaScript); la herramienta lo determina
a partir de la extensión de archivo.

La invocación de la acción es la misma para acciones Python que para acciones JavaScript:

```
wsk action invoke --blocking --result helloPython --param name World
```
{: pre}

```
  {
      "greeting": "Hello World!"
  }
```
{: screen}


## Creación de acciones Swift
{: #openwhisk_actions_swift}

El proceso de creación de acciones Swift es parecido al de las acciones JavaScript. En las secciones siguientes se proporciona una guía para la creación e invocación de una única acción Swift, y se añaden parámetros a dicha acción.

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

Las acciones Swift siempre consumen un
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

## Creación de acciones de Java
{: #openwhisk_actions_java}

El proceso de creación de acciones Java es parecido al de las acciones JavaScript y Swift. En las secciones siguientes se proporciona una guía para la creación e invocación de una única acción Swift, y se añaden parámetros a dicha acción.

Para compilar, probar y archivar archivos Java, debe tener un [JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) instalado localmente.

### Creación e invocación de una acción
{: #openwhisk_actions_java_invoke}

Una acción Java es un programa Java con un método llamado `main` que tiene la firma exacta que se indica a continuación:
```
public static com.google.gson.JsonObject main(com.google.gson.JsonObject);
```
{: codeblock}

Por ejemplo, cree un archivo Java denominado `Hello.java` con el contenido siguiente:

```
import com.google.gson.JsonObject;
public class Hello {
    public static JsonObject main(JsonObject args) {
        String name = "stranger";
        if (args.has("name"))
            name = args.getAsJsonPrimitive("name").getAsString();
        JsonObject response = new JsonObject();
        response.addProperty("greeting", "Hello " + name + "!");
        return response;
    }
}
```
{: codeblock}

A continuación, compile `Hello.java` en un archivo JAR `hello.jar` tal como se indica a continuación:
```
javac Hello.java
jar cvf hello.jar Hello.class
```
{: pre}

**Nota:** [google-gson](https://github.com/google/gson) debe existir en CLASSPATH de Java cuando compile el archivo Java.

Puede crear una acción OpenWhisk denominada `helloJava` a partir de este archivo JAR tal como se indica a continuación:

```
wsk action create helloJava hello.jar --main Hello
```
{: pre}

Cuando se utiliza la línea de mandatos y un archivo de origen `.jar`, no es necesario especificar que
está creando una acción Java; la herramienta lo determina
a partir de la extensión de archivo.

Tiene que especificar el nombre de la clase principal con `--main`. Una clase principal apta es una que implemente un método `main` estático tal como se ha descrito anteriormente. Si la clase no está en el paquete predeterminado, utilice el nombre de clase completo de Java, por ejemplo `--main com.example.MyMain`.

La invocación de la acción es la misma para acciones Java que para acciones Swift y JavaScript:

```
wsk action invoke --blocking --result helloJava --param name World
```
{: pre}

```
  {
      "greeting": "Hello World!"
  }
```
{: screen}


## Creación de acciones Docker
{: #openwhisk_actions_docker}

Con acciones Docker de {{site.data.keyword.openwhisk_short}}, puede escribir sus acciones en cualquier lenguaje.

Su código se compila en un binario ejecutable y se incluye en una imagen Docker. El programa binario interactúa con el sistema
aceptando la entrada desde `stdin` y respondiendo por medio de `stdout`.

Como requisito previo, debe tener una cuenta de Docker Hub.  Para configurar un ID y cuenta gratuitos de Docker, acceda a
[Docker Hub](https://hub.docker.com){: new_window}.

Para las instrucciones siguientes, supondremos que el ID de usuario es `janesmith` y la contraseña es `janes_password`.  Suponiendo que
la CLI ya se ha configurado, son necesarios tres pasos para configurar un binario personalizado para que lo use
{{site.data.keyword.openwhisk_short}}. Tras hacerlo, la imagen de Docker subida se podrá utilizar como una acción.

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
  Dockerfile      README.md       buildAndPush.sh example.c
  ```
  {: screen}

  El esqueleto es una plantilla de contenedor de Docker en la que puede inyectar código en forma de binarios personalizados.

2. Configure su binario personalizado en el esqueleto blackbox. El esqueleto ya incluye un programa en C que puede usar.

  ```
  cat dockerSkeleton/example.c
  ```
  {: pre}
  ```
  #include <stdio.h>

  int main(int argc, char *argv[]) {
      printf("This is an example log message from an arbitrary C program!\n");
      printf("{ \"msg\": \"Hello from arbitrary C program!\", \"args\": %s }",
             (argc == 1) ? "undefined" : argv[1]);
  }
  ```
  {: codeblock}

  Puede modificar este valor cuando sea necesario o añadir código y dependencias adicionales a la imagen de docker.
  En el último caso, es posible que sea necesario modificar el `archivo Docker` según convenga para crear el ejecutable.
  El binario debe estar en el contenedor en `/action/exec`.

  El ejecutable recibe un único argumento de la línea de mandatos. Es la serialización de una cadena del objeto JSON que representa los argumentos para la acción. El programa puede registrarse en `stdout` o `stderr`.
  Por convenio, la última línea de la salida *debe* ser un objeto JSON en forma de cadena que represente el resultado de la acción.

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
  chmod +x buildAndPush.sh
  ```
  {: pre}
  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}
  
  Tenga en cuenta que parte del archivo example.c está compilado como parte del proceso de compilación de imagen de Docker,
por lo que no necesita C compilado en su máquina.
  De hecho, salvo cuando compile el binario en una máquina de host compatible, es posible que no se ejecute dentro del contenedor porque los formatos no coinciden.
  
  El contenedor de Docker ahora se puede utilizar como acción de {{site.data.keyword.openwhisk_short}}.
  
  
  ```
  wsk action create --docker example janesmith/blackboxdemo
  ```
  {: pre}
  
  Observe el uso de `--docker` al crear una acción. Actualmente se presupone que todas las imágenes de Docker se alojan en Docker Hub.
  La acción se puede invocar como cualquier otra acción de {{site.data.keyword.openwhisk_short}}.
  
  ```
  wsk action invoke --blocking --result example --param payload Rey
  ```
  {: pre}
  ```
  {
      "args": {
          "payload": "Rey"
      },
      "msg": "Hello from arbitrary C program!"
  }
  ```
  {: screen}
  
  Para actualizar la acción de Docker, ejecute buildAndPush.sh para cargar la imagen más reciente en Docker Hub. Esto permitirá al sistema extraer la nueva imagen de Docker la próxima vez que ejecute el código para la acción.
  Si no hay contenedores recientes, cualquier invocación nueva utilizará la imagen de Docker nueva.
  Sin embargo, si hay un contenedor reciente que utiliza una versión anterior de la imagen de Docker, las nuevas invocaciones seguirán utilizando esta imagen a no ser que se ejecute wsk action update. Esto indicará al sistema que para las nuevas invocaciones debe ejecutar una extracción de Docker para obtener su nueva imagen de Docker.
 
  ```
  ./buildAndPush.sh janesmith/blackboxdemo
  ```
  {: pre}
  ```
  wsk action update --docker example janesmith/blackboxdemo
  ```
  {: pre}
  
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
  
## Acceso a metadatos de acción dentro del cuerpo de la acción

El entorno de acción contiene varias propiedades que son específicas de la acción que se está ejecutando.
Esto permite que la acción funcione según programa con activos de OpenWhisk mediante la API REST o permite establecer una alarma interna cuando la acción está a punto de alcanzar su presupuesto de tiempo permitido.
Se accede a las propiedades mediante el entorno del sistema para todos los tiempos de ejecución admitidos: Node.js, Python, Swift, Java y acciones Docker cuando se utiliza el esqueleto OpenWhisk Docker. 

* `__OW_API_HOST` el host de API correspondiente al despliegue OpenWhisk que ejecuta esta acción
* `__OW_API_KEY` la clave de API del asunto que invoca la acción; esta clave puede ser una clave de API restringida
* `__OW_NAMESPACE` el espacio de nombres de *activation* (puede diferir del espacio de nombres de la acción)
* `__OW_ACTION_NAME` el nombre completo de la acción que se está ejecutando
* `__OW_ACTIVATION_ID` el ID de activación de esta instancia de la acción en ejecución
* `__OW_DEADLINE` el tiempo aproximado en que esta acción habrá consumido toda su cuota de duración (medida en milisegundos epoch)
