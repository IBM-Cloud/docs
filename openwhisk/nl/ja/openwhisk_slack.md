---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Slack パッケージの使用
{: #openwhisk_catalog_slack}

`/whisk.system/slack` パッケージは、
[Slack API](https://api.slack.com/) を使用する便利な方法を提供します。

このパッケージには、以下のアクションが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/slack` | パッケージ | url、channel、username | Slack API と対話 |
| `/whisk.system/slack/post` | アクション | text、url、channel、username | Slack チャネルへメッセージをポスト |

`username`、`url`、および `channel` の各値を使用してパッケージ・バインディングを作成することをお勧めします。バインディングを使用すると、パッケージでアクションを起動するたびに値を指定する必要はありません。

## Slack チャネルへのメッセージのポスト

`/whisk.system/slack/post` アクションは、指定された Slack チャネルにメッセージをポストします。パラメーターは次のとおりです。


- `url`: Slack の Webhook URL。
- `channel`: メッセージのポスト先の Slack チャネル。
- `username`: メッセージをポストするユーザーの名前。
- `text`: ポストするメッセージ。
- `token`: (オプション) Slack [アクセス・トークン](https://api.slack.com/tokens)。Slack アクセス・トークンの使用について詳しくは、[以下](./catalog.md#using-the-slack-token-based-api)を参照してください。

以下は、Slack を構成し、パッケージ・バインディングを作成して、
メッセージをチャネルにポストする例です。

1. チームに Slack の [Incoming Webhook](https://api.slack.com/incoming-webhooks) を構成します。
  
  Slack の構成後、`https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc` のような Web フック URL を取得します。これは次のステップで必要になります。
  
2. Slack の資格情報、ポスト先のチャネル、およびポストするユーザー名を指定して、パッケージ・バインディングを作成します。
  
  ```
  wsk package bind /whisk.system/slack mySlack \
    --param url "https://hooks.slack.com/services/..." \
    --param username "Bob" \
    --param channel "#MySlackChannel"
  ```
  {: pre}
  
3. パッケージ・バインディングの `post` アクションを起動し、ご使用の Slack チャネルにメッセージをポストします。
  
  ```
  wsk action invoke mySlack/post --blocking --result \
    --param text "Hello from OpenWhisk!"
  ```
  {: pre}
  

## Slack トークン・ベースの API の使用

オプションで、webhook API ではなく、Slack のトークン・ベース API を使用することを選択できます。そうするよう選択した場合、Slack [アクセス・トークン](https://api.slack.com/tokens)を含んでいる `token` パラメーターを渡します。次に、任意の [Slack API メソッド](https://api.slack.com/methods)を `url` パラメーターとして使用します。例えば、メッセージをポストするために、`url` パラメーター値 [slack.postMessage](https://api.slack.com/methods/chat.postMessage) を使用します。
