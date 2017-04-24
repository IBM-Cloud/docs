# 使用 WebSocket 套件
{: #openwhisk_catalog_websocket}

`/whisk.system/websocket` 套件提供便利的方式，以將訊息張貼至 WebSocket。

該套件包含下列動作：

| 實體 | 類型 | 參數 | 說明 |
| --- | --- | --- | --- |
| `/whisk.system/websocket` | 套件 | uri | 與 WebSockets 進行通訊的公用程式 |
| `/whisk.system/websocket/send` | 動作 | uri、payload | 將有效負載傳送至 WebSocket URI |

如果您計劃將許多訊息傳送至相同的 WebSocket URI，則建議使用 `uri` 值來建立套件連結。使用連結，您就不需要每次使用 `send` 動作時都指定值。

## 將訊息傳送至 WebSocket

`/whisk.system/websocket/send` 動作會將有效負載傳送至 WebSocket URI。參數如下所示：

- `uri`：WebSocket 伺服器的 URI（例如：ws://mywebsockethost:80）
- `payload`：您想要傳送至 WebSocket 的訊息
