---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java para desenvolvedores de aplicativos
{: #java}


É possível construir e customizar aplicativos que interagem com sua organização no {{site.data.keyword.iot_full}} usando Java™. Uma biblioteca do cliente Java para a {{site.data.keyword.iot_short_notm}}, documentação e exemplos são fornecidos para ajudá-lo a começar com o desenvolvimento de aplicativos.

{:shortdesc}

## Fazendo download de cliente e recursos de Java
{: #java_client_download}

Última atualização: 25 de outubro de 2016
{: .last-updated}

Para acessar as bibliotecas do cliente Java e as amostras para o {{site.data.keyword.iot_short_notm}}, acesse o repositório [iot-java](https://github.com/ibm-watson-iot/iot-java) no GitHub e conclua as instruções de instalação.


## Construtor
{: #constructor}

O construtor cria a instância do cliente e aceita o objeto `Properties`, que contém as definições a seguir:

| Definição     |Descrição     |
|----------------|----------------|
|`org` |Um valor obrigatório que deve ser configurado para o ID de sua organização. Se estiver usando um fluxo de iniciação rápida, especifique `quickstart`.|
|`id` |O ID exclusivo do aplicativo em sua organização.|
|`auth-method`  |O método de autenticação. O único método que é suportado é `apikey`.|
|`auth-key`   |Uma chave API opcional que se deve especificar ao configurar o valor de método de autenticação para `apikey`.|
|`auth-token`   |Um token de chave API que também é necessário ao configurar o valor de método de autenticação para `apikey`. |
|`clean-session`|Um valor true ou false necessário somente se você desejar se conectar ao aplicativo no modo de assinatura durável. Por padrão, `clean-session` está configurado como `true`.|
|`Porta`|O número da porta a qual se conectar. Especifique 8883 ou 443. Se você não especificar um número de porta, o cliente se conectará ao {{site.data.keyword.iot_short_notm}} no número de porta 8883 por padrão.|
|`MaxInflightMessages`  |Configura o número máximo de mensagens em andamento para a conexão. O valor padrão é 100.|
|`Automatic-Reconnect`  |Um valor true ou false que é necessário quando você deseja reconectar automaticamente o dispositivo ao {{site.data.keyword.iot_short_notm}} enquanto ele está em um estado desconectado. O valor-padrão é false.|
|`Disconnected-Buffer-Size`|O número máximo de mensagens que podem ser armazenadas na memória enquanto o cliente está desconectado. O valor-padrão é
5000.|
|`shared-subscription`|Um valor booleano que deve ser configurado como true se quiser construir aplicativos escaláveis que balanceiam a carga de mensagens entre várias instâncias do aplicativo. Para obter mais informações, consulte [Aplicativos escaláveis](../mqtt.html#scalable_apps).

O objeto `Properties` cria definições que são usadas para interagir com o módulo do {{site.data.keyword.iot_short_notm}}. Se você não especificar as propriedades para este objeto ou se especificar `quickstart`, o cliente se conecta ao serviço de iniciação rápida do {{site.data.keyword.iot_short_notm}} como um dispositivo não registado.

A amostra de código a seguir mostra como é possível construir a instância do aplicativo cliente (`ApplicationClient`) no modo `quickstart`:

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

A amostra de código a seguir mostra como é possível construir a instância do aplicativo cliente (`ApplicationClient`) no modo de fluxo registrado:

```
    Properties options = new Properties();
    options.put("org", "uguhsp");
    options.put("id", "app" + (Math.random() * 10000));
    options.put("Authentication-Method","apikey");
    options.put("API-Key", "<API-Key>");
    options.put("Authentication-Token", "<Authentication-Token>");

    ApplicationClient myClient = new ApplicationClient(options);
```

### Usando um arquivo de configuração

Em vez de incluir o objeto `Properties` diretamente, é possível usar um arquivo de configuração que contém os pares nome-valor para o objeto `Properties`, conforme descrito na amostra de código a seguir:

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
O arquivo de configuração do aplicativo especificado deve estar no formato a seguir:

```
    [application]
    org=$orgId
    id=$myApplication
    auth-method=apikey
    auth-key=$key
    auth-token=$token
    enable-shared-subscription=true|false
```

## Conectando-se ao {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Para conectar-se ao {{site.data.keyword.iot_short_notm}}, use a função `connect()`. A função `connect()` inclui um parâmetro booleano opcional chamado `autoRetry`, que determina se a biblioteca tenta se reconectar quando há uma falha na conexão MqttException. Por padrão, `autoRetry` está configurado como true. Se uma conexão MqttSecurityException falha devido a detalhes incorretos de registro de dispositivo transmitidos, a biblioteca não tenta se reconectar, mesmo se `autoRetry` estiver configurado como true.

Para configurar o intervalo 'keep alive' para MQTT, é possível usar opcionalmente o método `setKeepAliveInterval(int)` antes de chamar a função `connect()`. O valor `setKeepAliveInterval(int)` é medido em segundos e define o intervalo de tempo máximo entre mensagens que são enviadas ou recebidas. Quando usado, o cliente pode detectar quando o servidor não está mais disponível sem aguardar o final do período de tempo limite de TCP/IP ser atingido. O cliente assegura que pelo menos uma mensagem viaje pela rede em cada período de intervalo 'keep alive'. Se zero mensagens relacionadas a dados são recebidas durante o período de tempo limite, o cliente envia uma pequena mensagem de `ping`, que o servidor reconhece. Por padrão, `setKeepAliveInterval(int)` é configurado para 60 segundos. Para desativar o recurso de processamento 'keep alive' no cliente, configure o valor `setKeepAliveInterval(int)` para 0.

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    myClient.setKeepAliveInterval(120);
    myClient.connect();
```

Para controlar o número de novas tentativas que ocorrem quando há uma falha na conexão, especifique um número inteiro na função myClient.connect(), conforme descrito no fragmento de código a seguir:

```
    DeviceClient myClient = new DeviceClient(options);
    myClient.setKeepAliveInterval(120);
    myClient.connect(10);
```

Depois que seu aplicativo cliente conecta-se com sucesso ao serviço {{site.data.keyword.iot_short_notm}}, ele pode assinar eventos de dispositivos e status e também publicar dispositivo eventos e comandos de dispositivos.

## Assinando eventos de dispositivo
{: #subscribing_device_events}

Eventos são o mecanismo pelo qual os dispositivos publicam dados no {{site.data.keyword.iot_short_notm}}. O dispositivo controla o conteúdo do evento e designa um nome para cada evento que ele envia.

Quando um evento é recebido pela instância do {{site.data.keyword.iot_short_notm}}, as credenciais do evento recebido identificam o dispositivo de envio, o que significa que um dispositivo não pode personificar outro dispositivo.


Por padrão, os aplicativos assinam todos os eventos de todos os dispositivos conectados. Use o tipo de dispositivo, ID do dispositivo, evento e parâmetros de formato da mensagem para controlar o escopo da assinatura. As amostras de código a seguir mostram como é possível usar esses parâmetros para definir o escopo de uma assinatura:

### Assinando todos os eventos de todos os dispositivos


```
    myClient.connect();
    myClient.subscribeToDeviceEvents();
```
### Assinando todos os eventos de todos os dispositivos de um tipo específico


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino");
```

### Assinando todos os eventos de um dispositivo específico


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee");
```
### Assinando um evento específico de dois ou mais dispositivos diferentes

```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent");
    myClient.subscribeToDeviceEvents("iotsample-arduino", "10aabbccddee", "myEvent");
```
### Assinando eventos publicados no formato JSON


```

    myClient.connect();
    myClient.subscribeToDeviceEvents("iotsample-arduino", "00aabbccddee", "myEvent", "json", 0);
```

**Nota**: um único cliente pode suportar diversas assinaturas.

## Manipulando eventos a partir de dispositivos
{: #handling_device_events}

Para processar os eventos que são recebidos por suas assinaturas, registre um método de retorno de chamada de evento. As mensagens são retornadas como uma instância da classe de eventos que tem os parâmetros a seguir:

|Parâmetro|Tipo de Dados|Descrição|
|:---|:---|
|`event.device`|Seqüência de caracteres|Identifica o dispositivo de forma exclusiva entre todos os tipos de dispositivos na organização.|
|`event.deviceType`|Seqüência de caracteres|Identifica o tipo de dispositivo. Normalmente, o deviceType é um agrupamento de dispositivos que fazem uma tarefa específica, por exemplo, "weatherballoon" poderia ser um tipo de dispositivo.|
|`event.deviceId`|Seqüência de caracteres|Representa o ID do dispositivo. Normalmente, para um tipo de dispositivo específico, o deviceId é um identificador exclusivo desse dispositivo, por exemplo um número de série ou endereço MAC.|
|`event.event`|Seqüência de caracteres|Normalmente usado para agrupar eventos específicos, por exemplo, "status", "warning" e "data".|
|`event.format`|Seqüência de caracteres|O formato pode ser qualquer sequência, por exemplo, JSON.  |
|`event.data`|Dicionário|Os dados para a carga útil da mensagem. O comprimento máximo é 131072 bytes.|
|`event.timestamp`|Date and time|A data e hora do evento|


O código a seguir fornece uma implementação de amostra do retorno de chamada de evento:

```
  import com.ibm.iotf.client.app.Event;
  import com.ibm.iotf.client.app.EventCallback;
  import com.ibm.iotf.client.app.Command;

  import java.util.concurrent.BlockingQueue;
  import java.util.concurrent.LinkedBlockingQueue;

  /**
    * A sample Event callback class that processes the device events in a separate thread.
    *
    */
   class MyEventCallback implements EventCallback, Runnable {

	// A queue to hold and process the Events for smooth handling of MQTT messages
	private BlockingQueue<Event> evtQueue = new LinkedBlockingQueue<Event>();

	public void
processEvent(Event e) {
		try {
			evtQueue.put(e);
		} catch (InterruptedException e1) {
			e1.printStackTrace();
		}
	}

	@Override
	public void processCommand(Command cmd) {
		System.out.println("Command received:: " + cmd);
	}

	@Override
	public void run() {
		while(true) {
			Event e = null;
			try {
				e = evtQueue.take();
				// In this example, the only output is the event
				System.out.println("Event:: " + e.getDeviceId() + ":" + e.getEvent() + ":" + e.getPayload());
			} catch (InterruptedException e1) {
				// Ignore the Interuppted exception, retry
				continue;
			}
		}
	}
    }
```

Quando o retorno de chamada de evento é incluído em ApplicationClient, o método `processEvent()` é chamado sempre que um evento que corresponde à assinatura for publicado. O fragmento a seguir mostra como incluir o retorno de chamada de evento na instância ApplicationClient:



```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceEvents();
```

Semelhante à assinatura de eventos do dispositivo, o aplicativo pode assinar comandos que são enviados para os dispositivos. A amostra de código a seguir mostra como assinar todos os comandos para todos os dispositivos da organização:

```

    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToDeviceCommands();
```

Os métodos sobrecarregados estão disponíveis para controlar a assinatura do comando. O método `processCommand()` é chamado quando um comando é enviado para o dispositivo que corresponde à assinatura de comando.


## Assinando status do dispositivo
{: #subscribing_device_status}

Semelhante à assinatura de eventos de dispositivos, os aplicativos podem assinar status de dispositivos, como conexão e desconexão do dispositivo com relação ao {{site.data.keyword.iot_short_notm}}. Por padrão, essa assinatura inclui atualizações de status para todos os dispositivos conectados. Use os parâmetros tipo de dispositivo e ID do dispositivo para controlar o escopo da assinatura. As amostras de código a seguir mostram como é possível usar esses parâmetros para definir o escopo de uma assinatura:

### Assinar as atualizações de status para todos os dispositivos

```
    myClient.connect();
    myClient.subscribeToDeviceStatus();
```

### Assinar as atualizações de status para todos os dispositivos de um tipo específico


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino");
```

### Assinar as atualizações de status para dois dispositivos diferentes


```

    myClient.connect();
    myClient.subscribeToDeviceStatus("iotsample-arduino", "00aabbccddee");
    myClient.subscribeToDeviceStatus("iotsample-arduino", "10aabbccddee");
```

**Nota**: um único cliente pode suportar diversas assinaturas.

## Manipulando atualizações de status a partir de dispositivos
{: #handling_device_status_updates}

Para processar as atualizações de status que são recebidas por suas assinaturas, você precisa registrar um método de retorno de chamada de evento de status. Para os eventos de status `Connect` e `Disconnect`, as mensagens são retornadas como uma instância da classe Status, que contém os parâmetros a seguir:


| Parâmetro     |Tipo de Dados     |
|----------------|----------------|
|`status.clientAddr` |Cadeia|
|`status.protocol`  |Cadeia|
|`status.clientId`   |Cadeia|
|`status.user`   |Cadeia|
|`status.time`   |java.util.Date|
|`status.action` |Cadeia|
|`status.connectTime`   |java.util.Date|
|`status.port`|inteiro|

As propriedades a seguir são configuradas somente quando o evento de status é `Disconnect`:

| Propriedade     |Tipo de Dados     |
|----------------|----------------|
|`status.writeMsg` |inteiro|
|`status.readMsg`  |inteiro|
|`status.reason`   |Cadeia|
|`status.readBytes`   |inteiro|
|`status.writeBytes`   |inteiro|


A amostra de código a seguir fornece uma implementação de exemplo do retorno de chamada de status:

```

  private static class MyStatusCallback implements StatusCallback {

      public void processApplicationStatus(ApplicationStatus status) {
          System.out.println("Application Status = " + status.getPayload());
      }

      public void processDeviceStatus(DeviceStatus status) {
          if(status.getAction() == "Disconnect") {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction()
                                  + "  reason: " + status.getReason());
          } else {
              System.out.println("device: "+status.getDeviceId()
                                  + "  time: "+ status.getTime()
                                  + "  action: " + status.getAction());
          }
      }
  }
```

Quando o retorno de chamada de status é incluído no aplicativo cliente, o método `processDeviceStatus()` é chamado sempre que um dispositivo que corresponde aos critérios é conectado ou desconectado do {{site.data.keyword.iot_short_notm}}. A amostra de código a seguir mostra como é possível incluir a instância de retorno de chamada de status para o aplicativo cliente:

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
Os aplicativos podem assinar qualquer outro status de aplicativo, como conexão e desconexão do aplicativo para {{site.data.keyword.iot_short_notm}}. O fragmento de código a seguir mostra como assinar o status do aplicativo de uma organização {{site.data.keyword.iot_short_notm}}:

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
O método sobrecarregado está disponível para controlar a assinatura de status para um aplicativo específico. O método `processApplicationStatus()` é chamado sempre que um aplicativo que corresponde aos critérios é conectado ou desconectado do {{site.data.keyword.iot_short_notm}}.


## Publicando eventos a partir de dispositivos
{: #publishing_events_devices}

A amostra de código a seguir mostra como os aplicativos poderão publicar eventos como se eles tivessem originado de um dispositivo.

```

    myClient.connect()

    //Generate the event to be published
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

    // publish the event on behalf of device
    myClient.publishEvent(deviceType, deviceId, "blink", event);
```


Os eventos podem ser publicados em diferentes formatos, por exemplo, JSON, sequência, binário e mais. Por padrão, a biblioteca publica eventos no formato JSON, mas se você preferir, será possível especificar os dados em diferentes formatos. Por exemplo, para publicar dados no formato de sequência, use o fragmento de código a seguir.

```
    myClient.connect();
    String data = "cpu:"+60;
    status = myClient.publishEvent("load", data, "text", 2);
```
**Observação:** no exemplo de código anterior, a carga útil do evento deve estar no formato de sequência.

Qualquer dado XML pode ser convertido para sequência e publicado como a seguir:

```
    status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

Da mesma forma, para publicar eventos no formato binário, use a matriz de bytes conforme descrita no exemplo a seguir:

```
    myClient.connect();
    byte[] cpuLoad = new byte[] {60, 35, 30, 25};
    status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### Publicar eventos usando HTTP
{: #publishing_events_http}

Além de usar MQTT, também é possível configurar seus aplicativos para publicar eventos de dispositivo para {{site.data.keyword.iot_short_notm}} por meio de HTTP. As etapas a seguir descrevem a sequência para a publicação de eventos de dispositivo de publicação por meio de HTTP:

1. Construa a instância ApplicationClient usando o arquivo de propriedades.
2. Construa o evento que precisa ser publicado.
3. Especifique o nome do evento, o tipo de dispositivo e o ID do dispositivo.
4. Publique o evento usando o método `publishEventOverHTTP`(), conforme mostrado no exemplo de código a seguir:

```
    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	boolean status = myClient.publishApplicationEventforDeviceOverHTTP(deviceId, deviceType, "blink", event, ContentType.json);
```

Para obter a amostra de código completa, consulte o exemplo de aplicativo [HttpApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java).

Com base nas configurações no arquivo de propriedades, o método `publishEventOverHTTP()` publica o evento em iniciação rápida ou no fluxo registrado. Quando `quickstart` é especificado como o ID da organização no arquivo de propriedades, o método `publishEventOverHTTP()` publica o evento para o serviço de iniciação rápida do {{site.data.keyword.iot_short_notm}} em formato
de HTTP simples. Quando uma organização registrada válida é especificada no arquivo de propriedades, o evento sempre será publicado usando HTTPS (Protocolo de Transporte de Hipertexto Seguro) para que toda a comunicação seja segura.

O protocolo HTTP (Protocolo de Transporte de Hipertexto) fornece entrega 'no máximo uma vez', o que é semelhante ao nível de qualidade de serviço 'no máximo uma vez' (QoS 0) do protocolo MQTT. Ao usar entrega 'no máximo uma vez' para publicar eventos, o aplicativo deve implementar a lógica de nova tentativa quando ocorrer um erro.


## Publicando comandos para dispositivos
{: #publishing_commands_devices}

Os aplicativos podem publicar comandos em dispositivos conectados, conforme mostrado no exemplo a seguir:

```

    myClient.connect()

    //Generate the event to be published
    JsonObject data = new JsonObject();
    data.addProperty("name", "stop-rotation");
    data.addProperty("delay",  0);

    //Registered flow allows 0, 1 and 2 QoS
    myAppClient.publishCommand(deviceType, deviceId, "stop", data);
```

### Publicar comandos usando HTTP
{: #publishing_commands_http}

Além de usar MQTT, também é possível configurar seus aplicativos para publicar comandos para o dispositivo conectado por meio de HTTP. As etapas a seguir descrevem a sequência para a publicação de eventos de dispositivo usando HTTP:

1. Construa a instância ApplicationClient usando o arquivo de propriedades
2. Construa o comando que precisa ser publicado
3. Especifique o nome do comando, o tipo de dispositivo e o ID do dispositivo
4. Publique o comando usando o método `publishCommandOverHTTP`(), conforme mostrado no código a seguir:

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	// Generate a JSON object of the event to be published
	JsonObject event = new JsonObject();
	event.addProperty("reboot", 5);

	boolean response = myClient.publishCommandOverHTTP("execute", event);
```

Para visualizar a amostra de código completa, consulte o aplicativo de exemplo [HttpCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpCommandPublish.java).

O protocolo HTTP (Protocolo de Transporte de Hipertexto) fornece entrega 'no máximo uma vez', o que é semelhante ao nível de qualidade de serviço 'no máximo uma vez' (QoS 0) do protocolo MQTT. Ao usar a entrega 'no máximo uma vez' para publicar comandos, o aplicativo deve implementar a lógica de nova tentativa quando ocorre um erro. Para obter mais informações, consulte [API de REST HTTP para aplicativos](../api.html).


## Amostras
{: #samples}

-  [MQTTApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java) - Um aplicativo de amostra que demonstra como é possível publicar eventos de dispositivos.
-   [RegisteredApplicationCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java) - Um aplicativo de amostra que demonstra como é possível publicar um comando em um dispositivo.
-  [RegisteredApplicationSubscribeSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java) - Um aplicativo de amostra que demonstra como é possível assinar diferentes eventos, como eventos de dispositivos, comandos de dispositivos, status de dispositivos e status de aplicativos.
-   [SharedSubscriptionSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java) - Um aplicativo de amostra que demonstra como é possível construir um aplicativo escalável que balanceia a carga de mensagens entre diversas instâncias do aplicativo.
-  [Amostra de backup e restauração](https://github.com/ibm-messaging/iot-backup-restore-sample) - uma amostra que apresenta como é possível fazer backup e restaurar a configuração do dispositivo no {{site.data.keyword.cloudant}}.
