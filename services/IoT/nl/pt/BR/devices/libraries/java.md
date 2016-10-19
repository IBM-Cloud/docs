---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Java para desenvolvedores de dispositivos
{: #java}

Última atualização: 02 de agosto de 2016
{: .last-updated}


É possível usar Java para construir e customizar dispositivos que interagem com sua organização no {{site.data.keyword.iot_full}}. Use as informações e exemplos que são fornecidos para iniciar o desenvolvimento de seus dispositivos usando Java.
{:shortdesc}

## Fazendo download de cliente e recursos de Java
{: #java_client_download}

Para acessar as bibliotecas do cliente Java e as amostras para o {{site.data.keyword.iot_short_notm}}, acesse o repositório [iot-java](https://github.com/ibm-watson-iot/iot-java) no GitHub e conclua as instruções de instalação.


## Construtor
{: #constructor}

O construtor cria a instância do cliente e aceita um objeto de propriedades que contém as definições a seguir:

|Definição |Descrição |
|:---|:---|
|`org` |O ID de sua organização. Este campo é requerido. Se estiver usando um fluxo de iniciação rápida, especifique `quickstart`.|
|`type`  |O tipo de seu dispositivo. Este campo é requerido.|
|`id`  |O ID de seu dispositivo. Este campo é requerido.|
|`auth-method`   |O método de autenticação a ser usado. O único valor atualmente suportado é `token`.|
|`auth-token`   |Um token de autenticação para conectar seu dispositivo de forma segura ao Watson IoT Platform.|
|`clean-session`|Um valor true ou false necessário somente se você desejar se conectar ao aplicativo no modo de assinatura durável. Por padrão, `clean-session` está configurado como `true`.|

**Nota:** para conectar o dispositivo no modo de assinatura durável, configure `clean-session` para `false`. Para obter mais informações sobre sessão limpa, consulte a seção 'Buffers de assinatura e sessão limpa' da [Documentação de MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

O objeto de propriedades cria definições que são usadas para interagir com o módulo do {{site.data.keyword.iot_short_notm}}.

O código a seguir mostra um dispositivo publicando eventos no modo de iniciação rápida.

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

Em vez de usar um objeto de propriedades diretamente, é possível usar um arquivo de configuração que contém os pares nome-valor para as propriedades. Se você estiver usando um arquivo de configuração que contém um objeto de propriedades, use o formato do código a seguir:

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

Conecte-se ao {{site.data.keyword.iot_short_notm}} chamando a função connect. A função connect aceita um parâmetro booleano opcional `autoRetry`, que é `true` por padrão. O parâmetro `autoRetry` permite que a biblioteca se reconecte quando ocorre um erro MqttException. Observe que a biblioteca não tenta se reconectar quando ocorre um erro MqttSecurityException porque detalhes de registro do dispositivo incorretos foram usados, mesmo se o parâmetro `autoRetry` estiver configurado para `true`.

```
DeviceClient myClient = new DeviceClient(options);

myClient.connect(true);
```

Após a conexão bem-sucedida com o serviço do {{site.data.keyword.iot_short_notm}}, o cliente do dispositivo pode executar operações, como publicar eventos e assinar comandos do dispositivo a partir de um aplicativo.


## Publicando eventos
{: #publishing_events}

Eventos são o mecanismo pelo qual os dispositivos publicam dados no {{site.data.keyword.iot_short_notm}}. O dispositivo controla o conteúdo do evento e designa um nome para cada evento que ele envia.

Quando um evento é recebido pela instância do {{site.data.keyword.iot_short_notm}}, as credenciais do evento recebido identificam o dispositivo de envio, o que significa que um dispositivo não pode personificar outro dispositivo.

Eventos podem ser publicados em qualquer um dos três [níveis de qualidade de serviço (QoS)](../../reference/mqtt/index.html#qos-levels) definidos pelo protocolo MQTT. Por padrão, os eventos são publicados em QoS=0.

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

É possível aumentar os [níveis de QoS (qualidade de serviço)](../../reference/mqtt/index.html#qos-levels) para os eventos que são publicados. Eventos que têm um nível de QoS (qualidade de serviço) maior que zero podem demorar mais tempo para publicar devido às informações de recebimento de confirmação adicionais incluídas.

```
myClient.connect();

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

//Registered flow allows 0, 1 and 2 QoS
myClient.publishEvent("status", event, 2);
```

### Publicar evento usando HTTP

Além de MQTT, os dispositivos podem publicar eventos no {{site.data.keyword.iot_short_notm}} usando HTTP (Protocolo de Transporte de Hipertexto) e usando as etapas a seguir:

* Construir a instância DeviceClient usando o arquivo de propriedades.
* Construir um evento que precisa ser publicado.
* Especificar o nome do evento e publicar o evento usando o método `publishEventOverHTTP()`, conforme mostrado no código a seguir:

``` sourceCode
DeviceClient myClient = new DeviceClient(deviceProps);

JsonObject event = new JsonObject();
event.addProperty("name", "foo");
event.addProperty("cpu",  90);
event.addProperty("mem",  70);

int httpCode = myClient.publishEventOverHTTP("blink", event);
```

É possível localizar o código inteiro no exemplo do dispositivo [HttpDeviceEventPublish].

Com base nas configurações do arquivo de propriedades, o método `publishEventOverHTTP()` publica o evento no modo de iniciação rápida ou no modo de fluxo registrado. Quando o ID da Organização no arquivo de propriedades é `quickstart`, o método `publishEventOverHTTP()` publica o evento no serviço de iniciação rápida de exemplo do dispositivo e publica o evento em formato HTTP (Protocolo de Transporte de Hipertexto) simples. Quando uma organização registrada válida é usada no arquivo de propriedades, esse método sempre publica o evento em HTTPS (Protocolo de Transporte de Hipertexto Seguro), que é HTTP (Protocolo de Transporte de Hipertexto) sobre SSL, de forma que todas as comunicações sejam protegidas.

O protocolo HTTP (Protocolo de Transporte de Hipertexto) fornece entrega 'no máximo uma vez', o que é semelhante ao nível de qualidade de serviço 'no máximo uma vez' (QoS 0) do protocolo MQTT. Ao usar entrega 'no máximo uma vez' para publicar eventos, o aplicativo deve implementar a lógica de nova tentativa quando ocorrer um erro.

[HttpDeviceEventPublish]: https://github.com/ibm-messaging/iot-device-samples/blob/master/java/device-samples/src/main/java/com/ibm/iotf/sample/client/device/HttpDeviceEventPublish.java

## Manipulando comandos
{: #handling_commands}

Quando o cliente do dispositivo se conecta, ele automaticamente assina todos os comandos para esse dispositivo. Para processar comandos específicos, você precisa registrar um método de retorno de chamada de comando.
As mensagens são retornadas como uma instância da classe de comandos que tem as propriedades a seguir:

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

Para obter uma lista de amostras de dispositivos e de gerenciamento de dispositivos desenvolvidas usando a biblioteca do cliente Java do {{site.data.keyword.iot_short_notm}}, consulte o [Repositório do GitHub](https://github.com/ibm-messaging/iot-device-samples/tree/master/java).
