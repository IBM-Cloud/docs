---

copyright:
  years: 2015, 2016
  
---

# Monitorando aplicativos
{: #app-monitoring}
Última atualização: 22 de setembro de 2016
{: .last-updated}

Além de recursos de segurança, o {{site.data.keyword.amafull}} também fornece monitoramento e análise para seus aplicativos móveis. É possível registrar logs de clientes e monitorar dados com o {{site.data.keyword.amashort}} client SDK. Os desenvolvedores podem controlar quando enviar esses dados para o serviço {{site.data.keyword.amashort}}. Todos os eventos de segurança, tais como sucesso ou falha de autenticação, que ocorrem no serviço {{site.data.keyword.amashort}} são registrados automaticamente.
<!--
**Note**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

Quando os dados são entregues para o {{site.data.keyword.amashort}}, é possível usar o Painel de monitoramento do {{site.data.keyword.amashort}} para obter insights da análise sobre seus aplicativos móveis, dispositivos e logs do cliente. As informações sobre solicitações que seu aplicativo faz aos recursos que são protegidos por {{site.data.keyword.amashort}} são registradas por padrão.

Os dados registrados automaticamente incluem informações como número de autenticações, novos dispositivos e novos usuários. Além disso, é possível configurar o {{site.data.keyword.amashort}} client SDK para relatar as informações a seguir:

### Estatísticas de uso de seus aplicativos móveis
{: #usage-stats}

É possível configurar seus aplicativos móveis para registrar eventos do ciclo de vida do aplicativo e enviar os dados registrados ao serviço {{site.data.keyword.amashort}} com algumas chamadas API simples. É possível registrar o número de
aberturas de apps, notificações push recebidas, etc.

### Captura de log do lado do cliente
{: #client-side-logcapture}

Aplicativos no campo ocasionalmente apresentam problemas que requerem atenção
do desenvolvedor para serem corrigidos. Muitas vezes é difícil reproduzir
esses problemas. Desenvolvedores que trabalharam no código podem não ter o
ambiente ou o dispositivo exato com o qual testar. Nessas situações,
é útil ter a capacidade de recuperar logs de depuração a partir de dispositivos
clientes conforme os problemas ocorrem no ambiente em que
acontecem.

### Preservar dados capturados
{: #preserve-captureddata}

Não há como garantir que todos os dados capturados sejam preservados no lado do cliente. Seus
usuários podem estar executando o aplicativo móvel offline e
acumulando simultaneamente dados analíticos e de log capturados. Como
o cliente está offline com espaço de sistema de arquivos limitado, eventos registrados
mais antigos devem ser limpos em favor da preservação de eventos registrados mais
recentemente. Cabe ao desenvolvedor decidir quando enviar dados capturados ao serviço {{site.data.keyword.amashort}} usando as APIs fornecidas.

## Usando o Painel de monitoramento do {{site.data.keyword.amashort}}
{: #monitoring-dashboard}

1. Abra o Painel {{site.data.keyword.Bluemix}} e clique em seu aplicativo {{site.data.keyword.Bluemix_notm}}.

2. Quando seu painel do aplicativo {{site.data.keyword.Bluemix_notm}} for aberto, clique em um tile do {{site.data.keyword.amashort}}.

3. Clique no botão **Monitoramento** na navegação do
Painel {{site.data.keyword.amashort}}.


## Ativando, configurando e usando o Criador de logs
{: #enable-logger}

O {{site.data.keyword.amashort}} client SDK fornece uma estrutura de criação de log que é semelhante a outras estruturas de log com as quais você pode estar familiarizado, tais como, `java.util.logging` ou `log4j`. A estrutura de criação de log suporta várias instâncias do criador de logs por pacote, diferentes níveis de log, captura ou rastreios de pilha para um travamento de aplicativo e mais.

Também é possível configurar os dados registrados para que sejam persistidos em um
armazenamento local, o qual pode ser enviado para o serviço
{{site.data.keyword.amashort}} on demand.

A estrutura de criação de log do {{site.data.keyword.amashort}} client SDK suporta os níveis de log a seguir, listados do menos para o mais detalhado, com as diretrizes de uso recomendadas:

* `FATAL` - Usar para travamentos ou interrupções irrecuperáveis. O nível FATAL
é reservado para registrar erros irrecuperáveis, que aparecem
para usuários, como uma paralisação do aplicativo.
* `ERROR`: Usar para exceções inesperadas ou erros de protocolo de rede inesperados.
* `WARN` - Para registrar avisos de uso que não são considerados
erros críticos, como o uso de APIs descontinuadas ou resposta de rede lenta.
* `INFO` - Use para relatar eventos de inicialização e outros
dados que possam ser úteis.
* `DEBUG` - Use para relatar instruções de depuração para ajudar
os desenvolvedores a resolver defeitos do aplicativo.

#### Cenário de nível de log
{: #log-level-scenario}

Quando o nível do criador de logs estiver configurado como `FATAL`, o criador de logs capturará exceções de não captura, mas não capturará logs que levam ao evento de travamento. É possível configurar um nível do criador de logs mais detalhado para assegurar que os logs que podem levar a uma entrada do criador de logs `FATAL`, como `WARN` e `ERROR`, também sejam capturados.

Assegure-se de que tenha inicializado o {{site.data.keyword.amashort}} client SDK antes de usar a estrutura de criação de log. As amostras a seguir demonstram o uso básico de uma estrutura de criação de log do {{site.data.keyword.amashort}} client SDK.

<!-- **Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available.-->

#### Android
{: #enable-logger-android}

```Java BMSClient.getInstance().initialize(this.getApplicationContext(), BMSClient.REGION_US_SOUTH); // Make sure that you point to your region
Logger logger = Logger.getLogger("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

O parâmetro **bluemixRegion** especifica qual implementação do Bluemix você está usando, por exemplo, `BMSClient.REGION_US_SOUTH` e `BMSClient.REGION_UK`. 

#### iOS - Swift
{: #enable-logger-swift}

```Swift
BMSClient.sharedInstance.initialize(bluemixRegion: BMSClient.REGION_US_SOUTH) // You can change the region
Analytics.initializeWithAppName(your_app_name_here, apiKey: your_api_key_here, hasUserContext: false, deviceEvents: DeviceEvent.LIFECYCLE)

let logger = Logger.logger(forName: "myLogger")

logger.debug(“debug info")
logger.info(“info message")
logger.warn(“warning message")
logger.error(“error message")
logger.fatal(“fatal message")
```
{: codeblock}
<!--
**Note:** The {{site.data.keyword.amashort}} client SDK is implemented with Objective-C, therefore you might need to add the `IMFLoggerExtension.swift` file to your Swift project to use the previous logger API. You can find this file in the [{{site.data.keyword.amashort}} client SDK archive](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).
-->

#### Cordova
{: #enable-logger-android-cordova}

```JavaScript
BMSClient.initialize(BMSClient.REGION_US_SOUTH); // You can change the region

var logger = BMSLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```
{: codeblock}

É possível localizar os métodos adicionais a seguir em classes do Criador de logs:

* `setCapture` - Ativa ou desativa informações de log
persistentes a serem enviadas para o serviço {{site.data.keyword.amashort}}
posteriormente.
* `setLevel` - Configura o nível de log mínimo para salvar mensagens de log.
* `send` - Envia logs persistidos para o serviço {{site.data.keyword.amashort}}.

Por exemplo, quando a captura estiver ATIVADA e o nível do criador de logs estiver configurado
como FATAL, o criador de logs irá capturar exceções não capturadas. Exceções não capturadas geralmente aparecem para os usuários como travamentos do aplicativo, mas não capturam nenhum log que levariam para o evento de travamento. Ou então, um nível de criador de logs mais detalhado garante que os logs que levam a uma entrada do criador de logs FATAL, tal com WARN e ERROR, também sejam capturados.

**Nota:** Localize referências completas da API do criador de logs para cada plataforma em [SDKs, amostras, referência da API](sdks-samples-apis.html). A API do criador de logs faz parte do Núcleo do {{site.data.keyword.amashort}} client SDK.


### Amostra de uso do criador de logs
{: #sample-logger-usage}

Os fragmentos de código a seguir mostram o uso do criador de logs de amostra:

#### Android
{: #enable-logger-sample-android}

```Java
// Configure Logger to save logs to the device so that they 
// can later be sent to the {{site.data.keyword.amashort}} service
// Disabled by default; set to true to enable
Logger.storeLogs(true);

// Change the minimum log level (optional) // The default setting is Logger.LEVEL.DEBUG Logger.setLogLevel(Logger.LEVEL.INFO);

// Create two logger instances // You can create multiple log instances to organize your logs Logger logger1 = Logger.getLogger("logger1"); Logger logger2 =
Logger.getLogger("logger2");

// Log messages with different levels // Debug message for feature 1 // Info message for feature 2 logger1.debug("debug message"); //the logger1.debug message is not
logged because the logLevelFilter is set to Info logger2.info("info message");

// Send logs to the {{site.data.keyword.amashort}} service
Logger.send();
```
{: codeblock}

#### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Configure Logger to save logs to the device so that they can later be sent to the {{site.data.keyword.amashort}} service
// Disabled by default; set to true to enable
Logger.logStoreEnabled = true

// Change the minimum log level (optional) // The default setting is LogLevel.Debug Logger.logLevelFilter = LogLevel.Info

// Create two logger instances // You can create multiple log instances to organize your logs let logger1 = Logger.logger(forName: "feature1Logger") let logger2 =
Logger.logger(forName: "feature2Logger")

// Log messages with different levels logger1.debug("debug message for feature 1") 
//the logger1.debug message is not logged because the logLevelFilter is set to Info logger2.info("info message for feature 2")

// Send logs to the {{site.data.keyword.amashort}} service
Logger.send()
```
{: codeblock}

#### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Enable persisting logs
BMSLogger.setCapture(true);

// Set the minimum log level to be printed and persisted
BMSLogger.setLevel(BMSLogger.INFO);

// Create two logger instances
var logger1 = BMSLogger.getInstance("logger1");
var logger2 = BMSLogger.getInstance("logger2");    

// Log messages with different levels
logger1.debug("debug message");
logger2.info("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
BMSLogger.send(success, failure);
```
{: codeblock}

### Ativando os logs internos do {{site.data.keyword.amashort}} client SDK
{: #enable-logger-sdklogs}
Esse recurso está disponível atualmente somente na versão Android do {{site.data.keyword.amashort}} client SDK.

O {{site.data.keyword.amashort}} client SDK fornece uma experiência melhor de desenvolvimento por não aumentar desnecessariamente a saída Logcat com suas mensagens de depuração interna. Portanto, por padrão, as mensagens de log interno que são produzidas pelo
{{site.data.keyword.amashort}} SDK com o nível DEBUG não são impressas. É possível ativar a impressão de todas as mensagens de log interno do {{site.data.keyword.amashort}} client SDK com a API a seguir:


```
Logger.setSDKInternalLoggingEnabled(true);
```
{: codeblock}

## Reunindo análise de uso
{: #usage-analytics}

É possível configurar o {{site.data.keyword.amashort}} client SDK para registrar a análise de uso e enviar os dados registrados ao serviço {{site.data.keyword.amashort}}.
<!--
**Important**: The monitoring functions of the {{site.data.keyword.amashort}} service are planned to be migrated to the new [{{site.data.keyword.mobileanalytics_short}} service](https://console.ng.bluemix.net/catalog/services/mobile-analytics). The new Swift SDK leverages the new {{site.data.keyword.mobileanalytics_short}} service, which provides a much richer analytics experience. The {{site.data.keyword.mobileanalytics_short}} service is currently in experimental phase with plans to be made generally available later this year. We recommend investigating migrating your applications to use the new {{site.data.keyword.mobileanalytics_short}} service and Swift SDK since the monitoring functions of {{site.data.keyword.amashort}} service are planned to be discontinued when {{site.data.keyword.mobileanalytics_short}} is generally available. -->

**Nota:** Assegure-se de que tenha ativado a captura de criação de log antes de iniciar o registro da análise de uso.

Use as APIs a seguir para iniciar a gravação e o envio da análise de uso:

#### Android
{: #usage-analytics-android}

```Java
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.disable();
	
// Enable recording of usage analytics Analytics.enable();
	
Analytics.log(eventJSONObject);
	
// Send recorded usage analytics to the Mobile Analytics Service Analytics.send();
```
{: codeblock}

#### iOS - Swift
{: #usage-analytics-swift}

```Swift
// Disable recording of usage analytics (for example, to save disk space)
// Recording is enabled by default
Analytics.enabled = false

// Enable recording of usage analytics Analytics.enabled = true

// Send recorded usage analytics to the {{site.data.keyword.mobileanalytics_short}} Service
Analytics.send()
```
{: codeblock}

#### Cordova
{: #usage-analytics-cordova}

```JavaScript
// Enable usage analytics recording
BMSAnalytics.enable();

// Send recorded usage analytics to the {{site.data.keyword.amashort}} Service
BMSAnalytics.send();
```
{: codeblock}

**Nota:** Quando estiver desenvolvendo aplicativos Cordova, use a API nativa para ativar a gravação do evento de ciclo de vida do aplicativo.
