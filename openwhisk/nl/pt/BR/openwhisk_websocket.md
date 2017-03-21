## Usando o pacote WebSocket
{: #openwhisk_catalog_websocket}

O pacote `/whisk.system/websocket` oferece uma maneira conveniente de postar mensagens em um WebSocket.

O pacote inclui a ação a seguir:

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/websocket` | pacote | uri | Utilitários para comunicação com WebSockets |
| `/whisk.system/websocket/send` | ação | uri, payload | Enviar a carga útil para o URI do WebSocket |

Se você planeja enviar muitas mensagens para o mesmo URI do WebSocket, sugere-se criar uma ligação de pacote com o valor `uri`. Com a ligação, não será necessário especificar o valor cada vez que a ação `send` for usada.

### Enviando uma mensagem para um WebSocket

A ação `/whisk.system/websocket/send` enviará uma carga útil para um URI do WebSocket. Os parâmetros são como segue:

- `uri`: o URI do servidor websocket (por exemplo, ws://mywebsockethost:80)
- `payload`: a mensagem que você deseja enviar ao WebSocket
