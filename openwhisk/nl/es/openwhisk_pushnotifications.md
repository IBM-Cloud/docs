---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilización del paquete de notificaciones push
{: #openwhisk_catalog_pushnotifications}

El paquete `/whisk.system/pushnotifications` le permite trabajar con un servicio de envío por push.

El paquete incluye la información de entrada y acción siguiente:

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | paquete | appId, appSecret  | Trabaje con el servicio Push |
| `/whisk.system/pushnotifications/sendMessage` | acción | text, url, deviceIds, platforms, tagNames, gcmPayload, gcmSound, gcmCollapseKey, gcmDelayWhileIdle, gcmPriority, gcmTimeToLive, gcmSync, gcmVisibility, gcmStyleType, gcmStyleTitle, gcmStyleUrl, gcmStyleText, gcmStyleLines, apnsBadge, apnsCategory, apnsIosActionKey, apnsPayload, apnsType, apnsSound, fireFoxTitle, fireFoxIconUrl, fireFoxTimeToLive, fireFoxPayload, chromeTitle, chromeIconUrl, chromeTimeToLive, chromePayload, chromeAppExtTitle, chromeAppExtCollapseKey, chromeAppExtDelayWhileIdle, chromeAppExtIconUrl, chromeAppExtTimeToLive, chromeAppExtPayload | Envíe notificaciones push a uno o más dispositivos especificados |
| `/whisk.system/pushnotifications/webhook` | canal de información | events | Active sucesos desencadenantes en actividades de dispositivo (registro, anulación del registro, suscripción o anulación de suscripción de dispositivos) en el servicio Push |
Se recomienda la creación de un enlace de paquete con los valores de `appId` y `appSecret`. Así, no necesita especificar estas credenciales cada vez que invoque las acciones del paquete.

## Creación de un enlace de paquete Push
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
  

## Envío de notificaciones push
{: #openwhisk_catalog_pushnotifications_send}

La acción `/whisk.system/pushnotifications/sendMessage` envía notificaciones push a los dispositivos registrados. Los parámetros son según se indica a continuación:
- `text`: el mensaje de notificación a mostrar al usuario. Por ejemplo: `-p text "Hi ,OpenWhisk send a notification"`.
- `url`: un URL opcional que se puede enviar junto con la alerta. Por ejemplo: `-p url "https:\\www.w3.ibm.com"`.
- `deviceIds` La lista de dispositivos especificados. Por ejemplo: `-p deviceIds ["deviceID1"]`.
- `plataformas` Enviar una notificación a los dispositivos de las plataformas especificadas. 'A' para dispositivos Apple (iOS) y 'G' para dispositivos Google (Android). Por ejemplo `-p platforms ["A"]`.
- `tagNames` Enviar una notificación a los dispositivos que se han suscrito a cualquiera de estas etiquetas. Por ejemplo `-p tagNames "[\"tag1\"]" `.
- `gcmPayload`: carga útil JSON personalizada que se enviará como parte del mensaje de notificación. Por ejemplo: `-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmSound`: archivo de sonido (en el dispositivo) que se intentará reproducir cuando la notificación llegue al dispositivo.
- `gcmCollapseKey`: este parámetro identifica un grupo de mensajes
- `gcmDelayWhileIdle`: cuando este parámetro se establece en true, indica que el mensaje no se enviará hasta que el dispositivo esté activo.
- `gcmPriority`: establece la prioridad del mensaje.
- `gcmTimeToLive`: este parámetro especifica cuánto tiempo (en segundos) se conservará el mensaje en el almacenamiento GCM si el dispositivo está fuera de línea.
- `gcmSync`: la mensajería del grupo de dispositivos facilita que cada instancia de app de un grupo refleje el estado actualizado de mensajería.
- `gcmVisibility`: private/public - visibilidad de esta notificación, que afecta a cómo y cuándo se muestran las notificaciones en una pantalla bloqueada segura.
- `gcmStyleType`: especifica el tipo de notificaciones expandible. Los valores posibles son `bigtext_notification`, `picture_notification`, `inbox_notification`.
- `gcmStyleTitle`: especifica el título de la notificación. El título se muestra cuando se expande la notificación. El título se debe especificar para las tres notificaciones expandibles.
- `gcmStyleUrl`: URL del que se debe obtener la imagen para la notificación. Se debe especificar para picture_notification.
- `gcmStyleText`: texto detallado que se tiene que visualizar cuando se expande una bigtext_notification. Se debe especificar para bigtext_notification.
- `gcmStyleLines`: matriz de series que se debe visualizar en modalidad de bandeja de entrada para inbox_notification. Se debe especificar para inbox_notification.
- `apnsBadge`: número a mostrar como identificador del icono de aplicación.
- `apnsCategory`: identificador de categoría a utilizar para las notificaciones push interactivas.
- `apnsIosActionKey`: título de la clave de Acción.
- `apnsPayload`: carga útil JSON personalizada que se enviará como parte del mensaje de notificación.
- `apnsType`: ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound`: nombre del archivo de sonido del paquete de aplicación. El sonido de este archivo se reproduce como una alerta.
- `fireFoxTitle`: especifica el título que se debe definir para la notificación WebPush.
- `fireFoxIconUrl`: el URL del icono que se debe establecer para la notificación WebPush.
- `fireFoxTimeToLive`: este parámetro especifica cuánto tiempo (en segundos) se debe conservar el mensaje en el almacenamiento GCM si el dispositivo está fuera de línea.
- `fireFoxPayload`: carga útil JSON personalizada que se enviará como parte del mensaje de notificación.
- `chromeTitle`: especifica el título que se debe definir para la notificación WebPush.
- `chromeIconUrl`: el URL del icono que se debe establecer para la notificación WebPush.
- `chromeTimeToLive`: este parámetro especifica cuánto tiempo (en segundos) se debe conservar el mensaje en el almacenamiento GCM si el dispositivo está fuera de línea.
- `chromePayload`: carga útil JSON personalizada que se enviará como parte del mensaje de notificación.
- `chromeAppExtTitle`: especifica el título que se debe definir para la notificación WebPush.
- `chromeAppExtCollapseKey`: este parámetro identifica un grupo de mensajes.
- `chromeAppExtDelayWhileIdle`: cuando este parámetro se establece en true, indica que el mensaje no se debe enviar hasta que el dispositivo esté activo.
- `chromeAppExtIconUrl`: el URL del icono que se debe establecer para la notificación WebPush.
- `chromeAppExtTimeToLive`: este parámetro especifica cuánto tiempo (en segundos) se debe conservar el mensaje en el almacenamiento GCM si el dispositivo está fuera de línea.
- `chromeAppExtPayload`: carga útil JSON personalizada que se enviará como parte del mensaje de notificación.

A continuación se muestra un ejemplo de envío de una notificación push desde el paquete *pushnotification*.

- Enviar una notificación push utilizando la acción `sendMessage` del enlace de paquete que ha creado anteriormente. Asegúrese de sustituir `/myNamespace/myPush` por su nombre de paquete.
  
  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking --result  -p url https://example.com -p text "this is my message"  -p sound soundFileName -p deviceIds "[\"T1\",\"T2\"]"
  ```
  {: pre}
  ```json
  {
    "result": {
    "pushResponse":
      {
        "messageId":"11111H",
        "message":{
          "alert":"this is my message",
          "url":""
        },
        "settings":{
          "apns":{
            "sound":"default"
          },
          "gcm":{
            "sound":"default"
            },
          "target":{
            "deviceIds":["T1","T2"]
          }
        }
      }
    },
      "status": "success",
      "success": true
  }
  ```
  

## Activación de un suceso desencadenante en la actividad del servicio de notificaciones push
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
  
3. Podría crear una regla que envíe un mensaje cada vez que se registra un nuevo dispositivo. Cree una regla nueva utilizando la acción y desencadenante anteriores.
  
  ```
  wsk rule create --enable myRule myPushTrigger sendMessage
  ```
  {: pre}
  
  Compruebe los resultados en el `sondeo de activación de wsk`.

  Registre el dispositivo en la aplicación Bluemix; puede ver la ejecución de `rule`,`trigger` y `action` en openWhisk [dashboard] (https://console.{Domain}/openwhisk/dashboard).

  La acción enviará una notificación push.
  
