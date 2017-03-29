---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Ativando aplicativos da web para receber o {{site.data.keyword.mobilepushshort}}
{: #web_notifications}
Última atualização: 16 de fevereiro de 2017
{: .last-updated}

É possível ativar os aplicativos da web Google Chrome, Mozilla Firefox e Safari para receber o
{{site.data.keyword.mobilepushshort}}. Assegure-se de que você tenha passado por [Configurando credenciais para um provedor de notificação](t__main_push_config_provider.html) antes de continuar com as etapas.

## Instalando o SDK do cliente do navegador da web para {{site.data.keyword.mobilepushshort}}
{: #web_install}

Este tópico descreve como instalar e usar o SDK de Push do JavaScript do cliente para desenvolver ainda mais os seus aplicativos da web.

### Inicializando no aplicativo da web

Para instalar o SDK do Javascript no aplicativo da web do Google Chrome, conclua as etapas:

Faça download dos arquivos `BMSPushSDK.js`, `BMSPushServiceWorker.js` e
`manifest_Website.json` por meio do
[SDK
de push da web do Bluemix](https://codeload.github.com/ibm-bluemix-mobile-services/bms-clientsdk-javascript-webpush/zip/master){: new_window}.

1. Edite o arquivo `manifest_Website.json`.
	- Para o navegador Google Chrome, mude `name` para o nome do seu site. Por
exemplo, `www.dailynewsupdates.com`. Mude o
`gcm_sender_id` para o seu sender_ID do Firebase Cloud Messaging
(FCM) ou do Google Cloud Messaging (GCM). Para obter mais
informações, veja [Obtendo o seu ID de
emissor e chave API](t_push_provider_android.html). O valor gcm_sender_id contém somente números.

		```
			{
	"name": "YOUR_WEBSITE_NAME",
  			"gcm_sender_id": "GCM_Sender_Id"
			 }
		```
    		{: codeblock}
 
	- Para o navegador Mozilla Firefox, inclua os valores a seguir no arquivo `manifest_Website.json`. Forneça
um `name` apropriado. Isso seria o nome de seu website.

		```
			{ 
	"name": "YOUR_WEBSITE_NAME"
			 }
		```
    		{: codeblock}

2. Mude o nome do arquivo `manifest_Website.json` para `manifest.json`.
3. Inclua o `BMSPushSDK.js`,
`BMSPushServiceWorker.js` e
`manifest.json` no diretório-raiz do seu website.
3. Inclua o `manifest.json` na tag `<head>` de seu arquivo html.
	```
		<link rel="manifest" href="manifest.json">
	```
    	{: codeblock}
4. Inclua o SDK de push da web do Bluemix em seu aplicativo da web.
	```
		<script src="BMSPushSDK.js" async></script>
	```
    	{: codeblock}

**Nota**: assegure-se de que o código seja implementado e que o link de amostra seja acessado usando `https` e não `http`. 

## Inicializando o Web Push SDK 
{: #web_initialize}

Inicialize o SDK de push com o `app GUID` e o `app Region` do Bluemix {{site.data.keyword.mobilepushshort}}.  

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
  "websitePushIDSafari": "Optional parameter for Safari Push Notifications only. The value should match the website Push ID provided during the server side configuration."
  }
  	bmsPush.initialize(initParams, callback)
```
	{: codeblock}

**Nota**: se suas credenciais de FCM forem mudadas para SDK de push da web, a
entrega da mensagem poderá falhar para o navegador Chrome. Assegure-se de chamar
`bmsPush.unRegisterDevice` para evitar falha.

Você poderá ver erros relacionados à configuração se fornecer um parâmetro errado. Para obter mais informações, veja [Resolvendo erros de configuração Push da web](troubleshooting_config_errors.html).

## Registrando o aplicativo da web
{: #web_register}

Use a API **register()** para registrar o dispositivo no serviço
{{site.data.keyword.mobilepushshort}}. Use qualquer uma das
opções a seguir, com base em seu navegador.

- Para o registro a partir do Google Chrome, inclua a Chave API do Firebase Cloud Messaging (FCM) ou do Google Cloud
Messaging (GCM) e a URL do website no painel de configuração da web de serviço {{site.data.keyword.mobilepushshort}} do Bluemix. Para obter mais informações, consulte [Configurando as credenciais do Google Cloud Messaging](t_push_provider_android.html) na configuração do Chrome.

- Para registro a partir do Mozilla Firefox, inclua a URL do website no painel de configuração da web do serviço Bluemix {{site.data.keyword.mobilepushshort}} na configuração do Firefox.

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
  "websitePushIDSafari": "Optional parameter for Safari Push Notifications only. The value should match the website Push ID provided during the server side configuration."
  }
  bmsPush.initialize(params, callback)
    bmsPush.register(function(response) {
    alert(response.response)
  })
```
    {: codeblock}






