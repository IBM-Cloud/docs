## WebSocket-Paket verwenden
{: #openwhisk_catalog_websocket}

Das Paket `/whisk.system/websocket` bietet eine bequeme Möglichkeit, Nachrichten an einen WebSocket zu senden (posten).

Das Paket enthält die folgende Aktion:

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/websocket` | Paket | uri | Dienstprogramme zur Kommunikation mit WebSockets |
| `/whisk.system/websocket/send` | Aktion | uri, payload | Nutzdaten (payload) an den WebSocket-URI senden |

Wenn Sie planen, viele Nachrichten an denselben WebSocket-URI zu senden, wird empfohlen, eine Paketbindung mit dem Wert `uri` zu erstellen.  Mit der Bindung brauchen Sie den Wert nicht jedes Mal anzugeben, wenn Sie die Aktion `send` verwenden.

### Nachricht an einen WebSocket senden

Die Aktion `/whisk.system/websocket/send` sendet Nutzdaten (payload) an einen WebSocket-URI. Die folgenden Parameter sind verfügbar:

- `uri`: Der URI des WebSocket-Servers (z. B.: ws://mywebsockethost:80)
- `payload`: Die Nachricht, die an den WebSocket gesendet werden soll
