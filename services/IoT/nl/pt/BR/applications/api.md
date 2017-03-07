---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-02-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# API REST HTTP para aplicativos
{: #api}

Use a API (interface de programação de aplicativos) REST HTTP (Protocolo de Transporte de Hipertexto) do {{site.data.keyword.iot_full}} para construir e customizar aplicativos que interagem com sua organização no {{site.data.keyword.iot_short_notm}}.
{:shortdesc}

## Recursos
{: #capabilities}

A API (interface de programação de aplicativos) REST HTTP (Protocolo de Transporte de Hipertexto) do {{site.data.keyword.iot_short_notm}} suporta os recursos e funções a seguir para aplicativos:

- Recuperação de informações da organização
- Operações em massa do dispositivo (listar, incluir e remover)
- Operações do tipo de dispositivo (listar, criar, excluir, visualizar detalhes e atualizar)
- Operações do dispositivo (listar, incluir, remover, visualizar detalhes, atualizar, visualizar local e visualizar informações de gerenciamento)
- Operações de diagnóstico do dispositivo (limpar logs, recuperar logs, incluir informação de log, excluir logs, obter logs específicos, limpar códigos de erro, obter códigos de erro do dispositivo e incluir códigos de erro)
- Determinação de problema da conexão (listar eventos de log da conexão de dispositivo)
- Cache do último evento (visualizar o último evento para um dispositivo específico)
- Operações de solicitação de gerenciamento de dispositivo (listar solicitações de gerenciamento de dispositivo, iniciar solicitações, limpar status da solicitação, obter detalhes de uma solicitação, listar todos os status das solicitações por dispositivo e obter o status da solicitação para um dispositivo específico)
- Operações de gerenciamento de uso (recuperar a quantia total de dados usados)
- Publicação de eventos de dispositivo (beta)
- Consulta do status de serviço (recuperar status de serviços por organização)

## Acessando a documentação da API de REST HTTP
{: #api_link}

Para acessar a documentação da API de REST HTTP do {{site.data.keyword.iot_short_notm}} e obter mais informações sobre como construir e customizar seus aplicativos, acesse a URL a seguir:  [https://docs.internetofthings.ibmcloud.com/swagger/v0002.html](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html)

A única versão da API (interface de programação de aplicativos) REST HTTP (Protocolo de Transporte de Hipertexto) do {{site.data.keyword.iot_short_notm}} suportada é a versão 2. Assegure que suas soluções {{site.data.keyword.iot_short_notm}} estejam usando a versão 2.

# API (interface de programação de aplicativos) do sistema de mensagens REST HTTP (Protocolo de Transporte de Hipertexto) para aplicativos
{: #rest_messaging_api}

## Publicando eventos e comandos
{: #event_command_publication}

Além de usar o protocolo de sistema de mensagens MQTT, também é possível configurar seus aplicativos para publicar eventos e comandos no {{site.data.keyword.iot_short_notm}} por HTTP (Protocolo de Transporte de Hipertexto) usando um dos comandos a seguir da API (interface de programação de aplicativos) REST HTTP (Protocolo de Transporte de Hipertexto):

### Solicitação de POST de evento não segura
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Solicitação de POST de evento segura
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**Nota:** porta 443, a porta SSL padrão, também pode ser especificada para proteger as chamadas API HTTP.

### Solicitação de POST de comando não segura
<pre class="pre">http://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:1883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></pre>
{: codeblock}

### Solicitação de POST de comando segura
<pre class="pre">https://<var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com:8883/api/v0002/application/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/commands/<var class="keyword varname">eventId</var></pre>
{: codeblock}

Se você estiver conectando um dispositivo ou aplicativo ao serviço de iniciação rápida, substitua **orgId** pela sequência 'quickstart'.

**Notas:**
- Embora os aplicativos possam reutilizar uma conexão HTTP para postar eventos ou comandos em dispositivos diferentes, o cabeçalho de HTTP de autorização não pode ser mudado.
- Porta 443, a porta SSL padrão, também pode ser especificada para proteger as chamadas API HTTP.

### Authentication

Todas as solicitações devem incluir um cabeçalho de autorização. Autenticação Básica é o único método suportado. Os aplicativos são autenticados usando chaves API (interface de programação de aplicativos). Quando um aplicativo faz qualquer solicitação por meio da API (interface de programação de aplicativos) REST HTTP (Protocolo de Transporte de Hipertexto) do {{site.data.keyword.iot_short_notm}}, as credenciais a seguir são necessárias:

```
username = API key (for example, a-orgId-a84ps90Ajs)
password = Authentication token
```

### Cabeçalhos de solicitação Content-Type

Um cabeçalho de solicitação `Content-Type` deve ser fornecido com a solicitação. A tabela a seguir mostra como os tipos suportados são mapeados para os formatos internos do{{site.data.keyword.iot_short_notm}}.

|cabeçalho Content-Type|Formato no {{site.data.keyword.iot_short_notm}}|
|:---|:---|
|texto/simples|"texto"
|aplicativo/json| "json"
|aplicativo/xml | "xml"
|application/octet-stream|"bin"

### Qualidade de Serviço

Semelhante ao nível 0 de serviço de entrega de qualidade de serviço MQTT "no máximo uma vez", o sistema de mensagens REST HTTP (Protocolo de Transporte de Hipertexto) fornece entrega de mensagem não persistente, mas valida se a solicitação está correta e se pode ser entregue ao servidor antes de enviar a resposta HTTP. Uma resposta que contém um código de status HTTP (Protocolo de Transporte de Hipertexto) 200 confirma que a mensagem foi entregue ao servidor. Ao usar o nível de qualidade de serviço MQTT "no máximo uma vez" ou o equivalente de HTTP (Protocolo de Transporte de Hipertexto) para entregar mensagens de eventos, o dispositivo ou o aplicativo deve implementar a lógica de nova tentativa para garantir a entrega.


Para obter mais informações sobre o protocolo MQTT e os níveis de qualidade de serviço para o {{site.data.keyword.iot_short_notm}}, consulte [Sistema de mensagens MQTT](../reference/mqtt/index.html).
