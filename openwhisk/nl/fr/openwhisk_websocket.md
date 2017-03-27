## Utilisation du package WebSocket
{: #openwhisk_catalog_websocket}

Le package `/whisk.system/websocket` offre un moyen très pratique de publier de messages sur un WebSocket.

Le package inclut l'action suivante :

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/websocket` | package | uri | Utilitaires permettant de communiquer avec des WebSockets |
| `/whisk.system/websocket/send` | action | uri, payload | Envoi du contenu à l'URI de WebSocket |

Si vous prévoyez d'envoyer un grand nombre de messages au même URI de WebSocket, il est recommandé de créer une liaison de package avec la valeur `uri`.  Grâce à la liaison, vous n'avez pas besoin de spécifier la valeur à chaque fois que vous utilisez l'action `send`.

### Envoi d'un message à un WebSocket

L'action `/whisk.system/websocket/send` envoie un contenu à un URI de WebSocket. Les paramètres sont les suivants :

- `uri` : URI du serveur Websocket (par exemple, ws://mywebsockethost:80)
- `payload` : message que vous souhaitez envoyer au WebSocket
