---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Desenvolvendo gateways no {{site.data.keyword.iot_short_notm}} usando Java
{: #java_cli_gw}

Se os seus dispositivos não puderem se conectar diretamente à sua organização no {{site.data.keyword.iot_full}}, será possível construir e customizar gateways usando Java™. Uma biblioteca do cliente Java para {{site.data.keyword.iot_short_notm}}, documentação e exemplos são fornecidos para ajudá-lo na introdução ao desenvolvimento do gateway.
{:shortdesc}

## Fazendo download de cliente e recursos de Java
{: #java_client_download}

Para acessar as bibliotecas do cliente Java e as amostras para o {{site.data.keyword.iot_short_notm}}, acesse o repositório [iot-java](https://github.com/ibm-watson-iot/iot-java) no GitHub e conclua as instruções de instalação.

## Construtor
{: #constructor}

O construtor constrói a instância do cliente de gateway e aceita o objeto `Properties`, que contém as definições a seguir:

|Definição |Descrição |
|:----|:----|
|`org`|Um valor obrigatório que deve ser configurado para o ID de sua organização. Se estiver usando um fluxo de iniciação rápida, especifique `quickstart`.|
|`domain`|A URL do terminal do sistema de mensagens, que é opcional. Se você não especificar um valor para um domínio, a URL usará como padrão `internetofthings.ibmcloud.com`, que é o servidor de produção do {{site.data.keyword.iot_short_notm}}.|
|`type`|Um valor necessário que especifica o tipo do gateway.|
|`id` |Um valor necessário que especifica o ID exclusivo do gateway.|
|`auth-method`|O método de autenticação a ser usado. O único método que é suportado é `token`.|
|`auth-token`|Um token de autenticação de chave API para conectar com segurança seu gateway ao {{site.data.keyword.iot_short_notm}}.|
|`clean-session`|Um valor true ou false necessário somente se você desejar se conectar ao gateway no modo de assinatura durável. Por padrão, `clean-session` é configurado como true.|
|`WebSocket`|Um valor true ou false necessário somente se você desejar se conectar ao gateway usando websockets.|
|`Porta`|O número da porta a qual se conectar. Especifique 8883 ou 443. Se você não especificar um número de porta, o cliente se conectará ao {{site.data.keyword.iot_short_notm}} no número de porta 8883 por padrão.|
|`MaxInflightMessages`|Configura o número máximo de mensagens em andamento para a conexão. O valor padrão é 100.|
|`Automatic-Reconnect`|Um valor true ou false necessário quando você desejar reconectar automaticamente o gateway ao {{site.data.keyword.iot_short_notm}} enquanto ele estiver em um estado desconectado. O valor-padrão é false.|
|`Disconnected-Buffer-Size`|O número máximo de mensagens que podem ser armazenadas na memória enquanto o cliente está desconectado. O valor-padrão é
5000.|

**Nota:** para conectar o gateway no modo de assinatura durável, configure `clean-session` como `false`. Para obter mais informações sobre sessão limpa, consulte a seção 'Buffers de assinatura e sessão limpa' da [Documentação de MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

O objeto `Properties` cria definições que são usadas para interagir com o módulo do {{site.data.keyword.iot_short_notm}}.

A amostra de código a seguir mostra como construir uma instância do cliente de gateway:

```java
Properties options = new Properties();
options.setProperty("org", "<Your organization ID>");
options.setProperty("type", "<The gateway device type>");
options.setProperty("id", "The gateway device ID");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "API token");
GatewayClient gwClient = new GatewayClient(options);

```


### Usando um arquivo de configuração

Em vez de usar o objeto `Properties` diretamente para criar uma instância de gateway, é possível usar um arquivo de configuração que contém os pares nome-valor para as propriedades do gateway. Para usar um arquivo de configuração para construir o objeto `Properties` para o gateway, use o formato de código a seguir:

```Java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
...
```

O conteúdo do arquivo de configuração deve estar no seguinte formato:

```java
[Gateway]
org=$orgId
domain=$domain
typ=$myGatewayDeviceType
id=$myGatewayDeviceId
auth-method=token
auth-token=$token

```

## Conectando-se ao {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Para conectar-se ao {{site.data.keyword.iot_short_notm}}, use a função `connect()`. A função `connect()` inclui um parâmetro booleano opcional chamado `autoRetry`, que determina se a biblioteca tentará se reconectar quando uma conexão de exceção MQTT (MqttException) falhar. Por padrão, `autoRetry` está configurado como true. Se uma conexão MqttSecurityException falha devido a detalhes incorretos de registro de dispositivo transmitidos, a biblioteca não tenta se reconectar, mesmo se `autoRetry` estiver configurado como true.

Para configurar o intervalo keep-alive para MQTT, é possível usar opcionalmente o método `setKeepAliveInterval(int)` antes de chamar a função `connect()`. O valor `setKeepAliveInterval(int)` é medido em segundos e define o intervalo de tempo máximo entre mensagens que são enviadas ou recebidas. Quando um valor `setKeepAliveInterval(int)` é especificado, o cliente pode detectar que o servidor não está mais disponível sem esperar que o término do período de tempo limite de TCP/IP seja atingido. O cliente assegura que pelo menos uma mensagem seja transmitida pela rede em cada período de intervalo keep-alive. Se zero mensagens relacionadas a dados são recebidas durante o período de tempo limite, o cliente envia uma pequena mensagem de `ping`, que o servidor reconhece. Por padrão, `setKeepAliveInterval(int)` é configurado para 60 segundos. Para desativar o recurso de processamento keep-alive no cliente, configure o valor `setKeepAliveInterval(int)` como 0.

```java
Properties props = GatewayClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient.connect();
```

Para controlar o número de novas tentativas que ocorrem quando uma conexão falha, use a função connect(int numberOfTimesToRetry) sobrecarregada.

```java
GatewayClient gwClient = new GatewayClient(props);
gwClient.setKeepAliveInterval(80);
gwClient .connect(10);
```

Depois que o cliente de gateway se conecta com sucesso ao {{site.data.keyword.iot_short_notm}}, o gateway pode publicar eventos e assinar comandos para si mesmo e também em nome dos dispositivos que estão conectados ao gateway.

## Registrando dispositivos protegidos pelo gateway
{: #register_device_gateway}

É possível registrar dispositivos que estão protegidos pelo gateway que está conectado à sua instância do {{site.data.keyword.iot_short_notm}} automaticamente ou desenvolvendo código usando a API.

### Registro de dispositivo automático
Será possível registrar seus dispositivos no {{site.data.keyword.iot_short_notm}} automaticamente sempre que o gateway publicar quaisquer eventos ou assinar quaisquer comandos para os dispositivos conectados a ele.

### Registro de dispositivo da API
Também será possível usar a API do {{site.data.keyword.iot_short_notm}} para registrar dispositivos que estiverem protegidos por um gateway na instância do {{site.data.keyword.iot_short_notm}}.

Para simplificar o desenvolvimento com a API do {{site.data.keyword.iot_short_notm}}, inicie uma instância do cliente da API chamando o método api(), que é descrito na amostra de código a seguir:

```java
import com.ibm.iotf.client.api.APIClient;
....

GatewayClient gwClient = new GatewayClient(props);
gwClient.connect();

APIClient api = gwClient.api();
```
Ao receber o identificador do cliente da API, é possível iniciar o registro de dispositivos em um gateway, que é descrito na amostra de código a seguir:

```java
gwClient.connect();

  String deviceToBeAdded = "{\"deviceId\": \"" + DEVICE_ID +
					"\",\"authToken\": \"qwer123\"}";

    JsonParser parser = new JsonParser();
    JsonElement input = parser.parse(deviceToBeAdded);
    JsonObject response = this.gwClient.api().registerDeviceUnderGateway(DEVICE_TYPE, gwDeviceId, gwDeviceType, input);

```

Quando um dispositivo que está protegido por um gateway é registrado, o dispositivo é associado ao gateway pelos valores dos atributos `gwDeviceId` e `gwDeviceType`.

## Publicando eventos
{: #publish_events}

Eventos são o mecanismo pelo qual os gateways e os dispositivos publicam dados no {{site.data.keyword.iot_short_notm}}. O gateway ou o dispositivo controla o conteúdo do evento e designa um nome para cada evento que ele envia. Um gateway pode publicar eventos a partir dele mesmo e em nome de qualquer dispositivo conectado pelo gateway.

Quando um evento é recebido pela instância do {{site.data.keyword.iot_short_notm}}, as credenciais do evento recebido identificam o gateway de envio, o que significa que um gateway não pode personificar outro dispositivo.

Eventos podem ser publicados em qualquer um dos três [níveis de qualidade de serviço (QoS)](../../reference/mqtt/index.html#qos-levels) definidos pelo protocolo MQTT.  Por padrão, os eventos são publicados em QoS=0.

### Código para publicar eventos de gateway no nível de QoS padrão

```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event);
```

### Código para aumentar o nível de QoS padrão de um evento

É possível aumentar os [níveis de QoS](../../reference/mqtt/index.html#qos-levels) dos eventos de gateway que são publicados. Os eventos que têm um nível de QoS maior que zero podem demorar mais para serem publicados em razão das informações de recebimento de confirmação extras incluídas.


```java
gwClient.connect();
  JsonObject event = new JsonObject();
  event.addProperty("name", "foo");
  event.addProperty("cpu",  90);
  event.addProperty("mem",  70);

gwClient.publishGatewayEvent("status", event, 2);
```

### Código para publicar eventos em formatos customizados

Os eventos podem ser publicados em diferentes formatos, por exemplo, JSON, sequência, binário e mais. Por padrão, a biblioteca publica eventos no formato JSON, mas se você preferir, será possível especificar os dados em diferentes formatos. Por exemplo, para publicar dados no formato de sequência, use o fragmento de código a seguir:

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishGatewayEvent("load", data, "text", 2);
```

**Observação:** no exemplo de código anterior, a carga útil do evento deve estar no formato de sequência.

Os dados XML podem ser convertidos no formato de sequência e publicados conforme descritos na amostra de código a seguir:

```java
status = gwClient.publishGatewayEvent("load", xmlConvertedString, "xml", 2);
```

Da mesma forma, para publicar eventos no formato binário, use a matriz de bytes que é descrita no exemplo a seguir:

```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishGatewayEvent("blink", cpuLoad , "binary", 1);
```

### Código para publicar eventos por meio de dispositivos
{: #publishing_events_devices}

Um gateway pode publicar eventos em nome de qualquer dispositivo que seja conectado pelo gateway passando os valores type ID e device ID apropriados do evento original, que é descrito na amostra a seguir:

```java

gwClient.connect()

//Generate the event to be published
    JsonObject event = new JsonObject();
    event.addProperty("name", "foo");
    event.addProperty("cpu",  60);
    event.addProperty("mem",  40);

// publish the event on behalf of device
gwClient.publishDeviceEvent(deviceType, deviceId, eventName, event);
```

Use o método `publishDeviceEvent()` sobrecarregado para publicar o evento de dispositivo em um nível de qualidade de serviço preferencial. Para obter mais informações sobre a estrutura de tópico usada, veja [Conectividade MQTT para gateways](../mqtt.html).

### Código para publicar eventos de dispositivo que estão em um formato customizado

Semelhante aos eventos de gateway, os eventos de dispositivo também podem ser publicados em formatos diferentes. Por padrão, a biblioteca publica eventos de dispositivo no formato JSON, mas se você preferir, será possível especificar os dados em formatos diferentes. Por exemplo, para publicar dados no formato de sequência, use a amostra de código a seguir:

```java
gwClient.connect();
String data = "cpu:80";
boolean status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", data, "text", 2);
```

**Nota:** a carga útil do evento deve estar no formato de sequência.

Todos os dados XML podem ser convertidos no formato de sequência e publicados conforme mostrado no exemplo a seguir:

```java
status = gwClient.publishDeviceEvent(deviceType, deviceId, "load", xmlConvertedString, "xml", 2);
```

Da mesma forma, para publicar eventos de dispositivo no formato binário, use a matriz de bytes descrita no exemplo a seguir:
```java
gwClient.connect();
byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = gwClient.publishDeviceEvent(deviceType, deviceId, "blink", cpuLoad , "binary", 1);
```

## Manipulando comandos
{: #handling_commands}

O gateway pode assinar comandos que são direcionados no próprio gateway e para qualquer dispositivo que seja conectado com a proteção de um gateway. Quando o cliente de gateway se conecta, ele assina automaticamente todos os comandos desse gateway. Mas para assinar todos os comandos dos dispositivos que são conectados por meio do gateway, use o método `subscribeToDeviceCommands()` sobrecarregado, que é descrito no exemplo a seguir:

```java
gwClient.connect()

// subscribe to commands on behalf of device
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

Para processar comandos específicos, é necessário registrar um método de retorno de chamada `Command`. As mensagens são retornadas como uma instância da classe `Command` e contêm as propriedades a seguir:


| Propriedade     |Tipo de Dados     | Descrição|
|----------------|----------------|---------------
|`deviceType`|Seqüência de caracteres| O tipo de dispositivo para o qual o comando é recebido.|
|`deviceId`|Seqüência de caracteres| O ID do dispositivo para o qual o comando é recebido, que pode ser o gateway ou um dispositivo que é conectado por meio do gateway.|
|`data`|Objeto| A carga útil do comando.|
|`format`|Seqüência de caracteres| O formato da carga útil do comando, que pode ser qualquer sequência, por exemplo, JSON. binário, texto ou outro.|
|`command`|Seqüência de caracteres|O nome do comando.|
|`timestamp`|org.joda.time.DateTime|A data e hora no ponto em que o comando é enviado.|

A amostra de código a seguir descreve como é possível implementar o método de retorno de chamada `Command`:

```java
import com.ibm.iotf.client.gateway.Command;
import com.ibm.iotf.client.gateway.GatewayCallback;

public class GatewayCommandCallback implements GatewayCallback, Runnable {
	// A queue to hold and process the commands
	private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

	public void processCommand(Command cmd) {
  	    queue.put(cmd);
  	}

  	public void run() {
  	    while(true) {
  	        Command cmd = queue.take();
  	        System.out.println("Command " + cmd.getData());

  	        // code to process the command
  	    }
  	}

  	/**
	 * If a gateway subscribes to a topic of a device or sends data on behalf of a device
	 * that the gateway does not have permission to connect to, the message or the subscription is ignored.
	 * This behavior is different compared with the behavior of applications, where the connection is terminated.
	 * The Gateway is notified on the the notification topic:
	 */
  	@Override
public void processNotification(Notification notification) {

}
  }

```
Quando o retorno de chamada `Command` é incluído no cliente de gateway, o método `processCommand()` é chamado sempre que qualquer comando que tenha os critérios inscritos é publicado.

A amostra de código a seguir descreve como incluir o retorno de chamada `Command` na instância do cliente de gateway.

```java
gwClient.connect()
GatewayCommandCallback callback = new GatewayCommandCallback();
gwClient.setGatewayCallback(callback);
//Subscribe to a device that is connected to the gateway
gwClient.subscribeToDeviceCommands(DEVICE_TYPE, DEVICE_ID);
```

Os métodos sobrecarregados estão disponíveis para controlar a assinatura do comando.

### Listando dispositivos que são conectados por meio de um gateway
{: #list_devices_gw}


Para recuperar todos os dispositivos que são conectados por meio do gateway especificado (typeId, deviceId) ao {{site.data.keyword.iot_short_notm}}, chame o método `getDevicesConnectedThroughGateway()`.

```java
gwClient.connect()
gwClient.api().getDevicesConnectedThroughGateway(gatewayType, gatewayId);
```

## Amostras
{: #samples}

Há várias amostras disponíveis para ajudá-lo a conectar gateways e dispositivos que estão protegidos por gateways à instância do {{site.data.keyword.iot_short_notm}}. As amostras usam a biblioteca do cliente Java do {{site.data.keyword.iot_short_notm}} e estão localizadas no [Repositório do GitHub de amostras do gateway ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples){: new_window}.

## Receitas
{: #recipes}

| Orientação     | Descrição|
|----------------|----------------
|[Conectando seu dispositivo como um gateway ao {{site.data.keyword.iot_short_notm}} ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-gateway-to-watson-iot-platform/){: new_window}| Um projeto do GitHub e instruções detalhadas que explicam como conectar um gateway Raspberry Pi e dispositivos Arduino Uno protegidos pelo gateway ao {{site.data.keyword.iot_short_notm}}.
|[Raspberry Pi como um gateway gerenciado no {{site.data.keyword.iot_short_notm}} ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/){: new_window}|Uma extensão da orientação de gateway anterior que explica como conectar seu gateway Raspberry Pi como um dispositivo gerenciado no {{site.data.keyword.iot_short_notm}} e como executar operações de gerenciamento de dispositivo.
