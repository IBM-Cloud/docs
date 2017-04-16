---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Instrumentando seu aplicativo para usar os SDKs do cliente do {{site.data.keyword.mobileanalytics_short}}
{: #mobileanalytics_sdk}

Os SDKs do {{site.data.keyword.mobileanalytics_full}} permitem instrumentar o aplicativo móvel.
{: shortdesc}

O {{site.data.keyword.mobileanalytics_short}} permite que você colete duas <!--three--> categorias de dados e cada uma requer um grau
diferente de instrumentação:

1. Dados predefinidos - esta categoria inclui informações sobre uso genérico e sobre o
dispositivo que se aplicam a todos os aplicativos. Dentro desta categoria estão
os metadados de dispositivo (sistema operacional e modelo de dispositivo) e dados de uso (usuários ativos e sessões de aplicativo) que indicam o volume, a frequência
ou a duração de uso do aplicativo. Os dados predefinidos são coletados automaticamente após você inicializar o SDK do
{{site.data.keyword.mobileanalytics_short}} em seu aplicativo.

2. Mensagens de log do aplicativo - esta categoria permite que o desenvolvedor inclua, em todo o aplicativo, linhas de código que registram mensagens customizadas para ajudar no desenvolvimento e na
depuração. O desenvolvedor designa um nível de severidade/detalhamento para cada mensagem de log e pode, subsequentemente, filtrar mensagens por nível designado ou preservar espaço de armazenamento
configurando o aplicativo para ignorar mensagens que estiverem em um nível inferior a um
determinado nível de log. Para coletar dados do log do aplicativo, deve-se inicializar o SDK
do {{site.data.keyword.mobileanalytics_short}} dentro do seu aplicativo, bem como incluir
uma linha de código para cada mensagem de log.

3. Eventos customizados - essa categoria inclui dados que você mesmo define e que são
específicos do seu app. Esses dados representam eventos que ocorrem em seu app, tais como
visualizações de página, toques do botão ou compras no aplicativo. Além de inicializar o SDK do {{site.data.keyword.mobileanalytics_short}} no aplicativo, deve-se incluir uma linha de código para cada evento customizado que você desejar rastrear. 

Atualmente, os SDKs estão disponíveis para Android, iOS,
WatchOS e Cordova.

## Identificando o valor da chave API de suas credencias de serviço
{: #analytics-clientkey}

Identifique o valor da **Chave API** antes de configurar o Client SDK. A chave API é necessária para inicializar o Client SDK.

1. Abra o painel de serviço do {{site.data.keyword.mobileanalytics_short}}.
2. Expanda **Visualizar credenciais** para revelar o valor de sua chave API. Você precisará do valor da Chave API ao inicializar o SDK
do cliente {{site.data.keyword.mobileanalytics_short}}.


## Inicializando o seu aplicativo para coletar análise
{: #initalize-ma-sdk}

Inicialize seu aplicativo para permitir o envio de logs para o serviço {{site.data.keyword.mobileanalytics_short}}.

1. Importe o SDK do Cliente.

	### Android
	{: #android-import}

	Inclua as seguintes instruções `importar`
no início do seu arquivo de projeto:
	
  	```
  	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.analytics.api.*;
import com.ibm.mobilefirstplatform.clientsdk.android.logger.api.*;
  	```
  	{: codeblock}
  
	### iOS
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
   
   ### Cordova
	{: #cordova-import}
		
	Inclua o plug-in Cordova executando o comando a seguir por meio do diretório-raiz do
seu aplicativo Cordova:

   ```Javascript
   cordova plugin add bms-core
   ```
   {: codeblock}  

2. Inicialize o SDK do cliente
{{site.data.keyword.mobileanalytics_short}} em seu
aplicativo.

	### Android
	{: #android-init}
	
	Inicialize o SDK do cliente do {{site.data.keyword.mobileanalytics_short}} em seu aplicativo Android incluindo o código de inicialização no método `onCreate` da atividade principal em seu aplicativo Android ou em um local que funcione melhor para seu projeto.

	```Java
	BMSClient.getInstance().initialize(getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
	```
	{: codeblock}

  Deve-se inicializar o `BMSClient` com
o parâmetro **bluemixRegion**. No inicializador, o
valor **bluemixRegion** especifica qual
implementação do
{{site.data.keyword.Bluemix_notm}} você
está usando, por exemplo,
`BMSClient.REGION_US_SOUTH` e
`BMSClient.REGION_UK`. 
    <!-- , or `BMSClient.REGION_SYDNEY`.--> 
    
 ### iOS
 {: #ios-init}
    
 Primeiro inicialize a classe
`BMSClient`, usando o código a seguir. Coloque o código de inicialização no método `application(_:didFinishLaunchingWithOptions:)` de seu delegado do aplicativo ou em um local que funcione melhor para o seu projeto.
	
    ```Swift 
    BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.Region.usSouth) // Make sure that you point to your region
    ```
   {: codeblock}

   Deve-se inicializar o `BMSClient` com
o parâmetro **bluemixRegion**. No inicializador, o
valor **bluemixRegion** especifica qual
implementação do
{{site.data.keyword.Bluemix_notm}} você
está usando, por exemplo,
`BMSClient.Region.usSouth` ou
`BMSClient.Region.unitedKingdom`.
    <!-- , or `BMSClient.Region.Sydney`. -->
    
 ### Cordova
 {: #cordova-init}
    
 Inicialize o **BMSClient** e o
**BMSAnalytics**. Você precisará do valor da
[**Chave
API](#analytics-clientkey).

  ```Javascript
  var applicationName = "HelloWorld";
  var apiKey =  "your_api_key_here";
  var hasUserContext = true;
  var deviceEvents = [BMSAnalytics.ALL];

  BMSClient.initialize(BMSClient.REGION_US_SOUTH); //Make sure you point to your region	
  BMSAnalytics.initialize(applicationName, apiKey, hasUserContext, deviceEvents)
  ```
  {:codeblock}

 Para usar o SDK do cliente do {{site.data.keyword.mobileanalytics_short}}, deve-se inicializar o `BMSClient` com o parâmetro **bluemixRegion**. No inicializador, o valor **bluemixRegion** especifica qual implementação do {{site.data.keyword.Bluemix_notm}} está sendo usada, por exemplo, `BMSClient.REGION_US_SOUTH` ou `BMSClient.REGION_UK`.
    <!-- , or `BMSClient.REGION_SYDNEY`. -->
    
3. Inicialize o Analytics usando seu objeto de aplicativo e
dando a ele seu nome do seu aplicativo. 

	O nome que você seleciona para o seu aplicativo (`your_app_name_here`) é exibido no console do
{{site.data.keyword.mobileanalytics_short}} como o nome do aplicativo. O nome do aplicativo é usado como um filtro para procurar logs do aplicativo no painel. Ao usar o mesmo nome de aplicativo entre as plataformas (por exemplo, Android e iOS), é possível ver todos os logs desse aplicativo com o mesmo nome, independentemente de qual plataforma os logs foram enviados.

	Também será necessário o valor da [**Chave API**](#analytics-clientkey).

	### Android
	{: #android-init-analytics}
	
	```Java
	// In this code example, Analytics is configured to record lifecycle events.
	Analytics.init(getApplication(), "your_app_name_here", apiKey, hasUserContext, Analytics.DeviceEvent.ALL);
	```
	{: codeblock}
	
	**Nota:** configure o valor de `hasUserContext` como **true** ou **false**. Se false (valor padrão), cada dispositivo será contado como um usuário ativo. O
método [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users), que permite a você controlar o número de usuários
por dispositivo que estão ativamente usando o seu aplicativo, não funcionará quando `hasUserContext` for false. Se true, cada uso de [`Analytics.setUserIdentity("username")`](sdk.html#android-tracking-users) será contado como um usuário ativo. Não há nenhuma identidade de usuário padrão quando `hasUserContext` é true e, portanto, deve ser configurado para preencher os gráficos de usuário ativo.
	
	### iOS
	{: #ios-initialize-analytics}
	
 	```Swift 
	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", hasUserContext: false, deviceEvents: .lifecycle, .network)
 	```
 	{: codeblock}
 	
   ### watchOS
   {: #watchos-initialize-analytics}
	 	
 	```Swift
 	Analytics.initialize(appName: "your_app_name_here", apiKey: "your_api_key_here", deviceEvents: .network)
 	```
 	{: codeblock}
 	
 	Um parâmetro `deviceEvents` opcional reúne automaticamente a análise para eventos de nível do dispositivo.
	
 **Nota:** configure o valor de `hasUserContext` como **true** ou **false**. Se false (valor padrão), cada dispositivo será contado como um usuário ativo. O
método [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users), que permite a você controlar o número de usuários por
dispositivo que estão ativamente usando o seu aplicativo, não funcionará quando `hasUserContext` for false. Se `hasUserContext` for true, cada uso de [`Analytics.userIdentity = "username"`](sdk.html#ios-tracking-users) será contado como um usuário ativo. Não há nenhuma identidade de usuário padrão quando `hasUserContext` é true e, portanto, deve ser configurado para preencher os gráficos de usuário ativo.

 #### watchOS
 {: #watchos-record-device}

 É possível registrar eventos do dispositivo no WatchOS usando os métodos `Analytics.recordApplicationDidBecomeActive()` e `Analytics.recordApplicationWillResignActive()`.
  
 Inclua a linha a seguir no método `applicationDidBecomeActive()` da
classe ExtensionDelegate:
 
	```
	Analytics.recordApplicationDidBecomeActive()
	```
   {: codeblock}

 Inclua a linha a seguir no método `applicationWillResignActive()` da
classe ExtensionDelegate:
 
	```
	Analytics.recordApplicationWillResignActive()
	```
	{: codeblock}	
		
4. Você já inicializou seu aplicativo para coletar análise. Em
seguida, será possível [enviar
dados de analítica](sdk.html#app-monitoring-gathering-analytics) para o serviço do {{site.data.keyword.mobileanalytics_short}}.


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
		
// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send(new ResponseListener() {
            @Override
	    public void onSuccess(Response response) {
                // Handle Analytics send success here.
            }

            @Override
            public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
                // Handle Analytics send failure here.
            }
        });
```
{: codeblock}
	
Amostra de análise de uso para registrar um evento:
	
```
// Log a custom analytics event
JSONObject eventJSONObject = new JSONObject();
	
eventJSONObject.put("customProperty" , "propertyValue");

Analytics.log(eventJSONObject);
```
{: codeblock}


#### iOS - Swift
{: #ios-usage-api}

```
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.isEnabled = false

// Enable recording of usage analytics
Analytics.isEnabled = true

// Send recorded usage analytics to the Mobile Analytics Service
Analytics.send(completionHandler: { (response: Response?, error: Error?) Em

    if let response = response {
        // Handle Analytics send success here.
    }
    if let error = error {
        // Handle Analytics send failure here.
    }
})
```
{: codeblock}

Amostra de análise de uso para registrar um evento:

```Swift
// Log a custom analytics event
let eventObject = ["customProperty": "propertyValue"]
Analytics.log(metadata: eventObject)
```
{: codeblock}

#### Cordova
{: #usage-analytics-cordova}

  ```JavaScript
  // Enable usage analytics recording
  BMSAnalytics.enable();
  
  // Disable usage analytics recording
  BMSAnalytics.disable();

  // Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
  BMSAnalytics.send(
	function(response) {
		console.log('success: ' + response);
		},
	function (err) {
		console.log('fail: ' + err);
		});
  ```
  {: codeblock}

Amostra de análise de uso para registrar um evento:

```JavaScript
// Log a custom analytics event
var eventObject = {"customProperty": "propertyValue"}
BMSAnalytics.log(eventObject)
```
{: codeblock}

  
  **Nota:** Quando estiver desenvolvendo aplicativos Cordova, use a API nativa para ativar a gravação do evento de ciclo de vida do aplicativo.
  
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

    Quando o nível do criador de logs estiver configurado
como `DEBUG`, você também obterá os logs do SDK
do cliente Mobile Analytics, que serão incluídos ao enviar logs.

  <!--**Note:** Find full Logger API references for each platform at [SDKs, samples, API reference](sdks-samples-apis.html). The Logger API is part of the--> <!--{{site.data.keyword.mobileanalytics_short}} Client SDK Core.-->

### Amostra de uso do criador de logs
{: #sample-logger-usage}

**Nota:** certifique-se de ter instrumentado
o seu aplicativo para usar o SDK do cliente
{{site.data.keyword.mobileanalytics_short}} antes de usar a estrutura de criação de log.
 
  Os fragmentos de código a seguir mostram o uso do criador de logs de amostra:
#### Android
{: #android-logger-sample}

```
// Configure Logger to save logs to the device so that they 
// can later be sent to the Mobile Analytics service
// Disabled by default; set to true to enable
Logger.storeLogs(true);

// Change the minimum log level (optional) // The default setting is Logger.LEVEL.DEBUG Logger.setLogLevel(Logger.LEVEL.INFO);

// Create two logger instances // You can create multiple log instances to organize your logs Logger logger1 = Logger.getLogger("logger1"); Logger logger2 =
Logger.getLogger("logger2");

// Log messages with different levels // Debug message for feature 1 // Info message for feature 2 logger1.debug("debug message"); //the logger1.debug message is not
logged because the logLevelFilter is set to Info logger2.info("info message");

// Send logs to the Mobile Analytics Service
        Logger.send(new ResponseListener() {
                    @Override
	    public void onSuccess(Response response) {
                        // Handle Logger send success here.
                    }

                    @Override
                    public void onFailure(Response response, Throwable throwable, JSONObject jsonObject) {
                        // Handle Logger send failure here.
                    }
                });        
```
{: codeblock}

#### iOS - Swift
{: #ios-logger-sample-swift2}

```
// Configure Logger to save logs to the device so that they 
// can later be sent to the Mobile Analytics service
// Disabled by default; set to true to enable
Logger.isLogStorageEnabled = true

// Change the minimum log level (optional)
// The default setting is LogLevel.debug
Logger.logLevelFilter = LogLevel.info

// Create two logger instances
// You can create multiple log instances to organize your logs
let logger1 = Logger.logger(name: "feature1Logger")
let logger2 = Logger.logger(name: "feature2Logger")

// Log messages with different levels
logger1.debug(message: "debug message for feature 1") 
// The logger1.debug message is not logged because the 
// logLevelFilter is set to info
logger2.info(message: "info message for feature 2")

// Send logs to the Mobile Analytics Service
Logger.send(completionHandler: { (response: Response?, error: Error?) Em
    
    if let response = response {
        logger.debug(message: "Status code: \(response.statusCode)")
        logger.debug(message: "Response: \(response.responseText)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
})
```
{: codeblock}

**Dica**: por questões de privacidade, é possível desativar a saída do Criador de logs de aplicativos construídos no modo de liberação. Por padrão, a classe de Criador de logs imprime logs no console Xcode. Nas configurações de construção para seu destino, inclua uma sinalização `-D RELEASE_BUILD` na seção **Outra sinalizações do Swift** da configuração de construção da liberação.
    

#### Cordova
{: #enable-logger-sample-cordova}

  ```
  // Enable persisting logs
  BMSLogger.storeLogs(true);

  // Set the minimum log level to be printed and persisted
  BMSLogger.setLogLevel(BMSLogger.INFO);

  var logger1 = BMSLogger.getLogger("logger1");
  var logger2 = BMSLogger.getLogger("logger2");   

  // Log messages with different levels
  logger1.debug ("debug message");
  logger2.info ("info message");

  // Send persisted logs to the {{site.data.keyword.mobileanalytics_short}} Service
  BMSLogger.send();
  BMSAnalytics.send();
  ```
  {: codeblock}


<!--## Enabling the {{site.data.keyword.mobileanalytics_short}} Client SDK internal logs
{: #enable-logger-sdklogs}

  The {{site.data.keyword.mobileanalytics_short}} Client SDK provides a better development experience by not unnecessarily increasing the console output with its internal debug messages. Therefore, by default, internal log messages that are produced by the {{site.data.keyword.mobileanalytics_short}} SDK with the DEBUG level are not printed. You can enable printing of all internal log messages of the {{site.data.keyword.mobileanalytics_short}} Client SDK with the following API:

#### Android
{: #enable-logger-print-android}

```
{: codeblock}
Logger.setSDKDebugLoggingEnabled(true);
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-print-swift}

```
Logger.sdkDebugLoggingEnabled = true
```
{: codeblock}
-->

## Fazendo uma solicitação de rede
{: #network-requests}

É possível configurar o SDK do cliente do {{site.data.keyword.mobileanalytics_short}} para [fazer uma solicitação de rede](/docs/mobile/sdk_network_request.html). Certifique-se
de já ter inicializado `BMSClient` e `BMSAnalytics`, além de ter
importado os SDKs do cliente.

<!--
#### Android
{: #android-network-requests}

**Note:** This code snippet assumes that you have [imported the Client SDKs](#android-import).

```
public void makeGetCall(){
    Thread thread = new Thread(new Runnable() {
        @Override
        public void run() {
            try  {
                Request request = new Request("http://httpbin.org/get", "GET");
                    request.send(null, null);
            } catch (Exception e) {
                // Handle failure here.
            }
        }
    });
    thread.start();
}
```
{: codeblock}

-->

<!-- 
#### Swift 3.0
{: #ios-network-requests}

 ```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: Error?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
 
 -->

<!-- Commenting out bmsurlsession
```
// Make a network request
let urlSession = BMSURLSession(configuration: .default, delegate: nil, delegateQueue: nil)
var request = URLRequest(url: URL(string: "http://httpbin.org/get")!)
request.httpMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTask(with: request) { (data: Data?, response: URLResponse?, error: Error?) in
    if let httpResponse = response as? HTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = String(data: data!, encoding: .utf8) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->

<!--
#### Swift 2.2
{: ios-swift22-network-requests}

```Swift
 	// Make a network request
	let customResourceURL = "<your resource URL>"
	let request = Request(url: customResourceURL, method: HttpMethod.GET)

	let callBack:BMSCompletionHandler = {(response: Response?, error: NSError?) in
   	if error == nil {
       	    print ("response:\(response?.responseText), no error")
    	  } else {
       	    print ("error: \(error)")
    	}
	}
	request.send(completionHandler: callBack)
 ```
 {: codeblock}
-->
<!--
```
// Make a network request
let urlSession = BMSURLSession(configuration: .defaultSessionConfiguration(), delegate: nil, delegateQueue: nil)
let request = NSMutableURLRequest(URL: NSURL(string: "http://httpbin.org/get")!)
request.HTTPMethod = "GET"
request.allHTTPHeaderFields = ["foo":"bar"]

urlSession.dataTaskWithRequest(request) { (data: NSData?, response: NSURLResponse?, error: NSError?) in
    if let httpResponse = response as? NSHTTPURLResponse {
        logger.info(message: "Status code: \(httpResponse.statusCode)")
    }
    if data != nil, let responseString = NSString(data: data!, encoding: NSUTF8StringEncoding) {
        logger.info(message: "Response data: \(responseString)")
    }
    if let error = error {
        logger.error(message: "Error: \(error)")
    }
}.resume()
```
{: codeblock}
-->
<!--
#### Cordova
{: #cordova-network-requests}

```
var success = function(data){
     console.log("success", data);
 }
 var failure = function(error)
     {console.log("failure", error);
 }
 var request = new BMSRequest("<your application route>", BMSRequest.GET);
 request.send(success, failure);
```
{: codeblock}

-->

## Relatório analítico de travamento
{: #report-crash-analytics}

É possível ver [dados de travamento de aplicativo](app-monitoring.html#monitor-app-crash) enviando informações de analítica e de log para
{{site.data.keyword.mobileanalytics_short}}.

O método `Analytics.send()` preenche as tabelas **Visão geral de travamento** e **Travamentos**
na página **Travamentos**. Os gráficos nesta seção são ativados usando a inicialização e enviando o processo para analítica; nenhuma configuração
especial é necessária.

O método `Logger.send()` preenche as tabelas **Resumo de travamento** e **Detalhes de travamento**
na página **Resolução de problemas**. Deve-se ativar o seu aplicativo para armazenar e enviar logs para preencher os gráficos nesta seção,
incluindo uma instrução adicional em seu código do aplicativo:

#### Android
{: #android-crash-statement}

* `Logger.storeLogs(true);`
<!-- * `Logger.setLogLevel(Logger.LEVEL.FATAL); // or greater` -->

Veja [uso do criador de logs de amostra](sdk.html#android-logger-sample).

#### iOS
{: #ios-crash-statement}

* `Logger.isLogStorageEnabled = true`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

Veja [uso do criador de logs de amostra](sdk.html##ios-logger-sample-swift2).

#### Cordova
{: #cordova-crash-statement}

* `BMSLogger.storeLogs(true);`
<!-- * `Logger.logLevelFilter = LogLevel.Fatal // or greater` -->

Veja [uso do criador de logs de amostra](sdk.html##ios-logger-sample-swift2).


## Rastreando usuários ativos
{: #trackingusers}

Se o seu aplicativo puder reconhecer usuários exclusivos em um dispositivo, será possível rastrear, opcionalmente, quantos usuários estão usando ativamente o
seu aplicativo, passando o nome do usuário ativo para {{site.data.keyword.mobileanalytics_short}}. 

Ative o rastreamento de usuário inicializando {{site.data.keyword.mobileanalytics_short}} com
`hasUserContext=true`. Caso contrário, o {{site.data.keyword.mobileanalytics_short}} irá capturar apenas um usuário por dispositivo. 
#### Android
{: #android-tracking-users}

Inclua o código a seguir para controlar quando o usuário efetua login:

```
Analytics.setUserIdentity("username");
```
{: codeblock}

<!--Add the following code for when the user logs out:

```
Analytics.clearUserIdentity();
```
{: codeblock}
-->

#### iOS - Swift
{: #ios-tracking-users}

Inclua o código a seguir para controlar quando o usuário efetua login:

```
Analytics.userIdentity = "username"
```
{: codeblock}

<!--
Add the following code for when the user logs out:

```
Analytics.userIdentity = nil
```
{: codeblock}
-->

#### Cordova
{: #cordova-tracking-users}

Inclua o código a seguir para controlar quando o usuário efetua login:

```
BMSAnalytics.setUserIdentity("username");
```
{: codeblock}


<!--## Configuring MobileFirst Platform Foundation servers to use the {{site.data.keyword.mobileanalytics_short}} service (optional)
{: #configmfp}
  If you are using MobileFirst Platform Foundation Server V7 and higher, you can configure it to use the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobileanalytics_short}} service to store analytics and logged data. 
  
  Configure MobileFirst Platform V7.0, V7.1, and V8.0 Beta servers to send analytics data to the {{site.data.keyword.mobileanalytics_short}} service on {{site.data.keyword.Bluemix_notm}}.

  1. Visit the dashboard for the {{site.data.keyword.mobileanalytics_short}} service where you want to send analytics data and note the browser URL for the dashboard.
  2. Determine the value for reporting analytics, as follows:
  	1. Get the {{site.data.keyword.mobileanalytics_short}} service route from the dashboard URL. The {{site.data.keyword.mobileanalytics_short}} service route is the part of the URL before ``/analytics/console/dashboard``.  

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

## O Que Fazer A Seguir
{: #what-to-do-next}

Agora é possível acessar o
{{site.data.keyword.mobileanalytics_short}}
Console para ver a analítica de uso, como novos
dispositivos e o total de dispositivos que estão usando o aplicativo. Também é
possível monitorar o seu aplicativo
<!--[creating custom charts](app-monitoring.html#custom-charts),-->[configurando
alertas](app-monitoring.html#alerts) e [monitorando travamentos do aplicativo](app-monitoring.html#monitor-app-crash).

# rellinks

## Referência da API
{: #api}
* [API de REST![Ícone de link externo](../../icons/launch-glyph.svg "Ícone de link externo")](https://mobile-analytics-dashboard.{DomainName}/analytics-service/ "Ícone de link externo"){:new_window}
