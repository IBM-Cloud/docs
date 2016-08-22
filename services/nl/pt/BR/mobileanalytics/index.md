---

copyright:
  years: 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introdução ao {{site.data.keyword.mobileanalytics_short}} (Experimental)  

{: #gettingstartedtemplate}
*Última atualização: 1 de julho de 2016*
{: .last-updated}

Use o serviço {{site.data.keyword.mobileanalytics_full}} para medir o estado, o comportamento e o contexto de seus aplicativos móveis, usuários móveis e dispositivos móveis.
{: shortdesc}

Para deixar o serviço {{site.data.keyword.mobileanalytics_short}} funcionando rapidamente, siga estas etapas:

1. Depois de [criar uma instância](https://console.{DomainName}/docs/services/reqnsi.html#req_instance) do serviço {{site.data.keyword.mobileanalytics_short}}, é possível acessar o Console do {{site.data.keyword.mobileanalytics_short}} clicando em seu ladrilho na seção Serviços do Painel do {{site.data.keyword.Bluemix}}.

  **Importante:** ao abrir inicialmente seu
serviço Mobile Analytics recém-criado, uma janela poderá ser exibida
para confirmar que você permite que o {{site.data.keyword.Bluemix_notm}} forneça as informações necessárias para o serviço sobre si, para que o serviço possa validar sua identidade. Clique em **Confirmar** para continuar no console do {{site.data.keyword.mobileanalytics_short}}. Se você cancelar, o console do {{site.data.keyword.mobileanalytics_short}} não será aberto.

2. Instale os [SDKs do cliente](install-client-sdk.html) do {{site.data.keyword.mobileanalytics_short}}. Opcionalmente,
é possível usar o {{site.data.keyword.mobileanalytics_short}}
[REST API](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}.

3. Importe os SDKs do cliente e inicialize-os com o fragmento de código a seguir para registrar a análise de uso.

	#### Android
	{: #android-initialize}
	1. Importe o SDK do cliente:

		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```
	2. Inicialize o SDK do cliente dentro de seu código do aplicativo para registrar a análise de uso e as sessões de aplicativo, usando o valor da
[chave de acesso](sdk.html#analytics-clientkey). 

		```Java
			try {
			     BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH);
			}
			catch (MalformedURLException e) {
	            //The Bluemix region provided is invalid
	        }
				Analytics.init(getApplication(), your_app_name, your_access_key, Analytics.DeviceEvent.LIFECYCLE);
		```
    O parâmetro **bluemixRegion** especifica qual implementação do Bluemix você está usando, por exemplo, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` ou `BMSClient.REGION_SYDNEY`.

  #### iOS
  {: #ios-initialize}
  1. Importe as estruturas `BMSCore` e `BMSAnalytics`:
  ```
    import BMSCore
    import BMSAnalytics
    ```
  2. Inicialize o SDK do cliente dentro de seu código do
aplicativo para registrar a análise de uso e as sessões de
aplicativo, usando o valor da
[chave de acesso](sdk.html#analytics-clientkey). 
 
	```Swift
	BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH) //You can change the region
	Analytics.initializeWithAppName(your_app_name, apiKey: your_access_key, deviceEvents: DeviceEvent.LIFECYCLE)
	```
   O parâmetro **bluemixRegion** especifica qual implementação do Bluemix você está usando, por exemplo, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` ou `BMSClient.REGION_SYDNEY`.

4. Envie análise de uso registrada para o Mobile Analytics Service. Uma maneira simples de testar a análise é executar o código a seguir quando o aplicativo for iniciado:

	#### Android
	{: #android-send}

	É possível incluir o método `Analytics.send()` no método `onCreate` da atividade principal em seu aplicativo Android ou em um local que funcione melhor para o projeto.

	```
	Analytics.send();
	```

	#### iOS
	{: #ios-send}

	Use o método `Analytics.send` para enviar os dados de análise para o servidor. Coloque o método `Analytics.send` no método `application(_:didFinishLaunchingWithOptions:)` de seu delegado do aplicativo ou em um local que funcione melhor para o seu projeto.

	```
	Analytics.send()
	```

	Leia o tópico [Instrumentando seu aplicativo](sdk.html).
5. Compile e execute o aplicativo em seu emulador ou dispositivo.

6. Acesse **Painel** do {{site.data.keyword.mobileanalytics_short}} para ver a análise de uso, como novos dispositivos e total de dispositivos usando o aplicativo. 
Também é possível monitorar o seu aplicativo ao <!--[creating custom charts](app-monitoring.html#custom-charts),-->[configurar
alertas](app-monitoring.html#alerts) e
[monitorar
travamentos do aplicativo](app-monitoring.html#monitor-app-crash).


# rellinks

## SDK
* [SDK Android ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK iOS ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}

## Referência da API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
