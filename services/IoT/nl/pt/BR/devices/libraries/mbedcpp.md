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


# mBed C++ para desenvolvedores de dispositivos
{: #mbedcpp}

Use a [biblioteca do cliente mBed C++](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/) para conectar [dispositivos mBed](https://www.mbed.com/en/), como [LPC1768](https://developer.mbed.org/platforms/mbed-LPC1768/) ou [FRDM-K64F](https://developer.mbed.org/platforms/FRDM-K64F/), facilmente ao serviço do {{site.data.keyword.iot_full}}.
{:shortdesc}

Para obter mais informações, consulte [ibmiotf](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTF/) em [developer.mbed.org](https://developer.mbed.org/).

Embora a biblioteca use C++, ainda evita alocações de memória dinâmica e o uso de funções STL, pois os dispositivos mBed às vezes têm modelos de memória idiossincráticos que tornam a portabilidade difícil. De qualquer forma, a biblioteca permite que você torne o uso de memória tão previsível quanto possível.

## Dependências
{: #dependencies}

|Dependência |Descrição|
|:---|:---|
|[Biblioteca Eclipse Paho MQTT](https://developer.mbed.org/teams/mqtt/code/MQTT/)|Fornece uma biblioteca do cliente MQTT para dispositivos mBed. Para obter mais informações, veja [Bibliotecas do cliente Embedded MQTT C/C++](http://www.eclipse.org/paho/clients/c/embedded/)|
|[Biblioteca EthernetInterface](https://developer.mbed.org/users/mbed_official/code/EthernetInterface/)|Uma biblioteca de IP mBed por Ethernet.|

## Como usar a biblioteca
{: #library_use}

Use o [compilador mBed](https://developer.mbed.org/compiler/) para criar seus aplicativos ao usar a biblioteca do cliente mBed C++ IBMIoTF. O compilador mBed fornece um IDE (ambiente de desenvolvimento integrado) C/C++ leve on-line configurado para gravar, compilar e fazer download de programas para execução em seu microcontrolador mBed.

**Nota:** você não precisa instalar ou configurar nada para iniciar a execução de mBed.

Para obter informações sobre como conectar um microcontrolador ARM mBed NXP LPC 1768 ao {{site.data.keyword.iot_short_notm}}, veja a orientação [Biblioteca do cliente mBed C++ para o IBM Watson IoT Platform](https://developer.ibm.com/recipes/tutorials/mbed-c-client-library-for-ibm-iot-foundation/).

## Construtor
{: #constructor}

O construtor cria a instância do cliente e aceita os parâmetros a seguir:

|Parâmetro |Descrição |
|:---|:---|
|`org` |O ID de sua organização. Esse valor é requerido. Se estiver usando um fluxo de iniciação rápida, especifique `quickstart`.|
|`type`   |O tipo de seu dispositivo. Este campo é requerido.|
|`id`   |O ID de seu dispositivo. Este campo é requerido.|
|`auth-method`   |O método de autenticação, que é um campo opcional necessário apenas para um fluxo registrado. O único valor atualmente suportado é `token`.|
|`auth-token`   |Um token de autenticação para conectar seu dispositivo de forma segura ao Watson IoT Platform. Este é um campo opcional necessário apenas para um fluxo registrado.|

Esses parâmetros criam definições que são usadas para interagir com o serviço do {{site.data.keyword.iot_short_notm}}.

A amostra de código a seguir descreve como uma instância de DeviceClient pode interagir com o serviço de iniciação rápida do {{site.data.keyword.iot_short_notm}}:

```
  #include "DeviceClient.h"
  ....
  ....

  // Set {{site.data.keyword.iot_short_notm}} connection parameters
  char organization[11] = "quickstart";     // For a registered connection, replace with your org
  char deviceType[8] = "LPC1768";           // For a registered connection, replace with your device type
  char deviceId[3] = "01";                  // For a registered connection, replace with your device id

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId);

  // Get the DeviceID(MAC Address) if we are in quickstart mode and device ID is not specified
  if((strcmp(organization, QUICKSTART) == 0) && (strcmp("", deviceId) == 0))
  {
  	char tmpBuf[50];
  	client.getDeviceId(tmpBuf, sizeof(tmpBuf));
  }
  ....
```

Conforme mostrado na amostra de código anterior, se o ID do dispositivo não for especificado, DeviceClient usa o endereço de Controle de Acesso à Mídia (MAC) do dispositivo como o ID do dispositivo para se conectar ao {{site.data.keyword.iot_short_notm}}. O código de dispositivo pode usar o método `getDeviceId()` para recuperar o ID do dispositivo da instância de DeviceClient.

O bloco de códigos a seguir mostra como criar uma instância de DeviceClient para interagir com a organização registrada do {{site.data.keyword.iot_short_notm}}.

```
  #include "DeviceClient.h"
  ....
  ....

  // Set {{site.data.keyword.iot_short_notm}} connection parameters
  char organization[11] = "hrcl78";
  char deviceType[8] = "LPC1768";
  char deviceId[3] = "LPC176801";
  char method[6] = "token";
  char token[9] = "password";

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);
  ....
```

## Conectando-se ao {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

O dispositivo pode se conectar ao {{site.data.keyword.iot_short_notm}} chamando a função connect na instância de DeviceClient.

```
  #include "DeviceClient.h"
  ....
  ....

  // Create DeviceClient
  IoTF::DeviceClient client(organization, deviceType, deviceId, method, token);

  bool status = client.connect();

```
Após a conexão bem-sucedida, o dispositivo pode publicar eventos no {{site.data.keyword.iot_short_notm}} e pode receber comandos.

Além disso, o dispositivo pode consultar o status da conexão usando o método `isConnected()`, que é mostrado no exemplo a seguir:

```
  #include "DeviceClient.h"
  ....
  ....

  client.isConnected();

```


## Publicando eventos
{: #publishing_events}

Eventos são o mecanismo pelo qual os dispositivos publicam dados no {{site.data.keyword.iot_short_notm}}. O dispositivo controla o conteúdo do evento e designa um nome para cada evento que ele envia.

Quando um evento é recebido pela instância do {{site.data.keyword.iot_short_notm}}, as credenciais do evento recebido identificam o dispositivo de envio, o que significa que um dispositivo não pode personificar outro dispositivo.

Eventos podem ser publicados em qualquer um dos três [níveis de qualidade de serviço (QoS)](../../reference/mqtt/index.html#qos-levels) definidos pelo protocolo MQTT. Por padrão, os eventos são publicados em QoS 0.

### Publicar evento usando a qualidade de serviço padrão

A amostra abaixo demonstra como publicar os pontos de dados a seguir no {{site.data.keyword.iot_short_notm}} no formato JSON:

- LPC1768, como o eixo x, y e z
- Posição do joystick
- Leitura da temperatura atual

```
	boolean status = client.connect();

	// Create buffer to hold the event
	char buf[250];

	// Construct an event message with desired datapoints in JSON format
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf);
	....
```
Para a amostra completa, consulte[ IBMIoTClientLibrarySample](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp).

### Aumentando o nível de QoS (qualidade de serviço) para um evento

É possível aumentar os [níveis de QoS (qualidade de serviço)](../../reference/mqtt/index.html#qos-levels) para os eventos que são publicados. Eventos que têm um nível de QoS (qualidade de serviço) maior que `0` podem demorar mais tempo para publicar devido às informações de recebimento de confirmação adicionais incluídas.

**Nota:** o modo de fluxo de iniciação rápida suporta apenas QoS 0.

```
	#include "MQTTClient.h"

	boolean status = client.connect();

	// Create buffer to hold the event
	char buf[250];

	// Construct an event message with desired datapoints in JSON format
	sprintf(buf,
            "{\"d\":{\"myName\":\"IoT mbed\",\"accelX\":%0.4f,\"accelY\":%0.4f,\"accelZ\":%0.4f,
            \"temp\":%0.4f,\"joystick\":\"%s\",\"potentiometer1\":%0.4f,\"potentiometer2\":%0.4f}}",
            MMA.x(), MMA.y(), MMA.z(), sensor.temp(), joystickPos, ain1.read(), ain2.read());

        status = client.publishEvent("blink", buf, MQTT::QOS2);
	....
```

### Manipulando o erro de conexão perdida durante a publicação de eventos


Quando o método `publishEvent()` retornar o valor false, será possível verificar o status da conexão e chamar `reConnect()` se a conexão for perdida.

```
	#include "MQTTClient.h"

	status = client.publishEvent("blink", buf, MQTT::QOS2);

	if(status == false) {
	    // Check if connection is lost and retry
	    while(!client.isConnected())
	    {
	        client.reConnect();
	        wait(5.0);
	    }
	}
	....
```
A biblioteca não armazena os eventos que são publicados durante o estado desconectado, portanto, o dispositivo precisa chamar o método `publishEvent()` novamente para enviar esses eventos após a conexão ser restabelecida.


## Manipulando comandos
{: #handling_commands}

Quando o cliente do dispositivo se conecta, ele automaticamente assina todos os comandos para esse dispositivo. Para processar comandos específicos, você precisa registrar um método de retorno de chamada de comando.
As mensagens são retornadas como uma instância da classe de comandos que tem as propriedades a seguir:

|Propriedade |Descrição|
|:---|:---|
|`command` | O nome do comando que foi chamado.|  
|`format`  |O formato do evento. O formato pode ser qualquer sequência, por exemplo, JSON. |
|`payload`  |Os dados para a carga útil do comando. O comprimento máximo é 131072 bytes. |


O código a seguir define uma função de retorno de chamada de comando de amostra que processa o comando de intervalo de intermitência do LED (diodo emissor de luz) do aplicativo e configura o identificador da função na instância de DeviceClient para que o método de retorno de chamada seja executado sempre que o dispositivo receber o comando de intermitência.

```
    #include "DeviceClient.h"
    #include "Command.h"

    // Process the command and set the LED blink interval
    void processCommand(IoTF::Command &cmd)
    {
        if (strcmp(cmd.getCommand(), "blink") == 0)
    	{
    	    char *payload = cmd.getPayload();
    	    char* pos = strchr(payload, '}');
    	    if (pos != NULL) {
    	        *pos = '\0';
    	        char* ratepos = strstr(payload, "rate");
    	        if(ratepos == NULL)
    	            return;
    	        if ((pos = strchr(ratepos, ':')) != NULL)
    	        {
    	            int blink_rate = atoi(pos + 1);
    	            blink_interval = (blink_rate <= 0) ? 0 : (blink_rate > 50 ? 1 : 50/blink_rate);
    	        }
    	    }
    	} else {
            WARN("Unsupported command: %s\n", cmd.getCommand());
        }
    }

    client.setCommandCallback(processCommand);

    client.yield(1000);  // allow the MQTT client to receive messages
    ....
```
Para a amostra completa, consulte[ IBMIoTClientLibrarySample](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/file/e58533b6bc6b/src/Main.cpp).

**Nota:** a função `client.yield()` deve ser chamada periodicamente para receber comandos.
A função `client.yield()` permite que o dispositivo receba comandos do Watson IoT Platform e mantenha a conexão ativa. Se a função `client.yield()` não for chamada dentro do prazo especificado pelo intervalo keepAlive, quaisquer comandos que forem enviados da plataforma não serão recebidos pelo dispositivo. O valor designado à função `client.yield()` especifica a duração (em milissegundos) para leitura de dados do soquete antes que o controle seja retornado ao aplicativo.

## Desconectando o cliente
{: #disconnect_client}

Para desconectar o cliente e liberar as conexões, execute o fragmento de código a seguir:

```
	...
	client.disconnect();
	....
```
## Amostras
{: #samples}

[IBMIoTClientLibrarySample](https://developer.mbed.org/teams/IBM_IoT/code/IBMIoTClientLibrarySample/) é uma amostra de código que mostra como usar a biblioteca do cliente do {{site.data.keyword.iot_short_notm}} para conectar os dispositivos mbed LPC1768 ou FRDM-K64F à instância de serviço.
