---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Uso de servicios habilitados para {{site.data.keyword.openwhisk_short}} 
{: #openwhisk_ecosystem}
*Última actualización: 28 de marzo de 2016*

En {{site.data.keyword.openwhisk}}, un catálogo de paquetes le ofrece una forma rápida de mejorar sus apps con prestaciones útiles, y para acceder a servicios externos en el ecosistema. Algunos de los servicios externos que están habilitados para {{site.data.keyword.openwhisk_short}} son Cloudant, The Weather Company, Slack y GitHub.
{: shortdesc}

El catálogo está disponible como paquetes en el espacio de nombres `/whisk.system`. Consulte [Revisión de paquetes](./openwhisk_packages.html#openwhisk_packagedisplay) para obtener información sobre
cómo explorar el catálogo usando la herramienta de línea de mandatos.

Los temas que siguen documentan algunos de los paquetes del catálogo.

## Uso del paquete Cloudant
{: #openwhisk_catalog_cloudant}
El paquete `/whisk.system/cloudant` le permite trabajar con una base de datos Cloudant. Incluye las acciones e información de entrada siguientes.

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | paquete | {{site.data.keyword.Bluemix_notm}}ServiceName, host, username, password, dbname, includeDoc, overwrite | Trabajar con una base de datos Cloudant |
| `/whisk.system/cloudant/read` | acción | dbname, includeDoc, id | Leer un documento de la base de datos |
| `/whisk.system/cloudant/write` | acción | dbname, overwrite, doc | Escribir un documento en la base de datos |
| `/whisk.system/cloudant/changes` | feed | dbname, includeDoc | Activar sucesos desencadenantes para cambios en la BD |

En los temas siguientes se muestra la configuración de una base de datos Cloudant, la configuración de un paquete asociado y el uso de acciones e información de entrada (feeds) en el paquete `/whisk.system/cloudant`.

### Configuración de una base de datos Cloudant en {{site.data.keyword.Bluemix_notm}}

Si utiliza {{site.data.keyword.openwhisk_short}} desde {{site.data.keyword.Bluemix}}, {{site.data.keyword.openwhisk_short}} crea automáticamente enlaces de paquete para sus instancias de servicio
Cloudant de {{site.data.keyword.Bluemix_notm}}. Si no utiliza {{site.data.keyword.openwhisk_short}} y Cloudant desde
{{site.data.keyword.Bluemix_notm}}, continúe en el paso siguiente.

1. Crear una instancia de servicio de Cloudant en su [panel de control](http://console.ng.{{site.data.keyword.Bluemix_notm}}.net) de {{site.data.keyword.Bluemix_notm}}.

  Asegúrese de recordar el nombre de la instancia de servicio y la organización y el espacio de
{{site.data.keyword.Bluemix_notm}} en el que se encuentra.

2. Asegúrese de que su CLI de {{site.data.keyword.openwhisk_short}} esté en el espacio de nombres correspondiente para la organización y
espacio de {{site.data.keyword.Bluemix_notm}} que ha utilizado en el paso anterior.

  ```
  wsk property set --namespace my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space
  ```
  {: pre}

  Si quiere puede utilizar `wsk property set --namespace` para establecer un espacio de nombres de una lista de
aquellos que tenga accesibles.

3. Actualizar los paquetes de su espacio de nombres. La renovación crea automáticamente un enlace de paquete para
la instancia de servicio de Cloudant que ha creado.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  enlaces creados:
  {{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  paquetes
  /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1 private binding
  ```
  {: screen}

  Debe ver el nombre completo del enlace de paquete que corresponde a su instancia de servicio Cloudant de
{{site.data.keyword.Bluemix_notm}}.

4. Compruebe si el enlace de paquete creado anteriormente está configurado con su host de instancia de servicio de
{{site.data.keyword.Bluemix_notm}} de Cloudant y las credenciales.

  ```
  wsk package get /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: pre}
  ```
  ok: got package /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1, projecting parameters
  [
      ...
      {
          "key": "username",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}"
      },
      {
          "key": "host",
          "value": "cdb18832-2bbb-4df2-b7b1-{{site.data.keyword.Bluemix_notm}}.cloudant.com"
      },
      {
          "key": "password",
          "value": "c9088667484a9ac827daf8884972737"
      }
      ...
  ]
  ```
  {: screen}

### Configuración de una base de datos Cloudant fuera de {{site.data.keyword.Bluemix_notm}}

Si no utiliza {{site.data.keyword.openwhisk_short}} en {{site.data.keyword.Bluemix_notm}} o si quiere configurar
su base de datos Cloudant fuera de {{site.data.keyword.Bluemix_notm}}, debe crear manualmente un enlace de paquete
para su cuenta Cloudant. Necesita el nombre de host, nombre de usuario y contraseña de la cuenta Cloudant.

1. Crear un enlace de paquete configurado para su cuenta Cloudant.

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username 'MYUSERNAME' -p password 'MYPASSWORD' -p host 'MYCLOUDANTACCOUNT.cloudant.com'
  ```
  {: pre}

2. Comprobar que el enlace de paquete existe.

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myCloudant private binding
  ```
  {: screen}


### Atender a cambios en una base de datos Cloudant

Puede utilizar la información de entrada `changes` para configurar un servicio para que active un desencadenante
para cada cambio de su base de datos Cloudant.

1. Crear un desencadenante con la información de entrada `changes` en el enlace de paquete que ha
creado anteriormente. Asegúrese de sustituir `/myNamespace/myCloudant` por su nombre de paquete.

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb --param includeDocs true
  ```
  {: pre}
  ```
  ok: created trigger feed myCloudantTrigger
  ```
  {: screen}

2. Sondeo de activaciones.

  ```
  wsk activation poll
  ```
  {: pre}

3. En su panel de control de Cloudant, modifique un documento existente o cree uno nuevo.

4. Observe las nuevas activaciones para el desencadenante `myCloudantTrigger` en busca de los cambios de documento.

**Nota**: si no detecta nuevas activaciones, consulte las secciones siguientes sobre la lectura y escritura
en una base de datos Cloudant. La prueba de los pasos de lectura y escritura más abajo ayudarán a comprobar que sus credenciales de Cloudant son correctas.

Ahora puede crear reglas y asociarlas a acciones para reaccionar a actualizaciones de documento.

El contenido de los sucesos generados depende del valor del parámetro `includeDocs` al crear el desencadenante. Si se
establece en true, cada suceso desencadenante que se activa incluye el documento Cloudant modificado. Por ejemplo, pensemos en el
documento modificado siguiente:

  ```
  {
    "_id": "6ca436c44074c4c2aa6a40c9a188b348",
    "_rev": "3-bc4960fc13aa368afca8c8427a1c18a8",
    "name": "Heisenberg"
  }
  ```
  {: screen}

El código en este ejemplo genera un suceso desencadenante con los parámetros `_id`, `_rev` y `name` correspondientes. De hecho, la representación JSON del suceso desencadenante es idéntica al documento.

De lo contrario, si `includeDocs` es falso, los sucesos incluyen los parámetros siguientes:

- `id`: el id. del documento
- `seq`: el identificador de secuencia generado por Cloudant.
- `changes`: una matriz de objetos, cada uno de los cuales tiene un campo `rev` que contiene
el id de revisión del documento.

La representación JSON del suceso desencadenante es según se indica a continuación:

  ```
  {
      "id": "6ca436c44074c4c2aa6a40c9a188b348",
      "seq": "2-g1AAAAL9aJyV-GJCaEuqx4-BktQkYp_dmIfC",
      "changes": [
          {
              "rev": "2-da3f80848a480379486fb4a2ad98fa16"
          }
      ]
  }
  ```


### Escritura en una base de datos Cloudant

Puede utilizar una acción para almacenar un documento en una base de datos Cloudant llamada `testdb`. Asegúrese de que
esta base de datos exista en su cuenta Cloudant.

1. Almacenar un documento usando la acción `write` en el enlace de paquete que ha creado anteriormente. Asegúrese de sustituir
`/myNamespace/myCloudant` por el nombre de paquete.

  ```
  wsk action invoke /myNamespace/myCoudant/write --blocking --result --param dbname testdb --param doc '{"_id":"heisenberg", "name":"Walter White"}'
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCoudant/write with id 62bf696b38464fd1bcaff216a68b8287
  response:
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```
  {: screen}

2. Compruebe que el documento exista, buscándolo en su panel de control Cloudant.

  El URL de panel de control para la base de datos `testdb` es parecido a: `https://MYCLOUDANTACCOUNT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100`.


### Leer de una base de datos Cloudant

Puede utilizar una acción para obtener un documento de una base de datos Cloudant llamada `testdb`. Asegúrese de que
esta base de datos exista en su cuenta Cloudant.

1. Obtener un documento usando la acción `read` en el enlace de paquete que ha creado anteriormente. Asegúrese de sustituir
`/myNamespace/myCloudant` por el nombre de paquete.

  ```
  wsk action invoke /myNamespace/myCoudant/read --blocking --result --param dbname testdb --param id heisenberg
  ```
  {: pre}
  ```
  {
    "_id": "heisenberg",
    "_rev": "1-9a94fb93abc88d8863781a248f63c8c3"
    "name": "Walter White"
  }
  ```
  {: screen}


## Uso del paquete Alarm
{: #openwhisk_catalog_alarm}

El paquete `/whisk.system/alarms` se puede utilizar para activar un desencadenante con una frecuencia especificada. Esto es útil
para configurar trabajos o tareas recurrentes, como la invocación de una acción de copia de seguridad del sistema cada hora.

El paquete incluye la información de entrada siguiente.

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | paquete | - | Utilidad de alarmas y periodicidad |
| `/whisk.system/alarms/alarm` | feed | cron, trigger_payload, maxTriggers | Activar suceso desencadenante de forma periódica |


### Activación periódica de un suceso desencadenante

La información de entrada `/whisk.system/alarms/alarm` configura un servicio de alarma para activar un suceso desencadenante
con una frecuencia especificada. Los parámetros son como se indica a continuación:

- `cron`: una serie, basada en la sintaxis crontab de UNIX, que indica cuándo activar el desencadenante en Hora Universal Coordinada (UTC). La serie es una
secuencia de seis campos separados por espacios: `X X X X X X `. Para obtener más detalles sobre cómo utilizar sintaxis cron, consulte: https://github.com/ncb000gt/node-cron.

- `trigger_payload`: el valor de este parámetro pasa a ser el contenido del desencadenante cada vez que se activa
el desencadenante.

- `maxTriggers`: dejar de activar desencadenantes cuando se alcanza este límite. El valor predeterminado es 1000.

A continuación se muestra un ejemplo de la creación de un desencadenante que se activará una vez cada 20 segundos con
los valores `name` y `place` en el suceso desencadenante.

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron '/20 * * * * *' --param trigger_payload '{"name":"Odin","place":"Asgard"}'
  ```
  {: pre}

Cada suceso generado incluirá como parámetros las propiedades especificadas en el valor `trigger_payload`. En este caso,
cada suceso desencadenante tendrá los parámetros `name=Odin` y `place=Asgard`.


## Uso del paquete Weather
{: #openwhisk_catalog_weather}

El paquete `/whisk.system/weather` ofrece una forma cómoda de invocar la API de The Weather Company.

El paquete incluye la acción siguiente.

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/weather` | paquete | apiKey | Servicios de The Weather Company |
| `/whisk.system/weather/forecast` | acción | apiKey, latitude, longitude | Previsión a 10 días de Weather.com |

Aunque no es obligatorio, se recomienda crear un enlace de paquete con el valor `apiKey`. Así, no necesita especificar
la clave cada vez que invoque las acciones del paquete.

### Obtención de la previsión meteorológica para una ubicación

La acción `/whisk.system/weather/forecast` devuelve una previsión meteorológica de 10 días para un lugar,
invocando la API de The Weather Company. Los parámetros son según se indica a continuación:

- `apiKey`: una clave de API para The Weather Company que tiene autorización para invocar la API de previsión meteorológica a 10 días vista
- `latitude`: la coordenada de latitud de la ubicación
- `longitude`: la coordenada de longitud de la ubicación

A continuación se muestra un ejemplo de la creación de un enlace de paquete y luego la obtención de una previsión a 10 días.

1. Crear un enlace de paquete con su clave de API.

  ```
  wsk package bind /whisk.system/weather myWeather --param apiKey 'MY_WEATHER_API'
  ```
  {: pre}

2. Invocar la acción `forecast` en su enlace de paquete para obtener la previsión meteorológica.

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude '43.7' --param longitude '-79.4'
  ```
  {: pre}

  ```
  {
      "forecasts": [
          {
              "dow": "Wednesday",
              "max_temp": -1,
              "min_temp": -16,
              "narrative": "Chance of a few snow showers. Highs -2 to 0C and lows -17 to -15C.",
              ...
          },
          {
              "class": "fod_long_range_daily",
              "dow": "Thursday",
              "max_temp": -4,
              "min_temp": -8,
              "narrative": "Mostly sunny. Highs -5 to -3C and lows -9 to -7C.",
              ...
          },
          ...
      ],
  }
  ```
  {: screen}


## Uso del paquete Watson
{: #openwhisk_catalog_watson}

El paquete `/whisk.system/watson` ofrece una forma cómoda de invocar distintas API de Watson.

El paquete incluye las acciones siguientes.

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/watson` | paquete | usuario, contraseña | Acciones para las API de analíticas de Watson |
| `/whisk.system/watson/translate` | acción | translateFrom, translateTo, translateParam, username, password | Traducir texto |
| `/whisk.system/watson/languageId` | acción | payload, username, password | Identificar idioma |

Aunque no es obligatorio, se recomienda crear un enlace de paquete con los valores `username` and `password`. Así, no necesita especificar
estas credenciales cada vez que invoque las acciones del paquete.

### Traducción de texto

La acción `/whisk.system/watson/translate` traduce texto de un idioma a otro. Los parámetros son según se indica a continuación:

- `username`: nombre de usuario de la API de Watson
- `password`: contraseña de la API de Watson
- `translateParam`: el  parámetro de entrada a traducir. Por ejemplo, si es `translateParam=payload`, el valor del parámetro `payload` que se pasa a la acción, se traduce
- `translateFrom`: un código de dos dígitos del lenguaje origen
- `translateTo`: un código de dos dígitos del idioma de destino.

A continuación se muestra un ejemplo de la creación de un enlace de paquete y la traducción de algún texto.

1. Crear un enlace de paquete con sus credenciales de Watson.

  ```
  wsk package bind /whisk.system/watson myWatson --param username 'MY_WATSON_USERNAME' --param password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. Invocar la acción `translate` en su enlace de paquete para traducir algún texto de inglés a español.

  ```
  wsk action invoke myWatson/translate --blocking --result --param payload 'Blue skies ahead' --param translateParam 'payload' --param translateFrom 'en' --param translateTo 'es'
  ```
  {: pre}

  ```
  {
      "payload": "Se esperan cielos despejados"
  }
  ```
  {: screen}


### Identificación del idioma de un texto

La acción `/whisk.system/watson/languageId` identifica el idioma de un texto. Los parámetros son según se indica a continuación:

- `username`: nombre de usuario de la API de Watson
- `password`: contraseña de la API de Watson
- `payload`: el texto a identificar.

A continuación se muestra un ejemplo de la creación de un enlace de paquete y la identificación del idioma de un texto.

1. Crear un enlace de paquete con sus credenciales de Watson.

  ```
  wsk package bind /whisk.system/watson myWatson -p username 'MY_WATSON_USERNAME' -p password 'MY_WATSON_PASSWORD'
  ```
  {: pre}

2. Invocar la acción `languageId` en su enlace de paquete para identificar el idioma.

  ```
  wsk action invoke myWatson/languageId --blocking --result --param payload 'Se esperan cielos despejados'
  ```
  {: pre}
  ```
  {
    "payload": "Se esperan cielos despejados",
    "language": "es",
    "confidence": 0.710906
  }
  ```
  {: screen}


## Uso del paquete Slack
{: #openwhisk_catalog_slack}

El paquete `/whisk.system/slack` ofrece una forma cómoda de utilizar las [API de Slack](https://api.slack.com/).

El paquete incluye las acciones siguientes:

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/slack` | paquete | url, channel, username | Interactuar con la API de Slack. |
| `/whisk.system/slack/post` | acción | text, url, channel, username | Publicar un mensaje en un canal de Slack |

Aunque no es obligatorio, se recomienda crear un enlace de paquete con los valores `username`, `url` y 'channel'. Con enlace, no necesita especificar los valores cada vez que invoca la acción en el paquete.

### Publicación de un mensaje en un canal de Slack

La acción `/whisk.system/slack/post` publica un mensaje en un canal de Slack especificado. Los parámetros son según se indica a continuación:

- `url`: el URL de webhook de Slack.
- `channel`: el canal de Slack en el que publicar el mensaje.
- `username`: el nombre con el que publicar el mensaje.
- `text`: un mensaje a publicar.

A continuación se muestra un ejemplo sobre la configuración de Slack, creación de un enlace de paquete y publicación de un mensaje en un canal.

1. Configurar un [webhook de entrada](https://api.slack.com/incoming-webhooks) de Slack para su equipo.

  Tras configurar Slack, debe obtener un URL de Webhook parecido a
`https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Lo necesitará en el paso siguiente.

2. Crear un enlace de paquete con sus credenciales de Slack, el canal en el que quiera publicar y el nombre de usuario con el que publicar.

  ```
  wsk package bind /whisk.system/slack mySlack --param url 'https://hooks.slack.com/services/...' --param username 'Bob' --param channel '#MySlackChannel'
  ```
  {: pre}

3. Invocar la acción `post` en su enlace de paquete para publicar un mensaje en su canal Slack.

  ```
  wsk action invoke mySlack/post --blocking --result --param text 'Hello from OpenWhisk!'
  ```
  {: pre}


## Uso del paquete GitHub
{: #openwhisk_catalog_github}

El paquete `/whisk.system/github` ofrece una forma cómoda de utilizar las [API de GitHub](https://developer.github.com/).

El paquete incluye la información de entrada siguiente:

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/github` | paquete | username, repository, accessToken | Interactuar con la API de GitHub |
| `/whisk.system/github/webhook` | feed | events, username, repository, accessToken | Activar sucesos desencadenantes en caso de actividad de GitHub |

Aunque no es obligatorio, se recomienda crear un enlace de paquete con los valores `username`, `repository` y `accessToken`.  Con enlace, no necesita especificar los valores cada vez que use la información de entrada en el paquete.

### Activación de un suceso desencadenante con actividad GitHub

La información de entrada `/whisk.system/github/webhook` configura un servicio para activar un desencadenante
cuando haya actividad en el repositorio de GitHub especificado. Los parámetros son según se indica a continuación:

- `username`: el nombre de usuario del repositorio GitHub.
- `repository`: el repositorio GitHub.
- `accessToken`: su señal de acceso personal de GitHub. Cuando [cree su
señal](https://github.com/settings/tokens), asegúrese de seleccionar los ámbitos repo:status y public_repo. Además, asegúrese de que no tiene webhooks ya definidos en su repositorio.
- `events`: el [tipo de actividad GitHub](https://developer.github.com/v3/activity/events/types/) de interés.

A continuación se muestra un ejemplo de creación de un desencadenante que se activará cada vez que haya una nueva confirmación con un
repositorio GitHub.

1. Generar una [señal de acceso personal](https://github.com/settings/tokens) de GitHub.

  La señal de acceso se usará en el paso siguiente.


2. Crear un enlace de paquete configurado para su repositorio de GitHub y con su señal de acceso.

  ```
  wsk package bind /whisk.system/github myGit --param username myGitUser --param repository myGitRepo --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}

3. Crear un desencadenante para el tipo de suceso `push` de GitHub usando su información de entrada de `myGit/webhook`.

  ```
  wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}

