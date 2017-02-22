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

# Utilización de servicios de {{site.data.keyword.Bluemix_notm}} habilitados para {{site.data.keyword.openwhisk_short}}
{: #openwhisk_ecosystem}

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
| `/whisk.system/cloudant` | paquete | {{site.data.keyword.Bluemix_notm}}ServiceName, host, username, password, dbname, overwrite | Trabajar con una base de datos Cloudant |
| `/whisk.system/cloudant/read` | acción | dbname, includeDoc, id | Leer un documento de la base de datos |
| `/whisk.system/cloudant/write` | acción | dbname, overwrite, doc | Escribir un documento en la base de datos |
| `/whisk.system/cloudant/changes` | feed | dbname, maxTriggers | Activar sucesos desencadenantes para cambios en la BD |

En los temas siguientes se muestra la configuración de una base de datos Cloudant, la configuración de un paquete asociado y el uso de acciones e información de entrada (feeds) en el paquete `/whisk.system/cloudant`.

### Configuración de una base de datos Cloudant en {{site.data.keyword.Bluemix_notm}}
{: #openwhisk_catalog_cloudant_in}

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
  created bindings:
  {{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /my{{site.data.keyword.Bluemix_notm}}Org_my{{site.data.keyword.Bluemix_notm}}Space/{{site.data.keyword.Bluemix_notm}}_testCloudant_Credentials-1 private binding
  ```
  {: screen}

  Verá el nombre completo del enlace de paquete que corresponde a su instancia de servicio Cloudant de
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
{: #openwhisk_catalog_cloudant_outside}

Si no utiliza {{site.data.keyword.openwhisk_short}} en {{site.data.keyword.Bluemix_notm}} o si quiere configurar
su base de datos Cloudant fuera de {{site.data.keyword.Bluemix_notm}}, debe crear manualmente un enlace de paquete
para su cuenta Cloudant. Necesita el nombre de host, nombre de usuario y contraseña de la cuenta Cloudant.

1. Crear un enlace de paquete configurado para su cuenta Cloudant.

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username MYUSERNAME -p password MYPASSWORD -p host MYCLOUDANTACCOUNT.cloudant.com
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
{: #openwhisk_catalog_cloudant_listen}

Puede utilizar la información de entrada `changes` para configurar un servicio para que active un desencadenante
para cada cambio de su base de datos Cloudant. Los parámetros son según se indica a continuación:

- `dbname`: nombre de la base de datos Cloudant.
- `maxTriggers`: dejar de activar desencadenantes cuando se alcanza este límite. El valor predeterminado es 1000. Puede establecerlo en un máximo de 10.000. Si intenta establecerlo en más de 10.000, se rechazará la solicitud.

1. Crear un desencadenante con la información de entrada `changes` en el enlace de paquete que ha
creado anteriormente. Asegúrese de sustituir
`/myNamespace/myCloudant` por el nombre de paquete.

  ```
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
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
en una base de datos Cloudant. Probar los siguientes pasos de lectura y escritura le ayudará a comprobar si sus credenciales de Cloudant son correctas.

Ahora puede crear reglas y asociarlas a acciones para reaccionar a actualizaciones de documento.

El contenido de los sucesos generados tiene los siguientes parámetros:

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
{: #openwhisk_catalog_cloudant_write}

Puede utilizar una acción para almacenar un documento en una base de datos Cloudant llamada `testdb`. Asegúrese de que
esta base de datos exista en su cuenta Cloudant.

1. Almacenar un documento usando la acción `write` en el enlace de paquete que ha creado anteriormente. Asegúrese de sustituir
`/myNamespace/myCloudant` por el nombre de paquete.

  ```
  wsk action invoke /myNamespace/myCloudant/write --blocking --result --param dbname testdb --param doc "{\"_id\":\"heisenberg\",\"name\":\"Walter White\"}"
  ```
  {: pre}
  ```
  ok: invoked /myNamespace/myCloudant/write with id 62bf696b38464fd1bcaff216a68b8287
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
{: #openwhisk_catalog_cloudant_read}

Puede utilizar una acción para obtener un documento de una base de datos Cloudant llamada `testdb`. Asegúrese de que
esta base de datos exista en su cuenta Cloudant.

1. Obtener un documento usando la acción `read` en el enlace de paquete que ha creado anteriormente. Asegúrese de sustituir
`/myNamespace/myCloudant` por el nombre de paquete.

  ```
  wsk action invoke /myNamespace/myCloudant/read --blocking --result --param dbname testdb --param id heisenberg
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

### Utilización de una secuencia de acciones y de un desencadenante de cambios para procesar un documento desde una base de datos Cloudant

Puede utilizar una secuencia de acciones en una regla para captar y procesar el documento asociado a un suceso de cambio Cloudant.

A continuación se muestra un código de ejemplo de una acción que maneja un documento:
```
function main(doc){
  return { "isWalter:" : doc.name === "Walter White"};
}
```
{: codeblock}

Cree la acción para procesar el documento desde Cloudant:
```
wsk action create myAction myAction.js
```
{: pre}

Para leer un documento desde la base de datos, puede utilizar la acción `read` del paquete de Cloudant.
La acción `read` puede estar compuesta de `myAction` para crear una secuencia de acciones. 
```
wsk action create sequenceAction --sequence /myNamespace/myCloudant/read,myAction
```
{: pre}

Se puede utilizar la acción `sequenceAction` en una regla que active la acción sobre nuevos sucesos de desencadenante de Cloudant. 
```
wsk rule create myRule myCloudantTrigger sequenceAction
```
{: pre}

**Nota**: el desencadenante de `cambios` de Cloudant utilizado para dar soporte al parámetro `includeDoc` ya no recibe soporte. Tendrá que volver a crear desencadenantes creados anteriormente con `includeDoc`.
Siga estos pasos para volver a crear el desencadenante:

  ```
  wsk trigger delete myCloudantTrigger
  wsk trigger create myCloudantTrigger --feed /myNamespace/myCloudant/changes --param dbname testdb
  ```
  {: pre}

  Puede utilizar el ejemplo anterior para crear una secuencia de acciones para leer el documento modificado e invocar las acciones existentes.
  No olvide inhabilitar las reglas que ya no sean válidas y crear nuevas utilizando el patrón de la secuencia de acciones. 

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
{: #openwhisk_catalog_alarm_fire}

La información de entrada `/whisk.system/alarms/alarm` configura un servicio de alarma para activar un suceso desencadenante
con una frecuencia especificada. Los parámetros son según se indica a continuación:

- `cron`: una serie, basada en la sintaxis crontab de UNIX, que indica cuándo activar el desencadenante en Hora Universal Coordinada (UTC). La serie es una secuencia de cinco campos separados por espacios: `X X X X X`.
Para obtener más detalles sobre cómo utilizar sintaxis cron, consulte: http://crontab.org. A continuación se muestran algunos ejemplos de la frecuencia indicada por la serie:

  - `* * * * *`: cada minuto en punto.
  - `0 * * * *`: a cada hora en punto.
  - `0 */2 * * *`: cada 2 horas (p. ej. 02:00:00, 04:00:00, ...)
  - `0 9 8 * *`: a las 9:00:00AM (UTC) en el octavo día de cada mes

- `trigger_payload`: el valor de este parámetro pasa a ser el contenido del desencadenante cada vez que se activa
el desencadenante.

- `maxTriggers`: dejar de activar desencadenantes cuando se alcanza este límite. El valor predeterminado es 1000. Puede establecerlo en un máximo de 10.000. Si intenta establecerlo en más de 10.000, se rechazará la solicitud.

A continuación se muestra un ejemplo de la creación de un desencadenante que se activará una vez cada 2 minutos con los valores `name` y `place` en el suceso desencadenante.

  ```
  wsk trigger create periodic --feed /whisk.system/alarms/alarm --param cron "*/2 * * * *" --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

Cada suceso generado incluirá como parámetros las propiedades especificadas en el valor `trigger_payload`. En este caso,
cada suceso desencadenante tendrá los parámetros `name=Odin` y `place=Asgard`.

**Nota**: el parámetro `cron` también da soporte a una sintaxis personalizada de seis campos, donde el primer campo representa segundos.
Para obtener más detalles sobre cómo utilizar esta sintaxis cron personalizada, consulte: https://github.com/ncb000gt/node-cron.
A continuación se muestra un ejemplo que utiliza la notación de seis campos:
  - `*/30 * * * * *`: cada treinta segundos.

## Uso del paquete Weather
{: #openwhisk_catalog_weather}

El paquete `/whisk.system/weather` ofrece una forma cómoda de invocar la API de Weather Company Data para IBM Bluemix.

El paquete incluye la acción siguiente.

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/weather` | paquete | usuario, contraseña | Servicios de la API de Weather Company Data para IBM Bluemix  |
| `/whisk.system/weather/forecast` | acción | latitude, longitude, timePeriod | Previsión para el periodo de tiempo indicado|

Se recomienda la creación de un enlace de paquete con los valores de `username` and `password`. Así, no necesita especificar las credenciales cada vez que invoque las acciones del paquete.

### Obtención de la previsión meteorológica para una ubicación
{: #openwhisk_catalog_weather_forecast}

La acción `/whisk.system/weather/forecast` devuelve una previsión meteorológica para un lugar,
invocando la API de The Weather Company. Los parámetros son según se indica a continuación:

- `username`: nombre de usuario de The Weather Company Data para IBM Bluemix que tiene autorización para invocar la API de previsión meteorológica.
- `password`: contraseña de The Weather Company Data para IBM Bluemix que tiene autorización para invocar la API de previsión meteorológica.
- `latitude`: la coordenada de latitud de la ubicación.
- `longitude`: la coordenada de longitud de la ubicación.
- `timeperiod`: periodo de tiempo de la previsión. Las opciones válidas son '10day' - (predeterminada) Devuelve una previsión diaria para 10 días, '48hour' - Devuelve una previsión cada hora para 2 días, 'current' - Devuelve las condiciones meteorológicas actuales, 'timeseries' - Devuelve ambas observaciones actuales y observaciones pasadas para un máximo de 24 horas a partir de la fecha y hora actuales.


A continuación se muestra un ejemplo de la creación de un enlace de paquete y luego la obtención de una previsión a 10 días.

1. Crear un enlace de paquete con su clave de API.

  ```
  wsk package bind /whisk.system/weather myWeather --param username MY_USERNAME --param password MY_PASSWORD
  ```
  {: pre}

2. Invocar la acción `forecast` en su enlace de paquete para obtener la previsión meteorológica.

  ```
  wsk action invoke myWeather/forecast --blocking --result --param latitude 43.7 --param longitude -79.4
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


## Uso de los paquetes Watson
{: #openwhisk_catalog_watson}

Los paquetes Watson ofrecen una forma cómoda de invocar distintas API de Watson.

Se proporcionan los siguientes paquetes Watson:

| Paquete | Descripción |
| --- | --- |
| `/whisk.system/watson-translator`   | Paquete de traducción de texto e identificación de idioma |
| `/whisk.system/watson-textToSpeech` | Paquete para convertir texto en habla |
| `/whisk.system/watson-speechToText` | Paquete para convertir habla en texto |

**Nota**: el paquete `/whisk.system/watson` actualmente está en desuso, migre a los nuevos paquetes mencionados anteriormente, las nuevas acciones proporcionan la misma interfaz.

### Uso del paquete de Watson Translator

El paquete `/whisk.system/watson-translator` ofrece una forma cómoda de invocar API Watson a convertir.

El paquete incluye las acciones siguientes.

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/watson-translator` | paquete | usuario, contraseña | Paquete de traducción de texto e identificación de idioma  |
| `/whisk.system/watson-translator/translator` | acción | payload, translateFrom, translateTo, translateParam, username, password | Traducir texto |
| `/whisk.system/watson-translator/languageId` | acción | payload, username, password | Identificar idioma |

**Nota**: el paquete `/whisk.system/watson` está en desuso, incluidas las acciones `/whisk.system/watson/translate` y `/whisk.system/watson/languageId`.

#### Configuración del paquete de Watson Translator en Bluemix

Si utiliza OpenWhisk desde Bluemix, OpenWhisk crea automáticamente enlaces de paquete para sus instancias de servicio de Bluemix Watson.

1. Cree una instancia de servicio de Watson Translator en su [panel de control](http://console.ng.Bluemix.net) de Bluemix.

  Asegúrese de recordar el nombre de la instancia de servicio y la organización y el espacio de Bluemix en el que se encuentra.

2. Asegúrese de que su CLI de OpenWhisk esté en el espacio de nombres correspondiente para la organización y espacio de Bluemix que ha utilizado en el paso anterior.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  Si quiere puede utilizar `wsk property set --namespace` para establecer un espacio de nombres de una lista de
aquellos que tenga accesibles.

3. Actualizar los paquetes de su espacio de nombres. La renovación crea automáticamente un enlace de paquete para la instancia de servicio de Watson que ha creado.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_Translator_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_Translator_Credentials-1 private
  ```
  {: screen}


#### Configuración de un paquete de Watson Translator fuera de Bluemix

Si no utiliza OpenWhisk en Bluemix o si quiere configurar Watson Translator fuera de Bluemix, debe crear manualmente un enlace de paquete para el servicio de Watson Translator. Necesita el nombre de usuario del servicio de Watson Translator y la contraseña.

- Cree un enlace de paquete configurado para el servicio de Watson Translator.

  ```
  wsk package bind /whisk.system/watson-translator myWatsonTranslator -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### Traducción de texto
{: #openwhisk_catalog_watson_translate}

La acción `/whisk.system/watson-translator/translator` traduce texto de un idioma a otro. Los parámetros son según se indica a continuación:

- `username`: el nombre de usuario de la API de Watson.
- `password`: contraseña de la API de Watson.
- `payload`: el texto que se debe traducir.
- `translateParam`: el parámetro de entrada que indica el texto a traducir. Por ejemplo, si es `translateParam=payload`, el valor del parámetro `payload` que se pasa a la acción, se traduce.
- ` translateFrom`: un código de dos dígitos del lenguaje origen.
- `translateTo`: un código de dos dígitos del idioma de destino.

- Invoque la acción `translator` en su enlace de paquete para traducir algún texto de inglés a español.

  ```
  wsk action invoke myWatsonTranslator/translator --blocking --result --param payload 'Blue skies ahead' --param translateFrom 'en' --param translateTo 'fr'
  ```
  {: pre}

  ```
  {
      "payload": "Se esperan cielos despejados"
  }
  ```
  {: screen}


#### Identificación del idioma de un texto
{: #openwhisk_catalog_watson_identifylang}

La acción `/whisk.system/watson-translator/languageId` identifica el idioma de algún texto. Los parámetros son según se indica a continuación:

- `username`: el nombre de usuario de la API de Watson.
- `password`: contraseña de la API de Watson.
- `payload`: el texto a identificar.

- Invocar la acción `languageId` en su enlace de paquete para identificar el idioma.

  ```
  wsk action invoke myWatsonTranslator/languageId --blocking --result --param payload 'Ciel bleu a venir'
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


### Uso del paquete Watson Text to Speech
{: #openwhisk_catalog_watson_texttospeech}

El paquete `/whisk.system/watson-textToSpeech` ofrece una forma cómoda de invocar API Watson para convertir el texto a voz.

El paquete incluye las acciones siguientes.

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/watson-textToSpeech` | paquete | usuario, contraseña | Paquete para convertir texto en habla |
| `/whisk.system/watson-textToSpeech/textToSpeech` | acción | payload, voice, accept, encoding, username, password | Convertir texto en audio |

**Nota**: el paquete `/whisk.system/watson` está en desuso, incluida la acción `/whisk.system/watson/textToSpeech`.

#### Configuración del paquete Watson Text to Speech en Bluemix

Si utiliza OpenWhisk desde Bluemix, OpenWhisk crea automáticamente enlaces de paquete para sus instancias de servicio de Bluemix Watson.

1. Cree una instancia de servicio Watson Text to Speech en el [panel de control](http://console.ng.Bluemix.net) de Bluemix.

  Asegúrese de recordar el nombre de la instancia de servicio y la organización y el espacio de Bluemix en el que se encuentra.

2. Asegúrese de que su CLI de OpenWhisk esté en el espacio de nombres correspondiente para la organización y espacio de Bluemix que ha utilizado en el paso anterior.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  Si quiere puede utilizar `wsk property set --namespace` para establecer un espacio de nombres de una lista de
aquellos que tenga accesibles.

3. Actualizar los paquetes de su espacio de nombres. La renovación crea automáticamente un enlace de paquete para la instancia de servicio de Watson que ha creado.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_TextToSpeech_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_TextToSpeec_Credentials-1 private
  ```
  {: screen}


#### Configuración de un paquete Watson Text to Speech fuera de Bluemix

Si no utiliza OpenWhisk en Bluemix o si quiere configurar Watson Text to Speech fuera de Bluemix, debe crear manualmente un enlace de paquete para el servicio de Watson Text to Speech. Necesita el nombre de usuario del servicio de Watson Text to Speech y la contraseña.

- Cree un enlace de paquete configurado para el servicio de Watson Speech to Text.

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonTextToSpeech -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### Conversión de texto a habla
{: #openwhisk_catalog_watson_speechtotext}

La acción `/whisk.system/watson-speechToText/textToSpeech` convierte texto en un texto hablado. Los parámetros son según se indica a continuación:

- `username`: el nombre de usuario de la API de Watson.
- `password`: contraseña de la API de Watson.
- `payload`: texto que se debe convertir en habla.
- `voice`: voz de la persona que habla.
- `accept`: formato del archivo de audio.
- `encoding`: codificación de los datos binarios del habla.


- Invoque la acción `textToSpeech` en el enlace del paquete para convertir el texto.

  ```
  wsk action invoke myWatsonTextToSpeech/textToSpeech --blocking --result --param payload 'Hey.' --param voice 'en-US_MichaelVoice' --param accept 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
    "payload": "<base64 encoding of a .wav file>"
  }
  ```
  {: screen}


### Uso del paquete Watson Speech to Text
{: #openwhisk_catalog_watson_speechtotext}

El paquete `/whisk.system/watson-speechToText` ofrece una forma cómoda de invocar API Watson para convertir la voz a texto.

El paquete incluye las acciones siguientes.

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/watson-speechToText` | paquete | usuario, contraseña | Paquete para convertir habla en texto |
| `/whisk.system/watson-speechToText/speechToText` | acción | payload, content_type, encoding, username, password, continuous, inactivity_timeout, interim_results, keywords, keywords_threshold, max_alternatives, model, timestamps, watson-token, word_alternatives_threshold, word_confidence, X-Watson-Learning-Opt-Out | Convertir audio en texto |

**Nota**: el paquete `/whisk.system/watson` está en desuso, incluida la acción `/whisk.system/watson/speechToText`.

#### Configuración del paquete Watson Speech to Text en Bluemix

Si utiliza OpenWhisk desde Bluemix, OpenWhisk crea automáticamente enlaces de paquete para sus instancias de servicio de Bluemix Watson.

1. Cree una instancia de servicio de Watson Speech to Text en el [panel de control](http://console.ng.Bluemix.net) de Bluemix.

  Asegúrese de recordar el nombre de la instancia de servicio y la organización y el espacio de Bluemix en el que se encuentra.

2. Asegúrese de que su CLI de OpenWhisk esté en el espacio de nombres correspondiente para la organización y espacio de Bluemix que ha utilizado en el paso anterior.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  Si quiere puede utilizar `wsk property set --namespace` para establecer un espacio de nombres de una lista de
aquellos que tenga accesibles.

3. Actualizar los paquetes de su espacio de nombres. La renovación crea automáticamente un enlace de paquete para la instancia de servicio de Watson que ha creado.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Watson_SpeechToText_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Watson_SpeechToText_Credentials-1 private
  ```
  {: screen}


#### Configuración de un paquete Watson Speech to Text fuera de Bluemix

Si no utiliza OpenWhisk en Bluemix o si quiere configurar Watson Speech to Text fuera de Bluemix, debe crear manualmente un enlace de paquete para el servicio de Watson Speech to Text. Necesita el nombre de usuario del servicio de Watson Speech to Text y la contraseña.

- Cree un enlace de paquete configurado para el servicio de Watson Speech to Text.

  ```
  wsk package bind /whisk.system/watson-speechToText myWatsonSpeechToText -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


#### Conversión de habla a texto

La acción `/whisk.system/watson-speechToText/speechToText` convierte el audio en texto. Los parámetros son según se indica a continuación:

- `username`: el nombre de usuario de la API de Watson.
- `password`: contraseña de la API de Watson.
- `payload`: datos binarios codificados del habla para convertir en texto.
- `content_type`: tipo MIME del audio.
- `encoding`: codificación de los datos binarios del habla.
- `continuous`: indica si se devuelven varios resultados finales que representan frases consecutivas separadas por pausas prolongadas.
- `inactivity_timeout`: tiempo, en segundos, después del cual, si solo se detecta silencio en el audio enviado, la conexión se cierra.
- `interim_results`: indica si el servicio debe devolver resultados temporales.
- `keywords`: lista de palabras clave para detectar en el audio.
- `keywords_threshold`: valor de confianza que se encuentra en el límite inferior para detectar una palabra clave.
- `max_alternatives`: número máximo de transcripciones alternativas que deben devolverse.
- `model`: identificador del modelo que debe utilizarse para la solicitud de reconocimiento.
- `timestamps`: indica si se devuelve la alineación de tiempo para cada palabra.
- `watson-token`: proporciona un elemento de autenticación para el servicio como alternativa para proporcionar credenciales del servicio.
- `word_alternatives_threshold`: valor de confianza que se encuentra en el límite inferior para identificar una hipótesis como posible alternativa de palabra.
- `word_confidence`: indica si se devuelve para cada palabra una medida de confianza entre 0 y 1.
- `X-Watson-Learning-Opt-Out`: indica si se debe renunciar a la recopilación de datos para la llamada.
 

- Invoque la acción `speechToText` en el enlace de paquete para convertir el audio codificado.

  ```
  wsk action invoke myWatsonSpeechToText/speechToText --blocking --result --param payload <base64 encoding of a .wav file> --param content_type 'audio/wav' --param encoding 'base64'
  ```
  {: pre}
  ```
  {
    "data": "Hello Watson"
  }
  ```
  {: screen}
 
 
## Utilización del paquete Message Hub
{: #openwhisk_catalog_message_hub}

Este paquete le permite crear desencadenantes que reaccionan cuando se publica un mensaje en una instancia del servicio [Message Hub](https://developer.ibm.com/messaging/message-hub/) en Bluemix.

### Creación de un desencadenante que escuche una instancia de Message Hub
{: #openwhisk_catalog_message_hub_trigger}
Para crear un desencadenante que reaccione cuando se publican mensajes en una instancia de Message Hub, debe utilizar el canal de información denominado `messaging/messageHubFeed`. Este canal de información admite los siguientes parámetros: 

|Nombre|Tipo|Descripción|
|---|---|---|
|kafka_brokers_sasl|Matriz JSON de series|Este parámetro es una matriz de series de caracteres `<host>:<port>` que comprenden los intermediarios de la instancia de Message Hub|
|user|Serie|Su nombre de usuario de Message Hub|
|password|Serie|Su contraseña de Message Hub|
|topic|Serie|El tema que desea que escuche el desencadenante|
|kafka_admin_url|Serie de URL|El URL de la interfaz REST de administración de Message Hub|
|api_key|Serie|Su clave de API de Message Hub|
|isJSONData|Booleano (Opcional - default=false)|Si tiene el valor `true`, el canal de información intentará analizar el contenido del mensaje como JSON antes de pasarlo como carga útil del desencadenante. |

Aunque esta lista de parámetros puede parecer larga, se pueden establecer automáticamente mediante el mandato de CLI package refresh: 

1. Cree una instancia del servicio Message Hub bajo su organización actual y el espacio que utiliza para OpenWhisk.

2. Compruebe que el tema que desea escuchar ya existe en Message Hub o cree un tema nuevo para escuchar mensajes, como por ejemplo `mytopic`.

2. Actualizar los paquetes de su espacio de nombres. La renovación crea automáticamente un enlace de paquete para la instancia del servicio Message Hub que ha creado.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```
  {: screen}

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```
  {: screen}

  Ahora su enlace de paquete contiene credenciales asociadas a la instancia de Message Hub. 

3. Todo lo que tiene que hacer es crear un desencadenante que se active cuando se publiquen mensajes nuevos en Message Hub.

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

### Configuración de un paquete de Message Hub fuera de Bluemix

Si no utiliza OpenWhisk en Bluemix o si quiere configurar Message Hub fuera de Bluemix, debe crear manualmente un enlace de paquete para el servicio Message Hub. Necesita la información sobre conexión y credenciales del servicio Message Hub. 

- Cree un enlace de paquete configurado para el servicio de Message Hub.

  ```
  wsk trigger create MyMessageHubTrigger -f /whisk.system/messaging/messageHubFeed -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443 -p api_key <your API key>
  ```
  {: pre}

### Escucha de mensajes destinados a una instancia de Message Hub
{: #openwhisk_catalog_message_hub_listen}
Después de crear un desencadenante, el sistema supervisará el tema específico en el servicio de mensajería. Cuando se publiquen nuevos mensajes, se activará el desencadenante. 

La carga útil del desencadenante contendrá un campo `messages`, que es una matriz de mensajes publicados desde la última vez que se activó el desencadenante. Cada objeto de mensaje de la matriz contendrá los siguientes campos: 
- topic
- partition
- offset
- key
- value

En términos de Kafka, estos campos deberían resultar evidentes. Sin embargo, el campo `value` requiere una especial consideración. Si el parámetro `isJSONData` se ha establecido `false` (o no se ha establecido) al crear el desencadenante, el campo `value` será el valor sin formato del mensaje publicado. Sin embargo, si `isJSONData` se ha establecido en `true` al crear el desencadenante, el sistema intentará analizar este valor como objeto JSON en la medida de lo posible. Si el análisis se realiza correctamente, `value` en la carga útil del desencadenante será el objeto JSON resultante. 

Por ejemplo, si se publica el mensaje `{"title": "Some string", "amount": 5, "isAwesome": true}` con `isJSONData` establecido en `true`, la carga útil del desencadenante se parecerá a la siguiente: 

```
{
  "messages": [
      {
        "partition": 0,
        "key": null,
        "offset": 421760,
        "topic": "mytopic",
        "value": {
            "amount": 5,
            "isAwesome": true,
            "title": "Some string"
        }
      }
  ]
}
```

Sin embargo, si se publica el mismo contenido de mensaje con `isJSONData` establecido en `false`, la carga útil del desencadenante se parecerá a esta: 

```
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421761,
      "topic": "mytopic",
      "value": "{\"title\": \"Some string\", \"amount\": 5, \"isAwesome\": true}"
    }
  ]
}
```

### Los mensajes se colocan por lotes
Habrá notado que la carga útil del desencadenante contiene una matriz de mensajes. Esto significa que si genera mensajes destinados al sistema de mensajería con rapidez, el canal de información intentará colocar por lotes los mensajes publicados en una sola activación del desencadenante. Esto permite publicar los mensajes en el desencadenante de forma más rápida y eficiente. 

Tenga en cuenta que, si el desencadenante activa acciones de codificación, el número de mensajes de la carga útil no está técnicamente enlazado, aunque siempre será mayor que 0. 


## Uso del paquete Slack
{: #openwhisk_catalog_slack}

El paquete `/whisk.system/slack` ofrece una forma cómoda de utilizar las [API de Slack](https://api.slack.com/).

El paquete incluye las acciones siguientes:

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/slack` | paquete | url, channel, username | Interactuar con la API de Slack. |
| `/whisk.system/slack/post` | acción | text, url, channel, username | Publicar un mensaje en un canal de Slack |

Se recomienda la creación de un enlace de paquete con los valores de `username`, `url` y `channel`. Con enlace, no necesita especificar los valores cada vez que invoca la acción en el paquete.

### Publicación de un mensaje en un canal de Slack
{: #openwhisk_catalog_slack_post}

La acción `/whisk.system/slack/post` publica un mensaje en un canal de Slack especificado. Los parámetros son según se indica a continuación:

- `url`: el URL de webhook de Slack.
- `channel`: el canal de Slack en el que publicar el mensaje.
- `username`: el nombre con el que publicar el mensaje.
- `text`: un mensaje a publicar.
- `token`: (opcional) una [señal de acceso](https://api.slack.com/tokens) de Slack. Consulte [a continuación](./openwhisk_catalog.html#openwhisk_catalog_slack_token) para obtener más información sobre el uso de señales de acceso de Slack.

A continuación se muestra un ejemplo sobre la configuración de Slack, creación de un enlace de paquete y publicación de un mensaje en un canal.

1. Configurar un [webhook de entrada](https://api.slack.com/incoming-webhooks) de Slack para su equipo.

  Tras configurar Slack, obtendrá un URL de webhook parecido a
`https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Lo necesitará en el paso siguiente.

2. Crear un enlace de paquete con sus credenciales de Slack, el canal en el que quiera publicar y el nombre de usuario con el que publicar.

  ```
  wsk package bind /whisk.system/slack mySlack --param url "https://hooks.slack.com/services/..." --param username Bob --param channel "#MySlackChannel"
  ```
  {: pre}

3. Invocar la acción `post` en su enlace de paquete para publicar un mensaje en su canal Slack.

  ```
  wsk action invoke mySlack/post --blocking --result --param text "Hello from OpenWhisk!"
  ```
  {: pre}

### Uso de la API basada en señales de Slack
{: #openwhisk_catalog_slack_token}

Si lo prefiere, puede optar por utilizar la API basada en señales de Slack, en lugar de la API de webhook. Si elige esta opción, pase un parámetro de `señal` con la [señal de acceso](https://api.slack.com/tokens) de Slack correspondiente. A continuación, puede utilizar cualquiera de los [métodos de API de Slack](https://api.slack.com/methods) como parámetro `url`. Por ejemplo, para publicar un mensaje, utilizaría un valor de parámetro `url` de [slack.postMessage](https://api.slack.com/methods/chat.postMessage).

## Uso del paquete GitHub
{: #openwhisk_catalog_github}

El paquete `/whisk.system/github` ofrece una forma cómoda de utilizar las [API de GitHub](https://developer.github.com/).

El paquete incluye la información de entrada siguiente:

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/github` | paquete | username, repository, accessToken | Interactuar con la API de GitHub |
| `/whisk.system/github/webhook` | feed | events, username, repository, accessToken | Activar sucesos desencadenantes en caso de actividad de GitHub |

Se recomienda la creación de un enlace de paquete con los valores de `username`, `repository` y `accessToken`.  Con enlace, no necesita especificar los valores cada vez que use la información de entrada en el paquete.

### Activación de un suceso desencadenante con actividad GitHub
{: #openwhisk_catalog_github_fire}

La información de entrada `/whisk.system/github/webhook` configura un servicio para activar un desencadenante
cuando haya actividad en el repositorio de GitHub especificado. Los parámetros son según se indica a continuación:

- `username`: el nombre de usuario del repositorio GitHub.
- `repository`: el repositorio GitHub.
- `accessToken`: su señal de acceso personal de GitHub. Cuando [cree su
señal](https://github.com/settings/tokens), asegúrese de seleccionar los ámbitos repo:status y public_repo. Además, asegúrese de que no tiene webhooks ya definidos en su repositorio.
- `events`: el [tipo de suceso GitHub](https://developer.github.com/v3/activity/events/types/) de interés.

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

Una confirmación en el repositorio GitHub utilizando `git push` provoca que el webhook active el desencadenante. Si existe una regla que coincide con el desencadenante, se invocará la acción asociada.
La acción recibe la carga útil de webhook de GitHub como parámetro de entrada. Cada suceso de webhook de GitHub tiene un esquema JSON similar, pero es un objeto de carga útil exclusivo determinado por su tipo de suceso.
Para obtener más información sobre el contenido de la carga útil, consulte la documentación de la API de
[Carga útil y sucesos GitHub](https://developer.github.com/v3/activity/events/types/).


## Uso del paquete Push
{: #openwhisk_catalog_pushnotifications}

El paquete `/whisk.system/pushnotifications` le permite trabajar con un servicio de envío por push. 

El paquete incluye la información de entrada y acción siguiente:

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | paquete | appId, appSecret  | Trabaje con el servicio Push |
| `/whisk.system/pushnotifications/sendMessage` | acción | text, url, deviceIds, platforms, tagNames, apnsBadge, apnsCategory, apnsActionKeyTitle, apnsSound, apnsPayload, apnsType, gcmCollapseKey, gcmDelayWhileIdle, gcmPayload, gcmPriority, gcmSound, gcmTimeToLive | Envíe notificaciones push a uno o más dispositivos especificados |
| `/whisk.system/pushnotifications/webhook` | feed | events | Active sucesos desencadenantes en actividades de dispositivo (registro, anulación del registro, suscripción o anulación de suscripción de dispositivos) en el servicio Push |
Se recomienda la creación de un enlace de paquete con los valores de `appId` and `appSecret`. Así, no necesita especificar estas credenciales cada vez que invoque las acciones del paquete.

### Creación de un enlace de paquete Push
{: #openwhisk_catalog_pushnotifications_create}

Al crear un enlace de paquete de notificaciones push, debe especificar los parámetros siguientes:

-  `appId`: GUID de app de Bluemix.
-  `appSecret`: appSecret del servicio de notificaciones push de Bluemix.

A continuación se muestra un ejemplo de la creación de un enlace de paquete.

1. Cree una aplicación de Bluemix en el [Panel de control de Bluemix](http://console.ng.bluemix.net).

2. Inicialice el servicio de notificación push y enlace el servicio con la aplicación de Bluemix

3. Configure la [aplicación de notificación push](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

  Asegúrese de recordar el `GUID de App` y el `Secreto de App` de la app de Bluemix que ha creado.


4. Crear un enlace de paquete con `/whisk.system/pushnotifications`.

  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
  ```
  {: pre}

5. Comprobar que el enlace de paquete existe.

  ```
  wsk package list
  ```
  {: pre}

  ```
  packages
  /myNamespace/myPush private binding
  ```
  {: screen}

### Envío de notificaciones push
{: #openwhisk_catalog_pushnotifications_send}

La acción `/whisk.system/pushnotifications/sendMessage` envía notificaciones push a los dispositivos registrados. Los parámetros son según se indica a continuación:
- `text`: el mensaje de notificación a mostrar al usuario. Por ejemplo: `-p text "Hi ,OpenWhisk send a notification"`.
- `url`: un URL opcional que se puede enviar junto con la alerta. Por ejemplo: `-p url "https:\\www.w3.ibm.com"`.
- `deviceIds` La lista de dispositivos especificados. Por ejemplo: `-p deviceIds "[\"deviceID1\"]"`.
- `plataformas` Enviar una notificación a los dispositivos de las plataformas especificadas. 'A' para dispositivos Apple (iOS) y 'G' para dispositivos Google (Android). Por ejemplo `-p platforms "[\"A\"]"`.
- `tagNames` Enviar una notificación a los dispositivos que se han suscrito a cualquiera de estas etiquetas. Por ejemplo `-p tagNames "[\"tag1\"]" `.
- `gcmPayload`: carga útil JSON personalizada que se enviará como parte del mensaje de notificación. Por ejemplo: `-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`: archivo de sonido (en el dispositivo) que se intentará reproducir cuando la notificación llegue al dispositivo.
- `gcmCollapseKey`: este parámetro identifica un grupo de mensajes
- `gcmDelayWhileIdle`: cuando este parámetro se establece en true, indica que el mensaje no se enviará hasta que el dispositivo esté activo.
- `gcmPriority`: establece la prioridad del mensaje.
- `gcmTimeToLive`: este parámetro especifica cuánto tiempo (en segundos) se conservará el mensaje en el almacenamiento GCM si el dispositivo está fuera de línea.
- `apnsBadge`: número a mostrar como identificador del icono de aplicación.
- `apnsCategory`: identificador de categoría a utilizar para las notificaciones push interactivas.
- `apnsIosActionKey`: título de la clave de Acción.
- `apnsPayload`: carga útil JSON personalizada que se enviará como parte del mensaje de notificación.
- `apnsType`: ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound`: nombre del archivo de sonido del paquete de aplicación. El sonido de este archivo se reproduce como una alerta.

A continuación se muestra un ejemplo de envío de una notificación push desde el paquete pushnotification.

1. Enviar una notificación push utilizando la acción `sendMessage` del enlace de paquete que ha creado anteriormente. Asegúrese de sustituir `/myNamespace/myPush` por su nombre de paquete.

  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking --result  -p url https://example.com -p text "this is my message"  -p sound soundFileName -p deviceIds "[\"T1\",\"T2\"]"
  ```
  {: pre}

  ```
  {
  "result": {
  "pushResponse": "{"messageId":"11111H","message":{"message":{"alert":"this is my message","url":"http.google.com"},"settings":{"apns":{"sound":"default"},"gcm":{"sound":"default"},"target":{"deviceIds":["T1","T2"]}}}"
  },
      "status": "success",
      "success": true
  }
  ```
  {: screen}

### Activación de un suceso desencadenante en la actividad Push
{: #openwhisk_catalog_pushnotifications_fire}

`/whisk.system/pushnotifications/webhook` configura el servicio Push para activar un desencadenante cuando hay una actividad de dispositivo tal como un registro / anulación de registro o una suscripción / anulación de suscripción de dispositivo en una aplicación especificada

Los parámetros son según se indica a continuación:

- `appId:` GUID de app de Bluemix.
- `appSecret:` appSecret del servicio de notificaciones push de Bluemix.
- `events:` los sucesos con soporte son `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe`, `onUnsubscribe`. Para obtener notificaciones de todos los sucesos, utilice el carácter comodín `*`.

A continuación se muestra un ejemplo de creación de un desencadenante que se activará cada vez que se registre un nuevo dispositivo con la aplicación del servicio de notificaciones push.

1. Crear un enlace de paquete configurado para su servicio de notificaciones push con su appId y appSecret.

  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}

2. Crear un desencadenante para el tipo de suceso `onDeviceRegister` del servicio de notificaciones push utilizando su información de entrada de `myPush/webhook`.

  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}
