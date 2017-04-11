---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Conectividade MQTT para dispositivos
{: #mqtt}

MQTT é o protocolo primário que dispositivos e aplicativos usam para se comunicar com o {{site.data.keyword.iot_full}}. Bibliotecas do cliente, informações e amostras são fornecidas para ajudá-lo a conectar e integrar seus dispositivos com o {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Conexões do cliente
{: #client_connections}

Para obter informações sobre segurança do cliente e como conectar clientes MQTT a dispositivos no {{site.data.keyword.iot_short_notm}}, consulte [Conectando aplicativos, dispositivos e gateways ao {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).


## Conectando dispositivos ao serviço de iniciação rápida
{: #connecting_devices}

O serviço de iniciação rápida é o nível de serviço mais rápido. Ele não oferece confirmação de recebimento e não suporta níveis de qualidade de serviço (QoS) MQTT maiores que zero. Ao se conectar ao serviço de iniciação rápida, autenticação ou registro não é necessário e o `orgId` deve estar configurado como `quickstart`.

Se você estiver escrevendo código de dispositivo para ser usado com iniciação rápida, esteja ciente de que os recursos de serviço a seguir do {{site.data.keyword.iot_short_notm}} não são suportados no modo de iniciação rápida:

-  Assinando comandos
-  Protocolo de Gerenciamento de Dispositivo
-  Sessões limpas ou duráveis

**Importante:** mensagens que são enviadas de dispositivos a uma taxa maior que uma por segundo podem ser descartadas.


## Autenticação de MQTT
{: #mqtt_authentication}

Para gateways e dispositivos, o {{site.data.keyword.iot_short_notm}} usa autenticação baseada em token MQTT.

Para ativar a autenticação MQTT, envie um nome de usuário e uma senha ao fazer uma conexão MQTT.

### User name

O nome do usuário é o mesmo valor para todos os dispositivos: `use-token-auth`. Esse valor faz com que o {{site.data.keyword.iot_short_notm}} use o token de autenticação do dispositivo, que é especificado como a senha.

### Password

A senha para cada dispositivo é o token de autenticação exclusivo que foi gerado quando o dispositivo foi registrado com o {{site.data.keyword.iot_short_notm}}.

## Publicando eventos
{: #publishing_events}

Os dispositivos publicam nos tópicos de eventos no formato a seguir:

<pre class="pre">iot-2/evt/<var class="keyword varname">event_id</var>/fmt/<var class="keyword varname">format_string</var></pre>
{: codeblock}

Em que

-  **event_id** é o ID do evento, por exemplo `status`.  O ID de evento pode ser qualquer sequência válida em MQTT. Se caracteres curinga não forem usados, os aplicativos de assinante devem usar essa sequência em seu tópico de assinatura para receber os eventos que são publicados em seu tópico.
-  **format_string** é uma sequência que define o tipo de conteúdo da carga útil da mensagem, de modo que o receptor da mensagem pode determinar como analisar o conteúdo. Os valores de tipo de conteúdo comuns incluem, mas não estão limitados a "json", "xml", "txt" e "csv". O valor pode ser qualquer sequência válida em MQTT.

**Importante:** a carga útil da mensagem limita-se a no máximo 131072 bytes. Mensagens maiores que esse limite são rejeitadas.

### Mensagens retidas
As organizações do {{site.data.keyword.iot_short_notm}} não estão autorizadas a publicar mensagens MQTT retidas. Se um dispositivo enviar uma mensagem retida, o serviço {{site.data.keyword.iot_short_notm}} substituirá a sinalização de mensagem retida quando ela estiver configurada como true e processará a mensagem como se a sinalização de mensagem retida estivesse configurada como false.


## Assinando comandos
{: #subscribing_to_commands}

Os dispositivos podem assinar tópicos de comando no formato a seguir:

<pre class="pre">iot-2/cmd/<var class="keyword varname">command_id</var>/fmt/<var class="keyword varname">format_string</var></pre>
{: codeblock}

Em que
 - **command_id** é o ID do comando, por exemplo, `update`. O ID do comando pode ser qualquer sequência válida no protocolo MQTT.  Se caracteres curinga não forem usados, um dispositivo deverá usar essa sequência em seu tópico de assinatura para receber comandos que são publicados em seu tópico.
 - **format_string** é uma sequência que define o tipo de conteúdo da carga útil de comando, de modo que o receptor do comando pode determinar como analisar o conteúdo. Os valores de tipo de conteúdo comuns incluem, mas não estão limitados a "json", "xml", "txt" e "csv". O valor pode ser qualquer sequência válida em MQTT.

Os dispositivos não podem assinar eventos de outros dispositivos. Um dispositivo recebe comandos que são publicados apenas em seu próprio dispositivo.

## Dispositivos gerenciados
{: #managed-devices}

Suporte para gerenciamento de ciclo de vida de dispositivo é opcional. O Protocolo de gerenciamento de dispositivo usa a mesma conexão MQTT que seu dispositivo já usa para eventos e controle de comando.

### Níveis de qualidade de serviço e sessão limpa

Os dispositivos gerenciados podem publicar mensagens que tenham um nível de qualidade de serviço (QoS) 0 ou 1.

As mensagens com QoS=0 podem ser descartadas e não persistem após a reinicialização do servidor de sistema de mensagens. As mensagens com QoS=1 podem ser enfileiradas e persistem após a reinicialização do servidor de sistema de mensagens. A durabilidade da assinatura determina se uma solicitação será enfileirada. O parâmetro `cleansession` da conexão que fez a assinatura determina a durabilidade da assinatura.  

O {{site.data.keyword.iot_short_notm}} publica solicitações que têm um nível de QoS (qualidade de serviço) igual a 1 para suportar o enfileiramento de mensagens. Para enfileirar mensagens enviadas enquanto um dispositivo gerenciado não está conectado, configure o dispositivo para não usar sessões limpas, configurando o parâmetro `cleansession` como false.

**Aviso:**
se o seu dispositivo gerenciado usar uma assinatura durável, qualquer comando que for enviado para seu dispositivo enquanto ele estiver off-line será relatado como operação com falha se o dispositivo não se reconectar ao serviço antes de o tempo da solicitação ser atingido. No entanto, quando o dispositivo se reconectar, essas solicitações serão processadas pelo dispositivo. Uma assinatura durável é especificada pelo parâmetro `cleansession=false`.

### Tópicos

Um dispositivo gerenciado é necessário para assinar o tópico a seguir para manipular solicitações e respostas do serviço do {{site.data.keyword.iot_short_notm}}:

```
iotdm-1/#
```


Um dispositivo gerenciado publica em tópicos que são específicos do tipo de solicitação de gerenciamento que está sendo executada:

- O dispositivo gerenciado publica respostas de gerenciamento de dispositivo em `iotdevice-1/response`.
- Para outros tópicos nos quais um dispositivo gerenciado pode publicar, consulte [Protocolo de gerenciamento de dispositivo](device_mgmt/index.html) e [Solicitações de gerenciamento de dispositivo](device_mgmt/requests.html).



### Formato da Mensagem

Todas as mensagens são enviadas no formato JSON.

**Solicitações**  
Solicitações são formatadas conforme mostrado na amostra de código a seguir:

<pre class="pre">{  "d": {...}, "<var class="keyword varname">reqId</var>": "b53eb43e-401c-453c-b8f5-94b73290c056" }</pre>
{: codeblock}

Em que:

 - **d** transporta qualquer dado relevante para a solicitação.
 - **reqId** é um identificador da solicitação e deve ser copiado para uma resposta. Se uma resposta não for necessária, será possível omitir o campo *reqId*.

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
 - **rc** é um código de resultado da solicitação original.
 - **message** é um elemento opcional com uma descrição de texto do código de resposta.
 - **d** é um elemento de dados opcional que acompanha a resposta.
 - **reqId** é o ID da solicitação original, que é usado para correlacionar respostas com solicitações. O dispositivo deve assegurar que todos os IDs de solicitação sejam exclusivos. Respostas a solicitações do {{site.data.keyword.iot_short_notm}} devem incluir o valor de **reqId** correto.

Para obter mais informações sobre mensagens de solicitação e resposta específicas, consulte [Protocolo de gerenciamento de dispositivo](device_mgmt/index.html) e [Solicitações de gerenciamento de dispositivo](device_mgmt/requests.html).
