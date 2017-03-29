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

# Slack 패키지 사용
{: #openwhisk_catalog_slack}

`/whisk.system/slack` 패키지는 [Slack API](https://api.slack.com/)를 사용하는 편리한 방법을 제공합니다.

패키지에는 다음 조치가 포함됩니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/slack` | 패키지 | url, channel, username | Slack API와 상호작용 |
| `/whisk.system/slack/post` | 조치 | text, url, channel, username | Slack 채널에 메시지 게시 |

`username`, `url`, `channel` 값을 사용하여 패키지 바인딩을 작성하도록 권장합니다. 바인딩을 사용하면, 패키지에서 조치를 호출할 때마다 값을 지정할 필요가 없습니다.

## Slack 채널에 메시지 게시

`/whisk.system/slack/post` 조치는 메시지를 지정된 Slack 채널에 게시합니다. 매개변수는 다음과 같습니다.

- `url`: Slack 웹훅 URL입니다.
- `channel`: 메시지를 게시할 Slack 채널입니다.
- `username`: 메시지를 게시할 사용자 이름입니다.
- `text`: 게시할 메시지입니다.
- `token`: (선택사항) Slack [액세스 토큰](https://api.slack.com/tokens)입니다. Slack 액세스 토큰 사용에 대한 세부사항은 [아래의 내용](./catalog.md#using-the-slack-token-based-api)을 참조하십시오.

다음은 Slack을 구성하고 패키지 바인딩을 작성하여 메시지를 채널에 게시하는 예입니다.

1. 팀을 위해 Slack [수신 웹훅](https://api.slack.com/incoming-webhooks)를 구성하십시오.
  
  Slack이 구성되면 웹훅 URL이 `https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`와 같이 표시됩니다. 다음 단계에서 이 URL이 필요합니다.
  
2. Slack 신임 정보, 게시할 채널 및 게시할 때 사용할 사용자 이름을 사용하여 패키지 바인딩을 작성하십시오.
  
  ```
  wsk package bind /whisk.system/slack mySlack \
    --param url "https://hooks.slack.com/services/..." \
    --param username "Bob" \
    --param channel "#MySlackChannel"
  ```
  {: pre}
  
3. 패키지 바인딩에서 `post` 조치를 호출하여 사용자의 Slack 채널에 메시지를 게시하십시오.
  
  ```
  wsk action invoke mySlack/post --blocking --result \
    --param text "Hello from OpenWhisk!"
  ```
  {: pre}
  

## Slack 토큰 기반 API 사용

원하는 경우, 선택적으로 웹훅 API 대신 Slack의 토큰 기반 API를 사용하도록 선택할 수 있습니다. 이렇게 선택하는 경우, Slack [액세스 토큰](https://api.slack.com/tokens)이 포함된 `token` 매개변수를 전달하십시오. 그런 다음 [Slack API 메소드](https://api.slack.com/methods)를 `url` 매개변수로 사용할 수 있습니다. 예를 들어, 메시지를 게시하려면 [slack.postMessage](https://api.slack.com/methods/chat.postMessage)의 `url` 매개변수값을 사용합니다. 
