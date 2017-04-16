---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Ejemplos de Insights for Twitter
{: #examples}

Para empezar a utilizar el servicio {{site.data.keyword.twittershort}}, utilice los ejemplos proporcionados para saber cómo aprovechar sus prestaciones.
{: shortdesc}

## Demo de Insights for Twitter
{: #insights_twitter_demo}

Tiene a su disposición una aplicación de ejemplo para realizar búsquedas en los flujos de datos de Twitter que utilizan el servicio {{site.data.keyword.twittershort}}. Para acceder a la aplicación, vaya a [https://cdetestapp.mybluemix.net/](https://cdetestapp.mybluemix.net/){: new.window}. La aplicación se abre en el navegador y visualiza un campo de búsqueda, con los botones **Búsqueda de Twitter** y **Número de Twitter**. 

![Imagen de interfaz de usuario con el campo de búsqueda.](images/sample1_UI.jpg "Imagen de interfaz de usuario con el campo de búsqueda.")

En la aplicación de ejemplo puede buscar tuits utilizando al mismo tiempo los parámetros y operadores soportados que se describen en [Lenguaje de consulta](twitter_rest_apis.html#querylanguage){: new.window}. Por ejemplo, si escribe "IBM Twitter" (con un espacio para denotar una operación AND booleana), y pulsa **Búsqueda en Twitter**, devuelva lot tuits que contienen los dos términos.

![Imagen de término de consulta y resultados de búsqueda.](images/sample1_tweet_search.jpg "Imagen de término de consulta y resultados de búsqueda devueltos.")

Con "IBM Twitter" especificado en el campo de búsqueda, al pulsar **Número de Twitter** devuelve el número de tuits que contienen los dos términos.

![Imagen de término de consulta y resultados de recuento devueltos.](images/sample1_tweet_count.jpg "Imagen de término de consulta y resultados de recuento devueltos.")

## Creación de un seguimiento de reglas
{: #creating_rule_track}

Como usuario Plan de entrada, puede crear seguimientos basados en reglas para filtrar tuits recopilados en el flujo de datos PowerTrack. Los ejemplos en secciones posteriores demuestran cómo editar y suprimir seguimientos, así como ejecutar una llamada de API search o count en la secuencia PowerTrack. Para crear un seguimiento de regla, emita una solicitud **POST** con la operación /api/v1/tracks, especifique el tipo de seguimiento (**Regla**), indique un 'EndDate' e incluya como mínimo una regla. El siguiente fragmento de código es una solicitud de ejemplo que incluye dos reglas:

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks
HTTP/1.1 Content-Type: application/json
{
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "type": "Rule",
    "rules": [
        {"value": "Canada"},
        {"value": "sport hockey"}
    ]
}
```

El nombre de usuario (`username`) y la contraseña (`password`) son exclusivos para la instancia de servicio y aplicación. Esta información se puede obtener de las variables de entorno **VCAP_SERVICES**. Para obtener más información, consulte [Guía de iniciación a {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

El cuerpo de la respuesta se parece al siguiente fragmento de código:

```
HTTP/1.1 201 Created
Content-Type: application/json;charset=utf-8
Location: https://cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
{
    "id": "66ff1961-51fe-4475-8bcd-c02f071d6fd1",
    "type": "Rule",
    "state": "Active",
    "createdDate": "2015-08-06T20:38:28.940Z",
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "rules": [
        {
          "id": "06497963-4fe3-47e8-90cd-aaef25f31314"
          "value": "Canada"
        },
        {
          "id": "d021165d-85e2-456a-af16-b9c026d76208",
          "value": "sport hockey"
        }
    ]
}
```

La respuesta incluye el ID exclusivo que está asociado con el seguimiento recién creado. Además,
a cada regla se le asigna un ID exclusivo. endDate indica cuando el seguimiento deja de recopilar mensajes y debe ajustarse al formato UTC (`AAAA-MM-DD` o `AAAA-MM-DDTHH:MM:SSZ`). La propiedad de tipo debe especificarse como **Regla** o **Agregado**. Como este ejemplo muestra la creación de un seguimiento basado en reglas, se ha especificado el tipo **Regla**.

Si no se especifica la propiedad de estado en la solicitud, de forma predeterminada se crea el seguimiento y está **Activo**. La propiedad de nombre es opcional y no es necesario que sea exclusiva. Para gestionar mejor los filtros, se
recomienda seleccionar un nombre descriptivo y exclusivo.

Para obtener información más detallada sobre la sintaxis de reglas, consulte el {{site.data.keyword.twittershort}} [Lenguaje de consulta](twitter_rest_apis.html#querylanguage){: new.window}.

## Creación de un seguimiento agregado
{: #creating_aggregated_track}

Como usuario Plan de entrada, puede crear seguimientos agregados
que combinan dos o más seguimientos existentes. Los seguimientos agregados pueden incluir seguimientos basados en
reglas y otros seguimientos agregados. La búsqueda de tuits desde un seguimiento agregado devuelve resultados desde sus seguimientos constituyentes. Para crear un segumiento agregado, emita una solicitud **POST** con la operación /api/v1/tracks, especifique el tipo de seguimiento (**Agregado**) e incluya uno o más trackIds. El siguiente fragmento de código es una solicitud de ejemplo que incluye dos seguimientos:

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks
HTTP/1.1 Content-Type: application/json
{
    "name": "My Aggregated Track",
    "type": "Aggregated",
    "trackIds": [
       {"id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"},
       {"id": "180356df-9a78-491e-b070-f3ffbe00bdf2"}
     ]
}
```
El nombre de usuario (`username`) y la contraseña (`password`) son exclusivos para la instancia de servicio y aplicación. Esta información se puede obtener de las variables de entorno **VCAP_SERVICES**. Para obtener más información, consulte [Guía de iniciación a {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

El cuerpo de la respuesta se parece al siguiente fragmento de código:

```
HTTP/1.1 201 Created
Content-Type: application/json;charset=utf-8
Location: https://cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
{
  "id": "9808fb82-7ea8-4b8e-9cd5-ad653a6dabe6",
  "type": "Aggregated",
  "createdDate": "2015-08-07T17:05:51.214Z",
  "name": "My Aggregated Track",
  "trackIds": [
    {
      "id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"
    },
    {
      "id": "180356df-9a78-491e-b070-f3ffbe00bdf2"
    }
  ]
}
```

La respuesta incluye el ID exclusivo que está asociado con el seguimiento agregado. A diferencia de los seguimientos basados en reglas, los seguimientos agregados no incluyen propiedades endDate o state, ya que estas propiedades se gestionan dentro de los seguimientos basados en
reglas individuales.

## Edición de seguimientos
{: #editing_tracks}

Se pueden editar seguimientos agregados o de reglas para mejorar
la forma en la que se filtran los datos en el flujo PowerTrack. Cuando se añaden (o modifican) reglas en seguimientos existentes, los mensajes recuperados basados en reglas anteriores continuan en el
seguimiento. Para asegurarse de que los resultados de búsqueda
devuelven datos para el conjunto de reglas más reciente, suprima
el seguimiento y crear un seguimiento nuevo con el conjunto
de reglas previsto.

El ejemplo de [Creación de un seguimiento de reglas](#creating_rule_track){: new.window} ha incluido dos reglas con un ID de seguimiento de `66ff1961-51fe-4475-8bcd-c02f071d6fd1`. Para añadir una nueva regla con un valor "Champions", utilice la operación POST /api/v1/tracks/{track Id} y añada la nueva regla.

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/66ff1961-51fe-4475-8bcd-c02f071d6fd1
HTTP/1.1 Content-Type: application/json
{
    "endDate": "2015-10-03T10:23:00Z",
    "name": "My First Rule Track",
    "type": "Rule",
    "rules": [
        {"value": "Canada"},
        {"value": "sport hockey"},
        {"value": "Champions"}
    ]
}
```
De manera similar, puede eliminar reglas de un
seguimiento existente emitiendo una operación GET
/api/v1/tracks/{track Id} y eliminando valores no deseados.

El ejemplo de [Creación de un seguimiento agregado](#creating_aggregated_track) ha incluido dos seguimientos. Se puede añadir otro seguimiento, con el ID `c4562594-1eeb-4a95-8fac-255428d74bce`, al seguimiento agregado existente emitiendo la siguiente operación:

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/9808fb82-7ea8-4b8e-9cd5-ad653a6dabe6
HTTP/1.1 Content-Type: application/json
{
  "trackIds": [
    {"id": "a22206cd-b72b-4b7d-a5a3-e2d08ce02a88"},
    {"id": "180356df-9a78-491e-b070-f3ffbe00bdf2"},
    {"id": "c4562594-1eeb-4a95-8fac-255428d74bce"}
  ]
}
```

## Supresión de seguimientos
{: #deleting_tracks}

Puede suprimir seguimientos que ya no son necesarios emitiendo una operación DELETE /api/v1/tracks/{trackId}. Esta
acción se puede aplicar tanto a los seguimientos
agregados como a los basados en reglas. Los seguimientos incluidos
en un seguimiento agregado no se pueden suprimir hasta que se
elimine el seguimiento de todos los seguimientos agregados. El siguiente ejemplo demuestra cómo suprimir un seguimiento con el ID `a22206cd-b72b-4b7d-a5a3-e2d08ce02a88`:

```
DELETE https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
```

De manera alternativa, puede detener la recopilación de tuits desde un seguimiento particular cambiando su estado
a Inactivo. En lugar de suprimir el seguimiento, el ejemplo siguiente inhabilita el
seguimiento:

```
POST https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/a22206cd-b72b-4b7d-a5a3-e2d08ce02a88
HTTP/1.1
{
    "state": "Inactive"
}
```

## Búsqueda de tuits
{: #searching_tweets}

Puede emitir una operación GET en la aplicación para recuperar
tuits de cualquier flujo de datos. Por ejemplo, la búsqueda de tuits Decahose se implementa como: `/api/v1/messages/search?q=QUERY&size=NUMBER&from=NUMBER`. Para
los usuarios del Plan de entrada, la búsqueda de tuits desde el flujo
de datos PowerTrack se implementa como: `/api/v1/tracks/{trackId}/messages/search?q=QUERY&size=NUMBER&from=NUMBER`.

El parámetro "size" especifica el número de mensajes que se debe devolver en una respuesta de consulta, mientras que el parámetro "from" indica el mensaje inicial a devolver en el
conjunto de resultados completo. La referencia {trackId} es el identificador exclusivo para un seguimiento específico.
Utilizando cURL, puede buscar en la secuencia Decahose tuits que contengan "IBM" escribiendo:

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/search?q=IBM
```

Emitiendo
la misma consulta en el flujo
PowerTrack debe especificarse como: 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/search?q=IBM
```

El nombre de usuario (`username`) y la contraseña (`password`) son exclusivos para la instancia de servicio y aplicación. Esta información se puede obtener de las variables de entorno **VCAP_SERVICES**. Para obtener más información, consulte [Guía de iniciación a {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

El servicio devuelve respuestas en formato JSON. La tabla
siguiente lista los posibles códigos de respuesta.

| **Código de estado de HTTP** 	| **Motivo**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| Correcto                                                               	|
| 400              	| Faltan propiedades de solicitud de carga útil o las propiedades no son válidas.                   	|
| 401              	| La autenticación ha fallado. Se requieren un nombre de usuario y una contraseña que sean válidos. 	|
| 403              	| Prohibido, límite alcanzado.                                        	|
| 500              	| Se ha producido un error interno.                                  	|

** Tabla 1. Mensajes de respuesta

El cuerpo de la respuesta puede ser como este:

```
{
    "search": {
        "results": 16283624
    },
    "tweets": [{
        "message": {
            ...
            "body": "this is a nice tweet",
            "actor": {
                "followersCount”: 456,
                "displayName": "IBM Tweeter"
                ...
            },
            "cde": {
                "sentiment": {"polarity": "POSITIVE"...
                },
                "author": {"gender": "male"...
                },
                ...
            }
        }
    }]
}
```

La expresión de consulta codificada en el URL recupera los tuits acerca de una película, según un periodo de tiempo especificado y el número de apariciones. Este ejemplo se podría utilizar para determinar el grado de interés o las reacciones que suscita el tráiler de una película.

```
/api/v1/messages/search?q=%28posted:2015-02-01T00:00:00Z%20AND%20%23americansniper%29&size=5 
```

Al descodificar el URL, la sintaxis de consulta y la operación se convierte en "(posted:2015-02-01T00:00:00Z AND #americansniper) &size=5".

## Cómo contar el número de tuits
{: #counting_tweets}

Puede aplicar una operación GET en la aplicación para recuperar el número de tuits que aparecen como coincidencias de una consulta especificada. Las consultas para Decahose se emiten como: `/api/v1/messages/count?q=QUERY`, mientras que las llamadas al flujo PowerTrack utilizan el siguiente formato: 

```
/api/v1/tracks/{trackId}/messages/count?q=QUERY
```

Utilizando cURL, puede encontrar el número de tuits, en
Decahose, que contienen "IBM" utilizando:

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/messages/count?q=IBM
```

La
misma consulta se puede emitir en el origen de datos PowerTrack como: 

```
curl https://<username>:<password>@cdeservice.mybluemix.net:443/api/v1/tracks/{trackId}/messages/count?q=IBM
```

El nombre de usuario (`username`) y la contraseña (`password`) son exclusivos para la instancia de servicio y aplicación. Esta información se puede obtener de las variables de entorno **VCAP_SERVICES**. Para obtener más información, consulte [Guía de iniciación a {{site.data.keyword.twittershort}}](index.html#insights_twitter_overview){: new.window}.

El servicio devuelve respuestas en formato JSON. En la tabla siguiente se indican los mensajes de respuesta posibles.

| **Código de estado de HTTP** 	| **Motivo**                                                           	|
|------------------	|------------------------------------------------------------------	|
| 200              	| Correcto                                                               	|
| 400              	| Faltan propiedades de solicitud de carga útil o las propiedades no son válidas.                   	|
| 401              	| La autenticación ha fallado. Se requieren un nombre de usuario y una contraseña que sean válidos. 	|
| 403              	| Prohibido, límite alcanzado.                                        	|
| 500              	| Se ha producido un error interno.                                  	|

**Tabla 2. Mensajes de respuesta**

El cuerpo de la respuesta puede ser como este:
```
{
  "related": {
      "search": {
          "href": "https://server.bluemix.net/api/v1/messages/search?q=ibm" 
      }
  },
  "search": {
      "results": 21695
  }
}
```

La expresión de consulta siguiente recupera el número de tuits positivos que contienen "IBM" y "Bluemix". En
este caso, los tuits desde Decahose se devuelven en la respuesta.

`.../api/v1/messages/count?q="IBM Bluemix sentiment:positive`

La expresión de consulta siguiente codificada en el URL recupera el número de tuits que contienen "IBM" en un periodo especificado de tiempo. Esta
consulta de ejemplo puede ayudar a indicar la popularidad de un
asunto y determinar si es tendencia. Los tuits del flujo PowerTrack
se devuelven en este ejemplo.

`.../api/v1/tracks/{trackId}/messages/count?q=%28posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND %23IBM%29`

Al descodificar el URL, la sintaxis de consulta y la operación se convierten en "(posted:2015-02-01T00:00:00Z,2015-02-15T00:00:00Z AND #IBM)".
