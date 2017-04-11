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

# Utilisation du package Slack
{: #openwhisk_catalog_slack}

Le package `/whisk.system/slack` permet d'utiliser les [API Slack](https://api.slack.com/).

Le package inclut les actions suivantes :

| Entité | Type | Paramètres | Description |
| --- | --- | --- | --- |
| `/whisk.system/slack` | package | url, channel, username | Interagir avec l'API Slack |
| `/whisk.system/slack/post` | action | text, url, channel, username | Publier un message dans un canal Slack |

Il est recommandé de créer une liaison de package avec les valeurs `username`, `url` et `channel`. Grâce à la liaison, il n'est pas nécessaire de spécifier les valeurs à chaque fois que vous appelez l'action dans le
package.

## Publication d'un message dans un canal Slack

L'action `/whisk.system/slack/post` publie un message dans un canal Slack spécifié. Les paramètres sont les suivants :

- `url` : URL du webhook Slack.
- `channel` : canal Slack dans lequel publier le message.
- `username` : nom sous lequel publier le message.
- `text` : message à publier.
- `token` : (facultatif) [Jeton d'accès](https://api.slack.com/tokens) Slack. Voir [ci-après](./catalog.md#using-the-slack-token-based-api) pour plus de détails sur l'utilisation de jetons d'accès Slack.

L'exemple ci-dessous explique comment configurer Slack, créer une liaison de package et publier un message dans un canal.

1. Configurez un [webhook entrant](https://api.slack.com/incoming-webhooks) Slack pour votre équipe.
  
  Une fois Slack configuré, vous obtenez une adresse URL de webhook similaire à `https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Vous en aurez besoin à l'étape suivante.
  
2. Créez une liaison de package avec vos données d'identification Slack, le canal dans lequel publier le message, et le nom d'utilisateur sous
lequel publier le message.
  
  ```
  wsk package bind /whisk.system/slack mySlack \
    --param url "https://hooks.slack.com/services/..." \
    --param username "Bob" \
    --param channel "#MySlackChannel"
  ```
  {: pre}
  
3. Appelez l'action `post` dans votre liaison de package pour publier un message dans votre canal Slack.
  
  ```
  wsk action invoke mySlack/post --blocking --result \
    --param text "Hello from OpenWhisk!"
  ```
  {: pre}
  

## Utilisation de l'API reposant sur le jeton Slack

Si vous préférez, vous pouvez choisir d'utiliser l'API reposant sur le jeton Slack plutôt que l'API de webhook. Dans ce cas, transmettez un paramètre `token` contenant votre [jeton d'accès](https://api.slack.com/tokens) Slack. Vous pourrez ensuite utiliser l'une des [méthodes d'API Slack](https://api.slack.com/methods) comme paramètre `url`. Par exemple, pour envoyer un message, utilisez [slack.postMessage](https://api.slack.com/methods/chat.postMessage) comme valeur de paramètre `url`.
