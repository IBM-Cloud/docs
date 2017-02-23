---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-07-28"

---

  {:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# ﻿C# para desenvolvedor de aplicativos
{: #c_sharp}


É possível usar o C# para construir e customizar aplicativos que interagem com sua organização no {{site.data.keyword.iot_full}}. Use as informações e os exemplos fornecidos para iniciar o desenvolvimento de seus aplicativos usando o C#.
{:shortdesc}

## Fazendo download de cliente e recursos de C#
{: #csharp_client_download}

Para acessar as bibliotecas do cliente C# e as amostras para o {{site.data.keyword.iot_short_notm}}, acesse o repositório [iot-csharp](https://github.com/ibm-watson-iot/iot-csharp) no GitHub e conclua as instruções de instalação.


## Construtor
{: #constructor}

O construtor cria a instância do cliente e aceita argumentos que contêm as definições a seguir:

|Definição |Descrição |
|:---|:---|
|`orgId`   |O ID de sua organização.|
|`appId`   |O ID exclusivo de um aplicativo em sua organização.|
|`auth-key`   |Uma chave API (interface de programação de aplicativos) para conectar seu aplicativo de forma segura ao Watson IoT Platform|
|`auth-token`   |Um token de chave API (interface de programação de aplicativos) para conectar seu aplicativo de forma segura ao Watson IoT Platform.|

Se `appId` for o único argumento fornecido, o cliente se conecta ao serviço de iniciação rápida do {{site.data.keyword.iot_short_notm}} como um dispositivo não registrado. A lista de argumentos define como o cliente se conecta ao módulo do {{site.data.keyword.iot_short_notm}}.

```
ApplicationClient applicationClient = new ApplicationClient(orgId, appId, apiKey, authToken);
applicationClient.connect();
```


## Assinando eventos de dispositivo
{: #subscribe_device_events}

Os dispositivos usam eventos para publicar dados na instância do {{site.data.keyword.iot_short_notm}}. O dispositivo controla o conteúdo do evento e designa um nome para cada evento que envia.

Quando um evento é recebido pela instância do {{site.data.keyword.iot_short_notm}}, as credenciais do evento recebido identificam o dispositivo de envio, o que significa que um dispositivo não pode personificar outro dispositivo.

Por padrão, os aplicativos assinam todos os eventos de todos os dispositivos conectados. Use os parâmetros tipo de dispositivo, ID do dispositivo, evento e formato da mensagem para controlar o escopo da assinatura. As amostras de código a seguir mostram como é possível definir o escopo de uma assinatura usando esses parâmetros:

### Assinando todos os eventos de todos os dispositivos

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents();
```

### Assinando todos os eventos de todos os dispositivos de um tipo específico

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType);
```

### Assinando um evento específico de todos os dispositivos

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(evt);
```

###  Assinando um evento específico de dois ou mais dispositivos diferentes:

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt);
```

### Assinando todos os eventos publicados no formato JSON

```
applicationClient.connect();
applicationClient.subscribeToDeviceEvents(deviceType, deviceId, evt, "json", 0);
```

**Nota**: uma única instância do cliente pode suportar diversas assinaturas.

### Manipulando eventos a partir de dispositivos

Para processar eventos que são recebidos por suas assinaturas, registre um método de retorno de chamada de evento conforme mostrado no exemplo a seguir:

```
public static void processEvent(String eventName, string eventFormat, string eventData) {
// Do something
}
applicationClient.connect();
applicationClient.eventCallback += processEvent;
applicationClient.subscribeToDeviceEvents();
```
A tabela a seguir descreve os parâmetros do método de retorno de chamada de evento:

|Parâmetro|Tipo de Dados|Descrição|
|:---|:---|
|`eventName`|Seqüência de caracteres|Identifica o evento. |
|`eventFormat`|Seqüência de caracteres| O formato pode ser qualquer sequência, por exemplo, JSON.|
|`eventData`|Dicionário| Os dados para a carga útil da mensagem. O comprimento máximo é 131072 bytes.|


## Assinando status do dispositivo
{: #subscribe_device_status}

Por padrão, a assinatura está configurada para receber atualizações de status para todos os dispositivos conectados. Use os parâmetros tipo de dispositivo e ID do dispositivo para controlar o escopo da assinatura. As amostras de código a seguir mostram como é possível definir o escopo de uma assinatura usando esses parâmetros:

### Assinando atualizações de status para todos os dispositivos

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus();
```

### Assinando atualizações de status para dois dispositivos diferentes

```
applicationClient.connect();
applicationClient.subscribeToDeviceStatus += processDeviceStatus;
applicationClient.subscribeToDeviceStatus(deviceType, deviceId);
```

**Nota**: uma única instância do cliente pode suportar diversas assinaturas.

### Manipulando atualizações de status a partir de dispositivos

Para processar as atualizações de status recebidas por suas assinaturas, registre um método de retorno de chamada de evento conforme mostrado no exemplo a seguir:

```
public static void processDeviceStatus(String deviceType, string deviceId, string data)
        {
           //
        }
applicationClient.connect();
applicationClient.appStatusCallback += processAppStatus;
applicationClient.subscribeToApplicationStatus();
```

## Publicando eventos a partir de dispositivos
{: #publish_events_devices}

Os aplicativos podem publicar eventos como se eles tivessem originado de um dispositivo.

```
applicationClient.connect();
applicationClient.publishEvent(deviceType, deviceId, evt, data, 0);

```

A tabela a seguir descreve os parâmetros que são especificados no método `publishEvent()`:

|Parâmetro|Tipo de Dados|Descrição|
|:---|:---|
|`deviceType`|Seqüência de caracteres| O tipo de dispositivo. Normalmente, o deviceType é um agrupamento de dispositivos que executam uma tarefa específica, por exemplo, "weatherballoon".|
|`deviceId`|Seqüência de caracteres| O ID do dispositivo. Normalmente, para um tipo de dispositivo especificado, o deviceId é um identificador exclusivo desse dispositivo, por exemplo, um número de série ou um endereço de Controle de Acesso à Mídia.|
|`evt`|Seqüência de caracteres| O nome do servidor.|
|`format`|Seqüência de caracteres| O formato pode ser qualquer sequência, por exemplo, JSON.|
|`data`|Dicionário| Os dados para a carga útil da mensagem. O comprimento máximo é 131072 bytes.|
|`QoS`|Integer| A qualidade de serviço. Os valores válidos são `0`, `1`, `2`. |


## Publicando comandos para dispositivos
{: #publish_commands_devices}

Os aplicativos podem publicar comandos para dispositivos conectados.

```
applicationClient.connect();
applicationClient.publishCommand(deviceType, deviceId, "testcmd", "json", data, 0);
```
A tabela a seguir descreve os parâmetros que são especificados no método `publishCommand()`:

|Parâmetro|Tipo de Dados|Descrição|
|:---|:---|
|`deviceType`|Seqüência de caracteres| O tipo de dispositivo. Normalmente, o deviceType é um agrupamento de dispositivos que executam uma tarefa específica, por exemplo, "weatherballoon".|
|`deviceId`|Seqüência de caracteres| O ID do dispositivo. Normalmente, para um tipo de dispositivo especificado, o deviceId é um identificador exclusivo desse dispositivo, por exemplo, um número de série ou um endereço de Controle de Acesso à Mídia.|
|`command`|Seqüência de caracteres| O nome do comando.|
|`format`|Seqüência de caracteres| O formato pode ser qualquer sequência, por exemplo, JSON.|
|`data`|Dicionário| Os dados para a carga útil da mensagem. O comprimento máximo é 131072 bytes.|
|`QoS`|Integer| A qualidade de serviço. Os valores válidos são `0`, `1`, `2`. |
