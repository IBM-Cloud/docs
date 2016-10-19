---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java para desenvolvedores de aplicativos
{: #java}

Última atualização: 07 de setembro de 2016
{: .last-updated}

É possível usar Java para construir e customizar aplicativos que interagem com sua organização no {{site.data.keyword.iot_full}}. Use as informações e exemplos que são fornecidos para iniciar o desenvolvimento de seus aplicativos usando Java.
{:shortdesc}

## Fazendo download de cliente e recursos de Java
{: #java_client_download}

Para acessar as bibliotecas do cliente Java e as amostras para o {{site.data.keyword.iot_short_notm}}, acesse o repositório [iot-java](https://github.com/ibm-watson-iot/iot-java) no GitHub e conclua as instruções de instalação.


## Construtor
{: #constructor}

O construtor cria a instância do cliente e aceita um objeto `Properties` que contém as definições a seguir:

| Definição     |Descrição     |
|----------------|----------------|
|`org` |O ID de sua organização. Este é um valor obrigatório. Se estiver usando um fluxo de iniciação rápida, especifique `quickstart`.|
|`id` |O ID exclusivo do aplicativo em sua organização.|
|`auth-method`  |O método de autenticação para o qual o único valor atualmente suportado é `apikey`.|
|`auth-key`   |Uma chave API (interface de programação de aplicativos) opcional necessária quando auth-method estiver configurado como `apikey`.  |
|`auth-token`   |Um token de chave API (interface de programação de aplicativos) necessário quando auth-method estiver configurado como `apikey`. |
|`clean-session`|Um valor true ou false necessário somente se você desejar se conectar ao aplicativo no modo de assinatura durável. Por padrão, `clean-session` está configurado como `true`.|
|`shared-subscription`|Um valor booleano. Configure como `true` se você gostaria de construir aplicativos escaláveis que balanceiam a carga de mensagens entre várias instâncias do aplicativo. Para obter mais informações, consulte [Aplicativos escaláveis](mqtt.html#/scalable-applications#scalable-applications).
O objeto `Properties` cria definições que são usadas para interagir com o módulo do {{site.data.keyword.iot_short_notm}}. Se você não especificar as propriedades para este objeto ou se especificar `quickstart`, o cliente se conecta ao serviço de iniciação rápida do {{site.data.keyword.iot_short_notm}} como um dispositivo não registado.

A amostra de código a seguir mostra como é possível construir a instância ApplicationClient no modo `quickstart`:

```
    import com.ibm.iotf.client.app.ApplicationClient;
    import java.util.Properties;

    Properties options = new Properties();
    options.put("org", "quickstart");

    ApplicationClient myClient = new ApplicationClient(options);
```

A amostra de código a seguir mostra como é possível construir a instância ApplicationClient no modo de fluxo registrado:

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

Em vez de incluir um objeto `Properties` diretamente, é possível usar um arquivo de configuração contendo os pares nome-valor para o objeto `Properties` no formato a seguir:

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);
    ...
```
O arquivo de configuração de aplicativo deve estar no seguinte formato:

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

Para conectar-se ao {{site.data.keyword.iot_short_notm}} use a função `connect()`. A função `connect()` inclui um parâmetro booleano opcional chamado `autoRetry` que determina se a biblioteca tenta se reconectar no caso de uma falha de conexão MqttException. Por padrão, `autoRetry` está configurado como true. Se uma conexão MqttSecurityException falhar devido a detalhes incorretos de registro de dispositivo serem passados, a biblioteca não tenta se reconectar mesmo se `autoRetry` estiver configurado como `true`.

```
    Properties props = ApplicationClient.parsePropertiesFile(new File("C:\\temp\\application.prop"));
    ApplicationClient myClient = new ApplicationClient(props);

    myClient.connect();
```

Após conectar-se com sucesso ao serviço do {{site.data.keyword.iot_short_notm}}, seus aplicativos clientes podem assinar eventos de dispositivos, assinar status de dispositivos e publicar eventos e comandos de dispositivos.

## Assinando eventos de dispositivo
{: #subscribing_device_events}

Eventos são o mecanismo pelo qual os dispositivos publicam dados no {{site.data.keyword.iot_short_notm}}. O dispositivo controla o conteúdo do evento e designa um nome para cada evento que ele envia.

Quando um evento é recebido pela instância do {{site.data.keyword.iot_short_notm}}, as credenciais do evento recebido identificam o dispositivo de envio, o que significa que um dispositivo não pode personificar outro dispositivo.


Por padrão, os aplicativos assinam todos os eventos de todos os dispositivos conectados. Use os parâmetros tipo de dispositivo, ID do dispositivo, evento e formato da mensagem para controlar o escopo da assinatura.  As amostras de código a seguir mostram como é possível usar esses parâmetros para definir o escopo de uma assinatura:

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
|`event.deviceType`|Seqüência de caracteres|Identifica o tipo de dispositivo. Normalmente, o deviceType é um agrupamento de dispositivos que executam uma tarefa específica, por exemplo, "weatherballoon".|
|`event.deviceId`|Seqüência de caracteres|Representa o ID do dispositivo. Normalmente, para um tipo de dispositivo especificado, o deviceId é um identificador exclusivo desse dispositivo, por exemplo, um número de série ou um endereço de Controle de Acesso à Mídia.|
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

Quando o retorno de chamada de status é incluído em ApplicationClient, o método `processDeviceStatus()` é chamado sempre que um dispositivo que corresponde aos critérios for conectado ou desconectado do {{site.data.keyword.iot_short_notm}}. A amostra de código a seguir mostra como é possível incluir a instância de retorno de chamada de status em ApplicationClient:

```

    myClient.connect()
    myClient.setStatusCallback(new MyStatusCallback());
    myClient.subscribeToDeviceStatus();
```
Os aplicativos podem assinar qualquer outro status de aplicativo, como conexão e desconexão do aplicativo com relação ao Watson IoT Platform. O fragmento de código a seguir mostra como assinar o status do aplicativo na organização:

```
    myClient.connect()
    myClient.setEventCallback(new MyEventCallback());
    myClient.subscribeToApplicationStatus();
```
O método sobrecarregado está disponível para controlar a assinatura de status para um aplicativo específico. O método processApplicationStatus() é chamado sempre que um aplicativo que corresponde aos critérios for conectado ou desconectado do {{site.data.keyword.iot_short_notm}}.


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

### Publicar eventos usando HTTP
{: #publishing_events_http}

Além de MQTT, é possível configurar seus aplicativos para publicar eventos de dispositivo no {{site.data.keyword.iot_short_notm}} usando HTTP (Protocolo de Transporte de Hipertexto), concluindo as etapas a seguir:

* Construa a instância ApplicationClient usando o arquivo de propriedades
* Construa o evento que precisa ser publicado
* Especifique o nome do evento, o tipo de dispositivo e o ID do dispositivo
* Publique o evento usando o método `publishEventOverHTTP`(), conforme mostrado no código a seguir:

```

    	ApplicationClient myClient = new ApplicationClient(props);

    	JsonObject event = new JsonObject();
    	event.addProperty("name", "foo");
    	event.addProperty("cpu",  90);
    	event.addProperty("mem",  70);

    	code = myClient.publishEventOverHTTP(deviceType, deviceId, "blink", event);
```

Para a amostra de código completa, consulte o exemplo de aplicativo a seguir:

[HttpApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/HttpApplicationDeviceEventPublish.java)

Com base nas configurações no arquivo de propriedades, o método `publishEventOverHTTP()` publica o evento em iniciação rápida ou no fluxo registrado. Quando `quickstart` é o ID da organização especificado no arquivo de propriedades, o método `publishEventOverHTTP()` publica o evento no serviço de iniciação rápida do {{site.data.keyword.iot_short_notm}} em formato HTTP (Protocolo de Transporte de Hipertexto) simples. Quando uma organização registrada válida é especificada no arquivo de propriedades, o evento sempre será publicado usando HTTPS (Protocolo de Transporte de Hipertexto Seguro) para que toda a comunicação seja segura.

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


## Exemplos
{: #examples}


-  [MQTTApplicationDeviceEventPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/MQTTApplicationDeviceEventPublish.java) - Um aplicativo de amostra que demonstra como é possível publicar eventos de dispositivos.
-   [RegisteredApplicationCommandPublish](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationCommandPublish.java) - Um aplicativo de amostra que demonstra como é possível publicar um comando em um dispositivo.
-  [RegisteredApplicationSubscribeSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/RegisteredApplicationSubscribeSample.java) - Um aplicativo de amostra que demonstra como é possível assinar diferentes eventos, como eventos de dispositivos, comandos de dispositivos, status de dispositivos e status de aplicativos.
-   [SharedSubscriptionSample](https://github.com/ibm-messaging/iot-application-samples/blob/master/java/standalone-samples/src/main/java/com/ibm/iotf/sample/client/application/SharedSubscriptionSample.java) - Um aplicativo de amostra que demonstra como é possível construir um aplicativo escalável que balanceia a carga de mensagens entre diversas instâncias do aplicativo.
-  [Amostra de backup e restauração](https://github.com/ibm-messaging/iot-backup-restore-sample) - Uma amostra que demonstra como é possível fazer backup e restaurar a configuração do dispositivo em um banco de dados Cloudant NoSQL.
