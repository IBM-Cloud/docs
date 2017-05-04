# WebSocket 패키지 사용
{: #openwhisk_catalog_websocket}

`/whisk.system/websocket` 패키지는 WebSocket에 메시지를 게시하는 편리한 방법을 제공합니다.

패키지에는 다음 조치가 포함됩니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/websocket` | 패키지 | uri | WebSockets와 통신하기 위한 유틸리티 |
| `/whisk.system/websocket/send` | 조치 | uri, payload | WebSocket URI로 페이로드 전송 |

동일한 WebSocket URI로 많은 메시지를 보내려는 경우 `uri` 값으로 패키지 바인딩을 작성하는 것이 좋습니다. 바인딩을 사용하면 `send` 조치를 사용할 때마다 값을 지정하지 않아도 됩니다.

## WebSocket으로 메시지 전송

`/whisk.system/websocket/send` 조치는 WebSocket URI로 페이로드를 보냅니다. 매개변수는 다음과 같습니다.

- `uri`: websocket 서버의 URI(예: ws://mywebsockethost:80)
- `payload`: WebSocket으로 보내려는 메시지
