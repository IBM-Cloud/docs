---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilizzo del pacchetto Slack
{: #openwhisk_catalog_slack}

Il pacchetto `/whisk.system/slack` offre un pratico modo per utilizzare le [API Slack](https://api.slack.com/).

Il pacchetto include le seguenti azioni:

| Entità | Tipo | Parametri | Descrizione |
| --- | --- | --- | --- |
| `/whisk.system/slack` | pacchetto | url, channel, username | Interagire con la API Slack |
| `/whisk.system/slack/post` | azione | text, url, channel, username | Pubblicare un messaggio su un canale Slack |

Si consiglia di effettuare la creazione di un bind di pacchetto con i valori `username`, `url` e `channel`. Con il bind, non dovrai specificare i valori ogni volta che richiami l'azione nel pacchetto.

## Pubblicazione di un messaggio in un canale Slack

L'azione `/whisk.system/slack/post` pubblica un messaggio in uno specifico canale Slack. I parametri sono i seguenti:

- `url`: l'URL del webhook Slack.
- `channel`: il canale Slack nel quale pubblicare il messaggio.
- `username`: il nome con il quale pubblicare il messaggio.
- `text`: un messaggio da pubblicare.
- `token`: (facoltativo) un [token di accesso](https://api.slack.com/tokens) Slack. Vedi [sotto](./catalog.md#using-the-slack-token-based-api) per ulteriori dettagli sull'utilizzo dei token di accesso Slack.

Il seguente è un esempio di configurazione di Slack, creazione di un bind di pacchetto e pubblicazione di un messaggio in un canale.

1. Configura un [webhook in entrata](https://api.slack.com/incoming-webhooks) Slack per il tuo team.
  
  Dopo che Slack è stato configurato, ottieni un URL webhook simile a `https://hooks.slack.com/services/aaaaaaaaa/bbbbbbbbb/cccccccccccccccccccccccc`. Ti servirà nel prossimo passo.
  
2. Crea un bind di pacchetto con le tue credenziali Slack, il canale in cui vuoi pubblicare il messaggio e il nome utente con il quale vuoi farlo.
  
  ```
  wsk package bind /whisk.system/slack mySlack \
    --param url "https://hooks.slack.com/services/..." \
    --param username "Bob" \
    --param channel "#MySlackChannel"
  ```
  {: pre}
  
3. Richiama l'azione `post` nel tuo bind di pacchetto per pubblicare un messaggio nel canale Slack.
  
  ```
  wsk action invoke mySlack/post --blocking --result \
    --param text "Hello from OpenWhisk!"
  ```
  {: pre}
  

## Utilizzo dell'API basata sul token Slack

Se preferisci, puoi scegliere di utilizzare l'API basata su token Slack anziché l'API webhook. Se così fosse, devi passare un parametro `token` che contiene il tuo [token di accesso](https://api.slack.com/tokens) Slack. Puoi quindi utilizzare qualsiasi [metodo API Slack](https://api.slack.com/methods) come tuo parametro `url`. Ad esempio, per pubblicare un messaggio, puoi utilizzare il valore di parametro `url` [slack.postMessage](https://api.slack.com/methods/chat.postMessage).
