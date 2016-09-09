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
*Última atualização: 1 de agosto de 2016*
{: .last-updated}

Use o serviço {{site.data.keyword.mobileanalytics_full}} para medir o estado, o comportamento e o contexto de seus aplicativos móveis, usuários móveis e dispositivos móveis.
{: shortdesc}

Para deixar o serviço {{site.data.keyword.mobileanalytics_short}} funcionando rapidamente, siga estas etapas:

1. Depois de [criar uma instância](https://console.{DomainName}/docs/services/reqnsi.html#req_instance) do serviço {{site.data.keyword.mobileanalytics_short}}, é possível acessar o Console do {{site.data.keyword.mobileanalytics_short}} clicando em seu ladrilho na seção Serviços do Painel do {{site.data.keyword.Bluemix}}.

  **Importante:** ao abrir inicialmente seu
serviço Mobile Analytics recém-criado, uma janela poderá ser exibida
para confirmar que você permite que o {{site.data.keyword.Bluemix_notm}} forneça as informações necessárias para o serviço sobre si, para que o serviço possa validar sua identidade. Clique em **Confirmar** para continuar no console do {{site.data.keyword.mobileanalytics_short}}. Se você cancelar, o console do {{site.data.keyword.mobileanalytics_short}} não será aberto.
2. Instale os [SDKs do cliente](install-client-sdk.html) do {{site.data.keyword.mobileanalytics_short}}.
3. Importe os SDKs do cliente e inicialize-os com o fragmento de código a seguir para registrar a análise de uso.
  #### Android
  {: #android-initialize}
  1. Importe o SDK do cliente:
		
		```
		import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
		import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
		```

  2. Obtenha seu valor da [Chave de acesso](sdk.html#analytics-clientkey).
  3. Inicialize o SDK do Cliente dentro do seu código do aplicativo para registrar a
análise de uso e as sessões de aplicativo.
		
		```Java
		try {
		        BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH);
			}
			catch (MalformedURLException e) {
		        Log.e("your_app_name","URL should not be malformed:  " + e.getLocalizedMessage());
		    }
		   Analytics.init(getApplication(), "your_app_name", "your_access_key", Analytics.DeviceEvent.LIFECYCLE);
		```
    O parâmetro **bluemixRegion** especifica qual implementação do Bluemix você está usando, por exemplo, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` ou `BMSClient.REGION_SYDNEY`.

  #### iOS
  {: #ios-initialize}
  1. Importe as estruturas `BMSCore` e `BMSAnalytics`:

    ```
    import BMSCore
    import BMSAnalytics
    ```

  2. Obtenha seu valor da [Chave de acesso](sdk.html#analytics-clientkey).

  3. Inicialize o SDK do Cliente dentro do seu código do aplicativo para registrar a
análise de uso e as sessões de aplicativo.
	
	```Swift
	BMSClient.sharedInstance.initializeWithBluemixAppRoute("nil",bluemixAppGUID: "nil", bluemixRegion: BMSClient.REGION_US_SOUTH) //You can change the region
	Analytics.initializeWithAppName("your_app_name", accessKey: "your_access_key", deviceEvents: DeviceEvent.LIFECYCLE)
	```

    O parâmetro **bluemixRegion** especifica qual implementação do Bluemix você está usando, por exemplo, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` ou `BMSClient.REGION_SYDNEY`.

4. Envie análise de uso registrada para o Mobile Analytics Service. Uma maneira simples de testar a análise é executar o código a seguir quando o aplicativo for iniciado:

	#### Android
	{: #android-send}
	
	É possível incluir o método `Analytics.send()` no método `onCreate` da atividade principal em seu aplicativo Android ou em um local que funcione melhor para o projeto.
	
	```
	Analytics.send(new ResponseListener() {
	    @Override
	    public void onSuccess(Response response) {
	        Log.d("your_app_name", "Successfully sent analytics: " + response.toString());
	    }
		
	    @Override
	    public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
	        Log.e("your_app_name", "Failed to send analytics: ");
	        if (response != null) {
	            Log.e("your_app_name", response.toString());
	        }
	        if (throwable != null) {
	            Log.e("your_app_name","Stack trace: ", throwable);
	        }
	    }
	});
	```
	
	#### iOS
	{: #ios-send}
	
	
	Use o método `Analytics.send` para enviar os dados de análise para o servidor. Coloque o método `Analytics.send` no método `application(_:didFinishLaunchingWithOptions:)` de seu delegado do aplicativo ou em um local que funcione melhor para o seu projeto. 
		
	```
	Analytics.send { (response: Response?, error: NSError?) in
	  if response?.statusCode == 201 {
	      print("Successfully sent analytics: \(response?.responseText)")
	  }
	  else {
	      print("Failed to send analytics: \(response?.responseText). Error: \(error?.localizedDescription)")
	  }
	}
	```
Veja o tópico [Instrumentando seu aplicativo](sdk.html).
5. Compile e execute o aplicativo em seu emulador ou dispositivo.

6. Acesse **Painel** do {{site.data.keyword.mobileanalytics_short}} para ver a análise de uso, como novos dispositivos e total de dispositivos usando o aplicativo. Também é possível monitorar seu aplicativo ao <!-- [creating custom charts](app-monitoring.html#custom-charts), --> [configurar alertas](app-monitoring.html#alerts) e [monitorar travamentos do aplicativo](app-monitoring.html#monitor-app-crash). 


# rellinks

## SDK
* [SDK Android ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK iOS ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
