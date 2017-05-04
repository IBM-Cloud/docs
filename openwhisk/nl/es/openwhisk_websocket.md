# Utilización del paquete WebSocket
{: #openwhisk_catalog_websocket}

El paquete `/whisk.system/websocket` proporciona un método cómodo para publicar mensajes en un WebSocket.

El paquete incluye las acciones siguientes:

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/websocket` | paquete | uri | Programas de utilidad para comunicar con WebSockets |
| `/whisk.system/websocket/send` | acción | uri, payload | Enviar la carga útil al URI de WebSocket |

Si tiene intención de enviar varios mensajes al mismo URI de WebSocket, se recomienda crear un enlace de paquete con el valor `uri`.  Con enlace, no necesita especificar el valor cada vez que utilice la acción `send`.

## Envío de un mensaje a un WebSocket

La acción `/whisk.system/websocket/enviar` envía una carga útil a un URI de WebSocket. Los parámetros son según se indica a continuación:

- `uri`: el URI del servidor websocket (por ejemplo, ws://mywebsockethost:80)
- `payload`: el mensaje que desea enviar a WebSocket
