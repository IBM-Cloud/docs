---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# ﻿C# para desenvolvedor de dispositivo
{: #c_sharp}

É possível usar o C# para construir e customizar dispositivos que interagem com sua organização no {{site.data.keyword.iot_full}}. Use as informações e os exemplos fornecidos para iniciar o desenvolvimento de seus dispositivos usando o C#.
{:shortdesc}

## Fazendo download de cliente e recursos de C#
{: #csharp_client_download}

Para acessar o cliente C# e os recursos do {{site.data.keyword.iot_short_notm}}, acesse o repositório [iot-csharp ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-watson-iot/iot-csharp){: new_window} no GitHub e conclua as instruções de instalação.


## Construtor
{: #constructor}

O construtor cria a instância do cliente e aceita argumentos que contêm as definições a seguir:

|Definição |Descrição |
|:---|:---|
|`orgId`|O ID de sua organização.|
|`deviceType`|O tipo de seu dispositivo.|
|`deviceId` |O ID de seu dispositivo.|
|`auth-method`   |O método de autenticação a ser usado. O único valor atualmente suportado é `token`.|
|`auth-token`   |Um token de autenticação para conectar seu dispositivo de forma segura ao Watson IoT Platform.|


Se `deviceId` e `deviceType` forem os únicos argumentos fornecidos, o cliente se conecta ao serviço de iniciação rápida do {{site.data.keyword.iot_short_notm}} como um dispositivo não registado. A lista de argumentos define como o cliente se conecta ao módulo do {{site.data.keyword.iot_short_notm}}.


```
namespace com.ibm.iotf.client

public DeviceClient(string orgId, string deviceType, string deviceID, string auth-method, string auth-token)
        : base(orgId, "d" + CLIENT_ID_DELIMITER + orgId + CLIENT_ID_DELIMITER + deviceType + CLIENT_ID_DELIMITER + deviceID, "use-token-auth", auth-token)
    {

    }
```

## Publicando eventos
{: #publishing-events}

Os dispositivos usam eventos para publicar dados na instância do {{site.data.keyword.iot_short_notm}}. O dispositivo controla o conteúdo do evento e designa um nome para cada evento que envia.

Quando um evento é recebido pela instância do {{site.data.keyword.iot_short_notm}}, as credenciais do evento recebido identificam o dispositivo de envio, o que significa que um dispositivo não pode personificar outro dispositivo.

Eventos podem ser publicados em qualquer um dos três [níveis de qualidade de serviço (QoS)](../mqtt.html#managed-devices) definidos pelo protocolo MQTT. Por padrão, os eventos são publicados em QoS 0.


## Publicando um evento usando o nível padrão de qualidade de serviço
{: #publish_event_default_qos}

```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}");
```


## Publicando um evento usando um nível de qualidade de serviço definido pelo usuário
{: #publish_event_user_qos}

Eventos publicados em um nível de QoS (qualidade de serviço) MQTT maior que `0` incluem informações de confirmação de recebimento adicionais e podem demorar mais tempo para publicação do que eventos com nível de QoS igual a `0`.


```
deviceClient.connect();
deviceClient.publishEvent("event", "json", "{temp:23}", 2);
```

## Manipulando comandos
{: #handling_commands}

Quando um cliente do dispositivo se conecta, ele assina automaticamente quaisquer comandos desse dispositivo. Para processar comandos específicos, deve-se registrar um método de retorno de chamada de comando, conforme mostrado no exemplo a seguir:

```
public static void processCommand(string cmdName, string cmdFormat, string cmdData) {
...
 }
```

```
deviceClient.connect();
deviceClient.commandCallback += processCommand;
```
A tabela a seguir descreve os parâmetros do método commandCallback:

|Parâmetro|Tipo de Dados|Descrição|
|:---|:---|
|`cmdName`|Seqüência de caracteres|Identifica o comando. |
|`cmdFormat`|Seqüência de caracteres|O formato pode ser qualquer sequência, por exemplo, JSON.|
|`cmdData`|Dicionário|Os dados para a carga útil. O comprimento máximo é 131072 bytes.|
