---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-13"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Introdução ao {{site.data.keyword.mobileanalytics_short}}

{: #gettingstartedtemplate}

O {{site.data.keyword.mobileanalytics_full}} fornece aos desenvolvedores, administradores de TI e partes interessadas nos negócios insight sobre como seus apps móveis estão sendo executados e como estão sendo usados. O {{site.data.keyword.mobileanalytics_short}} permite que você:

* Monitore desempenho e uso de todos os seus aplicativos da sua área de trabalho ou tablet. 
* Identifique rapidamente tendências e anomalias, realize drill down para resolver os problemas e acione alertas quando Key Metrics atingir um limite crítico. 
{: shortdesc}

**Importante:** o {{site.data.keyword.mobileanalytics_short}} Console ainda não está pronto para o navegador do Internet Explorer, e alguma funcionalidade pode não funcionar corretamente. Para obter a melhor experiência, use o Firefox, o Chrome ou o Safari.

Para que o serviço do {{site.data.keyword.mobileanalytics_short}} esteja pronto para execução rapidamente, siga estas etapas:

1. Após você criar uma instância
<!--[create an instance](https://console.{DomainName}/docs/services/reqnsi.html#req_instance)-->do serviço
{{site.data.keyword.mobileanalytics_short}}, será possível acessar o Console do {{site.data.keyword.mobileanalytics_short}} clicando em seu
tile na seção **Serviços** do Painel do {{site.data.keyword.Bluemix}}.

 Para ajudá-lo a obter uma ideia imediata das visualizações e gráficos diversos e do valor que agregam, fornecemos uma opção **modo demo** no console do {{site.data.keyword.mobileanalytics_short}}, na qual as visualizações e os gráficos exibem *dados demo*. Os dados demo são o modo padrão do console quando ele é ativado inicialmente após o serviço ser instanciado. Quando você tiver seus próprios aplicativos e dados de analítica preenchidos no serviço, será possível alternar o modo demo para *desligado* a fim de visualizar os dados dos seus aplicativos em diferentes gráficos. O console do Mobile Analytics é somente leitura quando em modo demo, portanto, não será possível criar novas definições de alerta.

2. Instale os [SDKs do cliente](/docs/services/mobileanalytics/install-client-sdk.html) {{site.data.keyword.mobileanalytics_short}}. É
possível, opcionalmente, usar a {{site.data.keyword.mobileanalytics_short}} [API de REST![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/ "Ícone de link externo"){:new_window}.

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
    
 Configure o valor para `hasUserContext` como **true** ou **false**. Se false (valor padrão), cada dispositivo será contado como um usuário ativo.

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
 
 Configure o valor para `hasUserContext` como **true** ou **false**. Se false (valor padrão), cada dispositivo será contado como um usuário ativo.
	
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
	BMSAnalytics.send()
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
* [SDK do Android![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-android-analytics "Ícone de link externo"){: new_window}  
* [SDK do iOS![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-analytics "Ícone de link externo"){: new_window}
* [SDK principal do plug-in do Cordova![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://www.npmjs.com/package/bms-core "Ícone de link externo"){: new_window}

## Referência da API
{: #api}
* [API de REST![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/ "Ícone de link externo"){:new_window}
