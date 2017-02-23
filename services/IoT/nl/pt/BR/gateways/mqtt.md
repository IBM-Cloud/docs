---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Conectividade MQTT para gateways
{: #mqtt}

MQTT é o protocolo primário que dispositivos e aplicativos usam para se comunicar com o {{site.data.keyword.iot_full}}. As bibliotecas do cliente, informações e amostras são fornecidas para ajudá-lo a usar clientes MQTT como gateways para conectar seus dispositivos ao {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Conexões do cliente
{: #client_connections}

Para obter informações sobre segurança do cliente e como conectar clientes MQTT como gateways, consulte [Conectando aplicativos, dispositivos e gateways ao {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).

## Autenticação de MQTT
{: #authentication}
Para gateways e dispositivos, o {{site.data.keyword.iot_short_notm}} usa autenticação baseada em token MQTT.

Para ativar a autenticação MQTT, envie um nome de usuário e uma senha ao fazer uma conexão MQTT.

### User name
{: #username}

O nome do usuário é o mesmo valor para todos os gateways: `use-token-auth`. Esse valor faz com que o {{site.data.keyword.iot_short_notm}} use o token de autenticação do gateway, que é especificado como a senha.

### Password
{: #password}

A senha para cada gateway é o token de autenticação exclusivo que foi gerado quando o gateway foi registrado com o {{site.data.keyword.iot_short_notm}}.

## Publicando eventos
{: #pub_events}

Um gateway pode publicar eventos a partir dele mesmo e em nome de qualquer dispositivo conectado pelo gateway. Para publicar eventos, use o tópico a seguir e substitua `typeId` e `deviceId` apropriados com base na origem desejada do evento:

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/evt/<var class="keyword varname">eventId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}


**Exemplo**


|    |'typeID'|'deviceID'|
|:---|:---|:---|
|Gateway 1 |mygateway |gateway1 |
|Dispositivo 1 |mydevice |device1 |

-   O Gateway 1 pode publicar seus próprios eventos de status:  
    `iot-2/type/mygateway/id/gateway1/evt/status/fmt/json`
-   O Gateway 1 pode publicar eventos de status em nome do Dispositivo 1:  
    `iot-2/type/mydevice/id/device1/evt/status/fmt/json`

**Importante:** a carga útil da mensagem limita-se a no máximo 131072 bytes. Mensagens maiores que esse limite são rejeitadas.

### Mensagens retidas
As organizações do {{site.data.keyword.iot_short_notm}} não estão autorizadas a publicar mensagens MQTT retidas. Se um gateway enviar uma mensagem retida, o serviço {{site.data.keyword.iot_short_notm}} substituirá a sinalização de mensagem retida quando ela estiver configurada como true e processará a mensagem como se a sinalização de mensagem retida estivesse configurada como false.

## Assinando comandos
{: #subscribing_cmds}

Um gateway pode assinar comandos que são direcionados ao próprio gateway e a qualquer dispositivo na organização, incluindo outros gateways. Para assinar comandos, use o tópico a seguir e substitua por `typeId` e `deviceId` apropriados:

<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/cmd/<var class="keyword varname">commandId</var>/fmt/<var class="keyword varname">formatString</var></pre>
{: codeblock}

O curinga MQTT `+` pode ser usado para `typeId`, `deviceId`, `commandId` e `formatString` para assinar diversas fontes de comandos.

**Exemplo:**

|Dispositivo |`typeId`|`deviceId`|
|:---|:---|
|Gateway 1| mygateway   | gateway1   |
|Dispositivo 1 | mydevice    | device1    |


-   O Gateway 1 pode assinar comandos direcionados no gateway:  
    `iot-2/type/mygateway/id/gateway1/cmd/+/fmt/+`
-   O Gateway 1 pode assinar comandos enviados ao Dispositivo 1:  
    `iot-2/type/mydevice/id/device1/cmd/+/fmt/+`
-   O Gateway 1 pode assinar qualquer comando enviado a dispositivos do tipo `mydevice`:  
     `iot-2/type/mydevice/id/+/cmd/+/fmt/+`

**Importante:** sessões persistentes MQTT especificadas como `cleansession=false` não procuram dispositivos que se conectam a gateways. Se um dispositivo se conectar ao gateway A e depois se conectar ao gateway B, ele não receberá nenhuma mensagem publicada no gateway A para o dispositivo enquanto ele estava desconectado. Um gateway é proprietário do cliente MQTT e da assinatura, mas não dos dispositivos conectados ao gateway.

## Registro automático do gateway
{: #auto-reg}

Dispositivos de gateway podem registrar automaticamente dispositivos conectados a eles. Quando um gateway publica uma mensagem ou assina um tópico em nome de um dispositivo não registrado, esse dispositivo será registrado automaticamente.

As solicitações de registro dos dispositivos de gateway são reguladas para 128 solicitações pendentes por vez. Tentar conectar muitos novos dispositivos pode causar um atraso no registro dos dispositivos por meio do gateway.

**Aviso**

Se o gateway falhar ao registrar um dispositivo automaticamente, ele não tentará registrar esse dispositivo novamente por um curto tempo. Quaisquer mensagens ou assinaturas do dispositivo com falha serão descartadas durante esse tempo.

## Notificações do gateway
{: #notification}

Quando ocorrem erros durante a validação do tópico de publicação ou assinatura ou durante o registro automático, uma notificação é enviada ao dispositivo de gateway. Um gateway pode receber essas notificações assinando o tópico a seguir, substituindo os valores de `typeId` e `deviceId`:

```
iot-2/type/**typeId**/id/**deviceId**/notify
```
<pre class="pre">iot-2/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/notify</pre>
{: codeblock}

Mensagens recebidas no tópico de notificação usam o formato a seguir:

```   
{
   "Request": "<Request_Type>",
   "Time": "<Timestamp>",
   "Topic": "<Topic>",
   "Type": "<Device_Type>",
   "Id": "<Device_Id>",
   "Client": "<Client_ID>",
   "RC": "<Return_Code>",
   "Message": "<Message>"
}
```
Em que
-   Os valores de `Request_Type` são `publish` ou `subscribe`
-   `Timestamp` é o horário no formato ISO 8601
-   `Topic` é o tópico de solicitação do gateway
-   `Device_Type` é o tipo de dispositivo do tópico
-   `Device_Id` é o ID do dispositivo do tópico
-   `Client_ID` é o identificador de cliente da solicitação
-   `Return_Code` é o código de retorno
-   `Message` é a mensagem de erro

Um gateway pode receber as notificações a seguir:

-   O tópico não corresponde a nenhuma regra de tópico permitida.
-   O tipo de dispositivo não é válido.
-   O ID do dispositivo não é válido.
-   O número máximo de dispositivos por gateway foi atingido.
-   O número máximo de dispositivos por organização foi atingido.
-   Falha ao criar o dispositivo devido a erros internos.

## Gateways gerenciados
{: #managed_gateways}

Suporte para gerenciamento de ciclo de vida de dispositivo é opcional. O protocolo de gerenciamento de dispositivo usado pelo {{site.data.keyword.iot_short_notm}} usa a mesma conexão MQTT que o gateway usa para eventos e controle de comando.

### Níveis de qualidade de serviço e sessão limpa
{: #quality_service}

Os gateways gerenciados podem publicar mensagens que tenham um nível de qualidade de serviço (QoS) 0 ou 1.

As mensagens com QoS=0 podem ser descartadas e não persistem após a reinicialização do servidor de sistema de mensagens. As mensagens com QoS=1 podem ser enfileiradas e persistem após a reinicialização do servidor de sistema de mensagens. A durabilidade da assinatura determina se uma solicitação será enfileirada. O parâmetro `cleansession` da conexão que fez a assinatura determina a durabilidade da assinatura.  

O {{site.data.keyword.iot_short_notm}} publica solicitações que têm um nível de QoS (qualidade de serviço) igual a 1 para suportar o enfileiramento de mensagens. Para enfileirar mensagens enviadas enquanto um gateway gerenciado não está conectado, configure o dispositivo para não usar sessões limpas, configurando o parâmetro `cleansession` como false.

**Aviso**

Quando um gateway gerenciado usa uma assinatura durável, comandos de gerenciamento de dispositivo que são enviados ao gateway enquanto ele está off-line são relatados como operações com falha se o gateway não se reconectar ao serviço antes que a solicitação atinja o tempo limite. Quando o gateway se reconectar, essas solicitações serão processadas pelo gateway. Assinaturas duráveis são especificadas pelo parâmetro `cleansession=false`.

O gateway é proprietário da sessão MQTT, independentemente dos dispositivos que estão por trás dela. Quando um dispositivo envia uma solicitação de assinatura por meio de um gateway, a solicitação não se move para outros gateways, independentemente de se a opção `cleansession=false` está configurada.

### Tópicos
{: #topics}

Um gateway gerenciado deve assinar os tópicos a seguir para manipular solicitações e respostas do {{site.data.keyword.iot_short_notm}}:

-   O gateway gerenciado assina respostas de gerenciamento de dispositivo em:  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/+</pre>
{: codeblock}
-   O gateway gerenciado assina solicitações de gerenciamento de dispositivo em:  
<pre class="pre">iotdm-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/+</pre>
{: codeblock}

Um gateway gerenciado publica as respostas e solicitações a seguir:

- Respostas de gerenciamento de dispositivo são publicadas em:  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/response/</pre>
{: codeblock}
- Solicitações de gerenciamento de dispositivo são publicadas em:  
<pre class="pre">iotdevice-1/type/<var class="keyword varname">typeId</var>/id/<var class="keyword varname">deviceId</var>/</pre>
{: codeblock}

O gateway pode processar mensagens do Protocolo de gerenciamento de dispositivo para ele mesmo e em nome de outros dispositivos conectados usando **typeId** e **deviceId** relevantes.

### Formato da Mensagem
{: #msg_format}

Todas as mensagens são enviadas no formato JSON.

**Solicitações**

Solicitações são formatadas conforme mostrado na amostra de código a seguir:

```   
    {  "d": {...}, "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056" }
```

-   `d` transporta qualquer dado relevante para a solicitação
-   `reqId` é um identificador da solicitação e deve ser copiado para uma resposta. Se uma resposta não for necessária, o campo não será usado.

**Respostas**

Respostas são formatadas conforme mostrado na amostra de código a seguir:

```
    {
        "rc": 0,
        "message": "success",
        "d": {...},
        "reqId": "b53eb43e-401c-453c-b8f5-94b73290c056"
    }
```
Em que:
-   `rc` é um código de resultado da solicitação original.
-   `message` é um elemento opcional com uma descrição de texto do código de resposta.
-   `d` é um elemento de dados opcional que acompanha a resposta.
-   `reqId` é o ID da solicitação original. O ID da solicitação é usado para correlacionar respostas com solicitações e o dispositivo precisa assegurar que todos os IDs de solicitação sejam exclusivos. Respostas a solicitações do {{site.data.keyword.iot_short_notm}} devem conter o valor de `reqId` correto.
