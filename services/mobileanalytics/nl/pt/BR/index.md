---

copyright:
  years: 2016
lastupdated: "2016-11-30"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introdução ao {{site.data.keyword.mobileanalytics_short}} (Beta)

{: #gettingstartedtemplate}

O {{site.data.keyword.mobileanalytics_full}} fornece aos desenvolvedores, administradores de TI e partes interessadas nos negócios insight sobre como seus apps móveis estão sendo executados e como estão sendo usados. Monitore desempenho e uso de todos os seus aplicativos da sua área de trabalho ou tablet. Identifique rapidamente tendências e anomalias, realize drill down para resolver os problemas e acione alertas quando Key Metrics atingir um limite crítico. 
{: shortdesc}

Para deixar o serviço {{site.data.keyword.mobileanalytics_short}} funcionando rapidamente, siga estas etapas:

1. Após você criar uma instância
<!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->do serviço
{{site.data.keyword.mobileanalytics_short}}, será possível acessar o Console do {{site.data.keyword.mobileanalytics_short}} clicando em seu
tile na seção **Serviços** do Painel do {{site.data.keyword.Bluemix}}.

 O serviço {{site.data.keyword.mobileanalytics_short}} é ativado com **modo de demo** ativado. O modo de demo preenche gráficos nas
páginas **DADOS DO APLICATIVO** e **ALERTAS**, de forma que você possa ver como os seus dados serão exibidos. É possível
desativar o modo de demo quando você tem os seus próprios dados. O console do {{site.data.keyword.mobileanalytics_short}} é somente leitura quando no modo de
demo; portanto, você não poderá criar novas definições de alerta.

2. Instale os [SDKs do cliente](/docs/services/mobileanalytics/install-client-sdk.html) {{site.data.keyword.mobileanalytics_short}}. É possível, opcionalmente, usar a [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window} do {{site.data.keyword.mobileanalytics_short}}.

3. Importe os SDKs do cliente e inicialize-os com o fragmento de código a seguir para
registrar a analítica de uso:

	#### Android
	{: #android-import}

	Inclua as seguintes instruções `importar`
no início do seu arquivo de projeto:
	
    ```
    import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
    ```
    {: codeblock}
  
 #### iOS
 {: #ios-import}
	
 **Nota:** o SDK Swift está disponível
para iOS e watchOS.
	
 Importe as estruturas `BMSCore` e `BMSAnalytics` ao incluir as instruções de `importação` a seguir no início do seu arquivo de
projeto `AppDelegate.swift`:

   ```Swift
  import BMSCore
  import BMSAnalytics
   ```
   {: codeblock}  
   
 #### Cordova
 {: #cordova-import}
		
 Inclua o plug-in Cordova executando o comando a seguir por meio do diretório-raiz do
seu aplicativo Cordova:

 ```Javascript
   cordova plugin add bms-core
   ```
 {: codeblock}  

4. Inicialize o SDK do cliente do {{site.data.keyword.mobileanalytics_short}}
em seu código do aplicativo para registrar a analítica de uso e as sessões do aplicativo usando
o valor [API Key](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).	
	
 #### Android
 {: #android-initialize}	

  ```
  BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // You can change the region
  Analytics.init(getApplication(), "your_app_name_here", "your_api_key_here", hasUserContext, Analytics.DeviceEvent.ALL);
  ```
  {: codeblock}
    
 O parâmetro **bluemixRegion** especifica qual implementação do {{site.data.keyword.Bluemix_notm}} você está usando, por exemplo,
`BMSClient.REGION_US_SOUTH` e `BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.Region.Sydney`.-->

 #### iOS
 {: #ios-initialize}
  
  Inicialize o Client SDK dentro de seu código de aplicativo para registrar a analítica de uso e as sessões de aplicativo, usando o valor da [Chave API](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).
	
  ```Swift
		BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // You can change the region
		Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: deviceEvents: .lifecycle, .network)
  ```
  {: codeblock}
			
   O parâmetro **bluemixRegion** especifica
qual implementação do Bluemix você está usando, por exemplo,
`BMSClient.Region.usSouth` ou
`BMSClient.Region.unitedKingdom`.
	<!-- , or `BMSClient.REGION_SYDNEY`. -->
	
 #### Cordova
 {: #cordova-initialize}
	
 Inicialize o Client SDK dentro de seu código de aplicativo para registrar a analítica de uso e as sessões de aplicativo, usando o valor da [Chave API](/docs/services/mobileanalytics/sdk.html#analytics-clientkey).
	
  ```
  var appName = "your_app_name_here";
  var apiKey = "your_api_key_here";
	
  BMSClient.initialize(BMSClient.REGION_US_SOUTH); // You can change the region
  BMSAnalytics.initialize(appName, apiKey, false, [BMSAnalytics.ALL])
  ```
  {: codeblock}
  
  O parâmetro **bluemixRegion** especifica qual implementação do {{site.data.keyword.Bluemix_notm}} você está usando, por exemplo,
`BMSClient.REGION_US_SOUTH` e `BMSClient.REGION_UK`.
  
 **Nota:** o nome que você selecionar para o seu aplicativo (`your_app_name_here`) será exibido no console do {{site.data.keyword.mobileanalytics_short}} como o nome do aplicativo. O nome do aplicativo é usado como um filtro para procurar logs do aplicativo no painel. Ao usar o mesmo nome de aplicativo entre as plataformas (por exemplo, Android e iOS), é possível ver todos os logs desse aplicativo com o mesmo nome, independentemente de qual plataforma os logs foram enviados.

5. Envie análise de uso registrada para o Mobile Analytics Service. Uma maneira simples de testar a análise é executar o código a seguir quando o aplicativo for iniciado:

	#### Android
	{: #android-send}

	Use o método `Analytics.send()` para enviar os dados de analítica para o servidor. É possível colocar o método
`Analytics.send()` em qualquer lugar no método `onCreate` da atividade principal em seu aplicativo Android ou em um local que
funcione melhor para o seu projeto. 
	
	É possível inserir `Analytics.send()` em qualquer lugar.

	```
	Analytics.send();
	```
	{: codeblock}

	#### iOS
	{: #ios-send}

	Use o método `Analytics.send` para enviar os dados de análise para o servidor. É possível colocar o método `Analytics.send`
em qualquer lugar no método `application(_:didFinishLaunchingWithOptions:)` de seu delegado de aplicativo ou em um local que funcione melhor para o
seu projeto. 

	```
	Analytics.send()
	```
	{: codeblock}
	
	#### Cordova
	{: #cordova-send}
	
	Use o método `BMSAnalytics.send` para
enviar dados de analítica para o servidor. Coloque o método
`BMSAnalytics.send` em um local que funcione
melhor para o seu projeto.
	
	```
	BMSAnalytics.send
	```
	{: codeblock}
	
	Leia o tópico
[Instrumentando
seu aplicativo](/docs/services/mobileanalytics/sdk.html) para aprender sobre recursos adicionais
do {{site.data.keyword.mobileanalytics_short}}, como
[criação de log](/docs/services/mobileanalytics/sdk.html#app-monitoring-logger),
[solicitações de rede](/docs/services/mobileanalytics/sdk.html#network-requests)
e [analítica de travamento](/docs/services/mobileanalytics/sdk.html#report-crash-analytics).
	
6. Compile e execute o aplicativo em seu emulador ou dispositivo.

7. Acesse o
{{site.data.keyword.mobileanalytics_short}} Console para ver
a analítica de uso de seu aplicativo. Também é
possível monitorar o seu aplicativo
<!--[creating custom charts](app-monitoring.html#custom-charts),-->[configurando
alertas](/docs/services/mobileanalytics/app-monitoring.html#alerts) e [monitorando travamentos do aplicativo](/docs/services/mobileanalytics/app-monitoring.html#monitor-app-crash).


# rellinks

## SDK
* [SDK Android ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics){: new_window}  
* [SDK iOS ](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics){: new_window}
* [SDK do
plug-in do Cordova Core](https://www.npmjs.com/package/bms-core){: new_window}

## Referência da API
{: #api}
* [API REST](https://mobile-analytics-dashboard.{DomainName}/analytics-service/){:new_window}
