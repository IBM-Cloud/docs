---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java para desenvolvedores de dispositivos
{: #java}

É possível construir e customizar dispositivos que interagem com sua organização no {{site.data.keyword.iot_full}} usando Java™. Uma biblioteca do cliente Java para {{site.data.keyword.iot_short_notm}}, documentação e exemplos são fornecidos para ajudá-lo a começar com o desenvolvimento do dispositivo.
{:shortdesc}

## Fazendo download de cliente e recursos de Java
{: #java_client_download}

Para acessar as bibliotecas do cliente Java e as amostras para o {{site.data.keyword.iot_short_notm}}, acesse o repositório [iot-java](https://github.com/ibm-watson-iot/iot-java) no GitHub e conclua as instruções de instalação.

## Construtor
{: #constructor}

O construtor cria a instância do cliente e aceita o objeto `Properties`, que contém as definições a seguir:

|Definição |Descrição |
|:----|:----|
|`org` |Um valor obrigatório que deve ser configurado para o ID de sua organização. Se estiver usando um fluxo de iniciação rápida, especifique `quickstart`.|
|`type`  |Um valor obrigatório que especifica o tipo do dispositivo.|
|`id`  |Um valor obrigatório que especifica o ID exclusivo do dispositivo.|
|`auth-method`  |O método de autenticação a ser usado. O único método que é suportado é `token`.|
|`auth-token`   |Um token de autenticação para conectar seu dispositivo de forma segura ao {{site.data.keyword.iot_short_notm}}.|
|`clean-session`|Um valor true ou false necessário somente se você desejar se conectar ao aplicativo no modo de assinatura durável. Por padrão, `clean-session` é configurado como true.|
|`Porta`|O número da porta a qual se conectar. Especifique 8883 ou 443. Se você não especificar um número de porta, o cliente se conectará ao {{site.data.keyword.iot_short_notm}} no número de porta 8883 por padrão.|
|`MaxInflightMessages`  |Configura o número máximo de mensagens em andamento para a conexão. O valor padrão é 100.|
|`Automatic-Reconnect`  |Um valor true ou false que é necessário quando você deseja reconectar automaticamente o dispositivo ao {{site.data.keyword.iot_short_notm}} enquanto ele está em um estado desconectado. O valor-padrão é false.|
|`Disconnected-Buffer-Size`|O número máximo de mensagens que podem ser armazenadas na memória enquanto o cliente está desconectado. O valor-padrão é
5000.|
|`WebSocket`|Um valor true ou false necessário quando você deseja usar conexões de websocket com o {{site.data.keyword.iot_short_notm}}. O valor-padrão é false.|

**Nota:** para conectar o dispositivo no modo de assinatura durável, configure `clean-session` para `false`. Para obter mais informações sobre sessão limpa, consulte a seção 'Buffers de assinatura e sessão limpa' da [Documentação de MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

O objeto `Properties` cria definições que são usadas para interagir com o módulo do {{site.data.keyword.iot_short_notm}}.

A amostra de código a seguir mostra como os dispositivos podem publicar eventos no modo de iniciação rápida.

```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class QuickstartDeviceEventPublish {

    public static void main(String[] args) {

        //Provide the device specific data using Properties class
        Properties options = new Properties();
        options.setProperty("org", "quickstart");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Quickstart flow allows only QoS = 0
        myClient.publishEvent("status", event, 0);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

A amostra de código a seguir mostra como os dispositivos podem publicar eventos em um fluxo registrado.


```
package com.ibm.iotf.sample.client.device;

import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublish {

    public static void main(String[] args) {

        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registered flow allows 0, 1 and 2 QoS
        myClient.publishEvent("status", event);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

### Usando um arquivo de configuração

Em vez de usar o objeto `Properties` diretamente, é possível usar um arquivo de configuração que contém os pares nome-valor para as propriedades. Se você estiver usando um arquivo de configuração que contém o objeto `Properties`, use o formato do código a seguir:

```
package com.ibm.iotf.sample.client.device;

import java.io.File;
import java.util.Properties;

import com.google.gson.JsonObject;
import com.ibm.iotf.client.device.DeviceClient;

public class RegisteredDeviceEventPublishPropertiesFile {

    public static void main(String[] args) {
        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = DeviceClient.parsePropertiesFile(new File("C:\\temp\\device.prop"));

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();

        //Generate a JSON object of the event to be published
        JsonObject event = new JsonObject();
        event.addProperty("name", "foo");
        event.addProperty("cpu",  90);
        event.addProperty("mem",  70);

        //Registered flow allows 0, 1 and 2 QoS
        myClient.publishEvent("status", event, 1);
        System.out.println("SUCCESSFULLY POSTED......");

  ...
```

O conteúdo do arquivo de configuração deve estar no seguinte formato:

```
    [device]
    org=$orgId
    typ=$myDeviceType
    id=$myDeviceId
    auth-method=token
    auth-token=$token
```

## Conectando-se ao {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}


Para conectar-se ao {{site.data.keyword.iot_short_notm}}, use a função `connect()`. A função `connect()` inclui um parâmetro booleano opcional chamado `autoRetry`, que determina se a biblioteca tenta se reconectar quando há uma falha na conexão MqttException. Por padrão, `autoRetry` está configurado como true. Se uma conexão MqttSecurityException falha devido a detalhes incorretos de registro de dispositivo transmitidos, a biblioteca não tenta se reconectar, mesmo se `autoRetry` estiver configurado como true.

Para configurar o intervalo 'keep alive' para MQTT, é possível usar opcionalmente o método `setKeepAliveInterval(int)` antes de chamar a função `connect()`. O valor `setKeepAliveInterval(int)` é medido em segundos e define o intervalo de tempo máximo entre mensagens que são enviadas ou recebidas. Quando usado, o cliente pode detectar quando o servidor não está mais disponível sem aguardar o final do período de tempo limite de TCP/IP ser atingido. O cliente assegura que pelo menos uma mensagem viaje pela rede em cada período de intervalo 'keep alive'. Se zero mensagens relacionadas a dados são recebidas durante o período de tempo limite, o cliente envia uma pequena mensagem de `ping`, que o servidor reconhece. Por padrão, `setKeepAliveInterval(int)` é configurado para 60 segundos. Para desativar o recurso de processamento 'keep alive' no cliente, configure o valor `setKeepAliveInterval(int)` para 0.


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(true);
```

Para controlar o número de novas tentativas que ocorrem quando há uma falha de conexão, use a função connect(int numberOfTimesToRetry) sobrecarregada.


```
DeviceClient myClient = new DeviceClient(options);
myClient.setKeepAliveInterval(120);
myClient.connect(10);
```

Depois que seu dispositivo se conectar com sucesso ao {{site.data.keyword.iot_short_notm}}, ele poderá publicar eventos e assinar comandos de dispositivo a partir de um aplicativo.


## Publicando eventos
{: #publishing_events}

Eventos são o mecanismo pelo qual os dispositivos publicam dados no {{site.data.keyword.iot_short_notm}}. O dispositivo controla o conteúdo do evento e designa um nome para cada evento que ele envia.

Quando um evento é recebido pela instância do {{site.data.keyword.iot_short_notm}}, as credenciais do evento recebido identificam o dispositivo de envio, o que significa que um dispositivo não pode personificar outro dispositivo.

Eventos podem ser publicados em qualquer um dos três [níveis de qualidade de serviço (QoS)](../../reference/mqtt/index.html#qos-levels) definidos pelo protocolo MQTT.  Por padrão, os eventos são publicados em QoS=0.

### Publicar eventos no nível de QoS (qualidade de serviço) padrão

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

myClient.publishEvent("status", event);
```


### Aumentando o nível de QoS (qualidade de serviço) para um evento

É possível aumentar os [níveis de QoS (qualidade de serviço)](../../reference/mqtt/index.html#qos-levels) para os eventos que são publicados. Eventos com um nível de QoS (qualidade de serviço) maior que zero podem demorar mais tempo para serem publicados devido às informações extras de recebimento de confirmação que são incluídas.

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//Registered flow allows 0, 1 and 2 QoS
myClient.publishEvent("status", event, 2);
```

### Publicando eventos em formatos customizados

Os eventos podem ser publicados em diferentes formatos, por exemplo, JSON, sequência, binário e mais. Por padrão, a biblioteca publica eventos no formato JSON, mas se você preferir, será possível especificar os dados em diferentes formatos. Por exemplo, para publicar dados no formato de sequência, use o fragmento de código a seguir.

```
myClient.connect();

String data = "cpu:"+getProcessCpuLoad();
status = myClient.publishEvent("load", data, "text", 2);
```

**Observação:** no exemplo de código anterior, a carga útil do evento deve estar no formato de sequência.

Qualquer dado XML pode ser convertido para o formato de sequência e publicado como a seguir.

```
status = myClient.publishEvent("load", xmlConvertedString, "xml", 2);
```

Da mesma forma, para publicar eventos no formato binário, use a matriz de bytes que é descrita no exemplo a seguir:

```
myClient.connect();

byte[] cpuLoad = new byte[] {30, 35, 30, 25};
status = myClient.publishEvent("blink", cpuLoad , "binary", 1);
```

### Publicar eventos usando HTTP
{: #publishing_events_http}


Além de usar MQTT, também é possível configurar seus dispositivos para publicar eventos para a {{site.data.keyword.iot_short_notm}} por meio de HTTP. As etapas a seguir descrevem a sequência para publicar eventos por meio de HTTP:

1. Construa uma instância `DeviceClient` usando o arquivo de propriedades.
2. Construir um evento que precisa ser publicado.
3. Especifique o nome do evento e, depois, publique o evento usando o método`publishEventOverHTTP()`, conforme mostrado na amostra de código a seguir:

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

boolean response  = myClient.api().publishDeviceEventOverHTTP("blink", event, ContentType.json);
```

Para visualizar o código inteiro, consulte o exemplo de dispositivo [HttpDeviceEventPublish].

Com base nas configurações no arquivo de propriedades, o método `publishEventOverHTTP()` publica o evento no modo de iniciação rápida ou no modo de fluxo registrado. Quando o ID da organização no arquivo de propriedades é configurado como `quickstart`, o método `publishEventOverHTTP()` publica o evento para o serviço de iniciação rápida de exemplo do
dispositivo e publica o evento em formato HTTP simples. Quando uma organização registrada válida é especificada no arquivo de propriedades, os eventos são publicados de forma segura por meio de HTTPS.

O protocolo HTTP (Protocolo de Transporte de Hipertexto) fornece entrega 'no máximo uma vez', o que é semelhante ao nível de qualidade de serviço 'no máximo uma vez' (QoS 0) do protocolo MQTT. Ao usar a entrega 'no máximo uma vez' para publicar eventos, o aplicativo deverá implementar a lógica de nova tentativa sempre que houver um erro.

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## Manipulando comandos
{: #handling_commands}

Quando o cliente do dispositivo se conecta, ele automaticamente assina todos os comandos para esse dispositivo. Para processar comandos específicos, você precisa registrar um método de retorno de chamada de comando.
As mensagens são retornadas como uma instância da classe `Command`, que contém as propriedades a seguir:

| Propriedade     |Tipo de Dados     | Descrição|
|----------------|----------------|
|`payload` |java.lang.Cadeia| Os dados para a carga útil da mensagem.|
|`format`  |java.lang.Cadeia| O formato pode ser qualquer sequência, por exemplo, JSON.|
|`command`   |java.lang.Cadeia|Identifica o comando.|
|`timestamp`   |org.joda.time.DateTime|A data e hora do evento.|


``` sourceCode
package com.ibm.iotf.sample.client.device;

import java.util.Properties;
import java.util.concurrent.BlockingQueue;
import java.util.concurrent.LinkedBlockingQueue;


import com.ibm.iotf.client.device.Command;
import com.ibm.iotf.client.device.CommandCallback;
import com.ibm.iotf.client.device.DeviceClient;


//Implement the CommandCallback class to provide the way in which you want the command to be handled
class MyNewCommandCallback implements CommandCallback, Runnable {

    // A queue to hold & process the commands for smooth handling of MQTT messages
    private BlockingQueue<Command> queue = new LinkedBlockingQueue<Command>();

    /**
    * This method is invoked by the library whenever there is command matching the subscription criteria
    */
    @Override
    public void processCommand(Command cmd) {
        try {
            queue.put(cmd);
            } catch (InterruptedException e) {
        }
    }

    @Override
    public void run() {
        while(true) {
            Command cmd = null;
            try {
                //In this sample, we just display the command
                cmd = queue.take();
                System.out.println("COMMAND RECEIVED = '" + cmd.getCommand() + "'\twith Payload = '" + cmd.getPayload() + "'");
            } catch (InterruptedException e) {}
        }
    }
}

public class RegisteredDeviceCommandSubscribe {


    public static void main(String[] args) {

        //Provide the device specific data, as well as Auth-key and token using Properties class
        Properties options = new Properties();

        options.setProperty("org", "uguhsp");
        options.setProperty("type", "iotsample-arduino");
        options.setProperty("id", "00aabbccde03");
        options.setProperty("auth-method", "token");
        options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");

        DeviceClient myClient = null;
        try {
            //Instantiate the class by passing the properties file
            myClient = new DeviceClient(options);
        } catch (Exception e) {
            e.printStackTrace();
        }

        //Pass the above implemented CommandCallback as an argument to this device client
        myClient.setCommandCallback(new MyNewCommandCallback());

        //Connect to the {{site.data.keyword.iot_short_notm}}
        myClient.connect();
    }
}
```

## Amostras
{: #samples}

Para obter uma lista de amostras de dispositivo e de gerenciamento de dispositivo desenvolvidas usando a biblioteca de cliente Java do {{site.data.keyword.iot_short_notm}}, veja o [repositório do GitHub iot-device-samples](https://github.com/ibm-messaging/iot-device-samples/tree/master/java).
