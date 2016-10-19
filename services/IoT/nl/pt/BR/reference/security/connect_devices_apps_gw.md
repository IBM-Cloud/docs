---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Conexões de aplicativos, dispositivos e gateways com o {{site.data.keyword.iot_short_notm}}
{: #connect_devices_apps_gw}
Última atualização: 08 de setembro de 2016
{: .last-updated}

Aplicativos, dispositivos e gateways podem se conectar ao {{site.data.keyword.iot_full}} por meio do protocolo MQTT. Os dispositivos também podem se conectar e publicar eventos no {{site.data.keyword.iot_short_notm}} por meio da API (interface de programação de aplicativos) HTTP (Protocolo de Transporte de Hipertexto).
{: shortdesc}


## URLs de conexão do cliente
{: #client_connect_url}

Para conectar clientes de dispositivo, aplicativo e gateway à sua instância do {{site.data.keyword.iot_short_notm}}, use as URLs (Localizadores Uniformes de Recursos) de conexão a seguir:

### Endereço do sistema de mensagens

<pre class="pre"><var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com</pre>
{: codeblock}

### URL (Localizador Uniforme de Recursos) de conexão da API (interface de programação de aplicativos) REST HTTP (Protocolo de Transporte de Hipertexto)

<pre class="pre">https://<var class="keyword varname">orgId</var>.internetofthings.ibmcloud.com/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**Notas**
- *orgId* é o ID da organização exclusivo que foi gerado quando você registrou a instância de serviço.
- Se você estiver conectando um dispositivo ou aplicativo ao serviço de iniciação rápida, especifique 'quickstart' como o valor de *orgId*.

## Segurança de porta
{: #client_port_security}

Assegure que as portas necessárias estejam abertas e ativadas para comunicação.

|Tipo de conexão |Número da porta|
|:---|:---|
|Não Protegido|1883|
|Protegido|8883|
|Protegido|443|

Os clientes MQTT se conectam usando credenciais apropriadas, como tokens de autenticação de dispositivo para dispositivos e chaves API (interface de programação de aplicativos) e tokens para aplicativos. Como o sistema de mensagens MQTT para a porta não segura 1883 envia essas credenciais em texto simples, sempre use as alternativas seguras 8883 ou 443 em seu lugar. As portas seguras forçam a criptografia das credenciais de TLS (Segurança da Camada de Transporte). Esteja ciente de que deve-se ativar TLS (Segurança da Camada de Transporte) no aplicativo usando o método tls_set() na biblioteca Python MQTT. Caso contrário, os dados poderão ser enviados de forma não segura.

Ao proteger o sistema de mensagens MQTT nas portas 8883 ou 443, bibliotecas do cliente mais novas confiam automaticamente no certificado que é apresentado pelo {{site.data.keyword.iot_short_notm}}. Se esse não for o caso para seu ambiente do cliente, será possível fazer download e usar a cadeia de certificados integral de [messaging.pem](https://github.com/ibm-messaging/iot-python/blob/master/src/ibmiotf/messaging.pem).


## Requisito do TLS
{: #tls_requirements}
Algumas bibliotecas do cliente de Segurança da Camada de Transporte (TLS) não suportam domínios que incluem um curinga. Se não for possível mudar as bibliotecas com sucesso, desative a verificação de certificado.

O {{site.data.keyword.iot_short_notm}} requer TLS V1.2 e os conjuntos de criptografia a seguir:
- ECDHE-RSA-AES256-GCM-SHA384
- AES256-GCM-SHA384
- ECDHE-RSA-AES128-GCM-SHA256
- AES128-GCM-SHA256

## Autenticação de cliente MQTT
{: #mqtt_authentication}

**Importante:** cada cliente MQTT requer um ID de cliente exclusivo. Se você tentar conectar um cliente em sua organização usando um ID de cliente que já está conectado, a primeira conexão será desfeita.

Dispositivos e gateways conectados diretamente ao {{site.data.keyword.iot_short_notm}} exibem um ícone de status no painel para indicar que estão conectados. Os dispositivos conectados indiretamente por meio de um gateway são mostrados como desconectados porque o painel não está ciente de dispositivos conectados por meio de um gateway.

### Identificadores de cliente MQTT

Para que dispositivos, aplicativos e gateways serem autenticados com sucesso, defina cada cliente MQTT usando os identificadores de cliente e formato a seguir:

|Tipo de Cliente |ID|Formato do ID MQTT|
|:---|:---|:---|
|Aplicativos|a|<pre class="pre">a:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|Aplicativos Escaláveis|x|<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|Dispositivos|d|<pre class="pre">d:<var class="keyword varname">orgId</var>:<var class="keyword varname">deviceType</var>:<var class="keyword varname">deviceId</var></pre>|
|Gateways|h|<pre class="pre">g:<var class="keyword varname">orgId</var>:<var class="keyword varname">typeId</var>:<var class="keyword varname">deviceId</var></pre>|

Em que
- *orgId* é o ID da organização exclusivo de seis caracteres que foi gerado quando você registrou o serviço.
- *appId* é um identificador de sequência exclusivo definido pelo usuário para o cliente.
- *deviceId* identifica exclusivamente um dispositivo ou gateway entre todos os tipos e é análogo a um número de série.
- *device_type* é o identificador para o tipo de dispositivo que está se conectando e é análogo a um número de modelo.
- *typeId* é um identificador do tipo de gateway que está se conectando e é análogo a um número de modelo.

Os valores de *appId*, *type_id*, *device_type* e *device_id* devem ter no máximo 36 caracteres e podem conter somente:
- Caracteres alfanuméricos (a-z, A-Z, 0-9)
- Traços (-)
- Sublinhados (_)
- Pontos (.)

**Notas:**
- Ao se conectar ao serviço de iniciação rápida, autenticação não é necessária.
- Você não precisa registrar um aplicativo antes de se conectar.


### Conectando aplicativos usando MQTT

Aplicativos do {{site.data.keyword.iot_short_notm}} requerem a chave API (interface de programação de aplicativos) para se conectarem a uma organização. Quando uma chave API (interface de programação de aplicativos) é registrada, um token é gerado e ele deve ser usado com essa chave API.

O código a seguir fornece um exemplo de uma chave API (interface de programação de aplicativos):

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}

O exemplo a seguir mostra um token de autenticação típico:

```
 MP$08VKz!8rXwnR-Q*
```

Ao fazer uma conexão MQTT usando uma chave API (interface de programação de aplicativos), assegure que os requisitos a seguir sejam atendidos:

- O ID do cliente MQTT está no formato a seguir: a:*orgId*:*appId*
- O nome do usuário MQTT é a chave API (interface de programação de aplicativos), por exemplo, a-*orgId*-a84ps90Ajs
- A senha MQTT é o token de autenticação, por exemplo, *MP$08VKz!8rXwnR-Q*

Para obter mais informações, consulte [Conectividade MQTT para aplicativos](../../applications/mqtt.html).

### Autenticação do Dispositivo

#### Nome
do Usuário
O serviço do {{site.data.keyword.iot_short_notm}} suporta apenas autenticação baseada em token para dispositivos; portanto, cada dispositivo tem apenas um nome de usuário válido.
Um valor igual a `use-token-auth` indica ao serviço que o token de autenticação para o gateway ou dispositivo é usado como a senha para a conexão MQTT.

Para obter mais informações, consulte [Conectividade MQTT para dispositivos](../../devices/mqtt.html)

#### senhas
Se o cliente estiver usando autenticação baseada em token, envie o token de autenticação do dispositivo como a senha para todas as conexões MQTT.
