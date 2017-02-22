---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Ativando os Apps Chrome e Extensões para receber {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Última atualização: 18 de janeiro de 2017
{: .last-updated}

É possível ativar os Apps Chrome e Extensões para receber o {{site.data.keyword.mobilepushshort}}. Assegure-se de que você tenha passado por [Configurando credenciais para um provedor de notificação](t__main_push_config_provider.html) antes de continuar com as etapas.

## Instalando o SDK do cliente para {{site.data.keyword.mobilepushshort}}
{: #web_install}

Este tópico descreve como instalar e usar o SDK de Push do JavaScript do cliente para desenvolver ainda mais os seus Apps Chrome e Extensões.

### Inicialização nos Apps Google Chrome e Extensões

Para instalar o SDK do Javascript nos Apps Chrome e Extensões, conclua as etapas:

Faça download do `BMSPushSDK.js` e do `manifest_Chrome_Ext.json` (para Extensões do Chrome) ou do `manifest_Chrome_App.json` (para Apps Chrome) a partir do [SDK de push da web do Bluemix ![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master "Ícone de link externo"){: new_window}.



- Para Apps Chrome, configure o arquivo manifest:
 1. No arquivo `manifest_Chrome_App.json`, forneça o nome, a descrição e os ícones.
 2. Inclua o `BMSPushSDK.js` no `app.background.scripts`.
 3. Mude o `manifest_Chrome_App.json` para `manifest.json`.

- Para Extensões do Chrome, configure o arquivo manifest:
 1. No arquivo `manifest_Chrome_Ext.json` forneça o nome, a descrição e os ícones.
 2. Inclua o `BMSPushSDK.js` no `background.scripts`.
 3. Mude o `manifest_Chrome_Ext.json` para `manifest.json`.

No arquivo `background.js` inclua o seguinte para receber notificações push 
```
chrome.gcm.onMessage.addListener(BMSPushBackground.onMessageReceived)
chrome.notifications.onClicked.addListener(BMSPushBackground.notification_onClicked);
chrome.notifications.onButtonClicked.addListener(BMSPushBackground.notifiation_buttonClicked); 
```
	{: codeblock}



## Inicializando o SDK de Push 
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

## Registrando os Apps Chrome e Extensões
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




