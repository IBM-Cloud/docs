---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-21"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# APIs do sistema de mensagens HTTP para dispositivos de gateway (Beta)
{: #api}

**Importante:** o recurso API HTTP do {{site.data.keyword.iot_full}} para dispositivos de gateway está disponível apenas como parte de um programa beta limitado. Atualizações futuras podem incluir mudanças incompatíveis com a versão atual desse recurso. Experimente e [informe-nos o que acha ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://developer.ibm.com/answers/smart-spaces/17/internet-of-things.html){: new_window}.

## Acessando a documentação da API de sistema de mensagens HTTP para dispositivos de gateway
{: #rest_messaging_api}

Para acessar a documentação da API de sistema de mensagens HTTP do {{site.data.keyword.iot_short_notm}} e localizar mais informações sobre o envio de eventos usando dispositivos de gateway, veja [API de sistema de mensagens HTTP do {{site.data.keyword.iot_short_notm}} ![Ícone de link externo](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/http-messaging.html){: new_window}.


## Conexões do cliente
{: #client_connections}

Para obter informações sobre a segurança do cliente e como conectar clientes a dispositivos de gateway no {{site.data.keyword.iot_short_notm}}, veja [Conectando aplicativos, dispositivos e gateways ao {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).


## Publicando eventos
{: #event_publication}

Além de usar o protocolo de sistema de mensagens MQTT, também é possível configurar seus dispositivos de gateway para publicar eventos no {{site.data.keyword.iot_short_notm}} sobre HTTP usando comandos da API de sistema de mensagens HTTP.

Para enviar uma solicitação de `POST` de um dispositivo que está conectado ao {{site.data.keyword.iot_short_notm}}, use uma das URLs a seguir:

### Solicitação de POST não segura
<pre class="pre"><code class="hljs">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

### Solicitação de POST segura
<pre class="pre"><code class="hljs">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></code></pre>

**Notas importantes:**
- É possível enviar eventos de dispositivo de gateway apenas usando o sistema de mensagens HTTP. Use o protocolo de sistema de mensagens MQTT para enviar solicitações para outros recursos de gerenciamento de dispositivo de gateway e controle.
- Porta 443, a porta SSL padrão, também pode ser especificada para proteger as chamadas API HTTP.
- Se um gateway não estiver designado à função *Gateway padrão*, ele poderá publicar eventos em nome de qualquer dispositivo na organização. Se o dispositivo que está conectado ao gateway não estiver registrado, o gateway registrará esse dispositivo automaticamente.
- Designe a função *Gateway padrão* se você desejar verificar os níveis de autorização do dispositivo.

Para obter mais informações sobre a função de gateways e grupos de recursos, veja [Controle de acesso ao gateway (Beta)](../gateways/gateway-access-control.html).

### Authentication

Todas as solicitações devem incluir um cabeçalho de autorização. Autenticação Básica é o único método suportado. Quando um dispositivo faz uma solicitação de HTTP usando a API de REST HTTP do {{site.data.keyword.iot_short_notm}}, as credenciais a seguir são necessárias:

|Credencial|Entrada requerida|
|:---|:---|
|User name| `g/{orgId}/{gwType}/{gwDevId}` ou `g-{orgId}-{gwType}-{gwDevId}`
|Password| O token de autenticação que era gerado automaticamente ou especificado manualmente quando você registrava o dispositivo de gateway.

Em que:

<dl>
<dt>orgId</dt>  
<dd>O nome da organização, que deve corresponder ao nome especificado no cabeçalho do host.</dd>

<p></p>
<dt>gwType</dt>  
<dd>O tipo de gateway. </dd>
<dd>Se você usar o caractere hífen "-" como um delimitador no nome de usuário, esse valor não deverá incluir um caractere de hífen. </dd>
<p></p>
<dt>gwDevId</dt>  
<dd>O identificador de dispositivo de gateway. </dd>
</dl>


### Cabeçalhos de solicitação Content-Type

Um cabeçalho de solicitação `Content-Type` deve ser fornecido com a solicitação. A tabela a seguir mostra como os tipos suportados são mapeados para os formatos internos do {{site.data.keyword.iot_short_notm}}:

|cabeçalho Content-Type|Formato no {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|texto/simples|"texto"
|aplicativo/json| "json"
|aplicativo/xml | "xml"
|application/octet-stream|"bin"

### Qualidade de Serviço

Semelhante ao nível 0 de serviço de entrega de qualidade de serviço MQTT "no máximo uma vez", o sistema de mensagens REST HTTP fornece entrega de mensagem não persistente, mas valida se a solicitação está correta e se pode ser entregue ao servidor antes de enviar a resposta HTTP. Uma resposta que contém um código de status HTTP 200 confirma que a mensagem foi entregue ao servidor. Ao usar o nível de qualidade de serviço MQTT "no máximo uma vez" ou o equivalente de HTTP (Protocolo de Transporte de Hipertexto) para entregar mensagens de eventos, o dispositivo ou o aplicativo deve implementar a lógica de nova tentativa para garantir a entrega.

Para obter mais informações sobre o protocolo MQTT e os níveis de qualidade de serviço para o {{site.data.keyword.iot_short_notm}}, consulte [Sistema de mensagens MQTT](../reference/mqtt/index.html).

Para obter mais informações sobre como gerenciar dispositivos de gateway usando APIs, veja [APIs de REST HTTP para dispositivos de gateway](../gateways/gw_api.html).
