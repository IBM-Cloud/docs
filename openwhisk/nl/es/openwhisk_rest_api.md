---

copyright:
  years: 2017
lastupdated: "2017-05-04"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilización de la API REST de OpenWhisk
{: #openwhisk_rest_api}

Tras habilitar su entorno OpenWhisk, puede usar OpenWhisk con sus apps web o apps móviles con llamadas a la API REST.


Para obtener más detalles sobre las API para acciones, activaciones, paquetes, reglas y desencadenantes, consulte la [Documentación de la API de OpenWhisk](http://petstore.swagger.io/?url=https://raw.githubusercontent.com/openwhisk/openwhisk/master/core/controller/src/main/resources/apiv1swagger.json).


Todas las funciones del sistema están disponibles a través de la API REST. Hay una colección y puntos finales de entidad para acciones, activadores, reglas, paquetes, activaciones y espacios de nombres.

Los puntos finales de colección son:
- `https://{APIHOST}/api/v1/namespaces`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations`

`{APIHOST}` es el nombre de host de la API de OpenWhisk (por ejemplo, openwhisk.ng.bluemix.net, 172.17.0.1, 192.168.99.100, 192.168.33.13 y así sucesivamente).
Para `{namespace}`, se puede utilizar el carácter `_` para especificar el *espacio de nombre predeterminado* del usuario. 

Puede realizar una solicitud GET en los puntos finales de colección para obtener una lista de todas las entidades de la colección.

Hay puntos finales de entidad para cada tipo de entidad:
- `https://{APIHOST}/api/v1/namespaces/{namespace}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/actions/[{packageName}/]{actionName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/triggers/{triggerName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/rules/{ruleName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/packages/{packageName}`
- `https://{APIHOST}/api/v1/namespaces/{namespace}/activations/{activationName}`

Los puntos finales de espacio de nombres y activación solo admiten solicitudes GET. Los puntos finales de acciones, desencadenantes, reglas y paquetes admiten solicitudes GET, PUT y DELETE. Los puntos finales de acciones, activadores y reglas también admiten solicitudes POST, que se utilizan para invocar acciones y activadores, y para habilitar o inhabilitar reglas. 

Todas las API están protegidas con autenticación HTTP básica. 
Utilice la herramienta [wskadmin](../tools/admin/wskadmin) para generar un nuevo espacio de nombres y autenticación. Las credenciales de autenticación básica se encuentran en la propiedad `AUTH` del archivo `~/.wskprops`, delimitadas por dos puntos. 
También puede recuperar estas credenciales con la interfaz de línea de mandatos ejecutando `wsk property get --auth`.


A continuación se muestra un ejemplo en el que se utiliza la herramienta de mandatos [cURL](https://curl.haxx.se) para obtener la lista de todos los paquetes del espacio de nombres `whisk.system`: 

```bash
curl -u USERNAME:PASSWORD https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/packages
```
{: pre}

```json
  [
  {
    "name": "slack",
    "binding": false,
    "publish": true,
    "annotations": [
      {
        "key": "description",
        "value": "Package that contains actions to interact with the Slack messaging service"
      }
    ],
    "version": "0.0.1",
    "namespace": "whisk.system"
  }
]
```

En este ejemplo, la autenticación se pasa con el distintivo `-u` que también se puede pasar como parte del URL como `https://$AUTH@{APIHOST}`

La API de OpenWhisk admite llamadas solicitud-respuesta de clientes web. OpenWhisk responde a las solicitudes de `OPTIONS` con cabeceras de uso compartido de recursos de distintos orígenes. Actualmente, estos orígenes están permitidos (es decir, Access-Control-Allow-Origin es "`*`") y Access-Control-Allow-Headers produce Authorization y Content-Type.

**Atención:** debido a que OpenWhisk admite en este momento únicamente una clave por espacio de nombres, no se recomienda utilizar CORS si no es para experimentar. Utilice [Acciones web](webactions.md) o una [Pasarela de API](apigateway.md) para exponer sus acciones al público y no utilizar la clave de autorización OpenWhisk para aplicaciones de cliente que precisan CORS.    

## Utilización de la modalidad detallada de la interfaz de línea de mandatos
{: #openwhisk_rest_api_cli_v}
OpenWhisk CLI es una interfaz para la API REST de OpenWhisk.
Puede ejecutar la interfaz de línea de mandatos en una modalidad detallada con el distintivo `-v`, con el que imprimirá toda la información sobre las respuestas y solicitudes HTTP. 

En el siguiente mandato se solicita obtener el valor del espacio de nombres para el usuario actual.
```
wsk namespace list -v
```
{: pre}
```
REQUEST:
[GET]	https://openwhisk.ng.bluemix.net/api/v1/namespaces
Req Headers
{
  "Authorization": [
    "Basic XXXYYYY"
  ]
}
RESPONSE:Got response with code 200
Resp Headers
{
  "Content-Type": [
    "application/json; charset=UTF-8"
  ]
}
Response body size is 28 bytes
Response body received:
["john@example.com_dev"]
```

Como puede ver, la información que se visualiza proporciona las propiedades de la solicitud HTTP, realiza un método HTTP `GET` en el URL `https://openwhisk.ng.bluemix.net/api/v1/namespaces` utilizando una cabecera de autenticación básica `Basic XXXYYYY`. Observe que el valor de autorización corresponde a su serie de autorización OpenWhisk codificada en base64. El tipo de contenido de la respuesta es `application/json`.

## Acciones
{: #openwhisk_rest_api_actions}
Si desea crear o actualizar una acción, envíe una solicitud HTTP con el método `PUT` de la colección de acciones. Por ejemplo, para crear una acción `nodejs:6` con el nombre `hello` utilizando un contenido de archivo individual se utilizaría el siguiente mandato: 
```bash
curl -u $AUTH -d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"}}' -X PUT -H "Content-Type: application/json" https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true 
```
{: pre}

Para realizar una invocación de creación de bloqueo en una acción, enviaría una solicitud HTTP con un método `POST` y un cuerpo con el parámetro `name`: 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}'  
```
{: pre}
Obtendría la respuesta siguiente:
```json
{
  "duration": 2,
  "name": "hello",
  "subject": "john@example.com_dev",
  "activationId": "c7bb1339cb4f40e3a6ccead6c99f804e",
  "publish": false,
  "annotations": [{
    "key": "limits",
    "value": {
      "timeout": 60000,
      "memory": 256,
      "logs": 10
    }
  }, {
    "key": "path",
    "value": "john@example.com_dev/hello"
  }],
  "version": "0.0.1",
  "response": {
    "result": {
      "payload": "Hello John"
    },
    "success": true,
    "status": "success"
  },
  "end": 1493327653769,
  "logs": [],
  "start": 1493327653767,
  "namespace": "john@example.com_dev"
}
```
Si tan solo desea obtener el `response.result`, ejecutaría de nuevo el mandato con el parámetro de consulta `result=true`
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?blocking=true&result=true" \
-X POST -H "Content-Type: application/json" \
-d '{"name":"John"}' 
```
{: pre}
Obtendría la respuesta siguiente:
```json
{
  "payload": "hello John"
}
```

## Anotaciones y acciones web
{: #openwhisk_rest_api_webactions}
Para crear una acción como, por ejemplo, una acción web, necesitará añadir una [anotación](annotations.md) `web-export=true` para las acciones web. Puesto que las acciones web son públicamente accesibles, debería proteger los parámetros predefinidos (por ejemplo, tratándolos como finales) con la anotación `final=true`. Si crea o actualiza una acción con el distintivo de CLI `--web true` este mandato añadirá tanto las anotaciones `web-export=true` como `final=true`. 

En este ejemplo se ejecuta el mandato curl proporcionando una lista completa de anotaciones a establecer en la acción
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/hello?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"hello","exec":{"kind":"nodejs:6","code":"function main(params) { return {payload:\"Hello \"+params.name}}"},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}'
```
{: pre}
Ahora podría invocar a esta acción como un URL público sin la necesidad de una autorización OpenWhisk. A continuación se realizaría la invocación utilizando el URL público de la acción incluida una extensión opcional como, por ejemplo, `.json` o `.http` al final del URL.
```bash
curl https://openwhisk.ng.bluemix.net/api/v1/web/john@example.com_dev/default/hello.json?name=John
```
{: pre}
```json
{
  "payload": "Hello John"
}
```
Observe que este código fuente de ejemplo no funcionará con `.http`, consulte la documentación de las [acciones web](webactions.md) para obtener información sobre cómo hacerlo.
## Secuencias
{: #openwhisk_rest_api_sequences}
Si desea crear una secuencia de acciones, necesitará crearla proporcionando los nombres de las acciones que forman la secuencia en el orden deseado de forma que la salida desde la primera acción se pase como una entrada para la siguiente acción. 

$ wsk action create sequenceAction --sequence /whisk.system/utils/split,/whisk.system/utils/sort

En este ejemplo se crea una secuencia con las acciones `/whisk.system/utils/split` y `/whisk.system/utils/sort`.
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/actions/sequenceAction?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"sequenceAction","exec":{"kind":"sequence","components":["/whisk.system/utils/split","/whisk.system/utils/sort"]},"annotations":[{"key":"web-export","value":true},{"key":"raw-http","value":false},{"key":"final","value":true}]}' 
```
{: pre}

Tenga en cuenta que los nombres de las acciones deben estar totalmente calificados al especificarlos. 

## Desencadenantes
{: #openwhisk_rest_api_triggers}
La información mínima que se necesita para crear un desencadenante es su nombre. Tiene la posibilidad de incluir en el desencadenante parámetros predeterminados que se pasan a la acción a través de una regla cuando dicho desencadenante se activa.  

En este ejemplo se crea un desencadenante con el nombre `events` con el parámetro `type` predeterminado estableciendo el valor `webhook`. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"events","parameters":[{"key":"type","value":"webhook"}]}' 
```
{: pre}

Ahora siempre que tuviese un suceso que necesitase activar este desencadenante tal solo sería necesario una solicitud HTTP con un método `POST` utilizando la clave de autorización OpenWhisk. 

Para activar el desencadenante `events` con el parámetro `temperature`, enviaría la siguiente solicitud HTTP. 

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/events \
-X POST -H "Content-Type: application/json" \
-d '{"temperature":60}' 
```
{: pre}

### Desencadenantes con acciones de canal de información
{: #openwhisk_rest_api_triggers_feed}
Hay varios desencadenantes especiales que se pueden crear utilizando una acción de canal de información. La acción de canal de información es una acción que ayuda en la configuración de un proveedor de canales de información que estará a cargo de activar el desencadenante siempre que se dé un suceso para ello. Para obtener más información sobre cómo utilizar los proveedores de canales de información, consulte la documentación de [feeds.md]. 

Algunos de los desencadenantes disponibles que dan soporte a las acciones de canal de información son alarmas/periódicas, Slack, Github, Cloudant/Couchdb y messageHub/Kafka. También es posible crear su propia acción y proveedor de canal de información. 

Vamos a crear un desencadenante con el nombre `periodic` para que se active cada 2 horas (es decir, 02:00:00, 04:00:00, ...).

Esto se puede realizar con un solo mandato desde la CLI
```bash
wsk trigger create periodic --feed /whisk.system/alarms/alarm \
  --param cron "0 */2 * * *" -v
```
{: pre}
Puesto que se está utilizando el distintivo `-v`, se envían dos solicitudes HTTP, una para crear el desencadenante `periodic` y otra para invocar una acción de canal de información `/whisk.system/alarms/alarm` con los parámetros para configurar el canal de información para activar el desencadenante cada 2 horas.
Para hacer lo mismo con la API REST, creamos primero el desencandenante 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"periodic","annotations":[{"key":"feed","value":"/whisk.system/alarms/alarm"}]}'  
```
{: pre}

La anotación `feed` se almacena en el desencadenante. Más tarde se utilizará esta anotación para saber qué acción de canal de información hay que utilizar al suprimir el desencadenante. 

Ahora que se ha creado el desencadenante, invocaremos la acción de canal de información
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"cron\":\"0 */2 * * *\",\"lifecycleEvent\":\"CREATE\",\"triggerName\":\"/_/periodic\"}" 
```
{: pre}

La supresión del desencadenante se parece a su creación, esta vez suprimiendo el desencadenante y también utilizando la acción de canal de información para configurar el proveedor de canal de información para suprimir el manejador para el desencadenante. 

Invocamos la acción de canal de información para suprimir el manejador de desencadenante desde el proveedor de canal de información
```bash
curl -u $AUTH "https://openwhisk.ng.bluemix.net/api/v1/namespaces/whisk.system/actions/alarms/alarm?blocking=true&result=false" \
-X POST -H "Content-Type: application/json" \
-d "{\"authKey\":\"$AUTH\",\"lifecycleEvent\":\"DELETE\",\"triggerName\":\"/_/periodic\"}"  
```
{: pre}

Ahora suprimiremos el desencadenante con una solicitud HTTP utilizando el método `DELETE`
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/triggers/periodic \
-X DELETE -H "Content-Type: application/json" 
```
{: pre}

## Reglas
{: #openwhisk_rest_api_rules}
Para crear una regla que asocia un desencadenante con una acción, envíe una solicitud HTTP con un método `PUT` proporcionando el desencadenante y la acción en el cuerpo de la solicitud. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"name":"t2a","status":"","trigger":"/_/events","action":"/_/hello"}' 
```
{: pre}

Tiene la posibilidad de habilitar o inhabilitar las reglas, y cambiar su estado actualizando su propiedad de estado. Por ejemplo, inhabilitaremos la regla `t2a` enviando en el cuerpo la solicitud `status: "inactive"` con un método `POST`. 
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/rules/t2a?overwrite=true \
-X POST -H "Content-Type: application/json" \
-d '{"status":"inactive","trigger":null,"action":null}'  
```
{: pre}

## Paquetes
{: #openwhisk_rest_api_packages}
Antes de crear una acción en un paquete, primero hay que crearlo. Para crear un paquete con el nombre `iot` enviaría una solicitud HTTP con un método `PUT`

```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/packages/iot?overwrite=true \
-X PUT -H "Content-Type: application/json" \
-d '{"namespace":"_","name":"iot"}' 
```
{: pre}

## Activaciones
{: #openwhisk_rest_api_activations}
Para obtener una lista de las últimas 3 activaciones utilice una solicitud HTTP con un método `GET`, pasaría el parámetro de consulta `limit=3`
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations?limit=3
```
{: pre}

Para obtener todos los detalles de una activación incluidos los resultados y registros, enviaríamos una solicitud HTTP con un método `GET` pasando el identificador de activación como un parámetro de vía de acceso
```bash
curl -u $AUTH https://openwhisk.ng.bluemix.net/api/v1/namespaces/_/activations/f81dfddd7156401a8a6497f2724fec7b
```
{: pre}
