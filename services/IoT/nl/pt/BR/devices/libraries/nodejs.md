---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-09-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Node.js para desenvolvedores de dispositivos
{: #nodejs}

É possível adaptar as bibliotecas do cliente e as amostras em Node.js para construir e desenvolver código do dispositivo que interaja com sua organização no {{site.data.keyword.iot_full}}.
{:shortdesc}

Use as informações e exemplos que são fornecidos para iniciar o desenvolvimento de seus dispositivos usando Node.js.

## Fazendo download de cliente e recursos do Node.js
{: #node.js_client_downloads}

Para acessar as bibliotecas do cliente em Node.js para o {{site.data.keyword.iot_short_notm}} e outros recursos disponíveis, acesse o repositório [iot-nodejs](https://github.com/ibm-watson-iot/iot-nodejs) no GitHub e conclua as instruções de instalação.


Para obter mais informações, consulte os recursos a seguir:

- [Amostras para dispositivos](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples) no Github
- O repositório [ibmiotf](https://www.npmjs.com/package/ibmiotf) no NPM

## Construtor
{: #constructor}

O construtor constrói a instância do cliente do dispositivo. Ele aceita um JSON de configuração que contém as definições a seguir:

|Definição |Descrição |
|:---|:---|
|`org` |O ID de sua organização.|
|`type`  |O tipo de seu dispositivo. Normalmente, o deviceType é um agrupamento de dispositivos que executam uma tarefa específica, por exemplo, "weatherballoon".|
|`id`  |O ID de seu dispositivo. Normalmente, para um tipo de dispositivo especificado, o deviceId é um identificador exclusivo desse dispositivo, por exemplo, um número de série ou um endereço de Controle de Acesso à Mídia.|
|`auth-method`   |O método de autenticação a ser usado. O único valor atualmente suportado é `token`.|
|`auth-token`   |Um token de autenticação para conectar seu dispositivo de forma segura ao Watson IoT Platform. Este campo será obrigatório se `auth-method` for `token`.|

**Nota:** se desejar usar o serviço de iniciação rápida, você precisará enviar apenas as três primeiras propriedades.

```
    var iotf = require("ibmiotf");
    var config = {
		"org" : "organization",
		"id" : "deviceId",
		"type" : "deviceType",
		"auth-method" : "token",
		"auth-token" : "authToken"
    };


    var deviceClient = new iotf.IotfDevice(config);
```

### Usando um arquivo de configuração

Em vez de passar a configuração diretamente, é possível usar um arquivo de configuração JSON para fornecer as propriedades de configuração necessárias, conforme mostrado no exemplo a seguir:


```  
    var iotf = require("ibmiotf");
    var config = require("./device.json");
    var deviceClient = new iotf.IotfDevice(config);  
```
The `device.json` configuration file must be in the following format:

```
	{
	  "org": "xxxxx",
	  "type": "raspi",
	  "id": "pi1",
	  "auth-method" : "token",
	  "auth-token" : "xxxxxxxxxxxxxxxx"
	}

```  

## Conectando-se ao {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

É possível conectar-se ao {{site.data.keyword.iot_short_notm}} chamando a função `connect`.

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//setting the log level to debug. By default its 'warn'
	deviceClient.log.setLevel('debug');

	deviceClient.connect();

	deviceClient.on('connect', function(){
		var i=0;
		console.log("connected");
		setInterval(function function_name () {
			i++;
			deviceClient.publish('myevt', 'json', '{"value":'+i+'}', 2);
		},2000);
	});

```

Após a conexão bem-sucedida com o serviço do {{site.data.keyword.iot_short_notm}}, o cliente do dispositivo envia um evento `connect`. Esse processo significa que toda a lógico do dispositivo pode ser implementada dentro desta função de retorno de chamada.

O cliente do dispositivo tenta se reconectar automaticamente quando perde a conexão. Quando a reconexão for bem-sucedida, o cliente enviará um evento `reconnect`.

## Criação de log
{: #logging}

Por padrão, apenas eventos de log do tipo *warn* são registrados. Se você deseja aumentar ou diminuir o nível de criação de log, use a função log.setLevel. Os níveis de log a seguir são suportados:
- rastreamento
- depuração
- informativa
- aviso
- error

```
	var iotf = require("ibmiotf");
	var config = require("./device.json");

	var deviceClient = new iotf.IotfDevice(config);

	//setting the log level to debug. By default its 'warn'
	deviceClient.log.setLevel('debug');

```


## Publicando eventos
{: #publishing_events}

Eventos são o mecanismo pelo qual os dispositivos publicam dados no {{site.data.keyword.iot_short_notm}}. O dispositivo controla o conteúdo do evento e designa um nome para cada evento que ele envia.

Quando um evento é recebido pela instância do {{site.data.keyword.iot_short_notm}}, as credenciais do evento recebido identificam o dispositivo de envio, o que significa que um dispositivo não pode personificar outro dispositivo.

É possível aumentar o nível de qualidade de serviço (QoS) para os eventos que são publicados. Eventos com um nível de QoS (qualidade de serviço) maior que `0` podem demorar mais tempo para serem publicados devido às informações de recebimento de confirmação adicionais incluídas.

**Nota:** o modo de fluxo de iniciação rápida suporta apenas um nível de QoS (qualidade de serviço) igual a `0`.


Eventos podem ser publicados com as propriedades a seguir:

|Propriedade |Descrição|
|:---|:---|
|`eventType`  | O tipo de evento a ser publicado, por exemplo, status ou GPS. |  
|`eventFormat`  |O formato do evento, por exemplo, JSON. |
|`data`  | A carga útil do evento, que deve ser uma sequência de buffers. |
|`QoS`  | A qualidade de serviço MQTT para o evento de publicação. Os valores suportados são 0, 1 e 2.|


```
    var deviceClient = new Client.IotfDevice(config);

    deviceClient.connect();

    deviceClient.on("connect", function () {
       //publish an event at the default quality of service
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

       //publish an event at the user-defined quality of service
       var myQosLevel=2
       deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);
  });

```

## Manipulando comandos
{: #handling_commands}

Quando o cliente do dispositivo conecta, ele automaticamente assina qualquer comando para esse dispositivo. Para processar comandos específicos, deve-se registrar uma função de retorno de chamada de comando. O cliente do dispositivo chama a função de retorno de chamada de comando quando um comando é recebido. A função de retorno de chamada tem as propriedades a seguir:

|Propriedade |Descrição|
|:---|:---|
|`commandName`  | Uma sequência, especificando o nome do comando que foi chamado. |  
|`format`  | Uma sequência, especificando o formato do evento, por exemplo, JSON. |
|`payload`  | Uma sequência, especificando os dados para a carga útil do comando.  |
|`topic`  | Ao publicar como um dispositivo, a sequência de tópicos não inclui o tipo de dispositivo ou o ID do dispositivo; estes são obtidos do identificador de cliente.  Por exemplo, `iot-2/evt/event_id/fmt/format_string`.  Ao publicar como um aplicativo ou gateway em nome de um dispositivo, o tópico deve incluir o tipo de dispositivo e o ID do dispositivo.  Por exemplo, `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`.|


```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publish an event at the default quality of service
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("command", function (commandName,format,payload,topic) {
		if(commandName === "blink") {
			console.log(blink);
			//function to be performed for this command
			blink(payload);
		} else {
			console.log("Command not supported.. " + commandName);
		}
	});

```

## Manipulando erros
{: #handling_errors}

Quando o cliente do dispositivo encontra um erro, ele envia um evento *error*.

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	deviceClient.on("connect", function () {
		//publish an event at the default quality of service
		deviceClient.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

	});

	deviceClient.on("error", function (err) {
		console.log("Error : "+err);
	});
	....

```

## Desconectando o cliente
{: #disconnecting_client}

A amostra a seguir demonstra como é possível desconectar o cliente e liberar a conexão:

```
	var deviceClient = new Client.IotfDevice(config);

	deviceClient.connect();

	client.on("connect", function () {
		//publish an event at the default quality of service
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}');

		//publishing event at the user-defined quality of service
		var myQosLevel=2
		client.publish("status","json",'{"d" : { "cpu" : 60, "mem" : 50 }}', myQosLevel);

		//disconnect the client
		client.disconnect();
	});

	....
```
