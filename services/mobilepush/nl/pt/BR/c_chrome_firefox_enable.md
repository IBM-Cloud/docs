---

copyright:
 years: 2015 2016

---


# Ativando aplicativos da web para receber o {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Última atualização: 17 de outubro de 2016
{: .last-updated}

Agora é possível ativar os aplicativos da web Google Chrome e Mozilla Firefox para receber o {{site.data.keyword.mobilepushshort}}.

## Instalando o SDK do cliente do navegador da web para {{site.data.keyword.mobilepushshort}}
{: #web_install}

Este tópico descreve como instalar e usar o SDK de Push do JavaScript do cliente para desenvolver ainda mais os seus aplicativos da web.

### Inicialização no aplicativo da web Google Chrome

Para instalar o SDK do Javascript no aplicativo da web Chrome, conclua as etapas:

Faça download do `BMSPushSDK.js`, do `BMSPushServiceWorker.js` e do `manifest_Website.json` a partir do
[SDK de push da Web do Bluemix](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master).

1. Edite o arquivo `manifest_Website.json`.

Para o navegador Google Chrome, mude `name` para o nome do seu site. Mude `gcm_sender_id` para o seu ID do emissor do Firebase Cloud Messaging
(FCM) ou do Google Cloud Messaging (GCM). Para obter mais informações, consulte
[Documentação
do Google](https://developers.google.com/web/fundamentals/getting-started/codelabs/push-notifications/#make_a_project_on_the_google_developer_console). O valor gcm_sender_id contém somente números.

```
 {
  "name": "YOUR_WEBSITE_NAME",
      "gcm_sender_id": "GCM_Sender_Id"
 }
```
    {: codeblock}
 
Para o navegador Mozilla Firefox, inclua os valores a seguir no arquivo `manifest.json`.     Mude `name` para o nome do seu
site.

```
{
  "name": "YOUR_WEBSITE_NAME"
 }
```
    {: codeblock}

2. Mude o nome do arquivo `manifest_Website.json` para `manifest.json`.
3. Inclua o `BMSPushSDK.js`, `BMSPushServiceWorker.js` e `manifest.json` em seu diretório-raiz.
3. Inclua o `manifest.json` na tag `<head>` de seu arquivo html.
```
 <link rel="manifest" href="manifest.json">
```
    {: codeblock}
4. Inclua o Bluemix Web push SDK no aplicativo da web a partir do GitHub.
```
 <script src="BMSPushSDK.js" async></script>
```
    {: codeblock}

## Inicializando o Web Push SDK 
{: #web_initialize}

Inicialize o push SDK com o `app GUID` e `app Region` do serviço Bluemix {{site.data.keyword.mobilepushshort}}.  

Para obter o GUID do app, selecione a opção **Configuração** na área de janela de navegação para seus serviços de push inicializados e clique em **Opções móveis**. Modifique o fragmento de código para usar o parâmetro appGUID do serviço de notificações push do Bluemix.

O `App Region` especifica o local no qual o serviço {{site.data.keyword.mobilepushshort}} é hospedado. É possível usar um destes três valores:

 - Para Dalas EUA:	 `.ng.bluemix.net`
 - Para Reino Unido:			 `.eu-gb.bluemix.net`
 - Para Sydney:		 `.au-syd.bluemix.net`

```
 var bmsPush = new BMSPush();
    function callback(response) {
 alert(response.response)
    }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
   "clientSecret":"clientSecret of your push service"
    }
  bmsPush.initialize(params, callback)
```
	{: codeblock}

## Registrando o aplicativo da web
{: #web_register}

Use a API `register()` para registrar o dispositivo no serviço
{{site.data.keyword.mobilepushshort}}. Para o registro a partir do Google Chrome, inclua a Chave API do Firebase Cloud Messaging (FCM) ou do Google Cloud
Messaging (GCM) e a URL do website no painel de configuração da web de serviço {{site.data.keyword.mobilepushshort}} do Bluemix. Para obter mais informações, consulte [Configurando as credenciais do Google Cloud Messaging](t_push_provider_android.html) na configuração do Chrome.

Para registro a partir do Mozilla Firefox, inclua a URL do website no painel de configuração da web do serviço Bluemix {{site.data.keyword.mobilepushshort}} na configuração do Firefox.

Use o fragmento de código a seguir para registrar o serviço Bluemix
{{site.data.keyword.mobilepushshort}}.
```
var bmsPush = new BMSPush();
    function callback(response) {
     alert(response.response)
    }
  var initParams = {
  "appGUID":"push app GUID",
  "appRegion":"Region where service hosted",
  "clientSecret":"clientSecret of your push service"
  }
  bmsPush.initialize(params, callback)
    bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}

## Enviando {{site.data.keyword.mobilepushshort}} básicas
  {: #send}

Depois de ter desenvolvido seus aplicativos, é possível enviar uma notificação push. 

1. Selecione **Enviar notificações** e componha uma mensagem escolhendo **Notificações da web** como a opção **Enviar para**. 
2. Digite a mensagem que precisa ser entregue no campo **Mensagem**.
3. É possível optar por fornecer configurações opcionais:
  - **Título da notificação**: esse é o texto que seria exibido como título de alerta de mensagem.
  - **URL do ícone de notificação**: se sua mensagem precisar ser entregue com um ícone de notificação de app, forneça o link para o ícone no campo.
  - **Carga útil adicional**: especifica os valores de carga útil customizados para suas notificações.

A imagem a seguir mostra a opção de notificações da web no painel.

  ![Tela de notificações](images/DashboardWebpush.jpg)
  
## Etapas Seguintes
  {: #next_steps_tags}

Depois de configurar com êxito notificações básicas,
é possível configurar notificações baseadas em tag e opções
avançadas.

Inclua esses recursos do serviço {{site.data.keyword.mobilepushshort}} em seu app. Para usar notificações baseadas em tag, consulte [Notificações baseadas em tag](c_tag_basednotifications.html). Para
usar opções de notificações avançadas, veja [Notificações avançadas](t_advance_badge_sound_payload.html).



