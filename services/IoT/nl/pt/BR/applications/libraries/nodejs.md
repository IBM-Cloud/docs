---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-07-29"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



# Node.js para desenvolvedores de aplicativos
{: #nodejs}

Última atualização: 29 de julho de 2016
{: .last-updated}

É possível adaptar as bibliotecas do cliente e as amostras em Node.js para construir e customizar aplicativos que interagem com sua organização no {{site.data.keyword.iot_full}}.
{:shortdesc}

Use as informações e exemplos que são fornecidos para iniciar o desenvolvimento de seus aplicativos usando Node.js.

## Fazendo download de cliente e recursos do Node.js
{: #nodejs_client_download}

Para acessar as bibliotecas do cliente em Node.js para o {{site.data.keyword.iot_short_notm}} e outros recursos disponíveis, acesse o repositório [iot-nodejs](https://github.com/ibm-watson-iot/iot-nodejs) no GitHub e conclua as instruções de instalação.


Para obter mais informações, consulte os recursos a seguir:
- [Amostras de aplicativos](https://github.com/ibm-watson-iot/iot-nodejs/tree/master/samples) no GitHub.
- [ibmiotf](https://www.npmjs.com/package/ibmiotf) no NPM.
- Seção [Referência](#reference_nodejs) deste documento.


## Construtor
{: #constructor}

O construtor cria a instância do aplicativo cliente e aceita um arquivo de configuração JSON que contém as propriedades a seguir:

| Propriedade     |Descrição     |
|----------------|----------------|
|`org` |O ID de sua organização. Este é um valor obrigatório.|
|`id`  |O ID exclusivo de seu aplicativo dentro de sua organização.|
|`auth-key`   |Uma chave API (interface de programação de aplicativos) para conectar seu aplicativo de forma segura ao Watson IoT Platform.|
|`auth-token`   |Um token de chave API (interface de programação de aplicativos) para conectar seu dispositivo de forma segura ao Watson IoT Platform.|
|`type`  |O tipo de assinatura. Especifique `shared` para ativar a assinatura compartilhada.|


Para usar iniciação rápida, apenas as duas primeiras propriedades são necessárias.

```
  var Client = require("ibmiotf");
	var appClientConfig = {
		"org" : orgId,
		"id" : appId,
		"auth-key" : apiKey,
		"auth-token" : apiToken
	}

	var appClient = new Client.IotfApplication(appClientConfig);
```


### Usando um arquivo de configuração


Em vez de passar as propriedades JSON diretamente, também é possível usar um arquivo de configuração que está esboçado na amostra de código a seguir:

```

  var Client = require("ibmiotf");
	var appClientConfig = require("./application.json");
	var appClient = new Client.IotfApplication(appClientConfig);
```

Assegure que o arquivo de configuração JSON esteja no formato a seguir:

```
    {
	  "org": 'xxxxx',
	  "id": 'myapp',
	  "auth-key": 'a-xxxxxxx-zenkqyfiea',
	  "auth-token": 'xxxxxxxxxx'
    }
```


## Conectando-se ao {{site.data.keyword.iot_short_notm}}
{: #connecting_to_iotp}

Para se conectar ao {{site.data.keyword.iot_short_notm}}, envie uma solicitação *connect*, conforme a seguir:

```
  var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

	//Add your code here
	});
```

Após conectar-se com sucesso ao serviço do {{site.data.keyword.iot_short_notm}}, o aplicativo cliente envia um evento `connect` para que qualquer lógica possa ser implementada dentro desta função de retorno de chamada.



O aplicativo cliente tenta se reconectar automaticamente quando perde a conexão. Quando a reconexão for bem-sucedida, o cliente enviará um evento `reconnect`.



## Criação de log
{: #logging}

Por padrão, apenas eventos de log do tipo `warn` são registrados. Se você deseja aumentar ou diminuir o nível de criação de log, use a função `log.setLevel`. Os níveis de log a seguir são suportados:
- rastreamento
- depuração
- informativa
- aviso
- error

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
```

## Assinaturas compartilhadas
{: #shared_subscriptions}

Use o recurso de assinatura compartilhada para construir aplicativos escaláveis que balanceiam a carga de mensagens entre várias instâncias do aplicativo. Para ativar o balanceamento de carga, configure o campo `type` para `shared`, o que é mostrado no exemplo a seguir:

```

	var appClientConfig = {
	  org: 'xxxxx',
	  id: 'myapp',
	  "auth-key": 'a-xxxxxx-xxxxxxxxx',
	  "auth-token": 'xxxxx!xxxxxxxx',
	  "type" : "shared" // make this connection as shared subscription
	};
	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
```

## Manipulando erros
{: #handling_errors}

Quando o aplicativo cliente encontra um erro, um evento `error` é gerado.

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();
	//setting the log level to 'trace'
	appClient.log.setLevel('trace');
	appClient.on("connect", function () {

	//Add your code here
	});
	appClient.on("error", function (err) {
		console.log("Error : "+err);
	});
```

## Assinando eventos de dispositivo
{: #subscribing_device_events}

Eventos são o mecanismo pelo qual os dispositivos publicam dados na instância do {{site.data.keyword.iot_short_notm}}. O dispositivo controla o conteúdo do evento e designa um nome para cada evento que ele envia.

Quando um evento é recebido pela instância do {{site.data.keyword.iot_short_notm}}, as credenciais do evento recebido identificam o dispositivo de envio, o que significa que um dispositivo não pode personificar outro dispositivo.


Por padrão, os aplicativos assinam todos os eventos de todos os dispositivos conectados. Use os parâmetros tipo de dispositivo, ID do dispositivo, evento e formato da mensagem para controlar o escopo da assinatura. As amostras de código a seguir mostram como é possível usar esses parâmetros para definir o escopo de uma assinatura:

### Assinando todos os eventos de todos os dispositivos


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents();
	});
```

### Assinando todos os eventos de todos os dispositivos de um tipo específico

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("mydeviceType");
	});
```

### Assinando um evento específico de todos os dispositivos


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("+","+","myevent");
	});
```

### Assinando um evento específico de dois ou mais dispositivos diferentes

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","myevent");
		appClient.subscribeToDeviceEvents("myOtherDeviceType","device02","myevent");
	});
```

### Assinando todos os eventos publicados no formato JSON


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
```

**Nota**: um único cliente pode suportar diversas assinaturas.

### Manipulando eventos a partir de dispositivos


Para processar os eventos que são recebidos por suas assinaturas, implemente um método de retorno de chamada de evento. O aplicativo cliente {{site.data.keyword.iot_short_notm}} envia o evento `deviceEvent`. Esta função possui as seguintes propriedades:

- deviceType
- deviceId
- eventType
- formatar
- payload
- t¢pico

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceEvents("myDeviceType","device01","+","json");

	});
	appClient.on("deviceEvent", function (deviceType, deviceId, eventType, format, payload) {

		console.log("Device Event from :: "+deviceType+" : "+deviceId+" of event "+eventType+" with payload : "+payload);

	});
```


## Assinando status do dispositivo
{: #subscribing_device_status}

Por padrão, quando você assina status de dispositivo, atualizações de status são recebidas para todos os dispositivos conectados. Use os parâmetros tipo e ID para controlar o escopo da assinatura. Um único cliente pode suportar várias assinaturas.

### Assinando atualizações de status para todos os dispositivos

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus();

	});
```

### Assinando atualizações de status para todos os dispositivos de um tipo específico


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType");

	});
```

### Assinando atualizações de status para dois dispositivos diferentes

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
```

### Manipulando atualizações de status a partir de dispositivos

Para processar as atualizações de status que são recebidas por suas assinaturas, implemente um método de retorno de chamada de status de dispositivo. O aplicativo cliente {{site.data.keyword.iot_short_notm}} envia o evento `deviceStatus`. Esta função possui as seguintes propriedades:

-   deviceType
-   deviceId
-   payload
-   t¢pico

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		appClient.subscribeToDeviceStatus("myDeviceType","device01");
		appClient.subscribeToDeviceStatus("myOtherDeviceType","device02");

	});
	appClient.on("deviceStatus", function (deviceType, deviceId, payload, topic) {

		console.log("Device status from :: "+deviceType+" : "+deviceId+" with payload : "+payload);

	});
```


## Publicando eventos a partir de dispositivos
{: #publishing_device_events}


Os aplicativos podem publicar eventos como se eles tivessem originado de um dispositivo. A função requer as propriedades a seguir:

-   deviceType
-   deviceId
-   eventType
-   formatar
-   dados


```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50};
		myData = JSON.stringify(myData);
		appClient.publishDeviceEvent("myDeviceType","device01", "myEvent", "json", myData);

	});
```


## Publicando comandos para dispositivos
{: #publishing_commands_devices}

Os aplicativos podem publicar comandos para dispositivos conectados. A função requer as propriedades a seguir:

-   deviceType
-   deviceId
-   eventType
-   formatar
-   dados

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10};
		myData = JSON.stringify(myData);
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

	});
```


## Desconectando o cliente
{: #disconnect_client}

A amostra a seguir desconecta o cliente e também libera as conexões:

```

	var appClient = new Client.IotfApplication(appClientConfig);

	appClient.connect();

	appClient.on("connect", function () {

		var myData={'DelaySeconds' : 10}
		appClient.publishDeviceCommand("myDeviceType","device01", "reboot", "json", myData);

		appClient.disconnect();
	});
```


## Referência
{: #reference_nodejs}

A tabela a seguir descreve os parâmetros que são usados nas funções descritas nesta documentação do Node.js:

|Parâmetro|Tipo de Dados|Descrição|
|:---|:---|
|`deviceType`|Seqüência de caracteres|O tipo de dispositivo. Normalmente, o deviceType é um agrupamento de dispositivos que executam uma tarefa específica, por exemplo, "weatherballoon".|
|`deviceId`|Seqüência de caracteres|O ID do dispositivo. Normalmente, para um tipo de dispositivo especificado, o deviceId é um identificador exclusivo desse dispositivo, por exemplo, um número de série ou um endereço de Controle de Acesso à Mídia.|
|`eventType`|Seqüência de caracteres|Um grupo de eventos específicos, por exemplo "status", "warning" e "data".|
|`format`|Seqüência de caracteres|O formato pode ser qualquer sequência, por exemplo, JSON.  |
|`data`|Dicionário|Os dados para a carga útil da mensagem. O comprimento máximo é 131072 bytes.|
|`payload`|Seqüência de caracteres|Os dados para a carga útil da mensagem. O comprimento máximo é 131072 bytes.|
|`topic`|Seqüência de caracteres|Ao publicar como um dispositivo, a sequência de tópicos não inclui o tipo de dispositivo ou o ID do dispositivo; estes são obtidos do identificador de cliente.  Por exemplo, `iot-2/evt/event_id/fmt/format_string`.  Ao publicar como um aplicativo ou gateway em nome de um dispositivo, o tópico deve incluir o tipo de dispositivo e o ID do dispositivo.  Por exemplo, `iot-2/type/device_type/id/device_id/evt/event_id/fmt/format_string`.|
