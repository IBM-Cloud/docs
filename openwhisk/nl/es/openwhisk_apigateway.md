---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-26"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Pasarela de API
{: #openwhisk_apigateway}

La gestión de API permite gestionar acciones de OpenWhisk. 

La pasarela de API actúa como un proxy para las [acciones web](webactions.md) y les proporciona características adicionales como, por ejemplo, direccionamiento de métodos HTTP, id/secretos de cliente, limitación de tasas de llamadas, CORS, visualización de utilización de API y registros de respuestas y permite definir políticas de compartición de API.
Para obtener más información sobre la característica de la pasarela de API consulte la [documentación de gestión de api](/docs/apis/management/manage_openwhisk_apis.html#manage_openwhisk_apis)

## Creación de API desde acciones web de OpenWhisk utilizando su navegador. 

Con la pasarela de API puede exponer una acción de OpenWhisk como una API. Después de definir la API, puede aplicar políticas de seguridad y de limitación de tasa de llamadas, visualizar la utilización de las API y los registros de respuesta, así como definir políticas de compartición de API. En el panel de control de OpenWhisk, pulse el [separador API](https://console.ng.bluemix.net/openwhisk/apimanagement).


## Creación de API desde acciones web de OpenWhisk utilizando la interfaz de línea de mandatos

### Configuración de la interfaz de línea de mandatos de OpenWhisk

Configure la interfaz de línea de mandatos de OpenWhisk con la apihost `wsk property set --apihost openwhisk.ng.bluemix.net`. Para poder utilizar la `wsk api`, el archivo de configuración de interfaz de línea de mandatos `~/.wskprops` debe contener la señal de acceso de Bluemix. Para obtener la señal de acceso utilice el mandato de interfaz de línea de mandatos `wsk bluemix login`. Para obtener más información sobre el mandato, ejecute `wsk bluemix login -h`

**Nota:** Si el mandato produce errores indicando que es necesario el inicio de sesión único (sso), tenga en cuenta que actualmente no se da soporte a esta característica. Como método alternativo inicie una sesión con la interfaz de línea de mandatos de CloudFoundry utilizando `cf login` y, a continuación, copie la señal de acceso desde el archivo de configuración del directorio HOME `~/.cf/config.json` en el archivo `~/.wskprops` como la propiedad `APIGW_ACCESS_TOKEN="valor de AccessToken"`. Elimine el prefijo `Bearer ` al copiar la serie de la señal de acceso. 

**Nota:** Las API que haya creado con `wsk api-experimental` seguirán funcionando por un periodo breve, aunque debe empezar a migrar sus API a acciones web y reconfigurar sus api existentes con el nuevo mandato de interfaz de línea de mandatos `wsk api`. 

### Creación de su primera API utilizando la interfaz de línea de mandatos

1. Crear un archivo JavaScript con el contenido siguiente. Para este ejemplo, el nombre de archivo es 'hello.js'.
  ```javascript
  function main({name:name='Serverless API'}) {
      return {payload: `Hello world ${name}`};
  }
  ```
  {: codeblock}
  
2. Cree una acción web desde la siguiente función JavaScript. En este ejemplo, la acción se llama 'hello'. Asegúrese de añadir el distintivo `--web true`. 
  
  ```
  wsk action create hello hello.js --web true
  ```
  {: pre}
  ```
  ok: created action hello
  ```
  
3. Cree una API con la vía de acceso `/hello`, vía `/world` y método `get` con el tipo de respuesta `json`
  
  ```
  wsk api create /hello /world get hello --response-type json
  ```
  ```
  ok: created API /hello/world GET for action /_/hello
  https://${APIHOST}:9001/api/21ef035/hello/world
  ```
Se genera un nuevo URL que expone la acción `hello` mediante un método **GET** HTTP.    
4. Vamos a probarlo enviando una solicitud HTTP al URL.
  
  ```
  $ curl https://${APIHOST}:9001/api/21ef035/hello/world?name=OpenWhisk
  ```
  ```json
{
  "payload": "Hello world OpenWhisk"
  }
  ```
Se invocó la acción web `hello`, devolviendo de vuelta un objeto JSON que incluye el parámetro `name` enviado mediante el parámetro de consulta. Puede pasar parámetros a la acción mediante parámetros de consulta sencillos o mediante el cuerpo de la solicitud. Las acciones web permiten invocar una acción de forma pública sin la clave de API de autorización de OpenWhisk.   
### Control completo sobre la respuesta HTTP
  
  El distintivo `--response-type` controla el URL de destino de la acción web que la pasarela API debe intermediar. Utilizando `--response-type json` como antes devuelve el resultado completo de la acción en formato JSON y de forma automática establece la cabecera Content-Type con `application/json` lo que le permitirá empezar a tratar con facilidad la respuesta.  
  
  Una vez haya empezado, deseará tener un control completo sobre las propiedades de respuesta HTTP como, por ejemplo `statusCode` o `headers`, y devolver distintos tipos de contenido en `body`. Puede hacer esto mediante `--response-type http` para configurar el URL de destino de la acción web con la extensión `http`. 

  Puede elegir cambiar el código de la acción para satisfacer con la devolución de las acciones web con la extensión `http` o incluir la acción en una secuencia pasando su resultado a una nueva acción que transforma el resultado para que corresponda a una respuesta HTTP con el formato adecuado. Puede obtener más información sobre los tipos de respuesta y las extensiones de acciones web en la documentación de [acciones web](webactions.md).  

  Cambie el código de `hello.js` que devuelve las propiedades JSON `body`, `statusCode` y `headers`
  ```javascript
  function main({name:name='Serverless API'}) {
      return {
        body: new Buffer(JSON.stringify({payload:`Hello world ${name}`})).toString('base64'), 
        statusCode:200, 
        headers:{ 'Content-Type': 'application/json'}
      };
  }
  ```
  {: codeblock}
 Tenga en cuenta que body se debe devolver codificado en `base64` y no como una serie.
  
  Actualice la acción con el resultado modificado
  ```
  wsk action update hello hello.js --web true
  ```
  {: pre}
  Actualice la API con `--response-type http`
  ```
  wsk api create /hello /world get hello --response-type http
  ```
  {: pre}
  Ahora llamaremos a la API actualizada
```
  curl https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/hello/world
  ```
  {: pre}
  ```json
{
  "payload": "Hello world Serverless API"
  }
  ```
  Ahora tiene un control completo de sus API, puede controlar el contenido como devolviendo HTML o establecer el código de estado para estados como No encontrado (404), No autorizado (401) o incluso Error interno de servidor (500).
### Exposición de varias acciones web

Supongamos que desea exponer un conjunto de acciones correspondientes a un club de lectura para sus amigos.
Tiene una serie de acciones que implementar como programas de fondo para el club de lectura:

| acción | método HTTP | descripción |
| ----------- | ----------- | ------------ |
| getBooks    | GET | obtener detalles libro  |
| postBooks   | POST | añade un libro |
| putBooks    | PUT | actualiza detalles libro |
| deleteBooks | DELETE | suprime un libro |

Vamos a crear una API para el club de lectura, llamada `Book Club`, con `/club` como vía de acceso base de URL HTTP y `books` como su recurso.
```
wsk api create -n "Book Club" /club /books get getBooks --response-type http
wsk api create /club /books post postBooks              --response-type http
wsk api create /club /books put putBooks                --response-type http
wsk api create /club /books delete deleteBooks          --response-type http
```

Observe que la primera acción expuesta con la vía de acceso base `/club` obtiene la etiqueta de API llamada `Book Club` y otras acciones expuestas bajo `/club` se asociarán con `Book Club`

Vamos a generar una lista de todas las acciones que acabamos de exponer.

```
wsk api list -f
```
```
ok: APIs
Action: getBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: get
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: postBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: post
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: putBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: put
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
Action: deleteBooks
  API Name: Book Club
  Base path: /club
  Path: /books
  Verb: delete
  URL: https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

Ahora, como simple diversión, vamos a añadir un libro nuevo, `JavaScript: The Good Parts`, con un HTTP **POST**
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": "success"
}
```

Vamos a obtener una lista de libros que utilizan nuestra acción `getBooks` mediante HTTP **GET**
```
curl -X GET https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### Exportación de configuración
Vamos a exportar la API denominada `Book Club` a un archivo que podemos utilizar como base para volver a crear las API utilizando un archivo como entrada. 
```
wsk api get "Book Club" > club-swagger.json
```

Vamos a probar el archivo swagger; para ello suprimiremos todos los URL expuestos bajo una vía de acceso base común.
Puede suprimir todos los URL expuestos que utilizan la vía de acceso base `/club` o la etiqueta de nombre de API `"Book Club"`:
```
wsk api delete /club
```
```
ok: deleted API /club
```
### Modificación de la configuración

Para editar la configuración en el panel de control OpenWhisk, pulse el [separador API](https://console.ng.bluemix.net/openwhisk/apimanagement) para configurar, por ejemplo, la seguridad o limitar las tasas de llamadas. 

### Importación de la configuración

Ahora restauraremos la API denominada `Book Club` utilizando el archivo `club-swagger.json`
```
wsk api create --config-file club-swagger.json
```
```
ok: created api /books delete for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books get for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books post for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
ok: created api /books put for action deleteBook
https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```

Podemos verificar que la API se ha vuelto a crear
```
wsk api list /club
```
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
postBooks                 post         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
putBooks                   put         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
deleteBooks             delete         Book Club       https://service.us.apiconnect.ibmcloud.com/gws/apigateway/api/21ef035/club/books
```
