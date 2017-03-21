## Utilizzo del pacchetto WebSocket
{: #openwhisk_catalog_websocket}

Il pacchetto `/whisk.system/websocket` offre una soluzione pratica per pubblicare i messaggi in un WebSocket.

Il pacchetto include la seguente azione:

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/websocket` | pacchetto | uri | Programmi di utilità per comunicare con WebSocket |
| `/whisk.system/websocket/send` | azione | uri, payload | Invia il payload all'URI WebSocket |

Se prevedi di inviare numerosi messaggi allo stesso URI WebSocket, si consiglia di creare un bind di pacchetto con il valore `uri`.  Con il bind, non dovrai specificare il valore ogni volta che usi l'azione `send`.

### Invio di un messaggio a un WebSocket

L'azione `/whisk.system/websocket/send` invierà un payload a un URI WebSocket. I parametri sono i seguenti:

- `uri`: l'URI del server websocket (ad esempio, ws://mywebsockethost:80)
- `payload`: il messaggio che vuoi inviare a WebSocket
