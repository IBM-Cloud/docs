---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Dispositivos e fornecedores suportados
{: #supportedcloud}

O {{site.data.keyword.iotinsurance_full}} suporta integração com vários fornecedores de nuvem e dispositivos.
{: shortdesc}

## Dispositivos suportados por fornecedor
{: #supportedvendors}
A tabela a seguir lista os fornecedores e dispositivos que são suportados pelo
{{site.data.keyword.iotinsurance_short}} e descreve o tipo de integração. Os tipos
de integração a seguir estão disponíveis:

  - **{{site.data.keyword.iot_short_notm}}** - o dispositivo
ou hub publica os eventos de sensor diretamente no {{site.data.keyword.iot_short_notm}}. O {{site.data.keyword.iotinsurance_short}} pode processar os eventos de sensor diretamente ou depois que o {{site.data.keyword.iotinsurance_short}} Transformer os modifica levemente.

  - **Nuvem para nuvem** - o dispositivo ou hub publica os eventos de sensor em uma nuvem de terceiros. O {{site.data.keyword.iotinsurance_short}} Transformer lê os eventos da nuvem de terceiros e os publica no {{site.data.keyword.iot_short_notm}}.

<table>
<thead>
<tr>
<th>Nome do Fornecedor</th>
<th>Tipo de integração</th>
<th>Dispositivos testados</th>
<th>Informações de fornecedor </th>
</tr>
</thead>
<tbody>
<tr>
<td>Bosch E-Call</td>
<td>{{site.data.keyword.iot_short_notm}}.  
Um app de gateway foi escrito para testar a integração.</td>
<td>Bosch Retrofit E-Call</td>
<td>[Website do fornecedor ![Ícone de link externo](../../icons/launch-glyph.svg)](http://www.bosch-connectivity.com/en/what_we_offer/products_and_solutions_1/retrofit_ecall/connected_devices_3){: new_window}</td>
</tr>
<tr>
<td>EnOcean</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>Botão</li>
<li>Contato</li>
<li>Temperatura</li>
</ul>
</td>
<td>[Website do fornecedor ![Ícone de link externo](../../icons/launch-glyph.svg)](https://www.enocean.com/en/</td>){: new_window}
</tr>
<tr>
<td>WiButler (iExergy)</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>Detector de fumaça</li>
<li>Botão</li></td>
</ul>
<td>[Website do fornecedor ![Ícone de link externo](../../icons/launch-glyph.svg)](https://www.wibutler.com/en_GB){: new_window}</td>
</tr>
<tr>
<td>Wink</td>
<td>Nuvem para nuvem</td>
<td>Vazamento de água</td>
<td>[Website do fornecedor ![Ícone de link externo](../../icons/launch-glyph.svg)](https://www.wink.com/){: new_window}</td>
</tr>
<tr>
<td>Yanzi</td>
<td>{{site.data.keyword.iot_short_notm}} e Nuvem para nuvem</td>
<td>Nenhum sensor foi testado.</td>
<td>[Website do fornecedor ![Ícone de link externo](../../icons/launch-glyph.svg)](https://ibm.ent.box.com/notes/126680846739){: new_window}</td>
</tr>
</tbody>
</table>

## Integrando dispositivos e nuvens do fornecedor
{: #integratingdevices}
É possível integrar seus dispositivos e as nuvens do fornecedor com o {{site.data.keyword.iotinsurance_short}}. As seções a seguir fornecem procedimentos de
integração e registros do usuário de amostra para cada fornecedor.

Para obter mais informações sobre a integração de sensores e dispositivos, veja
[Kit de ferramentas do dispositivo](iotinsurance_device_toolkit.html):


### EnOcean
#### Procedimento de integração
  1. Crie um gateway na instância do {{site.data.keyword.iot_short_notm}} que está conectada ao {{site.data.keyword.iotinsurance_short}}.
  2. Conecte o hub EnOcean ao gateway {{site.data.keyword.iot_short_notm}}.
  3. Inclua o identificador do gateway ao registro do usuário no {{site.data.keyword.iotinsurance_short}}.

#### Registro do usuário de amostra

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "digital-concepts-gateway1"
    ],
    ...
}
```

### WiButler (iExergy)

#### Procedimento de integração
A integração com os dados do WiButler atualmente é suportada somente como uma prova de
conceito ou como uma visualização técnica e não é destinada para uso de produção. O hardware WiButler requer uma atualização de firmware para transmitir dados para o {{site.data.keyword.iot_short_notm}}.

#### Registro do usuário de amostra

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "Wibutler-Gateway-ID"
    ],
    ...
}
```

### Wink

#### Procedimento de integração

**Opção 1**
  1. Obtenha os [tokens de autorização do Wink ![Ícone de link externo](../../icons/launch-glyph.svg)](http://docs.winkapiv2.apiary.io/#){: new_window}.
  2. Inclua o token de autorização ao usuário correspondente no sistema
{{site.data.keyword.iotinsurance_short}} usando a API
{{site.data.keyword.iotinsurance_short}}.

**Opção 2**  
Integre usando o app móvel (descontinuado). Esse método funciona somente com a versão 1.0 do {{site.data.keyword.iotinsurance_short}}.

#### Registro do usuário de amostra

```
{
  "username": "user@example.com",
  "password": "",
  ....
  "deviceID": "528DB5CA-7F3D-4478-A4EB-994E7F118B6B",
  "assets": [
    {
      "name": "default",
      "providers": [
        {
          "name": "wink",
          "tokens": {
            "data": {
              "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
              "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
              "token_type": "bearer",
              "token_endpoint": "https://api.wink.com/oauth2/token",
              "scopes": "full_access"
            },
            "errors": [],
            "pagination": {},
            "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
            "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
            "token_type": "bearer",
            "token_endpoint": "https://api.wink.com/oauth2/token",
            "scopes": "full_access"
          }
        }
      ]
    }
  ]
}

```

### Yanzi
#### Procedimento de integração
**Opção 1**  
  Inclua credenciais da nuvem Yanzi ao yanzi-config.json no diretório do fornecedor do
repositório do Transformer.  O objeto "yanziCloud" é o local correto das credenciais.  

**Opção 2**  
  O Yanzi usa uma integração de nuvem para nuvem entre a nuvem Yanzi e o
{{site.data.keyword.iot_short_notm}}. A autorização para essa integração ocorre dentro
da nuvem Yanzi. Após a conclusão da autorização, a nuvem Yanzi envia eventos para o
{{site.data.keyword.iot_short_notm}}. Deve-se incluir também as credenciais da instância
do {{site.data.keyword.iot_short_notm}} ao yanzi-config.json no diretório do fornecedor
do repositório do Transformer, usando o objeto "iotfCredentials".

#### Registro do usuário de amostra

```
{
  "yanziCloud": {
      "cirrusHost": "wss://",
      "username": "",
      "password": "",
      "locationId": "",
      "unitDid": ""
  },
  "iotfCredentials": {
      "org": "",
      "apiKey": "",
      "apiToken": "",
      "type": "shared",
      "mqtt_host": "gbdprt.messaging.internetofthings.ibmcloud.com",
      "domain": "internetofthings.ibmcloud.com"
  }
}
```

### Dados do Weather Company
#### Procedimento de integração
A integração com os dados do Weather Company atualmente é suportada somente como uma prova
de conceito ou como uma visualização técnica e não é destinada para uso de produção.

Forneça um endereço para recuperar as condições de clima atuais (temperatura externa) do Weather Company para um local específico.



#### Registro do usuário de amostra

```
{ "username": "johndoe",
   "fullname": "John Doe",
    "firstname": "John",
    "lastname": "Doe",
    "password": "",
     "accessLevel": 13,
     "address": "Mies-van-der-Rohe-Straße 6, 80807 München, Germany",
     ...
}

```
