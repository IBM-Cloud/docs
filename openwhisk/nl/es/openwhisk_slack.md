---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Uso del paquete Slack
{: #openwhisk_catalog_slack}

El paquete `/whisk.system/slack` ofrece una forma cómoda de utilizar las [API de Slack](https://api.slack.com/).

El paquete incluye las acciones siguientes:

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/slack` | paquete | url, channel, username | Interactuar con la API de Slack |
| `/whisk.system/slack/post` | acción | text, url, channel, username | Publicar un mensaje en un canal de Slack |

Se recomienda la creación de un enlace de paquete con los valores de `username`, `url` y `channel`. Con enlace, no necesita especificar los valores cada vez que invoca la acción en el paquete.

## Publicación de un mensaje en un canal de Slack

La acción `/whisk.system/slack/post` publica un mensaje en un canal de Slack especificado. Los parámetros son según se indica a continuación:

- `url`: el URL de webhook de Slack.
- `channel`: el canal de Slack en el que publicar el mensaje.
- `username`: el nombre con el que publicar el mensaje.
- `text`: un mensaje a publicar.
- `token`: (opcional) una [señal de acceso](https://api.slack.com/tokens) de Slack. Consulte [a continuación](./catalog.md#using-the-slack-token-based-api) para obtener más información sobre el uso de señales de acceso de Slack.

A continuación se muestra un ejemplo sobre la configuración de Slack, creación de un enlace de paquete y publicación de un mensaje en un canal.

1. Configurar un [webhook de entrada](https://api.slack.com/incoming-webhooks) de Slack para su equipo.
  
  Tras configurar Slack, obtendrá un URL de webhook parecido a
`https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Lo necesitará en el paso siguiente.
  
2. Crear un enlace de paquete con sus credenciales de Slack, el canal en el que quiera publicar y el nombre de usuario con el que publicar.
  
  ```
  wsk package bind /whisk.system/slack mySlack \
    --param url "https://hooks.slack.com/services/..." \
    --param username "Bob" \
    --param channel "#MySlackChannel"
  ```
  {: pre}
  
3. Invocar la acción `post` en su enlace de paquete para publicar un mensaje en su canal Slack.
  
  ```
  wsk action invoke mySlack/post --blocking --result \
    --param text "Hello from OpenWhisk!"
  ```
  {: pre}
  

## Uso de la API basada en señales de Slack

Si lo prefiere, puede optar por utilizar la API basada en señales de Slack, en lugar de la API de webhook. Si elige esta opción, pase un parámetro de `señal` con la [señal de acceso](https://api.slack.com/tokens) de Slack correspondiente. A continuación, puede utilizar cualquiera de los [métodos de API de Slack](https://api.slack.com/methods) como parámetro `url`. Por ejemplo, para publicar un mensaje, utilizaría un valor de parámetro `url` de [slack.postMessage](https://api.slack.com/methods/chat.postMessage).
