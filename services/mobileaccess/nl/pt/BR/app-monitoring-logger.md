---

copyright:
  years: 2015, 2016
  
---

# Ativando, configurando e usando o Criador de logs
{: #enable-logger}
Última atualização: 6 de maio de 2016
{: .last-updated}

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

Assegure-se de que tenha inicializado o {{site.data.keyword.amashort}} client SDK antes de usar a estrutura de criação de log. As amostras a seguir demonstram o uso básico de uma estrutura de criação de log do {{site.data.keyword.amashort}} client SDK.

**Importante**: as funções de monitoramento do serviço {{site.data.keyword.amashort}} são planejadas para
serem migradas para o novo serviço do [ {{site.data.keyword.mobileanalytics_short}}](https://console.ng.bluemix.net/catalog/services/mobile-analytics). O novo Swift SDK alavanca o novo serviço {{site.data.keyword.mobileanalytics_short}}, que fornece uma experiência analítica muito mais rica. O serviço {{site.data.keyword.mobileanalytics_short}} está atualmente em fase experimental com planos de se tornar geralmente disponível posteriormente este ano. Recomendamos investigar a migração de seus aplicativos para usar o novo serviço {{site.data.keyword.mobileanalytics_short}} e o Swift SDK, uma vez que as funções de monitoramento do serviço {{site.data.keyword.amashort}} estão planejadas para serem descontinuadas quando o {{site.data.keyword.mobileanalytics_short}} estiver geralmente disponível.

### Android
{: #enable-logger-android}

```Java
BMSClient.getInstance().initialize(context, appRoute, appGUID);

Logger logger = Logger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");
```

### iOS - Objective-C
{: #enable-logger-objectc}

**Importante:** embora o Objective-C SDK permaneça totalmente suportado e ainda seja considerado o SDK primário para o {{site.data.keyword.Bluemix}} Mobile Services, ele está planejado para ser descontinuado posteriormente este ano em favor do novo Swift SDK.

O Objective-C SDK relata dados de monitoramento para o Monitoring Console do serviço {{site.data.keyword.amashort}}. Se você depende das funções de monitoramento do serviço {{site.data.keyword.amashort}}, continue a usar o Objective-C SDK.

```Objective-C
[[IMFClient sharedInstance] initializeWithBackendRoute:appRoute backendGUID:appGUID];

IMFLogger *logger = [IMFLogger loggerForName:@"myLogger"];

[logger logDebugWithMessages:@"debug"];
[logger logInfoWithMessages:@"info"];
[logger logWarnWithMessages:@"warn"];
[logger logErrorWithMessages:@"error"];
[logger logFatalWithMessages:@"fatal"];

```

### iOS - Swift
{: #enable-logger-swift}

```Swift
IMFClient.sharedInstance().initializeWithBackendRoute(appRoute, backendGUID: appGuid)

let logger = IMFLogger(forName: "myLogger");

logger.logDebugWithMessages("debug");
logger.logInfoWithMessages("info");
logger.logWarnWithMessages("warn");
logger.logErrorWithMessages("error");
logger.logFatalWithMessages("fatal");
```

**Nota:** o {{site.data.keyword.amashort}} client SDK é implementado com Objective-C; portanto, pode ser necessário incluir o arquivo `IMFLoggerExtension.swift` em seu projeto do Swift para usar a API do criador de logs anterior. É possível localizar esse arquivo no [archive do {{site.data.keyword.amashort}} client SDK](https://hub.jazz.net/git/bluemixmobilesdk/imf-ios-sdk/archive?revstr=master).


### Cordova
{: #enable-logger-android-cordova}

```JavaScript
BMSClient.initialize(appRoute , appGUID);

var logger = MFPLogger.getInstance("myLogger");

logger.debug("debug info");
logger.info("info message");
logger.warn("warning message");
logger.error("error message");
logger.fatal("fatal message");

```

É possível localizar os métodos adicionais a seguir em classes do Criador de logs:

* `setCapture` - Ativa ou desativa informações de log
persistentes a serem enviadas para o serviço {{site.data.keyword.amashort}}
posteriormente.
* `setLevel` - Configura o nível de log mínimo para salvar mensagens de log.
* `send` - Envia logs persistidos para o serviço {{site.data.keyword.amashort}}.

Por exemplo, quando a captura estiver ATIVADA e o nível do criador de logs estiver configurado
como FATAL, o criador de logs irá capturar exceções não capturadas. Exceções não capturadas geralmente aparecem para os usuários como travamentos do aplicativo, mas não capturam nenhum log que levariam para o evento de travamento. Ou então, um nível de criador de logs mais detalhado garante que os logs que levam a uma entrada do criador de logs FATAL, tal com WARN e ERROR, também sejam capturados.

**Nota:** Localize referências completas da API do criador de logs para cada plataforma em [SDKs, amostras, referência da API](sdks-samples-apis.html). A API do criador de logs faz parte do Núcleo do {{site.data.keyword.amashort}} client SDK.


## Uso de Amostra
{: #sample-logger-usage}

Os fragmentos de código a seguir mostram o uso do criador de logs de amostra:

### Android
{: #enable-logger-sample-android}

```Java
// Enable persisting logs
Logger.setCapture(true);

// Set the minimum log level to be printed and persisted
Logger.setLevel(Logger.LEVEL.INFO);

// Create two logger instances
Logger logger1 = Logger.getInstance("logger1");
Logger logger2 = Logger.getInstance("logger2");

// Log messages with different levels
logger1.debug("debug message");
logger2.info("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
Logger.send();
```

### iOS - Objective-C
{: #enable-logger-sample-objectc}

```Objective-C
// Enable persisting logs
[IMFLogger setCapture:YES];

// Start capturing uncaught exceptions
[IMFLogger captureUncaughtExceptions];

// Set the minimum log level to be printed and persisted
[IMFLogger setLogLevel:IMFLogLevelInfo];

// Create two logger instances
IMFLogger *logger1 = [IMFLogger loggerForName:@"logger1"];
IMFLogger *logger2 = [IMFLogger loggerForName:@"logger2"];

// Log messages with different levels
[logger1 logDebugWithMessages:@"debug message"];
[logger2 logInfoWithMessages:@"info message"];

// Send persisted logs to the {{site.data.keyword.amashort}} service
[IMFLogger send];
```

### iOS - Swift
{: #enable-logger-sample-swift}

```Swift
// Enable persisting logs
IMFLogger.setCapture(true)

// Start capturing uncaught exceptions
IMFLogger.captureUncaughtExceptions()

// Set the minimum log level to be printed and persisted
IMFLogger.setLogLevel(IMFLogLevel.Info)

// Create two logger instances
let logger1 = IMFLogger(forName: "logger1");
let logger2 = IMFLogger(forName: "logger2");

// Log messages with different levels
logger1.logDebugWithMessages("debug message")
logger2.logInfoWithMessages("info message")

// Send persisted logs to the {{site.data.keyword.amashort}} service
IMFLogger.send()

```

### Cordova
{: #enable-logger-sample-cordova}

```JavaScript
// Enable persisting logs
MFPLogger.setCapture(true);

// Set the minimum log level to be printed and persisted
MFPLogger.setLevel(MFPLogger.INFO);

// Create two logger instances
var logger1 = MFPLogger.getInstance("logger1");
var logger2 = MFPLogger.getInstance("logger2");    

// Log messages with different levels
logger1.debug("debug message");
logger2.info("info message");

// Send persisted logs to the {{site.data.keyword.amashort}} service
MFPLogger.send(success, failure);
```

## Ativando os logs internos do {{site.data.keyword.amashort}} client SDK
{: #enable-logger-sdklogs}
Esse recurso está disponível atualmente somente na versão Android do {{site.data.keyword.amashort}} client SDK.

O {{site.data.keyword.amashort}} client SDK fornece uma experiência melhor de desenvolvimento por não aumentar desnecessariamente a saída Logcat com suas mensagens de depuração interna. Portanto, por padrão, as mensagens de log interno que são produzidas pelo
{{site.data.keyword.amashort}} SDK com o nível DEBUG não são impressas. É possível ativar a impressão de todas as mensagens de log interno do {{site.data.keyword.amashort}} client SDK com a API a seguir:


```
Logger.setSDKInternalLoggingEnabled(true);
```
