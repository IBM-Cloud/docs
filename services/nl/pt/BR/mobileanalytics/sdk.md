---

copyright:
  years: 2015, 2016

---

# Instrumentando seu aplicativo para usar os SDKs do cliente do {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}
*Última atualização: 27 de abril de 2016*
{: .last-updated}

Os SDKs do {{site.data.keyword.mobileanalytics_full}} permitem instrumentar o aplicativo móvel.
{: shortdesc}

O {{site.data.keyword.mobileanalytics_short}} permite coletar três categorias de dados e cada uma requer um grau diferente de instrumentação:

1.  Dados predefinidos - esta categoria inclui informações sobre uso genérico e dispositivo que se aplicam a todos os aplicativos. Nessa categoria estão os metadados do dispositivo (sistema operacional e modelo de dispositivo) e dados de uso (usuários ativos e sessões de aplicativo) que indicam o volume, frequência ou duração de uso do aplicativo. Os dados predefinidos são coletados automaticamente após a inicialização do SDK do {{site.data.keyword.mobileanalytics_short}} em seu aplicativo.
2. Eventos customizados - esta categoria inclui dados que você mesmo define e que são específicos para seu aplicativo. Esses dados representam eventos que ocorrem no aplicativo, como visualizações da página, toques do botão ou compras do aplicativo. Além de inicializar o SDK do {{site.data.keyword.mobileanalytics_short}} no aplicativo, deve-se incluir uma linha de código para cada evento customizado que você desejar rastrear.
3. Mensagens de log do cliente - esta categoria permite que o desenvolvedor inclua linhas de código em todo o aplicativo que registram mensagens customizadas para ajudar no desenvolvimento e na depuração. O desenvolvedor designa um nível de severidade/detalhamento a cada mensagem de log e pode, subsequentemente, filtrar mensagens de filtro por nível designado ou preservar espaço de armazenamento configurando o aplicativo para ignorar mensagens que estão abaixo de um determinado nível de log. Para coletar dados do log do cliente, deve-se inicializar o SDK do {{site.data.keyword.mobileanalytics_short}} dentro do aplicativo, bem como incluir uma linha de código para cada mensagem de log.

Atualmente os SDKs estão disponíveis para Android, iOS e WatchOS.

## Identificando seu valor da Chave do cliente
{: #analytics-clientkey}

Identifique o valor da **Chave do cliente** antes de configurar o SDK do cliente. A Chave do cliente é necessária para inicializar o SDK do cliente.
1. Abra o painel de serviço do {{site.data.keyword.mobileanalytics_short}}.
2. Clique no ícone de chave inglesa para abrir a guia Chaves API.
3. Na guia Chaves API, anote o valor da Chave do cliente.


## Inicializando o aplicativo Android para coletar análise
{: #initalize-ma-sdk-android}

Inicialize seu aplicativo para permitir o envio de logs para o serviço {{site.data.keyword.mobileanalytics_short}}.

1. Importe o SDK do cliente incluindo a instrução `import` a seguir na parte superior do arquivo de projeto:

  ```
  import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  ```
  {: codeblock}

2. Inicialize o SDK do cliente do {{site.data.keyword.mobileanalytics_short}} em seu aplicativo Android incluindo o código de inicialização no método `onCreate` da atividade principal em seu aplicativo Android ou em um local que funcione melhor para seu projeto.

	```Java
	try {
            BMSClient.getInstance().initialize(this.getApplicationContext(), "", "", BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
        } catch (MalformedURLException e) {
            Log.e(your_app_name,"URL should not be malformed:  " + e.getLocalizedMessage());
        } 
  ```
  {: codeblock}

  Para usar o SDK do cliente do {{site.data.keyword.mobileanalytics_short}}, deve-se inicializar o `BMSClient` com o parâmetro **bluemixRegion**. No inicializador, o valor **bluemixRegion** especifica qual implementação do {{site.data.keyword.Bluemix_notm}} está sendo usada, por exemplo, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` ou `BMSClient.REGION_SYDNEY`.
  <!-- Set this value with a `BMSClient.REGION` static property. -->

  <!--You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Inicialize o Analytics usando seu objeto de aplicativo Android e fornecendo a ele o nome de seu aplicativo. Também é necessário o valor da [**Chave do cliente**](#analytics-clientkey).
	
	```Java 	Analytics.init(getApplication(), "my_app", apiKey, Analytics.DeviceEvent.LIFECYCLE); 	// In this code example, Analytics is configured to record lifecycle
events.
	```
  {: codeblock}

	**Dica:** o nome do aplicativo é usado como um filtro para procurar logs do cliente no painel. Ao usar o mesmo nome de aplicativo entre as plataformas (por exemplo, Android e iOS), é possível ver todos os logs desse aplicativo com o mesmo nome, independentemente de qual plataforma os logs foram enviados.

## Inicializando o aplicativo iOS para coletar análise
{: #init-ma-sdk-ios}

Inicialize seu aplicativo para permitir o envio de logs para o serviço {{site.data.keyword.mobileanalytics_short}}. O SDK do Swift está disponível para iOS e watchOS.

1. Importe as estruturas `BMSCore` e `BMSAnalytics` incluindo as instruções `import` na parte superior do arquivo de projeto `AppDelegate.swift`:

  ```Swift
  import BMSCore
  import BMSAnalytics
  ```
  {: screen}

2. Para usar o SDK do cliente do {{site.data.keyword.mobileanalytics_short}}, deve-se inicializar primeiro a classe `BMSClient` usando o código a seguir.

  Coloque o código de inicialização no método `application(_:didFinishLaunchingWithOptions:)` de seu delegado do aplicativo ou em um local que funcione melhor para o seu projeto.

    ```Swift
    BMSClient.sharedInstance.initializeWithBluemixAppRoute(nil, bluemixAppGUID: nil, bluemixRegion: BMSClient.REGION_US_SOUTH)`
    ```
    {: codeblock}

    Para usar o SDK do cliente do {{site.data.keyword.mobileanalytics_short}}, deve-se inicializar o `BMSClient` com o parâmetro **bluemixRegion**. No inicializador, o valor **bluemixRegion** especifica qual implementação do {{site.data.keyword.Bluemix_notm}} está sendo usada, por exemplo, `BMSClient.REGION_US_SOUTH`, `BMSClient.REGION_UK` ou `BMSClient.REGION_SYDNEY`.
   
   <!-- Set this value with a `BMSClient.REGION` static property. -->

   <!-- You can optionally pass the **applicationGUID** and **applicationRoute** values if you are using another {{site.data.keyword.Bluemix_notm}} service that requires these values, otherwise you can pass empty strings.-->

3. Inicialize o Analytics fornecendo a ele o nome de aplicativo móvel. Também é necessário o valor da [**Chave do cliente**](#analytics-clientkey).

  O nome do aplicativo é usado como um filtro para procurar logs do cliente em seu Painel do {{site.data.keyword.mobileanalytics_short}}. Usando o mesmo nome de aplicativo entre as plataformas (por exemplo, Android e iOS), é possível ver todos os logs desse aplicativo com o mesmo nome, independentemente de qual plataforma os logs foram enviados.

  Um parâmetro `deviceEvents` opcional reúne automaticamente a análise para eventos de nível do dispositivo.

  ### iOS
    {: #ios-initialize-analytics}

      ```
      Analytics.initializeWithAppName("AppName", apiKey: your_client_key,
      deviceEvents: DeviceEvent.LIFECYCLE)
      ```

  ### watchOS
  {: #watchos-initialize-analytics}

	```
	  Analytics.initializeWithAppName("AppName", apiKey: your_api_key)
	```

  É possível registrar eventos do dispositivo no WatchOS usando os métodos `Analytics.recordApplicationDidBecomeActive()` e `Analytics.recordApplicationWillResignActive()`.
  
  Inclua a linha a seguir no método `applicationDidBecomeActive()` da classe ExtensionDelegate.

	```
	Analytics.recordApplicationDidBecomeActive()
	```
  {: codeblock}

  Inclua a linha a seguir no método applicationWillResignActive() da classe ExtensionDelegate:
	```
	Analytics.recordApplicationWillResignActive()
	```
  {: codeblock}

## Reunindo análise de uso
{: #app-monitoring-gathering-analytics}

  É possível configurar o {{site.data.keyword.mobileanalytics_short}} Client SDK para registrar a análise de uso e enviar os dados registrados ao
serviço {{site.data.keyword.mobileanalytics_short}}.

  Use as APIs a seguir para iniciar a gravação e o envio da análise de uso:

#### Android
{: #android-usage-api}
	
```
// Disable recording of usage analytics (for example, to save disk space) // Recording is enabled by default Analytics.disable();
	
// Enable recording of usage analytics Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// Send recorded usage analytics to the Mobile Analytics Service Analytics.send();
```
	
Amostra de análise de uso para registrar um evento:
	
```
// Log a custom analytics event for custom charts, which is represented by a JSON object: JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");
```

#### iOS - Swift
{: #ios-usage-api}

```
// Disable recording of usage analytics (for example, to save disk space) // Recording is enabled by default Analytics.enabled = false

// Enable recording of usage analytics Analytics.enabled = true

// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service Analytics.send()
```

Amostra de análise de uso para registrar um evento:

```
// Log a custom analytics event for custom charts let eventObject = ["customProperty": "propertyValue"] Analytics.log(eventObject)
```

  <!--Removing Cordova for experimental-->
  <!--### Cordova-->
  <!--{: #usage-analytics-cordova}-->

  <!--```JavaScript-->
  <!--// Enable usage analytics recording-->
  <!--Analytics.enable();-->

  <!--// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--Analytics.send();-->
  <!--```-->
  <!--**Note:** When you are developing Cordova applications, use the native API to enable application lifecycle event recording.-->

## Ativando, configurando e usando o Criador de logs
{: #app-monitoring-logger}

  O {{site.data.keyword.mobileanalytics_full}} Client SDK fornece uma estrutura de criação de log que é semelhante a outras estruturas de log com as quais você pode estar familiarizado, tais como, `java.util.logging` ou `log4j`. A estrutura de criação de log suporta múltiplas instâncias do criador de logs por pacote, níveis diferentes de log, captura de rastreios de pilha para um travamento do aplicativo e muito mais.

  Também é possível configurar os dados registrados a serem armazenados no dispositivo no qual o aplicativo está em execução e enviar esses logs do dispositivo para o {{site.data.keyword.mobileanalytics_short}} Service em um momento posterior.

  <!-- Initialization has to happen first to be able to collect logs and send them to the {{site.data.keyword.mobileanalytics_short}} service. -->

  A estrutura de criação de log do SDK do cliente do {{site.data.keyword.mobileanalytics_short}} suporta os níveis de log a seguir, que são listados do menos ao mais detalhado, com as diretrizes de uso recomendadas:

  * `FATAL` - Usar para travamentos ou interrupções irrecuperáveis. O nível `FATAL` é reservado para registrar erros irrecuperáveis, que aparecem para os usuários como um travamento do aplicativo
  * `ERROR` - Usar para exceções inesperadas ou erros de protocolo de rede inesperados
  * `WARN` - Usar para registrar avisos de uso que não são considerados erros críticos, como uso de APIs descontinuadas ou resposta de rede lenta
  * `INFO` - Usar para relatar eventos de inicialização e outros dados que podem ser importantes, mas não urgentes
  * `DEBUG` - Usar para relatar instruções de depuração para ajudar os desenvolvedores a resolver defeitos do aplicativo

    #### Cenário de nível de log
    {: #log-level-scenario}

    Quando o nível do criador de logs estiver configurado como `FATAL`, o criador de logs capturará exceções de não captura, mas não capturará logs que levam ao evento de travamento. É possível configurar um nível do criador de logs mais detalhado para assegurar que os logs que podem levar a uma entrada do criador de logs `FATAL`, como `WARN` e `ERROR`, também sejam capturados.

  <!--**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core.-->

  <!--### Cordova-->


  <!--```JavaScript-->

  <!--var logger = MFPLogger.getInstance("myLogger");-->

  <!--logger.debug("debug info");-->
  <!--logger.info("info message");-->
  <!--logger.warn("warning message");-->
  <!--logger.fatal("fatal message");-->

  <!--```-->


### Amostra de uso do criador de logs
{: #sample-logger-usage}

**Nota:** certifique-se de que você tenha instrumentado seu aplicativo para usar o [{{site.data.keyword.mobileanalytics_short}} Client SDK](sdk.html) antes de usar a estrutura de criação de log.
 
  Os fragmentos de código a seguir mostram o uso do criador de logs de amostra:

#### Android
{: #android-logger-sample}

```
// Configure Logger to save logs to the device so that they // can later be sent to the {{site.data.keyword.mobileanalytics_short}} service // Disabled by default;
set to true to enable Logger.storeLogs(true);

// Change the minimum log level (optional) // The default setting is Logger.LEVEL.DEBUG Logger.setLogLevel(Logger.LEVEL.INFO);

// Send logs to the {{site.data.keyword.mobileanalytics_short}} Service Logger.send();
```

Cenários de criador de logs:

```
// Create two logger instances // You can create multiple log instances to organize your logs Logger logger1 = Logger.getLogger("logger1"); Logger logger2 =
Logger.getLogger("logger2");

// Log messages with different levels // Debug message for feature 1 // Info message for feature 2 logger1.debug("debug message"); //the logger1.debug message is not
logged because the logLevelFilter is set to Info logger2.info("info message");
```

#### iOS - Swift
{: ios-logger-sample}

```
// Configure Logger to save logs to the device so that they can later be sent to the {{site.data.keyword.mobileanalytics_short}} service // Disabled by default; set
to true to enable Logger.logStoreEnabled = true

// Change the minimum log level (optional) // The default setting is LogLevel.Debug Logger.logLevelFilter = LogLevel.Info

// Send logs to the {{site.data.keyword.mobileanalytics_short}} Service Logger.send()
```

Cenários de criador de logs:
    
```
// Create two logger instances // You can create multiple log instances to organize your logs let logger1 = Logger.logger(forName: "feature1Logger") let logger2 =
Logger.logger(forName: "feature2Logger")
	
// Log messages with different levels logger1.debug("debug message for feature 1") 
//the logger1.debug message is not logged because the logLevelFilter is set to Info logger2.info("info message for feature 2")
```

**Dica**: por questões de privacidade, é possível desativar a saída do Criador de logs para aplicativos que são construídos no modo de liberação. Por padrão, a classe de Criador de logs imprime logs no console Xcode. Nas configurações de construção para seu destino, inclua uma sinalização `-D RELEASE_BUILD` na seção **Outra sinalizações do Swift** da configuração de construção da liberação.
    

  <!-- ### Cordova-->
  <!--{: #enable-logger-sample-cordova}-->

  <!--// Enable persisting logs-->
  <!--MFPLogger.setCapture(true);-->

  <!--// Set the minimum log level to be printed and persisted-->
  <!--MFPLogger.setLevel(MFPLogger.INFO);-->

  <!--var logger1 = MFPLogger.getInstance("logger1");-->
  <!--var logger2 = MFPLogger.getInstance("logger2");   -->

  <!--// Log messages with different levels-->
  <!--logger1.debug ("debug message");-->
  <!--logger2.info ("info message");-->

  <!--// Send persisted logs to the {{site.data.keyword.mobileanalytics_short}} Service-->
  <!--```-->

<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs}

  The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android}

```
Logger.setSDKDebugLoggingEnabled(true);
```

#### iOS - Swift
{: #enable-logger-print-swift}

```
Logger.sdkDebugLoggingEnabled = true
```
-->

## Rastreando usuários ativos
{: #trackingusers}
É possível rastrear, opcionalmente, quantos usuários estão usando ativamente seu aplicativo, passando o nome do usuário ativo para o {{site.data.keyword.mobileanalytics_short}}.

#### Android
{: #android-tracking-users}

Inclua o código a seguir para quando o usuário efetuar login:

```
Analytics.setUserIdentity("username");
```

Inclua o código a seguir para quando o usuário efetuar logout:

```
Analytics.clearUserIdentity();
```

#### iOS - Swift
{: #ios-tracking-users}

Inclua o código a seguir para quando o usuário efetuar login:

```
Analytics.userIdentity = "username"
```

Inclua o código a seguir para quando o usuário efetuar logout:

```
Analytics.userIdentity = nil
```

<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before `/analytics/console/dashboard`.  

  		For example, if the dashboard URL is: `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde`
      {: screen}

  		then the Analytics Service Route is
      `http://mobile-analytics-dashboard.ng.bluemix.net`
      {: screen}

  	2. Get the [Client API Key](#analytics-clientkey) value from the Analytics dashboard.

  	You will use the {{site.data.keyword.mobileanalytics_short}} service route and API Key to construct a URL to report analytics data, depending on the version of your MobileFirst Platform server. -->

<!--  3. Copy the URL for your {{site.data.keyword.mobileanalytics_short}} service dashboard. Include the `instanceId` query parameter, for example:
      `http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=1212345abcde`
      {: screen}

  4. Configure the values for the MobileFirst Platform server JNDI properties, as follows:-->

<!--    ### MobileFirst Platform V7.0
    {: #mfp70}

        The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/data?tenant=<Client API Key>`
        {: screen}

        The `wl.analytics.console.url` JNDI property is the Analytics service dashboard URL.

        #### Example of MobileFirst Platform V7.0 JNDI property values
        {: #example-mfp70-jndi-values}

        For a MobileFirst Platform project named `Myproj7000`, based on the examples in steps 2 and 3, replace the current JNDI property values in the `server.xml` file with:
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
        ```
        {: screen}
        ```
        <jndiEntry jndiName="MyProj7000/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
        ```
        {: screen}

    ### MobileFirst Platform V7.1
    {: #mfp71}

      The format of the `wl.analytics.url` JNDI property is: `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`
      {: screen}

      #### Example of MobileFirst Platform JNDI V7.1 property values
      {: #example-mfp71-jndi-values}

      For a MobileFirst Platform project named `MyProj7101`, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/v2/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="MyProj7101/wl.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}

      ### MobileFirst Platform V8.0
      {: #mfp80}

      The format of the `mfp.analytics.url` JNDI property is:
      `<Analytics Service Route>/analytics-service/rest/v2/<Client API Key>`  

    #### Example MobileFirst Platform V8.0 Beta JNDI property values
      {: example-mfp80b-jndi-values}

      For a MobileFirst Platform project named `mfp`, which is the default, replace the current JNDI property values in the `server.xml` file with:
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data?tenant=12345abcde"'/>
      ```
      {: screen}
      ```
      <jndiEntry jndiName="mfp/mfp.analytics.console.url" value='"http://mobile-analytics-dashboard.ng.bluemix.net/analytics/console/dashboard?instanceId=12345abcde"'/>
      ```
      {: screen}
-->
<!-- #### Ignored events and event retention
{: #ignored-events}
The {{site.data.keyword.mobileanalytics_short}} service saves the following data for ignored events and event retention:
  
<dl>	
<dt>Ignored events</dt>
	<dd>`ANALYTICS_SDK_CFG_IGNORE_AppPushAction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_ServerLog: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransaction: true`
		  `ANALYTICS_SDK_CFG_IGNORE_NetworkTransactionSummarizedHourly: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushNotification: true`
		  `ANALYTICS_SDK_CFG_IGNORE_PushSubscription: true`</dd>
</dt>
<dt>Event retention</dd>
<dd>
`ANALYTICS_TTL_AlertNotification: 14d`<br>
`ANALYTICS_TTL_CustomData: 7d`<br>
`ANALYTICS_TTL_Device: 90d`<br>
`ANALYTICS_TTL_AppLog: 3d`<br>
`ANALYTICS_TTL_AppSession: 7d`
</dd>
</dt>
</dl>
  
-->

# rellinks

## Referência da API
{: #api}
* [API REST](https://mobile-analytics-dashboard.eu-gb.bluemix.net/analytics-service/){:new_window}
