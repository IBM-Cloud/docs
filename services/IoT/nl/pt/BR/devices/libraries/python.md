---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-10-27"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Python para desenvolvedores de dispositivos
{: #python}

É possível usar Python para construir e desenvolver código de dispositivo para interagir com sua organização no {{site.data.keyword.iot_full}}. O cliente Python para o {{site.data.keyword.iot_short_notm}} fornece uma API (interface de programação de aplicativos) para facilitar interação simples com recursos do {{site.data.keyword.iot_short_notm}} abstraindo os protocolos subjacentes, como MQTT e HTTP (Protocolo de Transporte de Hipertexto).
{:shortdesc}

Use as informações e exemplos que são fornecidos para iniciar o desenvolvimento de seus dispositivos usando Python.

## Fazendo download de cliente e recursos do Python
{: #python_client_download}

Para acessar o cliente Python para o {{site.data.keyword.iot_short_notm}} e outros recursos disponíveis, acesse o repositório [iot-python](https://github.com/ibm-watson-iot/iot-python) no GitHub e conclua as instruções de instalação.

## Construtor
{: #constructor}

O dicionário de opções cria definições que são usadas para interagir com o módulo do {{site.data.keyword.iot_short_notm}}. O construtor cria a instância do cliente e aceita o dicionário de opções que contém as definições a seguir:

|Definição|Descrição |
|:---|:---|
|`orgId`|O ID de sua organização.|
|`type`|O tipo do dispositivo. O tipo de dispositivo é um agrupamento para dispositivos que executam uma tarefa específica, por exemplo, "weatherballoon".|
|`id`|Um ID exclusivo para identificar um dispositivo. Geralmente, para um tipo de dispositivo especificado, o ID do dispositivo é um identificador exclusivo desse dispositivo, por exemplo, um número de série ou endereço MAC.|
|`auth-method`|O método de autenticação. O único método que é suportado é `apikey`.|
|`auth-token`|Um token de chave API que também é necessário ao configurar o valor de método de autenticação para `apikey`.|
|`clean-session`|Um valor true ou false necessário somente se você desejar se conectar ao aplicativo no modo de assinatura durável. Por padrão, `clean-session` é configurado como true.|

Se nenhum dicionário de opções for fornecido, o cliente conecta-se ao serviço de iniciação rápida do {{site.data.keyword.iot_short_notm}} como um dispositivo não registrado.

```python

import ibmiotf.device
try:
  options = {
    "org": orgId,
    "type": deviceType,
    "id": deviceId,
    "auth-method": authMethod,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### Usando um arquivo de configuração

Em vez de definir um dicionário de opções diretamente, também é possível definir um dicionário de opções separadamente em um arquivo de configuração, conforme esboçado na amostra de código a seguir:

```python

import ibmiotf.device
try:
  options = ibmiotf.device.ParseConfigFile(configFilePath)
  client = ibmiotf.device.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

O arquivo de configuração que contém o dicionário de opções deve estar no formato a seguir:

```python

[device]
org=orgID
type=deviceType
id=deviceId
auth-method=token
auth-token=token
clean-session=true/false
```

## Publicando eventos
{: #publishing_events}

Eventos são o mecanismo pelo qual os dispositivos publicam dados no {{site.data.keyword.iot_short_notm}}. O dispositivo controla o conteúdo do evento e designa um nome para cada evento que ele envia.

Quando um evento é recebido pela instância do {{site.data.keyword.iot_short_notm}}, as credenciais do evento recebido identificam o dispositivo de envio, o que significa que um dispositivo não pode personificar outro dispositivo.

Os eventos podem ser publicados com qualquer um dos três níveis de qualidade de serviço (QoS) definidos pelo protocolo MQTT.  Por padrão, os eventos são publicados com um nível de QoS (qualidade de serviço) `0`.

### Publicar um evento usando a qualidade de serviço padrão

```
client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData)
```

### Aumentando o nível de QoS (qualidade de serviço) para um evento

É possível aumentar o [nível de qualidade de serviço (QoS)](../../reference/mqtt/index.html#qos-levels) para eventos publicados. Eventos que têm um nível de QoS (qualidade de serviço) superior a `0` podem levar mais tempo para publicar devido às informações de recebimento de confirmação adicionais incluídas.

**Nota:** o modo de fluxo de iniciação rápida suporta apenas um nível de QoS (qualidade de serviço) igual a `0`.

```
client.connect()
myQosLevel=2
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent("status", "json", myData, myQosLevel)
```
## Manipulando comandos
{: #handling_commands}

Quando o cliente do dispositivo se conecta, ele assina automaticamente qualquer comando especificado para este dispositivo. Para processar comandos específicos, você precisa registrar um método de retorno de chamada de comando. As mensagens são retornadas como uma instância da classe de comandos que contém as propriedades a seguir:

|Propriedade|Tipo de Dados|Descrição|
|:---|:---|
|`command`|Seqüência de caracteres|Identifica o comando.|
|`format`|Seqüência de caracteres|O formato pode ser qualquer sequência, por exemplo, JSON.|
|`data`|Dicionário|Os dados para a carga útil. O comprimento máximo é 131072 bytes.|
|`timestamp`|Date and time|A data e hora do evento.|


```python

def myCommandCallback(cmd):
  print("Command received: %s" % cmd.data)
  if cmd.command == "setInterval":
    if 'interval' not in cmd.data:
      print("Error - command is missing required information: 'interval'")
    else:
      interval = cmd.data['interval']
  elif cmd.command == "print":
    if 'message' not in cmd.data:
      print("Error - command is missing required information: 'message'")
    else:
      print(cmd.data['message'])

...
client.connect()
client.commandCallback = myCommandCallback
```

## Suporte ao formato de mensagem personalizada
{: #custom_message_format}

Por padrão, o formato da mensagem está configurado como `json`, o que significa que a biblioteca suporta a codificação e a decodificação de objetos do dicionário Python no formato JSON. Quando o formato da mensagem é configurado como `json-iotf`, a mensagem é codificada em conformidade com a especificação de carga útil JSON do {{site.data.keyword.iot_short_notm}}. Para incluir suporte para seus próprios formatos de mensagem customizados, consulte a [Amostra do Formato de mensagem customizado](https://github.com/ibm-watson-iot/iot-python/tree/master/samples/customMessageFormat) no GitHub.

Ao criar um módulo codificador customizado, deve-se registrá-lo no cliente do dispositivo conforme esboçado no exemplo a seguir:

```python

import myCustomCodec

client.setMessageEncoderModule("custom", myCustomCodec)
client.publishEvent("status", "custom", myData)
```
Se um evento for enviado em um formato desconhecido ou se um dispositivo não reconhecer o formato, a biblioteca de dispositivo retorna uma condição `MissingMessageDecoderException`.
