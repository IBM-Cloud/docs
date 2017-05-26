---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-07"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# APIs de REST HTTP para dispositivos de gateway
{: #api_link}


Para acessar a documentação da API de REST HTTP do {{site.data.keyword.iot_short_notm}} e localizar mais informações sobre como criar, atualizar, excluir e listar dispositivos, veja [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html).

A única versão da API (interface de programação de aplicativos) REST HTTP (Protocolo de Transporte de Hipertexto) do {{site.data.keyword.iot_short_notm}} suportada é a versão 2. Assegure que suas soluções {{site.data.keyword.iot_short_notm}} estejam usando a versão 2.

## Conexões do cliente
{: #client_connections}

Para obter informações sobre a segurança do cliente e como conectar clientes a dispositivos de gateway no {{site.data.keyword.iot_short_notm}}, veja [Conectando aplicativos, dispositivos e gateways ao {{site.data.keyword.iot_short_notm}}](../reference/security/connect_devices_apps_gw.html).


### Authentication

Todas as solicitações devem incluir um cabeçalho de autorização. Autenticação Básica é o único método suportado. Quando um dispositivo faz uma solicitação de HTTP usando a API de REST HTTP do {{site.data.keyword.iot_short_notm}}, as credenciais a seguir são necessárias:

|Credencial|Entrada requerida|
|:---|:---|
|User name| `g/{orgId}/{gwType}/{gwDevId}`
|Password| O token de autenticação que era gerado automaticamente ou especificado manualmente quando você registrava o dispositivo de gateway.

em
que:

<dl>
<dt>orgId</dt>  
<dd>O nome da organização, que deve corresponder ao nome especificado no cabeçalho do host.</dd>

<p></p>
<dt>gwType</dt>  
<dd>O tipo de gateway. </dd>
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

## Último cache de eventos
{: #last-event-cache}

Usando a API (interface de programação de aplicativos) de cache do último evento do {{site.data.keyword.iot_short_notm}}, é possível recuperar o último evento que foi enviado por um dispositivo. Essa API funcionará estando o dispositivo on-line ou off-line, permitindo recuperar o status do dispositivo independentemente de sua localização física ou do status de uso. É possível recuperar o último valor registrado de um ID de evento para um dispositivo específico ou o último valor registrado para cada ID do evento que foi relatado por um dispositivo específico. Os dados do último evento de um dispositivo podem ser recuperados para qualquer evento específico que tenha ocorrido há até 365 dias.

Para solicitar o valor mais recente para um ID de evento específico, use a solicitação de API a seguir, que retornará o último valor registrado para o ID de evento "energia":

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events/power
```

A resposta é retornada no formato JSON a seguir:

```
{
    "deviceId": "<device-id>",
    "eventId": "power",
    "format": "json",
    "payload": "eyJzdGF0ZSI6Im9uIn0=",
    "timestamp": "2016-03-14T14:12:06.527+0000",
    "typeId": "<device-type>"
}
```

**Observação:** enquanto a resposta da API está no formato JSON, cargas úteis do evento podem ser gravadas em qualquer formato. Cargas úteis retornadas pela API Last Event Cache são codificadas em base64.

Para solicitar o valor mais recente para cada ID do evento que foi relatado por um dispositivo, use a solicitação de API a seguir:

```
GET /api/v0002/device/types/<device-type>/devices/<device-id>/events
```

A resposta inclui todos os IDs de evento que foram enviados pelo dispositivo. No exemplo a seguir, os valores são retornados para os eventos “energia” e “temperatura”.

```
[
    {
        "deviceId": "<device-id>",
        "eventId": "power",
        "format": "json",
        "payload": "eyJzdGF0ZSI6Im9uIn0=",
        "timestamp": "2016-03-14T14:12:06.527+0000",
        "typeId": "<device-type>"
    },
    {
        "deviceId": "<device-id>",
        "eventId": "temperature",
        "format": "json",
        "payload": "eyJpbnRlcm5hbCI6MjIsICJleHRlcm5hbCI6MTZ9",
        "timestamp": "2016-03-14T14:17:44.891+0000",
        "typeId": "<device-type>"
    }
]
```
