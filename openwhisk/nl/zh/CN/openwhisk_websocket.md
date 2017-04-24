# 使用 WebSocket 包
{: #openwhisk_catalog_websocket}

通过 `/whisk.system/websocket` 包，可方便地将消息发布到 WebSocket。

此包中包含以下操作：

| 实体 | 类型 | 参数 | 描述 |
| --- | --- | --- | --- |
| `/whisk.system/websocket` | 包 | uri | 用于与 WebSocket 进行通信的实用程序 |
| `/whisk.system/websocket/send` | 操作 | uri 和 payload | 将有效内容发送到 WebSocket URI |

如果计划将许多消息发送到同一 WebSocket URI，建议使用 `uri` 值创建包绑定。通过绑定，就无需在每次使用 `send` 操作时指定此值。

## 向 WebSocket 发送消息

`/whisk.system/websocket/send` 操作会将有效内容发送到 WebSocket URI。参数如下所示：

- `uri`：WebSocket 服务器的 URI（例如 ws://mywebsockethost:80）
- `payload`：希望发送到 WebSocket 的消息
