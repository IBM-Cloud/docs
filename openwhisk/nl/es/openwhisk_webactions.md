---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Acciones web
{: #openwhisk_webactions}

Las acciones de la web son acciones de OpenWhisk anotadas para permitirle crear rápidamente aplicaciones basadas en la web. Esto le permite programar la lógica subyacente a la que la aplicación web puede acceder de forma anónima sin necesidad de disponer de una clave de autenticación de OpenWhisk. Depende del desarrollador de la acción si desea implementar su propio sistema de autenticación y autorización (es decir, flujo de OAuth).
{: shortdesc}

Las activaciones de acciones de la web estarán asociadas al usuario que ha creado la acción. Estas acciones transfieren el coste de la activación de una acción del que efectúa la llamada al propietario de la acción.

Tomaremos como ejemplo la siguiente acción JavaScript `hello.js`,
```javascript
function main({name}) {
  var msg = 'you did not tell me who you are.';
  if (name) {
    msg = `hello ${name}!`
  }
  return {body: `<html><body><h3>${msg}</h3></body></html>`}
}
```
{: codeblock}  

Puede crear una *acción de la web* `hello` en el paquete `demo` para el espacio de nombres `guest` utilizando el distintivo `--web` de la CLI con el valor `true` o `yes`:
```
wsk package create demo
```
{: pre}
```
wsk action create /guest/demo/hello hello.js --web true
```
{: pre}

Si especifica el distintivo `--web` con el valor `true` o `yes`, se puede acceder a una acción mediante la interfaz REST sin necesidad de credenciales. Una acción web se puede invocar utilizando un URL estructurado del siguiente modo:
`https://{APIHOST}/api/v1/web/{QUALIFIED ACTION NAME}.{EXT}`. El nombre completo de una acción consta de tres partes: el espacio de nombres, el nombre del paquete y el nombre de la acción.

*El nombre completo de la acción debe incluir el nombre de su paquete, que es 'default' si la acción no está en un paquete con nombre.*

Un ejemplo es `guest/demo/hello`. La vía de acceso a la API de la acción de la web se puede utilizar con `curl` o `wget` sin una clave de API. Incluso se puede escribir directamente en el navegador.

Intente abrir [https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello?name=Jane](https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello?name=Jane) en su navegador web. O intente invocar la acción a través de `curl`:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello?name=Jane
```
{: pre}

A continuación se muestra un ejemplo de acción de la web que realiza una redirección de HTTP:
```javascript
function main() {
  return { 
    headers: { location: 'http://openwhisk.org' },
    statusCode: 302
  }
}
```
{: codeblock}    

O define una cookie:
```javascript
function main() {
  return { 
    headers: { 
      'Set-Cookie': 'UserID=Jane; Max-Age=3600; Version=',
      'Content-Type': 'text/html'
    },
    statusCode: 200,
    body: '<html><body><h3>hello</h3></body></html>' }
}
```
{: codeblock}  

O devuelve `image/png`:
```javascript
function main() {
    let png = <base 64 encoded string>
    return { headers: { 'Content-Type': 'image/png' },
             statusCode: 200,
             body: png };
}
```
{: codeblock}  

Or returns `application/json`:
```javascript
function main(params) { 
    return {
        statusCode: 200,
        headers: { 'Content-Type': 'application/json' },
        body: new Buffer(JSON.stringify(params)).toString('base64'),
    };
}
```
{: codeblock}  

It is important to be aware of the [límite de tamaño de respuesta](./openwhisk_reference.html) de las acciones, ya que las respuestas que superen los límites predefinidos del sistema fallarán. No se deben enviar en línea objetos grandes a través de OpenWhisk, sino que se deben deferir a un almacén de objetos, por ejemplo.

## Manejo de solicitudes HTTP con acciones
{: #openwhisk_webactions_http}

Una acción de OpenWhisk que no sea una acción de la web necesita autenticación y debe responder con un objeto JSON. Por el contrario, las acciones de la web se pueden invocar sin autenticación y se pueden utilizar para implementar manejadores HTTP que respondan con contenido de *headers*, *statusCode* y *body* de distintos tipos. La acción de la web debe devolver un objeto JSON, pero el sistema OpenWhisk (concretamente el `controlador`) tratará una acción de la web de forma distinta si su resultado incluye una o varias de las siguientes como propiedades JSON de nivel superior:

- `headers`: un objeto JSON en el que las claves son nombres de cabeceras y los valores son series de caracteres correspondientes a dichas cabeceras (el valor predeterminado es sin cabeceras).
- `statusCode`: un código de estado de HTTP válido (el valor predeterminado es 200 OK).
- `body`: una serie de caracteres que puede ser texto sin formato o una serie codificada en base64 (para datos binarios).

El controlador pasará las cabeceras especificadas por la acción, si las hay, al cliente HTTP cuando finalice la solicitud/respuesta. Asimismo, el controlador responderá con el código de estado proporcionado cuando exista. Por último, el cuerpo se pasa como cuerpo de la respuesta. A no ser que se declare `content-type header` en el valor `headers` de los resultados de la acción, el cuerpo se pasa tal cual si es una serie de caracteres (de lo contrario se genera un error). Si se ha definido `content-type`, el controlador determina si componen la respuesta datos binarios o texto sin formato y decodifica la serie con un decodificador base64 si es necesario. Si el cuerpo no se decodifica correctamente, se devuelve un error al emisor de la llamada.

*Nota*: un objeto JSON o matriz se trata como datos binarios y se debe codificar en base64 tal como se muestra en el ejemplo anterior.

## Contexto HTTP

Todas las acciones de la web reciben, cuando se invocan, detalles adicionales de solicitud HTTP como parámetros del argumento de entrada de la acción. Son los siguientes:

- `__ow_method` (tipo: serie): el método HTTP de la solicitud.
- `__ow_headers` (tipo: correlación entre serie y serie): cabeceras de la solicitud.
- `__ow_path` (tipo: serie): vía de acceso no comparada de la solicitud (la comparación finaliza después de consumir la extensión de la acción).
- `__ow_user` (tipo: serie): espacio de nombres que identifica el asunto autenticado de OpenWhisk
- `__ow_body` (tipo: serie): entidad del cuerpo de la solicitud, como serie codificada en base64 cuando el contenido es binario o serie de texto sin formato en caso contrario
- `__ow_query` (tipo: serie): parámetros de la consulta procedentes de la solicitud como serie sin analizar

Una solicitud no puede sustituir ninguno de los parámetros `__ow_` mencionados anteriormente; si lo hiciera, la solicitud fallaría con el estado 400 Solicitud errónea.

El valor `__ow_user` solo aparece cuando la acción de la web tiene una [anotación que indica que requiere autenticación](./openwhisk_annotations.html#openwhisk_annotations_webactions) y permite que una acción de la web implemente su propia política de autorización. `__ow_query` solo está disponible cuando una acción de la web elige manejar la [solicitud HTTP "sin procesar"](#raw-http-handling). Es una serie que contiene los parámetros de la consulta analizados del URI (separados por `&`). La propiedad `__ow_body` aparece cuando se gestionan solicitudes HTTP "sin procesar" o cuando la entidad de la solicitud HTTP no es un objeto JSON ni datos de formulario. De lo contrario las acciones de la web reciben parámetros de consulta y de cuerpo como propiedades de primera clase en los argumentos de la acción, donde los parámetros de cuerpo prevalecen sobre los parámetros de consulta, que a su vez prevalecen sobre los parámetros de acción y de paquete.

## Características adicionales

Las acciones de la web incorporan algunas características adicionales que incluyen:

- `Extensiones de contenido`: la solicitud debe especificar el tipo de contenido deseado como `.json`, `.html`, `.http`, `.svg` o `.text`. Para ello se añade una extensión al nombre de la acción en el URI, de modo que se haga referencia a la acción `/guest/demo/hello` como `/guest/demo/hello.http`, por ejemplo para recibir una respuesta HTTP. Para su comodidad, supondremos que se utiliza la extensión `.http` cuando no se detecta ninguna extensión.
- `Proyección de campos desde el resultado`: la vía de acceso que sigue al nombre de la acción se utiliza para proyectar uno o varios niveles de respuesta. Por ejemplo, `/guest/demo/hello.html/body`. Esto permite una acción que devuelve un diccionario `{body: "..." }` para proyectar la propiedad `body` y devolver directamente el valor de su serie. La vía de acceso proyectada sigue un modelo de vía de acceso absoluta (como en XPath).
- `Parámetros de consulta y de cuerpo como entrada`: la acción recibe parámetros de consulta y parámetros en el cuerpo de la solicitud. El orden de prioridad para fusionar parámetros es el siguiente: parámetros de paquete, parámetros de acción, parámetros de consulta, parámetros de cuerpo y cada uno de los valores de sustitución y anteriores en caso de solapamiento. Por ejemplo, `/guest/demo/hello.http?name=Jane` pasará el argumento `{name: "Jane"}` a la acción.
- `Datos de formulario`: además de `application/json` estándar, las acciones de la web pueden recibir como entrada un URL codificado procedente de los datos `application/x-www-form-urlencoded data`.
- `Activación mediante varios verbos HTTP`: se puede invocar una acción de la web mediante uno de estos métodos HTTP: `GET`, `POST`, `PUT`, `PATCH` y `DELETE`, así como `HEAD` y `OPTIONS`.
- `Gestión de entidades que no son de cuerpo JSON ni HTTP sin procesar (RAW HTTP)`: una acción de la web puede aceptar un cuerpo de solicitud HTTP que no sea un objeto JSON y puede optar por recibir siempre estos valores como valores opacos (texto sin formato cuando no están en binario o serie codificada en base64 en caso contrario).

El ejemplo siguiente muestra brevemente cómo puede utilizar estas características en una acción de la web. Supongamos que tenemos una acción `/guest/demo/hello` con el siguiente cuerpo:
```javascript
function main(params) { 
    return { response: params };
}
```

Cuando se invoca esta acción una acción de la web, puede alterar la respuesta de la acción de la web protegiendo diferentes vías de acceso desde el resultado.
Por ejemplo, para devolver el objeto completo y ver los argumentos que recibe la acción:

```
 curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json
 ```
{: pre}
```json
{
  "response": {
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

y con un parámetro de consulta:
```
 curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane
 ```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "get",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

o datos de formulario:
```
 curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -d "name":"Jane"
 ```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "10",
      "content-type": "application/x-www-form-urlencoded",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

o un objeto JSON:
```
 curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: application/json' -d '{"name":"Jane"}'
```
{: pre}
```json
{
  "response": {
    "name": "Jane",
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

y para proyectar únicamente el nombre (como texto):
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.text/response/name?name=Jane
```
{: pre}
```
Jane
```

En el ejemplo anterior verá que, para su comodidad, los parámetros de consulta, datos de formulario y entidades de cuerpo de objeto JSON se tratan como diccionarios ya que se puede acceder directamente a sus valores como propiedades de entrada de la acción. Esto no se aplica a las acciones de la web que optan por gestionar las entidades de solicitud HTTP de forma más directa ni cuando la acción de la web recibe una entidad que no es un objeto JSON.

A continuación encontrará un ejemplo de uso de un tipo de contenido "text" con el mismo ejemplo mostrado anteriormente:
```
curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json -H 'Content-Type: text/plain' -d "Jane"
```
{: pre}
```json
{
  "response": {
    "__ow_method": "post",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "4",
      "content-type": "text/plain",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": "",
    "__ow_body": "Jane"
  }
}
```


## Extensiones de contenido
{: #openwhisk_webactions_extensions}

Generalmente se necesita una extensión de contenido cuando se invoca una acción de la web; si no se especifica, se adopta `.http` como valor predeterminado. Las extensiones `.json` y `.http` no necesitan una vía de acceso de proyección. Sin embargo, para las extensiones `.html`, `.svg` y `.text` se supone que la vía de acceso predeterminada coincide con el nombre de la extensión. Por lo tanto, para invocar una acción de la web y recibir una respuesta `.html`, la acción debe responder con un objeto JSON que conste de una propiedad de nivel superior denominada `html` (o la respuesta debe estar en la vía de acceso especificada de forma explícita). Es decir, `/guest/demo/hello.html` equivale a proyectar la propiedad `html` de forma explícita, como en el caso de `/guest/demo/hello.html/html`. El nombre completo de la acción debe incluir el nombre de su paquete, que es `default` si la acción no está en un paquete con nombre.


## Parámetros protegidos
{: #openwhisk_webactions_protected}

Generalmente se necesita una extensión de contenido cuando se invoca una acción de la web; si no se especifica, se adopta `.http` como valor predeterminado. Las extensiones `.json` y `.http` no necesitan una vía de acceso de proyección. Sin embargo, para las extensiones `.html`, `.svg` y `.text` se supone que la vía de acceso predeterminada coincide con el nombre de la extensión. Por lo tanto, para invocar una acción de la web y recibir una respuesta `.html`, la acción debe responder con un objeto JSON que conste de una propiedad de nivel superior denominada `html` (o la respuesta debe estar en la vía de acceso especificada de forma explícita). Es decir, `/guest/demo/hello.html` equivale a proyectar la propiedad `html` de forma explícita, como en el caso de `/guest/demo/hello.html/html`. El nombre completo de la acción debe incluir el nombre de su paquete, que es `default` si la acción no está en un paquete con nombre.


## Parámetros protegidos

Los parámetros de la acción están protegidos y se tratan como inalterables. Los parámetros finalizan automáticamente cuando se habilitan las acciones web.

```
 wsk action create /guest/demo/hello hello.js \
      --parameter name Jane \
      --web true
```

El resultado de estos cambios es que `name` se vincula a `Jane` y no lo pueden modificar ni los parámetros de la consulta ni los del cuerpo debido a la anotación final. Esto protege la acción frente a parámetros de consulta o de cuerpo que intenten modificar este valor, ya sea intencionadamente o por accidente. 

## Inhabilitación de acciones de la web

Para inhabilitar la invocación de una acción web mediante la API web (`https://openwhisk.ng.bluemix.net/api/v1/web/`), pase el valor `false` o `no` al distintivo `--web` cuando actualice una acción con la CLI.

```
 wsk action update /guest/demo/hello hello.js --web false
```
{: pre}

## Manejo de HTTP RAW

Una acción de la web puede optar por interpretar y procesar un cuerpo HTTP directamente, sin la promoción de un objeto JSON a las propiedades de primera clase disponibles para la entrada de la acción (es decir, `args.name` frente a analizar `args.__ow_query`). Esto se hace con `raw-http` [annotation](annotations.md). Utilizaremos el ejemplo anterior, pero ahora como una acción de la web HTTP "sin procesar" que recibe `name` como parámetro de consulta y como valor JSON en el cuerpo de la solicitud HTTP:
```
 curl https://openwhisk.ng.bluemix.net/api/v1/web/guest/demo/hello.json?name=Jane -X POST -H "Content-Type: application/json" -d '{"name":"Jane"}' 
```
{: pre}
```json
{
  "response": {
    "__ow_method": "post",
    "__ow_query": "name=Jane",
    "__ow_body": "eyJuYW1lIjoiSmFuZSJ9",
    "__ow_headers": {
      "accept": "*/*",
      "connection": "close",
      "content-length": "15",
      "content-type": "application/json",
      "host": "172.17.0.1",
      "user-agent": "curl/7.43.0"
    },
    "__ow_path": ""
  }
}
```

Observe que en este caso el contenido JSON está codificado en Base64 porque se trata como un valor binario. La acción se debe descodificar en Base64 y JSON debe analizar este valor para recuperar el objeto JSON. OpenWhisk utiliza la infraestructura [Spray](https://github.com/spray/spray) para [determinar](https://github.com/spray/spray/blob/master/spray-http/src/main/scala/spray/http/MediaType.scala#L282) qué tipos de contenido son binarios y cuáles son texto sin formato.


### Habilitación del manejo de HTTP sin procesar

Las acciones HTTP web sin procesar se habilitan asignando al distintivo `--web` el valor `raw`.

```
 wsk action create /guest/demo/hello hello.js --web raw
```

### Inhabilitación del manejo de HTTP sin procesar

La inhabilitación de HTTP sin procesar se consigue pasando el valor `false` o `no` al distintivo `--web`.

```
 wsk update create /guest/demo/hello hello.js --web false
```

### Decodificación de contenido de cuerpo binario de Base64

Si se utiliza el manejo de HTTP sin procesar, el contenido `__ow_body` se decodificará en Base64 cuando la solicitud content-type sea binaria.
A continuación encontrará funciones que muestran cómo decodificar el contenido del cuerpo en Node, Python y Swift. Simplemente guarde el método que se muestra bajo el archivo, cree una nueva acción
web HTTP sin procesar utilizando el artefacto guardado e invoque la acción web.

#### Node

```javascript
  function main(args) {
    decoded = new Buffer(args.__ow_body, 'base64').toString('utf-8')
    return {body: decoded}
}
```
{: codeblock}

#### Python

```python
def main(args):
    try:
        decoded = args['__ow_body'].decode('base64').strip()
        return {"body": decoded}
    except:
        return {"body": "Could not decode body from Base64."}
```
{: codeblock}

#### Swift

```swift
extension String {
    func base64Decode() -> String? {
        guard let data = Data(base64Encoded: self) else {
            return nil
        }

        return String(data: data, encoding: .utf8)
    }
}

func main(args: [String:Any]) -> [String:Any] {
    if let body = args["__ow_body"] as? String {
        if let decoded = body.base64Decode() {
            return [ "body" : decoded ]
        }
    }

    return ["body": "Could not decode body from Base64."]
}
```
{: codeblock}

Como ejemplo, guarde la función Node como `decode.js` y ejecute los mandatos siguientes:
```
 wsk action create decode decode.js --web raw
```
{: pre}
```
ok: created action decode
```
```
curl -k -H "content-type: application" -X POST -d "Decoded body" https:// openwhisk.ng.bluemix.net/api/v1/web/guest/default/decodeNode.json
```
{: pre}
```json
{
  "body": "Decoded body"
}
```

## Tratamiento de errores
{: #openwhisk_webactions_errors}

Cuando una acción OpenWhisk falla, hay dos modalidades de anomalías. La primera se conoce como *error de aplicación* y es similar a una excepción interceptada: la acción devuelve un objeto JSON que contiene una propiedad `error` de nivel superior. La segunda es un *error de desarrollador*, que se produce cuando la acción falla de forma catastrófica y no genera ninguna respuesta (este caso es similar a una excepción no capturada). En el caso de acciones de la web, el controlador trata los errores de aplicación del siguiente modo:

- Cualquier proyección de vía de acceso especificada se pasa por alto y el controlador proyecta en su lugar la propiedad `error`.
- El controlador aplica el manejo de contenido implícito según la extensión de la acción al valor de la propiedad `error`.

Los desarrolladores deben saber cómo se pueden utilizar las acciones de la web y deben generar consecuentemente las respuestas a los errores. Por ejemplo, una acción de la web que se utilice con la extensión `.http` debe devolver una respuesta HTTP, como por ejemplo `{error: { statusCode: 400 }`. Si no es así, se producirá una discordancia entre el tipo de contenido implícito a partir de la extensión y el tipo de contenido de la acción en la respuesta al error. Hay que tener especial cuidado con las acciones de la web que son secuencias, ya que los componentes que forman una secuencia pueden generar errores adecuados cuando es necesario.

