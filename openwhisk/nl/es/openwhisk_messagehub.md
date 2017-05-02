---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-04"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilización del paquete Message Hub
{: #openwhisk_catalog_message_hub}

Este paquete le permite comunicarse con instancias de [Message Hub](https://developer.ibm.com/messaging/message-hub) para publicar y consumir mensajes utilizando la API de Kafka nativa de alto rendimiento.
{: shortdesc}

## Creación de un desencadenante que escuche una instancia de IBM MessageHub
{: #openwhisk_catalog_message_hub_trigger}

Para crear un desencadenante que reaccione cuando se publican mensajes en una instancia de Message Hub, debe utilizar el canal de información denominado `/messaging/messageHubFeed`. Esta acción de canal de información admite los siguientes parámetros:

|Nombre|Tipo|Descripción|
|---|---|---|
|kafka_brokers_sasl|Matriz JSON de series|Este parámetro es una matriz de series de caracteres `<host>:<port>` que comprenden los intermediarios de la instancia de Message Hub|
|user|Serie|Su nombre de usuario de Message Hub|
|password|Serie|Su contraseña de Message Hub|
|topic|Serie|El tema que desea que escuche el desencadenante|
|kafka_admin_url|Serie de URL|El URL de la interfaz REST de administración de Message Hub|
|isJSONData|Booleano (Opcional - default=false)|Si tiene el valor `true`, el proveedor intentará analizar el valor del mensaje como JSON antes de pasarlo como carga útil del desencadenante.|
|isBinaryKey|Booleano (Opcional - default=false)|Si tiene el valor `true`, el proveedor codificará el valor de la clave como Base64 antes de pasarlo como carga útil del desencadenante.|
|isBinaryValue|Booleano (Opcional - default=false)|Si tiene el valor `true`, el proveedor codificará el valor del mensaje como Base64 antes de pasarlo como carga útil del desencadenante.|

Aunque esta lista de parámetros puede parecer larga, se pueden establecer automáticamente mediante el mandato de CLI package refresh:

1. Cree una instancia del servicio Message Hub bajo su organización actual y el espacio que utiliza para OpenWhisk.

2. Compruebe que el tema que desea escuchar ya existe en Message Hub o cree un tema nuevo, como por ejemplo `mytopic`.

3. Actualizar los paquetes de su espacio de nombres. La renovación crea automáticamente un enlace de paquete para la instancia del servicio Message Hub que ha creado.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Message_Hub_Credentials-1
  ```

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1 private
  ```

  Ahora su enlace de paquete contiene credenciales asociadas a la instancia de Message Hub.

4. Ahora todo lo que tiene que hacer es crear un desencadenante que se active cuando se publiquen mensajes nuevos en el tema Message Hub.

  ```
  wsk trigger create MyMessageHubTrigger -f /myBluemixOrg_myBluemixSpace/Bluemix_Message_Hub_Credentials-1/messageHubFeed -p topic mytopic
  ```
  {: pre}

## Configuración de un paquete de Message Hub fuera de Bluemix

Si quiere configurar Message Hub fuera de Bluemix, debe crear manualmente un enlace de paquete para el servicio Message Hub. Necesita la información sobre conexión y credenciales del servicio Message Hub.

1. Cree un enlace de paquete configurado para el servicio de Message Hub.

  ```
  wsk package bind /whisk.system/messaging myMessageHub -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p user <your Message Hub user> -p password <your Message Hub password> -p kafka_admin_url https://kafka-admin-prod01.messagehub.services.us-south.bluemix.net:443
  ```
  {: pre}

2. Ahora puede crear un desencadenante utilizando el nuevo paquete que se activará cuando se publiquen mensajes nuevos en el tema Message Hub.

  ```
  wsk trigger create MyMessageHubTrigger -f myMessageHub/messageHubFeed -p topic mytopic -p isJSONData true
  ```
  {: pre}


## Escucha de mensajes
{: #openwhisk_catalog_message_hub_listen}

Después de crear un desencadenante, el sistema supervisará el tema específico en el servicio de mensajería. Cuando se publiquen nuevos mensajes, se activará el desencadenante.

La carga útil del desencadenante contendrá un campo `messages`, que es una matriz de mensajes publicados desde la última vez que se activó el desencadenante. Cada objeto de mensaje de la matriz contendrá los siguientes campos:
- topic
- partition
- offset
- key
- value

En términos de Kafka, estos campos deberían resultar evidentes. Sin embargo, `key` tiene una función opcional `isBinaryKey` que permite que `key` transmita datos binarios. Además, el campo `value` requiere una especial consideración. Dispone de los campos opcionales `isJSONData` e `isBinaryValue` para gestionar los mensajes binarios y JSON. Estos campos, `isJSONData` e `isBinaryValue`, no se pueden utilizar juntos.

Por ejemplo, si `isBinaryKey` se ha establecido en `true` al crear el desencadenante, `key` se codificará como una serie Base64 cuando se devuelva de su carga útil de un desencadenante activado.

Por ejemplo, su se publica el valor de `key` `Some key` con `isBinaryKey` establecido en `true`, la carga útil del desencadenante será como la siguiente:

```json
{
    "messages": [
       {
            "partition": 0,
            "key": "U29tZSBrZXk=",
            "offset": 421760,
            "topic": "mytopic",
            "value": "Some value"
        }
    ]
}
```

Si el parámetro `isJSONData` se ha establecido `false` (o no se ha establecido) al crear el desencadenante, el campo `value` será el valor sin formato del mensaje publicado. Sin embargo, si `isJSONData` se ha establecido en `true` al crear el desencadenante, el sistema intentará analizar este valor como objeto JSON en la medida de lo posible. Si el análisis se realiza correctamente, `value` en la carga útil del desencadenante será el objeto JSON resultante.

Por ejemplo, si se publica el mensaje `{"title": "Some string", "amount": 5, "isAwesome": true}` con `isJSONData` establecido en `true`, la carga útil del desencadenante se parecerá a la siguiente:

```json
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

```json
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

Al igual que sucede con `isJSONData`, si `isBinaryValue` se ha establecido en `true` durante la creación del desencadenante, el `value` resultante en la carga útil del desencadenante se codificará como una serie Base64.

Por ejemplo, su se publica el valor de `value` `Some data` con `isBinaryValue` establecido en `true`, la carga útil del desencadenante se parecerá a la siguiente:

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "U29tZSBkYXRh"
    }
  ]
}
```

Si se publica el mismo mensaje sin `isBinaryData` establecido en `true`, la carga útil del desencadenante se parecerá a la del siguiente ejemplo:

```json
{
  "messages": [
    {
      "partition": 0,
      "key": null,
      "offset": 421760,
      "topic": "mytopic",
      "value": "Some data"
    }
  ]
}
```

### Los mensajes se colocan por lotes
Habrá notado que la carga útil del desencadenante contiene una matriz de mensajes. Esto significa que si genera mensajes destinados al sistema de mensajería con rapidez, el canal de información intentará colocar por lotes los mensajes publicados en una sola activación del desencadenante. Esto permite publicar los mensajes en el desencadenante de forma más rápida y eficiente.

Tenga en cuenta que, si el desencadenante activa acciones de codificación, el número de mensajes de la carga útil no está técnicamente enlazado, aunque siempre será mayor que 0. A continuación se muestra un ejemplo de un mensaje por lotes (observe el campo en el valor *offset*):
 
 ```json
 {
   "messages": [
       {
         "partition": 0,
         "key": null,
         "offset": 100,
         "topic": "mytopic",
         "value": {
             "amount": 5
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 101,
         "topic": "mytopic",
         "value": {
             "amount": 1
         }
       },
       {
         "partition": 0,
         "key": null,
         "offset": 102,
         "topic": "mytopic",
         "value": {
             "amount": 999
         }
       }
   ]
 }
 ```

## Generación de mensajes en Message Hub
Si desea utilizar una acción de OpenWhisk para generar un mensaje en Message Hub, puede utilizar la acción `/messaging/messageHubProduce`. Esta acción toma los siguientes parámetros:

|Nombre|Tipo|Descripción|
|---|---|---|
|kafka_brokers_sasl|Matriz JSON de series|Este parámetro es una matriz de series de caracteres `<host>:<port>` que comprenden los intermediarios de la instancia de Message Hub|
|user|Serie|Su nombre de usuario de Message Hub|
|password|Serie|Su contraseña de Message Hub|
|topic|Serie|El tema que desea que escuche el desencadenante|
|value|Serie|El valor del mensaje que desea generar|
|key|Serie (opcional)|La clave del mensaje que desea generar|

Aunque los tres primeros parámetros se pueden enlazan automáticamente mediante `wsk package refresh`, a continuación se muestra un ejemplo de cómo invocar la acción con todos los parámetros necesarios:

```
wsk action invoke /messaging/messageHubProduce -p kafka_brokers_sasl "[\"kafka01-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka02-prod01.messagehub.services.us-south.bluemix.net:9093\", \"kafka03-prod01.messagehub.services.us-south.bluemix.net:9093\"]" -p topic mytopic -p user <your Message Hub user> -p password <your Message Hub password> -p value "Este es el contenido de mi mensaje"
```
{: pre}

## Ejemplos

### Integración de OpenWhisk con IBM Message Hub, Node Red, IBM Watson IoT, IBM Object Storage e IBM Data Science Experience
Un ejemplo que integra OpenWhisk con IBM Message Hub, Node Red, IBM Watson IoT, IBM Object Storage, y el servicio de IBM Data Science Experience (Spark) podría ser [que encontrará aquí](https://medium.com/openwhisk/transit-flexible-pipeline-for-iot-data-with-bluemix-and-openwhisk-4824cf20f1e0).

## Referencia
- [IBM Message Hub](https://developer.ibm.com/messaging/message-hub/)
- [Apache Kafka](https://kafka.apache.org/)
