---

copyright:
  years: 2016, 2017
lastupdated: "2016-12-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

# Controle de acesso ao gateway (BETA)

**Importante**: esse recurso está disponível atualmente como parte de um beta limitado.

Os dispositivos de gateway são autorizados a agir em nome de outros dispositivos. Os grupos de recursos de gateway definem em nome de quais dispositivos de uma organização cada gateway pode agir. Os gateways podem ser designados à função *Gateway padrão*. Os gateways padrão só podem publicar ou assinar mensagens em nome de dispositivos em seu grupo de recursos.
{: #shortdesc}


## Designando uma função a um gateway

A designação de uma função a um gateway é obrigatória para que o gateway tenha um grupo de recursos. Os gateways sem um grupo de recursos podem agir em nome de todos os dispositivos na organização. A designação da função *Gateway padrão* cria automaticamente um novo grupo de recursos para o gateway. Quando um gateway é designado a um grupo de recursos, ele só pode agir em nome dos dispositivos desse grupo de recursos e de si mesmo, mesmo se a sua função for mudada.

Para designar uma função a um gateway, use a API a seguir:

```
PUT /authorization/devices/{deviceId}/roles
```

Para obter detalhes do esquema de solicitação, veja a [documentação da API do {{site.data.keyword.iot_full}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/put_authorization_devices_deviceId_roles).

## Incluindo dispositivos e removendo dispositivos de um grupo de recursos

Antes que um gateway com a função *Gateway padrão* possa agir em nome de um dispositivo, o dispositivo deve ser um membro do grupo de recursos designado ao gateway. Para incluir vários dispositivos em um grupo de recursos ao mesmo tempo, use a API a seguir:

```
 PUT /bulk/devices/{groupId}/add
```

O grupo no qual incluir dispositivos deve ser especificado no caminho da solicitação e os dispositivos a serem incluídos devem ser especificados no corpo da solicitação. Para obter mais informações sobre o esquema de solicitação e as respostas, veja a [documentação da API do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/put_bulk_devices_groupId_add).

Para remover múltiplos dispositivos de um grupo de recursos, use a API a seguir:

```
PUT /bulk/devices/{groupId}/remove
```

Os dispositivos especificados no corpo da solicitação serão removidos do grupo especificado no caminho da solicitação. Para obter mais informações sobre o esquema de solicitação e a resposta, veja a [documentação da API do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/put_bulk_devices_groupId_remove).

## Localizando um grupo de recursos

Os grupos de recursos podem ter tags de procura associadas. As tags de procura podem ser usadas para recuperar os detalhes de um grupo de recursos usando a API a seguir:

```
GET /groups
```

Essa API retorna os grupos de recursos associados à tag de procura usada. Se nenhuma tag de procura for especificada, todos os grupos de recursos serão retornados. <!-- For more information about the request schema, response, and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

O ID de um grupo de recursos pode ser localizado usando a API a seguir:

```
GET /authorization/devices/{deviceId}
```

Essa API retorna o identificador exclusivo dos grupos de recursos dos quais esse dispositivo é um membro. Mais informações sobre essa API podem ser localizadas na [documentação da API do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/get_authorization_devices_deviceId).

## Consultando um grupo de recursos

Os grupos de recursos podem ser consultados dentro de vários parâmetros para retornar as propriedades completas de todos os dispositivos no grupo, os identificadores exclusivos de todos os dispositivos no grupo ou as propriedades do grupo de recursos.

Para retornar as propriedades completas de todos os dispositivos no grupo de recursos especificado, use a API a seguir:

```
GET /bulk/devices/{groupId}
```

Essa API retorna a lista de propriedades completas para todos os membros do grupo de recursos especificado. Para obter mais informações sobre o esquema de solicitação, respostas e como paginar pelos resultados, veja a [documentação da API do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/limited-gateway.html#!/Limited_Gateway/get_bulk_devices_groupId).

Para retornar somente os identificadores exclusivos dos membros do grupo de recursos, use a API a seguir:

```
GET /bulk/devices/{groupId}/ids
```

Essa API retorna os identificadores exclusivos de todos os dispositivos que são membros do grupo de recursos. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Para retornar as propriedades do grupo de recursos, use a API a seguir:

```
GET /groups/{groupId}
```

Essa API retorna as propriedades do grupo de recursos (nome, descrição, tags de procura e identificador exclusivo) especificado no caminho, mas não retorna a lista de membros do grupo de recursos. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Criando e excluindo um grupo de recursos.

Os grupos de recursos podem ser criados e excluídos independentemente da conexão de gateways. Para criar um grupo de recursos, use a API a seguir:

```
POST /groups
```

Essa API cria um grupo de recursos e retorna os detalhes do grupo. <!-- For details on the request schema and the responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Para excluir um grupo de recursos, use a API a seguir:

```
DELETE /groups/{groupId}
```

Essa API exclui o grupo de recursos especificado. Dispositivos que eram membros do grupo são removidos do grupo, mas os próprios dispositivos não são afetados de qualquer outra forma. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Atualizando propriedades do grupo



  - /groups/{groupId}
    - PUT: atualiza as propriedades do grupo especificado.

## Recuperando e atualizando propriedades do dispositivo.

Há várias maneiras de recuperar propriedades do dispositivo usando a API; cada API retorna informações diferentes. Para recuperar as propriedades de dispositivo de todos os dispositivos conectados à sua organização do {{site.data.keyword.iot_short_notm}}, use a API a seguir:

```
GET /authorization/devices:

```

Essa API retorna as propriedades de todos os dispositivos conectados à organização, incluindo suas propriedades relevantes de controle de acesso (função, status, data de expiração). <!-- For more information on responses and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Para recuperar propriedades do dispositivo sem recuperar as informações relevantes de controle de acesso, use a API a seguir:

```
GET /authorization/devices/{deviceId}
```

Essa API retorna todas as propriedades de dispositivo do dispositivo especificado sem retornar as informações de controle de acesso. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} device model documentation](LINK TO DEVICE MODEL) and [API documentation](LINK TO CORRECT API). -->

Para recuperar as informações de controle de acesso de um dispositivo específico, use a API a seguir:

```
GET /authorization/devices/{deviceId}/roles:
```

Essa API recupera as informações relevantes de controle de acesso para o dispositivo especificado sem retornar outras propriedades de dispositivo. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

As propriedades do dispositivo podem ser atualizadas de duas maneiras. As propriedades podem ser atualizadas sem mudar as propriedades de controle de acesso ou as propriedades de controle de acesso podem ser atualizadas diretamente.

Para atualizar propriedades do dispositivo sem afetar as propriedades de controle de acesso, use a API a seguir:

```
PUT /authorization/devices/{deviceId}
```

Essa API só atualizará propriedades do dispositivo que não estiverem associadas ao controle de acesso. <!-- For more information on request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Para atualizar somente as propriedades de controle de acesso do dispositivo especificado, use a API a seguir:

```
PUT /authorization/devices/{deviceId}/withroles:
```

Essa API somente atualizará as propriedades de controle de acesso do dispositivo especificado. <!-- For more information on the request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->
