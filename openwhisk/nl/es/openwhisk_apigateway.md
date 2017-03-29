---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# API Gateway (Experimental)
{: #openwhisk_apigateway}

La aplicación [Web Actions](openwhisk_webactions.html) está disponible a nivel general. 

Web Actions le permite invocar una acción con métodos HTTP que no sean POST sin la clave de API de autorización de la acción. 

Como resultado de los comentarios de los usuarios, Web Actions constituye el modelo de programación elegido para crear acciones de OpenWhisk capaces de manejar sucesos HTTP. 

La mayoría de las funciones de API Gateway se han fusionado en Web Actions; Web Actions le permite manejar cualquier solicitud HTTP y devolver respuestas HTTP con control completo por parte de la acción de la web. 

Pronto estará disponible una integración revisada de OpenWhisk API Gateway. Se configurará para que sirva como proxy de Web Actions, ofreciendo las funciones de API Gateway como limitación de velocidad, validación de señales oauth, claves API, etc. 

**Nota:** las API que haya creado con `wsk api-experimental` seguirán funcionando, aunque debe empezar a migrar sus API a acciones de la web. 

## Configuración de CLI de OpenWhisk
{: #openwhisk_apigateway_cli}
Esta característica experimental solo funciona con el nuevo modelo de autenticación de OpenWhisk, en el que cada espacio de nombres tiene asociada una clave de autenticación exclusiva.
Siga las instrucciones de [Configurar CLI](https://console.ng.bluemix.net/openwhisk/cli) para ver cómo se establece la clave de autenticación para su espacio de nombres específico.

## Exposición de una acción de OpenWhisk
{: #openwhisk_apigateway_hello}

Vamos a exponer una acción sencilla que ya viene preinstalada con OpenWhisk

```
wsk api-experimental create /hello /echo get /whisk.system/utils/echo
```
{: pre}
```
ok: created api /echo GET for action /whisk.system/utils/echo
https://21ef035.api-gw.mybluemix.net/hello/echo
```
{: screen}
Se genera un nuevo URL que expone la acción `echo` mediante un método **GET** HTTP.

Vamos a probarlo enviando una solicitud HTTP al URL.
```
curl https://21ef035.api-gw.mybluemix.net/hello/echo?marco=polo
```
{: pre}
Se invocará la acción `echo`, que devolverá una serie de caracteres JSON con los parámetros enviados.
```
{
  "marco":"polo"
}
```
{: screen}

Puede pasar parámetros a la acción mediante parámetros de consulta sencillos o mediante un cuerpo de solicitud.

### Exposición de varias acciones
{: #openwhisk_apigateway_actions}

Supongamos que desea exponer un conjunto de acciones correspondientes a un club de lectura para sus amigos.
Tiene una serie de acciones que implementar como programas de fondo para el club de lectura:

| acción | método http | descripción |
| ----------- | ----------- | ------------ |
| getBooks    | GET | obtener detalles libro  |
| postBooks   | POST | añade un libro |
| putBooks    | PUT | actualiza detalles libro |
| deleteBooks | DELETE | suprime un libro |

Vamos a crear una API para el club de lectura, llamada `Book Club`, con `/club` como vía de acceso base de URL HTTP y `books` como su recurso.
```
wsk api-experimental create -n "Book Club" /club /books get getBooks
wsk api-experimental create /club /books post postBooks
wsk api-experimental create /club /books put putBooks
wsk api-experimental create /club /books delete deleteBooks
```
{: pre}

Observe que la primera acción expuesta con la vía de acceso base `/club` obtiene la etiqueta de API llamada `Book Club` y otras acciones expuestas bajo `/club` se asociarán con `Book Club`

Vamos a generar una lista de todas las acciones que acabamos de exponer.

```
wsk api-experimental list
```
{: pre}
```
ok: apis
Action                   Verb          API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

Ahora, como simple diversión, vamos a añadir un libro nuevo, `JavaScript: The Good Parts`, con un HTTP **POST**
```
curl -X POST -d '{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}' https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": "success"
}
```
{: screen}

Vamos a obtener una lista de libros que utilizan nuestra acción `getBooks` mediante HTTP **GET**
```
curl -X GET https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: pre}
```
{
  "result": [{"name":"JavaScript: The Good Parts", "isbn":"978-0596517748"}]
}
```

### Exportación de configuración
Vamos a exportar la API denominada `Book Club` a un archivo que podemos utilizar como base para volver a crear las API utilizando un archivo como entrada. 
```
wsk api-experimental get "Book Club" > club-swagger.json
```
{: pre}

Vamos a probar el archivo swagger; para ello suprimiremos todos los URL expuestos bajo una vía de acceso base común.
Puede suprimir todos los URL expuestos que utilizan la vía de acceso base `/club` o la etiqueta de nombre de API `"Book Club"`:
```
wsk api-experimental delete /club
```
{: pre}
```
ok: deleted API /club
```
{: screen}

Ahora restauraremos la API denominada `Book Club` utilizando el archivo `club-swagger.json`
```
wsk api-experimental create --config-file club-swagger.json
```
{: pre}
```
ok: created api /books delete for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books get for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books post for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
ok: created api /books put for action deleteBook
https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

Podemos verificar que la API se ha vuelto a crear
```
wsk api-experimental list /club
```
{: pre}
```
ok: apis
Action                    Verb         API Name        URL
getBooks                   get         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
postBooks                 post         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
putBooks                   put         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
deleteBooks             delete         Book Club       https://2ef15285-gws.api-gw.mybluemix.net/club/books
```
{: screen}

- **Nota**: en estos momentos esta característica es una oferta experimental que ofrece a los usuarios la oportunidad de probarla y realizar comentarios. Ya se han recibido los siguientes comentarios:
  - No existe la posibilidad de personalizar el control de acceso HTTP para Cross-Origin Resource Sharing (CORS); actualmente, las cabeceras de la respuesta de API generada están configuradas para permitir cualquier verbo HTTP u origen (i.e. *). Siembre se devuelven las siguientes cabeceras:
    - Access-Control-Allow-Origin: *
    - Access-Control-Allow-Headers: Authorization, Content-Type
    - Access-Control-Allow-Methods: GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS
  - Solo se admite el tipo de contenido `application/json` para solicitud y respuesta.
  - No se puede controlar la respuesta mediante programación desde la acción OpenWhisk.
  - Todas las acciones OpenWhisk se exponen mediante acceso público; no existe la posibilidad de configurar una clave de API personalizada.
  - No se admiten parámetros de vía de acceso, solo parámetro de consulta y cuerpo de solicitud.
  - Si la API se crea sin un nombre de API, el nombre será la vía de acceso base y no se puede modificar
  - Cuando se vuelve a crear una API mediante un archivo de entrada, antes se debe suprimir la API.
  - Cuando se exportan API, contienen la clave de API de OpenWhisk; esta información es confidencial, sin plantilla disponible.
