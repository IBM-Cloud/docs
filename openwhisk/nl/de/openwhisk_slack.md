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

# Slack-Paket verwenden
{: #openwhisk_catalog_slack}

Das Paket `/whisk.system/slack` bietet eine komfortable Methode zur Verwendung der [Slack-APIs](https://api.slack.com/).

Das Paket enthält die folgenden Aktionen:

| Entität | Typ | Parameter | Beschreibung |
| --- | --- | --- | --- |
| `/whisk.system/slack` | Paket | url, channel, username | Interaktion mit der Slack-API |
| `/whisk.system/slack/post` | Aktion | text, url, channel, username | Senden einer Nachricht an einen Slack-Kanal |

Es wird empfohlen, eine Paketbindung mit den Werten `username`, `url` und `channel` zu erstellen. Mit der Bindung brauchen Sie die Werte nicht jedes Mal anzugeben, wenn Sie die Aktion im Paket aufrufen.

## Nachricht an einen Slack-Kanal senden

Die Aktion `/whisk.system/slack/post` sendet eine Nachricht an einen angegebenen Slack-Kanal. Die folgenden Parameter sind verfügbar:

- `url`: Die URL für den Slack-Web-Hook.
- `channel`: Der Slack-Kanal, an den die Nachricht zu senden ist.
- `username`: Der Name, unter dem die Nachricht gesendet werden soll.
- `text`: Ein zu sendender Nachrichtentext.
- `token`: (optional) Ein Slack-[Zugriffstoken](https://api.slack.com/tokens). Weitere Informationen zur Verwendung des Slack-Zugriffstokens finden Sie [unten](./catalog.md#using-the-slack-token-based-api).

Das folgende Beispiel zeigt die Konfiguration von Slack, die Erstellung einer Paketbindung und das Senden einer Nachricht an einen Kanal.

1. Konfigurieren Sie für Ihr Team einen [eingehenden Web-Hook](https://api.slack.com/incoming-webhooks) für Slack.
  
  Nach der Konfiguration von Slack erhalten Sie eine Web-Hook-URL, die ungefähr wie folgt aussieht: `https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Sie benötigen diese im nächsten Schritt.
  
2. Erstellen Sie eine Paketbindung mit Ihren Slack-Berechtigungsnachweisen, mit dem Kanal, an den gesendet werden soll, sowie mit dem Benutzernamen, unter dem gesendet werden soll.
  
  ```
  wsk package bind /whisk.system/slack mySlack \
    --param url "https://hooks.slack.com/services/..." \
    --param username "Bob" \
    --param channel "#MySlackChannel"
  ```
  {: pre}
  
3. Rufen Sie die Aktion `post` in Ihrer Paketbindung auf, um eine Nachricht an Ihren Slack-Kanal zu senden.
  
  ```
  wsk action invoke mySlack/post --blocking --result \
    --param text "Hello from OpenWhisk!"
  ```
  {: pre}
  

## Slack-Token-basierte API verwenden

Sie können auf Wunsch auch die Slack-Token-basierte API statt der Web-Hook-API verwenden. Übergeben Sie in einem solchen Fall in einem `Token` die Parameter, die Ihr Slack-[Zugriffstoken](https://api.slack.com/tokens) enthalten. Sie können dann eine beliebige [Slack-API-Methode](https://api.slack.com/methods) als Parameter `url` verwenden. Um beispielsweise eine Nachricht zu senden, verwenden Sie den Parameterwert `url` von [slack.postMessage](https://api.slack.com/methods/chat.postMessage).
