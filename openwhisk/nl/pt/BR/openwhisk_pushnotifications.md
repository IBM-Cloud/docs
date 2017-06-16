---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-01"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Usando o pacote Push Notifications
{: #openwhisk_catalog_pushnotifications}

O pacote `/whisk.system/pushnotifications` permite trabalhar com um serviço de push.

O pacote inclui a ação e o feed a seguir:

| Entidade | Tipo | Parâmetros | Descrição |
| --- | --- | --- | --- |
| `/whisk.system/pushnotifications` | pacote | appId, appSecret  | Trabalhar com o serviço de push |
| `/whisk.system/pushnotifications/sendMessage` | ação | text, url, deviceIds, platforms, userIds, tagNames, gcmCollapseKey, gcmCategory, gcmIcon, gcmDelayWhileIdle, gcmSync, gcmVisibility, gcmPayload, gcmPriority, gcmSound, gcmTimeToLive, gcmStyleType, gcmStyleTitle, gcmStyleUrl, gcmStyleText, gcmStyleLines, gcmLightsLedArgb, gcmLightsLedOnMs, gcmLightsLedOffMs, apnsBadge, apnsCategory, apnsIosActionKey, apnsPayload, apnsType, apnsSound, apnsTitleLocKey, apnsLocKey, apnsLaunchImage, apnsTitleLocArgs, apnsLocArgs, apnstitle, apnsSubtitle, apnsAttachmentUrl, fireFoxTitle, fireFoxIconUrl, fireFoxTimeToLive, fireFoxPayload, safariTitle, safariUrlArgs, safariAction, chromeTitle, chromeIconUrl, chromeTimeToLive, chromePayload, chromeAppExtTitle, chromeAppExtCollapseKey, chromeAppExtDelayWhileIdle, chromeAppExtIconUrl, chromeAppExtTimeToLive, chromeAppExtPayload | Enviar notificação push para um ou mais dispositivos especificados |
| `/whisk.system/pushnotifications/webhook` | alimentação | eventos | Disparar eventos acionadores nas atividades de dispositivo (registro, remoção de registro, assinatura, cancelamento de assinatura do dispositivo) no serviço de Push |
É sugerido criar uma ligação de pacote com os valores `appId` e
`appSecret`. Dessa forma, não será necessário especificar essas
credenciais toda vez que chamar as ações no pacote.

## Criando uma ligação de pacote de Push
{: #openwhisk_catalog_pushnotifications_create}

Ao criar uma ligação de pacote de Notificações push, deve-se especificar os parâmetros a seguir,

-  `appId`: o GUID do aplicativo Bluemix.
-  `appSecret`: o appSecret de serviço de notificação push do Bluemix.

A seguir está um exemplo de criação de uma ligação de pacote.

1. Crie um aplicativo Bluemix em [Bluemix Dashboard](http://console.ng.bluemix.net).

2. Inicialize o Serviço de Notificação Push e ligue o serviço ao aplicativo Bluemix

3. Configure o [aplicativo
de Notificação push](https://console.ng.bluemix.net/docs/services/mobilepush/index.html).

  Certifique-se de lembrar do `App GUID` e do `App Secret` do aplicativo Bluemix que você criou.

4. Crie uma ligação de pacote com as `/whisk.system/pushnotifications`.

  ```
  wsk package bind /whisk.system/pushnotifications myPush -p appId myAppID -p appSecret myAppSecret
  ```
  {: pre}
  
5. Verifique se a ligação do pacote existe.

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myPush private binding
  ```


## Enviando notificações push
{: #openwhisk_catalog_pushnotifications_send}

A ação `/whisk.system/pushnotifications/sendMessage` envia notificações push para dispositivos registrados. Os parâmetros são como segue:

- `text`: a mensagem de notificação a ser mostrada ao usuário. Por exemplo: `-p text "Hi ,OpenWhisk send a notification"`.
- `url`: uma URL opcional que pode ser enviada junto com o alerta. Por exemplo: `-p url "https:\\www.w3.ibm.com"`.
- `deviceIds` A lista de dispositivos especificados. Por exemplo: `-p deviceIds ["deviceID1"]`.
- `platforms` Envie notificação para os dispositivos das plataformas especificadas. 'A' para dispositivos Apple (iOS) e 'G' para dispositivos Google (Android). Por exemplo, `-p platforms ["A"]`.
- `userIds` - Envie notificação para os dispositivos dos usuários especificados. Por exemplo: `-p userIds "[\"testUser\"]"`
- `tagNames` Envie notificação para os dispositivos que foram inscritos em qualquer uma dessas tags. Por exemplo, `-p tagNames "[\"tag1\"]" `.

- `gcmCollapseKey`: esse parâmetro identifica um grupo de mensagens
- `gcmCategory` - O identificador de categoria a ser usado para as notificações push interativas.
- `gcmIcon` - Especifique o nome do ícone a ser exibido para a notificação. Certifique-se de que o ícone já esteja empacotado com o aplicativo cliente.
- `gcmDelayWhileIdle`: quando esse parâmetro é configurado como verdadeiro, ele indica que a mensagem não será enviada até que o dispositivo fique ativo.
- `gcmSync`: as mensagens do grupo de dispositivos torna possível a cada instância do app em um grupo refletir o estado mais recente do sistema de mensagens.
- `gcmVisibility`: privada/pública - a visibilidade dessa notificação, que afeta como e quando as notificações são reveladas em uma tela bloqueada segura.
- `gcmPayload`: carga útil de JSON customizada que será enviada como parte da mensagem de notificação. Por exemplo: `-p gcmPayload "{\"hi\":\"hello\"}"`
- `gcmPriority`: configura a prioridade da mensagem.
- `gcmSound`: o arquivo de som (no dispositivo) que tentará ser reproduzido quando a notificação chegar no dispositivo.
- `gcmTimeToLive`: esse parâmetro especifica por quanto tempo (em segundos) a mensagem será mantida no armazenamento de GCM se o dispositivo estiver off-line.
- `gcmStyleType`: especifica os tipos de notificações expansíveis. Os valores possíveis são `bigtext_notification`, `picture_notification`, `inbox_notification`.
- `gcmStyleTitle`: especifica o título da notificação. O título é exibido quando a notificação é expandida. O título deve ser especificado para todas as três notificações expansíveis.
- `gcmStyleUrl`: uma URL da qual a imagem precisa ser obtida para a notificação. Deve ser especificado para `picture_notification`.
- `gcmStyleText`: o texto grande que precisa ser exibido ao expandir um `bigtext_notification`. Deve ser especificado para `bigtext_notification`.
- `gcmStyleLines`: uma matriz de sequências que deve ser exibida no estilo de caixa de entrada para `inbox_notification`. Deve ser especificado para `inbox_notification`.
- `gcmLightsLedArgb` - A cor do led. O hardware fará a melhor aproximação.
- `gcmLightsLedOnMs` - O número de milissegundos que o LED deve estar ativo enquanto está piscando. O hardware fará a melhor aproximação.
- `gcmLightsLedOffMs` - O número de milissegundos que o LED deve estar inativo enquanto está piscando. O hardware fará a melhor aproximação.

- `apnsBadge`: o número a ser exibido como o badge do ícone do aplicativo.
- `apnsCategory`: o identificador de categoria a ser usado para as notificações push interativas.
- `apnsIosActionKey`: o título da chave Ação.
- `apnsPayload`: carga útil de JSON customizada que será enviada como parte da mensagem de notificação.
- `apnsType`: ['DEFAULT', 'MIXED', 'SILENT'].
- `apnsSound`: o nome do arquivo de som no pacote configurável do aplicativo. O som desse arquivo é reproduzido como um alerta.
- `apnsTitleLocKey` - A chave para uma sequência de títulos no arquivo Localizable.strings da localização atual. A sequência chave de caracteres pode ser formatada com especificadores %@ e %n$@ para usar as variáveis especificadas na matriz `titleLocArgs`.
- `apnsLocKey` - Uma chave para uma sequência de mensagem de alerta em um arquivo Localizable.strings da localização atual (que é configurada pela preferência de idioma do usuário). A sequência chave de caracteres pode ser formatada com especificadores %@ e %n$@ para usar as variáveis especificadas na matriz locArgs.
- `apnsLaunchImage` - O nome de um arquivo de imagem no pacote configurável do app, com ou sem a extensão do nome do arquivo. A imagem é usada como a imagem de ativação quando os usuários tocam no botão de ação ou movem a régua de controle da ação.
- `pnsTitleLocArgs` - Valores de sequência variável que devem aparecer no lugar dos especificadores de formato em `title-loc-key`.
- `apnsLocArgs` - Valores de sequência variável que devem aparecer no lugar dos especificadores de formato em `locKey`.
- `apnstitle` - O título de Notificações push Rich (Suportado apenas no iOS 10 e acima).
- `apnsSubtitle` - O subtítulo das Notificações Rich. (Suportado apenas no iOS 10 e acima).
- `apnsAttachmentUrl` - O link para a mídia de notificações de iOS (vídeo, áudio, GIF, imagens - Suportado apenas no iOS 10 e acima).

- `fireFoxTitle`: especifica o título a ser configurado para a Notificação WebPush.
- `fireFoxIconUrl`: a URL do ícone a ser configurado para a Notificação WebPush.
- `fireFoxTimeToLive`: esse parâmetro especifica quanto tempo (em segundos) a mensagem deverá ser mantida no armazenamento de GCM se o dispositivo estiver off-line.
- `fireFoxPayload`: a carga útil de JSON customizada que será enviada como parte da mensagem de notificação.

- `chromeTitle`: especifica o título a ser configurado para a Notificação WebPush.
- `chromeIconUrl`: a URL do ícone a ser configurado para a Notificação WebPush.
- `chromeTimeToLive`: esse parâmetro especifica quanto tempo (em segundos) a mensagem deverá ser mantida no armazenamento de GCM se o dispositivo estiver off-line.
- `chromePayload`: a carga útil de JSON customizada que será enviada como parte da mensagem de notificação.

- `safariTitle` - Especifica o título a ser configurado para o Safari Push Notifications.
- `safariUrlArgs` - Os argumentos de URL que precisam ser usados com esta notificação. Isso precisa ser fornecido na forma de uma Matriz JSON.
- `safariAction` - O rótulo do botão de ação.

- `chromeAppExtTitle`: especifica o título a ser configurado para a Notificação WebPush.
- `chromeAppExtCollapseKey`: esse parâmetro identifica um grupo de mensagens.
- `chromeAppExtDelayWhileIdle`: quando esse parâmetro é configurado como true, ele indica que a mensagem não deve ser enviada até o dispositivo ficar ativo.
- `chromeAppExtIconUrl`: a URL do ícone a ser configurado para a Notificação WebPush.
- `chromeAppExtTimeToLive`: esse parâmetro especifica quanto tempo (em segundos) a mensagem deverá ser mantida no armazenamento de GCM se o dispositivo estiver off-line.
- `chromeAppExtPayload`: a carga útil de JSON customizada que será enviada como parte da mensagem de notificação.

Aqui está um exemplo de envio de notificação push do pacote *pushnotification*.

- Envie uma notificação push usando a ação `sendMessage` na ligação de pacote anteriormente criada. Certifique-se de substituir `/myNamespace/myPush` pelo nome de seu pacote.

  ```
  wsk action invoke /myNamespace/myPush/sendMessage --blocking --result  -p url https://example.com -p text "this is my message"  -p sound soundFileName -p deviceIds "[\"T1\",\"T2\"]"
  ```
  {: pre}
  ```json
     {
    "result": {
    "pushResponse": 
      {
        "messageId":"11111H",
        "message":{
          "alert":"this is my message",
          "url":""
        },
        "settings":{
          "apns":{
            "sound":"default"
          },
          "gcm":{
            "sound":"default"
            },
          "target":{
            "deviceIds":["T1","T2"]
          }
        }
      }
    },
      "status": "success",
      "success": true
  }
  ```


## Disparando um evento acionador na atividade do serviço Push Notifications
{: #openwhisk_catalog_pushnotifications_fire}

O `/whisk.system/pushnotifications/webhook` configura o serviço de
push para disparar um acionador quando houver uma atividade de
dispositivo, como registro/remoção de registro ou assinatura/cancelamento
de assinatura de registro em um aplicativo especificado

Os parâmetros são como segue:

- `appId:` o GUID do app Bluemix.
- `appSecret`: o appSecret do serviço de notificação push do Bluemix.
- `events:` os eventos suportados são `onDeviceRegister`, `onDeviceUnregister`, `onDeviceUpdate`, `onSubscribe`,
`onUnsubscribe`. Para ser notificado de todos os eventos use o caractere curinga `*`.

Segue um exemplo de criação de um acionador que será disparado toda vez que houver um novo dispositivo registrado no aplicativo de serviço de Notificações push.

1. Crie uma ligação de pacote configurada para seu serviço de Notificações push com appId e appSecret.

  ```
  wsk package bind /whisk.system/pushnotifications myNewDeviceFeed --param appID myapp --param appSecret myAppSecret --param events onDeviceRegister
  ```
  {: pre}

2. Crie um acionador para o tipo de evento `onDeviceRegister` do serviço de Notificações push usando o feed `myPush/webhook`.

  ```
  wsk trigger create myPushTrigger --feed myPush/webhook --param events onDeviceRegister
  ```
  {: pre}

3. Você poderia criar uma regra que envia uma mensagem cada vez que um novo dispositivo é registrado. Crie uma nova regra usando a ação e o acionador anteriores.

  ```
  wsk rule create --enable myRule myPushTrigger sendMessage
  ```
  {: pre}

  Verifique os resultados no `wsk activation poll`.

  Registre um dispositivo em seu aplicativo Bluemix, é possível ver o `rule`, `trigger` e `action` sendo executados no openWhisk [painel] (https://console.{Domain}/openwhisk/dashboard).

  A ação enviará uma notificação push.

